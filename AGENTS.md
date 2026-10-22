# Vitaliza — Grupo 01

Case do Módulo 2 (Inteli). Análise de assinaturas e pagamentos da Vitaliza.

## Estrutura

| Pasta | Conteúdo | Regra |
|---|---|---|
| `docs/` | Enunciado e dicionário de dados | Consultar antes de qualquer análise |
| `dados/brutos/` | Os 12 arquivos originais e `heatmaps_90d/` | **Só leitura. Nunca editar, sobrescrever ou apagar.** |
| `dados/processados/` | Tabelas intermediárias do grupo | Sempre geradas por código em `src/` ou `notebooks/` |
| `notebooks/` | Exploração e análises | |
| `src/` | Código reutilizável (limpeza, métricas) | |
| `saidas/` | Gráficos, tabelas finais, apresentações | |

## Regras de trabalho

- O bruto nunca é editado. Toda limpeza gera um arquivo novo em `dados/processados/`, a partir de código versionado.
- Toda decisão de tratamento de dados (filtro, exclusão, premissa) é registrada em `decisoes.md` com data e justificativa.
- Ler CSVs com parser de verdade (pandas/csv), nunca `awk -F,` — há campos com vírgula entre aspas.
- Números entregues sempre com a ponte do valor bruto até o final, etapa por etapa.

## Armadilhas conhecidas em `pagamentos.csv`

1. `status` tem `aprovado`, `recusado`, `estornado`, `chargeback` — faturamento usa só `aprovado`.
2. `data_hora` mistura UTC (`...Z`) e horário local sem fuso. Converter tudo para Brasília (UTC−3) antes de agrupar por mês.
3. `valor` mistura `34.90` e `"R$ 34,90"`.
4. Há cobranças duplicadas: mesmo `user_id` + `data_hora` + `valor`, ambas aprovadas. Manter uma.
5. Líquido = bruto − taxas de canal (lojas, cartão, Pix). Ver `decisoes.md`.
