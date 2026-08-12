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
