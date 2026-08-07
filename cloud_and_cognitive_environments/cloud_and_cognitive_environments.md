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
