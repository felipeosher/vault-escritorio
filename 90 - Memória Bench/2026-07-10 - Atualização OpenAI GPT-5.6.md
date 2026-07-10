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

## Correção posterior

Felipe apontou que os modelos antigos ainda não tinham sido excluídos. Correção feita:
- Removidos do seletor configurado: `codex/gpt-5.5`, `openai/gpt-5.3-codex`, `openai/gpt-5.4`, `openai/gpt-5.4-pro`, `openai/gpt-5.5`.
- `models.mode` mudou de `merge` para `replace`, para evitar mescla automática com catálogo interno.
- Provider OpenAI declarado explicitamente com GPT-5.6 Sol/Terra/Luna.
- Catálogo embutido do plugin OpenAI ajustado em `/data/.npm-global/lib/node_modules/openclaw/dist/extensions/openai/openclaw.plugin.json`: removidos GPT 5.3/5.4/5.5; mantidos GPT-5.6 e modelos `o*`.

Backups:
- `/data/.openclaw/openclaw.json.bak-remove-old-openai-20260710-001423`
- `/data/.npm-global/lib/node_modules/openclaw/dist/extensions/openai/openclaw.plugin.json.bak-gpt56-20260710-002005`
