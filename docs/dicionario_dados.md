# Vitaliza: dicionário de dados

> Transcrição em Markdown de `docs/Vitaliza - Dicionário de dados.pdf` (MBA em IA e Dados para Negócios · Inteli · Business Case Módulo 2), gerada em 2026-10-22 para leitura rápida por agentes.
> **O PDF é a fonte oficial.** Se ele for atualizado, gere este arquivo de novo.

## 01 Sobre este documento

Este documento descreve os arquivos do data room da Vitaliza: de onde vem cada um, o que cada linha representa e o que significa cada coluna. É a referência para o trabalho com os dados. O contexto do negócio e os objetivos do case estão no documento *Vitaliza: enunciado do case*.

O time de dados da Vitaliza exportou os arquivos em 01/10/2026, com dados até a data de corte, 30/09/2026. Cada arquivo sai do sistema que o produz (o app, as lojas, o meio de pagamento do site, o BI, a rede social, o suporte e o CRM) e chega como esse sistema grava. Formatos de data, fusos horários, maiúsculas e nomes de categoria podem variar entre arquivos. Ninguém limpou os dados antes da entrega: conferir a qualidade de cada arquivo faz parte do trabalho.

Os arquivos estão organizados nas três formas de dado do módulo. **Tabelas** já chegam em linhas e colunas, uma linha por coisa (conta, assinatura, relação), e podem ir direto para a análise. **Logs de eventos** registram acontecimentos com data e hora, uma linha por acontecimento, e precisam ser contados ou medidos para virar tabela. **Texto e imagem** são conteúdo livre e precisam ser transformados em variável antes de entrar num modelo.

Cada seção a seguir trata de um arquivo: primeiro de onde ele vem e para que serve, depois as colunas. Nos quadros, os nomes de coluna e os valores aparecem exatamente como estão no arquivo. O `user_id` identifica a conta e liga todos os arquivos.

### Visão geral

| Forma | Arquivo | Uma linha por | Linhas | Seção |
|---|---|---|---|---|
| Tabela | `usuarios.csv` | conta | 64.948 | 02 |
| Tabela | `assinaturas.csv` | assinatura | 32.643 | 03 |
| Tabela | `amizades.csv` | relação de seguir | 113.480 | 04 |
| Tabela | `campanha_ago26.csv` | assinante sorteado | 14.120 | 05 |
| Log de eventos | `eventos_assinatura.csv` | evento | 275.565 | 06 |
| Log de eventos | `pagamentos.csv` | cobrança | 165.548 | 07 |
| Log de eventos | `uso_mensal.csv` | usuário e mês | 591.662 | 08 |
| Log de eventos | `atividades.parquet` | treino | 1.254.475 | 09 |
| Texto e imagem | `onboarding.csv` | conta | 63.929 | 10 |
| Texto e imagem | `pesquisa_saida.csv` | resposta | 643 | 11 |
| Texto e imagem | `feed_posts.csv` | post | 119.309 | 12 |
| Texto e imagem | `tickets_suporte.csv` | chamado | 4.422 | 13 |
| Texto e imagem | `heatmaps_90d/` | imagem | 12.426 + 13.047 | 14 |

## 02 Cadastro de contas

`usuarios.csv` · Tabela · uma linha por conta · 64.948 linhas

Toda pessoa que baixa o app e cria uma conta ganha uma linha neste arquivo, pague ou não. São todas as contas desde o lançamento, em setembro de 2020, e a maior parte delas usa só a versão grátis. Na criação da conta, a pessoa informa e-mail, data de nascimento, sexo, cidade, estado e CEP. O app completa o cadastro com o sistema do celular, a última versão do app vista e o relógio conectado, quando há um, e o marketing atribui o canal pelo qual a pessoa chegou.

Os campos informados pela pessoa são digitados por ela e não passam por validação. Este é o arquivo que liga todos os outros: para saber quem é quem em qualquer arquivo do data room, o caminho passa por aqui.

| Coluna | Descrição |
|---|---|
| `user_id` | identificador da conta |
| `email` | e-mail de cadastro |
| `data_cadastro` | data e hora do cadastro |
| `data_nascimento` | informada pelo usuário |
| `sexo` | informado pelo usuário |
| `cidade`, `uf` | informados pelo usuário, texto livre |
| `cep_prefixo` | 3 primeiros dígitos do CEP |
| `canal_aquisicao` | canal atribuído pelo marketing no cadastro |
| `sistema` | sistema do celular |
| `versao_app` | última versão do app vista |
| `relogio_conectado` | relógio conectado à conta, se houver |

## 03 Assinaturas

`assinaturas.csv` · Tabela · uma linha por assinatura · 32.643 linhas · retrato de 01/10/2026

Cada vez que uma conta passa a pagar, nasce uma assinatura. A mesma pessoa pode ter mais de uma ao longo do tempo: assina, sai e volta meses depois. O arquivo traz as 32.643 assinaturas criadas desde 2020, com plano, canal de cobrança, data da primeira cobrança e, para as que terminaram, quando e por quê.

O sistema de assinaturas guarda só a situação atual de cada assinatura: a cada mudança, o campo é sobrescrito. Por isso este arquivo é um retrato do dia da exportação, 01/10/2026, e não um histórico. Ele diz como cada assinatura estava em 01/10/2026, não como estava em qualquer data anterior. Para reconstruir a situação de um assinante numa data do passado, a fonte é `eventos_assinatura.csv` (seção 06).

| Coluna | Descrição |
|---|---|
| `assinatura_id` | identificador |
| `user_id` | conta |
| `plano_atual` | `mensal` ou `anual` |
| `canal_cobranca` | `app_store`, `google_play`, `web_cartao` ou `web_pix` |
| `inicio` | data da primeira cobrança |
| `status_atual` | situação em 01/10/2026 |
| `renovacao_automatica` | situação em 01/10/2026 |
| `data_fim` | quando a assinatura terminou, se terminou |
| `motivo_fim` | motivo registrado no fim, se houver |

## 04 Rede de seguidores

`amizades.csv` · Tabela · uma relação de seguir por linha · 113.480 linhas

A rede social da Vitaliza funciona por seguidores. Seguir alguém é uma decisão de mão única: se Ana segue Bruno e Bruno segue Ana, são duas linhas. Quem segue alguém passa a ver os treinos e os posts dessa pessoa no feed. O arquivo guarda todas as relações de seguir, com a data em que cada uma começou.

A rede é uma das três partes do produto e o que diferencia a Vitaliza de um app de treino individual. O arquivo permite estudar quem está conectado a quem: quantos seguidores cada pessoa tem, quem ela segue e quando essas conexões se formaram. Seguir e treinar junto são coisas diferentes: a companhia num treino específico fica registrada em `atividades.parquet` (seção 09).

| Coluna | Descrição |
|---|---|
| `seguidor_id` | quem segue |
| `seguido_id` | quem é seguido |
| `desde` | data em que passou a seguir |

## 05 Campanha de agosto de 2026

`campanha_ago26.csv` · Tabela · uma linha por assinante · 14.120 linhas

Em 10/08/2026, o CRM fez a primeira campanha de retenção da Vitaliza para toda a base pagante. Os 14.120 assinantes pagantes daquele dia foram sorteados em quatro grupos de tamanho parecido. Três grupos receberam, por push e e-mail, mensagens diferentes: desafio ("Novo desafio de 6 semanas montado para você"), cupom ("Oferta para voltar a treinar") e conteúdo ("Seu plano de treino personalizado está pronto"). O grupo de controle foi sorteado para não receber nada. O arquivo registra o grupo de cada assinante, a mensagem e a oferta enviadas e se a pessoa abriu e clicou.

É o único experimento controlado da base. Como os grupos foram sorteados, têm em média o mesmo perfil, e a diferença de saída entre um grupo que recebeu mensagem e o controle pode ser atribuída à mensagem. A empresa nunca analisou o resultado. Abertura e clique medem a atenção à mensagem; se a pessoa continuou assinante, só os eventos de assinatura dizem.

| Coluna | Descrição |
|---|---|
| `user_id` | conta |
| `grupo` | `controle` (sorteado para não receber), `desafio`, `cupom` ou `conteudo` |
| `enviado_em` | envio |
| `canal` | `push+email` |
| `titulo_mensagem` | título da mensagem enviada |
| `oferta` | oferta do grupo cupom: `30pct_3_meses` (mensal) ou `1_mes_gratis` (anual) |
| `abriu_push`, `abriu_email`, `clicou` | engajamento com a mensagem |

## 06 Eventos de assinatura

`eventos_assinatura.csv` · Log de eventos · um evento por linha · 275.565 linhas

Este é o histórico da vida de cada assinatura, um acontecimento por linha: início e fim do período de teste, início da assinatura, cada renovação, o desligamento e o religamento da renovação automática, o período de carência depois de uma cobrança recusada, a expiração, o cancelamento pelo site, o reembolso e o chargeback. Para quem paga pela App Store ou pelo Google Play, os eventos chegam por notificações que o servidor da loja envia à Vitaliza. Para quem paga pelo site, o próprio sistema da Vitaliza registra.

É a fonte para saber como cada assinante estava em qualquer data desde 01/07/2024: se estava em teste, pagando, com a renovação ligada ou desligada. É também onde aparece o cancelamento de quem paga pela loja, que a Vitaliza só conhece por estes avisos. Como os eventos vêm de sistemas diferentes, o horário de cada linha segue o sistema de origem.

| Coluna | Descrição |
|---|---|
| `user_id` | conta |
| `data_hora` | quando o evento foi recebido. As lojas mandam em UTC (terminado em "Z"); o site grava em horário de Brasília |
| `evento` | `trial_iniciado`, `trial_expirado`, `assinatura_iniciada`, `renovacao`, `renovacao_automatica_desligada`, `renovacao_automatica_religada`, `periodo_carencia`, `assinatura_expirada`, `cancelamento_web`, `reembolso`, `chargeback` |
| `plano` | plano no momento do evento |
| `canal_cobranca` | canal de cobrança |
| `detalhe` | informação adicional (nem sempre preenchida) |

*O histórico de eventos começa em 01/07/2024. Assinaturas mais antigas aparecem em `assinaturas.csv` com início anterior.*

## 07 Pagamentos

`pagamentos.csv` · Log de eventos · uma cobrança por linha · 165.548 linhas

Cada tentativa de cobrança vira uma linha. Para quem assina pela loja, a cobrança é feita pela Apple ou pelo Google, que repassam o valor à Vitaliza. Para quem assina pelo site, a Vitaliza cobra no cartão ou pelo Pix Automático. Quando uma cobrança é recusada, por cartão vencido ou sem limite, o sistema tenta de novo nos dias seguintes; cada tentativa é uma linha, com o número da tentativa. Um chargeback é a contestação da cobrança pelo cliente junto ao banco.

O arquivo mostra o dinheiro: quanto cada assinante pagou, quando e por qual meio, incluindo a mudança de preço do mensal em 01/03/2026 e os valores com cupom. Junto com os eventos de assinatura, permite distinguir quem saiu porque decidiu sair de quem saiu porque a cobrança falhou.

| Coluna | Descrição |
|---|---|
| `pagamento_id` | identificador |
| `user_id` | conta |
| `data_hora` | quando a cobrança foi processada |
| `valor` | valor cobrado em R$ |
| `metodo` | `app_store`, `google_play`, `cartao` ou `pix_automatico` |
| `status` | `aprovado`, `recusado`, `estornado` ou `chargeback` |
| `tentativa` | número da tentativa de cobrança |

## 08 Uso mensal

`uso_mensal.csv` · Log de eventos · uma linha por usuário e mês · 591.662 linhas

Esta é a tabela que a Vitaliza usa nos painéis de engajamento. Todo mês, o BI consolida, para cada usuário, quantos treinos foram registrados, de que tipo, quantos minutos somaram, em quantos dias a pessoa treinou e quantas vezes abriu o app. Cobre de janeiro de 2025 a setembro de 2026.

É a forma mais rápida de olhar o uso ao longo do tempo e também a mais resumida: o mês esconde o que aconteceu dentro dele, como uma semana parada ou um treino mais longo. Para o detalhe de cada treino em 2026, a fonte é `atividades.parquet` (seção 09).

| Coluna | Descrição |
|---|---|
| `user_id` | conta |
| `mes` | AAAA-MM |
| `atividades` | treinos registrados no mês |
| `atividades_ar_livre` | corrida, caminhada e pedal |
| `atividades_video` | treinos guiados em vídeo |
| `minutos` | minutos de treino |
| `dias_ativos` | dias com pelo menos um treino |
| `sessoes_app` | aberturas do app no mês |

## 09 Treinos

`atividades.parquet` · Log de eventos · um treino por linha · 1.254.475 linhas · 01/01 a 30/09/2026

Cada treino registrado em 2026 é uma linha, com início, tipo, duração e, quando há GPS, distância e ritmo. Os treinos chegam por três caminhos: registrados no próprio app, com o GPS do celular ou nos vídeos guiados, ou sincronizados de um relógio Garmin ou do Apple Health. Com relógio, vem também a frequência cardíaca média. Ao registrar um treino, a pessoa pode marcar outra conta como companhia.

É o registro mais detalhado do comportamento de cada assinante: quando treina, quanto, de que jeito e com quem. Por causa do tamanho, o arquivo está em formato parquet, que não abre no Excel. Leia com pandas, polars ou DuckDB.

| Coluna | Descrição |
|---|---|
| `atividade_id` | identificador |
| `user_id` | conta |
| `inicio` | data e hora de início, como veio da origem |
| `tipo` | tipo de treino |
| `duracao_min` | duração em minutos |
| `distancia_km` | distância, quando há GPS |
| `ritmo_min_km` | minutos por km, quando há GPS |
| `fc_media` | frequência cardíaca média, quando há relógio |
| `origem` | `app`, `garmin` ou `apple_health` |
| `gps_ok` | se o GPS registrou o percurso |
| `treino_com` | conta marcada como companhia de treino, se houver |

## 10 Questionário de entrada

`onboarding.csv` · Texto · uma linha por conta · 63.929 linhas

Desde o lançamento, ao criar a conta, a pessoa responde a um questionário curto: qual o objetivo com a Vitaliza, como conheceu o app, qual o nível dela e quantos dias por semana pretende treinar. O objetivo e o como conheceu são respostas livres, e o objetivo é opcional. As respostas vêm do jeito que a pessoa escreveu, como "quero perder uns 15kg", "ter mais disposição no dia a dia" ou "treinar junto com meu namorado".

É a primeira coisa que a pessoa diz sobre por que está ali, com as palavras dela. Para entrar num modelo, a resposta livre precisa virar variável: uma categoria, um número, uma data.

| Coluna | Descrição |
|---|---|
| `onboarding_id` | identificador da resposta |
| `user_id` | conta |
| `respondido_em` | data da resposta |
| `objetivo_texto` | resposta livre a "Qual o seu objetivo com a Vitaliza?" (opcional) |
| `como_conheceu` | resposta livre (opcional) |
| `nivel` | nível autodeclarado |
| `dias_por_semana` | quantos dias por semana pretende treinar (texto livre) |

## 11 Pesquisa de saída

`pesquisa_saida.csv` · Texto · uma resposta por linha · 643 linhas · desde 01/06/2026

Desde 01/06/2026, quem cancela pelo site vê uma pesquisa opcional: escolhe um motivo principal numa lista e pode deixar um comentário. Quem paga pela App Store ou pelo Google Play cancela na loja e nunca vê a pesquisa.

É a única fonte de motivo declarado na base, e cobre uma parte pequena das saídas: só quem paga pelo site, e só quem quis responder. O comentário é texto livre e pode complementar o motivo marcado.

| Coluna | Descrição |
|---|---|
| `resposta_id` | identificador |
| `user_id` | conta |
| `respondido_em` | data |
| `motivo_principal` | `preco`, `nao_uso`, `problema_tecnico`, `outro_app`, `saude` ou `outro` |
| `comentario` | texto livre (opcional) |

*Os 3.389 fins de assinatura de junho a setembro de 2026 e as 3.362 perdas da série mensal medem coisas diferentes: a série conta só quem estava ativo no início do mês e deixa de fora assinaturas que começaram e terminaram no mesmo mês. As 643 respostas, de 641 contas, incluem 289 de quem cancelou pelo site e seguia ativo em 30/09/2026, porque o período pago terminava depois do corte.*

## 12 Posts da rede social

`feed_posts.csv` · Texto · um post por linha · 119.309 linhas · desde 01/07/2025

Os posts que as pessoas publicam na rede social da Vitaliza, de 01/07/2025 a 30/09/2026, com o texto e o número de curtidas. São textos curtos, escritos no celular, quase sempre logo depois de um treino: "5km leves", "funcional em casa", "treino rápido de 30 min".

Os posts são o que cada pessoa conta por vontade própria, no tempo dela, e por isso podem dizer coisas que nenhuma tabela registra. Como todo texto, precisam virar variável antes de entrar num modelo. Como todo dado com data, só podem ser usados até a data de corte da análise.

| Coluna | Descrição |
|---|---|
| `post_id` | identificador |
| `user_id` | autor |
| `data_hora` | publicação |
| `texto` | texto do post |
| `curtidas` | curtidas recebidas |

## 13 Chamados ao suporte

`tickets_suporte.csv` · Texto · um chamado por linha · 4.422 linhas · desde 01/07/2025

Cada chamado aberto ao suporte, por chat, por e-mail ou pela página do app na loja, desde 01/07/2025. O arquivo traz a primeira mensagem do cliente, a categoria que o atendente escolheu ao registrar o chamado, a situação e a data de resolução. As mensagens vêm como o cliente escreveu: "esqueci a senha e o e-mail de recuperação não chega", "corrida registrada com distância zerada".

O suporte é onde aparecem problemas de cobrança, falhas do app e pedidos de cancelamento. Há duas versões do mesmo chamado: a categoria, que é a classificação do atendente, e o texto, que é o problema nas palavras do cliente.

| Coluna | Descrição |
|---|---|
| `ticket_id` | identificador |
| `user_id` | conta |
| `aberto_em` | abertura |
| `canal` | `chat`, `email` ou `loja` |
| `texto_cliente` | primeira mensagem do cliente |
| `categoria_atendente` | categoria escolhida pelo atendente |
| `status` | `resolvido`, `aberto` ou `sem_resposta` |
| `resolvido_em` | data de resolução |

## 14 Mapas de calor das rotas

`heatmaps_90d/` · Imagem · uma imagem por assinante e data · 12.426 em 31/07 e 13.047 em 30/09/2026

O perfil de cada pessoa no app mostra um mapa de calor com as rotas dos treinos ao ar livre: quanto mais vezes ela passou por um trecho, mais forte a cor. O data room traz essa imagem em duas datas, nas pastas `2026-07-31/` e `2026-09-30/`. Cada arquivo `<user_id>.png` é o mapa da pessoa nos 90 dias até a data da pasta.

É a única fonte que mostra onde e como a pessoa treina, e não só quanto. Para virar variável, a imagem precisa ser lida, seja contando pixels por cor, seja com um modelo que interpreta imagem.

- Só existe imagem para quem era assinante pagante naquela data e treinou ao ar livre no período.
- O mapa de fundo é estilizado e não corresponde a ruas reais.
- Cores do mapa de fundo: verde é parque, azul é água, a faixa cor de areia é praia e amarelo é avenida.
