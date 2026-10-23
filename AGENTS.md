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

## Como pedir uma análise

Todo pedido tem cinco partes. Se faltar alguma, pergunte antes de começar.

```
Pergunta:      a pergunta de negócio, com data/período explícito
Arquivos:      quais arquivos de dados/brutos/ usar (dicionário em docs/)
Regras:        filtros obrigatórios, o que não pode ser alterado
Saída:         o que entregar (número, tabela de filtros, código em notebooks/)
Pronto quando: o critério de conferência (ex.: soma por plano e canal bate com o total)
```

**Antes de rodar, mostre o plano e espere a aprovação.**

Ao entregar, confira antes de afirmar:
- O número bate com a referência do enunciado ou do dicionário, quando houver?
- Qual armadilha conhecida poderia distorcer o resultado, e ela foi tratada?
- Três registros do resultado conferidos à mão, de preferência contra uma fonte independente.
- Tabela de filtros com as linhas restantes após cada passo.

Exemplo (`notebooks/01_pagantes_ativos.ipynb`):

```
Pergunta: quantos assinantes pagantes ativos a Vitaliza tinha no corte, 30/09/2026?
Arquivos: dados/brutos/assinaturas.csv e dados/brutos/usuarios.csv, com o dicionário em docs/.
Regras: contas de teste (e-mail @vitaliza.com.br) não contam; mostre as linhas depois de cada
filtro; não altere nada em dados/brutos/.
Saída: o número, a tabela de filtros e o código em notebooks/.
Pronto quando: a soma por plano e por canal bate com o total.
```

## Ambiente

`python3 -m venv .venv && .venv/bin/pip install -r requirements.txt`. Notebooks leem de `../dados/brutos/`.

## Fluxo no Git

A `main` é protegida: nada de commit direto. Toda mudança vai numa branch e entra por pull request com 1 aprovação.

O repositório é **público** (a proteção da `main` só funciona em repositório público no plano gratuito). Por isso, notebooks sobem **sem saídas**: antes de cada commit, rode `.venv/bin/jupyter nbconvert --clear-output --inplace notebooks/*.ipynb` e confira que nenhuma linha de `dados/` aparece no diff.

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
- **Contas de teste** (e-mail `@vitaliza.com.br` em `usuarios.csv`) nunca contam: 14.813 ativas − 60 de teste = 14.753 pagantes. Normalizar o e-mail (`strip().lower()`) antes de testar o domínio — há 959 e-mails com maiúsculas ou espaços. Hoje as 60 coincidem com `plano_atual == 'cortesia'`, mas o critério é o e-mail.
- `eventos_assinatura.csv` também mistura fusos: lojas em UTC (`Z`), site em horário de Brasília.
- Dados com data só podem ser usados até o corte da análise (30/09/2026) — risco de vazamento no modelo.
- Heatmaps só existem para quem era pagante na data e treinou ao ar livre; ausência de imagem é informação, não dado faltante.

## Premissas de negócio (enunciado, seção 03)

Custo de servir R$ 4,20/mês; CAC R$ 118; CRM: WhatsApp R$ 0,40 (teto 1.500/mês), CS R$ 18 (teto 300/mês), e-mail R$ 0,01, push grátis (1/semana); orçamento CRM R$ 40.000/mês incluindo descontos e custo de IA generativa.
