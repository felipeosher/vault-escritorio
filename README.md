# Segundo Cérebro — Felipe Benchaya

Vault Obsidian que funciona como **segundo cérebro do Felipe** e **memória persistente do Bench** (agente OpenClaw).

Tudo que importa — negócios, ideias, pessoas, áreas da vida, jurídico e a memória do Bench — vive aqui, navegável no Obsidian e versionado no Git.

## Estrutura

- `00 - Entrada`: captura rápida / inbox. Tudo que ainda não foi classificado entra aqui.
- `10 - Negócios`: empreendimentos e projetos. Uma pasta por negócio.
- `20 - Escritório`: jurídico. Subpastas:
  - `01 - Processos`: uma pasta por processo.
  - `02 - Contratos`: cópia centralizada de contratos.
  - `03 - Clientes`: notas por cliente.
  - `04 - Modelos`: modelos de notas, relatórios e checklists.
- `30 - Ideias`: captura e desenvolvimento de ideias.
- `40 - Pessoas`: contatos, relacionamentos, contexto.
- `50 - Áreas da vida`: pessoal, finanças, saúde, estudos.
- `90 - Memória Bench`: memória persistente do Bench — decisões, preferências do Felipe, aprendizados e contexto entre sessões.
- `99 - Arquivo`: material encerrado / inativo.

## Como funciona o sync

- O vault mora no servidor OpenClaw e é versionado em Git (repositório privado no GitHub).
- O Bench lê e escreve notas direto no servidor e faz commit/push.
- O Felipe abre o mesmo vault no Obsidian (Windows) via plugin **Obsidian Git**, que sincroniza automaticamente.

## Observações

- A estrutura é viva: pastas e nomes podem mudar a qualquer momento sem perder histórico (Git).
- Conteúdo sensível (clientes/processos): repositório sempre **privado**.
