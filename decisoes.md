# Registro de decisões

Cada decisão de tratamento de dados ou premissa de cálculo entra aqui: data, decisão, justificativa, impacto.

---

## 2026-10-22 — Cálculo de faturamento mensal

**Decisão:** faturamento do mês segue quatro etapas, nesta ordem:

| Etapa | Regra | Set/2026 |
|---|---|---|
| 0. Soma ingênua | Todos os status | R$ 509.588 |
| 1. Só aprovados | Excluir `recusado`, `estornado`, `chargeback` | R$ 499.503 |
| 2. Fuso | Converter UTC → Brasília (UTC−3) antes de atribuir o mês | R$ 499.402 |
| 3. Duplicatas | Remover 2ª ocorrência de mesmo `user_id` + `data_hora` + `valor` aprovados (93 pares) | **R$ 492.572 (bruto)** |
| 4. Taxas de canal | App Store/Google Play 15%, cartão 3,5%, Pix 0,99% | **R$ 436.442 (líquido)** |

**Justificativa:** o faturamento é apurado no fuso da empresa; duplicatas com horário idêntico são falha de cobrança, não receita; líquido reflete o que efetivamente entra no caixa.

**Pendências:**
- As taxas foram reconstruídas para bater com a resposta de referência. Confirmar com a tabela oficial do enunciado.
- Estornos/chargebacks lançados no mês (set/26: −R$ 3.058,20) são excluídos, mas não descontados. Definir se a visão é caixa ou competência.

## 2026-10-22 — Tamanho da base

**Decisão:** base ativa = `status_atual == 'ativa'` em `assinaturas.csv` → 14.813 assinantes (de 32.643 históricos).

**Justificativa:** bate com a estimativa independente via pagamentos (mensal pago ≤31 dias + anual pago ≤365 dias = 14.846).
