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

**Decisão (revisada):** base pagante ativa = `status_atual == 'ativa'` em `assinaturas.csv`, excluindo contas de teste (e-mail `@vitaliza.com.br` em `usuarios.csv`, normalizado) → **14.753** (14.813 − 60). Código: `notebooks/01_pagantes_ativos.ipynb`.

**Justificativa:** bate exatamente com o enunciado (14.753; 57% anual / 43% mensal; App Store 36,6%, Google Play 33,6%, cartão 20,3%, Pix 9,5%). A primeira versão filtrava `plano_atual == 'cortesia'`; dá o mesmo resultado porque as 60 contas de teste são as 60 cortesias, mas o critério de negócio é a conta de teste, e o filtro por plano quebraria se surgisse uma cortesia real.

**Conferência manual:** 3 contas sorteadas (seed 42) têm cobrança aprovada recente em `pagamentos.csv`; a conta de teste conferida não tem nenhuma.

**Observação:** a conta de teste u_a044e148 tem assinatura iniciada em 2025-01-10, antes do cadastro (2025-06-04) — datas inconsistentes nas contas internas.

**Limite:** `assinaturas.csv` é retrato de 01/10/2026. Para ativos em datas anteriores (ex.: início de cada mês, para churn), reconstruir a partir de `eventos_assinatura.csv`.

## 2026-10-22 — Heatmaps

**Decisão:** zips extraídos em `dados/brutos/heatmaps_90d/{2026-07-31,2026-09-30}/` e zips removidos; pasta renomeada de `heatmaps/` para `heatmaps_90d/` para seguir o dicionário.

**Verificação:** 12.426 e 13.047 PNGs, iguais ao dicionário. Metadados `__MACOSX` da extração descartados.
