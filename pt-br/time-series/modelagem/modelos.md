# Tipos de Modelos

Nessa seção, vamos abordar os tipos de modelos disponíveis e suas principais informações.

### ARIMA 

ARIMA é um acrônimo para modelo de Média Móvel Integrada Autoregressiva. Esse modelo permite a influência dos valores passados das variáveis dependentes nos valores presentes, também conhecida como autocorrelação. Portanto, ele é aplicado para estimar modelos dinâmicos. Podemos dividir o ARIMA em três partes: i) parte autoregressiva (AR); ii) parte de média móvel (MA); e iii) parte de integração. Geralmente, o ARIMA(p,d,q) pode ser expresso na função abaixo: 

![](https://raw.githubusercontent.com/4intelligence/documentation/main/pt-br/time-series/modelagem/img/form_arima1.png)

onde p é a ordem da parte autoregressiva (AR), q é a ordem da parte de média móvel (MA), d é a ordem de integração da série, ou seja, o número de diferenças necessárias para tornar a série temporal estacionária, e e são os parâmetros do modelo. O intercepto, representado por c na equação, também é chamado de "drift" (desvio) neste modelo. A parte de média móvel (MA) representa a autocorrelação nos resíduos, que, se não for controlada, pode enviesar a estimativa dos parâmetros. O ARIMA também pode incluir variáveis exógenas para aumentar o poder de previsão. Quando isso acontece, o ARIMA é conhecido como ARIMAX. 

Para realizar a estimativa e a previsão, o motor de modelagem aplica um modelo de regressão com erros ARMA que estima as duas equações:  

![](https://raw.githubusercontent.com/4intelligence/documentation/main/pt-br/time-series/modelagem/img/form_arima2.png)

Na primeira equação, são estimados os parâmetros das variáveis exógenas (impactos) e, na segunda equação, é controlada a autocorrelação dos resíduos, que pode prejudicar a estimativa dos erros padrão dos parâmetros. Ambos os métodos, ARIMA e regressão com erros ARMA, são semelhantes e não há diferença em sua capacidade de previsão, mas o último tem a vantagem de manter a interpretação dos parâmetros estimados, como em regressões comuns (não dinâmicas). 

### Combinação de Modelos

Conforme o nome sugere, os métodos de combinação de previsões combinam valores previstos por diferentes modelos, seja linearmente ou usando técnicas mais sofisticadas, para gerar novas previsões. Atualmente, é testada a combinação dos 10 melhores modelos de acordo com o critério de acurácia escolhido pelo usuário (como o "MAPE"), de modo que os modelos 1 e 2 sejam combinados e métricas sejam calculadas, depois 1, 2 e 3 são combinados, e assim por diante. Todos os métodos são executados para cada combinação. Para cada técnica, é escolhida a combinação com o melhor critério escolhido pelo usuário. 

Para simplificar a explicação dos métodos usados, eles foram divididos em 3 blocos: A) Métodos Simples; B) Métodos de Regressão; C) Abordagem de Autovetores; 

**A) Métodos Simples** 

- Bates/Granger (1969) - comb_BG 

Ideia principal: ponderar as previsões usando o inverso do erro médio quadrado da previsão (média da diferença ao quadrado entre a previsão e os valores reais). 

- Combinação de Previsão de Classificação Inversa - comb_invW 

Ideia principal: Classificar o modelo com a menor previsão de erro quadrado médio como 1, o segundo menor como 2, etc. Em seguida, pegar a classificação inversa e verificar seu peso dividindo a classificação inversa pela soma das classificações inversas. 

- Combinação de Previsão Mediana - comb_MED 

Ideia principal: Usar a mediana das previsões em cada ponto no tempo. 

- Combinação de Previsão Média Simples - comb_SA 

Ideia principal: Usar a média das previsões em cada ponto no tempo. 

- Combinação de Previsão Média Aparada - comb_TA 

Ideia principal: Aparar um número desejado de modelos com base na classificação (MAE, MAPE ou RMSE) e tirar a média da previsão. Atualmente, é usado o RMSE. 

- Combinação de Previsão Média Winsorizada - comb_WA 

Ideia principal: Usar a média winsorizada das previsões em cada ponto no tempo. A ideia da média winsorizada é substituir os valores mais altos e mais baixos pelas observações mais próximas. 

- Combinação de Previsão Newbold/Granger (1974) - comb_NG 

Ideia principal: Semelhante a "4) Combinação de Previsão Padrão de Autovetor", mas impondo a restrição linear e'w = 1, onde 'e' é um vetor de uns. 

**B) Métodos de Regressão** 

- Combinação de Previsão de Mínimos Quadrados Ordinários - comb_OLS 

Ideia principal: O método OLS executa um modelo linear simples com interceptação usando as previsões como regressores e os valores reais como variável dependente. 

- Combinação de Previsão de Mínimos Quadrados Restritos - comb_CLS 

Ideia principal: Funciona como combinações de previsão de mínimos quadrados ordinários, mas adiciona restrições: (1) os pesos devem ser não negativos; (2) os pesos devem somar um; 

- Combinação de Previsão de Desvio Absoluto Mínimo - comb_LAD 

Ideia principal: Funciona de forma semelhante a uma combinação por meio de mínimos quadrados ordinários, mas minimiza o valor absoluto dos erros em vez de erros ao quadrado. Este método é mais robusto a valores atípicos, pois a magnitude da penalização é menor do que erros ao quadrado. 

**C) Abordagem de Autovetores**

- Combinação de Previsão Padrão de Autovetor - comb_EIG1 

Ideia principal: Minimizar o erro médio quadrado de previsão (v) por meio de uma combinação linear (w'((vv’)*w, onde w é o vetor de peso). Se a restrição imposta for do formato w'w = 1, a solução é encontrar o menor autovetor, que por sua vez está associado ao menor autovalor. 

- Combinação de Previsão de Autovetor com Correção de Viés - comb_EIG2 

Ideia principal: Muito semelhante a 1), mas agora cada vetor de erro de previsão é subtraído de sua média, eliminando possíveis vieses. 

- Combinação de Previsão de Autovetor Aparada - comb_EIG3 

Ideia principal: Muito semelhante a 1), mas pré-seleciona os melhores modelos que entrarão na combinação de acordo com um critério de otimização: MAE, MAPE ou RMSE, e mantém o número de modelos definidos pelo algoritmo de otimização incorporado. Atualmente, é usado o RMSE. 

- Combinação de Previsão de Autovetor com Viés Aparado - comb_EIG4 

Ideia principal: Combina 2 e 3. 

### Elementary

Atualmente, existem três tipos distintos de modelos elementares: o STL, o modelo ARIMA com variáveis indicadoras sazonais aditivas (ARIMA_SEASD) e o modelo Arima Sazonal (ARIMA_SEASM), que trata a sazonalidade de forma multiplicativa. Os modelos elementares recebem esse nome porque incluem apenas informações sobre a própria variável de resposta, sem a inclusão de quaisquer variáveis explicativas, exceto aquelas que consideram sazonalidade ou observações atípicas. 

**ARIMA_SEASD** 

Os modelos ARIMA com variáveis indicadoras sazonais aditivas e de observações atípicas têm a mesma estrutura descrita na seção ARIMA, onde as variáveis indicadoras são incluídas no modelo como variáveis explicativas. As variáveis indicadoras sazonais são incluídas considerando a frequência dos dados. Por exemplo, para um conjunto de dados mensal, são incluídas variáveis que indicam o mês do ano; para bimestral, são incluídas variáveis indicadoras do bimestre. Para um conjunto de dados diário, por outro lado, são adicionados dois conjuntos de variáveis indicadoras: aqueles que consideram o dia da semana e outros para o mês do ano. A ordem ótima dos termos ARIMA é identificada considerando todo o conjunto de dados de modelagem. 

**ARIMA_SEASM** 

O modelo Arima Sazonal considera a sazonalidade dentro de sua ordem sazonal de arima e pode incluir variáveis indicadoras de observações atípicas, se forem identificadas. Diferentemente de um modelo ARIMA regular, um modelo Arima Sazonal é da forma ARIMA(p,d,q)x(P,D,Q)m, onde P, D e Q são os termos auto-regressivos, de diferenciação e de média móvel sazonais, e m indica a frequência dos dados. Este modelo trata a sazonalidade considerando que ela é multiplicativa, ou seja, os padrões sazonais mudam ao longo do tempo, enquanto a sazonalidade aditiva (modelada através do ARIMA_SEASD) pressupõe que os padrões permanecem constantes. 

**STL** 

A decomposição sazonal e de tendência usando Loess (STL) é um método para estimar padrões na variável de resposta. Uma decomposição de série temporal consiste em separar os efeitos nos dados em uma tendência, sazonalidade e um erro. Isso possibilita ver claramente cada um desses efeitos individualmente e identificar aspectos importantes dos dados. A decomposição STL estima esses componentes de forma iterativa, usando a interpolação de Loess para suavizar a estimativa dos componentes sazonais e encontrar a estimativa de tendência. 

### Regressão Regularizada

As regressões regularizadas são métodos projetados para reduzir os coeficientes em direção a zero, penalizando coeficientes maiores na função de perda. A ideia é que esse tipo de modelo generalize melhor, uma vez que cada regressor contribui um pouco para o resultado, obtendo resultados mais "suaves". As regularizações podem ser do tipo L1 (Lasso) ou L2 (Ridge), com o ElasticNet combinando ambos. 

Os tipos L1 e L2 impõem uma penalização na função de perda, que é proporcional ao tamanho dos coeficientes absolutos para L1 e quadrático para L2. O modelo Lasso representa a regularização L1 e o Ridge L2, sendo que o Lasso pode reduzir os coeficientes a zero, e o Ridge pode reduzi-los em direção a zero, mas nunca alcançando-o completamente. Há um parâmetro, lambda, que controla o grau dessa penalidade; se ele tender ao infinito, os coeficientes se moverão em direção a zero. 

O ElasticNet combina L1 e L2 e possui um parâmetro adicional, "alpha", que é uma espécie de peso dado para L1, com seu peso "correspondente" proporcional a 1 - alpha para L2. 

### Random Forest

Random Forests, ou florestas de decisão aleatória, é um modelo proposto por Ho em 1995 com base em árvores de decisão. Ele visa resolver o problema de árvores de decisão que não generalizam bem para novos dados (*overfitting*), criando um conjunto de várias árvores usando um método chamado bagging (agregação *bootstrap*). 

O método funciona extraindo subamostras de recursos do conjunto de dados original e treinando diferentes árvores com essas subamostras. Os resultados de cada árvore são então combinados para problemas de regressão (como é o caso para previsão de séries temporais) ou obtém-se a maioria dos votos para classificação. 

Sendo um modelo não paramétrico, o Random Forest não possui parâmetros, mas sim hiperparâmetros, dentre os quais testamos dois: 

- mtry: número de preditores amostrados para divisão em cada nó; 
- ntree: número de árvores a serem geradas. 
