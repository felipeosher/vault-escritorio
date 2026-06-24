# Marina modelo GPT 5.5

## Conexões

[[Decisões]]

## Registro

Em 2026-06-24, Felipe pediu para mudar a linguagem/modelo da agente Marina para GPT 5.5.

- Agente: `concierge` / Marina.
- Workspace: `/data/.openclaw/workspace-concierge`.
- Rota WhatsApp: accountId `marina`.
- Modelo anterior: `anthropic/claude-opus-4.8`.
- Modelo novo: `openai/gpt-5.5`.
- Comando aplicado: `openclaw config set agents.list.1.model openai/gpt-5.5`.
- Validação: `openclaw agents list --bindings` passou a mostrar Marina com `Model: openai/gpt-5.5`.

Observação operacional: `openclaw gateway restart` informou que o serviço systemd está desabilitado, mas `openclaw gateway status` retornou `Connectivity probe: ok` no Gateway local.
