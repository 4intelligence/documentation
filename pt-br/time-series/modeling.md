 # Modeling types

## ARIMA  

ARIMA é um acrônimo para Autoregressive Integrated Moving Average model. Este modelo permite a influência dos valores passados das variáveis dependentes nos valores presentes, também chamada de autocorrelação. Assim, é aplicado para estimar modelos dinâmicos. Podemos dividir o ARIMA em três partes: i) a parte autorregressiva (AR); ii) a média móvel (MA) e; iii) parte de integração. Geralmente, o ARIMA(p,d,q) pode ser expresso como a função abaixo:

*adicionar fórmula*

em que, p é a ordem da parte AR, q é a ordem da parte MA, d é a ordem de integração da série, ou seja, o número de diferenças necessárias para tornar a série temporal estacionária. A interceptação, representada por c na equação, também é chamada de deriva neste modelo. A MA representa a autocorrelação nos resíduos, que, se não for controlada, pode enviesar a estimação dos parâmetros. O ARIMA também pode incluir variáveis exógenas para aumentar o poder de previsão. Nesse caso, o ARIMA é conhecido como ARIMAX.

Para realizar a estimativa e previsão, o FaaS aplica o modelo de regressão com erros ARMA que estima as duas equações:

* adicionar fórmula *

Na primeira equação, estima os parâmetros das variáveis exógenas (impactos) e, na segunda, controla a autocorrelação dos resíduos, que podem prejudicar a estimação dos erros padrão dos parâmetros. Ambos os métodos (ARIMA e regressão com erros ARMA) são semelhantes e não há diferença em sua capacidade de previsão, mas o último tem a vantagem de manter a interpretação dos parâmetros estimados como nas regressões comuns (não dinâmicas).

## Forecast Combination  

Conforme definido pelo nome, os métodos de combinação de previsão combinam valores previstos por diferentes modelos, seja linearmente ou usando técnicas mais sofisticadas, para gerar novas previsões. Atualmente, é testada a combinação dos 10 melhores modelos de acordo com o critério de precisão escolhido pelo usuário (como “MAPE”), de modo que os números de modelo 1 e 2 são combinados e as métricas são calculadas, depois 1, 2 e 3 são combinados , e assim por diante. Todos os métodos são executados para cada combinação. Para cada técnica é escolhida a combinação com o melhor critério escolhido pelo usuário.

Para simplificar a explicação dos métodos utilizados, eles foram divididos em 3 blocos: A) Métodos Simples; B) Métodos de Regressão; C) Abordagem de autovetores;

A) Métodos Simples

1) Bates/Granger (1969) - comb_BG

Idéia principal: ponderar as previsões usando o inverso da previsão do erro quadrático médio (média da diferença quadrada entre os valores previstos e reais).

2) Combinação de previsão de classificação inversa - comb_invW

Idéia principal: Classifique o modelo com a menor predição quadrática média como 1, a segunda mais baixa como 2, etc. Em seguida, pegue a classificação inversa e verifique seu peso dividindo a classificação inversa pela soma das classificações inversas.

3) Combinação de previsão mediana - comb_MED

Ideia principal: Use a mediana das previsões em cada ponto no tempo.

4) Combinação Simples de Previsão de Média - comb_SA

Ideia principal: Use a média das previsões em cada ponto no tempo.

5) Combinação de Previsão de Média Aparada - comb_TA

Ideia principal: Corte um número desejado de modelos com base na classificação (MAE, MAPE ou RMSE) e obtenha a previsão média. Atualmente, o RMSE é usado.

6) Combinação de Previsão de Média Winsorizada - comb_WA

Ideia principal: Use a média Winsorizada das previsões em cada ponto no tempo. A ideia da média Winsorizada é substituir os valores maiores e menores por suas observações mais próximas.

7) Newbold/Granger (1974) Combinação de previsão - comb_NG

Ideia principal: como “4) Combinação de previsão de autovetores padrão”, mas impondo a restrição linear e'w = 1, onde 'e' é um vetor de uns.

B) Métodos de regressão

1) Combinação de Previsão de Mínimos Quadrados Ordinários - comb_OLS

Ideia principal: O método OLS executa um modelo linear simples com intercepto usando como regressores as previsões e como variável dependente os valores reais.

2) Combinação de Previsão de Mínimos Quadrados Restritos - comb_CLS

Ideia principal: Funciona como combinações de previsão de Mínimos Quadrados Ordinários, mas adiciona as restrições: (1) Os pesos devem ser não negativos; (2) Os pesos devem somar um;

3) Combinação de previsão de menor desvio absoluto - comb_LAD

Ideia principal: Funciona de forma semelhante a uma combinação via Mínimos Quadrados Ordinários, mas minimiza o valor absoluto dos erros em vez dos erros quadrados. Este método é mais robusto para outliers, uma vez que a magnitude da penalização é menor do que os erros quadrados.

C) Abordagem de autovetores

1) Combinação padrão de previsão de autovetores - comb_EIG1

Ideia principal: Minimizar o erro de predição quadrático médio (v) através de uma combinação linear (w'*((v*v')*w, onde w é o vetor de peso). Se a restrição imposta for do formato w'w = 1, a solução é encontrar o menor autovetor, que por sua vez está associado ao menor autovalor.

2) Combinação de Previsão de Autovetores Correção de Viés - comb_EIG2

Ideia principal: Muito semelhante a 1), mas agora cada vetor de erro de previsão é subtraído de sua média, eliminando possíveis vieses.

3) Combinação de previsão de autovetores aparados - comb_EIG3

Ideia principal: Muito semelhante a 1), mas pré-seleciona os melhores modelos que entrarão em combinação de acordo com um critério de otimização: MAE, MAPE ou RMSE e mantém o número de modelos definidos pelo algoritmo de otimização embutido. Atualmente, o RMSE é usado.

4) Combinação de Previsão de Autovetores Corrigidos com Viés Aparado - comb_EIG4

Ideia principal: Combina 2 e 3.


## Elementary  

Atualmente existem três tipos distintos de modelos elementares, o STL, modelo Arima com variáveis indicadoras aditivas sazonais (ARIMA_SEASD) e modelo Arima Sazonal (ARIMA_SEASM), que trata a sazonalidade de forma multiplicativa. Os modelos elementares recebem esse nome porque incluem apenas informações sobre a própria variável resposta, sem a inclusão de nenhuma variável explicativa, exceto aquelas que respondem por sazonalidade ou observações outliers.

ARIMA_SEASD

Os modelos Arima com variáveis indicadoras aditivas sazonais e outliers têm a mesma estrutura descrita na seção Arima, onde as variáveis indicadoras são incluídas no modelo como variáveis explicativas. As variáveis indicadoras sazonais são incluídas considerando a frequência dos dados, por exemplo, para dataset mensal, são incluídas variáveis que indicam o mês do ano; para bimestre, são incluídas as variáveis indicadoras do bimestre. Por outro lado, para o conjunto de dados diários, são adicionados dois conjuntos de variáveis indicadoras, aquelas que representam o dia da semana e outro o mês do ano. A ordem ótima dos termos Arima é identificada considerando todo o conjunto de dados de modelagem.

ARIMA_SEASM

O modelo Sazonal Arima considera a sazonalidade dentro de sua ordem arima sazonal e pode incluir variáveis indicadoras atípicas, se forem identificadas. Diferentemente de um modelo Arima regular, um modelo Arima Sazonal é da forma ARIMA(p,d,q)x(P,D,Q)m, onde P, D e Q são as médias auto-regressivas, diferenciais e móveis sazonais termos, e m indica a frequência dos dados. Este modelo trata a sazonalidade considerando que ela é multiplicativa, ou seja. os padrões sazonais mudam ao longo do tempo, enquanto a sazonalidade aditiva (modelada por ARIMA_SEASD) assume que os padrões permanecem constantes.

STL

A decomposição sazonal e de tendência usando Loess (STL) é um método para estimar padrões dentro da variável de resposta. Uma decomposição de série temporal consiste em separar os efeitos nos dados em tendência, sazonalidade e erro, assim é possível ver com clareza cada um desses efeitos individualmente e identificar aspectos importantes dos dados. A Decomposição SLT estima esses componentes iterativamente, usando a interpolação de Loess para suavizar a estimativa dos componentes sazonais e encontrar a estimativa de tendência.

## Regularized Regression 

As regressões regularizadas são métodos projetados para encolher coeficientes em direção a zero, penalizando coeficientes maiores na função de perda. A ideia é que esse tipo de modelo generalize melhor, já que cada regressor contribui um pouco com o resultado, obtendo resultados “mais suaves”. As regularizações podem ser do tipo L1 (Lasso) ou L2 (Ridge), com o ElasticNet combinando ambos.

Os tipos L1 e L2 impõem uma penalidade na função de perda, que é proporcional ao tamanho dos coeficientes absolutos para L1 e é quadrática para L2. O modelo Lasso representa a regularização L1 e L2 Ridge, enquanto Lasso pode reduzir os coeficientes para zero, Ridge pode reduzi-los para zero, mas nunca alcançá-lo. Existe um parâmetro, lambda, que controla o grau dessa penalidade, se for ao infinito, os coeficientes se movem em direção ao ElasticNet combina L1 e L2 e tem um parâmetro adicional, “alpha”, que é uma espécie de peso dado para L1, com seu peso “contraparte” proporcional a 1 - alfa para L2.

## Random Forest 

Florestas aleatórias, ou florestas de decisão aleatórias, é um modelo proposto por Ho em 1995 baseado em árvores de decisão. Ele visa reduzir o problema da árvore de decisão de não generalizar bem para novos dados (overfitting), fazendo um conjunto de várias árvores usando um método chamado bagging (agregação de bootstrap).

O método funciona extraindo subamostras de recursos do conjunto de dados original e treinando diferentes árvores com essas subamostras. Os resultados de cada árvore são então calculados para problemas de regressão (que é o caso da previsão de séries temporais) ou o voto da maioria para classificação.

Por ser um modelo não paramétrico, o Random Forest não possui parâmetros, mas sim hiperparâmetros, dos quais testamos dois:

- mtry: número de preditores amostrados para divisão em cada nó;
- ntree: Número de árvores a crescer.