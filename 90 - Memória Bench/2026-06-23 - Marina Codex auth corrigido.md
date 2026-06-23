# Marina - Codex auth corrigido

Data: 2026-06-23

Felipe reportou que, ao tentar usar `gpt-5.5` Codex no agente Marina, aparecia erro de limite de assinatura:

> You've reached your Codex subscription usage limit. Next reset in 5 hours, Jun 23 at 10:35 PM GMT-3.

Diagnóstico:
- A Marina e o Bench estavam usando autenticações diferentes para Codex.
- Bench: `auth_mode: chatgpt`, com OAuth da conta ChatGPT/Codex.
- Marina: `auth_mode: apikey`, com chave `sk-proj...`.
- O erro de limite vinha da credencial API da Marina, não da conta OAuth usada pelo Bench.

Correção aplicada:
- Backup preservado do `auth.json` antigo da Marina em `auth.json.bak-wrong-apikey-*`.
- Copiado o `codex-home/auth.json` do Bench para a Marina.
- Marina agora usa `auth_mode: chatgpt` e o mesmo `account_id` OAuth do Bench.

Verificação:
- Teste direto com `CODEX_HOME=/data/.openclaw/agents/concierge/agent/codex-home` e modelo `gpt-5.5` respondeu `OK_MARINA_CODEX`.
- Teste cross-agent via `sessions_send` foi bloqueado por política de visibilidade (`tools.sessions.visibility`), então a validação operacional foi feita pelo CLI Codex apontado para o home da Marina.

Observação:
- Não registrar tokens, refresh tokens, API keys ou conteúdo integral de `auth.json` em notas.
