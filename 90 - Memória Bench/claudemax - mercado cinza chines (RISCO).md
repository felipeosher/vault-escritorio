---
data: 2026-06-22
tipo: risco-seguranca
status: aberto
prioridade: alta
---

# claudemax = mercado cinza chinês de API Claude (RISCO)

## Conexões
- [[Incidente claudemax 2026-06-21]]
- [[Aprendizados operacionais]]
- [[Decisões]]
- [[00 - Índice da Memória]]

## Resumo
A API que abastece este setup (`https://claudemax.uz2mit.easypanel.host`, provider `anthropic/*`) **não é a Anthropic oficial**. É um proxy/relay caseiro de um revendedor ("Cortex claude", contato WhatsApp) que opera no **mercado cinza chinês de revenda de API Claude**. Risco alto de privacidade, sigilo profissional e LGPD para o escritório.

## Como apareceu (2026-06-22)
- Felipe trouxe print de conversa no WhatsApp com o vendedor "Cortex claude".
- O vendedor admitiu textualmente: o painel *"se conecta com uma plataforma chinesa que oferece créditos de graça para teste, a gente cria várias contas"*.
- Justificou os travamentos/"resetar chave" como VPS compartilhada com muita gente enviando requisições.
- Ofereceu vender o "método" por **R$997 → R$500** (arquivo `.rar` para instalar em localhost na máquina do Felipe).
- Mandou uma chave `sk-...bae348e69` (descartável/compartilhada) para reativar o acesso.

## O que é tecnicamente
- `*.easypanel.host` é o domínio padrão do **EasyPanel** (PaaS self-hosted rodando em VPS de terceiro).
- `claudemax` respondeu apenas health check: `{"status":"ok","version":"1.1.2"}`. É um **relay/proxy**, não a Anthropic.
- O `.rar` "localhost" é o mesmo painel proxy apontando para as mesmas contas-laranja; só muda que roda na máquina do Felipe.

## Confirmação por pesquisa
Fontes: Tom's Hardware, SCMP, Reddit r/LocalLLM, letsdatascience, Medium. As "transfer stations" chinesas revendem API Claude a ~10% do preço oficial via:
- **Contas fraudulentas em massa** — créditos grátis abusados, cartões roubados, planos Max rachados. (Por isso as chaves morrem e "precisam resetar".)
- **Substituição de modelo** — pede Opus, recebe Sonnet/Haiku ou até Qwen relabelado; auditorias mostram queda de até ~47% de performance.
- **Data harvesting** — logam TODO prompt e TODA resposta e revendem como dado de treino. Anthropic já identificou ~24 mil contas fraudulentas (labs chineses) que coletaram ~16 milhões de trocas.
- **Bypass de verificação** — IDs gerados por IA, deepfake, KYC farms, SIM banks.
- `.rar` de origem desconhecida = vetor clássico das campanhas **"Claude Fraud"** de infostealer (roubam API keys, credenciais, carteiras cripto).

## De onde vem a cadeia (investigação aprofundada 2026-06-22)
O ecossistema tem 4 camadas:

**1. Raiz — bloqueio na China.** Anthropic bloqueia IPs chineses (403) e exige cartão internacional + telefone estrangeiro. Isso criou demanda por intermediários (中转站 = "transfer station") que revendem acesso aceitando Alipay/WeChat Pay.

**2. Software (parte open-source, em si legal).** A base técnica dos painéis é open-source:
- `one-api` (songquanpeng) e `new-api` (QuantumNous): sistemas de gerência/redistribuição de chaves LLM, unificam provedores numa API compatível OpenAI/Claude/Gemini, com dashboard, billing, rate limit e instalação 1-clique (BaoTa/EasyPanel).
- O `claudemax` do vendedor é quase certamente um `new-api`/`one-api` rodando no EasyPanel dele. O próprio projeto `new-api` publica aviso oficial CONTRA revenda fraudulenta usando o código.

**3. De onde vêm os créditos (parte ILEGAL — pergunta central do Felipe):**
- Account pooling: contas Anthropic/OpenAI em massa farmando créditos grátis (US$5/conta nova, US$50-300 com e-mail corporativo).
- Cartões roubados / virtuais para abrir contas pagas.
- Subscription subdivision: 1 plano Max rachado entre dezenas (arbitragem assinatura vs. valor de tokens).
- Refund arbitrage: abuso de política de reembolso para quota barata.
- Bypass KYC: IDs gerados por IA, deepfake em tempo real, KYC farms em países pobres, SIM banks para SMS.

**4. Como lucram além do preço:** model substitution (Opus→Sonnet/Haiku/Qwen relabelado) + data harvesting (revenda de prompts/respostas).

**Conclusão:** origem = farming de créditos grátis + contas fraudulentas + assinaturas rachadas, sobre software open-source de agregação (one-api/new-api), revendido por camadas de intermediários. Preço baixo subsidiado por fraude contra a Anthropic + venda dos dados do usuário. O "Cortex claude" é um revendedor pequeno/varejo dessa cadeia.

## Risco específico para o Felipe (advogado)
Tudo que passa pelo claudemax — petições, dados de processo, nomes de clientes, estratégia, documentos sigilosos — **está sendo potencialmente registrado por terceiro desconhecido num VPS qualquer**. Implicações:
- Violação de **sigilo profissional** (advogado).
- Violação de **LGPD** (dados pessoais de clientes a terceiro sem base legal).
- Risco **ético/OAB**.
- Uso (mesmo inadvertido) de serviço montado sobre **fraude contra a Anthropic**.
- A chave compartilhada `sk-...348e69` não deve ser confiada para nada sensível.

## Recomendação
1. **Parar de usar o claudemax para qualquer dado de cliente/processo — já.** É o modelo padrão atual (`anthropic/*`); precisa mudar.
2. **Não comprar o método nem rodar o `.rar`.** R$500 por acesso a fraude + risco de malware.
3. **Migrar para rota legítima**: Anthropic oficial (API/Claude CLI OAuth, já planejado) ou seguir no OpenAI oficial que já existe. Custa mais que os US$30-50/mês prometidos, mas é privado, estável e não expõe o escritório.

## Pendências
- [ ] Felipe decidir se troco o modelo padrão para tirar claudemax da frente (deixar OpenAI oficial até conectar Claude nativo). Aguardando OK para mostrar diff e aplicar.
- [ ] Conectar conta Claude CLI nativa (OAuth Anthropic) — rota legítima já prevista na nota do seletor de modelos.
- [ ] Atualizar a nota do seletor de modelos / MEMORY.md para registrar que claudemax = mercado cinza, não só "proxy de terceiros".
