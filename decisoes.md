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

**Taxas confirmadas** no enunciado, seção 03 (verificado em 2026-10-22).

**Pendência:**
- Estornos/chargebacks lançados no mês (set/26: −R$ 3.058,20) são excluídos, mas não descontados. Definir se a visão é caixa ou competência.

## 2026-10-22 — Tamanho da base

**Decisão:** base pagante ativa = `status_atual == 'ativa'` e `plano_atual != 'cortesia'` em `assinaturas.csv` → **14.753** (14.813 ativas − 60 cortesias).

**Justificativa:** bate exatamente com o enunciado (14.753; 57% anual / 43% mensal; App Store 36,6%, Google Play 33,6%, cartão 20,3%, Pix 9,5%). Cortesia não paga e não entra na base pagante.

**Limite:** `assinaturas.csv` é retrato de 01/10/2026. Para ativos em datas anteriores (ex.: início de cada mês, para churn), reconstruir a partir de `eventos_assinatura.csv`.

## 2026-10-22 — Heatmaps

**Decisão:** zips extraídos em `dados/brutos/heatmaps_90d/{2026-07-31,2026-09-30}/` e zips removidos; pasta renomeada de `heatmaps/` para `heatmaps_90d/` para seguir o dicionário.

**Verificação:** 12.426 e 13.047 PNGs, iguais ao dicionário. Metadados `__MACOSX` da extração descartados.
