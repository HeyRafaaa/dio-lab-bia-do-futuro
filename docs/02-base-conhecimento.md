# Base de Conhecimento

## Dados Utilizados

A base de conhecimento do RAMI utiliza dados financeiros necessários para analisar a situação do usuário, acompanhar seus gastos e auxiliar no planejamento financeiro.

| Arquivo                   | Formato | Utilização no RAMI                                                                                    |
| ------------------------- | ------- | ----------------------------------------------------------------------------------------------------- |
| `perfil_financeiro.json`  | JSON    | Armazenar renda, frequência de recebimento, despesas, objetivos e informações financeiras do usuário. |
| `transacoes.csv`          | CSV     | Registrar e analisar entradas e saídas de dinheiro, identificando padrões de gastos.                  |
| `contas_futuras.csv`      | CSV     | Controlar contas, parcelas e compromissos que ainda precisam ser pagos.                               |
| `orcamento.json`          | JSON    | Definir limites de gastos por categoria e acompanhar o consumo do orçamento.                          |
| `reserva_emergencia.json` | JSON    | Acompanhar depósitos, retiradas, saldo, rendimento e progresso da reserva de emergência.              |

### Relação entre os dados

Os dados são utilizados em conjunto para determinar quanto dinheiro o usuário realmente possui para gastar.

O RAMI não considera apenas o saldo atual. Ele cruza as informações de:

**Saldo atual + transações + contas futuras + despesas previstas + orçamento + valores reservados**

para calcular o **dinheiro realmente disponível**.

---

## Adaptações nos Dados

Os dados foram estruturados para representar uma situação financeira realista e permitir que o RAMI faça análises personalizadas.

Foram considerados:

* Diferentes fontes e frequências de renda.
* Contas fixas e variáveis.
* Parcelas e dívidas.
* Gastos do dia a dia.
* Limites de orçamento por categoria.
* Despesas futuras.
* Valores destinados à reserva de emergência.
* Metas financeiras.
* Histórico de transações.

Os dados podem ser atualizados conforme o usuário registra novas receitas, despesas, contas ou depósitos na reserva.

O objetivo é permitir que o RAMI acompanhe a evolução financeira do usuário ao longo do tempo, em vez de analisar apenas uma situação isolada.

---

## Estratégia de Integração

### Como os dados são carregados?

Os arquivos de dados são carregados pela aplicação e disponibilizados ao RAMI conforme a necessidade da interação.

Os dados financeiros do usuário são organizados por categorias, como:

* Perfil financeiro
* Transações
* Contas futuras
* Orçamento
* Reserva de emergência
* Objetivos financeiros

Quando o usuário realiza uma consulta, o sistema recupera os dados necessários para aquela análise.

Por exemplo, para responder:

> "Posso gastar R$ 200 hoje?"

o sistema deve consultar principalmente:

* Saldo atual
* Contas futuras
* Despesas essenciais previstas
* Gastos realizados
* Orçamento
* Valores reservados

---

### Como os dados são usados no prompt?

Os dados financeiros não devem ser inseridos permanentemente no **System Prompt**.

O System Prompt contém as regras de comportamento do RAMI, enquanto os dados do usuário são fornecidos dinamicamente conforme cada interação.

Dessa forma:

**System Prompt**
→ Define as regras, prioridades, personalidade e limitações do RAMI.

**Dados do usuário**
→ Fornecem a situação financeira atual.

**Motor de cálculo**
→ Realiza os cálculos necessários.

**RAMI**
→ Interpreta os resultados e apresenta uma orientação clara ao usuário.

Essa separação reduz o risco de o agente inventar informações e permite que os dados sejam atualizados sem alterar o prompt principal.

---

## Exemplo de Contexto Montado

Antes de responder a uma solicitação, o sistema pode montar um contexto como:

```text
DADOS FINANCEIROS DO USUÁRIO

Perfil:
- Renda mensal: R$ 3.500,00
- Próximo recebimento: 05/09
- Objetivo: Construir reserva de emergência

Saldo atual:
- R$ 1.800,00

Contas futuras:
- Aluguel: R$ 1.000,00
- Energia: R$ 180,00
- Internet: R$ 100,00
- Parcela: R$ 300,00

Despesas essenciais previstas:
- Alimentação: R$ 300,00
- Transporte: R$ 150,00

Gastos realizados no mês:
- Alimentação: R$ 450,00
- Lazer: R$ 180,00
- Compras: R$ 100,00

Orçamento:
- Alimentação: R$ 600,00
- Lazer: R$ 250,00
- Compras: R$ 150,00

Reserva de emergência:
- Total depositado: R$ 500,00
- Rendimento: R$ 4,20
- Total atual: R$ 504,20
- Meta atual: R$ 1.000,00
```

### Exemplo de análise

```text
Saldo atual: R$ 1.800,00

Contas futuras:
R$ 1.580,00

Despesas essenciais previstas:
R$ 450,00

Dinheiro realmente disponível:
R$ -230,00

Situação: 🔴 CRÍTICO

O usuário possui R$ 1.800,00 na conta, mas os compromissos e despesas previstas ultrapassam esse valor.

O RAMI deve alertar o usuário e priorizar as despesas essenciais antes de recomendar novos gastos.
```

> **Importante:** o RAMI deve utilizar somente os dados disponíveis e nunca preencher informações ausentes com valores inventados. Quando os dados forem insuficientes ou contraditórios, deve solicitar confirmação ao usuário.
