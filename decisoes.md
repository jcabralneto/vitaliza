# Registro de decisões

Todo problema de qualidade ou regra de cálculo entra na tabela: uma linha por decisão. A coluna **Dimensão** usa as cinco dimensões do `AGENTS.md` (Completude, Validade, Consistência, Unicidade, Temporalidade) ou **Regra** para regras de negócio. Quando a decisão precisar de explicação, detalhe na seção abaixo da tabela.

| Data | Arquivo | Dimensão | Problema | Decisão | Critério | Linhas afetadas | Quem |
|---|---|---|---|---|---|---|---|
| 2026-10-22 | `pagamentos.csv` | Validade | `valor` em dois formatos: `34.90` e `"R$ 34,90"` | Converter para número | Remover `R$ `, trocar vírgula por ponto | 19.750 | Leo + Claude |
| 2026-10-22 | `pagamentos.csv` | Temporalidade | `data_hora` mistura UTC (lojas) e horário de Brasília (site) | Converter tudo para Brasília antes de agrupar por mês | Sufixo `Z` = UTC → −3h; sem sufixo = já em Brasília | 112.126 em UTC; 53.422 em Brasília | Leo + Claude |
| 2026-10-22 | `pagamentos.csv` | Unicidade | Cobranças aprovadas duplicadas | Manter uma | Mesmo `user_id` + `data_hora` exata + `valor`, ambas `aprovado` | 1.941 na base (93 em set/26) | Leo + Claude |
| 2026-10-22 | `pagamentos.csv` | Regra | Faturamento somava todos os status | Faturamento usa só `aprovado`; líquido desconta taxas de canal | Ver [Faturamento mensal](#faturamento-mensal) | — | Leo + Claude |
| 2026-10-22 | `pagamentos.csv` | Consistência | Estorno `p_0160370` de R$ 299,90 sobre cobrança de R$ 239,90 | Marcar; não corrigir | Estorno maior que a cobrança original | 1 | Leo + Claude |
| 2026-10-22 | `assinaturas.csv` × `pagamentos.csv` | Consistência | 292 chargebacks em assinaturas × 296 em pagamentos | **Pendente:** investigar | — | 4 | — |
| 2026-10-22 | `usuarios.csv` | Validade | E-mails com maiúsculas ou espaços | Normalizar com `strip().lower()` antes de comparar | E-mail ≠ e-mail normalizado | 959 | Leo + Claude |
| 2026-10-22 | `usuarios.csv` × `assinaturas.csv` | Validade | Contas de teste; `plano_atual = cortesia` e `canal_cobranca = interno` não existem no dicionário | Excluir de toda contagem de assinantes | E-mail `@vitaliza.com.br` | 60 | Leo + Claude |
| 2026-10-22 | `assinaturas.csv` × `usuarios.csv` | Consistência | Assinatura com `inicio` anterior a `data_cadastro` | Marcar; **pendente:** entender a origem | `inicio < data(data_cadastro)` | 42 | Leo + Claude |
| 2026-10-22 | `onboarding.csv` | Completude | `objetivo_texto` e `como_conheceu` vazios | Manter nulo: o dicionário marca como opcionais | Nulo | 5.467 (8,6%) e 4.586 (7,2%) | Leo + Claude |
| 2026-10-22 | `onboarding.csv` | Completude | Respostas preenchidas sem conteúdo (`nada`, `😂`, `.`, `x`, `sla`, `kkkk`, `asdf`, `ok`, `-`, `nao sei`) | Marcar como **sem conteúdo**, separado de nulo; não apagar | Texto normalizado na lista | 13.768 em `objetivo_texto`; 11.515 em `como_conheceu` | Leo + Claude |
| 2026-10-22 | `onboarding.csv` | Completude | `nivel` e `dias_por_semana` vazios, sem o dicionário dizer que são opcionais | Marcar como "não informado"; não imputar | Nulo | 4.513 (7,1%) e 6.368 (10,0%) | Leo + Claude |
| 2026-10-22 | `onboarding.csv` | Validade | `dias_por_semana` em texto livre: `3`, `3x`, `3 vezes` | **Pendente:** extrair o número | Valor não numérico | 24.034 | — |
| 2026-10-22 | `heatmaps_90d/` | — | Imagens entregues em zip | Extrair em `2026-07-31/` e `2026-09-30/`; remover zips e `__MACOSX` | Contagem igual ao dicionário | 12.426 + 13.047 imagens | Leo + Claude |

---

## Detalhes

### Faturamento mensal

O faturamento do mês segue quatro etapas, nesta ordem:

| Etapa | Regra | Set/2026 |
|---|---|---|
| 0. Soma ingênua | Todos os status | R$ 509.588 |
| 1. Só aprovados | Excluir `recusado`, `estornado`, `chargeback` | R$ 499.503 |
| 2. Fuso | Converter UTC → Brasília (UTC−3) antes de atribuir o mês | R$ 499.402 |
| 3. Duplicatas | Remover 2ª ocorrência de mesmo `user_id` + `data_hora` + `valor` aprovados (93 pares) | **R$ 492.572 (bruto)** |
| 4. Taxas de canal | App Store/Google Play 15%, cartão 3,5%, Pix 0,99% (enunciado, seção 03) | **R$ 436.442 (líquido)** |

O faturamento é apurado no fuso da empresa; duplicatas com horário idêntico são falha de cobrança, não receita; líquido reflete o que efetivamente entra no caixa.

**Pendência:** estornos e chargebacks lançados no mês (set/26: −R$ 3.058,20) são excluídos, mas não descontados. Definir se a visão é caixa ou competência.

### Base pagante ativa

Base pagante ativa = `status_atual == 'ativa'` em `assinaturas.csv`, excluindo contas de teste → **14.753** (14.813 − 60). Código: `notebooks/01_pagantes_ativos.ipynb`.

Bate exatamente com o enunciado (14.753; 57% anual / 43% mensal; App Store 36,6%, Google Play 33,6%, cartão 20,3%, Pix 9,5%). A primeira versão filtrava `plano_atual == 'cortesia'`; dá o mesmo resultado porque as 60 contas de teste são as 60 cortesias, mas o critério de negócio é a conta de teste.

Conferência manual: 3 contas sorteadas (seed 42) têm cobrança aprovada recente em `pagamentos.csv`; a conta de teste conferida não tem nenhuma.

**Limite:** `assinaturas.csv` é retrato de 01/10/2026. Para ativos em datas anteriores (ex.: início de cada mês, para churn), reconstruir a partir de `eventos_assinatura.csv`.

### Completude do onboarding

Código: `notebooks/02_qualidade_onboarding.ipynb`. Somando nulos e respostas sem conteúdo, `objetivo_texto` fica vazio na prática em cerca de 30% das contas, não 8,6%. Para a extração com IA (objetivo 5 do case), essas respostas não devem ir ao modelo: custam e não informam. A lista de respostas sem conteúdo foi montada a partir das respostas curtas mais repetidas e pode crescer.
