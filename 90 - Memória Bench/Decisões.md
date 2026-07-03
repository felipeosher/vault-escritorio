# Decisões

Registro de decisões combinadas entre Felipe e Bench. Ordem cronológica.

---

## 2026-07-03 — Encerrar monitoramento Hostinger no heartbeat

**Contexto:** Felipe avisou que a questão da Hostinger já foi encerrada há muito tempo e pediu para tirar isso do heartbeat.

**Decisão operacional:** não colocar Hostinger no `HEARTBEAT.md` e não reativar monitoramento dessa thread/assunto sem novo pedido explícito.

**Ação aplicada:** cron `Monitorar conversa Hostinger` removido (id `35a659ca-1dae-4ac5-a23f-cf216600d003`). O `HEARTBEAT.md` principal já estava vazio/sem checks ativos.

---

## 2026-06-30 — Encerrar monitoramento de emails/heartbeat TIM/OKX

**Contexto:** Felipe avisou que o assunto dos emails já foi resolvido e mandou parar tudo relacionado a heartbeat/email.

**Decisão operacional:** não procurar mais por esses emails e não reativar monitoramento de Gmail/heartbeat sobre TIM/OKX sem novo pedido explícito.

**Ação aplicada:** cron `Monitor email TIM/OKX -> WhatsApp Felipe` removido e `HEARTBEAT.md` limpo para ficar sem tarefas periódicas.

---

## 2026-06-24 — Marina mudou para GPT 5.5

**Contexto:** Felipe pediu para mudar a linguagem/modelo da agente Marina para GPT 5.5.

**Alteração aplicada:** agente `concierge` / Marina alterada de `anthropic/claude-opus-4.8` para `openai/gpt-5.5`.

**Validação:** `openclaw agents list --bindings` confirmou `Model: openai/gpt-5.5` para a Marina.

**Conexões:** [[Marina modelo GPT 5.5]]

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

## 2026-06-23 — Aula 8: triagem de PDF jurídico virou proposta de skill

**Contexto:** na Aula 8 do mini-curso OpenClaw, Felipe escolheu transformar o fluxo de triagem jurídica de PDFs em uma skill durável.

**Decisão:** criar a proposta `triagem-pdf-juridico-vault`, em modo **B — skill jurídica completa**.

**Escopo da skill:**
- Felipe envia PDFs/documentos jurídicos pelo WhatsApp, WebChat ou upload local.
- Bench preserva o PDF original, classifica o documento, extrai dados-chave, cria nota-resumo e salva tudo no vault.
- A skill interliga cliente, processo e contrato com `[[wikilinks]]`.
- Quando for processo cível completo, usa o fluxo da skill `analista-processo-civil`.
- Quando houver prazo, risco ou providência óbvia, Bench já avisa Felipe junto com o resumo.
- Ao final, faz commit/push do vault e reporta o local salvo.

**Proposta criada:** `triagem-pdf-juridico-vault-20260623-4cbcdcf97b` no Skill Workshop, status pendente.

**Conexões:** [[Fluxo de triagem automática de PDF]]

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

## 2026-06-21 — Ferramenta de conhecimento: Obsidian (não Notion) + regra de interligação

**Contexto:** Felipe considerou migrar para o Notion para "ir a fundo em análise processual e estratégia".

**Decisão:** Ficar no Obsidian. Motivos: (1) Bench opera o vault direto por arquivo no disco — ler, escrever, commit, sync — sem fricção de API/rate limit; Notion viraria cliente de API. (2) Versionamento Git limpo. (3) Dados locais e sigilosos sob controle. (4) Análise profunda é texto estruturado + links + timeline, que markdown faz bem; para views relacionais tipo Notion, usar Dataview/Bases lendo o frontmatter das notas.

**Regra permanente (interligação) — confirmada por Felipe:**
- Toda entidade vira nota própria e tudo se interliga por `[[wikilink]]`.
- Processo linka cliente + contrato; contrato linka cliente + processos; cliente é a ficha-mãe que linka tudo dele.
- Sempre criar/atualizar as conexões ao arquivar qualquer documento. Nada de nota solta.
- Aproveitar backlinks automáticos e o grafo do Obsidian.

**Infra:** adicionado `.gitattributes` (LF) no vault para eliminar conflito fantasma CRLF/LF entre servidor (Linux) e Windows. Plugin Obsidian Git no Windows: ligar "Disable notifications" para parar o spam de popups de sync (sync continua ativo).

**Reforço do Felipe:** "vai sempre botando na memória do Bench, use como seu cérebro também". O vault é cérebro de trabalho ativo do Bench — registrar decisões/aprendizados/contexto aqui de forma contínua, não esporádica.

## 2026-06-21 — Caso Spazio: atuamos para a DEFESA (réu)

- Processo 0590155-64.2024.8.04.0001 — Despejo SICOOB (autor) x Spazio Academia (réu). **Felipe defende a Spazio (réu).**
- Situação desfavorável: liminar de despejo deferida (28/02/2025), não houve desocupação voluntária + depredação registrada (mov. 46.1, 29/05/2025), mandado de despejo com força policial autorizado, decisão reiterada em 19/02/2026, prazos decorridos em 06/03/2026 sem manifestação (cenário de revelia/inércia da defesa anterior — adv. anterior Mayara Almeida Macedo OAB/AM 14881).
- Export PROJUDI vai até 06/03/2026, mas foi gerado em 15/06/2026 → vão de ~3 meses a confirmar no PROJUDI.
- Notas interligadas criadas: [[Spazio Academia de Ginástica e Musculação]] (cliente) ↔ [[Contrato de Locação Comercial - Spazio 2022]] ↔ [[Resumo - Processo 0590155-64.2024.8.04.0001]].
- PENDENTE p/ montar dossiê estratégico de defesa: (1) Spazio ainda está no imóvel? (2) objetivo = resistir ao despejo ou negociar saída + reduzir passivo (débito + multa diária até R$60k)? (3) verificar andamento atual no PROJUDI.

---

## 2026-06-21 (madrugada) — VPS confirmado + estorno Managed + decisões da noite

**Ambiente:** Confirmado que estamos rodando no **VPS novo** (Debian 13 trixie, IP 187.77.234.92, OpenClaw 2026.6.8, gateway de pé). A migração do Managed → VPS foi concluída e validada. O ambiente Managed antigo pode ser cancelado.

**Estorno Hostinger (Managed OpenClaw):**
- Invoice **H_45212469**, R$54,99, compra em **16/06/2026**.
- Dentro da garantia de 30 dias (confirmado pela própria Hostinger — Nicole, em 19/06).
- E-mail formalizando o pedido de estorno **enviado** na thread "Re: Openclaw update" (thread Gmail `19edd3ebec3ce808`, msg enviada `19ee8dbdf85a2f02`) em 21/06/2026.
- ⚠️ **Ação que só o Felipe pode fazer:** segundo a Hostinger, o estorno é disparado por ele no **hPanel → Billing > Payments**. O e-mail formaliza/registra, mas pode ser que respondam pedindo o clique no painel. Bench não consegue logar na conta Hostinger.
- O estorno **encerra o serviço Managed e apaga os dados na hora** — sem problema, tudo já migrado e validado no VPS.
- Pendência: acompanhar a resposta da Hostinger e avisar o Felipe.

**Obsidian vs Notion (decisão):** Felipe cogitou migrar pro Notion para análises/estratégias processuais. Decisão = **ficar no Obsidian**. Motivos: integração direta do Bench (manipula arquivos no disco, não via API), versionamento Git limpo, dados locais/sigilosos, e Dataview/Bases entrega as views relacionais que o Notion tem. Profundidade de análise é texto estruturado + links, não limitação da ferramenta.

**Regra de interligação de notas (PERMANENTE):** toda entidade vira nota própria e tudo se interliga por `[[wikilink]]`. Processo linka cliente e contrato; contrato linka cliente e processos; cliente é a ficha-mãe que linka tudo dele. Sempre criar/atualizar essas conexões ao arquivar qualquer documento — nunca deixar nota solta. Aproveitar backlinks automáticos do Obsidian.

**.gitattributes (LF):** adicionado ao vault forçando LF nos arquivos de texto, pra acabar com o conflito fantasma CRLF/LF entre servidor (Linux) e Windows (Obsidian Git). Resolveu os alertas de conflito que o plugin dava no Windows. Felipe vai ligar "Disable notifications" no plugin Obsidian Git pra parar o spam de popups de sync.

**Caso Spazio (primeiro processo arquivado):** Processo 0590155-64.2024.8.04.0001 (despejo). ⚠️ **Felipe atua pela DEFESA (réu Spazio Academia)**, não pelo autor. Situação desfavorável: liminar de despejo deferida, mandado com força policial autorizado, prazos decorridos 06/03/2026 (cenário de revelia/inércia da defesa anterior — adv. anterior Mayara Almeida Macedo OAB/AM 14881). Export do PROJUDI vai só até 06/03/2026; há vão de ~3 meses até 15/06 a confirmar. Teia de notas criada: cliente ↔ contrato ↔ processo, todas interligadas. **Pendente:** montar dossiê estratégico da defesa — falta Felipe confirmar (1) se a Spazio ainda está no imóvel e (2) se objetivo é resistir ao despejo ou negociar saída reduzindo passivo.

---

## 2026-06-21 — Caso Spazio: virada de tese (defesa ativa)

**Contexto:** Felipe (que defende a Spazio/ré) produziu estratégia v2 atacando a raiz dominial em vez de só resistir ao despejo.

**Núcleo da tese:**
- O elo viciado a derrubar é a **DOAÇÃO DE 2020 (R-5)**: a Spazio doou seu único imóvel à sócia Amanda sem deliberação social/anuência de Nair.
- Efeito dominó: nula a doação de 2020 → Amanda nunca foi dona legítima → a dação de 2023 ao SICOOB é ineficaz → imóvel volta à Spazio.
- Reforços: abuso da personalidade/desvio de finalidade (art. 50 CC — bem social pagou dívida de R$ 6,5 mi do irmão Armando), fraude contra credores (158 CC), SICOOB não é terceiro de boa-fé (credor desde 2019).
- Contra a autora: inadequação da via/carência (485 VI), ilegitimidade ativa (nunca foi locador), exibição da CCB (396 CPC).

**PIVÔ que decide tudo:** confirmar se Nair assinou a doação de 2020 (Livro 949, fls. 135/136, 2º Ofício de Notas Manaus). Não assinou → tese fecha por vício de representação (1.015 p.ú. CC). Assinou → segue por art. 50/158 (exige provar desvio e prejuízo).

**Próximos passos (da estratégia):** reunião com Nair (questionário seção 6 por escrito); obter escritura 2020 + contrato social na JUCEA; peticionar efeito suspensivo no despejo + exibição da CCB; confirmada ausência de aval, ajuizar anulatória/declaratória c/c reintegração; avaliar notícia-crime.

**Notas criadas/interligadas no vault:** Estrategia defesa Spazio - v2; pessoas Nair, Amanda Campos Correa, Armando José Correa; resumo do processo, ficha do cliente e do contrato atualizados.

**Pendência operacional:** Felipe quer dossiê estratégico montado — boa parte já está na nota da estratégia v2. Próximo movimento real é a reunião com Nair e a obtenção dos documentos.

---

## 2026-06-21 — Transcrição de áudio via Gemini API

**Contexto:** Felipe mandou áudio; OpenAI API (transcrição) estava sem cota (`insufficient_quota`); Claude/Opus não transcreve áudio (Anthropic não aceita entrada de voz).

**Solução:** configurada **Gemini API** (Google AI Studio).
- Chave guardada em `/data/.config/gemini/key.env` (perm 600), fora do vault. Variável `GEMINI_API_KEY`.
- Modelo: `gemini-2.5-flash` (multimodal, aceita áudio). Endpoint `generativelanguage.googleapis.com/v1beta/.../generateContent`.
- Áudio .ogg/opus enviado em base64 (inline_data, mime audio/ogg). Funciona.
- Custo: cota gratuita do Gemini — sobra pro volume do Felipe (áudios curtos, esporádicos).

**Como transcrever (receita):** carregar a key.env, base64 do áudio, POST com inline_data + prompt de transcrição PT-BR, extrair `candidates[0].content.parts[0].text`.

**Aprendizado:** OpenAI NÃO é o único caminho de transcrição. Rotas: Gemini (configurada), Whisper local (offline, pendente), Groq/Deepgram/etc. Gemini também serve como rota multimodal alternativa (imagem/PDF/áudio) quando útil.

---

## 2026-06-21 — REGRA PERMANENTE: Passo a passo no WhatsApp

**Contexto:** Felipe pediu visibilidade em tempo real do que o Bench está fazendo quando recebe uma tarefa pelo WhatsApp.

**Regra:**
- Ao executar qualquer tarefa vinda do WhatsApp, enviar mensagens curtas de progresso a cada passo relevante ("lendo X...", "editando Y...", "commitando...").
- Ao entregar o resultado final, **apagar todas as mensagens intermediárias** de passo a passo para manter o chat limpo.
- Objetivo: Felipe acompanha em tempo real sem ficar no escuro, mas o histórico final fica só com o resultado.

---

## 2026-06-21 — Preferência de modelo: Claude > GPT 5.5

**Contexto:** Felipe avaliou que com o "cérebro" do Claude (Opus 4.8) o desempenho fica muito melhor que o GPT 5.5 para trabalho jurídico/operacional.

**Decisão:** Priorizar Claude (Opus 4.8 · claudemax) quando houver escolha. Manter cadeia de fallback para nunca ficar sem resposta.

---

## 2026-06-21 — Seletor de modelos: limpeza e convenção de rótulos

**Decisão:** Catálogo enxugado de 17 → 8 modelos. Convenção de rótulo: sempre escrever a ORIGEM no final do alias separada por " · " (claudemax, API, OAuth). Lista final e detalhes no MEMORY.md do sistema.

## Node PC via Tailscale conectado (2026-06-21)
- Node `Felipe PC` (Windows, tailnet `pc` / `100.88.39.101`) pareado, aprovado e testado (system.which OK) via Tailscale.
- Causa raiz do "não conecta": SERVIDOR tinha saído do tailnet (tailscaled `Logged out`/`NeedsLogin`), não o pareamento. `bind=tailnet` sem IP → `openclaw qr` falhava.
- Fix: subir daemon canônico (socket `/data/.openclaw/tailscale/tailscaled.sock`), `tailscale up --hostname=openclaw-bench-managed --accept-dns=false`, Felipe reautenticou login. Servidor voltou = `openclaw-bench-managed` / `100.115.201.125`. Serve OK.
- No PC: `Set-ExecutionPolicy CurrentUser RemoteSigned`, `npm i -g openclaw@2026.6.8` (mesma versão do gateway), `openclaw node run --host openclaw-bench-managed.tail3e6f03.ts.net --port 443 --tls`.
- Runbook atualizado: `workspace/memory/node-windows-tailscale-runbook.md`.

## Transcrição de áudio (2026-06-23)
- SEMPRE transcrever áudios com **Gemini 2.5 Flash** (`GEMINI_API_KEY`). Não usar OpenAI/Whisper por padrão (chave OpenAI sem cota em 2026-06-23). Só usar Whisper se Felipe pedir explicitamente.
- Sempre responder **por escrito** ao conteúdo do áudio, não só confirmar recebimento.
- Conexões: [[Decisões]]

## 2026-06-23 — Análise ClawHub (skills candidatas) — PENDENTE retomar
Felipe pediu análise das skills do ClawHub p/ subir produtividade 8→10 (Bench e Marina). Pediu p/ guardar e retomar mais tarde.
- Top: **Gog** (Google Workspace CLI — `gog` já instalado) e **Obsidian** (`obsidian-cli`, não instalado) → atacam os 2 eixos de atrito (Google + vault). **Nano Pdf** = ganho pontual jurídico.
- Antes de instalar: passar por gate de segurança (**Skill Vetter** ou **SkillScan**), pois ClawHub é registro aberto de terceiros e lidamos com dado sigiloso.
- Marina: escopo estreito de propósito; nada sob medida no catálogo; Gog ajuda indiretamente (agenda). Não inflar escopo dela.
- Fora: Self-Improving/Proactive (já temos), Humanizer, Weather (já temos), Github (gh ausente), Notion, Multi Search, Tavily, AdMapix, PollyReach, Nano Banana Pro.
- Veredito: sozinhas vão de 8→~9; o 10 depende de fluxo Google ponta a ponta + triagem de PDF lisa.
- Plano (aguardando OK): 1) instalar vetter; 2) auditar Gog/Obsidian/Nano Pdf; 3) ativar as que passarem.
- Detalhe completo: `memory/2026-06-23-clawhub-analise-skills.md` no workspace.
