# Vitaliza — Grupo 01

Case do Módulo 2 (Inteli). Análise de assinaturas e pagamentos da Vitaliza.

## Estrutura

| Pasta | Conteúdo | Regra |
|---|---|---|
| `docs/` | Enunciado e dicionário de dados: PDFs oficiais e versões `.md` (`enunciado.md`, `dicionario_dados.md`) | Ler os `.md` antes de qualquer análise; em caso de dúvida, o PDF prevalece |
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
5. Líquido = bruto − taxas de canal: lojas 15%, cartão 3,5%, Pix 0,99% (enunciado, seção 03).

## Outras armadilhas

- `assinaturas.csv` é um retrato de 01/10/2026, não histórico. Para a situação numa data passada, usar `eventos_assinatura.csv` (desde 01/07/2024).
- Assinante **pagante** ativo exclui `plano_atual == 'cortesia'`: 14.813 ativas − 60 cortesias = 14.753.
- `eventos_assinatura.csv` também mistura fusos: lojas em UTC (`Z`), site em horário de Brasília.
- Dados com data só podem ser usados até o corte da análise (30/09/2026) — risco de vazamento no modelo.
- Heatmaps só existem para quem era pagante na data e treinou ao ar livre; ausência de imagem é informação, não dado faltante.

## Premissas de negócio (enunciado, seção 03)

Custo de servir R$ 4,20/mês; CAC R$ 118; CRM: WhatsApp R$ 0,40 (teto 1.500/mês), CS R$ 18 (teto 300/mês), e-mail R$ 0,01, push grátis (1/semana); orçamento CRM R$ 40.000/mês incluindo descontos e custo de IA generativa.
