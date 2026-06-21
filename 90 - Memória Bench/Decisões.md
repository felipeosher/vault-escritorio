# Decisões

Registro de decisões combinadas entre Felipe e Bench. Ordem cronológica.

---

## 2026-06-21 — Triagem automática de PDF + regra de memória no vault

**Contexto:** Felipe quer que, ao jogar um PDF (principalmente pelo WhatsApp), o Bench classifique, guarde no Obsidian e analise/pergunte o que fazer.

**Combinado:**
- PDF chega **principalmente pelo WhatsApp** (webchat também aceito).
- **Guardar TUDO no vault**: PDF original + nota-resumo, sempre. Sem meio-termo.
- **Peso/Git:** quando o sync começar a dar problema por PDFs pesados, o Bench detecta, resolve (Git LFS ou pasta de anexos separada) e avisa o Felipe. Felipe não precisa monitorar isso.
- **Análise:** quando o tipo do documento for óbvio (ex.: achou um prazo num processo), o Bench já entrega a análise junto. Quando não for óbvio, pergunta o que fazer.
- Documento de tipo incerto → fica em `00 - Entrada/` com nota pedindo definição do Felipe.

**Regra de memória (corrigida):** o Bench passou a NÃO registrar com regularidade no vault. A partir de agora é **regra permanente**: gravar o que importa em `90 - Memória Bench/` (decisões, aprendizados, contexto) além do `MEMORY.md` do sistema. Sempre que houver decisão, evento relevante ou aprendizado, anotar aqui.

**Destino por tipo:**
- Processo judicial → `20 - Escritório/01 - Processos/`
- Contrato → `20 - Escritório/02 - Contratos/`
- Cliente novo → referência em `20 - Escritório/03 - Clientes/`
- Incerto → `00 - Entrada/`

---

## 2026-06-21 — Regra permanente: interligar notas (cliente ↔ contrato ↔ processo)

**Contexto:** Felipe perguntou se uma nota pode se conectar a outra como no Notion. Sim — o Obsidian faz isso com `[[wikilinks]]` + backlinks automáticos + grafo. É inclusive superior ao Notion nesse ponto.

**Regra permanente:** sempre que eu criar/atualizar uma nota jurídica, **interligar com wikilinks** todas as entidades relacionadas, em ambos os sentidos:
- **Processo** linka o **cliente** e o(s) **contrato(s)** envolvidos.
- **Contrato** linka o **cliente** e o(s) **processo(s)** relacionados.
- **Cliente** funciona como ficha-hub: lista e linka todos os seus processos, contratos, e demais notas.
- Usar `[[Nota#Seção]]` quando fizer sentido apontar pra um trecho específico.
- Nunca deixar uma entidade nova (cliente/contrato/processo) solta: sempre conectar à teia existente.

Objetivo: que abrir qualquer ficha (ex.: cliente) revele de cara tudo que se conecta a ela, navegável com um clique, com backlinks se montando sozinhos.

**Primeiro caso montado:** Spazio Academia — ficha do cliente + contrato de locação 2022 + processo de despejo 0590155-64.2024.8.04.0001, todos interligados.
