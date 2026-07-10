# 2026-07-10 - Atualização OpenAI GPT-5.6

## Conexões
- [[Decisões]]
- [[Aprendizados operacionais]]

Felipe pediu para atualizar os modelos de linguagem da OpenAI porque agora existe GPT-5.6.

Foi confirmado em fonte oficial OpenAI em 2026-07-10 que GPT-5.6 é uma família com Sol, Terra e Luna. No API, `gpt-5.6` é alias de `gpt-5.6-sol`.

Alteração feita no OpenClaw:
- `~/.openclaw/openclaw.json` agora usa `openai/gpt-5.6` como fallback OpenAI padrão.
- O agente `concierge` também recebeu `openai/gpt-5.6` como fallback.
- O seletor/config inclui `openai/gpt-5.6`, `openai/gpt-5.6-sol`, `openai/gpt-5.6-terra` e `openai/gpt-5.6-luna`.
- Claude Opus 4.8 continua primário por preferência operacional anterior do Felipe.

Backup do config criado antes da alteração: `/data/.openclaw/openclaw.json.bak-gpt56-20260710-000931`.
