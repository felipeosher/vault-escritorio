# Aprendizados operacionais

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
