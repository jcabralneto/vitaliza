# Entrega de John — preparação dos dados e diagnóstico

1. **Leitura rápida:** `sintese_para_relatorio.md` — seção pronta para revisão e integração ao relatório coletivo.
2. **Método e tabelas:** `diagnostico.md` — definições, denominadores, gráficos e limites.
3. **Variáveis:** `dicionario_base_analitica.md` e CSV equivalente.
4. **Números de apoio:** CSVs agregados e quatro gráficos SVG.
5. **Revisão:** `revisao_qualidade_entropia.md`, após validação.
6. **PDF de leitura:** `John_Preparacao_Diagnostico_S5.pdf` — seis páginas para leitura e discussão.

## O que cada frente recebe

| Pessoa | Material | Uso |
|---|---|---|
| Leonardo | Base de clusterização e dicionário | Selecionar e padronizar variáveis, tratar ausências, construir e validar os grupos |
| Claudinne | Filtros, alertas de qualidade, auditoria local e decisões | Explicar tratamentos e conferir limitações sem refazer toda a exploração |
| Kiril | Diagnóstico e, depois, tabela dos clusters de Leonardo | Construir personas ancoradas em evidências |
| Marcela | Base de contexto e tabelas por plano/canal | Complementar valor e priorização; aproximação mensal não é LTV nem retorno de contato |
| John | Síntese, diagnóstico e código reproduzível | Defender as definições e integrar a seção às demais contribuições |

## Bases individuais locais

Em `dados/processados/s5_john/`:

- `base_clusterizacao.csv`: 14.753 linhas, `user_id` e 17 variáveis candidatas; há ausências intencionais.
- `base_assinantes_corte.csv`: contexto, fontes separadas e alertas.
- `painel_churn_mensal.parquet`: 260.328 observações usuário-mês para diagnóstico histórico.
- `completude_por_coluna.csv`, `auditoria_qualidade.csv`, `manifesto_validacao.json` e conferências por amostra.

Esses arquivos não sobem ao Git. Para transferir ao grupo, usar o canal privado já adotado para os dados do case. Nenhum envio externo foi realizado nesta preparação.

## Reprodução

Na raiz do repositório:

```sh
.venv/bin/python src/preparar_diagnostico_s5.py
.venv/bin/python -m unittest discover -s tests -v
```

Para exportar o PDF, usar um ambiente com `requirements-relatorio.txt` instalado e executar `python src/exportar_relatorio_s5_pdf.py`. Depois, `.venv/bin/python src/validar_entrega_s5.py` confere os arquivos, executa os testes e registra a revisão editorial. A exportação desta entrega foi feita com o ambiente de documentos disponível no Codex, sem alterar o ambiente de dados existente.

Os documentos gerados preservam o corte e as definições do case. Não editar os CSVs manualmente para mudar resultados; corrigir a regra em código, registrar a decisão e reproduzir.
