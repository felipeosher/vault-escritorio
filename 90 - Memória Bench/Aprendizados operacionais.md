# Aprendizados operacionais

## 2026-06-22 — Incidente Claude/claudemax: API key desativada

- Sintoma: respostas falhando quando o modelo selecionado era Claude/claudemax.
- Diagnóstico nos logs: rota `anthropic/*` retornando 401 `authentication_error` com mensagem `API key disabled`.
- O perfil `anthropic:claude-cli` existia como alternativa, mas o OAuth estava expirado desde 2026-06-21.
- Mitigação aplicada: padrão temporário do OpenClaw alterado para `codex/gpt-5.5`; fallback reduzido para `google/gemini-2.5-flash`; gateway reiniciado manualmente porque systemd user não está instalado nesta VPS.
- Para restaurar Claude como padrão: reativar/renovar a chave claudemax ou renovar Claude CLI OAuth, testar, e só então voltar o primary para `anthropic/claude-opus-4.8`.

Pontos importantes que o Bench descobriu junto com o Felipe. Atualizo conforme aprendemos.

## Google Workspace via `gog` (2026-06-21)
- A conta `felipebenchaya@gmail.com` está conectada via OAuth com escopos `calendar, gmail, tasks`. As credenciais vieram no backup do OpenClaw managed antigo e **funcionam normalmente** nesta VPS — a desconfiança de que não migrariam não se confirmou.
- Ferramenta: `gog` (gogcli), v0.29.0. Binário em `/data/.local/bin/gog`.
- Em shell não-interativo, o keyring precisa de senha. Ela está em `/data/.config/gogcli/keyring.env` (`GOG_KEYRING_PASSWORD`). Carregar esse env antes de rodar `gog`, senão dá erro de "no TTY available for keyring".
- Sempre passar `--account felipebenchaya@gmail.com` (ou `GOG_ACCOUNT`).

### Listas do Google Tasks
- `Felipe's list` (principal)
- `Lista de demandas continuas`
- `Trabalho` (profissional/jurídico)
- `Lei da atração`

## Google Keep NÃO funciona (2026-06-21)
- A API do Keep é **Workspace-only**: exige conta Google Workspace (empresarial) + service account.
- Conta do Felipe é Gmail pessoal, então o Keep **não pode** ser controlado por mim via API. Não é bug de config, é limitação do Google.
- Decisão: para notas/ideias no celular, usar **Obsidian mobile** (mesmo vault via Git/Sync), não o Keep.

## Espelho mobile do vault (em definição)
- Plano: ver o conteúdo do Obsidian no celular.
- Caminho escolhido: Obsidian mobile para notas/ideias + Google Tasks para ações.
- Setup detalhado do Obsidian mobile fica para 2026-06-22 (evento no calendário às 9h).

## Obsidian como memória do Bench
- O Felipe pediu que eu vá registrando aqui (Memória Bench) os pontos importantes que descobrimos juntos, não só no MEMORY.md do sistema.
- Fluxo: aprendizado relevante → anoto aqui no vault → Felipe enxerga e edita no Obsidian.

## Incidente claudemax + PDF + browser (2026-06-21)
Ver nota dedicada: [[Incidente claudemax 2026-06-21]].
- Resumo: a chave da API claudemax estava **desabilitada na memória do processo** do gateway (rodando há 19h). Hot-reload (SIGUSR1) **não** recarrega credencial — só restart real do processo resolve.
- Sintoma: tudo caía em fallback silencioso até o Gemini 2.5 Flash. Texto funcionava, mas eu *parecia* ser o Opus sem ser. PDF/visão falhava (Opus 401, Gemini Pro "unknown model", OpenAI "PDF extraction disabled").
- Lição 1: `session_status` mostra o modelo *configurado*, não o que realmente respondeu. Conferir logs de `model-fallback` para saber o modelo real.
- Lição 2: leitura de PDF confiável aqui = extrair texto com `pypdf` via `exec`, não depender do plugin `pdf` nativo (que falha no anexo `media://`).
- Lição 3: o gateway roda sob supervisor `server.mjs` (wrapper Hostinger), **não** systemd. Restart manual fora dessa árvore derruba plugins (ex.: browser) e tira o autorestart. Realinhar sob `server.mjs` (ou restart do container) conserta.
- Regra reforçada pelo Felipe: **usar o Obsidian como segundo cérebro de verdade** — gravar incidentes/decisões no vault na hora, não só no MEMORY.md.

## 2026-06-26 — Claude mudou de claudemax para claudete
- Felipe trocou a rota Anthropic/Claude do OpenClaw para `https://claudete.claudelipe.com/v1`.
- A chave foi atualizada na configuração do OpenClaw, mas não deve ser registrada no vault.
- O endpoint novo lista modelos com prefixo `xpiki/kr/`, então o catálogo Anthropic foi atualizado para IDs como `anthropic/xpiki/kr/claude-opus-4.8`, `anthropic/xpiki/kr/claude-sonnet-4.6` e `anthropic/xpiki/kr/claude-haiku-4.5`.
- Rótulos do dashboard trocados de `claudemax` para `claudete`.
- Testes confirmados: `/v1/models` retornou 200; chamadas diretas com `xpiki/kr/claude-haiku-4.5`, `xpiki/kr/claude-sonnet-4.6` e `xpiki/kr/claude-opus-4.8` retornaram 200; `openclaw agent` local e via Gateway responderam corretamente com `anthropic/xpiki/kr/claude-haiku-4.5`.
