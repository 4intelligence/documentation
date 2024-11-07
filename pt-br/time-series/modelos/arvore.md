# Modelos de Árvore

Os Modelos de Árvore são um tipo de modelo de aprendizado de máquina que faz previsões com base em uma série de decisões, cada uma relacionada a uma variável específica do conjunto de dados. Eles são intuitivos, fáceis de interpretar e podem lidar com uma variedade de tipos de dados, tornando-os uma ferramenta valiosa para muitos problemas de modelagem de dados.

Os modelos de árvore têm uma característica importante que afeta diretamente sua usabilidade em modelagem de séries de tempo: eles não conseguem prever valores fora do alcance dos dados da amostra original. Isso ocorre porque um modelo de árvore toma decisões com base em regras derivadas dos dados de treinamento. Portanto, ele não é capaz de extrapolar ou prever um resultado que esteja além dos limites mínimos e máximos observados em seus dados de treinamento.

Para assegurar que as modelagens sejam precisas quando lidamos com séries temporais, nossa plataforma adota uma abordagem de dois passos. Primeiro, a tendência é identificada e modelada. Em seguida, o resíduo - a diferença entre a tendência e os dados originais - é modelado usando um modelo de árvore. Este método permite que a plataforma aproveite a capacidade de captura de padrões dos modelos de árvore, ao mesmo tempo em que considera a tendência subjacente na série temporal. Isso é particularmente útil para prever valores futuros com maior precisão, uma vez que, como mencionado anteriormente, os modelos de árvore não são capazes de extrapolar além dos limites dos dados de treinamento.

Abaixo descrevemos as principais características de cada um dos passos de modelagem:

## Primeiro Passo: tratar e modelar tendência

No primeiro passo de nossa abordagem, começamos identificando as séries que não apresentam estacionariedade. Este processo é realizado para cada uma das variáveis do conjunto de dados.  Quando identificamos variáveis que são não estacionárias, a tendência é extraída utilizando o modelo STL, que será reintegrada os resultados finais após o segundo passo do processo de modelagem.

Se a variável resposta foi submetida ao processo de extração de tendência, torna-se necessário projetar essa tendência. Esta projeção é realizada utilizando uma combinação de um modelo linear e um modelo ARIMA univariado. Foram realizados diversos testes com dados reais e sintéticos até que chegassemos na combinação de modelos proposta. 

## Segundo Passo: modelar a série usando o modelo de árvore

No segundo passo de nossa abordagem de modelagem, nos voltamos para o resíduo das séries das quais a tendência foi removida no primeiro passo. Este resíduo representa a diferença entre a série original e a tendência que extraímos. Ele captura as variações e padrões nos dados que a tendência não pode explicar. Para modelar este resíduo, empregamos uma variedade de modelos de árvore, incluindo Gradient Boosting, XGBoost, LightGBM e Random Forest. Suas principais características e diferenças são destacadas abaixo. 

### Gradient Boosting

Gradient Boosting é um algoritmo de aprendizado de máquina que utiliza a ideia de boosting, uma técnica que se baseia na ideia de criar um modelo preditivo forte a partir de vários modelos fracos. O Gradient Boosting constrói modelos de árvore de decisão sequencialmente, onde cada árvore é construída para corrigir os erros cometidos pela árvore anterior.

### XGBoost

XGBoost, ou Extreme Gradient Boosting, é uma implementação otimizada do Gradient Boosting. Ele é projetado para ser altamente eficiente, flexível e portátil. O XGBoost não apenas implementa o algoritmo de Gradient Boosting, mas também permite a regularização, que é um método para prevenir o sobreajuste, tornando-o mais robusto.

### LightGBM

LightGBM, ou Light Gradient Boosting Machine, é um algoritmo de boosting baseado em árvore desenvolvido pela Microsoft. É conhecido por sua eficiência e velocidade. O LightGBM difere de outros algoritmos de boosting ao crescer a árvore de decisão verticalmente (folha-sábia) em vez de horizontalmente (nível-sábio), o que pode resultar em uma melhor otimização de perdas e aumento do desempenho.

### Random Forest
 
Random Forest é um algoritmo de aprendizado de máquina que constrói uma floresta de árvores de decisão não correlacionadas durante a fase de treinamento. As previsões são então feitas pegando a média (para regressão) ou a moda (para classificação) das previsões de todas as árvores na floresta. O Random Forest é particularmente eficaz para lidar com dados de alta dimensionalidade e evita o sobreajuste, que é uma limitação comum de árvores de decisão individuais.