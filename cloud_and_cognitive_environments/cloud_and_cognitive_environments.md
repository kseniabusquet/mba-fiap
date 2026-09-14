# Cloud & Cognitive Environments

## Sumário

- [Cloud \& Cognitive Environments](#cloud--cognitive-environments)
  - [Sumário](#sumário)
  - [Sobre a disciplina](#sobre-a-disciplina)
  - [Aula 1 — Fundamentos \& Estratégia de Cloud](#aula-1--fundamentos--estratégia-de-cloud)
    - [1. Cloud como analogia da rede elétrica](#1-cloud-como-analogia-da-rede-elétrica)
    - [2. Modelos de serviço (IaaS, PaaS, SaaS, FaaS)](#2-modelos-de-serviço-iaas-paas-saas-faas)
    - [3. Modelos de deployment e provedores](#3-modelos-de-deployment-e-provedores)
    - [4. Os 6 Rs de migração](#4-os-6-rs-de-migração)
    - [5. Escalabilidade, SLA e Pricing](#5-escalabilidade-sla-e-pricing)
    - [6. Segurança: menor privilégio e RBAC](#6-segurança-menor-privilégio-e-rbac)
    - [7. Mão na massa: Resource Group e VM](#7-mão-na-massa-resource-group-e-vm)
    - [8. Infraestrutura como Código (IaC)](#8-infraestrutura-como-código-iac)
    - [9. Erros comuns e troubleshooting](#9-erros-comuns-e-troubleshooting)
    - [10. Recap e mensagens-âncora](#10-recap-e-mensagens-âncora)
  - [Aula 2 — Armazenamento \& Bancos de Dados](#aula-2--armazenamento--bancos-de-dados)
    - [1. Tipos de armazenamento (Object, File, Block)](#1-tipos-de-armazenamento-object-file-block)
    - [2. Blob Storage em profundidade](#2-blob-storage-em-profundidade)
    - [3. Redundância e distribuição geográfica](#3-redundância-e-distribuição-geográfica)
    - [4. Banco relacional, Key Vault e pool de conexões](#4-banco-relacional-key-vault-e-pool-de-conexões)
    - [5. NoSQL: famílias e casos de uso](#5-nosql-famílias-e-casos-de-uso)
    - [6. Busca vetorial, AI Search e RAG](#6-busca-vetorial-ai-search-e-rag)
  - [Aula 3 — Serverless, Containers \& Gestão de Identidade](#aula-3--serverless-containers--gestão-de-identidade)
    - [1. Serverless / FaaS: Azure Functions](#1-serverless--faas-azure-functions)
    - [2. API vs. MCP](#2-api-vs-mcp)
    - [3. Gatilhos (triggers) e padrões de consumo assíncrono](#3-gatilhos-triggers-e-padrões-de-consumo-assíncrono)
    - [4. Quando usar Function, Batch ou VM](#4-quando-usar-function-batch-ou-vm)
    - [5. Segredos e gestão de identidade: do hardcode ao Managed Identity](#5-segredos-e-gestão-de-identidade-do-hardcode-ao-managed-identity)
    - [6. Containers: o que são e por que usá-los](#6-containers-o-que-são-e-por-que-usá-los)
    - [7. Máquina Virtual vs. Container](#7-máquina-virtual-vs-container)
    - [8. Escalonamento horizontal (scale out/in)](#8-escalonamento-horizontal-scale-outin)
    - [9. Orquestração de containers no Azure](#9-orquestração-de-containers-no-azure)
    - [10. Paralelização de agentes de IA](#10-paralelização-de-agentes-de-ia)
  - [Aula 4 — Serviços Cognitivos \& APIs](#aula-4--serviços-cognitivos--apis)
    - [1. Três jeitos de colocar IA no agente: pronta, custom, LLM](#1-três-jeitos-de-colocar-ia-no-agente-pronta-custom-llm)
    - [2. Modelos de cobrança e o multiplicador de custo do LLM](#2-modelos-de-cobrança-e-o-multiplicador-de-custo-do-llm)
    - [3. Azure OpenAI em contexto](#3-azure-openai-em-contexto)
    - [4. Lab 1: provisionando o ecossistema cognitivo multi-service](#4-lab-1-provisionando-o-ecossistema-cognitivo-multi-service)
    - [5. Speech: STT e TTS](#5-speech-stt-e-tts)
    - [6. A mesma vacina da Aula 3: Managed Identity em serviços cognitivos](#6-a-mesma-vacina-da-aula-3-managed-identity-em-serviços-cognitivos)
    - [7. Language: sentimento, entidades e PII/LGPD](#7-language-sentimento-entidades-e-piilgpd)
    - [8. Vision: tags, OCR, object detection e Custom Vision](#8-vision-tags-ocr-object-detection-e-custom-vision)
    - [9. A matriz de decisão conceitual da aula](#9-a-matriz-de-decisão-conceitual-da-aula)
    - [10. Encerramento: destroy, a cinta de tools do agente e recap](#10-encerramento-destroy-a-cinta-de-tools-do-agente-e-recap)
    - [11. Gravação do Lab da Aula 4](#11-gravação-do-lab-da-aula-4)
  - [Aula 5 — Agentes de IA \& Microsoft Foundry](#aula-5--agentes-de-ia--microsoft-foundry)
    - [1. Do loop ao agente: o laço e as seis camadas](#1-do-loop-ao-agente-o-laço-e-as-seis-camadas)
    - [2. Chatbot, agente e harness: três nomes que o mercado confunde](#2-chatbot-agente-e-harness-três-nomes-que-o-mercado-confunde)
    - [3. MCP vs. Skills: dois jeitos de estender um agente](#3-mcp-vs-skills-dois-jeitos-de-estender-um-agente)
    - [4. Microsoft Foundry: a hierarquia Recurso → Projeto → Agente e os três tipos de agente](#4-microsoft-foundry-a-hierarquia-recurso--projeto--agente-e-os-três-tipos-de-agente)
    - [5. Tech for Tech vs. Tech for Business: os quatro motivadores de uma plataforma cloud de agentes](#5-tech-for-tech-vs-tech-for-business-os-quatro-motivadores-de-uma-plataforma-cloud-de-agentes)
    - [6. Os modelos disponíveis e suas portas de entrada no Foundry](#6-os-modelos-disponíveis-e-suas-portas-de-entrada-no-foundry)
    - [7. Comparando modelos: qualidade, segurança, performance e custo](#7-comparando-modelos-qualidade-segurança-performance-e-custo)
    - [8. Como o Foundry cobra: as oito métricas de billing e um exemplo de custo real](#8-como-o-foundry-cobra-as-oito-métricas-de-billing-e-um-exemplo-de-custo-real)
    - [9. Orçamento não é cota: o freio de verdade](#9-orçamento-não-é-cota-o-freio-de-verdade)
    - [10. Árvore de decisão: onde rodar o agente](#10-árvore-de-decisão-onde-rodar-o-agente)
    - [11. Autonomia do agente: reversibilidade × verificabilidade](#11-autonomia-do-agente-reversibilidade--verificabilidade)
    - [12. Laboratório: Deva, Deva2, Deva3 e o Deva contínuo](#12-laboratório-deva-deva2-deva3-e-o-deva-contínuo)
  - [Aula 6 — FinOps](#aula-6--finops)
    - [1. Do lab de agentes ao FinOps: fechando o ciclo com a Eva](#1-do-lab-de-agentes-ao-finops-fechando-o-ciclo-com-a-eva)
    - [2. FinOps: os 3 pilares e por que "cortar custo" é a definição errada](#2-finops-os-3-pilares-e-por-que-cortar-custo-é-a-definição-errada)
    - [3. Maturidade (Crawl/Walk/Run) e os três papéis de FinOps](#3-maturidade-crawlwalkrun-e-os-três-papéis-de-finops)
    - [4. Tags: a base de tudo](#4-tags-a-base-de-tudo)
    - [5. Lab 1: Cost Management, Advisor e Budget Alert na assinatura do aluno](#5-lab-1-cost-management-advisor-e-budget-alert-na-assinatura-do-aluno)
    - [6. Anatomia de custo: o que compõe a fatura de um datacenter](#6-anatomia-de-custo-o-que-compõe-a-fatura-de-um-datacenter)
    - [7. Otimização de compute e storage: Reserved, Spot, Right-sizing, lifecycle e o vilão do egress](#7-otimização-de-compute-e-storage-reserved-spot-right-sizing-lifecycle-e-o-vilão-do-egress)
    - [8. Lab 2 + Exercício: TCO da Quantum Commerce no Pricing Calculator](#8-lab-2--exercício-tco-da-quantum-commerce-no-pricing-calculator)
    - [9. FinOps em IA: o custo do agente é consequência do prompt, não da arquitetura](#9-finops-em-ia-o-custo-do-agente-é-consequência-do-prompt-não-da-arquitetura)
    - [10. A unidade econômica do agente: custo por turno e token economics](#10-a-unidade-econômica-do-agente-custo-por-turno-e-token-economics)
    - [11. As cinco alavancas de otimização e o equivalente das estratégias de desconto em IA](#11-as-cinco-alavancas-de-otimização-e-o-equivalente-das-estratégias-de-desconto-em-ia)
    - [12. Lab 3: FinOps na Eva — da régua à decisão](#12-lab-3-finops-na-eva--da-régua-à-decisão)
    - [13. Fechamento da disciplina: recap das 6 aulas](#13-fechamento-da-disciplina-recap-das-6-aulas)
  - [Material complementar — Terraform](#material-complementar--terraform)
    - [Terraform: criando máquinas na Azure](#terraform-criando-máquinas-na-azure)
    - [Criando o primeiro ambiente com o Terraform (AWS)](#criando-o-primeiro-ambiente-com-o-terraform-aws)

---

## Sobre a disciplina

- **Ementa:** visão geral das plataformas de nuvem do mercado, implementação prática de projetos, desenho de soluções orientadas a negócio e integração entre plataformas para aplicações de IA.
- **Formato de avaliação:** grupos de 3–4 alunos (Grupos "Quantum Commerce"), 5 entregas parciais de 10% cada + projeto final de 50% (entregue como ZIP, sem apresentação oral).
- **Pré-requisito:** conta de estudante Azure ativa, com crédito de US$ 100 válido por 12 meses (`MBA_Config_Azure_2026.pdf`).
- **Regra de ouro do curso:** *"Delete > Stop"* — sempre excluir o Resource Group (ou rodar `terraform destroy`) ao final de cada exercício para não consumir crédito à toa.

---

## Aula 1 — Fundamentos & Estratégia de Cloud

### 1. Cloud como analogia da rede elétrica

Cloud computing foi apresentado como uma "tomada elétrica": em vez de a empresa comprar, instalar e manter seus próprios servidores (datacenter próprio, com custo de refrigeração, energia, segurança física e risco de capacidade ociosa ou insuficiente), ela aluga capacidade de um datacenter remoto e compartilhado, pagando apenas pelo que consome e podendo escalar automaticamente.

### 2. Modelos de serviço (IaaS, PaaS, SaaS, FaaS)

Usando a analogia da pizza (quanto da "pilha" você quer gerenciar):

| Modelo | O que você gerencia | Exemplo |
|---|---|---|
| On-premise | Tudo (hardware, virtualização, SO, runtime, dados, aplicação) | Datacenter próprio |
| IaaS | SO, runtime, dados, aplicação | Azure VMs |
| PaaS | Dados e aplicação (o provedor cuida de SO e runtime) | App Service, Azure SQL |
| SaaS | Nada — só usa | Gmail, Office 365, Salesforce |
| FaaS (serverless) | Só a função — cobrança por execução | Azure Functions, Lambda |

### 3. Modelos de deployment e provedores

Quatro modelos de deployment: **Pública** (~80% das cargas, ex.: AWS/Azure/GCP), **Privada** (compliance/regulação, comum em bancos brasileiros por causa do BCB), **Híbrida** (on-prem + cloud pública, padrão para LGPD/latência) e **Multi-cloud** (evita lock-in, mas aumenta complexidade operacional).

Os três grandes provedores: **Azure** (líder enterprise, integração Microsoft, parceria FIAP com US$100 grátis), **AWS** (líder em market share, maior catálogo) e **GCP** (força em dados/ML, BigQuery e Vertex AI).

### 4. Os 6 Rs de migração

Framework para decidir como migrar uma carga de trabalho para a nuvem:

1. **Rehost** (lift & shift) — move para VM sem refatorar; rápido, mas captura pouco valor da cloud.
2. **Replatform** — pequenas otimizações (ex.: trocar banco por um gerenciado), mantendo a app.
3. **Refactor** — reescreve cloud-native (microsserviços, event-driven, serverless); maior esforço, maior ganho.
4. **Repurchase** — troca por SaaS (Salesforce, HubSpot); decisão de negócio.
5. **Retire** — desliga o que ninguém usa mais.
6. **Retain** — mantém on-premise por compliance, latência ou custo; não é falha, é estratégia legítima.

### 5. Escalabilidade, SLA e Pricing

- **Escalabilidade vertical** (scale up: mais CPU/RAM na mesma máquina) vs. **horizontal** (scale out: mais instâncias atrás de um balanceador, exige app stateless).
- **SLA:** cada "9" adicional de disponibilidade custa exponencialmente mais — 99,9% permite ~8h46min de downtime/ano; 99,999% permite apenas ~5min/ano.
- **Modelos de cobrança:** Pay-as-you-go (sem compromisso), Reserved (1–3 anos, 30–70% de desconto), Spot (capacidade ociosa, até 90% off, mas pode ser interrompida) e Savings Plan (compromisso de gasto flexível).
- Aviso recorrente do professor: recursos esquecidos ligados são a principal causa de faturas-surpresa.

### 6. Segurança: menor privilégio e RBAC

Princípio que se repete em todas as aulas: dar a cada usuário e agente **apenas o necessário**.

- **Reader** (só lê) → **Contributor** (lê e escreve) → **Owner** (tudo, inclusive dar permissão — perigoso).
- **RBAC** = Identidade (quem) → Role (o que pode fazer) → Escopo (onde pode fazer).
- **Managed Identity** é o padrão recomendado para identidade de agentes/serviços dentro do Azure (sem credencial para gerenciar); **Service Principal** só quando a Managed Identity não alcança (fora do Azure, multi-tenant).
- Riscos concretos de dar Owner a um agente de IA: ele pode escalar o próprio privilégio, ampliar o raio de explosão de um incidente (ex.: prompt injection), manter credencial 24/7 sem MFA, e cegar a auditoria.

### 7. Mão na massa: Resource Group e VM

Durante a gravação, o professor retomou e concluiu o laboratório prático da Aula 1 (que havia ficado pendente na aula anterior por problemas técnicos):

- Criação de um **Resource Group** (`rg-lab-aula01`), com tags para permitir consulta e agrupamento de custos.
- Criação de uma **VM Linux** (Ubuntu Server 24.04 LTS): escolha de família de VM (a turma usou `Standard_D2s_v3`, com foco didático nas famílias **B** — burst/econômica, **D** — uso geral, **F** — compute-intensivo, **M** — memória, **N** — GPU/ML), tipo de disco (HDD vs. SSD vs. SSD Premium) e região (East US 2, historicamente mais barata).
- Autenticação por **chave SSH pública/privada**; abertura das portas 22 (SSH), 80 (HTTP) e 443 (HTTPS).
- Conexão via **Cloud Shell** com a chave baixada, publicação de uma página HTML simples via `python3 -m http.server 80` para validar o IP público.
- Ao final, exclusão do Resource Group inteiro (não apenas "parar" a VM) para zerar o custo.

### 8. Infraestrutura como Código (IaC)

Bloco apontado como "o mais importante da aula em termos de retorno profissional":

- Problemas do provisionamento manual (cliques no portal): difícil de reproduzir, difícil de revisar, fácil de errar, impossível de auditar em escala.
- **IaC** é declarativo (descreve o estado desejado), idempotente (rodar 2x = mesmo resultado), versionável (Git) e auditável.
- **Terraform** (HCL, multi-cloud, usado como principal ferramenta da disciplina) vs. **Bicep** (sintaxe nativa Azure, mais enxuta, mas restrita ao Azure).
- Ciclo do Terraform demonstrado ao vivo: `terraform init` → `terraform plan` → `terraform apply` → (editar e reaplicar para observar idempotência) → `terraform destroy`.
- O professor refez a mesma VM criada manualmente, agora via Terraform, para que a turma sentisse a diferença entre "a dor do clicódromo" e a praticidade do código.

### 9. Erros comuns e troubleshooting

Discutidos ao vivo (a turma teve vários desses problemas durante o lab): erro de crédito/subscription sem saldo, erro de cota (tamanho de VM indisponível — trocar tamanho ou região), erro de SSH (conferir IP público, usuário `azureuser` e chave), e demora na exclusão do Resource Group (processo assíncrono, pode levar de 1 a 5 minutos).

### 10. Recap e mensagens-âncora

As quatro mensagens que a disciplina reforça ao longo de todas as aulas:

1. **Cloud é a base** — toda arquitetura de agentes de IA em escala depende de cloud.
2. **IaC é como Git para infraestrutura** — reprodutibilidade vence "funcionou na minha máquina".
3. **Identidade própria** — cada agente em produção deve ter sua identidade (Managed Identity).
4. **Menor privilégio** — sempre o mínimo necessário, em RBAC, Key Vault e identidades gerenciadas.

---

## Aula 2 — Armazenamento & Bancos de Dados

A aula começou com a analogia: *"na Aula 1 montamos a casa vazia (Resource Group, VM, IaC); agora vamos mobiliar — decidir onde vivem os dados que os agentes vão consumir."*

### 1. Tipos de armazenamento (Object, File, Block)

| Tipo | Uso | Azure | AWS | GCP |
|---|---|---|---|---|
| **Object Storage** | Dados não estruturados (imagens, vídeos, logs, backups), acesso via HTTP/REST | Blob Storage | S3 | Cloud Storage (GCS) |
| **File Storage** | Pastas compartilhadas entre VMs | Azure Files | EFS | Filestore |
| **Block Storage** | Disco de baixa latência atrelado a uma VM (não compartilhável) | Managed Disks | EBS | Persistent Disk |

### 2. Blob Storage em profundidade

- Estrutura de **chave–valor** (não existem pastas de verdade — "pasta" é só uma convenção de prefixo na chave). No Azure, o **container** é a "pasta raiz" obrigatória dentro de uma **Storage Account**.
- **Tiers de acesso** (mesmo byte, preços diferentes — cerca de 9x de diferença entre o mais caro e o mais barato):

| Tier | Custo/GB/mês (referência) | Quando usar |
|---|---|---|
| Hot | ~US$ 0,018 | Acesso frequente, dados quentes servidos a APIs/agentes |
| Cool | ~US$ 0,010 | Dados de 30+ dias sem acesso regular |
| Cold | ~US$ 0,0036 | Retenção de compliance, mínimo 90 dias |
| Archive | ~US$ 0,002 | Arquivamento real — minutos para recuperar |

- **Lifecycle policy**: uma política declarativa move automaticamente os blobs entre tiers (ex.: 0–30 dias Hot, 30–90 dias Cool, 90+ dias Archive) — casos citados: Itaú/Magalu (data lakes raw/trusted/refined), Netflix (CDN + tiers para catálogo popular vs. antigo).
- Durabilidade típica do Blob: 11 a 16 "noves" (99,999999999%+).

### 3. Redundância e distribuição geográfica

Hierarquia física: **Datacenter** → **Zona** (DCs próximos, baixíssima latência) → **Região** (agrupamento de zonas).

| Redundância | Cópias | Proteção |
|---|---|---|
| **LRS** (Locally Redundant) | 3 cópias, 1 datacenter | Nenhuma contra desastre regional |
| **ZRS** (Zone Redundant) | 3 zonas da região | Sobrevive à queda de uma zona |
| **GRS** (Geo Redundant) | LRS + região secundária | Desastre regional completo |
| **RA-GRS** | GRS + leitura na secundária | Menor resiliência de escrita, leitura mesmo sem failover |

Também foi discutido (em resposta a uma pergunta sobre compliance/LGPD em SaaS multiusuário global) como aplicações globais replicam front-end e banco de dados por região/zona e direcionam o usuário pela origem da requisição, mantendo dados sensíveis fisicamente na região exigida por regulação (ex.: dados de cidadãos europeus permanecendo na UE).

### 4. Banco relacional, Key Vault e pool de conexões

- **Banco relacional** continua sendo a escolha para ~90% dos casos: quando é preciso garantia **ACID** (atomicidade, consistência, isolamento, durabilidade) — carrinho, pedido, pagamento, faturamento, estoque. Exemplos citados: Oracle, SQL Server, MySQL, Firebase.
- **Conexão SQL**: abrir uma conexão nova a cada requisição (TCP + handshake + autenticação + TLS) é caro em escala; por isso se usa **pool de conexões** (conjunto de conexões pré-abertas e reaproveitadas) — essencial em aplicações web e Functions.
- **Key Vault**: nunca deixar senha/connection string hardcoded no código (vaza no Git, no log, no incidente). O padrão é guardar o segredo no Key Vault e a aplicação (via **Managed Identity**) buscar o segredo em runtime — a aplicação nunca "sabe" a senha diretamente.

### 5. NoSQL: famílias e casos de uso

"NoSQL não é um banco, é uma classe" — cinco famílias principais discutidas:

| Família | Exemplos | Uso típico |
|---|---|---|
| **Documento** (JSON aninhado) | Cosmos DB (SQL API), MongoDB | Domínios variáveis — reviews, carrinhos |
| **Key-Value** | Redis, DynamoDB | Cache, sessões, dados quentes de baixa atualização |
| **Colunar** (wide-column) | Cassandra, Cosmos DB (Cassandra API) | Grandes volumes, muitas colunas, telemetria |
| **Grafo** | Cosmos Gremlin, Neo4j | Relações complexas — detecção de fraude (ex.: correlação geolocalização + comportamento de cartão), análise de interdependência de sistemas |
| **Semântica/Vetorial** | Cosmos NoSQL (vector), Pinecone, AI Search, Neptune | Similaridade semântica |

Pontos discutidos ao vivo: diferença central do NoSQL é não ser relacional — não há `JOIN` nativo, relações se resolvem via código/API; **Cosmos DB** é versátil (documento + vetor + Gremlin) mas tem custo alto (instância + requisição + disponibilidade fixa), então vale sempre comparar com alternativas mais baratas para o mesmo caso de uso.

### 6. Busca vetorial, AI Search e RAG

- Texto é transformado em **vetores** (embeddings); a busca vetorial encontra itens semanticamente similares por proximidade, não por correspondência exata de palavra.
- **Hybrid search**: combina busca vetorial + ranking semântico + score de relevância (ex.: percentual de match com o benchmark) para devolver o resultado mais assertivo.
- Opções de vector database mencionadas: **Azure AI Search** (padrão de mercado da Azure), **pgvector** (extensão do PostgreSQL), **Pinecone** (serviço de terceiros especializado) e **Cosmos DB Vector**.
- Fluxo geral de um agente com RAG: pergunta do usuário → busca vetorial/semântica → contextualização via prompt → resposta gerada por um LLM.
- Um aluno trouxe o **Teorema CAP** (para NoSQL) e o **ACID** (para relacional) como frameworks complementares para decidir qual banco usar.

---

## Aula 3 — Serverless, Containers & Gestão de Identidade

A gravação começa concluindo pendências do laboratório da Aula 2 (parte da turma ainda travada na criação de recursos, com erro de imagem de VM indisponível em algumas regiões/subscriptions — o professor ajustou os scripts do repositório para forçar a busca da imagem e recomendou puxar a última versão). Encerrado esse ponto, a aula segue para o tema central: como publicar e escalar código na nuvem, dos dois lados do espectro — sem servidor (Functions) e em containers.

### 1. Serverless / FaaS: Azure Functions

Uma function é código que não precisa de uma máquina pré-instanciada para existir: ela fica "disposta", sobe sob demanda, executa e morre logo em seguida. Características centrais discutidas em aula:

- **Orientada a evento** — nunca roda "por rodar" com um agendamento fixo interno; é sempre disparada por algo externo (requisição HTTP, timer, mensagem em fila, upload em Blob Storage, Event Grid).
- **Cobrança por execução**, não por tempo de máquina ligada — o professor citou como referência algo em torno de 1 milhão de execuções e centenas de GB de memória/mês dentro do free tier do Azure, o que torna o custo efetivo próximo de zero para cargas leves e esporádicas.
- Equivalente direto na AWS: **Lambda** — mesmo modelo de recurso, nomenclatura diferente.
- Runtime: o mesmo código Python usado como exemplo na Aula 1 (função de consulta de estoque) pode ser publicado em uma VM, em um container ou em uma Function — a decisão de onde publicar depende do padrão de consumo, não da linguagem.

### 2. API vs. MCP

Os dois protocolos foram apresentados como complementares, não concorrentes. Uma **API** é um contrato fixo — desde a popularização pós-2012/2013, é o modelo dominante para expor funcionalidades entre sistemas: se a chamada não seguir exatamente o contrato (parâmetros, formato), não há retorno. O **MCP** não compete com a API — ele **consome** APIs (uma ou várias) de forma semântica: em vez de apenas ler um contrato fixo, o MCP entende que tipo de informação e que tipo de API tem pela frente e se resolve de forma mais flexível, inclusive quando a informação não está exatamente no formato esperado.

### 3. Gatilhos (triggers) e padrões de consumo assíncrono

Gatilhos comuns citados para disparar uma function ou um recurso serverless: chamadas **REST/HTTP**, **timer** (agendamento pré-determinado), consumo de **filas** de mensagens, upload de arquivo em **Blob Storage**, e **Event Grid** (eventos nativos do Azure).

Um ponto trabalhado com a turma via exemplos reais: quando um fluxo tem alto volume ou pode demorar, não se deve processar de forma síncrona (o chamador fica esperando, sujeito a timeout e engargalamento). O padrão discutido é **desacoplar via fila**: o serviço que recebe a requisição só grava um registro na fila e devolve a resposta imediatamente; um segundo serviço lê a fila, processa, grava o resultado e dispara um novo evento/fila para avisar quem estava aguardando. Exemplo usado: um pipeline de reconhecimento de imagem de exames médicos — a cada download de um exame pelo cliente, uma function cria o registro no Blob e dispara um evento, sem travar a experiência do usuário esperando o processamento terminar.

### 4. Quando usar Function, Batch ou VM

Não existe resposta única — a decisão depende do volume, do tempo de resposta esperado e da frequência de uso. Pontos levantados em aula, com exemplos do próprio professor (ex-responsável por processamento e autorização de pagamentos em banco):

- **Function**: ações pontuais, sob demanda, baixa/média volumetria, resposta em segundos — ideal para chamadas de API e reações a eventos.
- **Batch**: quando o volume é alto e processado em lote (ex.: fechamento de autorização de pagamentos) — o processamento roda separado do fluxo online, sem impor timeout à experiência do usuário; separa "recursos, mas sem custo" incorrendo em cada requisição individual.
- **Máquina Virtual**: quando a aplicação exige controle total do sistema operacional, roda continuamente 24/7, ou tem uma carga estável e alta o suficiente para não valer a pena escalar via function; custo é por hora de máquina ligada, sem cold start.
- Um exemplo de consulta analítica simples (produtos mais vendidos do dia, batendo direto em uma tabela grande do Data Lake) foi discutido como caso onde uma function ou o próprio site já resolvem, sem justificar infraestrutura mais pesada.

### 5. Segredos e gestão de identidade: do hardcode ao Managed Identity

Evolução de maturidade na forma de guardar credenciais, da pior para a melhor prática:

| Estratégia | Onde fica guardado | Quem acessa | Risco |
|---|---|---|---|
| Hardcoded no código | Dentro do próprio repositório Git | Qualquer um com acesso ao repositório | Altíssimo — vaza no Git, no log, em prints de tela |
| Variável de ambiente / arquivo de config | Arquivo de configuração, acesso via portal | Quem tem acesso ao ambiente/infra | Médio |
| Key Vault | Cofre de segredos dedicado | Aplicação com uma chave de acesso ao cofre | Baixo, mas a própria chave de acesso ainda pode ser exposta |
| **Managed Identity** | Não fica guardado em lugar nenhum | Função/recurso vinculado à identidade, sem chave para gerenciar | Mínimo — não há segredo para vazar |

O GitHub já atua como primeira barreira: ao tentar commitar uma credencial reconhecível, ele bloqueia o push e alerta sobre informação sensível, recomendando excluir o arquivo ou trocar a credencial imediatamente. Ainda assim, o professor reforçou (com exemplos do mercado financeiro brasileiro) que vazamento de código-fonte com Managed Identity é bem menos grave do que vazamento de usuário/senha de banco de dados hardcoded, porque não há credencial reutilizável exposta.

Um ponto discutido em resposta a uma pergunta de aluno: quando um agente precisa acessar múltiplos recursos (ex.: cinco "stories"/domínios diferentes), a prática recomendada **não** é criar uma identidade por recurso (gera complexidade de gestão desnecessária), mas sim organizar o RBAC por escopo de Resource Group, vinculando a Managed Identity às roles necessárias dentro daquele escopo — análogo ao uso de GPOs (Group Policy) no Windows, onde a permissão é dada por vínculo a um grupo/regra, não por credencial individual.

### 6. Containers: o que são e por que usá-los

Um container empacota código, dependências e parte do sistema operacional necessário para rodar uma aplicação de forma isolada e portátil — resolvendo diretamente o clássico problema de "na minha máquina funciona": diferenças de versão de SO, de servidor SQL, de bibliotecas entre ambiente de desenvolvimento, homologação e produção deixam de ser um risco porque a mesma imagem de container é levada, sem alteração, por todas as etapas.

Componentes do fluxo de containerização discutidos: o **Dockerfile** declara qual imagem de sistema operacional usar, quais dependências instalar e qual aplicação subir; a imagem resultante é publicada em um **registro de imagens** (Azure Container Registry, equivalente ao Docker Hub); a partir daí, subir e escalar uma nova instância é rápido, porque a imagem já está pronta e pré-configurada.

O professor conectou esse tema à arquitetura de **micro-frontends**, usando o exemplo de um app bancário: em vez de um aplicativo monolítico, cada "jornada" (Home, extrato, pagamentos, Pix, investimentos) é um conjunto independente de front-end + BFF + serviços, empacotado em containers próprios. Vantagem central: se a jornada de Pix cair, o time só desabilita aquela jornada — o app continua funcional nas demais, sem precisar tirar a aplicação inteira do ar.

### 7. Máquina Virtual vs. Container

| Aspecto | Máquina Virtual | Container |
|---|---|---|
| Camadas | Hypervisor + SO completo + dependências + app | Kernel compartilhado + camada fina de boot + app |
| Tempo de subida | ~1 a 2 minutos (varia com o tamanho da imagem) | Segundos — já sobe com tudo pré-configurado na memória |
| Isolamento | Total (SO próprio) | Por processo, com kernel compartilhado |
| Quando usar | Controle total do SO, cargas estáveis e contínuas | Portabilidade, deploys rápidos, escalonamento frequente, orquestração |

A vantagem prática de custo/velocidade do container aparece exatamente na frequência de deploy e escalonamento: como a imagem já vem pronta, o "setup" que uma VM paga toda vez que sobe não existe mais.

### 8. Escalonamento horizontal (scale out/in)

Uma máquina publicada na nuvem gera custo simplesmente por estar ligada — por isso a prática recomendada é manter uma capacidade base pequena (o professor usou o exemplo de duas instâncias) e escalar automaticamente por **triggers** conforme a demanda, tipicamente monitorando uso de CPU (ex.: subir nova instância ao ultrapassar um limiar) ou de memória (ex.: não deixar passar de 80% de consumo).

Exemplo usado em aula: uma campanha de vendas relâmpago (ex.: promoção de dois dias) faz o tráfego saltar de ~100–200 acessos/hora para ~20 mil/hora; sem escalonamento automático, a aplicação passa a devolver erros de sobrecarga (403/500) e a empresa perde vendas no pior momento possível. Com autoscaling configurado por trigger, novas instâncias sobem automaticamente durante o pico e são desligadas (**scale in**) quando a demanda cai — por exemplo, ao detectar a máquina ociosa (idle) por um tempo, ou processamento abaixo de um piso definido — evitando manter dezenas de máquinas paradas gerando custo depois que a campanha termina. Essa elasticidade sob demanda foi apontada como uma capacidade que datacenters próprios de 15–20 anos atrás simplesmente não ofereciam, por dependerem de capacidade fixa contratada.

### 9. Orquestração de containers no Azure

Modelos de execução de container discutidos, do mais simples ao mais robusto:

- **Container sem orquestrador** (Azure Container Instances) — forma mais simples de rodar um único container isolado, sem cluster nem health check; adequado para cargas pontuais e simples.
- **Azure Container Registry** — armazena e organiza as imagens para consumo sob demanda.
- **App Container (Container Apps)** — faz escalonamento automático dos containers.
- **Jobs** — simula processamento batch, escalando containers para cargas de processamento pontuais.
- **AKS (Azure Kubernetes Service)** — orquestração completa via Kubernetes; mais complexa, mas é o modelo adotado por grandes empresas quando é preciso organizar e escalonar um volume grande de containers de forma robusta. O professor observou que Kubernetes "não é a resposta para tudo" — para a maioria das cargas do dia a dia, ficar na gestão simples de containers já resolve; o AKS se justifica quando a escala e a complexidade organizacional exigem.

### 10. Paralelização de agentes de IA

Fechando a aula com uma ponte direta para "cognitive environments", o professor usou agentes de IA (citando o Manos e o ChatGPT como exemplos) para ilustrar o mesmo princípio de escalonamento aplicado a processamento de agentes: ao receber uma tarefa de pesquisa composta (ex.: comparar informações de várias fontes), o agente não processa tudo em uma única instância sequencial — ele **federa a tarefa em múltiplas instâncias paralelas**, cada uma responsável por uma sub-pesquisa, e depois compila os resultados. A alternativa monolítica (uma única instância pesquisando, guardando, pesquisando de novo, guardando) seria mais lenta e não escala. O dimensionamento de quantas instâncias paralelas usar segue a mesma lógica de escalonamento vista para containers e VMs: estimar volume esperado de uso, acompanhar a variação ao longo do tempo com um painel de monitoramento de custo, e ajustar o teto de paralelização de acordo.

---

## Aula 4 — Serviços Cognitivos & APIs

*Baseado apenas nos slides da aula (sem transcrição de áudio/vídeo disponível para esta aula).*

A provocação de abertura resume o tema: "teu agente já busca produtos, hoje ele ganha sentidos". Na Aula 3 o agente ganhou sua primeira tool (busca no catálogo); a Aula 4 pluga três novas capacidades — escutar (Speech), ler com inteligência (Language) e ver (Vision) — todas como serviços cognitivos prontos, consumidos via API, plugados em um endpoint serverless (Azure Function). Ao longo da aula, cada capacidade nova é usada como pretexto para revisitar a mesma pergunta: API pronta, modelo customizado ou LLM?

### 1. Três jeitos de colocar IA no agente: pronta, custom, LLM

| Categoria | O que é | Setup | Quando usar | Exemplos Azure |
|---|---|---|---|---|
| **API pronta** | Modelo genérico já treinado pelo provedor, consumido via REST | Minutos | Tarefa genérica e fechada (sentimento, OCR, transcrição) | Speech, Language, Vision |
| **Modelo customizado** | Você fornece os dados e treina/fine-tuna no seu domínio | Dias a semanas | Vocabulário próprio (peças industriais, contratos jurídicos, catálogo de marca) | Custom Vision, CLU |
| **LLM (foundation)** | Modelo de propósito geral para tarefas abertas — resumir, gerar, raciocinar | Minutos (mas caro em escala) | Tarefa aberta e criativa, sem categoria fechada | Azure OpenAI |

Regra mental repetida ao longo da aula: tarefa genérica e fechada → pronta; domínio próprio → custom; aberta e criativa → LLM. Comparando os três eixos de decisão — setup, custo unitário, latência e controle — a API pronta e o LLM sobem rápido (minutos), mas o custom Vision leva dias a semanas; em compensação, é o único que chega a 5/5 em domínio específico, contra 2/5 da API pronta. Padrão de uso sugerido: prototipar e validar com LLM (mais rápido para testar a ideia), depois migrar para API pronta ou modelo custom em produção, onde o custo por escala importa mais.

### 2. Modelos de cobrança e o multiplicador de custo do LLM

Cada categoria cobra de um jeito diferente:

- **API pronta** — por uso (chamada, caractere ou segundo). Referências citadas: Vision ~US$1/1.000 imagens, Language ~US$2/1M caracteres, Speech ~US$1/hora de áudio.
- **Custom** — custo de treinamento (Custom Vision ~US$1–2/hora de treino) + armazenamento do modelo + predição por chamada. Perfil CAPEX alto (treino, equipe especializada), OPEX baixo depois de treinado.
- **LLM** — por token, somando input + output, variando por modelo (Azure OpenAI ~US$2–15/1M tokens).

A mensagem central do bloco: em escala, trocar um serviço pronto por LLM pode multiplicar a conta por 10 a 50 vezes. Se a tarefa cabe num serviço pronto, o serviço pronto é a escolha por custo — reforçado depois, seção a seção, comparando sentiment analysis via serviço específico (~US$0,75/1M caracteres, latência <500ms) contra sentiment via LLM (~US$2–15/1M tokens, latência 1–3s).

### 3. Azure OpenAI em contexto

O Azure OpenAI é apresentado como o LLM gerenciado da Azure: API gerenciada para os modelos da OpenAI (GPT-4o, embeddings) e da própria Microsoft (Phi, DeepSeek), rodando dentro do Azure. Vantagens citadas sobre usar a OpenAI diretamente: os dados não vão para treino do modelo, hosting dentro do Azure (relevante para LGPD), e integração nativa com Managed Identity e isolamento de rede. Para esta disciplina o uso é pontual — gerar descrição de produto, resumir reviews, gerar embeddings para RAG —, com aprofundamento reservado para a disciplina de Knowledge Management & Prompt Engineering do MBA. O exercício bônus (N3) da entrega usa Azure OpenAI para gerar embeddings reais, fechando o loop com a busca vetorial vista na Aula 2.

### 4. Lab 1: provisionando o ecossistema cognitivo multi-service

O primeiro laboratório provisiona via Terraform o conjunto de recursos que sustenta a aula inteira, organizado em arquivos `.tf` separados por responsabilidade:

| Arquivo | O que define |
|---|---|
| `main.tf` | Providers, Resource Group, locals (tags + credenciais Mongo), data source de identidade |
| `variables.tf` | Localização (default `eastus2`) |
| `outputs.tf` | Outputs consumidos pelo guia e pelos scripts |
| `storage.tf` | Storage Account de dados + containers `audios` e `imagens` |
| `function.tf` | Storage da Function + App Service Plan + Function App + role assignment |
| `cognitive.tf` | Azure AI Services multi-service (Speech, Language, Vision em uma única conta) |
| `keyvault.tf` | Key Vault + role para o usuário + segredo `ai-services-key` |
| `mongodb.tf` | Container Group (ACI): MongoDB 7.0 + Mongo Express (interface web) |

Uma mudança notável em relação às aulas anteriores: o **MongoDB** (rodando em Azure Container Instances, open source) substitui o Cosmos DB como "servidor de documentos" do laboratório — mesmo papel arquitetural, mas sem o custo do serviço gerenciado da Azure. O recurso central da aula é a conta **Azure AI Services multi-service**: um único serviço cognitivo que expõe Speech, Language, Vision, Decision, Document Intelligence e Metrics Advisor sob a mesma chave e endpoint, o que simplifica o provisionamento — em vez de um recurso por capacidade, um recurso guarda-chuva para todas.

### 5. Speech: STT e TTS

- **Speech-to-Text (STT)** — converte áudio em texto. Suporta modo real-time via websocket (atendimento ao vivo — o mesmo padrão do caso "Sky" mencionado na Aula 3, de captura de formulário em streaming) e modo batch (URL de áudio → resultado). Recursos adicionais: diarização (separar quem fala em um áudio com múltiplos falantes), pontuação automática e filtro de profanidade. Apontado como um dos recursos cognitivos genéricos mais usados no mercado.
- **Text-to-Speech (TTS)** — converte texto em voz. Vozes neurais em PT-BR citadas como muito naturais (Antonio, Francisca, Brenda); SSML controla entonação, pausa e ênfase. Casos de uso: URA, audiobooks, acessibilidade — e, no laboratório, geração de um áudio de teste como fallback para exercitar o pipeline de transcrição.

No lab, o script `gerar_audio_tts.py` monta um payload SSML descrevendo a Quantum Commerce, autentica via `Ocp-Apim-Subscription-Key` (chave obtida do Key Vault, não hardcoded), chama o endpoint TTS da região e salva o áudio resultante (`audio-teste.wav`), que depois é enviado para o container `audios` da Storage Account. A função `transcrever` publicada na Function App faz o caminho inverso: baixa o áudio do Blob (via Managed Identity), obtém um token do Speech (via chave, nesse trecho específico do código) e chama o endpoint de reconhecimento, retornando a transcrição em JSON.

### 6. A mesma vacina da Aula 3: Managed Identity em serviços cognitivos

A aula reforça explicitamente que a lição de segurança da Aula 3 (evitar credencial hardcoded, preferir Managed Identity) se aplica igualmente aos serviços cognitivos — "mesma vacina, recurso diferente". Três formas de autenticar no AI Services, da mais simples à mais segura:

| Método | Como | Quando usar |
|---|---|---|
| **API Key** | Header `Ocp-Apim-Subscription-Key: <key>` | Dev/test rápido, ou cenário legado |
| **Token AAD / Managed Identity** | Header `Authorization: Bearer <token>`, negociado automaticamente | Padrão recomendado em produção |
| **Custom Domain + restrição de rede** | Combina autenticação com restrição de IP/VNet | Compliance enterprise |

A API Key funciona e é rápida para prototipar, mas ainda é uma chave que pode vazar; o token via Managed Identity elimina esse risco porque a Function tem identidade própria, ganha a role necessária (`Cognitive Services User`), e o token é negociado sozinho — sem segredo para gerenciar ou vazar. Pré-requisitos técnicos citados para a Managed Identity funcionar no AI Services: custom subdomain habilitado na conta cognitiva e a role `Cognitive Services User` atribuída à identidade.

### 7. Language: sentimento, entidades e PII/LGPD

Capacidades do Language listadas como "NLP as a Service", com foco da aula em duas delas — sentimento e entidades — sobre o pipeline de reviews da Quantum Commerce:

| Capacidade | O que faz | Caso prático |
|---|---|---|
| Sentiment Analysis | Classifica positivo/neutro/negativo + confiança | Reviews de clientes |
| Opinion Mining | Sentimento por aspecto específico (ex.: "entrega" → ruim) | Reviews granulares |
| Entity Recognition | Identifica pessoas, locais, organizações, datas, produtos | Produtos mencionados em texto livre |
| Key Phrase Extraction | Extrai frases/palavras-chave | Dashboards, roteamento |
| Language Detection | Identifica o idioma do texto | Roteamento multilíngue |
| PII Detection | Identifica e mascara CPF, e-mail, telefone | Compliance LGPD |
| Summarization | Resume textos longos | Reviews extensas |
| Custom CLU | NLU customizado para intenções | Entender o que o usuário quer de um agente |

O destaque de compliance é o **PII Detection**: reviews de clientes eventualmente trazem CPF, e-mail ou telefone que o cliente digitou sem perceber que estava expondo — o serviço identifica e mascara essa informação antes de logar ou usar o texto para treinar qualquer coisa, funcionando como uma camada automática de conformidade com a LGPD.

No Lab 3, o pipeline processa reviews armazenadas no MongoDB: busca reviews brutas no banco, envia para o Cognitive Services (Language), grava o resultado analisado de volta no banco. Um detalhe de engenharia citado: o filtro `NOT IS_DEFINED` evita reprocessar reviews que já passaram pela análise, tornando o pipeline idempotente a chamadas repetidas. Ao final, a aula pede explicitamente para os alunos revisarem o pipeline com foco em segurança — observando que os dados de conexão do Mongo ficam em variável de ambiente, a chave do AI Services vem do Key Vault, e nenhum valor sensível aparece exposto ou commitado no código.

### 8. Vision: tags, OCR, object detection e Custom Vision

Principais serviços de Vision as a Service apresentados:

| Serviço | O que faz |
|---|---|
| Image Tagging | Lista tags genéricas da imagem ("furniture", "chair", "office") — útil para auto-categorizar produtos |
| Object Detection | Devolve bounding boxes localizando itens na foto — ex.: contar produtos numa prateleira |
| OCR / Read API | Extrai texto de etiquetas, embalagens, documentos, devolvendo texto estruturado |
| Image Description | Gera legenda em linguagem natural descrevendo a imagem — acessibilidade |
| Image Embedding | Gera vetor (modelo Florence) para busca visual por similaridade |
| Smart Cropping | Recorte de thumbnail focado automaticamente no produto |

A escolha entre Vision pronto e Custom Vision segue a mesma regra do início da aula: vocabulário genérico (é uma cadeira? é uma mesa?) resolve cerca de 80% dos casos sem treinar nada e sobe em minutos; vocabulário próprio (é qual modelo específico da nossa marca?) exige Custom Vision, com 30 a 50 imagens por classe e treino de 10 a 30 minutos por um custo de ~US$1–2. Um caso citado como claramente do lado custom: detecção de defeitos específicos em peças de linha de produção industrial (porosidade, rechupe, trinca, furo) — vocabulário e padrões visuais específicos demais para um modelo genérico reconhecer.

No Lab 4, a função `analisar_imagem` recebe o nome do blob de uma imagem já enviada à Storage Account, chama o Cognitive Services (Vision) e devolve as características extraídas em JSON — o mesmo padrão arquitetural de "tool encapsulada atrás de um endpoint serverless" usado em Speech e Language, permitindo trocar o provedor de Vision no futuro (ou apontar para outra imagem, outro pipeline — como um hipotético pipeline de aprovação de crédito imobiliário citado como exemplo de reuso do mesmo padrão) sem alterar o contrato exposto ao agente.

### 9. A matriz de decisão conceitual da aula

A entrega conceitual do bloco de Vision generaliza a decisão pronto vs. custom vs. LLM em uma matriz de cenários:

| Cenário | Recomendado |
|---|---|
| "É uma cadeira?" — vocabulário genérico | Vision (pronto) |
| "É qual modelo da nossa marca?" — vocabulário próprio | Custom Vision |
| "Resuma esta etiqueta nutricional" | OCR + LLM |
| "Encontre produtos similares a esta foto" | Image Embeddings + AI Search |
| "Detecte produtos numa foto de prateleira" | Object Detection (custom) |

O padrão que a matriz revela: as melhores soluções não escolhem um serviço único, elas combinam serviços — OCR extrai o texto bruto, o LLM interpreta e resume; o Embedding vetoriza a imagem, o AI Search busca por similaridade. O agente (LLM orquestrador) funciona como o maestro que decide qual combinação de tools acionar para cada pedido do usuário.

### 10. Encerramento: destroy, a cinta de tools do agente e recap

O bloco final reforça a regra de ouro do curso com um adendo: **parar** um recurso não é o mesmo que **zerar** o custo — um container parado ou um Azure Container Registry ocioso ainda mantêm storage e registro reservados consumindo. Só `terraform destroy` apaga de fato Resource Group, Function, Service Plan, ACR e ACI de uma vez; a confirmação final deve ser feita olhando o Cost Management do portal para verificar que o gasto realmente caiu a zero.

Fechando o arco do "projeto integrado" da disciplina (Quantum Commerce), a aula amarra as quatro tools construídas até aqui num único endpoint serverless, todas expostas para o mesmo agente orquestrador:

```
GET  /produtos?categoria=...       # Aula 3 — busca no catálogo
POST /transcrever?blob=...         # Aula 4 — Speech
POST /analisar-reviews?limit=10    # Aula 4 — Language
POST /analisar-imagem?blob=...     # Aula 4 — Vision
```

Cada rota é exposta ao LLM como uma tool via function calling, e é o próprio modelo (o "maestro") quem decide, a partir do pedido do usuário, qual tool (ou combinação delas) acionar — a mesma anatomia de "cérebro com sentidos plugados" (Custom Tools, Speaking Tools, Vision Tools, Listening Tools em torno do LLM orquestrador) que abre a aula reaparece aqui fechada e funcional.

Os quatro recados finais da aula: (1) a categoria de IA a usar depende do formato da tarefa — genérica e fechada vai para pronta, domínio próprio vai para custom, aberta e criativa vai para LLM; (2) o agente aprende a escutar com a mesma prática de segurança da Aula 3, trocando API key por Managed Identity também nos serviços cognitivos; (3) o agente aprende a ler com sentimento, entidades e detecção de PII, aplicado sobre um pipeline real de reviews em banco de documentos; (4) o agente aprende a ver com tags, OCR e detecção de objetos, e a decisão pronto vs. custom vs. LLM é a entrega conceitual central da aula.

Sobre a estrutura da entrega da Aula 4 (10% da nota, dentro do total de 5 entregas parciais + projeto final): Nível 1 obrigatório cobre ecossistema cognitivo, pricing, segurança (API key vs. Managed Identity) e capacidades de Vision; Nível 2 obrigatório cobre pipeline robusto de reviews (sumarização + PII + opinion mining), casos de uso de Speech e a comparação pronto vs. custom; Nível 3 é bônus (até +2 pontos extras) e inclui embeddings reais com Azure OpenAI, Custom Vision e sumarização via LLM. A aula termina com o teaser da Aula 5.

---

### 11. Gravação do Lab da Aula 4

[Link - YouTube](https://www.youtube.com/watch?v=BdLWnULU224)

---

## Aula 5 — Agentes de IA & Microsoft Foundry

A aula muda de patamar: até aqui o agente ganhou tools (catálogo, Speech, Language, Vision) penduradas num endpoint serverless, mas quem decidia a sequência de chamadas ainda era código determinístico. A partir daqui o tema é o agente propriamente dito — um LLM que decide sozinho quando e como usar cada tool — e a plataforma gerenciada da Azure para hospedar, versionar e cobrar por esse tipo de sistema: o **Microsoft Foundry** (renomeado de "Azure AI Foundry"). A aula alterna teoria de arquitetura de agentes com uma demonstração ao vivo do portal do Foundry, incluindo comparação de modelos no playground e uma estimativa de custo real de um agente de exemplo.

### 1. Do loop ao agente: o laço e as seis camadas

Um agente é definido pelo seu **loop**: Observar → Pensar → Agir → Observar o resultado, repetido até a tarefa terminar ou até um dos três freios de segurança interromper o laço — **máximo de voltas** (`max_voltas`, evita loop infinito), **orçamento de tokens** (corta antes que o custo escape) e **timeout** (evita que uma tarefa trave o sistema indefinidamente). Sem esses freios, um agente mal instruído pode entrar em um ciclo de chamadas que não termina sozinho, gastando tokens (e dinheiro) a cada volta.

Em torno desse laço, o professor descreveu um agente como seis camadas empilhadas:

| Camada | O que é | Exemplo prático |
|---|---|---|
| **Loop** | O ciclo Observe → Think → Act | O motor do agente |
| **Contexto** | Instruções fixas de identidade e comportamento | `AGENTS.md` — com a regra prática de não passar de ~200 linhas, sob risco de o próprio contexto virar custo e ruído |
| **Memória** | O que o agente lembra entre interações | `MEMORY.md` — perfil do usuário, preferências, fatos recorrentes |
| **Ferramentas** | O que o agente pode fazer no mundo | MCP, Skills, tools nativas |
| **Autonomia** | Onde e por quanto tempo o agente roda | Sessão local vs. hospedado persistente |
| **Modelo** | O LLM que raciocina em cada volta do loop | GPT, Claude, DeepSeek, Gemini, Kimi |

### 2. Chatbot, agente e harness: três nomes que o mercado confunde

Um **chatbot** responde uma pergunta por vez, sem memória persistente de ações e sem capacidade de agir sobre o mundo além de gerar texto. Um **agente** tem o loop completo — observa, decide usar uma ferramenta, executa, observa o resultado e decide o próximo passo, tudo isso amarrado por contexto e memória persistente. Um **harness** é a camada de orquestração/infraestrutura que dá corpo ao agente — o "chassi" que gerencia sessão, ferramentas disponíveis, limites e execução (o próprio Claude Code, por exemplo, é um harness). A distinção importa na hora de escolher o que construir: nem todo problema de automação precisa de um agente completo — às vezes um chatbot ou uma function determinística resolve com menos custo e menos risco.

### 3. MCP vs. Skills: dois jeitos de estender um agente

Os dois padrões foram comparados como complementares, cada um resolvendo uma parte diferente do problema de "como um agente aprende a fazer algo novo":

- **MCP (Model Context Protocol)** — criado pela Anthropic e doado à Agentic AI Foundation (sob a Linux Foundation) em 12/09/2025; a especificação de 28/07/2026 tornou o protocolo *stateless*. MCP define como um agente se conecta a **ferramentas e fontes de dados externas** de forma padronizada — um servidor MCP expõe funções que qualquer agente compatível pode chamar, sem que o agente precise conhecer os detalhes de implementação de cada API por trás.
- **Skills** — especificação aberta (agentskills.io), baseada em **progressive disclosure**: um `SKILL.md` descreve, em linguagem natural, um procedimento ou conhecimento específico que o agente carrega sob demanda, só quando a tarefa exige. Skills resolvem o problema de instruir comportamento e procedimento (como fazer), enquanto MCP resolve o de conectividade e execução (com o que fazer).

Na prática, um agente maduro combina os dois: MCP para acessar sistemas e dados, Skills para saber como agir sobre eles em um domínio específico.

### 4. Microsoft Foundry: a hierarquia Recurso → Projeto → Agente e os três tipos de agente

O Foundry organiza tudo em três níveis:

1. **Recurso** — a unidade de região, cota e billing (equivalente à Storage Account ou Cognitive Services multi-service vistos nas aulas anteriores).
2. **Projeto** — a unidade de custo e de controle de acesso dentro de um recurso; é onde os modelos são implantados (deployment) e onde o consumo é medido.
3. **Agente** — a unidade funcional, de um dos três tipos:

| Tipo | O que é | Código necessário | Quando usar |
|---|---|---|---|
| **Prompt** | Agente definido só por instrução + modelo + ferramentas configuradas no portal | Nenhum | Ponto de partida — prototipagem rápida, sem infraestrutura própria |
| **Hosted** | Seu próprio código de agente rodando dentro de um container gerenciado pelo Foundry | Sim (seu código) | Quando a lógica do agente exige algo que o modo Prompt não cobre; custo cobrado por vCPU-hora + GiB-hora do container, além do consumo de tokens |
| **Workflow** | Um agente que orquestra outros agentes (Prompt, Hosted ou Workflow) | Configuração de orquestração | Processos multi-etapa que combinam várias capacidades especializadas |

### 5. Tech for Tech vs. Tech for Business: os quatro motivadores de uma plataforma cloud de agentes

Uma pergunta recorrente em aula: por que não simplesmente chamar a API da OpenAI ou da Anthropic direto do código, sem passar pelo Foundry? A resposta separa duas visões: **"Tech for Tech"** — construir o agente pela elegância técnica da solução — de **"Tech for Business"** — construir considerando o que a empresa realmente precisa para colocar aquilo em produção com segurança. Quatro motivadores concretos justificam pagar a "taxa" de rodar um agente dentro de uma plataforma cloud gerenciada, em vez de bater direto na API do provedor de modelo:

1. **Residência de dados** — garantir que dados sensíveis não saiam da região/jurisdição exigida (o mesmo tema de LGPD revisitado desde a Aula 2).
2. **Identidade corporativa** — o agente herda RBAC e Managed Identity da organização, em vez de uma chave de API solta.
3. **Sandbox de execução** — ambiente controlado e isolado para o agente rodar código ou acessar sistemas, sem expor a rede corporativa.
4. **Plano de controle** — visibilidade e governança centralizada sobre todos os agentes da empresa (quem publicou, o que consome, quanto custa).

### 6. Os modelos disponíveis e suas portas de entrada no Foundry

Nem todo modelo entra no Foundry pela mesma porta, e isso afeta diretamente o billing:

| Família | Porta de entrada | Implicação de billing |
|---|---|---|
| **OpenAI** (GPT-5.6 Sol/Terra/Luna) | Vendido diretamente pela Azure | SLA da Microsoft + aceita crédito (estudante, gratuito, CSP) |
| **DeepSeek V4** | Vendido diretamente pela Azure | Mesmo tratamento do OpenAI — SLA + crédito |
| **Anthropic Claude** | Parceiro via Marketplace | Cobrado em **CCU** (Claude Consumption Unit), que decrementa o MACC (compromisso de gasto Azure) — mas **não** aceita crédito de estudante, gratuito ou CSP |
| **Moonshot Kimi** | Parceiro via Marketplace | Mesmo tratamento do Claude — cobrança via CCU |
| **Google Gemini** | Fora do catálogo | Não disponível; só os pesos abertos do Gemma podem ser usados |

Um caso real mostrado em aula: rodar o mesmo modelo DeepSeek via Foundry custa cerca de **4,5x mais** do que chamar a API do DeepSeek diretamente — o professor foi enfático que isso não é bug nem sobrepreço arbitrário, é o preço da infraestrutura gerenciada (Entra ID, RBAC, SLA, isolamento) empacotada junto.

### 7. Comparando modelos: qualidade, segurança, performance e custo

O playground do Foundry foi demonstrado ao vivo comparando GPT-5, Claude, Kimi e DeepSeek na mesma pergunta, ancorando a escolha de modelo em quatro dimensões, não apenas preço por token:

1. **Qualidade** — acurácia da resposta para a tarefa específica.
2. **Segurança / ASR** (Attack Success Rate) — quanto menor, melhor; mede o quão resistente o modelo é a jailbreak e prompt injection.
3. **Performance** — latência P90 (não a média — o percentil 90 revela o pior caso comum).
4. **Custo por execução** — não custo por token; o número que importa é quanto custa **resolver a tarefa**, já considerando quantos tokens de entrada e saída ela normalmente consome.

A mensagem central: o modelo mais barato por token pode sair mais caro por execução, se precisar de mais iterações ou gerar respostas mais longas para chegar à mesma qualidade.

### 8. Como o Foundry cobra: as oito métricas de billing e um exemplo de custo real

O Foundry mede consumo em oito frentes, listadas do maior para o menor peso típico numa fatura:

| Métrica | O que mede |
|---|---|
| Uso de tokens | ~98% de uma fatura típica |
| vCPU/memória do agente Hosted | Container rodando código próprio |
| Armazenamento de vector knowledge | US$ 0,10/GB-dia após 1 GB gratuito |
| Sessões de code interpreter | Execução de código sandboxed |
| Web grounding | ~US$ 35 por 1.000 transações de busca |
| Application Insights | ~US$ 2,30/GB ingerido — **habilitado por padrão**, ponto de atenção porque gera custo mesmo sem ninguém pedir |

Um exemplo de custo trabalhado em aula, para um agente fictício chamado **Deva2**: rodando no modelo GPT-5.6 Terra, a estimativa mensal ficou em torno de **US$ 109,66**; trocando para o modelo Luna (mais leve), a mesma carga caiu para cerca de **US$ 13,04/mês** — uma diferença de quase 9x só pela escolha do modelo, reforçando o ponto da seção anterior sobre custo por execução.

### 9. Orçamento não é cota: o freio de verdade

Um ponto de segurança financeira destacado com ênfase: o **orçamento** (budget) configurado no Foundry só **envia um alerta por e-mail** quando o gasto se aproxima ou ultrapassa o limite — ele não interrompe o consumo. Quem efetivamente limita o gasto é a **cota** (TPM — tokens por minuto — configurada por deployment): um teto técnico que passa a recusar novas requisições ao ser atingido. Confundir os dois é um erro comum e caro — configurar só o orçamento dá uma falsa sensação de proteção.

### 10. Árvore de decisão: onde rodar o agente

A escolha entre agente Prompt, Hosted, Workflow, ou simplesmente usar Container Apps/Functions (sem Foundry) segue uma lógica de complexidade crescente: se o comportamento cabe inteiramente em instrução + ferramentas configuráveis no portal, Prompt resolve sem esforço de engenharia; se a lógica exige código customizado que o modo Prompt não cobre, Hosted é o caminho, aceitando o custo adicional de vCPU/memória do container gerenciado; se a tarefa precisa orquestrar múltiplos agentes especializados em sequência ou paralelo, Workflow é o padrão certo; e quando o caso de uso é essencialmente uma function determinística sem necessidade de raciocínio de LLM, a resposta certa pode nem envolver o Foundry — Functions ou Container Apps "puros", como visto na Aula 3, seguem sendo mais baratos e mais simples.

### 11. Autonomia do agente: reversibilidade × verificabilidade

Para decidir quanta autonomia dar a uma ação de agente (executar sozinho vs. pedir aprovação humana), o professor propôs uma matriz de duas dimensões: **reversibilidade** da ação (é fácil desfazer se der errado?) e **verificabilidade** do resultado (dá para confirmar automaticamente se a ação teve o efeito esperado?). Ações reversíveis e verificáveis podem ser totalmente autônomas; ações irreversíveis e difíceis de verificar (ex.: enviar um pagamento, deletar um recurso de produção) exigem aprovação humana explícita antes de executar — o mesmo princípio de menor privilégio e "Delete > Stop" que atravessa a disciplina desde a Aula 1, agora aplicado à decisão de design de um agente.

### 12. Laboratório: Deva, Deva2, Deva3 e o Deva contínuo

A aula usa uma progressão de exemplos do próprio professor como fio condutor didático, mostrada ao longo de várias aulas do curso:

- **Deva** (Aula 2) — os primeiros arquivos de contexto e memória de um agente simples.
- **Deva2** (Aula 3) — o agente publicado numa plataforma, usado no exemplo de custo desta aula.
- **Deva3** (Aula 5) — um agente com código customizado rodando em container, consumindo a API de Vision do Foundry para análise de imagem — um exemplo direto de agente Hosted.
- **Deva contínuo** (Lab 2 desta aula) — o exemplo mais avançado: uma demonstração de continuidade e memória revisável, em que sugestões de atualização de memória passam primeiro por um arquivo de pendências (`MEMORIA-PENDENTE.md`), exigem aprovação humana antes de virar `MEMORY.md` definitivo, mantêm uma fila de exceções para casos não previstos, e expõem deliberadamente uma superfície de ferramentas restrita: a API subjacente tem 14 operações, mas a especificação OpenAPI do agente só expõe 5 — nenhuma delas capaz de auto-aprovar suas próprias mudanças. É o princípio de menor privilégio (Aula 1) e de reversibilidade/verificabilidade (seção anterior) aplicado na prática a um agente que precisa lembrar de coisas entre sessões sem virar um risco de segurança.

---

## Aula 6 — FinOps

A última aula da disciplina muda de lente: depois de cinco aulas construindo arquitetura — cloud, dados, serverless, containers, serviços cognitivos e agentes — a pergunta que fecha o curso é econômica. A provocação de abertura resume o tema: *"a arquitetura mais bonita do mundo pode falir a empresa se o custo escapar do controle"*. FinOps é apresentado não como um adendo de fim de curso, mas como "a outra metade do trabalho" de quem projeta sistemas em nuvem.

### 1. Do lab de agentes ao FinOps: fechando o ciclo com a Eva

A aula começa retomando e concluindo o laboratório de agentes iniciado na Aula 5: os alunos baixam o projeto do agente **Eva** (um assistente pessoal com identidade, regras de resposta e uma função de exemplo para consultar datas), primeiro rodando localmente contra a API da OpenAI com uma chave pública fornecida pelo professor (`chave.zip`), depois migrando o mesmo agente para rodar via **Microsoft Foundry**, criando um projeto próprio no portal (`ai.azure.com`), fazendo o deploy de um modelo (GPT-4o ou GPT-5.4 mini, conforme disponibilidade) e trocando a autenticação por chave pública pelo modelo de identidade do **Entra ID** — o mesmo salto de maturidade de segurança (de chave hardcoded para identidade gerenciada) já visto nas Aulas 3 e 4, agora aplicado a um agente. Essa Eva publicada e instrumentada é o sistema real que o restante da aula usa como estudo de caso de FinOps aplicado a IA.

### 2. FinOps: os 3 pilares e por que "cortar custo" é a definição errada

Pela definição da FinOps Foundation, citada em aula, FinOps é uma **"disciplina cultural e prática que combina engenharia, finanças e negócios para maximizar valor de negócio em workloads de cloud"**. O ponto central: FinOps não é "ficar pão-duro" — gastar US$ 100 e gerar US$ 500 não é vitória se for uma oportunidade desperdiçada; gastar US$ 1.000 e gerar US$ 10.000 é melhor. FinOps mede o gasto para permitir decisão informada sobre onde investir, não para minimizar gasto por si só.

O ciclo virtuoso tem três pilares, e a maioria das empresas nunca passa do primeiro:

| Pilar | Foco | Ferramentas típicas |
|---|---|---|
| **1. Inform** | Visibilidade — quem gasta o quê, onde, quando | Cost Management, tags, dashboards |
| **2. Optimize** | Ação — reduzir custo sem perder qualidade | Advisor, Reserved Instances, lifecycle policies |
| **3. Operate** | Cultura — "every engineer is FinOps now" | KPIs, budgets, retrospectivas mensais |

### 3. Maturidade (Crawl/Walk/Run) e os três papéis de FinOps

Empresas evoluem em três estágios: **Crawl** (controle superficial — budget alerts e tags básicas, onde está a maioria das empresas), **Walk** (Reserved Instances, lifecycle policies e dashboards, empresas medianas) e **Run** (chargeback por time, retrospectivas mensais e um FinOps Engineer dedicado, empresas líderes). Três papéis dividem o trabalho: **cada engenheiro** (responsável pela arquitetura — toda decisão de design reflete em custo), o **Cloud Cost Analyst** (perfil analítico — relatórios, modelagem de custo, forecasting para a diretoria) e o **FinOps Engineer** (perfil consultivo — cost intelligence automatizada, dashboards, alertas, pipelines de custo, indicando melhorias).

### 4. Tags: a base de tudo

A cadeia lógica apresentada em aula: sem tag não há identificação; sem identificação não há alocação de custo; sem alocação de custo não há FinOps. Uma tag aplicada **na criação do recurso**, via Terraform, permite depois alocar custo por projeto, time, ambiente ou, no caso da disciplina, por aula — e o professor apontou que a turma já pratica isso desde a Aula 1, com tags como `aula = "3"`, `disciplina = "cloud-cognitive"`, `projeto = "quantum-commerce"` e `provisionado = "terraform"` nos arquivos `.tf`: FinOps básico, na prática, desde o primeiro laboratório do curso.

### 5. Lab 1: Cost Management, Advisor e Budget Alert na assinatura do aluno

O primeiro laboratório aplica o pilar Inform na própria assinatura Azure for Students de cada aluno: no portal, em **Cost Management → Cost analysis**, filtrando os últimos 30 dias com granularidade diária e agrupando por serviço, cada aluno identifica seus três maiores gastadores; depois repete o agrupamento por **Tag** (`aula`), revelando qual aula do curso consumiu mais crédito. Em seguida, o **Azure Advisor** (aba Cost) é consultado em busca de recomendações de otimização — tipicamente vazio para quem desprovisiona os recursos ao final de cada aula, o que é, em si, o aprendizado esperado. O laboratório fecha configurando um **budget alert** (nome, valor, período de reset mensal, condições de alerta em 50/80/100% e destinatário de e-mail), e uma discussão em grupo sobre quem já ultrapassou o crédito, o que fariam diferente, e como esse aprendizado se aplica à escala de uma empresa.

### 6. Anatomia de custo: o que compõe a fatura de um datacenter

Revisitando o tema de datacenter da Aula 1 sob a lente financeira, os custos de um datacenter se dividem em três blocos: **custos computacionais** (processador/memória dos servidores, armazenamento, tráfego de rede), **custos de infraestrutura** (energia, refrigeração, segurança física) e **custos de serviço** (plataformas, backups, licenças). Ao decidir o que usar na nuvem, as perguntas centrais viram: quais recursos o meu workload realmente vai consumir, quanto "extra" pago pela comodidade de administração serverless, e qual o ganho real de terceirizar essa administração.

### 7. Otimização de compute e storage: Reserved, Spot, Right-sizing, lifecycle e o vilão do egress

Revisitando o **lifecycle de storage** já visto na Aula 2 (Hot → Cool → Archive → delete), o ponto de FinOps é quantificar: mover blobs frios automaticamente entre tiers gera de 80% a 90% de economia em logs antigos, e em escala isso significa seis dígitos por ano — mas o Archive cobra uma **retrieval fee** para ler o dado de volta, então não serve para dados que ainda são acessados com frequência.

No lado de compute, cinco estratégias de desconto foram comparadas:

| Estratégia | Desconto | Risco | Quando usar |
|---|---|---|---|
| Pay-as-you-go | 0% | Nenhum | Dev/test imprevisível |
| Reserved Instances | ~30–50% | Compromisso de 1–3 anos | Workload 24/7 estável |
| Spot | ~60–90% | Pode ser interrompido | Batch, treino de ML |
| Savings Plan | ~25–40% | Compromisso de gasto | Múltiplos serviços, mais flexível |
| Right-sizing | Varia | Nenhum | Sempre — é o *low-hanging fruit* antes de assinar qualquer compromisso de 3 anos |

Por fim, o **egress** foi descrito como "o vilão silencioso": tráfego entrando na nuvem é grátis, tráfego saindo é cobrado por gigabyte, variando por região — uma cobrança que costuma pegar times de surpresa. Mitigação: manter a mesma nuvem e região de sistemas, clientes e fornecedores existentes, reaproveitar cópias, processar os dados na própria região e extrair apenas resultados agregados.

### 8. Lab 2 + Exercício: TCO da Quantum Commerce no Pricing Calculator

O segundo laboratório — que vale como a **entrega final de FinOps** do projeto integrado (feito em grupo) — pede o cálculo do **TCO (Total Cost of Ownership)** mensal da arquitetura completa da Quantum Commerce em escala real de produção (não free tier), somando nove componentes no Azure Pricing Calculator: Blob Storage (10 TB, dividido entre Hot/Cool/Archive), Azure SQL Hyperscale, Cosmos DB, Azure AI Search Standard S1, Function App Premium EP1, Azure AI Services multi-service (Language + Speech + Vision em volume), Azure ML (workspace + endpoint 24/7), Application Insights e egress. Depois de somar o total mensal em dólar e converter para reais, os alunos identificam os três itens mais caros e propõem uma otimização com economia estimada para cada um (exemplos discutidos: trocar Sentiment Analysis por um LLM só se usado com inteligência, aplicar scale-to-zero num endpoint de ML que hoje roda 24/7, usar Azure Front Door em vez de CDN externa, ou voltar uma Function Premium para o plano Consumption se o cold start for aceitável). O exercício fecha comparando o cenário com Reserved Instances de 1 e 3 anos nos itens que rodam 24/7, e redigindo, em um parágrafo, como apresentar esses números ao CFO da empresa fictícia.

### 9. FinOps em IA: o custo do agente é consequência do prompt, não da arquitetura

O bloco final da aula muda a régua de novo: em infraestrutura tradicional, você paga por **capacidade provisionada** — uma VM custa o mesmo ociosa ou a 100% de uso, e otimizar é encaixar capacidade na demanda. Num agente de IA, você paga por **uso**, e o uso é decidido pelo próprio código do agente: cada linha do `agent.md` entra na conta de toda chamada, para sempre, porque o histórico de contexto volta inteiro a cada volta do loop. A frase que resume o bloco: em infraestrutura, o custo é consequência da arquitetura; num agente, o custo é consequência do prompt — "every engineer is FinOps now" fica literal aqui, porque quem escreve o system prompt está, na prática, escrevendo a fatura.

Três fontes de número sobre o mesmo agente não batem entre si, e a divergência é esperada, não um defeito:

| Fonte | Granularidade | Atraso | Serve para |
|---|---|---|---|
| Cost Management | Recurso/dia, por tag | Horas | Pagar e cobrar |
| Métricas do Foundry | Deployment/minuto | Minutos | Entender consumo |
| Application Insights | Por turno, em dólar estimado | 2 a 5 minutos | Decidir agora |

Regra prática: para decidir no dia a dia, vale o número da própria telemetria; para faturar de verdade, vale o número do provedor.

### 10. A unidade econômica do agente: custo por turno e token economics

A métrica que falta em qualquer FinOps clássico, e que só o código do próprio agente sabe calcular, é o **custo por turno**: custo médio por interação × turnos por usuário por dia × usuários × 30 dias. A recomendação é ler o **p95**, não a média — a média é o que se paga num dia normal, o p95 é o que se paga quando o uso muda. Tecnicamente, isso é feito agrupando os logs do Application Insights por `operation_Id` (um turno = uma cadeia de chamadas com o mesmo identificador), somando o custo estimado de cada chamada de modelo dentro daquele turno.

A alavanca mais invisível é o **histórico como custo**: cinco iterações de um loop carregando 3.000 tokens de histórico cada geram cerca de 15.000 tokens de entrada num único turno, porque o histórico completo — junto com `agent.md`, `memory.md` e a descrição de todas as ferramentas disponíveis — volta a cada nova volta do laço. A proporção entre tokens de entrada e de saída costuma ser de 20 para 1, e como entrada e saída têm preços diferentes, essa proporção é o que decide se vale mais a pena encurtar o prompt ou encurtar a resposta esperada. O parâmetro `EVA_MAX_ITERACOES`, apresentado inicialmente como proteção técnica contra loop infinito, é também, na prática, o teto de gasto de um único turno — e deve ser dimensionado com o p95 observado, não por chute.

### 11. As cinco alavancas de otimização e o equivalente das estratégias de desconto em IA

Da mais barata para a mais cara de aplicar, cinco alavancas de otimização de um agente foram apresentadas: **encurtar o prompt** (`agent.md`, `memory.md` e descrições de ferramentas entram em toda iteração — é o ajuste mais barato), **teto de iterações** (`EVA_MAX_ITERACOES` limitando o gasto máximo de um turno), **escolher o modelo certo** (right-sizing de IA — comparar antes/depois na mesma consulta), **scale-to-zero** (`min-replicas 0`, o contêiner do agente desaparece quando ninguém usa) e **cache de resposta** (token vindo de cache não consome capacidade paga). A única dessas cinco que o FinOps clássico de infraestrutura já ensinava é o scale-to-zero — as outras quatro nascem especificamente do prompt e do comportamento do agente.

A tabela clássica de estratégias de desconto de compute (Aula 6, seção 7) tem um equivalente direto no mundo de modelos de IA:

| Estratégia (infra) | Equivalente em IA | O que muda |
|---|---|---|
| Pay-as-you-go | Standard, pago por token | O modo padrão da Eva — sem compromisso, sem SLA de latência |
| Reserved Instances | PTU + Azure Reservations | Capacidade dedicada, US$/PTU/hora; reserva de 1 mês ou 1 ano — mas reserva **não garante capacidade**: primeiro cria o deployment e confirma a capacidade, só então compra |
| Spot | Batch assíncrono | Tarifa reduzida, serve para lote, não para chat interativo |
| Right-sizing | Modelo e prompt menores | A alavanca de sempre, e a mais barata de aplicar |
| — (sem equivalente em infra) | Prompt caching | Token que vem do cache não consome capacidade — não existe paralelo no mundo de infraestrutura tradicional |

Um alerta prático: PTU é caro se ficar ocioso — para o volume de uma aula ou de um piloto, o modo Standard (pago por token) é o correto.

### 12. Lab 3: FinOps na Eva — da régua à decisão

O último laboratório do curso aplica Inform e Optimize diretamente na Eva publicada pelo aluno. Primeiro, no Cost Management, agrupando por tag (`projeto`, depois `aluno`, depois `Service name`) para descobrir se o custo predominante foi do modelo ou da observabilidade; depois, checando cobertura de marcação via `az resource list` filtrando recursos sem a tag `projeto` (qualquer resultado ali é custo sem dono). Em seguida, uma consulta KQL no Application Insights (`eva-appi → Monitoring → Logs`) calcula custo médio, p95 e número médio de iterações por turno — e um resultado zerado é esperado por design: os preços nascem em zero de propósito, porque um número inventado em painel de custo é pior do que nenhum painel. A partir desses dados, o laboratório pede a projeção do custo mensal (com a média e com o p95, para expor o risco), o cálculo de quanto custa por mês cada parágrafo do `agent.md` (tokens ≈ caracteres ÷ 4, multiplicado por iterações médias, turnos por mês e preço de entrada), e a configuração dos dois controles do pilar Operate: um budget alert no grupo de recursos em 50/80/100%, e um alerta de `TokenTransaction` por hora — lembrando que um agente em loop não derruba nada, só gasta.

Na escala de maturidade Crawl/Walk/Run aplicada à própria Eva: **Crawl** (tags + budget alert) e **Walk** (dashboards + otimizações já aplicadas, como scale-to-zero e teto de iterações) estão completos; **Run** (chargeback + KPI + retrospectiva mensal) está pela metade — a tag `aluno` já permite chargeback e o custo por turno já é um KPI calculável, mas falta o ritual: alguém precisa abrir o painel todo mês e decidir algo a partir dele. É exatamente o ponto levantado no início da aula: a maioria das empresas para no Inform.

### 13. Fechamento da disciplina: recap das 6 aulas

A aula — e o curso — fecham com um resumo do que foi construído ao longo de 6 aulas e 5 entregas parciais + 1 entrega final: uma arquitetura cloud real para a Quantum Commerce, cobrindo fundamentos de nuvem, processamento serverless, cinco tools prontas para alimentar agentes de verdade, uma tool com Machine Learning, agentes de IA, e FinOps para fechar. As ferramentas praticadas ao longo do curso — Azure Cloud, Azure Machine Learning, Cloud Shell, Pricing Calculator, git, Terraform, Docker (sem build) e uma quantidade relevante de scripts shell — são apresentadas explicitamente não como exercício descartável de curso, mas como portfólio a ser levado para o resto do MBA e para a carreira.

---

## Material complementar — Terraform

### Terraform: criando máquinas na Azure

O artigo parte de uma pergunta prática: por que não simplesmente criar a infraestrutura clicando no console da Azure? A resposta é a mesma reforçada ao longo do curso — provisionar pelo console não deixa documentação do que existe, dificulta alterações seguras e impede recriar o mesmo ambiente rapidamente em outro contexto (por exemplo, replicar produção para homologação). O Terraform resolve isso descrevendo a infraestrutura como código, com uma vantagem central sobre simplesmente automatizar tudo via script bash: **idempotência** — rodar o mesmo código várias vezes sempre leva ao mesmo resultado final, sem risco de duplicar recursos ou deixar o ambiente num estado inconsistente por causa de uma falha não tratada no meio do script.

O artigo destaca uma particularidade da Azure frente a outros provedores: ao contrário da AWS, a Azure não entrega uma rede virtual padrão junto com a conta — é preciso criar explicitamente uma **VNet** (Virtual Network, equivalente ao conceito de VPC) para cada projeto, o que **isola** os recursos entre projetos diferentes e limita o raio de impacto caso um deles tenha um incidente de segurança. Os nomes dos recursos também mudam de provedor para provedor: uma máquina virtual que na AWS se chama `aws_instance` vira `azurerm_virtual_machine` no provider da Azure.

Na parte prática, o artigo monta um exemplo mínimo de VM na Azure, resource a resource: a VM (`azurerm_virtual_machine`, com nome, tamanho de família — ex. `Standard_DS1_v2` — e a imagem do sistema operacional), o disco do sistema operacional, o perfil de acesso (usuário/senha ou, como alternativa mais segura sugerida no próprio artigo, autenticação por chave SSH em vez de senha), o **Resource Group** que agrupa e isola todos os recursos do projeto, a **rede virtual** com seu bloco de IPs privados e ao menos uma subnet dentro dela, e por fim a **interface de rede** que conecta a VM a essa subnet. O artigo reforça uma boa prática de segurança citada em todas as aulas do curso: nunca deixar usuário e senha (ou chave) hardcoded no arquivo de configuração versionado — o ideal é externalizar esses valores como variáveis, preenchidas fora do repositório. Ao final, `terraform apply` cria toda essa infraestrutura de uma vez e `terraform destroy` a remove por completo — o mesmo ciclo de vida (init → plan → apply → destroy) praticado nos laboratórios desta disciplina.

Fonte: [Terraform: criando máquinas na Azure — Alura](https://www.alura.com.br/artigos/terraform-maquinas-na-azure)

### Criando o primeiro ambiente com o Terraform (AWS)

Este segundo artigo é mais introdutório e usa a AWS como provedor de exemplo, com o objetivo de criar três instâncias EC2 (o equivalente, na AWS, à VM da Azure) a partir de poucas linhas de código. O pré-requisito de ambiente é o mesmo em espírito do que se vê nos laboratórios da disciplina: ter a CLI do provedor de nuvem instalada e autenticada localmente (no caso, `aws configure`, informando Access Key, Secret Key, região padrão e formato de saída) e o binário do Terraform instalado.

A estrutura mínima de um projeto Terraform é apresentada de forma didática: um arquivo `main.tf` que começa declarando o **provider** (qual nuvem e qual região usar) e, em seguida, um bloco `resource` por recurso desejado. No exemplo do artigo, um único bloco `resource "aws_instance"` cria as três instâncias de uma vez usando o atributo `count = 3`, com os nomes das máquinas gerados dinamicamente a partir do índice do contador (`alura0`, `alura1`, `alura2`) — uma forma compacta de criar múltiplos recursos semelhantes sem repetir o bloco inteiro três vezes. Os demais atributos do recurso definem a imagem de sistema operacional (AMI), o tipo de instância (`t2.micro`, dentro do free tier da AWS) e o nome do par de chaves SSH usado para acessar a máquina depois de criada.

O artigo fecha reforçando o mesmo ciclo de comandos: `terraform init` (baixa os plugins do provider necessários), `terraform plan` (mostra o que será criado antes de executar, permitindo revisar) e `terraform apply` (efetivamente provisiona os recursos, pedindo confirmação explícita antes de prosseguir). É a mesma sequência praticada no laboratório da Aula 1 desta disciplina, aqui numa versão ainda mais enxuta e focada em um único tipo de recurso.

Fonte: [Criando o primeiro ambiente com o Terraform — Alura](https://www.alura.com.br/artigos/criando-o-primeiro-ambiente-com-terraform)
