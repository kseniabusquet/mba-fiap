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
