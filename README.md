# Software S.A - Análise de churn 📑

Nesse projeto apliquei conceitos de estatística descritiva, análise exploratória dos dados (EDA) e linguagem python afim de investigar o aumento da taxa de churn (não renovação de contratos) no período avaliado. 
 
- [Notebook completo no Google Colab](https://colab.research.google.com/drive/1nDUoHjKJDtCB1sTncU3YMslcgYRynDy4?usp=sharing)
- [Notebook completo no GitHub](https://github.com/giulia-tuffanelli/analise_churn_saas/blob/04484599f3a13f33db928f850f9ca3ce5ecf0f38/Software%20SA%20-%20An%C3%A1lise%20de%20churn.ipynb)
- [Apresentação corporativa dos resultados](https://github.com/giulia-tuffanelli/analise_churn_saas/blob/29e204940cf56151acc0e8efcd9e9f598e1e8e9a/An%C3%A1lise%20de%20Churn%20-%20Software%20S.A%20-%20Giulia.ppsx)

## Índice
 
  1.	[Contexto](https://github.com/giulia-tuffanelli/analise_churn_saas/tree/main?tab=readme-ov-file#1-contexto)
  2.	[Ferramentas de análise](https://github.com/giulia-tuffanelli/analise_churn_saas/tree/main?tab=readme-ov-file#2-ferramentas-de-an%C3%A1lise)
  3.	[Etapas da análise e principais insights](https://github.com/giulia-tuffanelli/analise_churn_saas/tree/main?tab=readme-ov-file#3-etapas-de-an%C3%A1lise-e-principais-insights)
  4.	[Produtos do projeto](https://github.com/giulia-tuffanelli/analise_churn_saas/tree/main?tab=readme-ov-file#4produtos-do-projeto)
  5.	[Conclusão](https://github.com/giulia-tuffanelli/analise_churn_saas/tree/main?tab=readme-ov-file#5-conclus%C3%A3o) 
  6.	[Recomendações](https://github.com/giulia-tuffanelli/analise_churn_saas/tree/main?tab=readme-ov-file#6-recomenda%C3%A7%C3%B5es)

## 1. Contexto
A empresa Software SA é do ramo de tecnologia e oferece soluções no modelo Software as a Service (Saas). Os clientes utilizam o sistema da empresa por meio de assinaturas, em geral com pagamentos recorrentes mensais, trimestrais ou anuais.
 
O produto principal da Software SA é um sistema de ERP (Enterprise Resource Planning), um tipo de software utilizado por pequenas e médias empresas para gerenciar rotinas administrativas, como emissão de notas fiscais, controle de estoque, financeiro, entre outras. Nos últimos meses, alguns colaboradores levantaram a hipótese de que a taxa de churn (cancelamento de assinaturas) da plataforma estaria aumentando. Eles relatam que os clientes fazem o seguinte fluxo no momento do churn:
 
Vencimento do período de contrato ➜ Overdue (contrato em atraso) ➜ Churn (não renovação do contrato)
 
A empresa me contratou como Analista de Dados para investigar essa tendência e reportar a eles os achados relevantes para reverter a situação. Disponibilizaram para mim um conjunto de bases de dados em Excel contendo informações sobre os assinantes e seus respectivos eventos dentro da plataforma.
 
**O objetivo desse projeto é validar a hipótese de aumento da taxa de churn, levantar possíveis causas dessa rotatividade e ajudar as equipes de negócio a compreender melhor o comportamento dos clientes ao longo do tempo, que é essencial para manter uma base de usuários ativa e engajada no modelo de contratos por assinatura.** 
 
Sendo assim, alinhei com a empresa as seguintes entregas do projeto:
 
1.	Validar a hipótese levantada sobre o aumento do churn;
2.	Realizar análise para identificar padrões, comportamentos e outras informações relevantes para apoiar a equipe de negócios;
3.	Elaborar uma apresentação corporativa com os principais insights obtidos.

## 2. Ferramentas de análise

Python para Análise Exploratória de Dados (EDA):

- Pandas
- Seaborn
- Matplotlib
- Numpy
- Plotly express
- Scipy stats
 
Power Point para apresentação.

## 3. Etapas de análise e principais insights

Desenvolvi o projeto por meio de EDA, com uma etapa inicial de exploração univariada seguida de exploração multivariada, fazendo correlações relevantes para o projeto. A seguir descrevo cada etapa e seu resultado.

### a.	Exploração univariada

I.	Análise geral de todo o dataframe para conhecer a base de dados, entender os tipos de variável das colunas, investigar valores únicos, verificar valores ausentes ou nulos, verificar a qualidade dos dados (por exemplo: escrita inconsistente, zeros onde não deveriam existir, unidades inconsistentes) e analisar a distribuição das variáveis categóricas e numéricas. A base conta com 7042 clientes distintos e 22 variáveis (colunas). 

II.	Análise individual de cada variável para entender melhor o perfil de clientes atendidos, ticket médio e sua aderência ao uso do software ERP através de estatística descritiva. Essa análise foi fundamental para destacar as melhores variáveis para correlação com churn. Agrupei as variáveis nas 04 categorias abaixo para melhor organização do projeto.

**Perfil de clientes:** Em relação ao porte das empresas, há uma distribuição entre 50,47% como pequena empresa e 49,52% de micro empresas. As empresas são relativamente novas, com fundação entre 2001 e 2021, sendo os anos de fundação mais frequentes entre 2016 e 2021. Em relação à estrutura societária, 51,7% não possui mais de um sócio, enquanto as que possuem mais de 1 sócio são 48,3% da base de dados. Já em relação ao número de funcionários, 70% dos clientes possuem até 5 funcionários e os outros 30% possuem 6 ou mais. 

Sobre o tipo de contrato, os clientes se distribuem entre 24% com contrato anual, 20,9% trimestral e 55% em contrato mensal. Já em relação às formas de pagamento da assinatura, 33% dos clientes paga por boleto único, 22% por boleto mensal, 21,9% cartão de crédito à vista e 21,6% com cartão de crédito parcelado. Essa distribuição sugere que os clientes tem diferentes perfis de fluxo de caixa. 
As variáveis de tipo de contrato e forma de pagamento são relevantes para correlação com churn porque impactam diretamente em inadimplência e renovação das assinaturas.

<img width="541" height="272" alt="image" src="https://github.com/user-attachments/assets/87c072f4-01e8-400c-86e6-32eae43dd588" />

 
**Ticket médio:** As variáveis 'Receita Mensal' e 'Receita total' correspondem à renda gerada por cada cliente por mês e acumulada pelo período de permanência na assinatura. O ticket médio mensal é de R$ 64,76 e a mediana é de R$ 70,35, muito próxima a média, indicando que a maioria das receitas mensais é parecida. Porém, a distribuição é levemente assimétrica a direita, ou seja, existem poucos clientes que pagam mais caro na assinatura e uma proporção maior de clientes que pagam pouco. Já o ticket médio total é de R$ 2.283,30, com valor mínimo de receita total de R$ 18,80 e máximo R$ 8.684,80. Essa alta dispersão gera uma distribuição assimétrica à esquerda, com grande concentração de clientes que tem baixo valor de receita total e poucos clientes com valores muito altos. 

<img width="541" height="272" alt="image" src="https://github.com/user-attachments/assets/8f030605-41c4-4ed3-8c3e-870b6374a801" />


Os valores de receita são relevantes para análise de churn justamente porque valores baixos podem indicar menor tempo de permanência, menor percepção do valor do produto pelo cliente, baixo engajamento com o sistema e maior chance de cancelamento da assinatura.
 
**Aderência ao uso do sistema:** Entender o engajamento dos clientes com o software é importante para medir se a aderência ao uso pode ter relação com o churn, porque clientes menos engajados podem perceber menor valor do produto e buscar o cancelamento do contrato. As variáveis consideradas nessa análise e resultados são:
 
- Meses de permanência: Há clientes com 0 meses até 72 meses de permanência do contrato. Há uma concentração de ± 800 clientes com 0 meses e ± 700 com 72 meses, sendo a mediana (50% dos clientes) 29 meses de permanência e média de 32 meses. Essa alta distribuição no 0 se mostra compatível com o comportamento esperado de churn em serviços recorrentes, que muitos entram e saem rápido, e uma minoria se mantém ativa por vários anos.

<img width="415" height="291" alt="image" src="https://github.com/user-attachments/assets/942a072f-1df5-4a7e-a053-152cf2a5805e" />


- Utiliza serviços financeiros: Os clientes estão distribuídos entre 90,31% que fazem uso desse módulo do sistema e 9,7% não utilizam. Isso pode indicar que a contratação desses serviços é o padrão, e a não utilização é exceção.
- Faz conciliação bancária: 44% dos clientes faz essa conciliação de forma manual, 34,4% de forma automática e 21,7% não fazem. Essa distribuição é relevante para entender o grau de maturidade operacional e automação do cliente.
- Emite boletos: A maioria dos clientes (59%) utiliza o sistema para emissão de boletos, enquanto que 41% não. A emissão de boletos pode indicar clientes com maior fluxo de caixa.
- Frequência de utilização do módulo financeiro: Os clientes estão distribuídos em 71,2% que fazem pouco uso, 21,7% que nunca usaram e somente 28,7% que fazem uso frequente.
- Frequência de utilização do módulo emissão de nota fiscal: Para essa feature do sistema também há maior parte dos clientes no grupo que pouco usam, 43%. Os que nunca utilizaram somam 21,6% e que fazem uso frequente são 34%.
- Frequência de utilização da integração bancária, módulo de vendas, relatórios e APIs de integração: Para todos esses módulos, há um mesmo grupo de 1526 clientes que nunca utilizaram nenhum desses, totalizando 21,6%. Isso indica que há um segmento fixo de clientes que podem só usar as funções básicas do sistema , que podem não conhecer o funcionamento dos módulos ou que tem baixa adoção de tecnologia. Em integração bancária e vendas, há uma maior distribuição de clientes que pouco usam, em torno de 43,9% (3095) e 49,3% (3473) respectivamente. Em relatórios e APIs, a distribuição entre 'Pouco uso' e 'Uso frequente' é bem próxima, 38,4% (2.707) e 38,7% (2.732) usando frequentemente contra 39,9% (2.810) e 39,5% (2.785) usando pouco, respectivamente.
 
**Cancelamento:** Nessa categoria avaliei as variáveis 'churn', se houve ou não, e o mês que ele ocorreu, na coluna 'Mês churn'. Há um total de 73,5% (5174) dos clientes com dados nulos na variável 'churn' possivelmente porque ainda são ativos. Os demais clientes que cancelaram contrato somam 1869, sendo 911 em abril/25 e 958 em maio/25, totalizando uma taxa geral de churn de 26,5%. A maioria dos clientes está ativa, enquanto cerca de um quarto já cancelou o serviço. Esse desbalanceamento é típico de bases de clientes recorrentes, especialmente quando há crescimento ou retenção estável na base. Houve um aumento claro de churn entre esses meses, tanto em percentual como em valores absolutos. 

### b.	Exploração multivariada
 
**I.	Score de engajamento:** Após análise de cada variável, entendi que pode haver uma relação entre engajamento dos clientes com uso do sistema e cancelamento da assinatura. Por isso, criei um score médio de engajamento para conseguir quantificar o quando cada cliente tem de aderência ao software e se o perfil de uso é relevante para o churn. O score leva em consideração a frequência de uso das funcionalidades do sistema e se usa ou não o módulo financeiro e de emissão de boletos, com uma pontuação atrelada a cada valor. 
 
Defini a seguinte pontuação para a frequência de uso das features:
* Nunca utilizou = 0 pontos
* Pouco uso = 1 ponto
* Uso frequente = 2 pontos 
 
Para as funcionalidades que tem uso binário (serviços financeiros e emissão de boletos), defini o seguinte:
* Sim = 2 pontos
* Não = 0 pontos
 
Primeiro é feito a soma dos pontos por cada id_cliente e depois esse valor é dividido pela quantidade de features utilizadas, fazendo uma média do engajamento. Clientes que usam os serviços em maior frequência terão o score mais alto. Com o valor médio, criei uma coluna de nível de engajamento, que pode ser baixo, médio ou alto. Sendo 0.0 a 0.75 baixo, 0.75 a 1.5 médio e 1.5 a 2.0 alto engajamento. 
 
**II.	Distribuição de clientes por engajamento:** A base de clientes é composta em sua maioria por clientes com médio nível de engajamento, 49,19% (3465), seguida pelo alto engajamento com 28,63% (2017) e baixa aderência com 22,16% (1561). O score mínimo é de 0.25, totalizando 1080 clientes, e o máximo é 2.0 que corresponde a 161 clientes. Quase um quarto da base de clientes tem pouca aderência às funcionalidades. Essa parcela de clientes pode apresentar maior risco de churn por uma baixa percepção de valor e aplicabilidade do produto na rotina.

<img width="541" height="231" alt="image" src="https://github.com/user-attachments/assets/67781888-5a4c-46c6-8fdf-062cdfdf6cba" />

**III.	Análise temporal:** No mês de abril/25 houve um total de 911 churns, uma taxa de 14,8% em relação ao total de clientes ativos na base até o início do mês. Já em maio/25 houve um aumento para 958 churns, correspondente a uma taxa de 18,5% sobre os clientes remanescentes do mês anterior. Como a base só possui esses dois meses, não é possível afirmar que há uma tendência de aumento a longo prazo.

<img width="315" height="191" alt="image" src="https://github.com/user-attachments/assets/a1f83b60-4e0f-480b-b00c-edf193e5a78f" />

**IV.	Correlação das variáveis x taxa de churn:** Fiz correlações para analisar a influência desses fatores no cancelamento de assinaturas. Além disso, também fiz agrupamentos entre o engajamento e outras variáveis além de churn, para entender como a aderência ao sistema se relaciona com os outros fatores.
 
- Churn x tipo de empresa: A distribuição geral entre churn e não churn é a mesma que nas categorias micro e pequena empresa, com 73% de clientes que não deram churn e 26% que cancelaram a assinatura. Isso mostra que o tipo de empresa, isoladamente, não é determinante para churn nesse caso.
  
- Churn x funcionários: Empresas categorizadas até 5 funcionários funcionários tem risco de 16%  a mais de churn em relação a empresas com 6 ou mais funcionários. Isso pode indicar que empresas menores são mais sensíveis a fatores do mercado/sistema. O número de funcionários, isoladamente, também não é determinante para o churn.
  
- Churn x tipo de contrato: A taxa de churn é muito maior entre os clientes com contrato mensal, planos anuais praticamente não tem churn e os trimestrais também são bem estáveis. O contrato de curto prazo é indicador de risco e quanto maior o prazo do contrato, menor o risco de cancelamento. Porém, essa correlação deve ser analisada com cautela, já que o churn em contratos anuais ainda não foi notado, só será contabilizado no mês seguinte do cancelamento.
  
<img width="315" height="291" alt="image" src="https://github.com/user-attachments/assets/278b10a9-785f-406e-a512-9e25fdcf8893" />

- Churn x tipo de pagamento: A proporção de empresas que realiza pagamento único por boleto no grupo de churns é maior em relação às outras modalidades de pagamento, totalizando 45% do total. O churn diminui em contratos com modalidade de pagamento parcelado em boleto ou à vista no crédito, que sugere que os clientes podem ter uma organização financeira melhor com essas formas de pagamento a prazo do que valor integral do contrato à vista. 

<img width="315" height="291" alt="image" src="https://github.com/user-attachments/assets/c8ebac90-990c-4d9f-985c-6b5a3f79b34f" />

- Churn x receita mensal: Clientes que deram churn tem receita mensal média de R$ 74,4 e mediana de R$ 79,65. Já os que permaneceram apresentam média de receita mensal R$ 61,26 e mediana de R$ 74,44. O gráfico nos mostra que o grupo de clientes que cancelou o contrato tem valores centrais e faixa de receita mais elevados. Clientes de ticket médio mensal maior tem tendência a churn.

<img width="315" height="291" alt="image" src="https://github.com/user-attachments/assets/40f3ea7b-d4d9-4869-8d73-56e275894a4e" />

- Churn x receita total:  Clientes que deram churn tem receita total média de 1531,79 reais e mediana de 703,55 reais. Há uma grande dispersão entre essas medidas, que pode indicar que em média cancelam mais cedo ou geram menor receita ao longo do contrato através de planos mais básicos. Clientes que permaneceram apresentam média de receita mensal de 2555,34 e mediana de 1683,60 reais, medidas bem acima dos clientes que deram churn. Isso sugere que o churn não está necessariamente ligado à valores altos de contrato. O churn está concentrado no grupo de clientes que possui menor valor histórico.

<img width="315" height="291" alt="image" src="https://github.com/user-attachments/assets/8f42a9de-b23c-4df3-b73d-3e45b7376f6e" />

- Churn x Engajamento: O comportamento esperado para o modelo de negócios por assinatura seria que clientes com baixo engajamento apresentem as maiores taxas de churn, por uma baixa aderência ou menor conhecimento da aplicabilidade do sistema, e clientes com médio e alto engajamento tenham menor churn. Porém a análise evidencia que as maiores taxas de churn estão presentes no grupo de clientes com score entre 0.75 e 1.375, dentro do nível médio de aderência às features do sistema. Esse grupo tem maior taxa de churn, representando 37% do total. A taxa diminui à medida que o nível de engajamento aumenta, que é o comportamento esperado. A correlação de pearson, no valor de 0,125, confirma o que os gráficos mostram, que o engajamento maior ou menor não tem relação clara com a taxa de churn nesse caso.

<img width="541" height="331" alt="image" src="https://github.com/user-attachments/assets/1a97debe-86dd-4aa0-81a5-eaf63daf9e64" />

- Meses de permanência x engajamento: Agrupei os clientes por mês de permanência e score de engajamento desse grupo de clientes. Como o gráfico de bolhas apresentou grande dispersão sem linearidade aparente, calculei o coeficiente de pearson e o valor p dessas variáveis. Existe uma correlação fraca e positiva entre elas,  à medida que o tempo de permanência do cliente aumenta, há uma ligeira tendência de aumentar o engajamento. Porém, há todos os níveis de engajamento distribuídos pelas diversos meses de permanência dos clientes, então não é uma relação causal direta e exclusiva. Não podemos afirmar que a permanência do cliente está diretamente relacionada ao engajamento com o sistema.

<img width="315" height="291" alt="image" src="https://github.com/user-attachments/assets/5ecfd9ab-d2b2-4a3b-b365-3e60e775629b" />

- Engajamento, Receita e Permanência: Para essa análise fiz um mapa de calor com coeficiente de correlação de Pearson entre as variáveis. Há uma correlação forte e positiva (0.88) entre engajamento e receita mensal, sugerindo que clientes com maior receita mensal tendem a ter um score de engajamento mais alto, ou seja, utilizam mais as funcionalidades do sistema. A correlação é moderada (0.60) entre engajamento e receita total, sugerindo que clientes mais engajados tendem a ter uma receita total acumulada maior. Entre receita total e mensal a correlação também é moderada (0.65), clientes com planos mais caros (maior ticket médio) tendem a gerar uma receita total acumulada maior, que é o esperado para modelos de assinatura. Já a correlação entre meses de permanência e receita mensal é fraca (0.24), indicando que o valor do plano não tem relação direta com o tempo de permanência.

<img width="315" height="291" alt="image" src="https://github.com/user-attachments/assets/c81485a1-c771-4752-9564-e345d6996252" />

## 4.	Produtos do projeto

- [Notebook completo no Google Colab](https://colab.research.google.com/drive/1nDUoHjKJDtCB1sTncU3YMslcgYRynDy4?usp=sharing)
- [Notebook completo no GitHub](https://github.com/giulia-tuffanelli/analise_churn_saas/blob/04484599f3a13f33db928f850f9ca3ce5ecf0f38/Software%20SA%20-%20An%C3%A1lise%20de%20churn.ipynb)
- [Apresentação corporativa dos resultados](https://github.com/giulia-tuffanelli/analise_churn_saas/blob/29e204940cf56151acc0e8efcd9e9f598e1e8e9a/An%C3%A1lise%20de%20Churn%20-%20Software%20S.A%20-%20Giulia.ppsx)

## 5. Conclusão

A maioria dos clientes são empresas novas com fundação até 10 anos, de porte pequena ou micro empresa, com até 5 funcionários em sua equipe e com média de permanência de assinatura de 2 anos e 7 meses. Em torno de 65% dos clientes fazem conciliação bancária manual com o sistema ou não fazem. Quando avaliamos a frequência de uso das features do sistema, quase um quarto da base de clientes nunca utilizou esses módulos. Esses fatores apontam um baixo grau de maturidade operacional e menor uso de automação. 
 
A taxa geral de churn é de 26,5%. No mês de abril/25 houve um total de 911 churns, uma taxa de 14,8% em relação ao total de clientes ativos na base até o início do mês. Já em maio/25 houve um aumento para 958 churns, correspondente a uma taxa de 18,5% sobre os clientes remanescentes do mês anterior. Há um aumento evidente entre esses dois meses, mas não é possível afirmar que há uma tendência a longo prazo porque a base de dados possui somente esse período.
 
O porte da empresa e número de funcionários não teve relação com o cancelamento. Já em tipo de contrato, a taxa de churn é de 42% entre clientes com contrato mensal, enquanto que anual praticamente não apresenta churn e o trimestral é bem estável. Em relação ao tipo de pagamento da assinatura, a chance de clientes que pagam boleto único cancelarem o contrato é de 45%, quase duas vezes maior que as demais categorias. Isso sugere que os clientes podem ter uma melhor organização financeira com contratos mais longos e pagamentos parcelados ou com crédito, impactando diretamente no cancelamento e inadimplência. 
 
Avaliando o ticket médio, clientes com Receita Mensal maior tem tendência ao churn. Há uma grande dispersão dos valores entre os clientes, que pode indicar que em média cancelam mais cedo o contrato ou geram menor receita ao longo do contrato. Quando olhamos para Receita Total, o churn está concentrado no grupo de clientes que possui menor valor histórico. Valores mensais de assinatura não tem relação relevante com o cancelamento. 
 
Em modelos de negócio por assinatura, é esperado que clientes com menor engajamento tenham maior tendência ao churn. Nesse projeto o resultado obtido foi diferente, em que o churn está concentrado no grupo de clientes com engajamento médio, representando 37% do total. A menor taxa de churn está concentrada no grupo com baixo engajamento, seguido pelo grupo com alto engajamento.
 
Ao correlacionar as variáveis, observa-se resultados importantes. Clientes mais engajados pagam mais por mês e geram mais receita total. A correlação mais forte é entre engajamento e receita mensal, em que clientes mais engajados pagam mais por mês e, consequentemente, geram maior receita total. Já a relação entre meses de permanência e engajamento é fraca, em que há todos os níveis de engajamento distribuídos pelas diversos meses de permanência dos clientes. Por isso, não podemos afirmar que a permanência do cliente está diretamente relacionada ao engajamento com o sistema. Essa relação fraca também é observada entre os meses de permanência e receita mensal, indicando que o valor do plano mensal não tem relação direta com o tempo de permanência. 
 
A hipótese inicial de aumento do churn foi validada, com aumento evidente entre os dois meses analisados. Entretanto, esse aumento não está ligado diretamente ao porte da empresa e à aderência ao uso do sistema pelos clientes. O engajamento não é um bom indicador de retenção nesse caso, visto que clientes podem pagar mais e serem engajados, mas não necessariamente permanecerem mais com a assinatura. 
 
Portanto, a retenção dos clientes e menor churn estão mais relacionados ao tipo de contrato e forma de pagamento. Sugerindo que essa retenção pode depender de outros fatores como valor percebido do produto, previsibilidade financeira da empresa do cliente, fluxo de caixa, suporte técnico e efeitos da concorrência, por exemplo. O acompanhamento contínuo desses indicadores é fundamental para antecipar o risco de churn e mapear as estratégias de negócio. 

## 6. Recomendações

Como a relação entre churn e engajamento dos clientes com o sistema não é clara, é importante investigar fatores adicionais relacionados à retenção do cliente, como mudanças no suporte técnico e atendimento aos clientes, mudanças no produto, aumento de preço, concorrência com outras empresas do ramo, entender a percepção de valor do produto pelo cliente. Além disso, sugiro algumas ações adicionais:
 
- Incentivar ações para aumentar o engajamento dos clientes nos módulos pouco usados, com objetivo de tornar o sistema mais essencial às operações e aumentar o valor percebido
- Monitorar frequentemente a taxa de churn e entender com os clientes quais fatores estão relacionados ao cancelamento
- Incentivar a migração para contratos mais longos, como trimestrais e anuais, que apresentam maior estabilidade
- Incentivar modalidades de pagamento parcelado ou com crédito para diluir a cobrança, que pode ser relevante para empresas de pequeno porte e com menor estabilidade financeira
