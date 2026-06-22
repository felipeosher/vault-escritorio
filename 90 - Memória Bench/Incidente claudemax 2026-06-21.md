---
data: 2026-06-21
tipo: incidente
status: resolvido
---

# Incidente claudemax + PDF + browser (2026-06-21)

## Conexões
- [[claudemax - mercado cinza chines (RISCO)]]
- [[Aprendizados operacionais]]
- [[Decisões]]
- [[00 - Índice da Memória]]

> ⚠️ ATUALIZAÇÃO 2026-06-22: descobriu-se que o claudemax é um proxy do **mercado cinza chinês** de revenda de API Claude (fraude + data harvesting). As "chaves que morrem/precisam resetar" descritas aqui são sintoma das contas fraudulentas sendo derrubadas pela Anthropic. Ver [[claudemax - mercado cinza chines (RISCO)]].

## O que aconteceu
A API claudemax parou de responder pelo gateway, mesmo com a chave válida. Análise de PDF (inclusive pelo WhatsApp) falhava completamente. Tudo caía em fallback silencioso.

## Causa raiz (confirmada por logs + teste)
- O processo do gateway estava no ar há ~19h segurando na **memória uma chave claudemax ANTIGA, já desabilitada** no servidor.
- A chave correta (`...6e7f86`) estava no config/env e em disco, e funciona — testada via `curl` direto nos 3 modelos (opus-4.8, sonnet-4.6, haiku-4.5), todos HTTP 200.
- O gateway recebia `401 "API key disabled"` porque usava a chave velha em memória.
- Meus "restarts" anteriores foram só **SIGUSR1 (hot-reload)**: recarregam config (ex.: baseUrl) mas **NÃO recarregam a credencial** no cliente HTTP vivo.

## Cadeia de fallback observada
`opus-4.8 (401 disabled) → sonnet-4.6 (401 disabled) → gemini-2.5-flash (sucesso)`
- Resultado: respostas de texto vinham do **Gemini 2.5 Flash**, não do Opus, apesar do `session_status` dizer Opus.
- PDF/visão falhava em toda a cadeia: Opus 401, Gemini Pro "unknown model", OpenAI "PDF extraction disabled".

## Conserto que funcionou
1. Reverter a mudança de `baseUrl` (o `/v1` que eu havia adicionado era desnecessário; o problema nunca foi URL).
2. **Restart real do processo** (não hot-reload) para recarregar a chave correta.
3. Resultado: zero erros de auth desde 20:38; Opus voltou a ser o modelo real; leitura de PDF voltou.

## Efeito colateral
- O restart manual subiu o gateway **fora da árvore do supervisor `server.mjs`**, o que deixou o **plugin de browser desabilitado** e tirou o autorestart desse processo específico.
- Pendência: realinhar o gateway sob o `server.mjs` (ou restart do container) para religar o browser e restaurar resiliência.

## Lições permanentes
1. `session_status` mostra o modelo *configurado*, não o que respondeu. Para saber o modelo real, conferir logs `model-fallback/decision`.
2. Leitura de PDF confiável nesta VPS = extrair texto com **`pypdf` via exec**, não depender do plugin `pdf` nativo (falha no anexo `media://`).
3. O gateway roda sob **supervisor `server.mjs` (wrapper Hostinger)**, não systemd. Não instalar pm2/systemd — duplicaria o supervisor. Restart limpo = realinhar sob `server.mjs` ou reiniciar o container.
4. Hot-reload (SIGUSR1) não recarrega credenciais de provider. Troca/reativação de chave exige restart real do processo.

## Pendências em aberto
- [ ] Realinhar o gateway sob o `server.mjs` para religar o browser e restaurar autorestart.
- [ ] `memory_search` (embeddings OpenAI) fora por quota 429 — recarregar crédito ou trocar provider de embeddings.
- [ ] Rastrear encomenda Correios AD593614245BR (bloqueado pelo browser fora).
