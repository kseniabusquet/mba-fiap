# Ficha de decisão — Bloco 1 (rascunho, para o esquadrão revisar e assinar)

## D1. A lacuna mais cara

**Lacuna escolhida: LACUNA 8 — regras de sinal em `transacoes.yaml`.**

Preenchemos duas regras: `deposito_positivo` (`tipo != 'deposito' or valor > 0`) e `saida_negativa`
(`tipo not in ['saque','pix','cdb_aplicacao','compra_cartao'] or valor < 0`).

**Evidência:** no `transacoes.csv` do lote inicial, T990003 (`deposito`, valor `-300.00`) e T990004
(`deposito`, valor `-10.00`) são as únicas exceções ao padrão do arquivo inteiro — rodamos o contrato
contra as 2.011 linhas e confirmamos que todo `deposito` legítimo é positivo (min 0, exceto essas duas
plantadas) e todo `saque`/`pix`/`cdb_aplicacao`/`compra_cartao` é sempre negativo (entre -R$4.986 e
-R$20). Sem essa regra, essas duas linhas entrariam na Silver como depósitos negativos válidos.

**O que essa decisão rejeita que talvez fosse legítimo:** um estorno de depósito (o banco reverte um
depósito por erro operacional ou fraude) é legitimamente uma saída de caixa lançada com `tipo=deposito`
e `valor` negativo em alguns modelos de dados — e a nossa regra rejeitaria essa linha como se fosse
sujeira, quando na verdade seria um evento de negócio real que precisaria de um `tipo` próprio
(`estorno_deposito`) para não cair na quarentena. Validamos contra os dados de 2026 que temos e não
existe nenhuma linha assim no corpus, mas é o tipo de falso positivo que só aparece quando o produto
lança uma funcionalidade nova.

**Se a lacuna tivesse ficado em branco:** as quatro linhas com sinal errado (T990003, T990004, e o
equivalente do lado das saídas, se existisse) entrariam na Silver normalmente. O saldo calculado a
partir dessas transações ficaria sistematicamente errado, e é exatamente o tipo de erro que não dá
exceção nem warning — só aparece quando alguém soma o extrato e a conta não fecha, ou pior, quando o Q
informa um saldo errado para o cliente.

---

## D2. O que faltava na instrução

*Ainda em aberto — precisa ser respondido depois de rodar com o modelo de verdade (Qwen2.5-Coder-1.5B)
no Colab.* No ambiente em que preparamos este rascunho não temos acesso à internet necessária para
baixar o modelo (Hugging Face bloqueado), então validamos a lógica do contrato com o motor de regras
puro (`kit/contrato.py`) e com o backend `mock` do kit, que usa respostas canônicas fixas e **não
depende do texto da system message** — ou seja, não serve para responder esta pergunta.

Quando rodarem de verdade no Colab com `agentes.carregar_modelo(...)`, prestem atenção em duas frases
específicas da nossa system message e testem removê-las para ver se o Construtor erra:

- *"clientes vem primeiro porque transacoes tem chave estrangeira para cliente_id"* — sem essa frase, é
  bem provável que o modelo de 1,5B devolva uma ordem plausível mas errada (ex.: ordem alfabética), e o
  teste de fumaça vai acusar a maior parte das transações órfãs, igual ao bug descrito no enunciado.
- *"marquem o arquivo como processado com zero linhas nas duas contagens... e só depois somem 1 em
  drift e 1 em rows_rejected"* — essa é a parte mais fácil do modelo errar, porque pede pra ele lembrar
  que `ok` e `q` não existem dentro do bloco `except`. Se ele tentar usar `len(ok)` ali, o guardrail
  estático de sintaxe/nome indefinido deve reprovar na primeira tentativa.

Depois de rodar, substituam este parágrafo pela experiência real: o que o teste de fumaça acusou (se
acusou), o que vocês mudaram na system message, e qual decisão do pipeline (provavelmente a ordem das
fontes, que exige entender a FK) vocês não delegariam a um agente mesmo com instrução perfeita.

---

## D3. A linha da quarentena que vocês discordam

**Linha escolhida: `TF005` em `silver.quarentena` (fonte tarifas), motivo
`sem_sobreposicao_vigencia: sobrepõe TF001`.**

TF001 (saque, R$7,00, vigente de 2025-01-15 a 2026-01-09) e TF005 (saque, R$6,50, vigente de
2025-06-01 a 2025-08-01) se sobrepõem por inteiro — TF005 está cravado dentro do período de TF001.
O contrato rejeita TF005 (a segunda linha na ordenação por `vigencia_inicio`).

**Por que discordamos (ou pelo menos, por que a rejeição sozinha não resolve o problema):** o dado não
nos diz *qual das duas está errada*. Pode ser TF005 uma promoção temporária de dois meses (R$6,50 em
vez de R$7,00) que o time de produto lançou sem atualizar TF001 para refletir a pausa — nesse caso
TF001 é que deveria ter sido dividida em duas vigências (antes e depois da promoção), e TF005 é o dado
correto que faltou o "fechamento" da tarifa concorrente. O contrato manda a rejeitada para a quarentena
com motivo legível, mas não decide qual das duas é a verdade — só decide que as duas juntas não podem
estar vigentes ao mesmo tempo.

**O que mudaria no contrato, e o que isso quebraria:** poderíamos mudar a regra para, em vez de
descartar a mais recente, fechar automaticamente a vigência da mais antiga na data de início da mais
nova (regra de "a última vigência declarada vence"). Isso resolveria o caso da promoção, mas quebraria
o caso oposto: se TF005 fosse um erro de digitação (alguém subiu uma tarifa errada por engano com
vigência curta), a correção automática aplicaria esse erro como se fosse verdade, e ninguém revisaria.
Preferimos o comportamento atual — rejeitar e deixar visível na quarentena — porque um "quanto custava
o saque em julho de 2025" errado silenciosamente é pior do que um dado ausente que alguém do Red Team
vai notar e resolver com o time de produto antes do próximo `apply`.
