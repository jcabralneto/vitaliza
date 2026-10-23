# Vitaliza: enunciado do case

> Transcrição em Markdown de `docs/Vitaliza - Enunciado do case.pdf` (MBA em IA e Dados para Negócios · Inteli · Business Case Módulo 2), gerada em 2026-10-22 para leitura rápida por agentes.
> **O PDF é a fonte oficial.** Se ele for atualizado, gere este arquivo de novo.

## 01 Contexto e objetivos

### A pandemia e os apps de treino

Em março de 2020, a pandemia de covid-19 fechou academias e clubes e reduziu a circulação nas ruas. Um estudo com 455.404 usuários de um app de contagem de passos, em 187 países, registrou queda média de 27,3% nos passos diários nos 30 dias seguintes à declaração da pandemia, em 11 de março (TISON et al., 2020). Nos Estados Unidos, uma pesquisa que acompanhou 431 adultos mediu redução de 18,2% na atividade física durante o confinamento. Quem usava apps de atividade física perdeu menos, e o efeito foi maior nos apps com desafios, metas e outros recursos de gamificação (YANG; KOENIGSTORFER, 2020).

O celular passou a fazer o papel da academia. Os downloads de apps de fitness cresceram 46% do primeiro para o segundo trimestre de 2020 nas lojas da Apple e do Google, sem contar a China (ANG, 2020). Nos Estados Unidos, a categoria de saúde e fitness somou 405 milhões de instalações em 2020, 22% a mais que em 2019, e o gasto dos usuários nesses apps chegou a US$ 838 milhões, alta de 42% (CHAN, 2021).

Depois do pico, a aquisição esfriou e a receita continuou subindo. No quarto trimestre de 2022, a categoria teve cerca de 290 milhões de downloads no mundo, o menor volume desde o primeiro trimestre de 2020, quando foram 417 milhões. No mesmo ano, a receita dos apps de saúde e fitness chegou a US$ 1,7 bilhão, US$ 300 milhões acima de 2021 (REHFELDT, 2023). Com menos gente nova chegando, o crescimento passou a depender de manter pagando quem já assina.

### A corrida de rua no Brasil

No Brasil, a corrida de rua continuou crescendo depois da pandemia. No relatório anual do Strava de 2024, o país aparece em segundo lugar em número de corredores na plataforma, atrás dos Estados Unidos, e as atividades em grupo cresceram 109% no Brasil, contra 59% na média global (MÁQUINA DO ESPORTE, 2024). As inscrições vendidas pela Ticket Sports, plataforma de inscrição em provas, somaram 1,8 milhão em 2024, alta de 75% sobre 2023 (PACHECO, 2025). Em 2025, o país teve 5.241 corridas de rua organizadas, contra 2.827 em 2024, e um estudo da Box 1824 estimou em 15 milhões o número de corredores (CASTELLÓN, 2026).

Os líderes do mercado disputam esse público com personalização. Em 2024, o Strava lançou um recurso que transforma os dados de cada treino em análises individuais (STRAVA, 2024); em 2025, anunciou a compra do Runna, app de planos de treino de corrida (STRAVA, 2025).

### Por que retenção

Num app de assinatura, cada assinante perdido é receita futura que deixa de entrar. Reichheld e Sasser (1990) estimaram que empresas de serviços podiam aumentar o lucro em quase 100% retendo apenas 5% a mais dos clientes. Nos apps, a perda começa cedo: segundo o relatório anual da RevenueCat, quase 30% das assinaturas anuais são canceladas no primeiro mês, e, depois de um ano, os apps com plano anual barato mantêm até 36% dos assinantes, contra 6,7% dos apps com plano mensal caro (EITING, 2025).

### A Vitaliza

A Vitaliza é um app brasileiro de assinatura para quem treina. Foi lançada em setembro de 2020, em plena pandemia, e tem três partes: registro de treino ao ar livre com GPS (corrida, caminhada e pedal), treinos guiados em vídeo (funcional, força e yoga) e uma rede social em que as pessoas postam treinos, comentam e seguem umas às outras. O app conecta relógios Garmin e Apple Watch, e cerca de quatro em cada dez contas têm um relógio conectado.

O modelo é freemium. Registrar treino é grátis; o Premium é pago e começa com 7 dias de teste. Custa R$ 39,90 por mês ou R$ 299,90 por ano. No anual, a conta dá R$ 24,99 por mês, 37% menos que o mensal. O mensal custava R$ 34,90 até 28/02/2026 e subiu para R$ 39,90 em 01/03/2026. A assinatura se renova sozinha a cada mês ou a cada ano; quem cancela deixa de pagar dali em diante.

A base paga cresceu devagar nos primeiros anos: cerca de 400 assinantes no fim de 2020, 1.800 no fim de 2021, 3.100 no fim de 2022 e 4.500 no fim de 2023. A partir de 2024, junto com a expansão da corrida de rua, o ritmo mudou. A Vitaliza começou 2025 com 8.540 assinantes pagantes, terminou o ano com cerca de 13.200 e chegou a 14.753 em 30/09/2026, a data de corte da base de dados do case. A maior parte das 64.948 contas cadastradas usa só a versão grátis. As contas chegam principalmente por tráfego orgânico, influenciadores, anúncios, indicação de amigos e parcerias com empresas.

Dos 14.753 assinantes pagantes ativos em 30/09/2026, 57% estão no plano anual e 43% no mensal. O plano muda o ritmo da perda: no mensal, quem decide sair deixa de pagar no mês seguinte; no anual, só na renovação. Sete em cada dez assinantes pagam pela loja do celular (App Store, 36,6%, e Google Play, 33,6%) e três pagam pelo site da Vitaliza (cartão, 20,3%, e Pix, 9,5%). O canal parece detalhe de pagamento, mas decide onde a pessoa cancela e o que a empresa consegue ver disso (seção 02).

A métrica que a empresa acompanha é o **churn mensal**: assinaturas perdidas no mês divididas pelos assinantes ativos no início do mês. A média foi de 5,6% ao mês em 2025 e de 6,6% de janeiro a setembro de 2026. O pior mês foi abril de 2026: 1.154 assinaturas perdidas sobre 14.237 ativos no início do mês, 8,1%. Agosto (5,9%) e setembro (5,0%) ficaram abaixo da média de 2026. Com churn de 6,6% ao mês, a empresa mantém 93,4% da base de um mês para o outro. Olhar a taxa, e não o número de perdas, importa porque a base cresceu cerca de 68% no período, de 8.540 ativos no início de janeiro de 2025 para 14.319 no início de setembro de 2026: com mais gente, perde-se mais gente mesmo sem piora.

*A Vitaliza é fictícia e os dados da base foram gerados para o curso. Os dados de mercado citados nesta seção são reais.*

### O objetivo do case

O case pede que vocês usem a base da Vitaliza para responder ao que a empresa não consegue responder sozinha: quem vai sair, em quem vale a pena agir, com qual mensagem e quanto isso rende. Ao longo do módulo, a resposta vira um sistema de cinco peças:

1. **Dados:** os arquivos do data room, em três formas: tabelas, logs de eventos e texto e imagem. Cada arquivo está descrito no documento *Vitaliza: dicionário de dados*.
2. **Extração:** IA generativa lê texto e imagem e devolve campos com nome e formato combinados antes, que viram variáveis.
3. **Previsão:** um modelo treinado com o histórico da Vitaliza estima a probabilidade de saída de cada assinante.
4. **Decisão:** uma regra escolhe quem contatar, por qual canal e com qual oferta, dentro dos limites do CRM.
5. **Mensagem:** IA generativa escreve o texto para cada pessoa contatada, seguindo um briefing de negócio.

A seção 02 detalha o que a empresa não sabe e os objetivos que saem daí.

## 02 O que a empresa não sabe e o que o case pede

A Vitaliza tem muitos dados, mas não consegue responder a quatro perguntas que decidem a retenção.

### Quatro lacunas

1. **Por que o churn subiu em 2026.** Ninguém na empresa sabe explicar a subida. A empresa registra três fatos no período: o reajuste do plano mensal em 01/03/2026, o início da pesquisa de saída em junho e a campanha de retenção de 10/08/2026. Nenhum deles foi testado como causa, e pode haver outras.
2. **Por que cada assinante saiu.** Quem paga pela App Store ou pelo Google Play cancela nas configurações da loja, fora do app (APPLE, 2026a; GOOGLE, 2026a). A Vitaliza não vê essa tela. Recebe do servidor da loja dois avisos, sem o motivo: primeiro, que a renovação automática foi desligada; depois, no fim do período já pago, que a assinatura expirou (APPLE, 2026b; GOOGLE, 2026b). Entre um aviso e outro, a pessoa continua assinante e pode usar o app. Só quem paga pelo site cancela numa tela da Vitaliza, que desde 01/06/2026 tem uma pesquisa de saída opcional. De junho a setembro de 2026, 3.389 assinaturas terminaram: 2.271 pela loja e 1.118 pelo site. Só 353 dessas pessoas responderam à pesquisa, cerca de 10% do total. O motivo declarado existe para uma minoria que se escolheu sozinha, e tirar dela uma conclusão sobre todos é viés de seleção. Há uma consequência prática: uma oferta na hora do cancelamento só alcança quem paga pelo site. Para os outros 70%, a empresa precisa agir antes, a partir de sinais de uso, ou no intervalo entre os dois avisos.
3. **Se a campanha de 10/08/2026 funcionou.** A empresa sorteou os 14.120 assinantes pagantes daquele dia em quatro grupos de tamanho parecido. Três receberam, por push e e-mail, mensagens diferentes: desafio ("Novo desafio de 6 semanas montado para você"), cupom ("Oferta para voltar a treinar", com 30% de desconto por 3 meses no mensal ou 1 mês grátis no anual) e conteúdo ("Seu plano de treino personalizado está pronto"). O quarto grupo, de controle, não recebeu nada. Como a divisão foi por sorteio, os grupos têm, em média, o mesmo perfil, e a diferença de saída entre um grupo que recebeu mensagem e o controle pode ser atribuída à mensagem (KOHAVI; TANG; XU, 2020). O resultado nunca foi analisado.
4. **Quem vale a pena contatar.** O CRM tem teto: 1.500 mensagens de WhatsApp e 300 atendimentos do time de CS por mês, para 14.753 assinantes pagantes. O WhatsApp alcança cerca de 1 em cada 10 pagantes por mês, e cada oferta tem custo (seção 03). Escolher quem recebe o contato não é opcional.

### Os objetivos do case

Cada objetivo abaixo é uma pergunta de negócio, seguida do caminho técnico que o módulo percorre para respondê-la. A ordem segue os quatro tipos de análise, da descritiva à prescritiva (LEPENIOTI et al., 2020), e o roteiro do CRISP-DM: entender o negócio e os dados antes de modelar e avaliar o resultado antes de usá-lo (CHAPMAN et al., 2000). Cada objetivo usa o resultado do anterior.

1. **Contar e medir a base.** Quantos assinantes pagantes ativos a Vitaliza tinha no corte? Quanto perde por mês, e como isso varia por plano e por canal? A pergunta parece simples e não é: a mesma conta dá números diferentes conforme o arquivo e a regra usados. No caminho técnico estão a conferência de qualidade de cada arquivo, a integração das tabelas pelo `user_id` e a reconstrução da situação de cada assinante numa data a partir do histórico de eventos. É a análise descritiva, e um erro aqui contamina todo o resto.
2. **Explicar a subida de 2026.** O que mudou entre 2025 e 2026, e para quem? O objetivo é transformar suspeitas em hipóteses que os dados podem confirmar ou derrubar, por exemplo sobre plano, canal, tempo de casa, frequência de treino ou preço, e testá-las. A técnica é a análise exploratória com cruzamentos de duas variáveis e comparação entre grupos e períodos. É a análise diagnóstica, com um limite que precisa ficar claro: cruzamento aponta suspeitos, não prova causa.
3. **Conhecer os assinantes.** Quem são os assinantes da Vitaliza, em grupos que qualquer área da empresa entenda? Os segmentos são a base para escolher a mensagem e a oferta de cada pessoa. A técnica é a clusterização, que agrupa assinantes parecidos sem usar a informação de quem saiu (JAMES et al., 2023). O cuidado está na escolha das variáveis e da escala, que decidem quais grupos aparecem.
4. **Prever quem vai sair.** Qual a probabilidade de cada assinante sair nos 60 dias seguintes ao corte, até 29/11/2026? O resultado é uma lista ordenada por risco, que o CRM usa para escolher onde agir. A técnica é a classificação supervisionada: primeiro a regressão logística, como modelo de referência; depois as árvores de decisão, que se leem como regras; e por fim bagging e boosting, que combinam muitas árvores para errar menos (JAMES et al., 2023). O modelo precisa ser avaliado em dados que não viu no treino, com separação no tempo, e sem usar informação posterior ao corte (KAUFMAN et al., 2012).
5. **Medir o valor de texto e imagem.** O questionário de entrada, os posts da rede social, as mensagens ao suporte e os mapas de calor das rotas melhoram a previsão o bastante para pagar o custo de processá-los? Texto e imagem não entram num modelo como estão: precisam virar variável. A técnica é a extração com IA generativa, em que um modelo de linguagem lê o conteúdo e devolve campos com nome e formato combinados antes (GILARDI; ALIZADEH; KUBLI, 2023). A extração precisa ser conferida contra uma amostra rotulada à mão, com acerto e custo por assinante medidos. Para as imagens, também é possível contar pixels por cor, e vale comparar os dois caminhos. A resposta vem da comparação entre modelos com e sem essas variáveis.
6. **Decidir quem contatar, com qual mensagem, e quem deixar quieto.** Risco alto não basta. Siegel (2013, cap. 7) separa os clientes em quatro tipos pelo efeito do contato: os persuadíveis ficam só se forem contatados; os garantidos ficam de qualquer jeito; os perdidos saem de qualquer jeito; e os que não se deve perturbar saem justamente porque foram contatados, por exemplo quando a mensagem os lembra de que pagam por algo que quase não usam. Só no primeiro grupo o contato compensa o custo. O efeito do contato, chamado de uplift ou efeito incremental, não se vê numa pessoa só: mede-se comparando grupos sorteados (RADCLIFFE; SURRY, 2011; GUTIERREZ; GÉRARDY, 2017), e a campanha de agosto é esse sorteio. É a análise prescritiva: a regra de contato junta o risco, o efeito estimado de cada mensagem, os segmentos e os limites do CRM.
7. **Calcular quanto a ação rende.** Quanto a Vitaliza ganha com a regra de contato, em reais, comparada a não fazer nada? Só entra na conta a receita de quem ficou por causa do contato, menos o custo dos contatos e das ofertas. Quem ficaria de qualquer jeito não entra, e o cupom que recebeu é custo. Avaliar um modelo de churn pelo lucro que ele gera, e não só pela taxa de acerto, muda qual modelo é o melhor (VERBEKE et al., 2012). Os valores para a conta estão na seção 03.
8. **Escrever a mensagem.** O que dizer a cada pessoa contatada? A IA generativa volta como redatora: escreve para quem a regra mandou contatar, a partir do que a extração encontrou sobre a pessoa, e segue um briefing de negócio com tom, ofertas permitidas e o que não dizer. Com isso o sistema fecha: entra um assinante, saem o risco, a decisão e a mensagem.

## 03 Premissas de negócio

Estes são os valores que o financeiro e o CRM da Vitaliza usam para planejar novembro e dezembro de 2026. Toda conta de custo, receita e retorno do case parte deles.

### Preço e receita

O plano mensal custa R$ 39,90 desde 01/03/2026; até 28/02/2026, custava R$ 34,90. O plano anual custa R$ 299,90. Quem chega por cupom de influenciador paga R$ 239,90 no primeiro ano do anual e o preço cheio a partir da renovação.

O preço é o que o assinante paga, não o que a Vitaliza recebe. A App Store e o Google Play ficam com 15% de cada cobrança. No site, a operadora do cartão fica com 3,5% e o Pix Automático custa 0,99%. Uma mensalidade de R$ 39,90 deixa para a Vitaliza R$ 33,92 quando paga pela loja, R$ 38,50 no cartão e R$ 39,50 no Pix. Uma anuidade de R$ 299,90 paga pela loja deixa R$ 254,92. Como sete em cada dez assinantes pagam pela loja, a taxa de 15% é a que mais pesa na receita.

| Canal | Taxa | Mensal R$ 39,90 líquido | Anual R$ 299,90 líquido |
|---|---|---|---|
| App Store / Google Play | 15% | R$ 33,92 | R$ 254,92 |
| Cartão (site) | 3,5% | R$ 38,50 | — |
| Pix Automático (site) | 0,99% | R$ 39,50 | — |

*(Tabela de resumo adicionada nesta transcrição; os valores são os do texto.)*

### Custo de servir e de adquirir

Manter um assinante custa R$ 4,20 por mês, somando infraestrutura, conteúdo e suporte. Esse custo existe enquanto a pessoa for assinante, use ela o app ou não.

Trazer um assinante novo custou, em média, R$ 118 em 2026: é o custo de aquisição de cliente, ou CAC. Repor um assinante mensal da loja que saiu custa, portanto, o equivalente a cerca de três mensalidades e meia de receita líquida.

### Canais de contato

O CRM tem quatro canais, com custo e capacidade diferentes. As capacidades valem para novembro e dezembro de 2026.

O **push** tem custo desprezível, mas cada assinante pode receber no máximo um por semana. O **e-mail** custa R$ 0,01 por envio e não tem limite prático. O **WhatsApp** custa R$ 0,40 por mensagem e tem teto de 1.500 mensagens por mês. A **ligação ou chat ativo do time de CS** custa R$ 18,00 por atendimento e tem teto de 300 atendimentos por mês.

Com o teto todo usado, o WhatsApp custa R$ 600 por mês e o CS, R$ 5.400. Nos dois canais, o teto pesa mais que o custo: 1.500 mensagens alcançam cerca de um em cada dez pagantes, e 300 atendimentos, um em cada cinquenta. Cada contato dado a quem não precisava dele é um contato a menos para quem precisava.

| Canal | Custo por contato | Teto mensal |
|---|---|---|
| Push | desprezível | 1 por assinante por semana |
| E-mail | R$ 0,01 | sem limite prático |
| WhatsApp | R$ 0,40 | 1.500 mensagens |
| CS (ligação ou chat ativo) | R$ 18,00 | 300 atendimentos |

*(Tabela de resumo adicionada nesta transcrição; os valores são os do texto.)*

### Ofertas

O CRM pode usar quatro ofertas. Para o plano mensal, **30% de desconto por 3 meses**: o custo é o próprio desconto, R$ 11,97 por mês sobre os R$ 39,90, ou R$ 35,91 nos três meses. Para o plano anual, **1 mês grátis no fim do ciclo**: R$ 25,00 de receita abatida. Para qualquer plano, a **pausa da assinatura por até 60 dias**, em que a receita do período fica adiada, e o **plano de treino ou conteúdo personalizado**, sem custo direto.

Uma oferta dada a quem ficaria de qualquer jeito é custo sem retorno. Uma oferta dada a quem sairia de qualquer jeito também. A conta de retorno só fecha quando se sabe, ou se estima, quanto a oferta muda a chance de a pessoa ficar.

### Orçamento

O orçamento de CRM é de R$ 40.000 por mês, já contando os descontos concedidos. O custo de IA generativa usada pelo sistema, para escrever mensagens, extrair informação de texto ou ler imagens, sai do mesmo orçamento. Não há verba separada para isso: calculem o custo pela tabela de preços do provedor que o grupo escolher e incluam na conta.

## 04 Referências

ANG, Carmen. **Fitness apps grew by nearly 50% during the first half of 2020, study finds**. [S. l.]: World Economic Forum, 15 set. 2020. Disponível em: https://www.weforum.org/stories/2020/09/fitness-apps-gym-health-downloads/. Acesso em: 13 out. 2026.

APPLE. **Cancel a subscription from Apple**. Apple Support, 29 set. 2026a. Disponível em: https://support.apple.com/118428. Acesso em: 13 out. 2026.

APPLE. notificationType. *In*: APPLE. **App Store Server Notifications**. Cupertino: Apple Developer Documentation, [2026b]. Disponível em: https://developer.apple.com/documentation/appstoreservernotifications/notificationtype. Acesso em: 13 out. 2026.

CASTELLÓN, Lena. Corrida de rua cresce no Brasil: já são 15 milhões de praticantes, a maioria mulheres. **IstoÉ**, São Paulo, 1 fev. 2026. Disponível em: https://istoe.com.br/corrida-de-rua-15-milhoes-corredores-maioria-mulheres. Acesso em: 13 out. 2026.

CHAN, Stephanie. **State of health & fitness apps 2021**. San Francisco: Sensor Tower, fev. 2021. Disponível em: https://sensortower.com/blog/state-of-health-and-fitness-apps-report-2021. Acesso em: 13 out. 2026.

CHAPMAN, Pete; CLINTON, Julian; KERBER, Randy; KHABAZA, Thomas; REINARTZ, Thomas; SHEARER, Colin; WIRTH, Rüdiger. **CRISP-DM 1.0**: step-by-step data mining guide. [S. l.]: SPSS, 2000. 78 p.

EITING, Jacob. **The state of subscription apps 2025**: the year AI ate everything. [S. l.]: RevenueCat, 14 mar. 2025. Disponível em: https://www.revenuecat.com/blog/company/the-state-of-subscription-apps-2025-launch/. Acesso em: 13 out. 2026.

GILARDI, Fabrizio; ALIZADEH, Meysam; KUBLI, Maël. ChatGPT outperforms crowd workers for text-annotation tasks. **Proceedings of the National Academy of Sciences**, v. 120, n. 30, e2305016120, jul. 2023. DOI: https://doi.org/10.1073/pnas.2305016120.

GOOGLE. **Cancel, pause, or change a subscription on Google Play**. Google Play Help, [2026a]. Disponível em: https://support.google.com/googleplay/answer/7018481. Acesso em: 13 out. 2026.

GOOGLE. **Real-time developer notifications reference guide**. Android Developers: Play Billing, 6 out. 2026b. Disponível em: https://developer.android.com/google/play/billing/rtdn-reference. Acesso em: 13 out. 2026.

GUTIERREZ, Pierre; GÉRARDY, Jean-Yves. Causal inference and uplift modelling: a review of the literature. *In*: **Proceedings of the 3rd International Conference on Predictive Applications and APIs**. [S. l.]: PMLR, 2017. (Proceedings of Machine Learning Research, v. 67). p. 1-13. Disponível em: https://proceedings.mlr.press/v67/gutierrez17a.html. Acesso em: 13 out. 2026.

JAMES, Gareth; WITTEN, Daniela; HASTIE, Trevor; TIBSHIRANI, Robert; TAYLOR, Jonathan. **An introduction to statistical learning**: with applications in Python. Cham: Springer, 2023. DOI: https://doi.org/10.1007/978-3-031-38747-0.

KAUFMAN, Shachar; ROSSET, Saharon; PERLICH, Claudia; STITELMAN, Ori. Leakage in data mining: formulation, detection, and avoidance. **ACM Transactions on Knowledge Discovery from Data**, v. 6, n. 4, p. 1-21, dez. 2012. DOI: https://doi.org/10.1145/2382577.2382579.

KOHAVI, Ron; TANG, Diane; XU, Ya. **Trustworthy online controlled experiments**: a practical guide to A/B testing. [Cambridge]: Cambridge University Press, 2020. DOI: https://doi.org/10.1017/9781108653985.

LEPENIOTI, Katerina; BOUSDEKIS, Alexandros; APOSTOLOU, Dimitris; MENTZAS, Gregoris. Prescriptive analytics: literature review and research challenges. **International Journal of Information Management**, v. 50, p. 57-70, fev. 2020. DOI: https://doi.org/10.1016/j.ijinfomgt.2019.04.003.

MÁQUINA DO ESPORTE. Strava: running é o esporte mais praticado no mundo em 2024, com Brasil na vice-liderança. **Máquina do Esporte**, [S. l.], 6 dez. 2024. Disponível em: https://maquinadoesporte.com.br/running/strava-running-e-o-esporte-mais-praticado-no-mundo-em-2024-com-brasil-na-vice-lideranca/. Acesso em: 13 out. 2026.

PACHECO, Paula. Corrida de rua acelera no Brasil. **Fast Company Brasil**, [S. l.], 6 jan. 2025. Disponível em: https://fastcompanybrasil.com/money/corrida-de-rua-acelera-no-brasil/. Acesso em: 13 out. 2026.

RADCLIFFE, Nicholas J.; SURRY, Patrick D. **Real-world uplift modelling with significance-based uplift trees**. [Edinburgh]: Stochastic Solutions, 2011. (Portrait Technical Report TR-2011-1).

REHFELDT, Courtney. Health & fitness app market shows promise despite decline in downloads. **Athletech News**, [S. l.], 21 jul. 2023. Disponível em: https://athletechnews.com/health-fitness-app-market-shows-promise-despite-decline-in-downloads/. Acesso em: 13 out. 2026.

REICHHELD, Frederick F.; SASSER JR., W. Earl. Zero defections: quality comes to services. **Harvard Business Review**, Boston, v. 68, n. 5, p. 105-111, set./out. 1990.

SIEGEL, Eric. **Predictive analytics**: the power to predict who will click, buy, lie, or die. Hoboken: Wiley, 2013. 302 p.

STRAVA. **Strava's Athlete Intelligence translates workout data into simple and personalized insights**. San Francisco, 3 out. 2024. Disponível em: https://press.strava.com/articles/stravas-athlete-intelligence-translates-workout-data-into-simple-and. Acesso em: 13 out. 2026.

STRAVA. **Strava to acquire Runna, a leading running training app**. San Francisco, 17 abr. 2025. Disponível em: https://press.strava.com/articles/strava-to-acquire-runna-a-leading-running-training-app. Acesso em: 13 out. 2026.

TISON, Geoffrey H.; AVRAM, Robert; KUHAR, Peter; ABREAU, Sean; MARCUS, Greg M.; PLETCHER, Mark J.; OLGIN, Jeffrey E. Worldwide effect of COVID-19 on physical activity: a descriptive study. **Annals of Internal Medicine**, v. 173, n. 9, p. 767-770, nov. 2020. DOI: https://doi.org/10.7326/M20-2665.

VERBEKE, Wouter; DEJAEGER, Karel; MARTENS, David; HUR, Joon; BAESENS, Bart. New insights into churn prediction in the telecommunication sector: a profit driven data mining approach. **European Journal of Operational Research**, v. 218, n. 1, p. 211-229, abr. 2012. DOI: https://doi.org/10.1016/j.ejor.2011.09.031.

YANG, Yanxiang; KOENIGSTORFER, Joerg. Determinants of physical activity maintenance during the Covid-19 pandemic: a focus on fitness apps. **Translational Behavioral Medicine**, v. 10, n. 4, p. 835-842, ago. 2020. DOI: https://doi.org/10.1093/tbm/ibaa086.
