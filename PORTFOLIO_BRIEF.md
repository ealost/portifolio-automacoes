# Brief — Portfólio de Automação & Dados (Evandro Costa)

Este documento é a fonte de verdade para construir o site. Serve como
contexto para o Claude Code. Objetivo: uma página estática (single-page),
publicável via **GitHub Pages**, apresentando um portfólio de automações e
projetos de dados/IA.

---

## 1. Objetivo e escopo

- **Entregável:** uma landing page estática (HTML/CSS, JS só se necessário),
  hospedável no GitHub Pages sem build obrigatório. Se usar um framework/gerador,
  garantir saída estática e workflow de deploy (`.github/workflows`).
- **Público:** recrutadores e potenciais clientes (contratação CLT ou PJ,
  consultoria em automação de processos).
- **Idioma:** português (Brasil).
- **Tom:** técnico, direto, orientado a impacto. Sem jargão vazio.
- **Anonimização (OBRIGATÓRIA):** o site é público. NÃO citar nomes de
  empresas, sistemas proprietários, nomes de tabelas, CNPJs, e-mails internos,
  placas, CPFs, IDs de template ou endpoints. Descrever por função
  ("o ERP", "o data warehouse", "a API do banco", "uma controlada").

---

## 2. Identidade / contato

- **Nome:** Evandro Costa
- **Título sugerido no topo:** Engenheiro de Automação & Dados
  (ajustável — ver seção Copy)
- **E-mail:** ealost@live.com
- **Telefone / WhatsApp:** (41) 98704-8550
- **LinkedIn:** https://www.linkedin.com/in/evandrvm/
- **GitHub:** https://github.com/ealost
- **Username GitHub:** `ealost` (relevante para o caminho de publicação
  do Pages; ver seção Deploy)

---

## 3. Direção visual

Combinada com o cliente:

- **Tema escuro.** Base grafite com acento em laranja
  (o cliente já usa essa combinação em apresentações internas).
- **Hierarquia:** os projetos **1 (Editais com IA)** e **2 (Assistente de
  Dados)** são os carros-chefe — cards maiores/destaque no topo. Os cinco
  workflows de automação (itens 3–7) entram como cards menores abaixo,
  cada um com suas tags de stack.
- **Cabeçalho (hero):** resumo curto de quem é o Evandro + os contatos.
- **Cada card:** título, descrição, e as tags de tecnologia no rodapé do card.

### Paleta sugerida (ponto de partida, refine à vontade)

| Uso              | Hex aproximado |
|------------------|----------------|
| Fundo base       | `#16181D`      |
| Superfície/card  | `#1E2128`      |
| Texto primário   | `#E8E6E1`      |
| Texto secundário | `#9AA0A6`      |
| Acento (laranja) | `#E8833A`      |
| Borda sutil      | `#2A2E37`      |

> Estes valores são sugestão, não imposição. O importante é: escuro,
> grafite, acento laranja, boa legibilidade e contraste acessível.

### Diretrizes de design (do frontend-design)

- Gastar a ousadia em UM lugar. Deixar um elemento ser o memorável e manter
  o resto quieto e disciplinado.
- Evitar os "tells" de página gerada por IA: eyebrow em ALL-CAPS acima de
  cada título; meta-strings unidas por " · "; um "→" grudado em todo link;
  mesmo border-radius e mesma sombra cinza em tudo; cards idênticos picotados.
- Numeração (01/02/03) só se o conteúdo for realmente uma sequência —
  **aqui não é**, então não numerar os projetos como se fossem passos.
- Tipografia carrega a personalidade. Escolher 1–2 famílias com intenção
  (não as defaults óbvias). Se duas, que sejam nitidamente distintas.
- Movimento: no máximo um momento orquestrado (um reveal no load). Nada de
  fade-slide-up em cada seção nem hover-transition em todo card.

### Piso de qualidade

- Responsivo até mobile.
- Foco de teclado visível.
- `prefers-reduced-motion` respeitado.
- Contraste acessível (o acento laranja sobre grafite precisa passar em texto).
- Metatags de SEO/OpenGraph (título, descrição, imagem de preview).

---

## 4. Conteúdo — os 7 projetos

> Textos já anonimizados e prontos para uso. Itens 1 e 2 são destaque
> (mais detalhados, com bullets de engenharia). Itens 3–7 são workflows
> de automação, mais enxutos.

### DESTAQUE 1 — Portal de Análise de Editais com IA

Plataforma interna que automatiza a análise de editais de licitação pública.
O usuário envia o edital e o termo de referência em PDF e, em cerca de 5
minutos, recebe uma análise comercial completa — objeto, valores, prazos,
lotes, garantias, qualificação técnica e econômico-financeira e regras de
consórcio — junto de um checklist de habilitação categorizado. É um trabalho
que antes exigia horas de leitura manual de documentos com 60 a 150 páginas.

Construída com FastAPI e Gemini 2.5 Flash, usando RAG hierárquico (PageIndex)
para navegar documentos longos, autenticação corporativa via Active Directory
e deploy em Docker. Custa cerca de R$ 3 por edital processado, com rastreamento
de gasto por etapa do pipeline.

**Tags:** Python · FastAPI · Gemini API · RAG · HTMX · Tailwind · SQLite · Docker · LDAP

---

### DESTAQUE 2 — Assistente Corporativo de Dados em Linguagem Natural

Áreas como diretoria, financeiro e suprimentos dependiam do time de dados/BI
para qualquer pergunta do dia a dia — saldo de uma controlada, total comprado
por fornecedor, qual o procedimento de abastecimento. Cada dúvida virava um
chamado, um dashboard novo ou uma consulta manual: gargalo e demora. O portal
permite que qualquer colaborador autorizado pergunte em português e receba a
resposta direta dos dados oficiais do data warehouse, com o SQL sempre
disponível para auditoria.

Um agente de IA (LLM com function calling) recebe a pergunta, explora o schema,
gera e executa o SQL e responde em linguagem natural — tudo restrito por um
catálogo semântico (YAML por área) e por guardrails de segurança e custo.
Reúne, sob o mesmo agente, dados estruturados do data warehouse e documentos
internos (POPs indexados via RAG).

Destaques de engenharia:
- **Governança de acesso em camadas** — por seção, empresa e centro de custo,
  com filtros embutidos na consulta e validados nas ferramentas do agente,
  não apenas no prompt.
- **Guardrails de custo e segurança** — acesso somente leitura, dry-run com
  teto de bytes, limite de linhas e escopo de tabelas por categoria.
- **Perfil diretoria** que cruza áreas, ex.: projeção de caixa a partir de
  saldo, recebíveis e compromissos.
- **Observabilidade** — consumo de tokens e custo estimado por usuário,
  com auditoria das conversas.

**Tags:** Python · FastAPI · Gemini API · BigQuery · React · RAG · Docker · LDAP

---

### 3 — Integração Financeira: Lançamentos entre RH e ERP

Sincronização de dados entre o sistema de folha/RH e o ERP, processando
respostas XML (SOAP) do webservice do ERP via n8n, com geração de scripts de
atualização em massa e reconciliação dos lançamentos. Dados consolidados no
data warehouse.

**Tags:** n8n · SQL Server / ERP · Webservice SOAP · BigQuery · Python

---

### 4 — Automação Ambiental (MTR / CDF)

Pipeline completo em n8n para emissão de MTR (Manifesto de Transporte de
Resíduos) e monitoramento de CDF via API federal de resíduos. Dados em
arquitetura medallion no data warehouse, PDFs em storage na nuvem e
dashboards de acompanhamento.

**Tags:** n8n · API pública (SINIR) · BigQuery · Cloud Storage · BI

---

### 5 — VAN Bancária: Conciliação com API do Banco

Integração com a API do banco para conciliação financeira: leitura de extrato,
filtragem, deduplicação de lançamentos e notificação automática por e-mail.
Inclui reconciliação de retorno CNAB240 contra o ERP.

**Tags:** n8n · API bancária · CNAB240 · ERP · Integração de e-mail

---

### 6 — Lançamento Automático de Notas Fiscais no ERP

Fluxo que elimina a digitação manual de notas fiscais de serviço no financeiro.
Ao chegar um e-mail com a NF-e, um agente de IA extrai os dados estruturados
do corpo da mensagem (fornecedor, CNPJ, número da nota, valor, município,
coligada) e o fluxo valida cada um contra o ERP: confirma se o fornecedor
existe, se a nota está em aberto e recupera o centro de custo com base em
pagamentos anteriores do mesmo fornecedor.

Passando nas validações, o lançamento é gravado direto no ERP via webservice
e o remetente recebe a confirmação automática com valor líquido e previsão de
pagamento. Cada cenário de exceção — fornecedor não encontrado, nota
inexistente, caso de consórcio, necessidade de identificação pela obra —
dispara um e-mail direcionado ao responsável certo. Todo o processamento é
registrado no data warehouse para auditoria.

**Tags:** n8n · IA (extração de dados) · SQL Server / ERP · Webservice SOAP · BigQuery · Integração de e-mail

---

### 7 — Notificação e Indicação de Condutor em Multas

Automatiza todo o início do processo de indicação de condutor quando chega uma
nova notificação de infração. O fluxo dispara com o e-mail da autuação, extrai
os dados da multa (placa, auto de infração, datas, descrição), cruza a placa
com o cadastro de frota e a escala de uso do veículo para identificar quem era
o condutor, e registra tudo no data warehouse.

Identificado o condutor, o fluxo gera automaticamente o documento de indicação
para assinatura eletrônica e o envia por WhatsApp, com verificação de status de
entrega, novas tentativas em caso de falha e confirmação no canal interno da
equipe. Quando o condutor não é encontrado ou o cadastro está incompleto, o
processo é desviado para o time responsável tratar manualmente, em vez de travar.

**Tags:** n8n · BigQuery · Assinatura eletrônica (API) · WhatsApp (Twilio) · Slack · Integração de e-mail

---

## 5. Copy do hero (rascunho — refine)

Título: **Evandro Costa**
Subtítulo: Engenheiro de Automação & Dados

Parágrafo de abertura (sugestão):
> Desenho e construo automações de ponta a ponta — de pipelines de dados e
> integrações entre sistemas a agentes de IA aplicados a processos reais de
> negócio. Foco em tirar trabalho manual do caminho e devolver tempo e
> confiabilidade para a operação.

CTA: e-mail, LinkedIn e WhatsApp no cabeçalho e/ou num rodapé fixo.

> Nota: o cliente atua tanto como CLT quanto PJ/consultoria. Se fizer sentido,
> o hero pode sinalizar disponibilidade para os dois modelos.

---

## 6. Estrutura de página sugerida

```
[ Hero: nome, título, 1 parágrafo, contatos ]
[ Destaques: card 1 (Editais IA) | card 2 (Assistente de Dados) ]  <- maiores
[ Automações: grid dos itens 3–7 ]                                 <- menores
[ Rodapé: contatos repetidos + link do GitHub ]
```

---

## 7. Deploy (GitHub Pages)

- Repositório sugerido: `ealost/portfolio` (project site →
  `https://ealost.github.io/portfolio/`), ou `ealost.github.io`
  (user site → `https://ealost.github.io/`).
- Se for site estático puro: publicar direto da branch (`main` / `/root` ou
  `/docs`) nas Settings → Pages.
- Se usar gerador com build: criar workflow em
  `.github/workflows/deploy.yml` (GitHub Actions → Pages).
- Incluir `README.md` com instruções de desenvolvimento local e publicação.
- Se o site NÃO ficar na raiz do domínio (project site), atenção a caminhos
  relativos de assets (usar caminhos relativos, não absolutos com `/`).

---

## 8. Regras não-negociáveis (checklist final)

- [ ] Nenhum nome de empresa, sistema proprietário, tabela, CNPJ, CPF, placa,
      e-mail interno, endpoint ou ID de template aparece no site.
- [ ] Tema escuro grafite + acento laranja.
- [ ] Itens 1 e 2 em destaque; 3–7 como grid secundário.
- [ ] Responsivo, foco de teclado visível, reduced-motion respeitado.
- [ ] Contatos corretos: ealost@live.com · (41) 98704-8550 ·
      linkedin.com/in/evandrvm · github.com/ealost
- [ ] Publicável no GitHub Pages.
