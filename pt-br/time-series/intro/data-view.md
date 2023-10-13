# Visualização de dados 

## Dados Históricos

É possível analisar os dados da sua variável dependente, na visão do dado em nível original e nas transformações disponíveis.

**Original (orig)**

Corresponde à série temporal do usuário sem modificações de qualquer tipo. 

**Ajustado sazonalmente (sa)** 

Corresponde à série temporal do usuário após ter sido ajustada sazonalmente, o que significa que os efeitos sazonais foram removidos da série temporal. Por exemplo, se durante todos os meses de dezembro houver um aumento usual no valor da série temporal em comparação com o resto do ano, não haverá diferença perceptível no valor da série temporal. 

**MoM**

Abreviação de Month over Month (mês a mês), corresponde ao aumento ou diminuição percentual do valor em comparação com a mesma série temporal no mesmo dia do último mês. Por exemplo, em 1º de fevereiro de 2003 tivemos 80, e em 1º de janeiro de 2003 tivemos 88. Isso significa um aumento percentual de (88/80 - 1) = 10,0%. 

**YoY**

Abreviação de Year over Year (ano a ano), corresponde ao aumento ou diminuição percentual do valor em comparação com a mesma série temporal no mesmo dia do mesmo mês do ano anterior. Por exemplo, se em 1º de janeiro de 2004 tivemos 76,8, e em 1º de janeiro de 2003 tivemos 74. Isso significa um aumento percentual de (76,8/74,0 - 1) = 3,78%. 

**Acumulado nos últimos 12 meses (acum12m)**

Corresponde ao valor médio da série temporal durante o último ano em comparação com o valor médio da série temporal do ano anterior, obtendo-se o aumento ou diminuição percentual. Por exemplo, se estamos em 1º de janeiro de 2020, vamos pegar o valor médio de 1º de janeiro de 2019 a 1º de janeiro de 2020, dividir pelo valor médio de 1º de janeiro de 2018 a 1º de janeiro de 2019 e, em seguida, subtrair 1. 

**Diferença (diff)**

Corresponde ao aumento ou diminuição absoluto no valor da série temporal após cada período. Se a série temporal for diária, então a diferença absoluta diária da série temporal será calculada. Por exemplo, se em 1º de janeiro de 2004 tivemos 76,8, e em 1º de janeiro de 2003 tivemos 74. Isso significa um aumento absoluto de (76,8 - 74,0) = 2,8. 

## Correlação 

O coeficiente de correlação (ρ) mede a relação ou associação que existe entre duas variáveis. Usamos o coeficiente de correlação de Pearson, que mede a relação linear entre as variáveis de interesse, resultando em um valor entre -1 e 1. A equação para calcular o coeficiente de correlação de Pearson é apresentada abaixo: 

<img title="Janelas do cross validation" alt="Cross Validation" src="pt-br/time-series/start/images/dataview.1.png">

Se um valor de (ρ) for maior que 0, isso indica que existe uma correlação linear positiva ou relação entre as duas variáveis de interesse, ou seja, se a variável X aumenta, a variável Y também aumentará. Quando (ρ) assume um valor menor que 0, temos a interpretação oposta, ou seja, há uma correlação ou relação linear negativa entre as variáveis de interesse; se X aumenta, Y diminuirá. Quando o valor de (ρ) é igual a 0, isso indica que não há relação linear entre as variáveis. 

Uma maneira prática de visualizar o coeficiente de correlação é por meio da matriz de correlação, na qual cada coluna e linha da matriz representa uma variável, e a entrada (i,j) da matriz corresponde ao valor do coeficiente de correlação entre as variáveis (i,j). 

## Potenciais valores atípicos: 

**Método ARIMA**

A detecção de valores atípicos usando ARIMA funciona analisando os resíduos de um modelo ARIMA univariado com detecção automática da ordem AR e MA. Cada resíduo que fica fora da média mais/menos 2,5 desvios padrão é considerado um valor atípico. 

**Método SARIMA** 

A detecção de valores atípicos usando SARIMA funciona analisando os resíduos de um modelo SARIMA univariado com detecção automática dos componentes sazonais, AR e MA. Cada resíduo que fica fora da média mais/menos 2,5 desvios padrão é considerado um valor atípico. 

**Método Cook's** 

A Distância de Cook mede o efeito de cada observação no modelo de regressão linear, removendo uma observação por vez e avaliando seu efeito nos valores previstos. Observações com uma grande Distância de Cook indicam que tal ponto influencia os valores ajustados e, portanto, são valores atípicos em potencial. 

## Decomposição STL (Tendência, Sazonal, Restante) 

A seção de Decomposição STL mostra os componentes individuais da variável dependente. Os componentes são extraídos da série temporal original usando a abordagem "Decomposição Sazonal-Tendência usando Loess" (STL). 

No primeiro gráfico, é mostrada a tendência da variável, que descreve a direção dos dados, se está crescendo (tendência positiva), diminuindo (tendência negativa) ou estável. 

O segundo gráfico apresenta o componente sazonal da variável. Esse componente mostra padrões temporais recorrentes nos dados, geralmente em forma de oscilação. 

Por fim, o terceiro componente é o restante. Quando a sazonalidade e a tendência são subtraídas da série temporal original, os valores restantes são o componente de restante. É útil para analisar quanto ruído está presente na série temporal. 

Athanasopoulos, G., Hyndman, R. J. (2018). Previsão: Princípios e Prática. 

## Importância da Variável (%incMSE)  

A importância da variável, também conhecida como importância da característica, é calculada usando um modelo de Floresta Aleatória. Primeiramente, o Erro Quadrado Médio (MSE) do modelo é calculado e, em seguida, para cada variável, seus valores são substituídos por valores atribuídos aleatoriamente (dentro dos valores no conjunto de dados) e a diferença do MSE original é calculada. Essas diferenças no MSE são então classificadas e são as importâncias das variáveis exibidas pelo método %incMSE (aumento percentual no Erro Quadrado Médio). 

Uma variável mais importante terá um valor mais alto, o que significa que mudar o valor terá o maior impacto no desempenho do modelo. 
