# Avaliação e Métricas

## Como Avaliar o Agente

A avaliação do agente financeiro será realizada por meio de **testes estruturados**, utilizando os dados disponíveis na base de conhecimento. O objetivo é verificar se o agente consegue interpretar corretamente as informações financeiras, responder de forma coerente com o perfil do cliente e evitar a criação de informações que não estejam disponíveis nos dados fornecidos.

A avaliação será dividida em três aspectos principais: **assertividade, segurança e coerência**.

## Métricas de Qualidade

| Métrica           | O que avalia                                                                | Exemplo de teste                                                                                          |
| ----------------- | --------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| **Assertividade** | Verifica se o agente responde corretamente à pergunta realizada             | Consultar o valor gasto em determinada categoria e comparar com os dados de `transacoes.csv`              |
| **Segurança**     | Verifica se o agente evita inventar informações                             | Perguntar sobre um produto que não existe na base e verificar se o agente informa que não possui os dados |
| **Coerência**     | Verifica se as respostas são compatíveis com o perfil financeiro do cliente | Solicitar uma recomendação de investimento e verificar se ela está de acordo com o perfil registrado      |
| **Clareza**       | Verifica se as respostas são compreensíveis e objetivas                     | Fazer uma pergunta financeira e avaliar se a explicação é fácil de entender                               |

## Cenários de Teste

### Teste 1 — Consulta de gastos

* **Pergunta:** "Quanto gastei com alimentação?"
* **Fonte dos dados:** `transacoes.csv`
* **Resposta esperada:** O agente deve consultar as transações e apresentar o valor correspondente aos gastos com alimentação.
* **Resultado:** [ ] Correto  [ ] Incorreto

### Teste 2 — Consulta financeira

* **Pergunta:** "Qual é a minha situação financeira atual?"
* **Fonte dos dados:** `transacoes.csv` e demais dados financeiros disponíveis.
* **Resposta esperada:** O agente deve apresentar uma análise baseada nos dados disponíveis, destacando receitas, despesas e possíveis pontos de atenção.
* **Resultado:** [ ] Correto  [ ] Incorreto

### Teste 3 — Recomendação de investimento

* **Pergunta:** "Qual investimento você recomenda para mim?"
* **Fonte dos dados:** `perfil_investidor.json` e `produtos_financeiros.json`
* **Resposta esperada:** O agente deve recomendar uma opção compatível com o perfil do cliente e explicar de forma clara o motivo da recomendação.
* **Resultado:** [ ] Correto  [ ] Incorreto

### Teste 4 — Pergunta fora do escopo

* **Pergunta:** "Qual a previsão do tempo para amanhã?"
* **Resposta esperada:** O agente deve informar que sua finalidade é auxiliar em questões financeiras e que a pergunta está fora de seu escopo.
* **Resultado:** [ ] Correto  [ ] Incorreto

### Teste 5 — Informação inexistente

* **Pergunta:** "Quanto rende o produto XYZ?"
* **Resposta esperada:** Caso o produto não esteja presente na base de conhecimento, o agente deve informar que não possui informações suficientes para responder, sem inventar dados.
* **Resultado:** [ ] Correto  [ ] Incorreto

## Avaliação com Usuários

Além dos testes estruturados, o agente poderá ser testado por **3 a 5 pessoas**. Cada participante deverá avaliar as respostas utilizando uma escala de **1 a 5**, considerando as métricas definidas anteriormente.

| Avaliador   | Assertividade | Segurança | Coerência | Clareza |
| ----------- | ------------: | --------: | --------: | ------: |
| Avaliador 1 |               |           |           |         |
| Avaliador 2 |               |           |           |         |
| Avaliador 3 |               |           |           |         |
| Avaliador 4 |               |           |           |         |
| Avaliador 5 |               |           |           |         |
| **Média**   |               |           |           |         |

## Resultados

Após a realização dos testes, serão registrados os principais pontos positivos e oportunidades de melhoria do agente.

**O que funcionou bem:**

* [Descrever os pontos positivos identificados durante os testes.]
* [Registrar respostas que apresentaram alta assertividade.]
* [Registrar situações em que o agente demonstrou segurança ao reconhecer limitações.]

**O que pode melhorar:**

* [Descrever respostas que apresentaram erros ou inconsistências.]
* [Registrar informações que precisam ser adicionadas ou corrigidas na base de conhecimento.]
* [Identificar possíveis melhorias nas instruções do agente.]

## Métricas Técnicas — Opcional

Caso seja necessário realizar uma avaliação mais aprofundada, também podem ser acompanhadas métricas técnicas como:

* **Tempo de resposta:** tempo necessário para o agente responder;
* **Taxa de erros:** quantidade de respostas que apresentaram falhas;
* **Consumo de tokens:** quantidade de tokens utilizados nas interações;
* **Custo por interação:** custo estimado para processar cada consulta;
* **Taxa de respostas sem informação:** frequência com que o agente informa que não possui dados suficientes.

Essas métricas podem auxiliar na identificação de problemas de desempenho e na evolução contínua do agente.
