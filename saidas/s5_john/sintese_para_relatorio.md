# Síntese para o relatório do grupo — contribuição de John

## Preparação dos dados e diagnóstico

A análise integra os dados da Vitaliza até 30/09/2026 e reconstrói as assinaturas a partir dos eventos de início e expiração. Contas de teste são excluídas pelo domínio de e-mail normalizado. O resultado fecha com as referências do enunciado: 8.540 pagantes no início de 2025, 14.237 no início de abril/2026 e 14.753 ativos no corte. A base de segmentação tem uma linha por pagante, com indicadores observados de treino, uso social, suporte e perfil de entrada.

O churn é medido como a proporção dos ativos no início do mês que encerram a assinatura naquele mês. A média mensal simples foi de 5,62% em 2025 e 6,62% entre janeiro e setembro de 2026. Para comparar períodos equivalentes, janeiro a setembro apresenta 5,61% em 2025 contra 6,61% em 2026, usando perdas divididas pelas exposições usuário-mês. Abril/2026 foi o pico: 1.154 perdas entre 14.237 ativos no início do mês, ou 8,11%.

A piora permanece dentro dos dois planos. Entre janeiro e setembro, o mensal passou de 9,14% para 10,86%, e o anual de 2,45% para 3,32%. Uma decomposição aritmética da alta agregada de aproximadamente 1,00 ponto percentual atribui 1,25 p.p. à elevação das taxas dentro dos planos e −0,25 p.p. à mudança da composição. A maior participação do anual atenua a alta agregada; não a explica. Esses componentes descrevem a conta, sem identificar mecanismos causais. As taxas contratuais mensal e anual têm calendários distintos de renovação e não medem diretamente insatisfação.

O uso anterior apresenta associação com a saída posterior. Entre pagantes que já estavam ativos no início do mês de uso, o churn observado em 2026 foi de 11,18% para quem não treinou no mês anterior e de 4,04% para quem registrou oito ou mais treinos. O padrão persiste ao separar os planos: no mensal, 40,75% versus 7,49%; no anual, 8,79% versus 0,40%. Essas são taxas de grupos históricos, não probabilidades individuais de saída nem efeito de uma ação de retenção. O uso pode refletir diversas condições subjacentes; incentivar treino não tem benefício causal demonstrado por esta comparação.

O plano mensal passou de 10,07% de churn em janeiro–fevereiro/2026 para 12,82% em março–abril, retornando a 10,34% em maio–setembro. A proximidade com o reajuste de março justifica investigar sensibilidade a preço, sem excluir sazonalidade, tempo de assinatura e composição dos clientes. Não é possível atribuir essa variação ao reajuste apenas com a comparação entre períodos.

Os chamados classificados como técnicos somaram 17, 14, 20 e 19 de janeiro a abril/2026, seguidos de 383 em maio e 310 em junho. A tabela abrange todas as contas que abriram chamados; a versão restrita a pagantes no momento da abertura está disponível separadamente. O pico sugere uma investigação de problemas de produto nesse intervalo, mas não demonstra que uma atualização do aplicativo causou churn. A mudança de idioma nos registros desde 15/04/2026 também é um sinal de alteração de registro, não prova de defeito. Os picos de suporte posteriores não bastam para explicar o pico de churn de abril.

## Hipóteses e verificações necessárias

| Hipótese | Evidência que motiva investigar | Próxima verificação |
|---|---|---|
| Baixo engajamento antecipa parte das saídas | Gradiente de churn por uso anterior, também dentro dos planos | Comparar coortes, tempo de casa, elegibilidade de renovação e outras características anteriores à saída |
| Reajuste contribuiu para a piora do mensal | Churn mensal maior em março–abril após a mudança de preço | Comparar meses equivalentes, clientes e ciclos de renovação; separar mudanças de perfil |
| Problemas técnicos contribuíram para saídas | Concentração de tickets técnicos em maio–junho | Relacionar abertura anterior à saída, tema do ticket e recorrência; a versão atual do app não informa a versão histórica |
| Canal marca públicos ou fricções diferentes | Em 2026 as taxas vão de 5,96% na App Store a 7,33% no Pix | Estratificar por plano, tempo de casa e uso; separar cobrança involuntária de decisão de sair |

## Limitações que precisam acompanhar as conclusões

- O BI mensal e o detalhe tratado dos treinos não conciliam em 6.716 linhas de setembro, das quais 5.542 são dos pagantes atuais. O diagnóstico histórico usa o BI com sua origem explícita; as variáveis recomendadas para agrupamento usam a atividade detalhada tratada. Não se combinam as contagens como se fossem equivalentes.
- A atividade detalhada contém 9.383 cópias de registros de relógio no app, 3.649 durações inválidas antes da deduplicação, 999 distâncias incompatíveis com o ritmo e outras três distâncias altas sem duração/ritmo avaliável. As decisões e contagens de tratamento estão documentadas.
- A pesquisa de saída é opcional e restrita ao site. Ela descreve respondentes, sem representar todos os assinantes. Renovação desligada não equivale a expiração.
- Eventos e retrato discordam sobre renovação em cinco casos conhecidos; o estado inicial não está informado nos eventos relevantes de 1.112 pagantes antigos. Esses campos são mantidos separados e não entram no agrupamento proposto.
- Não há desfecho futuro até 29/11/2026, score individual, efeito incremental de contato ou ROI calculados nesta contribuição.

## Encaminhamento para as demais frentes

Leonardo recebe uma base por pagante e 17 variáveis candidatas de agrupamento, além da chave de integração. Deve selecionar variáveis, avaliar correlação e escalas, tratar ausências e validar os clusters. Os campos de volume de treino são relacionados entre si; usar todos sem escolha pode dar peso excessivo ao engajamento. Churn histórico por cluster exigirá aplicar a segmentação às observações históricas correspondentes, e não somente classificar quem sobreviveu até o corte.

Claudinne recebe os filtros, as medidas de qualidade e as pendências de conciliação. Kiril recebe o diagnóstico e, após a clusterização, poderá construir personas ancoradas em comportamentos observados. Marcela recebe plano, canal e uma aproximação mensal da última cobrança aprovada; esse valor não é receita contábil, LTV ou benefício de retenção. A priorização final exige complementar risco com valor, custos e capacidade de ação.

Fontes e rastreabilidade: enunciado e dicionário do case, decisões do grupo, código reproduzível, CSVs agregados e gráficos em `saidas/s5_john/`. As bases individuais e o manifesto de validação ficam em `dados/processados/s5_john/`, fora do repositório público. Esta seção está preparada para revisão e integração ao relatório do grupo.
