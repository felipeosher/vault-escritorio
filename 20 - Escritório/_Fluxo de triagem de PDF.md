# Fluxo de triagem automática de PDF

Procedimento que o Bench segue quando o Felipe envia um PDF (principalmente WhatsApp, também webchat).

## Conexões

- [[Decisões]]
- [[Analista de Processo Civil]]

## Status

- 2026-06-23: transformado em proposta formal de skill no Skill Workshop: `triagem-pdf-juridico-vault-20260623-4cbcdcf97b`.
- Modo escolhido na Aula 8: **B — skill jurídica completa**.

## Passos

1. **Ler e classificar** o documento:
   - Processo judicial / petição / decisão / sentença
   - Contrato / procuração
   - Documento de cliente
   - Outro / incerto

2. **Extrair dados-chave** conforme o tipo:
   - **Processo:** número CNJ, partes, vara/comarca, fase atual, próximos prazos.
   - **Contrato:** partes, objeto, valor, vigência, cláusulas de risco.
   - **Cliente:** nome, vínculo, contato.

3. **Guardar no vault** (sempre PDF original + nota-resumo):
   - Processo → `20 - Escritório/01 - Processos/`
   - Contrato → `20 - Escritório/02 - Contratos/`
   - Cliente novo → também referenciar em `20 - Escritório/03 - Clientes/`
   - Incerto → `00 - Entrada/` com nota pedindo definição.

4. **Criar nota-resumo** (markdown) com dados extraídos, data, origem, e link para o PDF guardado ao lado.

5. **Commit + push** no vault (Git).

6. **Responder ao Felipe:** "Guardei como [tipo] em [pasta]. Resumo: …".
   - Tipo óbvio com ação clara (ex.: prazo identificado) → já entregar análise.
   - Caso contrário → perguntar o que fazer.

7. **Análise jurídica quando couber:**
   - Processo cível completo → usar a skill `analista-processo-civil`.
   - Peça, decisão ou documento isolado → fazer análise proporcional: efeito prático, prazo aparente, risco e providência recomendada.
   - Separar fatos extraídos, inferências, riscos e sugestões para revisão humana.

## Manutenção

- Se o sync do Git ficar lento por PDFs pesados → migrar para Git LFS ou pasta de anexos separada, e avisar o Felipe.

## Convenção de nomes de nota

`AAAA-MM-DD - [Tipo] - [Identificador curto].md`
Ex.: `2026-06-21 - Processo - 0801234-56.2026 - Cliente X.md`

_Criado em 2026-06-21._
