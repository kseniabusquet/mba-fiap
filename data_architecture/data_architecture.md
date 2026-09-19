# Data Architecture

## Sumário

- [Data Architecture](#data-architecture)
  - [Sumário](#sumário)
  - [Aula 1 — Introdução e Arquiteturas de Referência](#aula-1--introdução-e-arquiteturas-de-referência)
    - [1. Dado, informação e o papel do arquiteto de dados](#1-dado-informação-e-o-papel-do-arquiteto-de-dados)
    - [2. Tipos de dados e frameworks de referência (DAMA, TOGAF, Modelo Canônico)](#2-tipos-de-dados-e-frameworks-de-referência-dama-togaf-modelo-canônico)
    - [3. SGBD: histórico, tipos e ACID vs. BASE](#3-sgbd-histórico-tipos-e-acid-vs-base)
    - [4. Data Warehouse: Inmon, Kimball e o pipeline ETL](#4-data-warehouse-inmon-kimball-e-o-pipeline-etl)
    - [5. Data Lake: origens, os 3 Vs e a mecânica do Hadoop/HDFS](#5-data-lake-origens-os-3-vs-e-a-mecânica-do-hadoophdfs)
    - [6. Arquitetura de referência de dados (camadas)](#6-arquitetura-de-referência-de-dados-camadas)
    - [7. Data Lakehouse: Delta Lake, Iceberg e Hudi](#7-data-lakehouse-delta-lake-iceberg-e-hudi)
    - [8. Data Mesh](#8-data-mesh)
    - [9. Estudos de caso em sala: Mega Loja](#9-estudos-de-caso-em-sala-mega-loja)
    - [10. Exemplos reais](#10-exemplos-reais)
  - [Aula 2 — Bancos de Dados Relacionais e Colunares (NoSQL)](#aula-2--bancos-de-dados-relacionais-e-colunares-nosql)
    - [1. Origem e objetivos do modelo relacional](#1-origem-e-objetivos-do-modelo-relacional)
    - [2. Características do modelo relacional e o diagrama ER](#2-características-do-modelo-relacional-e-o-diagrama-er)
    - [3. SQL: DDL, DML, DCL e TCL](#3-sql-ddl-dml-dcl-e-tcl)
    - [4. Controle de sessões: lock, isolamento e deadlock](#4-controle-de-sessões-lock-isolamento-e-deadlock)
    - [5. Metadados e catálogo do sistema](#5-metadados-e-catálogo-do-sistema)
    - [6. Armazenamento: camada lógica e física](#6-armazenamento-camada-lógica-e-física)
    - [7. Stored procedures e triggers](#7-stored-procedures-e-triggers)
    - [8. Transações e o modelo ACID](#8-transações-e-o-modelo-acid)
    - [9. Laboratório SQL: modelagem assistida por IA — caso "Mega Loja / Armazém"](#9-laboratório-sql-modelagem-assistida-por-ia--caso-mega-loja--armazém)
    - [10. Origem e fundamentos dos bancos NoSQL](#10-origem-e-fundamentos-dos-bancos-nosql)
    - [11. Tipos de bancos NoSQL](#11-tipos-de-bancos-nosql)
    - [12. ACID vs. BASE e o Teorema de CAP](#12-acid-vs-base-e-o-teorema-de-cap)
    - [13. Bancos colunares: conceito e funcionamento](#13-bancos-colunares-conceito-e-funcionamento)
    - [14. Cassandra: origem, características e arquitetura](#14-cassandra-origem-características-e-arquitetura)
    - [15. Replicação e modelagem no Cassandra](#15-replicação-e-modelagem-no-cassandra)
    - [16. Consultas no Cassandra e o ALLOW FILTERING](#16-consultas-no-cassandra-e-o-allow-filtering)
    - [17. Laboratório prático com Cassandra](#17-laboratório-prático-com-cassandra)
    - [18. Encerramento e próximos passos](#18-encerramento-e-próximos-passos)
  - [Aula 3 — Bancos de Documentos (MongoDB) e Bancos de Grafos (Neo4j)](#aula-3--bancos-de-documentos-mongodb-e-bancos-de-grafos-neo4j)
    - [1. Bancos de documentos: características e o modelo JSON](#1-bancos-de-documentos-características-e-o-modelo-json)
    - [2. Estrutura do MongoDB: instância, banco, coleção e documento](#2-estrutura-do-mongodb-instância-banco-coleção-e-documento)
    - [3. Particionamento, replicação e o Teorema de CAP no MongoDB](#3-particionamento-replicação-e-o-teorema-de-cap-no-mongodb)
    - [4. Modelagem: embutir (embed) vs. referenciar](#4-modelagem-embutir-embed-vs-referenciar)
    - [5. Quando usar e quando evitar o MongoDB](#5-quando-usar-e-quando-evitar-o-mongodb)
    - [6. Laboratório prático: subindo um MongoDB e primeiros comandos](#6-laboratório-prático-subindo-um-mongodb-e-primeiros-comandos)
    - [7. Estudo de caso em sala: remodelando a Mega Loja para o MongoDB](#7-estudo-de-caso-em-sala-remodelando-a-mega-loja-para-o-mongodb)
    - [8. Origem dos bancos de grafos: teoria dos grafos e as pontes de Königsberg](#8-origem-dos-bancos-de-grafos-teoria-dos-grafos-e-as-pontes-de-königsberg)
    - [9. Neo4j: nós, rótulos, propriedades e relacionamentos](#9-neo4j-nós-rótulos-propriedades-e-relacionamentos)
    - [10. Características do Neo4j e sua classificação no Teorema de CAP](#10-características-do-neo4j-e-sua-classificação-no-teorema-de-cap)
    - [11. Cypher: a linguagem de consulta do Neo4j](#11-cypher-a-linguagem-de-consulta-do-neo4j)
    - [12. Aplicações de bancos de grafos](#12-aplicações-de-bancos-de-grafos)
    - [13. Laboratório prático com Neo4j e o desafio de migração para grafos](#13-laboratório-prático-com-neo4j-e-o-desafio-de-migração-para-grafos)
    - [14. Encerramento e transição para os bancos vetoriais](#14-encerramento-e-transição-para-os-bancos-vetoriais)
  - [Aula 4 — Bancos Vetoriais para Agentes (Operação Q)](#aula-4--bancos-vetoriais-para-agentes-operação-q)
    - [1. Contexto: da gestão de dados à gestão de conhecimento — o cenário Quantum Finance](#1-contexto-da-gestão-de-dados-à-gestão-de-conhecimento--o-cenário-quantum-finance)
    - [2. Escalares, vetores e embeddings](#2-escalares-vetores-e-embeddings)
    - [3. Regras de infraestrutura do embedding e o lugar do RAG](#3-regras-de-infraestrutura-do-embedding-e-o-lugar-do-rag)
    - [4. Busca por similaridade: distância de cosseno e KNN](#4-busca-por-similaridade-distância-de-cosseno-e-knn)
    - [5. A escada de maturidade de dados para IA](#5-a-escada-de-maturidade-de-dados-para-ia)
    - [6. Anatomia de um banco vetorial e o pgvector](#6-anatomia-de-um-banco-vetorial-e-o-pgvector)
    - [7. Chunking: como fatiar os documentos](#7-chunking-como-fatiar-os-documentos)
    - [8. Modelagem do agente: tabela de conhecimento, tabela de memória e governança](#8-modelagem-do-agente-tabela-de-conhecimento-tabela-de-memória-e-governança)
    - [9. Laboratório guiado: estruturando o banco da Operação Q](#9-laboratório-guiado-estruturando-o-banco-da-operação-q)
    - [10. Segurança e isolamento: o vazamento de memória entre clientes](#10-segurança-e-isolamento-o-vazamento-de-memória-entre-clientes)
    - [11. Busca vetorial em escala: recall, P95 e a necessidade de índices](#11-busca-vetorial-em-escala-recall-p95-e-a-necessidade-de-índices)
    - [12. HNSW: estrutura, parâmetros e custo de memória](#12-hnsw-estrutura-parâmetros-e-custo-de-memória)
    - [13. IVFFlat e quantização de vetores](#13-ivfflat-e-quantização-de-vetores)
    - [14. Ecossistema de bancos vetoriais: FAISS, pgvector, Pinecone, Weaviate e Qdrant](#14-ecossistema-de-bancos-vetoriais-faiss-pgvector-pinecone-weaviate-e-qdrant)
    - [15. Como escolher o índice e o banco certo](#15-como-escolher-o-índice-e-o-banco-certo)
    - [16. Laboratório prático: dimensionando índices por SLA](#16-laboratório-prático-dimensionando-índices-por-sla)
    - [17. Encerramento e entrega](#17-encerramento-e-entrega)
  - [Aula 5 — Integração de Dados para Agentes (Os Dutos do Q)](#aula-5--integração-de-dados-para-agentes-os-dutos-do-q)
    - [1. Por que a fundação de dados sustenta os agentes: três falhas reais](#1-por-que-a-fundação-de-dados-sustenta-os-agentes-três-falhas-reais)
    - [2. Os três paradigmas de ingestão: Batch, CDC e API](#2-os-três-paradigmas-de-ingestão-batch-cdc-e-api)
    - [3. Batch: a janela de obsolescência](#3-batch-a-janela-de-obsolescência)
    - [4. ETL vs. ELT: onde a transformação acontece](#4-etl-vs-elt-onde-a-transformação-acontece)
    - [5. Bronze, Silver, Gold: a jornada do dado e o debate sobre governança (SOR, SOT, SPEC)](#5-bronze-silver-gold-a-jornada-do-dado-e-o-debate-sobre-governança-sor-sot-spec)
    - [6. Metadados e contratos de dados](#6-metadados-e-contratos-de-dados)
    - [7. Schema drift: o que fazer quando o esquema muda sem avisar](#7-schema-drift-o-que-fazer-quando-o-esquema-muda-sem-avisar)
    - [8. Idempotência e determinismo](#8-idempotência-e-determinismo)
    - [9. Time travel e auditoria de inferência](#9-time-travel-e-auditoria-de-inferência)
    - [10. O ferramental: do laboratório à produção](#10-o-ferramental-do-laboratório-à-produção)
    - [11. Agent 1, o Construtor, e o conceito de agent harness](#11-agent-1-o-construtor-e-o-conceito-de-agent-harness)
    - [12. Missão 1: o duto batch (laboratório)](#12-missão-1-o-duto-batch-laboratório)
    - [13. Cursor e efeito líquido](#13-cursor-e-efeito-líquido)
    - [14. LGPD e o padrão outbox: o caso Marina](#14-lgpd-e-o-padrão-outbox-o-caso-marina)
    - [15. Menor privilégio: o agente invoca, a view lê](#15-menor-privilégio-o-agente-invoca-a-view-lê)
    - [16. Model Context Protocol (MCP) e os três agentes trabalhando juntos](#16-model-context-protocol-mcp-e-os-três-agentes-trabalhando-juntos)
    - [17. Missão 2, o futuro dos pipelines (YAML como padrão) e encerramento da disciplina](#17-missão-2-o-futuro-dos-pipelines-yaml-como-padrão-e-encerramento-da-disciplina)

## Aula 1 — Introdução e Arquiteturas de Referência

### 1. Dado, informação e o papel do arquiteto de dados

A aula abre distinguindo **dado** (registro bruto, sem contexto — ex.: "42") de **informação** (dado interpretado em contexto — ex.: "42 anos"). Arquitetura de dados é a disciplina que define como esses dados são estruturados, armazenados, integrados, processados e disponibilizados para consumo, equilibrando três forças que aparecem repetidamente ao longo da aula: volume de dados, velocidade/tempestividade de acesso e custo de manter a plataforma.

O papel do arquiteto de dados foi descrito não apenas como técnico, mas como alguém que precisa justificar a plataforma para o negócio: estimar retorno, mapear a capacitação do time atual, considerar dependência de consultoria externa e antecipar pontos de falha ao integrar um ambiente on-premise com a nuvem. Essa cobrança "não técnica" (retorno sobre investimento, capacitação de equipe, manutenibilidade) voltou como tema central no primeiro estudo de caso da aula.

### 2. Tipos de dados e frameworks de referência (DAMA, TOGAF, Modelo Canônico)

Os slides classificam os dados em três categorias, com implicações diretas de arquitetura:

| Tipo | Característica | Exemplos |
|---|---|---|
| **Estruturado** | Schema fixo, organizado em linhas/colunas | Tabelas de banco relacional, planilhas |
| **Semiestruturado** | Tem alguma organização (tags, chaves), mas sem schema rígido | JSON, XML, logs |
| **Não estruturado** | Sem estrutura predefinida | Imagens, vídeos, áudio, texto livre, posts de rede social |

Dois frameworks de referência foram citados como pano de fundo para governança e arquitetura corporativa de dados: **DAMA** (DAMA-DMBOK, o corpo de conhecimento de referência para gestão de dados — qualidade, governança, modelagem, segurança) e **TOGAF** (framework de arquitetura corporativa mais amplo, que trata arquitetura de dados como uma das camadas dentro da arquitetura de negócio/aplicação/tecnologia). O **Modelo Canônico** foi apresentado como a prática de definir um formato de dado comum e neutro entre sistemas heterogêneos, para que a integração entre sistemas não dependa de tradução ponto a ponto entre cada par de formatos.

### 3. SGBD: histórico, tipos e ACID vs. BASE

Um **SGBD** (Sistema de Gerenciamento de Banco de Dados) é o software que administra a criação, consulta, atualização e controle de acesso a um banco de dados. A aula percorreu a evolução histórica dos modelos de banco de dados:

1. **Hierárquico** — dados em estrutura de árvore (um pai, vários filhos); rígido, pouco flexível para consultas ad hoc.
2. **Em rede** — generalização do hierárquico, permitindo múltiplos relacionamentos entre registros; ainda navegacional (a aplicação precisa "andar" pelos ponteiros).
3. **Orientado a objetos** — dados representados como objetos, próximos da forma como são manipulados no código; teve adoção limitada fora de nichos específicos.
4. **Relacional** — dados em tabelas com relacionamentos definidos por chaves, consultados via SQL declarativo; tornou-se o padrão dominante a partir dos anos 1970/80.
5. **NoSQL** — surge décadas depois, como resposta às limitações do relacional para volume, velocidade e variedade de dados na era da internet em escala (mais detalhado na seção do Data Lake).

O **ranking do site db-engines.com** foi citado como referência viva para acompanhar popularidade de SGBDs no mercado (histórico dominado por Oracle, MySQL, SQL Server, com PostgreSQL e MongoDB ganhando posição nos últimos anos).

A diferença central entre os dois grandes paradigmas atuais está nas garantias que cada um oferece:

| Garantia | Relacional (ACID) | NoSQL (BASE) |
|---|---|---|
| **A**tomicidade / **B**asically Available | Transação é tudo-ou-nada | Sistema disponível na maior parte do tempo, mesmo sob falha parcial |
| **C**onsistência / **S**oft state | Todo mundo enxerga o mesmo dado a qualquer momento | Estado pode variar temporariamente entre réplicas |
| **I**solamento / **E**ventual consistency | Transações concorrentes não se interferem | Consistência é alcançada eventualmente, não instantaneamente |
| **D**urabilidade | Dado gravado sobrevive a falhas | Idem, mas com tolerância maior a inconsistência temporária em troca de disponibilidade e escala |

O **Teorema CAP** (Consistência, Disponibilidade, Tolerância a Partição — escolha 2 de 3 sob falha de rede) foi trazido pela turma como framework complementar para justificar quando optar por NoSQL: em um sistema distribuído, não é possível garantir simultaneamente consistência e disponibilidade total durante uma partição de rede, então cada banco NoSQL faz uma escolha de qual sacrificar.

### 4. Data Warehouse: Inmon, Kimball e o pipeline ETL

O **Data Warehouse (DW)** foi apresentado a partir das duas escolas clássicas de modelagem:

- **Bill Inmon** — abordagem *top-down*: primeiro constrói-se um DW corporativo único, normalizado, e depois derivam-se Data Marts departamentais a partir dele. Prioriza consistência e uma única fonte de verdade.
- **Ralph Kimball** — abordagem *bottom-up*: constrói-se Data Marts por área de negócio primeiro (modelados em **Star Schema** — tabela fato central cercada de tabelas dimensão), que juntos formam o DW. Prioriza velocidade de entrega e proximidade com a necessidade do negócio.

Um Data Warehouse, segundo a definição clássica de Inmon usada nos slides, é **orientado por assunto** (organizado por tema de negócio, não por sistema de origem), **integrado** (dados de múltiplas fontes conciliados em um formato único), **não volátil** (uma vez carregado, o dado não é sobrescrito — apenas acumulado) e **variante no tempo** (mantém histórico, permitindo análise de tendência).

O fluxo que alimenta o DW é o **ETL** (Extract, Transform, Load): extrai dos sistemas transacionais, transforma (limpeza, padronização, agregação) e carrega no modelo dimensional do DW. Esse pipeline serve tipicamente cargas de trabalho **OLAP** (Online Analytical Processing — consultas analíticas, agregadas, sobre grandes volumes históricos), em contraste com os sistemas de origem, que são **OLTP** (Online Transactional Processing — muitas transações pequenas, de leitura e escrita, otimizadas para consistência imediata).

Os **Data Marts** foram descritos como subconjuntos do DW recortados por área de negócio (vendas, marketing, financeiro), podendo ser construídos de cima para baixo (recorte do DW corporativo, linha Inmon) ou de baixo para cima (unidade básica que compõe o DW, linha Kimball).

### 5. Data Lake: origens, os 3 Vs e a mecânica do Hadoop/HDFS

O **Data Lake** nasce da limitação do DW tradicional diante do crescimento explosivo de dados não estruturados e semiestruturados na era da internet. As origens técnicas remontam a papers do Google — **GFS** (Google File System) e **MapReduce** — que inspiraram a criação do **Hadoop** como implementação open source equivalente.

Os **3 Vs** que caracterizam o cenário de Big Data que motivou o Data Lake:

| V | Significado |
|---|---|
| **Volume** | Escala de dados muito além da capacidade prática de um DW relacional tradicional |
| **Velocidade** | Taxa de geração e necessidade de ingestão dos dados (batch vs. quase tempo real vs. streaming) |
| **Variedade** | Mistura de dados estruturados, semiestruturados e não estruturados na mesma plataforma |

A arquitetura do **HDFS** (Hadoop Distributed File System) foi explicada com um exemplo prático em sala: ao armazenar um arquivo (por exemplo, 10 GB), o HDFS o particiona em blocos de **128 MB** cada. Cada bloco é distribuído para uma máquina (**DataNode**) diferente e, em seguida, replicado com **fator de replicação 3** — ou seja, cada bloco existe em três DataNodes diferentes, garantindo tolerância a falha de máquina sem perda de dado. O **NameNode** é o componente central que mantém o mapa de qual bloco está em qual DataNode (os metadados), sendo consultado toda vez que um cliente precisa localizar ou reconstruir um arquivo.

O **MapReduce** é o modelo de processamento distribuído associado: a etapa **Map** aplica uma função em paralelo a cada partição do dado (perto de onde o dado está armazenado — "o processamento é executado onde o armazenamento está", como resumiu o professor); a etapa **Shuffle/Sort** reorganiza e agrupa os resultados intermediários por chave; e a etapa **Reduce** agrega os resultados finais.

Na nuvem, esse mesmo padrão de distribuição e redundância se traduz em conceitos de infraestrutura equivalentes: **regiões** e **zonas de disponibilidade** — AWS usa Availability Zones (AZs), GCP usa Zones, Azure usa Availability Zones — permitindo que serviços de Data Lake gerenciados (S3, GCS, Blob Storage) apliquem o mesmo princípio de replicação geográfica que o HDFS aplica entre máquinas de um cluster on-premise.

### 6. Arquitetura de referência de dados (camadas)

Os slides trazem um framework de referência genérico (aplicável a qualquer stack — on-premise, Azure, AWS ou GCP) organizado em camadas horizontais:

1. **Ingestão** — camada de entrada, batch ou streaming, trazendo dados de sistemas transacionais, APIs, redes sociais, arquivos, sensores.
2. **Armazenamento**, subdividido em três zonas de maturidade crescente:
   - **Raw** (bruta) — dado como chegou, sem transformação, preservado para auditoria e reprocessamento.
   - **Harmonized** (harmonizada) — dado limpo, padronizado, com schema aplicado, mas ainda granular.
   - **Curated** (curada) — dado agregado, modelado para consumo direto por análises e aplicações.
3. **Processamento** — motores de transformação/agregação que movem o dado entre as zonas de armazenamento (Spark, Databricks, Dataflow, etc.).
4. **Acesso** — camada de exposição do dado já processado (APIs, consultas SQL, feature stores).
5. **Visualização** — ferramentas de BI e dashboards consumindo a camada de acesso.

Transversal a essas camadas, uma camada de **Operacionalização** cobre governança, segurança, catalogação, linhagem (lineage) e monitoramento — presente em todas as etapas do fluxo, não apenas ao final.

### 7. Data Lakehouse: Delta Lake, Iceberg e Hudi

O **Data Lakehouse** combina a flexibilidade e o custo de armazenamento do Data Lake com garantias transacionais (ACID) tradicionalmente exclusivas do mundo de bancos relacionais e Data Warehouses — resolvendo o problema central discutido no segundo estudo de caso da aula: dados chegando de fontes diferentes ao Data Lake, sem consistência garantida entre eles.

Três implementações de tabela transacional sobre Data Lake foram apresentadas:

- **Delta Lake** (Databricks) — organiza o dado no padrão de camadas **bronze** (raw), **silver** (limpa/harmonizada) e **gold** (curada/agregada para consumo), com suporte a updates, deletes e merges com garantia ACID sobre arquivos Parquet, além de versionamento (time travel).
- **Apache Iceberg** — formato de tabela aberto, focado em performance de metadados em tabelas muito grandes, evolução de schema sem reescrever dados, e portabilidade entre motores de processamento diferentes.
- **Apache Hudi** — formato de tabela com foco forte em ingestão incremental e upserts eficientes, popular em cenários de streaming/CDC (Change Data Capture).

O professor reforçou o risco do **Data Swamp** — o Data Lake que, sem governança, curadoria e catalogação, vira um repositório de dados não confiáveis e não descobertos ("passei o leite e virou pântano", na analogia usada em sala): volume de dados sem qualidade e sem contexto não é ativo, é passivo.

### 8. Data Mesh

O **Data Mesh**, proposto por **Zhamak Dehghani**, foi apresentado como uma mudança de paradigma organizacional, não apenas técnica: em vez de centralizar todo o dado em uma plataforma única gerida por um time central de dados, cada domínio de negócio passa a ser dono e responsável pelos seus próprios dados como produto.

Os quatro princípios do Data Mesh:

1. **Domain ownership** (propriedade por domínio) — cada time de domínio de negócio é dono dos seus dados, não um time central de dados.
2. **Self-service data platform** (plataforma self-service) — infraestrutura comum que permite a cada domínio publicar e consumir dados sem depender de um time central para cada tarefa.
3. **Data as a product** (dado como produto) — cada conjunto de dados publicado por um domínio deve ter qualidade, documentação, SLA e descobribilidade como um produto de verdade, com "consumidores" internos.
4. **Federated computational governance** (governança federada e computacional) — padrões e políticas de governança (segurança, qualidade, compliance) são definidos de forma federada entre os domínios, mas aplicados de forma automatizada/computacional, não manual.

**Vantagens** discutidas: escalabilidade organizacional (o time central de dados deixa de ser gargalo), maior proximidade entre quem conhece o dado e quem o modela, e maior velocidade de entrega por domínio. **Desvantagens**: exige maturidade organizacional alta (nem toda empresa tem times de domínio prontos para essa responsabilidade), risco de duplicação e inconsistência entre domínios sem uma governança federada bem implementada, e maior complexidade de coordenação entre plataformas self-service.

### 9. Estudos de caso em sala: Mega Loja

A aula usou dois exercícios em grupo com o mesmo cenário fictício — a **Mega Loja**, uma varejista online — para forçar a turma a tomar decisões de arquitetura sob restrição real.

**Caso 1 — do Data Warehouse ao streaming.** Ponto de partida: a Mega Loja já opera um Data Warehouse tradicional (tabelas de vendas, inventário, cliente), alimentando relatórios semanais/mensais e consultas analíticas sobre desempenho de produto e estoque. Surge uma nova demanda de negócio: implementar marketing personalizado *customer centric*, o que exige analisar comportamento do usuário em tempo real, vindo de múltiplas fontes novas (redes sociais, navegação do site, cliques) — não apenas do sistema interno. A turma foi provocada a listar os fatores mais relevantes para redesenhar a arquitetura, e levantou: volume de dados, tempestividade/velocidade, qualidade e normalização de dados vindos de fontes heterogêneas, e rastreabilidade. O professor então ampliou a discussão para fatores não puramente técnicos que um arquiteto precisa considerar: capacidade do time atual de construir pipelines para dados não estruturados, disponibilidade da equipe (mesmo capacitada, pode estar alocada em outros projetos), dependência de consultoria externa (rápida para implantar, mas custosa para manter depois que sai), retorno sobre o investimento perante o negócio, e a complexidade de conectar um ambiente atualmente on-premise a uma nuvem, incluindo os pontos de falha que essa integração introduz. Um exemplo real trazido por um aluno: um formulário de cadastro de 9 etapas causava abandono; capturar cada etapa via webhook para o S3 permitiu identificar em qual etapa o cliente desistia (churn) e simplificar o formulário — cruzando esse dado de streaming com dados de rede social e Google Analytics para entender retenção.

**Caso 2 — inconsistência entre fontes no Data Lake.** Ponto de partida: a Mega Loja já implementou o Data Lake, resolvendo as questões do primeiro caso, armazenando transações, inventário, cliente, redes sociais, logs e navegação. Novo problema: inconsistência de dados entre as diferentes fontes armazenadas — dados de vendas do sistema não batendo com os dados de vendas registrados no mês, discrepância entre níveis de estoque no sistema de inventário e o que é reportado nas interações com clientes, e cadastro de cliente diferente entre canais (loja física, site, redes sociais) não sincronizado. O professor conectou explicitamente esse cenário ao risco de **Data Swamp** citado anteriormente. Divididos em grupos, os alunos discutiram prós e contras de possíveis soluções; os pontos que emergiram da discussão incluíram a necessidade de um pipeline de ETL como parte da solução (mas não a solução completa por si só — "ele é o combo, é parte da solução, não é o que resolve"), a necessidade de que uma atualização seja replicada de forma consistente independentemente da fonte de origem, e a importância de alinhar critérios e definições comuns entre os times/fontes (voltando à ideia do Modelo Canônico da seção 2) antes de tentar resolver o problema apenas com mais ferramenta.

### 10. Exemplos reais

Os slides trouxeram arquiteturas de referência de empresas reais para ilustrar os conceitos em produção, incluindo os pipelines de dados da **Netflix** (arquitetura de streaming de eventos e Data Lake em escala, sustentando recomendação e analytics) e da **Uber** (arquitetura de ingestão e processamento de dados de geolocalização e transações em tempo real). Também foram mencionadas ferramentas de nuvem para o ecossistema analítico do Google Cloud — **BigQuery** e **Dataflow** (com interface visual "drag and drop" para montar pipelines de ETL) — e o **Looker** como ferramenta de visualização/BI da GCP.

## Aula 2 — Bancos de Dados Relacionais e Colunares (NoSQL)

Aula ministrada pelo Prof. Leandro Mendes, em formato online, com cerca de 4h de duração. A aula abre retomando rapidamente o conteúdo da Aula 1 (Data Warehouse, Data Lake, Lakehouse, Data Mesh) e segue o plano: aprofundar bancos relacionais (com laboratório prático em SQL), depois entrar em bancos NoSQL com foco em colunares e prática com Cassandra.

### 1. Origem e objetivos do modelo relacional

Antes do modelo relacional, os dados viviam em arquivos sequenciais ou em bancos hierárquicos (anos 60/70) — navegacionais, sem padronização nem integridade formal, com cada aplicação definindo sua própria estrutura. Em 1970, **Edgar F. Codd**, pesquisador da IBM, propôs o modelo relacional: dados organizados em tabelas com estrutura predefinida, relacionamentos formais entre entidades e uma linguagem declarativa (SQL) para consulta e manipulação.

O modelo relacional resolve três problemas centrais:

- **Integridade** — regras que garantem que o dado seja válido, consistente e respeite as regras de negócio.
- **Independência** — antes dos bancos relacionais, a aplicação acumulava dois papéis: cuidar dos dados *e* das funcionalidades. O banco relacional separa a gestão do dado da camada de aplicação/processamento.
- **Padronização** — um modelo e uma linguagem comuns, entendidos por mais de uma aplicação, tornam o dado mais simples de acessar, consultar e utilizar.

### 2. Características do modelo relacional e o diagrama ER

O modelo relacional é **estruturado**: o esquema é definido *antes* da inserção do dado (schema-on-write), cada tabela tem colunas com tipos fixos, e dado fora desse esquema simplesmente não entra. As **chaves primária (PK)** e **estrangeira (FK)** são o mecanismo que garante unicidade e integridade referencial — um registro de produto, por exemplo, se relaciona a um único item de estoque, não a mais de um. As propriedades **ACID** garantem confiabilidade mesmo sob falhas ou acesso concorrente (detalhadas na seção 9). E o **SQL**, padronizado pela ISO/ANSI e implementado (com pequenas variações) por praticamente todos os SGBDs relacionais, é a linguagem declarativa que amarra tudo isso.

No diagrama de modelagem, os elementos centrais são: **entidade** (um objeto do mundo real sobre o qual se quer guardar dado — produto, cliente, uma ação como venda ou locação), **atributo** (as propriedades que descrevem a entidade), **chave primária** (identifica unicamente cada registro), **chave estrangeira** (referencia e conecta entidades diferentes) e **cardinalidade** (a natureza do relacionamento — um-para-um, um-para-muitos, muitos-para-muitos). Esse tipo de diagrama tem dois nomes técnicos que aparecem na prática: **MER** (Modelo de Entidade e Relacionamento, o modelo em si) e **DER** (Design/Diagrama de Entidade e Relacionamento, o desenho que antecede o modelo) — e um apelido bem mais popular entre times de dados: **"diagrama pé de galinha"**, por causa dos tracinhos usados para marcar a cardinalidade (o "pezinho" quando é "muitos", o traço simples quando é "um").

### 3. SQL: DDL, DML, DCL e TCL

Apesar do padrão ANSI, cada SGBD tem pequenas variações de sintaxe (Oracle e SQL Server, por exemplo, diferem em alguns comandos e funções), mas todos seguem os mesmos quatro grandes blocos da linguagem:

| Categoria | Função | Comandos |
|---|---|---|
| **DDL** (Data Definition Language) | Cria e gerencia a estrutura do banco | CREATE, ALTER, TRUNCATE, DROP, DESCRIBE, RENAME |
| **DML** (Data Manipulation Language) | Manipula os dados propriamente ditos | INSERT, UPDATE, DELETE, SELECT |
| **DCL** (Data Control Language) | Controla acesso e permissões | GRANT, REVOKE |
| **TCL** (Transaction Control Language) | Controla o início/fim de transações | BEGIN, COMMIT, ROLLBACK |

Um ponto levantado em aula: o SELECT entra no DML — o que soa estranho para quem pensa em DML só como "escrita" — porque, na prática, uma consulta também é uma forma de manipular/visualizar o dado de uma maneira específica.

### 4. Controle de sessões: lock, isolamento e deadlock

Como o banco fica em posição central recebendo conexões de múltiplas aplicações e usuários simultaneamente, ele precisa garantir que a concorrência não corrompa nem gere inconsistência. Três mecanismos centrais:

- **Lock** — o banco bloqueia um conjunto de linhas/registros durante uma operação, impedindo que outra sessão veja ou altere um dado que ainda não está atualizado. É, na prática, o CAP theorem em ação no dia a dia: o banco abre mão de disponibilidade momentânea para garantir consistência.
- **Isolamento de transações** — define o quanto uma transação em andamento é visível para outras sessões, configurável por nível (*read uncommitted*, *read committed*, *repeatable read*, *serializable*).
- **Deadlock** — quando duas sessões se bloqueiam mutuamente, cada uma esperando um recurso que a outra segura, e nenhuma consegue avançar. Normalmente cabe ao DBA identificar e "matar" manualmente uma das sessões para destravar a outra — uma situação que, na experiência do professor, acontece com mais frequência do que se gostaria.

### 5. Metadados e catálogo do sistema

**Metadado** é o dado que descreve a estrutura do banco — "dado sobre o dado". Todo SGBD mantém um catálogo/dicionário com: estrutura de cada tabela (colunas, tipos, constraints), índices e suas estatísticas de uso, usuários/permissões/roles, sessões ativas e queries em execução, e parâmetros de configuração do servidor. Um lembrete prático levantado em aula: quem já escreveu pipeline e "levou bronca do DBA" por não encerrar a sessão ao final do processamento sabe que isso consome recursos e gera esse tipo de metadado de sessão. Essas tabelas de sistema são consultáveis via SQL e variam de nome por SGBD: **INFORMATION_SCHEMA** no MySQL, **pg_catalog** no PostgreSQL, **ALL_TABLES**/**DBA_OBJECTS** no Oracle.

### 6. Armazenamento: camada lógica e física

O SGBD abstrai o armazenamento físico da aplicação, mas internamente organiza tudo em estruturas específicas: **tablespaces/datafiles** (arquivos físicos que guardam tabelas e índices), **redo log / WAL** (Write-Ahead Log — registro sequencial de toda operação antes de ser aplicada ao dado, usado para recovery em caso de falha; Oracle chama isso de redo log, enquanto o Postgres trabalha com o conceito de before/after image, mas o princípio é essencialmente o mesmo), **buffer pool** (área de memória RAM que mantém páginas de dado acessadas com frequência, reduzindo I/O em disco) e **índices** (tipicamente B-tree, que aceleram consultas ao custo de espaço e overhead de escrita).

Essa separação entre **nível lógico** (a visão abstrata, legível para humanos — entidades, tabelas, atributos) e **nível físico** (tablespaces, logs, buffer pool, índices, e por fim o sistema operacional gerenciando o dado persistido em disco) é um dos princípios centrais do modelo relacional: a aplicação opera sobre tabelas, não sobre arquivos.

### 7. Stored procedures e triggers

**Stored procedures** são rotinas armazenadas e executadas diretamente pelo SGBD, escritas em linguagens procedurais (PL/SQL no Oracle, T-SQL no SQL Server, PL/pgSQL no PostgreSQL). Na prática, cumprem um papel parecido ao de um pipeline: ao invés de subir um Airflow e escrever a lógica em Python/Spark, escreve-se a lógica como uma procedure, que fica armazenada, agendada e gerenciada pelo próprio banco. Vantagens: encapsulam regra de negócio (reduzindo tráfego de rede e garantindo consistência independente do cliente que acessa), são reutilizáveis, e permitem controle de acesso granular (dar acesso à procedure sem expor as tabelas subjacentes). Usos típicos: processamento em batch, importação de dados, integrações, cálculos complexos sobre grandes volumes. O trade-off: lógica dentro do banco é mais difícil de versionar, testar de forma automatizada e portar entre SGBDs diferentes — mesmo assim, ambientes com um core fortemente relacional ainda usam procedures em larga escala para resolver esse tipo de problema.

**Triggers (gatilhos)** são rotinas disparadas automaticamente pelo SGBD em resposta a um evento de manipulação de dado (INSERT, UPDATE, DELETE). Podem ser **BEFORE** (executam antes da operação que os disparou, úteis para validar/transformar o dado antes de persistir) ou **AFTER** (executam depois, úteis para auditoria ou propagação de mudanças), e configuráveis por granularidade (**FOR EACH ROW** ou por statement). Usos típicos: auditoria de alterações, atualização automática de campos de controle (created_at, updated_by), propagação de eventos para outras tabelas. O trade-off central: triggers executam de forma **implícita** — quem está fazendo um INSERT simples não tem visibilidade de que há lógica adicional sendo disparada por trás, o que eleva o custo de manutenção e depuração à medida que o sistema cresce em complexidade.

Um exemplo real trazido em aula para ilustrar esse risco: o modelo de dados do **SAP**. O SAP é um ERP alemão, muito bem estruturado e consistente — mas, ao ser localizado para a legislação fiscal/contábil brasileira (bem diferente da alemã), exige customização pesada, que historicamente entra via **tabelas "Z"** (prefixo que marca tabelas customizadas). O resultado é um modelo gigantesco e complexo, com tantos triggers, procedures e tabelas customizadas que existe todo um mercado especializado de desenvolvedores **ABAP** ganhando bem justamente para lidar com essa complexidade — um lembrete de que, quanto maior e mais crítico o sistema, mais parcimônia é necessária na hora de criar gatilhos e procedures.

### 8. Transações e o modelo ACID

Uma **transação** é uma unidade lógica de trabalho — uma ou mais operações que devem ser executadas de forma atômica, tudo ou nada. As propriedades ACID, já citadas na Aula 1, ganham aqui o contexto prático de transação:

- **Atomicidade** — a transação é realizada por completo ou não é realizada.
- **Consistência** — leva o banco de um estado válido a outro, respeitando todas as constraints e relações envolvidas.
- **Isolamento** — liga diretamente ao lock: o dado fica indisponível durante a transação, e transações concorrentes não devem interferir entre si.
- **Durabilidade** — uma vez feito o commit, a transação persiste mesmo diante de falha (queda de energia, por exemplo); o resultado final é sempre commit (atualiza) ou rollback (reverte ao estado anterior).

### 9. Laboratório SQL: modelagem assistida por IA — caso "Mega Loja / Armazém"

**Cenário.** Uma rede de varejo opera um armazém central com múltiplos departamentos; toda a operação de estoque precisa ser registrada em um modelo relacional que garanta integridade entre os dados de inventário e as movimentações. O professor fornece a estrutura base: `departamento` (id_departamento PK, nome, responsavel), `invent_mestre` (id_item PK, codigo_sku, descricao, id_departamento FK, unidade_medida, preco_custo) e `transac_mestre` (id_transacao PK, id_item FK, data_transacao, tipo, quantidade, origem_destino).

**Tarefa.** Cada grupo escolhe um departamento (comercial, backoffice, supply chain, expedição, eletrônicos etc.), desenha o modelo de dados necessário e usa IA generativa para acelerar a geração dos scripts de criação (DDL) e população (DML) — mas, como o professor reforçou, "o papel de vocês como arquiteto não muda: a IA acelera, mas não substitui". A tabela do departamento precisa se conectar à estrutura base via chave estrangeira, e o passo final é pedir à IA pelo menos 10 registros de INSERT simulando movimentações de entrada e saída consistentes com os saldos.

**O que avaliar no resultado da IA:** se a FK está corretamente referenciando `invent_mestre`, se os atributos fazem sentido para o tipo de produto, se os tipos de dado são adequados, e se algo relevante ficou de fora.

**Resultados discutidos em sala** ilustram bem esse papel de revisão crítica:

- O grupo do **departamento de expedição** começou com a IA modelando uma relação 1-para-1 entre expedição e item; ao explicar que uma expedição pode conter vários itens (e um item pode aparecer em várias expedições), a IA corrigiu para 1-para-N/N-para-1 e propôs uma tabela intermediária de relacionamento (`expedicao_item`). A IA também percebeu, sozinha, que faltava um campo de quantidade em estoque em `invent_mestre` para que as movimentações fizessem sentido, e adicionou atributos específicos do domínio (tipo de embalagem, peso bruto, dimensões, código de barras, local de separação, tipo de transporte, prazo de expedição).
- No **departamento de eletrônicos** (feito direto no Colab), um aluno identificou um gap real de modelagem por conta própria: se `invent_mestre` guarda só o preço atual e as transações referenciam esse mesmo campo, o histórico de preço fica defasado quando o valor do produto muda. O professor confirmou que é uma situação bem comum e conectou com a solução clássica de BI — manter uma dimensão de mudança lenta (slowly changing dimension) ou registrar o preço praticado em cada transação, em vez de depender só do valor atual.
- Outro grupo (**departamento comercial**) usou um agente de IA para gerar não só o SQL, mas todo um ambiente Docker Compose com o schema e as consultas analíticas prontas, subindo o banco em container e conectando via DBeaver.

**Setup do laboratório**, com duas opções:

- **Opção A — SQLite no Google Colab**: sem instalação, sem conta, execução incremental em memória (`sqlite3.connect(':memory:')`), habilitando chaves estrangeiras (`PRAGMA foreign_keys = ON`), executando o script com `conn.executescript(...)` e consultando com `pd.read_sql(...)`.
- **Opção B — Docker + MySQL**: ambiente mais próximo de produção (requer Docker/WSL instalado); `docker pull mysql:8`, `docker run` configurando senha de root e porta, `docker exec` para acessar o CLI, e `SET foreign_key_checks = 1` para habilitar FK.

**Roteiro de execução individual**: rodar o script base (departamento/invent_mestre/transac_mestre) → rodar o script do departamento gerado pela IA → rodar os INSERTs → testar a integridade (tentar inserir um item com departamento inexistente e observar o erro de FK) → rodar SELECTs com JOIN entre a tabela do departamento e `invent_mestre` → responder às perguntas analíticas: listar os itens do departamento ordenados por preço decrescente; contar as movimentações por tipo (ENTRADA/SAIDA/AJUSTE); identificar o item com maior volume total movimentado; listar itens com pelo menos uma saída nos últimos 30 dias; e fazer um JOIN trazendo os atributos específicos do produto junto com SKU e preço de custo.

### 10. Origem e fundamentos dos bancos NoSQL

O movimento que deu origem ao big data e ao NoSQL remonta aos papers do Google — **GFS** (2003) e **Bigtable** (desenvolvido internamente em 2004, publicado em 2006) — e ao paper do **Dynamo** da Amazon (2007). O termo **NoSQL** em si só foi cunhado em 2009. Uma observação recorrente do professor: "NoSQL" não significa "não é SQL" — significa **"Not Only SQL"**: bancos pensados para complementar o relacional, resolvendo o que ele sozinho não dá conta com a mesma eficiência.

As duas características que definem essa categoria são a **escalabilidade horizontal** (trabalhar com clusters de muitas máquinas em paralelo, de forma distribuída) e a **flexibilidade de esquema** (a estrutura pode evoluir ao longo do tempo, sem a obrigatoriedade de um schema predefinido rígido).

### 11. Tipos de bancos NoSQL

| Tipo | Características | Exemplos |
|---|---|---|
| **Documento** | Estrutura flexível (JSON/BSON), cada registro pode ter forma diferente; forte para catálogos, perfis, conteúdo variável | MongoDB, CouchDB |
| **Chave-valor** | Estrutura mínima — um índice e um valor associado; latência ultrabaixa, escala trivial; dominante em cache, controle de sessão, carrinho de compras | Redis, DynamoDB |
| **Colunar (wide column)** | Otimizado para agregação analítica em grandes volumes e para escrita rápida (ver seções 13-16) | Cassandra, HBase |
| **Grafo** | Entidades e relacionamentos como cidadãos de primeira classe; entrega ACID completo, mas com estrutura muito mais aberta; forte em detecção de fraude, redes sociais e algoritmos de clusterização (tema da próxima aula) | Neo4j |
| **Vetorial** | Armazena embeddings — representações numéricas de texto, imagem e áudio — consultados por similaridade semântica, não por igualdade exata; essencial para IA generativa | Pinecone, Weaviate, pgvector |
| **Multimodelo** | Suporta mais de um desses estilos na mesma engine | ArangoDB, Cosmos DB |

Vale registrar duas observações de cor da aula: o professor descreveu o Cosmos DB, meio de brincadeira, como "um Frankenstein" — nasceu como banco de documentos e hoje faz muito mais do que isso; e comentou já ter usado o pgvector (Postgres com extensão vetorial) em projeto real, achando a proposta interessante apesar de algumas limitações.

### 12. ACID vs. BASE e o Teorema de CAP

Enquanto o banco relacional opera no modelo **ACID**, os bancos NoSQL distribuídos operam predominantemente no modelo **BASE** (*Basically Available, Soft State, Eventually Consistent*). O **soft state** é o ponto que mais muda de mentalidade em relação ao relacional: o banco não garante que o dado está sempre perfeitamente sincronizado entre réplicas — ele propaga as alterações pelo cluster de forma mais "preguiçosa", conforme a necessidade, não de forma imediata. Daí vem a **consistência eventual**: tolera-se algum nível de defasagem (é possível ver um dado desatualizado até um refresh trazer a versão mais recente).

A escolha entre ACID e BASE não é puramente técnica — é, em boa parte, uma **decisão de negócio**. Um feed de rede social tolera alguns segundos de atraso para mostrar a última publicação; sistemas de passagem aérea toleram certos padrões de consistência eventual por desenho. Já em um sistema financeiro, a transação não pode tolerar inconsistência — muitas vezes é preferível ter indisponibilidade a ter inconsistência.

O **Teorema de CAP**, proposto por **Eric Brewer em 2000**, formaliza essa tensão: um sistema distribuído não consegue garantir simultaneamente mais do que duas das três propriedades — **Consistência**, **Disponibilidade** e **Tolerância a Partição**. Na prática, falhas de rede em sistemas distribuídos são inevitáveis, então a tolerância a partição não é opcional — a escolha real está entre priorizar consistência ou disponibilidade. Mapeando os exemplos usados em aula: bancos relacionais tradicionais operam em **CA** (assumem rede confiável e querem as duas coisas); MongoDB, HBase e Redis tendem a **CP** (consistência primeiro, depois disponibilidade); Cassandra e DynamoDB tendem a **AP** (disponibilidade em primeiro lugar). Uma ressalva importante levantada em 2026: hoje em dia vários desses bancos (o próprio Cassandra incluso) já têm configurações que permitem "navegar" entre os cantos do teorema — é possível abrir mão de disponibilidade para forçar consistência em uma operação específica — mas cada banco mantém uma característica nativa/padrão predominante.

### 13. Bancos colunares: conceito e funcionamento

O modelo colunar "pivota" a lógica do banco relacional: em vez de armazenar cada registro (linha) como um bloco completo, ele organiza e armazena o dado **por coluna**. A analogia usada em aula: consultar um banco colunar é como jogar batalha naval — você diz "quero essa coluna, essa célula específica" e o banco vai direto lá, ignorando o resto da tabela, em vez de trazer a linha inteira para depois filtrar.

Isso tem implicações práticas diretas:

- **Leitura** — consultas que tocam poucos atributos entre muitos registros ficam drasticamente mais rápidas (não há full table scan, a menos que se faça um SELECT * sem filtro algum).
- **Escrita** — escritas pontuais e aleatórias em colunas variadas custam mais (o banco precisa localizar a posição exata antes de atualizar); já para dado serializado e bem modelado (séries temporais), a escrita é extremamente rápida — exatamente o ponto forte do Cassandra.
- **Compressão** — valores contíguos do mesmo tipo comprimem muito melhor, especialmente em colunas de baixa cardinalidade ou séries temporais contínuas.
- **Família de colunas** — bancos como Cassandra e HBase agrupam colunas em famílias, adicionando um nível intermediário de organização (tabela → família de colunas → registros) e trazendo bastante flexibilidade de esquema.

Um alerta repetido em aula: como o **CQL** (linguagem de consulta do Cassandra) se parece muito com SQL, cria-se uma "memória muscular" que empurra a pessoa a tratar o Cassandra como se fosse um banco relacional — e isso gera problemas reais de produção quando a filosofia de modelagem por trás não é respeitada.

| Aspecto | Relacional | Colunar |
|---|---|---|
| Organização física | Por linha | Por coluna / família de colunas |
| Esquema | Rígido, definido antes da inserção | Flexível por família de colunas |
| Consistência | ACID, forte e imediata | BASE por padrão, eventual |
| Leitura analítica | Custo alto em grandes volumes | Otimizada — lê só as colunas necessárias |
| Escrita | Otimizada para registros individuais | Otimizada para alto volume |
| Joins | Suportados nativamente | Tecnicamente possíveis no Cassandra, mas fortemente desaconselhados (oneram muito o processamento) |
| Melhor para | Sistemas transacionais, integridade de negócio | IoT, logs, séries temporais, alta frequência de escrita |

O ponto mais importante de mudança de mentalidade: a modelagem colunar é **orientada à pergunta**, não à entidade. Uma boa prática recorrente é ter uma tabela para cada consulta que se pretende responder — o que parece estranho e gera bastante duplicação de dado, mas é exatamente isso que sustenta a eficiência do modelo.

**Exemplo real trazido pelo professor.** Em um projeto para uma empresa de cosméticos, a arquitetura combinava múltiplos bancos: assim que um novo vendedor se cadastrava no front-end, o dado descia imediatamente para o **Cassandra**, priorizando velocidade de escrita; esse insert disparava um modelo de machine learning via **Spark**, que buscava parâmetros no **MongoDB** para alocar o vendedor a um gerente, região e cluster de clientes; o resultado enriquecido era então gravado em um **Postgres** relacional, de onde a aplicação lia de volta para mostrar ao vendedor seu gerente e região já definidos. Outros exemplos clássicos citados: captura de dados de máquinas de extração de petróleo (Petrobras), telemetria de carro de Fórmula 1, e monitoramento de equipamentos de fábrica — todos cenários de escrita contínua e de alto volume, ideais para banco colunar.

**Quando usar colunar:** volume de escrita alto e contínuo (IoT, logs, métricas, eventos); dados com uma chave de identificação clara e conteúdo variável; leitura analítica sobre grandes volumes; necessidade de escala horizontal e distribuição geográfica entre múltiplos data centers; criticidade de disponibilidade (o sistema não pode parar). **Quando evitar:** modelo de dados fortemente relacional, com joins complexos; operações que exigem consistência forte e imediata; dados frequentemente atualizados em campos individuais; e, um ponto que o professor destacou como grave — times sem maturidade para modelagem orientada a query. Ele relatou já ter visto times precisando remover o Cassandra de produção simplesmente porque não conseguiam adaptar a filosofia de trabalho: em vez de um modelo único de data warehouse respondendo 15-30 perguntas diferentes, o Cassandra pede uma tabela nova (duplicada) para cada pergunta — e nem todo time se adapta a isso.

Entre os bancos colunares mais relevantes do mercado: o **Cassandra**, disparado o mais usado; o **Azure Cosmos DB**, multimodelo (nasceu como banco de documentos e hoje cobre muito mais); o **HBase**, projeto Apache open source que roda sobre o ecossistema Hadoop/HDFS; e o **ScyllaDB**, uma reimplementação do Cassandra em C++ (em vez de Java) criada justamente para eliminar a dor do garbage collector da JVM — o professor citou o **Santander** como exemplo real de empresa que migrou do Cassandra para o ScyllaDB.

### 14. Cassandra: origem, características e arquitetura

O **Cassandra** foi originalmente desenvolvido pelo **Facebook em 2007** para resolver a busca na caixa de entrada de mensagens — um problema que exigia escrita muito rápida e leitura distribuída. Em 2008 foi liberado como open source; em 2010, tornou-se projeto top-level da Apache Software Foundation, ganhando depois também uma versão licenciada mantida pela **DataStax**.

Características centrais: **arquitetura peer-to-peer**, sem nó mestre — diferente do HDFS, que tem um NameNode central coordenando os DataNodes, os nós do Cassandra são muito mais autônomos, sem ponto único de falha; **escala horizontal linear** (dobrar o número de nós dobra, na prática, a capacidade de throughput); **consistência configurável por operação** (não por banco inteiro — cada leitura ou escrita pode ser ajustada para priorizar consistência ou disponibilidade); e uma **linguagem de consulta própria**, o **CQL** (Cassandra Query Language), sintaticamente parecida com SQL, mas com restrições importantes (sem join, regras específicas para WHERE e criação de tabela). Entre os grandes adotantes: **Netflix, Apple, Instagram, Uber e Spotify** — sempre ligados a casos de escrita rápida e disponibilidade contínua, com séries temporais e dados históricos como o cenário onde o Cassandra mais se destaca.

Mecanicamente, os nós conversam entre si em sentido horário, em anel (*ring*), fazendo *heartbeats* periódicos; quando um nó cai, o vizinho percebe e assume o rebalanceamento necessário para manter o nível de replicação, usando um processo de votação/quórum para decidir quem assume a réplica perdida. Os dois componentes físicos da arquitetura são o **nó** (um servidor — a unidade básica de armazenamento, responsável por uma faixa de dados determinada pelo particionador; todos os nós são equivalentes, sem distinção entre primário e secundário) e o **data center** (um agrupamento *lógico* de nós, tipicamente correspondendo a uma região geográfica). Um **cluster** é o conjunto de data centers, com o dado replicado entre eles conforme a estratégia configurada.

O particionamento usa **consistent hashing**: um hash é gerado e cada intervalo dele é atribuído a um nó específico, que passa a ser responsável por aquele intervalo (e sua réplica). O hash deriva da **partition key**, parte da chave primária do Cassandra. Um ponto crítico: o Cassandra quer partições de tamanho uniforme — partições muito desbalanceadas (uma com 1 GB, outra com 500 MB) prejudicam a performance e complicam a entrada/saída de nós no cluster.

### 15. Replicação e modelagem no Cassandra

A replicação do Cassandra tem dois parâmetros: a **estratégia de replicação** (onde colocar as réplicas) e o **fator de replicação** (quantas cópias manter). A **SimpleStrategy** é usada com um único data center, distribuindo as réplicas peer-to-peer, em sentido horário no anel. A **NetworkTopologyStrategy** é usada quando há mais de um data center, replicando o dado entre regiões diferentes — útil, por exemplo, quando uma aplicação nos EUA replica para o Brasil e vice-versa; o segundo data center funciona simultaneamente como contingência, backup e otimização de throughput. Sobre o fator de replicação: um fator 1 significa uma única cópia; o "número mágico" mais usado é **3**, para não haver ponto único de falha — mas ambientes maiores e mais críticos podem usar fatores mais altos (5, 6, 7), enquanto um ambiente local de teste pode operar com fator 1.

O núcleo da modelagem no Cassandra é o par **partition key + clustering key**. Na sintaxe da chave primária, os parênteses de fora definem a **clustering key** (a chave ordenadora dentro da partição) e os parênteses de dentro definem a **partition key** (o que fisicamente agrupa o bloco de dado). Um ponto que costuma confundir quem vem do relacional: o Cassandra decide a ordenação do dado **na escrita, não na leitura** — os registros dentro de uma partição já são inseridos respeitando a ordem da clustering key, e é exatamente por isso que ele é tão rápido para séries temporais e cargas de escrita intensiva: não precisa procurar onde escrever, ele já sabe a posição.

**Um caso real de acidente de produção**, contado pelo professor a partir de sua própria experiência de consultoria (época da Accenture): um cliente tinha um cluster Cassandra que vivia caindo. Ao investigar, a causa era uma tabela particionada pelo atributo **"estado"** — como São Paulo sozinho gerava uma partição desproporcionalmente grande, nenhum nó conseguia comportá-la, e o cluster inteiro ficava instável. A lição: é preciso encontrar um atributo (ou combinação de atributos) que produza partições de tamanho aproximadamente uniforme — nem granular demais (um único registro por partição joga a vantagem do modelo fora, e nesse caso é melhor usar banco relacional mesmo) nem grande demais.

Como o Cassandra não suporta join, o padrão de modelagem "uma tabela por pergunta" na prática costuma envolver escrever uma vez em uma tabela principal de ingestão e usar um trigger ou um processo de ETL para replicar/remodelar esse dado nas demais tabelas — uma para cada consulta analítica que se precisa responder.

Por fim, o caminho de escrita explica a velocidade do banco: o dado é gravado primeiro em memória (**memtable**) e em um log sequencial (**commitlog**), e só depois é levado para o disco físico como **SSTable**. Essa gravação em duas etapas é extremamente rápida e central para os casos de alto volume — mas só compensa se a modelagem (o particionamento) estiver correta.

### 16. Consultas no Cassandra e o ALLOW FILTERING

No Cassandra, só é possível filtrar diretamente pelas chaves: a **partition key completa é obrigatória** em qualquer WHERE, e a **clustering key é opcional** como filtro adicional. Tentar filtrar por uma coluna que não é chave, sem tratamento especial, retorna erro — o banco se recusa a fazer um scan lento silenciosamente. O comando **ALLOW FILTERING** libera esse tipo de filtro, mas força o Cassandra a varrer todas as partições e olhar registro por registro — um antipadrão de performance, e exatamente o motivo pelo qual a prática recomendada é modelar "uma tabela por pergunta" em torno das chaves, em vez de depender de ALLOW FILTERING. Mesmo quando a partition key já foi usada e o ALLOW FILTERING entra só para um filtro adicional dentro dela, a consulta continua razoavelmente eficiente (o Cassandra já achou a partição certa antes de filtrar); ainda assim, o comando continua sendo exigido explicitamente sempre que o filtro sai do escopo da chave.

### 17. Laboratório prático com Cassandra

**Setup**, com duas opções: (A) **DataStax Astra DB** — conta gratuita em astra.datastax.com, criação de um banco (ex.: `dbdts`) com keyspace (ex.: `ksdts`), provedor AWS, região us-east-2 (geralmente a única disponível no free tier), com acesso direto ao **CQL Console** pelo navegador, sem instalação; (B) **Docker + Cassandra local** — `docker pull cassandra`, `docker network create cassandra`, `docker run` configurando hostname e rede, e `docker exec -it cassandra cqlsh` para acessar o terminal.

Criação de keyspace: `CREATE KEYSPACE IF NOT EXISTS <nome> WITH replication = {'class': 'SimpleStrategy', 'replication_factor': 1}; USE <nome>;` — vale notar que, ao criar um banco pela Astra, já vem um primeiro keyspace pronto (uma pegadinha comum em aula: tentar criar de novo um keyspace com o mesmo nome usado na criação do banco retorna erro de "já em uso").

Como exercício guiado, o professor criou ao vivo uma tabela simples `bandas` (id inteiro como PRIMARY KEY, nome texto, gênero texto) — aceita sem problema pelo Cassandra — e depois uma tabela `musicos` com chave composta no formato `PRIMARY KEY ((genero, banda), nome)`, para ilustrar a diferença entre partition key (parênteses de dentro) e clustering key (parênteses de fora). O CQL Console colore as colunas por papel (partição / clustering / dado) no resultado da consulta, o que ajuda bastante a visualizar a estrutura.

O roteiro prático seguido em aula: criar o keyspace → acessá-lo (USE) → criar a tabela `aula_cassandra` → inserir um registro → consultar → incluir uma nova coluna → consultar de novo e observar a mudança. Em seguida, exploração dos **tipos de dado multivalorados**: **set** (coleção ordenada de elementos únicos), **list** (elementos mantidos na ordem de inserção — índice começando em 0), **map** (pares de chave-valor) e **tuple** (estrutura de tamanho fixo capaz de armazenar múltiplos campos tipados — aceita até 32.768 campos) — com exercícios de criação, inserção e consulta em tabelas dedicadas para cada tipo (`aula_cassandra_set`, `aula_cassandra_list`, `aula_cassandra_map`, `aula_cassandra_tuple`).

Sobre **índices e filtros**: o exercício mostra primeiro que filtrar por uma coluna fora da chave, sem ALLOW FILTERING, dá erro; depois, que o ALLOW FILTERING funciona mas escaneia a tabela inteira (custoso em tabelas grandes); e por fim, como alternativa, a criação de um índice secundário sobre a coluna — o que acelera a consulta, mas com custo de escrita mais alto. É possível também criar índices especificamente sobre a chave de um map, o valor de um map, ou as entradas (entries) de um map.

Sobre **exclusão e limpeza**: exclusão de registros específicos, exclusão do conteúdo de uma única coluna, limpeza de conteúdo de campos set/list/map (lembrando que o índice de uma list começa em 0), TRUNCATE de tabela, remoção de índice, remoção de tabela, e criação/remoção de um keyspace só para testar o comando. Como desafios propostos ao final: o que acontece ao inserir o mesmo valor duas vezes; o que acontece ao inserir a mesma chave com valores diferentes; como fazer update nas tabelas; se é possível fazer delete sem usar a primary key; como fazer update em campos multivalorados (set/list/map); inserir elementos fora de ordem em um set; e criar uma tabela com campos tuple aninhados.

Como prática opcional extra, o professor também disponibilizou um roteiro equivalente em **MySQL via Docker** (usando o mesmo container do laboratório de SQL): criar e acessar um database, criar tabela, criar um usuário e testar GRANT/REVOKE (demonstrando ao vivo que um usuário sem permissão falha ao tentar inserir até receber o GRANT), fazer update/delete de registros, e até abrir o arquivo físico de dados no disco para confirmar que ele não é legível para humanos — reforçando, do lado relacional, a mesma separação lógico/físico vista na seção 6.

### 18. Encerramento e próximos passos

A entrega da aula reúne os dois exercícios (o laboratório SQL/relacional e a prática com Cassandra) em um único trabalho de sala, com prazo até a véspera da próxima aula — formato livre (Word, TXT, ZIP com os scripts), desde que traga os comandos utilizáveis e um racional mínimo do grupo sobre as decisões tomadas (não é necessário exportar a conversa completa com a IA). O professor sinalizou que um trabalho integrado maior, com mais tempo dedicado, será apresentado em uma aula futura.

Um fechamento que resume bem o espírito da aula veio de um aluno que se descreveu como "100% relacional": levou um tempo para a lógica do Cassandra fazer sentido, mas assim que ficou claro que a criação de tabela é orientada ao relatório/extração que se quer responder — e não à entidade de negócio — as peças se encaixaram. O professor reforçou o ponto: o conceito importa mais do que a ferramenta específica, porque na prática cada um vai usar a ferramenta que tiver disponível. A próxima aula aprofunda **bancos de grafos**, com Neo4j.

## Aula 3 — Bancos de Documentos (MongoDB) e Bancos de Grafos (Neo4j)

Aula ministrada pelo Prof. Leandro Mendes, dando sequência ao mapa de bancos NoSQL aberto na Aula 2. Depois de aprofundar o modelo colunar com Cassandra, a turma avança para mais dois paradigmas que resolvem problemas de modelagem diferentes: **documentos** (MongoDB) e **grafos** (Neo4j). A aula reserva a segunda metade para dois laboratórios práticos, remodelando o mesmo cenário de inventário (`invent_mestre`/`transac_mestre`) usado no laboratório SQL da Aula 2 — primeiro para o modelo de documentos, depois para o modelo de grafos.

### 1. Bancos de documentos: características e o modelo JSON

O **banco de documentos** guarda cada registro como um documento autocontido, tipicamente em **JSON** (internamente, o MongoDB serializa em **BSON**, uma variante binária do JSON). Diferente do modelo relacional, onde o esquema é definido antes da inserção e é igual para toda a tabela, aqui cada documento pode ter uma estrutura própria — campos podem existir em um documento e não existir em outro da mesma coleção, sem que isso gere erro ou exija uma migração de schema.

Essa flexibilidade tem uma implicação de armazenamento discutida em aula: como o documento só grava os campos que de fato possui, um atributo ausente não consome espaço nenhum — diferente do banco relacional, onde uma coluna opcional sem valor ainda ocupa espaço (ou ao menos overhead de metadado) em toda linha da tabela, esteja ela preenchida ou não. Em bases com muitos atributos opcionais e alta variação entre registros, isso se traduz em economia real de armazenamento.

### 2. Estrutura do MongoDB: instância, banco, coleção e documento

O MongoDB organiza o dado em quatro níveis hierárquicos: **instância** (o servidor/processo do MongoDB rodando), **banco de dados** (database, um namespace lógico dentro da instância), **coleção** (collection, o equivalente a uma tabela, mas sem schema fixo) e **documento** (o registro individual, em JSON/BSON). Cada documento recebe automaticamente um campo `_id` do tipo **ObjectId**, gerado pelo próprio MongoDB caso a aplicação não o informe explicitamente, garantindo unicidade sem que seja preciso implementar uma sequência ou UUID à parte.

Um ponto que gerou dúvida em aula foi se a instância do MongoDB também gerencia partição geográfica entre regiões, como o Cassandra faz com seus data centers. O professor esclareceu que não: por padrão, um cluster MongoDB inteiro permanece em uma única região — ele não tem, nativamente, o mesmo conceito de replicação multirregião gerenciada pelo próprio banco que o Cassandra oferece via `NetworkTopologyStrategy`. Isso é relevante na hora de comparar os dois bancos para cenários de disponibilidade geográfica.

### 3. Particionamento, replicação e o Teorema de CAP no MongoDB

O MongoDB escala horizontalmente por **sharding** (particionamento): os dados de uma coleção são divididos entre múltiplos nós conforme uma chave de partição (shard key), com um particionamento **primário** (a divisão inicial dos dados entre os shards) e mecanismos de particionamento **secundário** para redistribuir e balancear os dados à medida que o cluster cresce. Cada shard, por sua vez, é replicado dentro de um **replica set**, garantindo tolerância a falha de nó.

Dentro de um replica set, existe sempre um **nó primário** (que recebe as escritas) e um ou mais **nós secundários** (que replicam o dado do primário e podem atender leituras, dependendo da configuração). Quando o nó primário cai ou fica inacessível, o replica set realiza uma **eleição** entre os nós secundários para escolher o novo primário — um processo de votação que considera fatores como a atualidade dos metadados de cada nó (quão em dia sua réplica está), a capacidade de banda/configuração da máquina e o throughput que o nó consegue sustentar. Esse mecanismo de eleição é conceitualmente parecido com o esquema de votação/quórum do Cassandra, mas resolve um problema ligeiramente diferente: lá, o objetivo é decidir quem assume a réplica perdida em uma arquitetura peer-to-peer sem mestre; aqui, o objetivo é eleger um mestre único (o primário) em um modelo que tem, sim, um nó coordenador de escrita.

Essa arquitetura mestre-réplica com propagação assíncrona coloca o MongoDB no modelo **BASE**, com **soft state** — assim como o Cassandra, o MongoDB tende a priorizar disponibilidade em detrimento de consistência imediata sob partição de rede, sendo classificado como **AP** no Teorema de CAP (a mesma classificação do Cassandra, ainda que os dois cheguem lá por caminhos arquiteturais bem diferentes — um peer-to-peer sem mestre, outro com eleição de primário).

### 4. Modelagem: embutir (embed) vs. referenciar

A decisão de modelagem mais importante no MongoDB é escolher, para cada relacionamento entre entidades, se ele deve ser **embutido** (embedded — o dado relacionado vive como um sub-documento ou uma sub-coleção dentro do documento pai) ou **referenciado** (reference — o dado relacionado vive em uma coleção própria e é ligado por um identificador, de forma parecida com uma chave estrangeira, mas sem integridade referencial garantida pelo banco). Como recomendação prática, a orientação da aula foi não ultrapassar cerca de **10 sub-coleções** embutidas dentro de um mesmo documento, sob risco de o documento crescer demais e prejudicar performance de leitura e escrita.

Essa decisão apareceu de forma muito concreta no exercício prático da aula (seção 7), mas o critério geral discutido foi: **embuta** quando a cardinalidade do relacionamento é baixa a média e o dado embutido é sempre lido junto com o pai (não faz sentido separar); **referencie** quando o relacionamento é de alto volume (um-para-muitos com "muitos" grande, como um histórico de transações), quando o dado precisa ser consultado de forma independente do pai, ou quando o dado embutido mudaria com frequência e obrigaria reescrever muitos documentos pais a cada atualização (por exemplo, um preço de produto que varia por região — embuti-lo em cada cliente exigiria atualizar potencialmente milhões de documentos a cada reajuste). Um aluno resumiu bem essa lógica de decisão durante a aula, ao analisar se contas deveriam ficar embutidas dentro do documento de cliente: "eu armazenaria dentro do documento, um documento com outro documento dentro. Se você pensou em fazer join, você está no banco errado" — captando a ideia central de que, no MongoDB, a estrutura do documento deve antecipar a forma de leitura, e não empurrar a responsabilidade de juntar dados para uma consulta posterior (que o MongoDB, aliás, não resolve tão bem quanto um relacional).

### 5. Quando usar e quando evitar o MongoDB

**Casos de uso favoráveis:** arquiteturas de **persistência poliglota** (um exemplo trazido em aula: Redis para o carrinho de compras, MongoDB para o catálogo de produtos, e um banco relacional para as transações financeiras — cada banco resolvendo a parte do problema onde é mais forte); catálogos de produto e conteúdo variável (cada produto com atributos diferentes, sem forçar todos a caberem no mesmo schema); blogs e sistemas de CMS; gestão de configuração de aplicações; dados geoespaciais; redes sociais; e, de forma geral, sistemas com esquema pouco acoplado e em evolução constante — o exemplo citado foi o de startups em fase de descoberta de produto, onde o modelo de dados muda com frequência e a rigidez do schema relacional atrapalharia a velocidade de iteração.

**Anti-casos de uso:** sistemas fortemente transacionais e com entidades fortemente acopladas (onde a integridade referencial entre múltiplas tabelas é central ao negócio); cenários que dependem de **joins complexos** entre muitas entidades (o MongoDB não tem a mesma capacidade nativa de junção que o relacional); e operações que exigem **transações complexas com múltiplas etapas** e garantias fortes de atomicidade entre coleções diferentes.

Um tópico levantado por um aluno (Murilo) foi comparar bancos vetoriais nativos do MongoDB (MongoDB Atlas Vector Search) com o **pgvector** no Postgres para casos de RAG (Retrieval-Augmented Generation) de agentes de IA. A resposta do professor: a escolha depende muito da infraestrutura já existente e da maturidade do time — se a equipe já opera Postgres e o volume de dados vetoriais é o volume típico de um RAG de agente (não um caso de escala massiva), o pgvector tende a ser a opção mais simples, evitando introduzir mais uma peça de infraestrutura só para a capacidade vetorial. Esse tema retorna com muito mais profundidade na Aula 4.

### 6. Laboratório prático: subindo um MongoDB e primeiros comandos

O professor demonstrou duas formas de subir um ambiente MongoDB para o laboratório. A primeira, pelo **MongoDB Atlas** (o serviço gerenciado na nuvem), sofreu um contratempo ao vivo: o professor esqueceu de salvar a senha gerada automaticamente na criação do cluster e precisou apagar e recriar o ambiente do zero, se desculpando com a turma ("fui na pressa e esqueci") — um lembrete prático de que, mesmo em ambientes gerenciados, credenciais geradas automaticamente precisam ser salvas no momento da criação, porque normalmente não são recuperáveis depois.

Como alternativa mais previsível, o professor demonstrou o setup via **Docker**: `docker pull mongo` para baixar a imagem oficial, `docker run -p 27017:27017 -d --name aula-mongo mongo` para subir o container publicando a porta padrão do MongoDB, `docker exec -it aula-mongo bash` para acessar o shell do container e `mongosh` para abrir o console interativo do MongoDB. A partir daí, os comandos básicos demonstrados foram: `db.createCollection("colecao1")` para criar uma coleção explicitamente, `show collections` para listar as coleções existentes, `db.colecao1.insert({name: "Leandro", profissao: "professor"})` para inserir um documento, e `db.colecao1.find()` para consultá-lo de volta. Um ponto interessante ilustrado ao vivo: uma coleção **não é materializada** no banco até que o primeiro documento seja inserido nela — criar a coleção explicitamente é opcional, já que o próprio insert cria a coleção automaticamente caso ela ainda não exista.

### 7. Estudo de caso em sala: remodelando a Mega Loja para o MongoDB

O exercício em grupo pediu que a turma continuasse o mesmo cenário de dados bancário/financeiro trabalhado na Aula 2 — cinco tabelas relacionais (clientes, contas, transações, produtos/ofertas, entre outras), geradas com seed 42 e cerca de 2.000 clientes — mas agora **remodelando** (não apenas traduzindo) essa estrutura para um schema de documentos MongoDB, usando IA generativa para acelerar a geração dos scripts, exatamente como no laboratório SQL da Aula 2.

As decisões de modelagem discutidas nos grupos, e capturadas em detalhe durante os breakouts, ilustram bem os critérios da seção 4:

- **Contas embutidas dentro do cliente**, como um array de sub-documentos — decisão consensual, já que a cardinalidade cliente→contas é baixa a média e as contas são normalmente lidas junto com os dados do cliente.
- **Transações mantidas em coleção própria**, não embutidas — porque é uma relação um-para-muitos de alto volume. Um aluno (Renato) trouxe o raciocínio de custo explicitamente: "eu vou estar pagando por esse join... depende muito de como vai ser a utilização desse dado no dia a dia" — ao que o professor confirmou ("Exatamente") e acrescentou que, dependendo do caso de uso, as transações poderiam até ser reduzidas a um resumo consolidado por cliente em vez de manter o histórico completo embutido ou referenciado por inteiro.
- **Cliente-produto/ofertas mantidos em coleção própria**, também não embutidos — para permitir que um mesmo cliente pertença simultaneamente a múltiplos clusters de marketing (o exemplo usado em sala: um cliente poderia estar simultaneamente nos clusters "incenso" e "Pokémon"), algo que ficaria difícil de representar de forma limpa se a associação estivesse embutida rigidamente em um dos dois lados.
- **Produto referenciado por ID, não embutido** — porque preço e impostos variam por região; embutir o produto inteiro em cada documento de cliente exigiria atualizar todos os documentos afetados a cada mudança de preço, gerando, nas palavras discutidas em grupo, "gargalo e processamento desnecessário".

Os dados gerados pela IA para o exercício foram validados contra os resultados do laboratório SQL da Aula 2 (a mesma base, mesma seed), com os grupos conferindo que os totais batiam (na casa de milhões de registros de transação e percentuais de participação por departamento), reforçando que a remodelagem preservava a mesma realidade de negócio, apenas mudando a forma de organizar o dado.

### 8. Origem dos bancos de grafos: teoria dos grafos e as pontes de Königsberg

A segunda metade da aula muda de paradigma para **bancos de grafos**. A origem teórica remonta à **teoria dos grafos**, formalizada pelo matemático **Leonhard Euler em 1736** ao resolver o problema das **sete pontes de Königsberg** — a pergunta de se era possível atravessar as sete pontes da cidade (hoje Kaliningrado) passando por cada uma exatamente uma vez e retornando ao ponto de partida. Euler provou que não, e ao formalizar o problema como um conjunto de pontos (nós) conectados por linhas (arestas), lançou as bases matemáticas que hoje sustentam os bancos de dados orientados a grafo.

O **Neo4j** foi apresentado como o banco de grafos **nativo** e **open source** mais usado do mercado — "nativo" no sentido de que a estrutura de grafo não é uma camada sobre outro modelo de armazenamento, mas o próprio modelo de armazenamento e de processamento de consultas.

### 9. Neo4j: nós, rótulos, propriedades e relacionamentos

O modelo de dados do Neo4j é montado sobre quatro conceitos centrais:

- **Nó (node)** — um ponto de dado, o equivalente a uma entidade ou registro. Pode ter zero ou mais rótulos e zero ou mais propriedades.
- **Rótulo (label)** — uma etiqueta usada para agrupar nós por domínio (por exemplo, `:Pessoa`, `:Local`). Um rótulo não é um "balde" ou uma tabela rígida como no relacional — é apenas uma marcação que ajuda a filtrar e organizar consultas; um mesmo nó pode ter mais de um rótulo simultaneamente.
- **Propriedade (property)** — um par chave-valor, no formato JSON-like, atribuído a um nó ou a um relacionamento (por exemplo, `{nome: "Leandro", cidade: "São Paulo"}`).
- **Relacionamento (relationship)** — uma conexão direcionada entre dois nós, sempre com um tipo (por exemplo, `:MORA`). Um relacionamento pode ter suas próprias propriedades, um nó pode se relacionar consigo mesmo, e — diferente de nós, que podem ter múltiplos rótulos — um relacionamento no Neo4j tem sempre exatamente um tipo.

### 10. Características do Neo4j e sua classificação no Teorema de CAP

Diferente do MongoDB e do Cassandra, que operam no modelo BASE e são classificados como **AP**, o Neo4j oferece suporte **ACID completo**, sendo classificado como **CA** no Teorema de CAP — ele prioriza consistência e disponibilidade, assumindo (na configuração padrão) uma topologia menos distribuída geograficamente do que os bancos AP.

Outras características levantadas em aula: o Neo4j é **schemaless/typeless** (não exige schema fixo antes da inserção); é um **motor de processamento de grafo nativo** (Native Graph Processing Engine — GPE), o que significa que percorrer relacionamentos é uma operação de custo constante por salto, independentemente do tamanho total do banco (diferente de simular relacionamentos via joins em um relacional, cujo custo cresce com o volume); suporta importação/exportação em **JSON e XLS**, além de uma **API REST** nativa; e, na edição gratuita/open source, não impõe restrições de uso ("free-for-all"). Em termos de escala, o professor citou o limite teórico de cerca de **34,4 bilhões** de nós e relacionamentos por banco, sem suporte nativo a **sharding de subgrafo** (diferente do MongoDB, o Neo4j open source não particiona um único grafo entre múltiplos nós). Clustering de alta disponibilidade (HA) só está disponível na edição **Enterprise** — a versão open source roda em um único nó.

O conceito de **Knowledge Graph** (grafo de conhecimento) foi introduzido como a aplicação de grafos para representar não apenas dados brutos, mas relações semânticas entre conceitos — uma distinção que a aula deixou como gancho, com mais desenvolvimento nas aulas de Knowledge Management/Prompt Engineering do curso.

### 11. Cypher: a linguagem de consulta do Neo4j

O Neo4j usa o **Cypher** como linguagem declarativa de consulta, com uma sintaxe visual que imita a notação de grafo: parênteses `()` representam um nó, e um traço com colchetes e seta `-[]->` representa um relacionamento direcionado. Os três comandos centrais demonstrados foram `CREATE` (para criar nós e relacionamentos), `MATCH` (para buscar um padrão no grafo) e `RETURN` (para definir o que a consulta deve devolver).

Na prática guiada, o professor criou um nó simples com `CREATE (:Pessoa {nome: "Leandro", cidade: "São Paulo"})` e, em seguida, `MATCH (n) RETURN n` para visualizá-lo — gerando confusão inicial na turma porque o nó exibido no grafo mostrava só um atributo por padrão (resolvido ao clicar no nó e configurar quais propriedades/cores exibir na visualização). Na sequência, o professor criou um padrão com relacionamento — `CREATE (:Pessoa {...})-[:MORA]->(:Local {tipo: "cidade", nome: "São Paulo"})` — e demonstrou a diferença entre `MATCH (n:Pessoa)-[r:MORA]->(l:Local) RETURN l` e `RETURN n, r, l`: o nó "Leandro" criado isoladamente na etapa anterior (sem o relacionamento `:MORA`) não aparece no resultado de uma consulta que exige esse padrão de relacionamento — só nós que efetivamente participam do padrão casado pelo `MATCH` são retornados.

Sobre convenção de nomes de variável, a orientação foi usar `n`/`r` de forma genérica para nós e relacionamentos em consultas simples, e a primeira letra do rótulo (`p` para `:Pessoa`, `l` para `:Local`, por exemplo) em consultas mais complexas com múltiplos passos, para manter a legibilidade. Comandos administrativos também foram demonstrados: `SHOW DATABASES` para listar os bancos, `:use system` seguido de `SHOW USERS` para trocar de contexto e listar usuários, e `MATCH (n) RETURN count(n) AS nós` para contar o total de nós em um banco.

### 12. Aplicações de bancos de grafos

A aula levantou uma lista de aplicações reais de mercado para bancos de grafos: **redes sociais** e cálculo de grau de separação entre pessoas (o caso clássico do LinkedIn); **sistemas de recomendação** em e-commerce; **análise de churn** e **clusterização** de clientes; **Business Intelligence** relacional-avançado; e **otimização de rotas geoespaciais** — o exemplo citado por um aluno (Eduardo) e confirmado pelo professor foi o funcionamento de aplicativos como **Waze** e **Google Maps**, que modelam ruas e cruzamentos como grafos para calcular o menor caminho.

Um aluno (Rafa) trouxe um exemplo real de sua própria empresa (chamada "Viva"), que constrói uma base de histórico de interações em grafo para dar contexto omnichannel ao atendimento — de forma que o histórico de um cliente em diferentes canais (chat, telefone, e-mail) fique conectado como um único grafo de relacionamento, em vez de fragmentado em silos por canal. Outro exemplo citado foi um projeto de soberania de dados do governo brasileiro (um LLM apelidado "Gaia"), treinado usando grafos de conhecimento em vez de pura vetorização, que teria apresentado desempenho superior a outros modelos em benchmarks como ENEM e FUVEST — um exemplo levantado em aula que, por vir de um relato de segunda mão da turma, vale registrar como uma referência a verificar, e não como um dado confirmado com uma fonte oficial.

### 13. Laboratório prático com Neo4j e o desafio de migração para grafos

Assim como no MongoDB, o professor demonstrou duas formas de subir o Neo4j: via **Docker** (`docker pull neo4j` seguido de um `docker run` publicando as duas portas do serviço — **7474** para a interface web e **7687** para o protocolo Bolt de conexão — com troca da senha padrão `neo4j`/`neo4j` no primeiro acesso) e via **Neo4j Aura**, o console gerenciado na nuvem (`console.neo4j.io/login`), que alguns alunos tiveram dificuldade de acessar por instabilidade de conexão, contornada usando modo anônimo do navegador ou trocando de browser.

A interface do Neo4j Browser foi apresentada com um tour rápido: a barra lateral esquerda concentra informações do banco (nós, relacionamentos, propriedades), consultas Cypher salvas, histórico de comandos, documentação de referência e um ícone de configurações (incluindo limites de visualização de nós no grafo e alternância entre tema claro/escuro); o painel principal, à direita, é onde o Cypher é digitado e executado — reforçando que essa interação é puramente declarativa via Cypher, e não uma interface conversacional com um LLM. Os comandos `:play welcome` e `:clear`, além do tutorial embutido do "movie graph" (grafo de filmes de exemplo), foram usados para introduzir o ambiente.

O desafio prático da segunda parte da aula pediu que a turma convertesse, com apoio de IA generativa, o mesmo modelo de inventário relacional da Aula 2 (`invent_mestre`/`transac_mestre`) para um modelo de grafo no Neo4j, avaliando criticamente a resposta da IA: as transações viraram nós ou viraram relacionamentos? O que aconteceu com os atributos que existiam nas tabelas originais? Que novos tipos de relacionamento — que não existiam explicitamente no modelo relacional — passaram a fazer sentido no grafo? Como tratar os itens órfãos que, no relacional, dependiam de uma chave estrangeira para existir? E como usar o comando **MERGE** do Cypher para evitar duplicar nós ao reexecutar a carga de dados mais de uma vez. Nos grupos, uma decisão recorrente foi transformar o **departamento** em um **nó** próprio (em vez de mantê-lo como uma simples propriedade de cada item), justamente pela cardinalidade — vários itens pertencem ao mesmo departamento, então tratá-lo como nó permite consultas de correlação que uma propriedade isolada não sustentaria, como "se um fornecedor parar de entregar, quais itens nos departamentos serão afetados?".

Por conta do tempo consumido no laboratório de MongoDB, o professor optou por não cobrar a entrega do exercício de MongoDB, pedindo apenas a entrega do exercício de Neo4j — e decidiu também postergar o conteúdo de **bancos vetoriais**, originalmente previsto para o fim desta aula, para a aula seguinte, com mais tempo e profundidade dedicados ao tema.

### 14. Encerramento e transição para os bancos vetoriais

A aula fecha reconhecendo que o conteúdo de grafos foi denso e teve um início mais difícil (especialmente para quem vinha ainda absorvendo MongoDB na mesma sessão), mas destacando o valor do tema para o mercado. O professor sinalizou explicitamente que a próxima aula, dedicada a **bancos vetoriais**, vai complementar o que foi visto em grafos — os dois temas resolvem, de formas diferentes, o problema de dar mais significado e contexto ao dado além da simples busca por igualdade exata que o relacional oferece.

## Aula 4 — Bancos Vetoriais para Agentes (Operação Q)

Aula ministrada pelo Prof. Leandro Mendes, estruturada de forma diferente das anteriores: em vez de uma sequência linear de conceitos seguida de um laboratório único, a aula é organizada em torno de um cenário fictício contínuo — a **Operação Q** — que serve de fio condutor tanto para a teoria quanto para os dois laboratórios práticos da aula (antes e depois do intervalo). A aula tem quatro objetivos declarados: entender infraestrutura e modelagem de bancos de vetores, operação de runtime e segurança, engenharia de busca e índices, e tomada de decisão tecnológica por tipo de índice/configuração.

### 1. Contexto: da gestão de dados à gestão de conhecimento — o cenário Quantum Finance

O cenário de toda a aula é a **Quantum Finance**, um banco digital fictício em plena expansão, com **2 milhões de clientes** e **59 manuais internos** de política, tarifa e processo. A empresa opera o **Agente Q**, um agente automatizado que atende clientes, responde perguntas e analisa dados, apoiado por um **script avaliador determinístico** (sem juiz-LLM) que pontua, ao final do exercício, a qualidade do banco de vetores estruturado pelo aluno.

Cinco personas de cliente fictícias foram definidas para ancorar os requisitos do exercício: **Marina**, que está economizando para comprar uma moto e não quer receber oferta de cartão; **Carlos**, com foco total em investimentos; **Ana**, que renegociou uma dívida e vai exercer o **direito ao esquecimento** da LGPD; **Bruno**, um cliente novo cujo histórico não pode se misturar com o de nenhum outro cliente; e **Fernanda**, com um atendimento urgente de sinistro de seguro. Essas personas definem, na prática, os requisitos não-funcionais do banco de vetores que a turma precisa construir: citação exclusiva de documentos oficiais vigentes (sem alucinação), isolamento estrito de memória por cliente, e exclusão física e definitiva de dados sob pedido de LGPD.

O professor situou o banco vetorial no mapa da disciplina: depois de bancos relacionais (Aula 2), NoSQL de documentos e grafos (Aula 3), a Aula 4 marca a transição de olhar o banco puramente como armazenamento de dados para olhá-lo como **gestão de conhecimento** — a capacidade de buscar por significado semântico, não apenas por igualdade exata de valor.

### 2. Escalares, vetores e embeddings

Um **escalar** é um valor numérico único, sem direção — uma temperatura, uma tarifa, uma idade (um float, int ou similar). Um **vetor**, por sua vez, é uma lista estruturada de números que descreve algum elemento de forma multidimensional — por exemplo, um perfil de cliente pode ser vetorizado usando renda mensal, idade, produto, última compra e score como coordenadas.

O **embedding** é o processo — realizado por um modelo de rede neural específico e "congelado" — que converte texto (ou outro dado não estruturado) nessas coordenadas numéricas. Textos com significados semelhantes são mapeados para coordenadas próximas no espaço vetorial, e é justamente esse cálculo de proximidade que sustenta a busca semântica. Um ponto reforçado repetidamente em aula: **embedding não é o banco de vetores** — é a função/biblioteca de rede neural que gera os vetores a partir de um texto; o banco de vetores é quem armazena, indexa e consulta esses vetores depois de gerados. É possível, inclusive, trabalhar apenas com embedding (sem banco de vetores algum) em cenários pequenos, guardando os vetores em memória — um primeiro degrau que a aula detalha na seção 5.

Em resposta a perguntas da turma sobre como exatamente a rede neural decide os valores de cada coordenada, o professor foi direto: não existe um "valor ideal" ou um peso "melhor" — o que existe é que palavras e trechos em contextos semelhantes acabam gerando vetores próximos, porque é isso que permite ao modelo navegar sem ambiguidade e encontrar a resposta certa. A pontuação exata gerada por uma rede neural específica não é algo que se possa explicar termo a termo — só se pode observar e validar o comportamento agregado (proximidade semântica coerente).

### 3. Regras de infraestrutura do embedding e o lugar do RAG

Três regras de infraestrutura foram destacadas como críticas para qualquer projeto que use embeddings:

1. **Mesmo modelo na ingestão e na consulta.** Se um texto foi vetorizado com um modelo/biblioteca específico, a consulta precisa usar exatamente o mesmo modelo — modelos diferentes geram espaços vetoriais diferentes, e comparar vetores de modelos distintos não produz um resultado coerente.
2. **O número de dimensões do modelo define o tipo da coluna do banco.** No pgvector, por exemplo, a coluna é declarada como `vector(384)` se o modelo usado gera vetores de 384 dimensões — esse número é rígido e igual para toda a tabela.
3. **Trocar de modelo exige reindexação completa.** Se o modelo de embedding muda, os vetores antigos deixam de ser comparáveis aos novos, então é preciso recalcular e reconstruir a base inteira.

O laboratório da aula usa o modelo **`paraphrase-multilingual-MiniLM-L12-v2`**, com **384 dimensões**, rodando localmente via a biblioteca **Sentence Transformers**.

Sobre o lugar do **RAG** (Retrieval-Augmented Generation) nessa cadeia: o embedding puro (guardado em memória ou em uma lista simples) é o primeiro degrau, útil para POCs e classificação de intenção em tempo real; o RAG é o passo seguinte, adicionando uma camada de recuperação mais estruturada sobre os documentos vetorizados antes de alimentar o modelo de linguagem; e o banco de vetores de produção (o foco desta aula) é o degrau mais avançado, sustentando volume, concorrência e governança. O professor deixou claro que embedding e RAG não são aprofundados tecnicamente nesta aula porque o curso tem uma aula dedicada a Knowledge Management/Prompt Engineering — aqui eles são citados apenas na medida do necessário para justificar o banco de vetores.

Um esclarecimento à parte, motivado por uma pergunta em aula: ferramentas como **Elasticsearch** não fazem vetorização — elas são, na definição usada em sala, "um índice com esteroides": extremamente rápidas para busca de texto e termos em dados não estruturados, com forte paralelismo e tokenização, mas sem o cálculo matemático de proximidade semântica que caracteriza um banco vetorial.

### 4. Busca por similaridade: distância de cosseno e KNN

A busca em um banco de vetores não procura por igualdade exata, mas pela **região mais próxima** do espaço vetorial em relação ao vetor da pergunta — uma busca orientada por **similaridade de vizinhos**, tipicamente usando um modelo estilo **KNN** (K-Nearest Neighbors). A métrica mais usada é a **distância de cosseno**, que varia de **0** (mesma direção, vetores idênticos em orientação) a **2** (direções opostas), passando por **1** (vetores ortogonais, sem relação).

Uma pergunta recorrente na aula foi a diferença conceitual entre a busca vetorial e a busca em grafos (tema da aula anterior): no grafo, a resposta vem de **distância e trajeto** — qual é o tipo de conexão explícita entre dois pontos de dado; no banco vetorial, a resposta vem de **proximidade espacial** calculada em tempo real na hora da consulta — não existe uma aresta pré-definida entre dois vetores, apenas a distância matemática entre suas coordenadas, recalculada a cada busca.

Quando a busca é feita **sem índice** (busca linear), o banco compara o vetor da consulta contra cada vetor da tabela, um por um — funcional em volumes pequenos, mas inviável em escala. Quando o volume cresce, entram os **índices ANN** (Approximate Nearest Neighbor), que trocam uma pequena perda de precisão por um ganho de performance muito grande — tema desenvolvido em profundidade nas seções 11 a 13.

### 5. A escada de maturidade de dados para IA

A aula propõe uma "escada" de três degraus para pensar a maturidade de uma solução baseada em vetores:

| Degrau | Descrição | Exemplos de uso |
|---|---|---|
| **1. Embedding em memória** | Vetorização pura via biblioteca/modelo, guardada em uma lista ou estrutura em memória (NumPy), sem banco dedicado — funciona até a casa de dezenas de milhares de vetores | POCs, classificação de intenção de chat em tempo real |
| **2. RAG embarcado** | Um único processo local com um motor de busca semântica embarcado (Chroma ou FAISS local) | Assistentes sobre manuais, copilotos de código sobre um repositório local |
| **3. Banco de produção** | Banco nativo de vetores ou extensão vetorial sobre um SGBD (pgvector e similares), com suporte a milhões de vetores, concorrência de leitura/escrita, governança, LGPD e RBAC | Ambientes multi-cliente, agentes de produção com múltiplos usuários simultâneos |

O terceiro degrau é o foco do restante da aula: ambientes onde múltiplos clientes acessam agentes simultaneamente, exigindo governança de acesso, conformidade regulatória e capacidade de escala que os dois primeiros degraus não sustentam.

### 6. Anatomia de um banco vetorial e o pgvector

Uma analogia usada para explicar o funcionamento de um banco vetorial foi a de busca por localização: perguntar "quais restaurantes estão perto de mim" ao Google Maps retorna resultados dentro de um raio a partir da sua posição — o banco vetorial faz algo equivalente, buscando os pontos (vetores) mais próximos ao ponto da pergunta, dentro do "raio" (distância) configurado.

Na estrutura de uma linha típica de um banco vetorial, além do ID e do vetor propriamente dito (por exemplo, com 384 dimensões), é comum incluir colunas de metadado (para filtro e contexto) e uma coluna com o caminho/nome do documento original, para permitir a citação da fonte. Uma ressalva importante: um banco vetorial **não é** puramente relacional (embora o pgvector traga as capacidades relacionais junto), e também **não é** um banco de grafos — não há aresta ou nó, apenas blocos de dado cuja vizinhança é calculada em runtime, na hora da consulta, com base na distância entre coordenadas.

O **pgvector** é a extensão que traz capacidade vetorial para dentro do **Postgres**, unificando as vantagens de um banco relacional (ACID, joins, transações, backup) com armazenamento e indexação de vetores. O padrão de uso é: `CREATE EXTENSION vector;` para habilitar a extensão, seguido de um `CREATE TABLE` convencional com uma coluna adicional do tipo `vector(N)` (onde N é o número de dimensões do modelo de embedding usado); o `INSERT` inclui o vetor já calculado pela aplicação (o pgvector não gera embeddings sozinho — isso é responsabilidade da camada de aplicação); e a consulta usa `ORDER BY embedding <=> :vetor_consulta LIMIT k` para retornar os k vizinhos mais próximos, usando o operador de distância de cosseno.

Sobre manutenção em produção — pergunta levantada por um aluno com experiência em Postgres, questionando se o pgvector precisa de uma rotina de "reorg" como um banco relacional tradicional — o professor confirmou que sim: o banco tende a perder performance conforme cresce, e é normal recalibrar o tipo de índice, aumentar o tamanho do chunk (se estiver gerando alucinação por perda de contexto) ou reconstruir o índice periodicamente. Diferente de um banco relacional, onde a degradação costuma aparecer como lentidão mensurável, em um banco vetorial mal calibrado o sintoma mais comum é justamente **alucinação** — respostas incorretas ou fora de contexto — o que torna a observabilidade mais desafiadora: uma prática sugerida foi manter um conjunto fixo de perguntas de referência (com resposta e citação já conhecidas) para monitorar continuamente se a qualidade das respostas do banco está variando ao longo do tempo.

### 7. Chunking: como fatiar os documentos

Um documento inteiro (um PDF, um DOC, uma apresentação) não se torna um único vetor — ele é fatiado em **chunks** (pedaços menores: por frase, por parágrafo, por caractere ou por quebra de linha), e cada chunk vira uma linha/vetor separado no banco. A escolha do critério de fatiamento (e do tamanho do chunk) tem impacto direto na qualidade das respostas: um chunk pequeno demais pode quebrar um contexto que se estende por duas frases ou duas páginas relacionadas, fazendo o modelo perder a conexão entre as partes e gerar **alucinação por referência quebrada** — um problema que o professor relatou já ter enfrentado em projeto real, resolvido apenas ao trocar o algoritmo/tamanho de chunk usado na geração dos vetores.

O laboratório da aula usa o **método do kit** fornecido (`utils.chunk_paragrafo`), que fatia por parágrafo — cada quebra de linha em branco gera um novo chunk, prefixado com um cabeçalho de contexto (por exemplo, título do documento) antes de ser transformado em vetor.

### 8. Modelagem do agente: tabela de conhecimento, tabela de memória e governança

O padrão de modelagem central da aula divide o banco do agente em **duas tabelas com papéis distintos**:

- **Tabela `conhecimento`** — carregada de forma **offline**, contendo manuais oficiais, políticas, FAQs e tabelas vigentes. O agente **apenas lê** essa tabela, tipicamente filtrando por `status = 'oficial'` para garantir que só documentos vigentes sejam citados.
- **Tabela `memoria`** — de escrita e leitura em **tempo real**, onde o agente registra preferências, contexto de conversa e histórico por cliente, sempre filtrada por `cliente_id = :autenticado` para garantir isolamento.

Três regras de governança foram destacadas como críticas em qualquer arquitetura de agente sobre banco vetorial:

1. **O isolamento entre clientes deve ser garantido no código SQL da consulta, nunca delegado ao prompt do LLM.** Confiar que o modelo de linguagem "vai se lembrar" de filtrar por cliente é um risco de segurança real — o filtro precisa estar embutido na função/query, não na instrução textual dada ao agente.
2. **A LGPD exige exclusão física, não lógica.** Um pedido de "direito ao esquecimento" não deve ser resolvido com um soft delete (marcar como excluído, mantendo o dado fisicamente); o fluxo correto envolve um passo de confirmação/validação seguido de exclusão física real, dentro de um processo de conformidade — não uma ação irreversível tomada unilateralmente pelo agente no calor da conversa.
3. **Usar chaves estruturadas** conectando a tabela de memória à base de cadastro do cliente, em vez de depender apenas de texto livre, para reforçar a integridade e a auditabilidade do isolamento.

### 9. Laboratório guiado: estruturando o banco da Operação Q

O primeiro laboratório da aula usa o **Google Colab** para hospedar um Postgres com pgvector, carregando via um kit disponibilizado em um repositório público no GitHub: **59 documentos** fatiados em **244 chunks** de conhecimento oficial, e **24 conversas** históricas de clientes para a base de memória. O ponto de partida deliberadamente entregue pelo professor é um **esquema mínimo** — tabelas com apenas ID, texto e embedding, sem nenhuma coluna de metadado, filtro ou isolamento — para que a turma identifique e corrija as lacunas na prática.

Rodando a consulta inicial ("quanto custa sacar?") sobre esse esquema mínimo, o resultado veio impreciso: em vez de responder diretamente o valor da tarifa vigente, o agente trouxe um trecho longo, incluindo referência a uma tabela de tarifas **arquivada** de um ano anterior — uma demonstração ao vivo de como a ausência de metadado (como uma coluna de `status` distinguindo documento vigente de arquivado) degrada a qualidade da resposta mesmo com a infraestrutura vetorial funcionando corretamente. A partir daí, a atividade guiada foi refinando a estrutura: adicionando colunas de metadado (título, área, tipo, status, data, empresa), habilitando filtro por `status = 'oficial'` na query, e testando como o parâmetro de **limite/K** (quantos vizinhos considerar na busca) afeta o resultado — um aluno (Daniel) levantou uma pergunta operacionalmente relevante: como saber, em produção, se K=3 é o valor certo antes que o cliente receba uma resposta ruim? A resposta do professor foi que essa calibração de K deve ser definida e validada **antes** de o agente ir ao ar, através de testes com perguntas de referência — não descoberta reativamente depois que o cliente já recebeu uma resposta inadequada.

O restante do laboratório implementa a **função de memória do agente** (gravar interação, buscar memória, "esquecer" cliente), e conecta um agente real (usando **Ollama** para gestão local de modelo e o **Qwen 2.5** com 3 bilhões de parâmetros, dimensionado para caber no free tier do Colab) que interage com o banco de vetores através de ferramentas (tools) — uma delas, por exemplo, descrita como "busca política, tarifa e regras oficiais da Quantum Finance para qualquer pergunta sobre a empresa". Ao final, um **avaliador automático** (script determinístico, sem juiz-LLM) analisa o esquema criado, a ingestão, os metadados e a segurança, atribuindo uma pontuação de 0 a 100 — o esquema mínimo de partida, sem nenhum ajuste, pontua **35**.

### 10. Segurança e isolamento: o vazamento de memória entre clientes

A demonstração mais didática da aula sobre risco de segurança veio ao rodar a função de busca de memória **sem nenhum filtro de isolamento**: ao consultar a memória do cliente Bruno (cliente novo, cujo histórico não deveria se misturar com o de ninguém), o agente retornou também informações da cliente Marina (interessada em comprar uma moto) — porque a função `buscar_memoria`, embora recebesse o `cliente_id` como parâmetro, **não usava esse parâmetro no filtro da query SQL**, apenas na função de gravação. A correção discutida ao vivo foi simples de implementar (adicionar a cláusula `WHERE cliente_id = :cliente_id` na busca), mas o ponto pedagógico foi deliberado: mostrar que um agente pode parecer funcionalmente correto (respondendo perguntas, buscando memória) enquanto vaza dados de um cliente para outro, se a camada de isolamento não for auditada explicitamente no código da consulta — reforçando a regra de governança nº 1 da seção 8.

### 11. Busca vetorial em escala: recall, P95 e a necessidade de índices

Sem índice, uma busca vetorial funciona como entrar em uma biblioteca e vasculhar as prateleiras uma a uma; com índice **ANN**, funciona como usar o catálogo da biblioteca para ir direto ao corredor e à prateleira certos. Duas métricas centrais avaliam a qualidade de um índice:

- **Recall** — a precisão do retorno: quantos dos vizinhos verdadeiramente mais próximos foram de fato encontrados pela busca aproximada. Valores próximos de 1 (ou de 90-99%, a depender da escala usada) indicam alta fidelidade em relação à busca exata.
- **P95** — o valor de latência abaixo do qual 95% das consultas ficam. A aula explicou por que se usa P95 em vez de média: uma média pode esconder outliers graves (por exemplo, uma média de 20ms com alguns usuários esperando vários segundos) — o P95 revela melhor a experiência real da cauda mais lenta de usuários, sem cair no ruído estatístico de um P99 (mais sensível a outliers extremos) ou de uma média (que dilui o problema).

À medida que o volume de vetores cresce, a busca linear (sem índice) deixa de ser viável tanto por recall degradado (efeito indireto do volume, se a modelagem de chunk/metadado não acompanhar) quanto, principalmente, por latência — motivando os índices ANN detalhados a seguir.

### 12. HNSW: estrutura, parâmetros e custo de memória

O **HNSW** (Hierarchical Navigable Small World — "mundo pequeno navegável hierárquico") é um índice baseado em **grafo**: cada vetor vira um nó, conectado aos vizinhos mais próximos, organizado em **camadas** — uma camada inferior mais densa (analogia usada em aula: andar a pé, com muitos nós próximos), uma camada intermediária mais esparsa (de táxi) e uma camada superior ainda mais esparsa (de avião), permitindo que a busca "salte" rapidamente pelas camadas superiores até refinar na camada inferior. É importante notar que essa estrutura interna de grafo **não transforma o pgvector em um banco de grafos** — é apenas o algoritmo de indexação usado internamente para localizar vetores mais rápido, sem qualquer relação com o Neo4j da Aula 3.

Os parâmetros centrais do HNSW:

| Parâmetro | Papel | Valor padrão / observado |
|---|---|---|
| **m** | Número máximo de conexões por nó — impacta o recall e o consumo de RAM | 16 |
| **ef_construction** | Tamanho da varredura no momento da construção do índice — quanto maior, mais lento o build, mas melhor a qualidade final | 64 |
| **ef_search** | Tamanho da lista de candidatos considerados em tempo de busca — ajustável em runtime, por sessão | 40 |

O HNSW opera **inteiramente em memória RAM**, o que garante ganhos de performance muito expressivos, mas com custo de infraestrutura proporcional — a fórmula aproximada discutida em aula é **RAM ≈ N × (m × 2 × 8 bytes + d × 4 bytes)**, onde N é o número de vetores e d o número de dimensões. No benchmark medido em aula, sobre 100 mil vetores de 384 dimensões: o **build** do índice levou cerca de **83-99 segundos**, o índice ocupou aproximadamente **195 MB**, e a latência de consulta caiu de **~90ms** (busca sequencial/Seq Scan) para **~7ms** com HNSW — e em testes ao vivo durante o laboratório, o recall variou entre 0,67 e 0,84 dependendo do cenário/filtro, com P95 caindo de mais de 140ms para poucos milissegundos. Um aluno perguntou diretamente se aplicar HNSW é sempre a decisão certa: a resposta do professor foi que, na prática de projetos reais dos últimos anos, o ganho de qualidade e velocidade obtido ao sair de busca vetorial sem índice para HNSW indexado costuma ser "extremamente significativo" — mas o trade-off de memória precisa ser avaliado caso a caso (detalhado na seção 15).

### 13. IVFFlat e quantização de vetores

O **IVFFlat** (Inverted File Index) segue uma lógica bem diferente do HNSW: em vez de um grafo, ele usa **clusterização k-means**, calculando **centróides** que dividem o espaço vetorial em regiões (**lists**), e direcionando cada busca apenas às regiões mais prováveis de conter a resposta. Vantagens: **build muito mais rápido** (cerca de 3-3,5 segundos para 100 mil vetores, contra dezenas de segundos do HNSW) e **sem exigência de RAM dedicada** como o HNSW. Desvantagem central: o recall se degrada mais rapidamente sob **atualização intensa** de dados, exigindo reconstrução do índice com mais frequência do que o HNSW.

O número de **lists** a configurar segue uma regra prática: dividir o número de linhas por 1.000 para bases de até 1 milhão de registros (acima disso, a regra muda para uma função de raiz quadrada do total de linhas). Em tempo de consulta, o parâmetro **probes** define quantos clusters serão de fato examinados na busca — mais probes aumentam a precisão às custas de mais latência.

A **quantização** foi apresentada como uma técnica complementar de compressão de vetores, aplicável tanto isoladamente quanto combinada aos índices acima: o tipo **halfvec** (float16) reduz a RAM pela metade com recall praticamente idêntico ao float32 padrão; e a quantização **binária** (bit) pode reduzir o tamanho do vetor em até **32 vezes**, ao custo de um pré-filtro por distância de Hamming (`<~>`) seguido de um **re-ranking exato** sobre os candidatos reduzidos, para recuperar a precisão perdida na compressão agressiva. Uma analogia usada em aula para quantização: comprimir demais um espaço geográfico é como fundir bairros próximos (Pinheiros, Pompeia, Barra Funda) em uma única região maior — ganha-se velocidade de busca, mas perde-se granularidade fina de resposta.

Sobre quando escolher HNSW versus IVFFlat, o critério discutido foi: HNSW tende a fazer mais sentido para bases menores e mais estáveis, como agentes especialistas em documentação interna de um domínio específico, onde a navegação estruturada em grafo compensa o custo de RAM; IVFFlat tende a ser preferível para volumes maiores e cenários de tempo real com atualização constante, onde o ganho por compressão pesa mais do que a degradação de recall sob escrita intensa.

### 14. Ecossistema de bancos vetoriais: FAISS, pgvector, Pinecone, Weaviate e Qdrant

A aula comparou cinco opções do ecossistema de busca vetorial:

| Critério | FAISS | pgvector | Pinecone | Weaviate | Qdrant |
|---|---|---|---|---|---|
| **Natureza** | Biblioteca C++/Python (Meta) | Extensão do Postgres | SaaS gerenciado | SGBD nativo de grafo/vetor | SGBD nativo (Rust) |
| **Filtro por metadado** | Manual, via código | SQL completo | Suportado nativamente | Suportado nativamente | Suportado, com payloads JSON flexíveis |
| **Escrita/ACID** | Não se aplica (não é banco) | ACID completo | Eventual, conforme uso | Não é o foco central | Não é o foco central |
| **Busca híbrida** | Não | Lógica manual (vetor + SQL) | Nativa | Nativa (vetor + BM25) | Via "sparse vectors" |
| **Operação** | Requer engenharia própria | DBA tradicional | Sem infraestrutura própria | Requer operação de SGBD | Requer operação de SGBD |
| **Consumo de RAM** | Alto | Alto com HNSW | Conforme uso (cobrança por consumo) | Alto | Mais otimizado (ambiente Rust) |

O FAISS foi destacado como uma biblioteca (não um banco) — próxima de um embedding "cru", sem infraestrutura de persistência, ACID ou concorrência de escrita própria. O Pinecone foi descrito como a opção que exige menos esforço de infraestrutura, por ser inteiramente gerenciado. O Weaviate se diferencia por oferecer **busca híbrida nativa** (combinando busca vetorial com BM25, o algoritmo clássico de busca por palavra-chave). O Qdrant foi apontado como especialmente forte para cenários com filtros ricos sobre metadado estruturado em JSON, muito usado quando agentes/LLMs se conectam a sistemas web/mobile com payloads bem definidos.

### 15. Como escolher o índice e o banco certo

O método de decisão proposto segue quatro passos:

1. **Definir o SLA mínimo** da aplicação: recall mínimo aceitável, P95 máximo tolerado, limite de RAM disponível e taxa de escrita esperada.
2. **Estabelecer um gabarito** rodando a mesma consulta com busca exata (Seq Scan) para servir de referência de qualidade máxima possível.
3. **Medir** as variações de índice (HNSW e IVFFlat, com diferentes parâmetros) contra esse gabarito.
4. **Decidir** com base em custo de infraestrutura, performance e SLA de negócio — não apenas pela tecnologia mais nova ou mais badalada.

Um aluno comparou a escolha entre HNSW e IVFFlat com a escolha de engine de armazenamento no MySQL (MyISAM vs. InnoDB) — uma decisão tomada na modelagem da tabela, e não algo parametrizado a cada chamada de código; o professor confirmou a analogia. Outra pergunta discutida foi sobre quantos índices são necessários por tabela: a resposta foi que o índice se aplica **por coluna de vetor**, não por partição de tempo ou de uso — mesmo em uma tabela particionada, o índice cobre a tabela vetorial inteira, e o fator relevante para decidir a frequência de reconstrução do índice é a velocidade de crescimento e atualização do dado, não a divisão em múltiplos índices paralelos.

### 16. Laboratório prático: dimensionando índices por SLA

O segundo laboratório da aula simula a evolução da Quantum Finance para produção: a base de memória cresce para **100 mil vetores**, com mais de **5 mil clientes ativos simulados**, atendendo **três departamentos com SLAs distintos**:

| Cenário | Departamento | Recall mínimo | P95 máximo | Perfil de carga |
|---|---|---|---|---|
| **A** | Atendimento ao vivo | ≥ 0,95 | ≤ 20ms | Inserção intensiva contínua (chat em tempo real) |
| **B** | Auditoria de compliance | ≥ 0,99 | Irrelevante (batch noturno) | Varredura em lote, índice ≤ 100MB |
| **C** | Visão individual por cliente | ≥ 0,90 | ≤ 50ms | Consultas com filtros seletivos por cliente |

O dataset de teste usa **100 mil memórias sintéticas** com 384 dimensões e um **gabarito de 200 consultas** com vizinhos exatos pré-calculados por busca linear, contra o qual o avaliador automático mede recall, P95, tempo de build e aderência ao SLA de cada cenário. Na prática guiada, o professor demonstrou a comparação entre busca sem índice (Seq Scan, recall = 1 mas P95 de 76-192ms) e HNSW configurado (recall caindo para a faixa de 0,67-0,84, mas P95 despencando para 4-5,5ms) — uma troca explícita de precisão marginal por performance, que a turma foi então orientada a repetir formulando hipóteses próprias, testando parâmetros como `ef_search` (via `SET`), `iterative_scan = relaxed_order` (que ajuda o índice a continuar variando ramificações quando há cláusulas de filtro restritivas) e o número de `probes` no IVFFlat, para decidir qual configuração melhor atende cada um dos três cenários de SLA.

### 17. Encerramento e entrega

A entrega da aula é composta por dois laboratórios (o de modelagem/segurança do banco e o de dimensionamento de índices por SLA), mas a nota é atribuída com base em **apenas um deles**, à escolha do aluno — quem concluir os dois pode entregar ambos para feedback qualitativo, mas apenas o escolhido conta para nota. Um desafio bônus opcional (combinando quantização binária com re-ranking e comparação de estratégias de particionamento) foi disponibilizado à parte, valendo até 10 pontos extras. O prazo de entrega foi fixado para o domingo anterior à aula seguinte, dando a turma duas semanas de folga.

No fechamento, o professor resumiu os dois blocos da aula — infraestrutura/modelagem/segurança de banco vetorial no primeiro bloco, engenharia de índice e tomada de decisão técnica no segundo — e reforçou aplicações de mercado que conectam diretamente com o cenário da Quantum Finance: análise de histórico de crédito alinhada a cadastro em sistemas financeiros, agentes de conhecimento interno sobre documentação de processos, e catálogos/comportamento de cliente em e-commerce. A aula seguinte do curso (fora do escopo deste documento) foi anunciada como uma aula de **integração entre bancos**, aprofundando ainda mais a conexão entre bancos vetoriais e agentes de IA.

## Aula 5 — Integração de Dados para Agentes (Os Dutos do Q)

Última aula da disciplina, com o tema batizado nos slides de **"Os Dutos do Q"**: se a Aula 4 resolveu como o agente da Operação Q armazena e busca conhecimento e memória em um banco vetorial, a Aula 5 resolve como o dado chega até esse banco de forma confiável, governada e auditável — o encanamento que sustenta tudo que foi construído até aqui. A aula fecha o curso com dois laboratórios (Missão 1 e Missão 2), ambos girando em torno de um pipeline de ingestão real, escrito por um agente de IA e auditado por outro.

### 1. Por que a fundação de dados sustenta os agentes: três falhas reais

A aula abre com uma provocação: um agente é só tão bom quanto o dado que ele recebe, e um agente que decide, recomenda ou responde a partir de dado errado, desatualizado ou indevidamente retido é um problema de arquitetura de dados escondido atrás de uma conversa fluente. Três falhas concretas foram usadas para ancorar essa ideia ao longo da aula:

- **Dado parado (obsolescência silenciosa)** — um pipeline batch com janela de D+1 alimentando um agente que responde "em tempo real" sobre um saldo ou status que já mudou há horas, sem que ninguém tenha sido avisado do atraso.
- **Exclusão ignorada** — um cliente pede para ser esquecido (LGPD) e o dado é removido da tabela principal, mas continua vivo em uma cópia, em um índice vetorial ou na memória de um agente — o caso da aluna fictícia **Marina**, retomado em detalhe na seção 14.
- **Esquema que muda sem avisar** — uma fonte upstream adiciona, remove ou renomeia uma coluna, e o pipeline downstream ou quebra silenciosamente ou, pior, aceita o dado torto sem alarme, corrompendo tudo que é construído em cima dele.

Essas três falhas foram usadas como fio condutor para justificar, seção a seção, cada peça de engenharia que a aula apresenta a seguir: ingestão correta, contrato de dados, tratamento de schema drift, idempotência/determinismo e o padrão de exclusão auditável.

### 2. Os três paradigmas de ingestão: Batch, CDC e API

A aula organiza toda ingestão de dados em três grandes paradigmas, cada um com um trade-off diferente entre custo, complexidade e atualidade do dado:

| Paradigma | Como funciona | Latência típica | Complexidade | Quando usar |
|---|---|---|---|---|
| **Batch** | Extração agendada, em janelas (ex.: uma vez por dia) | Alta (horas a D+1) | Baixa | Relatórios, cargas históricas, dado que não muda de forma crítica hora a hora |
| **CDC** (Change Data Capture) | Lê o log de transações do banco de origem e publica cada mudança como evento | Segundos | Alta | Sistemas transacionais críticos, onde o downstream precisa refletir o estado atual quase em tempo real |
| **API** | Consumo via chamada HTTP, por *polling* (o consumidor pergunta periodicamente) ou *webhook* (a fonte avisa quando algo muda) | Minutos (polling) a segundos (webhook) | Média | Integração entre sistemas de terceiros ou serviços que não expõem acesso direto ao banco |

O **CDC** foi explicado com o **Debezium** como implementação de referência: em vez de fazer `SELECT * FROM tabela` repetidamente (o que sobrecarrega o banco de origem e ainda assim pode perder mudanças entre uma consulta e outra), o Debezium lê diretamente o **log de transações** do banco — o Redo Log no Oracle, o WAL (Write-Ahead Log) no Postgres — e publica cada `INSERT`/`UPDATE`/`DELETE` como um evento em um tópico Kafka, incluindo o estado anterior e o novo estado da linha (*before/after image*). A vantagem central: o CDC captura a mudança no momento em que ela acontece no banco, sem tocar diretamente nas tabelas de produção com consultas pesadas repetidas.

Para o paradigma de **API**, a turma discutiu a diferença prática entre **polling** (o consumidor pergunta "tem algo novo?" em intervalos fixos — simples de implementar, mas desperdiça chamadas quando não há novidade e pode atrasar a detecção de mudança) e **webhook** (a fonte empurra o evento assim que ele acontece — mais eficiente e quase em tempo real, mas exige que o consumidor exponha um endpoint disponível para receber a notificação). Dois exemplos reais trazidos pela turma ilustraram o contraste: o **QR Code do PIX**, em que o sistema de pagamentos notifica via webhook assim que a transação é confirmada (o cliente não fica consultando o status a cada segundo), contra cenários de mercado financeiro em que o consumo é feito por **polling** programado, porque a fonte de dado não oferece webhook ou porque o consumidor prefere controlar explicitamente a cadência de consulta.

### 3. Batch: a janela de obsolescência

Mesmo sendo o paradigma mais simples e mais barato de operar, o batch carrega um custo implícito que a aula chamou de **janela de obsolescência**: entre o momento em que o dado muda na origem e o momento em que ele é refletido no destino, existe uma janela de tempo (tipicamente **D+1**, ou seja, o dado de hoje só aparece amanhã) em que qualquer consumidor downstream — inclusive um agente de IA — está, tecnicamente, trabalhando com informação desatualizada. A decisão de usar batch não é um erro em si — para relatórios mensais ou cargas históricas é a opção certa, mais barata e mais simples — mas o arquiteto precisa deixar explícito para quem consome esse dado que ele carrega essa defasagem, principalmente quando esse consumidor é um agente que responde a um cliente como se estivesse vendo o presente.

### 4. ETL vs. ELT: onde a transformação acontece

A diferença entre **ETL** (Extract, Transform, Load) e **ELT** (Extract, Load, Transform) está na ordem em que a transformação acontece em relação à carga:

| | ETL | ELT |
|---|---|---|
| **Ordem** | Extrai → transforma (fora do destino) → carrega já transformado | Extrai → carrega bruto → transforma dentro do próprio destino |
| **Dado bruto sobrevive?** | Não necessariamente — o dado original pode não ser preservado após a transformação | Sim — o dado bruto fica persistido no destino, disponível para reprocessamento |
| **Onde roda o processamento** | Em um motor de transformação externo, antes de chegar ao destino | No próprio motor de armazenamento/processamento do destino (ex.: warehouse ou lakehouse com poder computacional) |
| **Custo** | Processamento pago fora do destino, geralmente em uma ferramenta de ETL dedicada | Processamento pago dentro do próprio destino, aproveitando o poder computacional que ele já tem |

O ELT ganhou força com o Data Lakehouse justamente porque passou a ser viável (e mais barato) transformar dentro do mesmo motor que já guarda o dado, em vez de manter uma camada de transformação separada — e porque preservar o dado bruto do jeito que chegou é o que permite reprocessar do zero quando uma regra de transformação muda ou quando se descobre um erro. A aula trouxe um exemplo do mercado de **games/streaming** (citado a partir de uma apresentação em um evento de Big Data em Nova York, sobre a Activision e o Call of Duty) para mostrar o outro lado: em cenários de streaming de altíssimo volume, às vezes nem faz sentido falar estritamente em ETL ou ELT — a transformação acontece continuamente, em micro-lotes, e a fronteira entre "extrair", "carregar" e "transformar" se dilui na prática.

### 5. Bronze, Silver, Gold: a jornada do dado e o debate sobre governança (SOR, SOT, SPEC)

Retomando a arquitetura **Medallion** (já introduzida na Aula 1, dentro do Delta Lake), a aula detalhou o papel de cada camada dentro do fluxo de ingestão:

| Camada | Conteúdo | Transformação aplicada |
|---|---|---|
| **Bronze** | Dado bruto, exatamente como chegou da fonte | Nenhuma — cópia fiel, inclusive de eventuais erros e inconsistências |
| **Silver** | Dado limpo, com schema validado, deduplicado, tipado corretamente | Limpeza, padronização, validação de contrato |
| **Gold** | Dado agregado e modelado para consumo direto | Agregações, junções, métricas de negócio já calculadas |

A discussão em sala foi além do que os slides trazem: um aluno questionou se nomear as camadas por bronze/silver/gold (que descrevem **estágio de processamento**) não confunde o time com a ideia de **confiabilidade/governança** do dado — afinal, um dado pode estar tecnicamente na camada silver e ainda assim não ser a fonte confiável para uma decisão de negócio. Isso levou à discussão de três termos usados no mercado para tratar exatamente da confiabilidade, e não do estágio de processamento:

- **SOR (System of Record)** — o sistema onde o dado nasce e é oficialmente registrado; a origem transacional.
- **SOT (Source of Truth / Fonte da Verdade)** — o local (não necessariamente o SOR) que é designado como referência oficial para consulta, podendo já ser uma versão processada e curada do dado.
- **SPEC** — usado em aula para se referir à especificação/contrato que define o formato esperado do dado, amarrando o que a fonte promete entregar ao que o consumidor espera receber.

O ponto de fechamento da discussão: Medallion (bronze/silver/gold) descreve **onde o dado está no pipeline**; SOR/SOT descrevem **em quem confiar**; e um bom desenho de governança usa os dois vocabulários lado a lado, sem tratar "estar na camada gold" como sinônimo automático de "ser a fonte da verdade" — a validação de contrato (seção 6) é o que efetivamente garante essa confiança, não o nome da camada.

### 6. Metadados e contratos de dados

Um **Data Contract** foi apresentado como um acordo formal, versionado e legível por máquina (tipicamente escrito em **YAML**) entre quem produz um dado e quem o consome, especificando estrutura, tipos, regras de qualidade e SLA de atualização — a peça de engenharia que dá sustentação prática ao conceito de **Data as a Product** do Data Mesh (Aula 1). Um data contract elimina a ambiguidade do "descobri em produção que o campo mudou de tipo", trazendo a validação para antes da ingestão.

A aula organizou os metadados descritos em um contrato em três categorias, cada uma com um dono diferente:

| Tipo de metadado | O que descreve | Dono típico |
|---|---|---|
| **Técnico** | Schema, tipos de dado, formato do arquivo, chaves | Time de engenharia de dados |
| **De negócio** | Significado do campo, regras de negócio, glossário, sensibilidade (PII) | Time de negócio / domínio dono do dado |
| **Operacional** | SLA de atualização, frequência de carga, ownership, contato para incidentes | Time de operação/plataforma de dados |

O contrato de dados usado no laboratório da aula (seção 12) é entregue como um YAML incompleto, com lacunas propositais que o time precisa preencher corretamente para que o pipeline funcione — a validação contra esse contrato é justamente o que decide se uma mudança de schema é aceita, rejeitada linha a linha, ou rejeita o arquivo inteiro (seção 7).

### 7. Schema drift: o que fazer quando o esquema muda sem avisar

**Schema drift** é quando a estrutura de um dado muda sem aviso prévio — uma coluna nova aparece, uma coluna esperada some, um tipo muda de inteiro para texto. A aula apresentou três estratégias possíveis de resposta, em ordem crescente de rigor:

1. **Aceitar em silêncio** — o pipeline simplesmente ingere o dado com a mudança, sem alertar ninguém. Classificada em aula como a **pior opção**: o problema não desaparece, só fica invisível até explodir mais tarde, geralmente na forma de um relatório errado ou de um agente respondendo com base em um campo mal interpretado.
2. **Rejeitar a linha** — o pipeline descarta apenas os registros que não respeitam o contrato, deixando passar o restante. Reduz o dano, mas ainda exige monitoramento para não perder dado silenciosamente linha a linha.
3. **Rejeitar o arquivo inteiro** — qualquer desvio de schema barra a carga inteira daquele lote, forçando intervenção humana antes de prosseguir. Foi a estratégia adotada como padrão no kit de laboratório da aula, justamente por ser a mais conservadora: força visibilidade do problema antes que qualquer dado contaminado entre no lake.

A escolha entre as três não é puramente técnica — depende de quão crítico é o dado e de qual é o custo de um falso negativo (deixar passar um dado ruim) versus o custo de um falso positivo (parar um pipeline inteiro por uma mudança inofensiva).

### 8. Idempotência e determinismo

Dois conceitos tratados como pré-requisito para qualquer pipeline confiável, especialmente quando ele pode ser reexecutado (por falha, por reprocessamento ou por um agente que decide rodar de novo):

**Idempotência** é a propriedade de que executar o mesmo pipeline duas vezes sobre o mesmo dado produz o mesmo resultado final, sem duplicar registros. As técnicas discutidas:

- **Chave natural** — usar um identificador de negócio estável (não um ID técnico gerado a cada execução) como chave de deduplicação.
- **MERGE, não APPEND** — em vez de sempre inserir (`APPEND`), o pipeline deve fazer um `MERGE` (upsert): se o registro já existe pela chave natural, atualiza; se não existe, insere. Rodar o mesmo lote duas vezes com `APPEND` duplica dado; com `MERGE`, o resultado final é idêntico.
- **Hash da linha** — calcular um hash do conteúdo da linha para detectar se ela de fato mudou, evitando reescrever (e gerar uma nova versão/timestamp) um registro que chegou de novo mas está idêntico ao que já existe.

**Determinismo** é a garantia de que, dado o mesmo dado de entrada, o pipeline sempre produz a mesma saída. A aula listou o que costuma **quebrar** determinismo na prática:

- Uso de `now()` ou `today()` dentro da lógica de transformação — o resultado passa a depender de *quando* o pipeline roda, não só do dado.
- Depender da **ordem de leitura dos arquivos** quando essa ordem não é garantida pelo sistema de arquivos ou pela fonte.
- IDs gerados pelo próprio destino (`auto increment`, UUID aleatório) em vez de vindos da origem ou derivados de forma determinística do conteúdo.
- `LIMIT` sem `ORDER BY` explícito, ou qualquer consulta sem paginação/corte determinístico, que pode trazer conjuntos de linhas diferentes em execuções diferentes.

Essa parte gerou boa discussão na turma, com alunos trazendo experiência real de **core banking** e de arquiteturas de **microsserviços**, relatando casos concretos em que um pipeline "funcionava sempre" até que a ordem de chegada de dois arquivos mudou, ou até que um `now()` escondido dentro de uma view intermediária começou a gerar resultados diferentes em reprocessamentos do mesmo dia.

### 9. Time travel e auditoria de inferência

Uma das vantagens do **Delta Lake** (e de formatos de tabela transacional equivalentes) retomada da Aula 1 é o **versionamento nativo**: cada operação de escrita (insert, update, delete, merge) gera uma nova versão da tabela, sem descartar as anteriores. Isso permite **time travel** — consultar a tabela exatamente como ela estava em uma versão ou um timestamp específico no passado.

No contexto de agentes, essa capacidade ganha um uso adicional além da auditoria contábil clássica: **auditoria de inferência**. Se um agente tomou uma decisão ou deu uma resposta às 14h de uma terça-feira, o time travel permite reconstruir exatamente qual era o estado do dado (conhecimento e memória) que o agente enxergava naquele momento — essencial para investigar por que um agente respondeu algo específico, especialmente quando o dado subjacente muda com frequência.

### 10. O ferramental: do laboratório à produção

A aula fez questão de separar o ferramental usado no ambiente de laboratório do ferramental típico de produção, para que a turma não confundisse "o que dá para aprender em um Colab" com "o que uma arquitetura de produção real usa em escala":

| | Laboratório (aula) | Produção (mercado) |
|---|---|---|
| **Motor de tabela transacional** | `delta-rs` (implementação Rust do Delta Lake, sem precisar de um cluster Spark) | Spark com Delta Lake nativo |
| **Motor de consulta** | DuckDB (embutido, roda no próprio processo, sem infraestrutura) | Spark com Photon (motor de execução vetorizado) |
| **Ambiente de execução** | Google Colab | Cluster gerenciado (Databricks, EMR, Dataproc) |
| **Governança/catálogo** | Convenções manuais no laboratório | Unity Catalog (ou equivalente) |
| **Ingestão incremental automatizada** | Simulada manualmente no laboratório | Auto Loader (ou equivalente) |

A escolha de `delta-rs` e DuckDB para o laboratório foi justificada pela leveza: os mesmos conceitos de contrato, idempotência, schema drift e time travel se aplicam igualmente em ambos os ambientes, mas o laboratório usa ferramentas que rodam localmente, sem exigir cluster, para que o foco fique na lógica de arquitetura e não na configuração de infraestrutura.

### 11. Agent 1, o Construtor, e o conceito de agent harness

A aula introduziu o conceito de **agent harness** — a estrutura que envolve e disciplina um agente de IA para que ele não apenas "converse", mas execute uma tarefa de engenharia de forma confiável e auditável. Um harness bem desenhado tem quatro peças:

1. **Superfície** — o conjunto de ferramentas e permissões que o agente de fato pode acionar (o que ele pode ler, escrever, chamar).
2. **Guardrail** — as regras que impedem o agente de tomar uma ação fora do escopo permitido, mesmo que o modelo "queira" (por exemplo, escrever fora do schema do contrato).
3. **Eval determinística** — testes automatizados, sem ambiguidade, que checam se a saída do agente atende a critérios objetivos (o pipeline gerado passa no teste de schema? é idempotente?).
4. **Juiz por LLM** — para critérios mais qualitativos, que não se reduzem a um teste determinístico (a qualidade do código está boa? o pipeline está bem documentado?), um segundo modelo de linguagem avalia a saída do primeiro.

Esse harness foi aplicado, no laboratório da aula, ao primeiro de três agentes do fluxo: o **Agente 1, "O Construtor"**, responsável por escrever o próprio pipeline de ingestão a partir do contrato de dados em YAML, usando um modelo pequeno e local, o **Qwen2.5-Coder 1.5B**, rodado dentro do próprio ambiente do laboratório (sem depender de uma API externa paga) — uma escolha deliberada para que a turma pudesse rodar o exercício de ponta a ponta sem custo de inferência.

### 12. Missão 1: o duto batch (laboratório)

O primeiro laboratório da aula, **Missão 1 — "O duto batch"**, coloca a turma para construir (com o Agente 1, o Construtor, escrevendo o código) um pipeline de ingestão batch a partir de um contrato de dados em YAML com **lacunas propositais** que precisam ser corretamente preenchidas antes que o pipeline funcione — testando, na prática, se o aluno entendeu contrato, schema drift, idempotência e determinismo o suficiente para revisar criticamente o que a IA gera, e não apenas aceitar o primeiro resultado.

A pontuação da missão segue uma rubrica detalhada, somando até 100 pontos entre seis critérios (25/20/25/10/10/10), mais um componente especial de **"Caos"** que pode subtrair até 20 ou somar até 20 pontos dependendo de como o pipeline se comporta diante de um cenário de dado inesperado injetado propositalmente pelo avaliador automático. A pontuação final é convertida em uma classificação:

| Faixa de pontuação | Classificação |
|---|---|
| ≥ 95 | **Ouro** |
| ≥ 80 | **Prata** |
| ≥ 60 | **Bronze** |
| < 60 | Não atingiu o mínimo |

Na discussão em sala sobre a dificuldade da missão, o aluno **Daniel** trouxe um feedback direto sobre o quanto o exercício exigia — sentindo o laboratório mais abstrato e mais distante do dia a dia do que os anteriores. O professor **Murilo** respondeu reforçando o papel esperado da turma dentro do exercício: **"a gente é só o arquiteto de dados aqui"** — o aluno não precisa escrever o pipeline linha a linha; precisa saber revisar, entender e corrigir o que o Agente 1 constrói, da mesma forma que um arquiteto de dados revisa criticamente o que uma IA generativa produz em um ambiente real de trabalho, eco direto da mesma mensagem já reforçada no laboratório SQL da Aula 2 ("o papel de vocês como arquiteto não muda: a IA acelera, mas não substitui").

Um problema técnico à parte também surgiu durante a execução prática: dificuldades no upload do arquivo `.zip` do laboratório no Colab levaram a um pequeno desvio de aula para troubleshooting em conjunto, resolvido reorientando os alunos afetados sobre o caminho correto de upload dentro do ambiente.

### 13. Cursor e efeito líquido

Voltando ao paradigma de ingestão via **API** (seção 2), a aula detalhou o padrão de **cursor**: em vez de repuxar a base inteira a cada execução, o pipeline guarda um cursor (tipicamente uma data/timestamp da última execução bem-sucedida, o padrão **cursor-by-date**) e, na próxima execução, pede à API apenas os registros alterados desde esse cursor — reduzindo drasticamente o volume de dado transferido e processado em cada rodada.

Esse padrão se conecta ao conceito de **efeito líquido**, discutido em conjunto com **SCD** (Slowly Changing Dimension, já mencionado na Aula 2 a propósito do histórico de preço): a diferença entre manter apenas um campo `updated_at` sobrescrito a cada mudança (perdendo o histórico intermediário) e manter uma nova versão a cada mudança relevante (preservando o histórico, ao custo de mais armazenamento e, quando o dado alimenta um banco vetorial, mais custo de reembedding a cada nova versão gerada) — uma decisão de arquitetura que precisa pesar o valor de manter histórico completo contra o custo de reprocessamento e de embedding repetido.

### 14. LGPD e o padrão outbox: o caso Marina

Retomando a primeira das três falhas da seção 1, a aula detalhou o **caso Marina**: uma cliente fictícia que exerce seu **direito de ser esquecida**, garantido pela LGPD, pedindo a exclusão de seus dados pessoais. O problema prático é que, em uma arquitetura com múltiplas camadas (Bronze/Silver/Gold), múltiplas cópias derivadas e, no caso de um agente, um banco vetorial com memória e conhecimento indexados, "apagar o dado" não é uma operação única — é uma operação que precisa se propagar de forma confiável e auditável por vários lugares.

O padrão apresentado como solução foi o **outbox pattern**, adaptado ao fluxo de exclusão: o pedido de exclusão de Marina entra como um evento (**Pedido → Silver → Outbox → Fora do lake**), passando pela camada Silver para validação e enriquecimento, sendo então publicado em uma tabela/tópico de **outbox** dedicado, que outros consumidores (incluindo o índice vetorial do agente) leem para efetivamente remover ou anonimizar o dado correspondente em seus próprios domínios — garantindo que a exclusão se propague de forma rastreável, em vez de depender de cada sistema downstream "lembrar" de checar se algo precisa ser apagado.

Um ponto de nuance discutido em aula: nem todo dado pode simplesmente sumir, mesmo diante de um pedido de exclusão — obrigações regulatórias (fiscais, contábeis, de prevenção a fraude) frequentemente exigem retenção por um prazo legal mínimo. A solução apresentada para esse conflito foi o padrão de **"legal DB"**: um armazenamento separado, de acesso restrito, isolado do restante da plataforma de dados (e, portanto, fora do alcance de qualquer agente ou pipeline de consumo geral), onde o dado que precisa ser retido por obrigação legal fica guardado apenas para fins de compliance, enquanto todo o resto da plataforma — incluindo a memória e o conhecimento do agente — trata Marina como efetivamente esquecida.

### 15. Menor privilégio: o agente invoca, a view lê

Conectando de volta à seção 10 da Aula 4 (o vazamento de memória entre clientes), a aula reforçou o princípio de **menor privilégio** como regra de ouro para qualquer agente com acesso a dado: o agente nunca deve ter acesso direto e irrestrito a SQL cru sobre as tabelas de produção. Em vez disso, o agente invoca **ferramentas (tools)** parametrizadas, que por sua vez leem através de **views** já restritas e filtradas (por exemplo, uma view que já embute o filtro `WHERE cliente_id = :id_do_agente_atual`), de forma que a superfície de acesso do agente seja definida pela arquitetura, não pela boa vontade do prompt.

Esse desenho tem duas vantagens diretas: reduz drasticamente a chance de um agente vazar dado de um cliente para outro (o cenário discutido na Aula 4) e torna o acesso **auditável** — cada chamada de ferramenta fica registrada, com parâmetros explícitos, em vez de uma query SQL livre que poderia ser praticamente qualquer coisa.

### 16. Model Context Protocol (MCP) e os três agentes trabalhando juntos

O **Model Context Protocol (MCP)** foi apresentado como o padrão que formaliza essa relação entre agente e ferramenta, resolvendo o que a aula chamou de **problema N×M**: sem um protocolo comum, cada combinação de agente e sistema (banco de dados, API, arquivo) exige uma integração sob medida, e o número de integrações cresce multiplicativamente à medida que se somam mais agentes e mais sistemas. O MCP resolve isso definindo três primitivas padronizadas:

- **Tools** — ações que o agente pode invocar (equivalente às views parametrizadas da seção 15).
- **Resources** — dados que o agente pode ler como contexto.
- **Prompts** — templates de instrução reutilizáveis que o servidor MCP expõe ao agente.

Com esse protocolo como base, a aula fechou o desenho de arquitetura da Operação Q com uma orquestração de **três agentes** trabalhando em conjunto, cada um com uma responsabilidade isolada (reforçando, mais uma vez, o princípio de menor privilégio, agora aplicado entre agentes, não só entre agente e dado):

1. **Agente 1 — "O Construtor"** (seção 11): escreve o pipeline de ingestão a partir do contrato YAML.
2. **Agente 2 — "O Auditor"**: valida o pipeline gerado pelo Construtor contra o contrato de dados e as regras de qualidade, retornando um veredito simples de **PASS/FAIL** — funcionando como a "eval determinística" e o "guardrail" do harness aplicados automaticamente a cada pipeline novo, antes que ele chegue a tocar em dado real.
3. **Agente 3 — "O Q"**: o agente final da disciplina, que efetivamente consome o dado já governado, limpo e validado pelos dois primeiros, para responder a perguntas e tomar decisões — fechando o ciclo iniciado na Aula 4.

### 17. Missão 2, o futuro dos pipelines (YAML como padrão) e encerramento da disciplina

O segundo laboratório da aula, **Missão 2 — "Serventia segura e governança"**, aplica de forma prática o padrão outbox do caso Marina (seção 14) e o princípio de menor privilégio (seção 15): a turma implementa o fluxo de exclusão de Marina de ponta a ponta e valida que o Agente 2 (o Auditor) de fato bloqueia qualquer tentativa de acesso ou resposta que ainda dependa do dado que deveria ter sido esquecido. A pontuação segue uma rubrica de quatro critérios somando 100 pontos (40/20/20/20), com o veredito do **Agente Auditor** avaliado à parte, também em 100 pontos — mas com uma regra de corte explícita: se a memória de Marina **sobreviver** em qualquer lugar que não seja o "legal DB", a pontuação da missão fica **travada em 40 pontos**, independentemente de qualquer outro critério ter sido cumprido corretamente — uma forma de deixar claro, na prática da nota, que a exclusão de dado pessoal não é um critério entre outros, é uma condição bloqueante.

Fechando a disciplina, a aula trouxe um exemplo real de mercado, citado a partir de uma apresentação da **Cogna** em um evento da **Databricks**: a tendência observada é de pipelines cada vez mais **parametrizados inteiramente em YAML**, com a lógica de transformação genérica e reutilizável escondida atrás do motor de execução, e cada novo pipeline sendo, na prática, apenas um novo arquivo de configuração — não mais código novo escrito do zero. O professor reforçou essa tendência com sua própria experiência de mercado, incluindo passagens por empresas como a **Quinto Andar**, onde esse movimento de "pipeline como configuração, não como código" já está em curso.

No encerramento, o professor recapitulou os cinco encontros da disciplina — do dado bruto e das arquiteturas de referência (Aula 1), passando pelos bancos relacionais e colunares (Aula 2), pelos bancos de documento e de grafo (Aula 3), pelos bancos vetoriais e a fundação de agentes (Aula 4), até os dutos de integração e governança que sustentam tudo isso (Aula 5) — como uma progressão única: da forma de guardar o dado até a forma de movê-lo com confiança para dentro de um agente de IA. A turma foi lembrada do prazo de entrega das duas missões da aula, fixado para o primeiro domingo de outubro, e convidada a preencher a pesquisa de avaliação da disciplina antes do encerramento oficial do curso.
