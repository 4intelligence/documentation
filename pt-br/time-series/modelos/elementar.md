# Elementar

Atualmente, existem três tipos distintos de modelos elementares: o STL, o modelo ARIMA com variáveis indicadoras sazonais aditivas (ARIMA_SEASD) e o modelo Arima Sazonal (ARIMA_SEASM), que trata a sazonalidade de forma multiplicativa. Os modelos elementares recebem esse nome porque incluem apenas informações sobre a própria variável de resposta, sem a inclusão de quaisquer variáveis explicativas, exceto aquelas que consideram sazonalidade ou observações atípicas.

### ARIMA_SEASD

Os modelos ARIMA com variáveis indicadoras sazonais aditivas e de observações atípicas têm a mesma estrutura descrita na seção ARIMA, no qual as variáveis indicadoras são incluídas no modelo como variáveis explicativas. As variáveis indicadoras sazonais são incluídas considerando a frequência dos dados. Por exemplo, para um conjunto de dados mensal, são incluídas variáveis que indicam o mês do ano; para bimestral, são incluídas variáveis indicadoras do bimestre. Para um conjunto de dados diário, por outro lado, são adicionados dois conjuntos de variáveis indicadoras: aqueles que consideram o dia da semana e outros para o mês do ano. A ordem ótima dos termos ARIMA é identificada considerando todo o conjunto de dados de modelagem.

### ARIMA_SEASM

O modelo ARIMA Sazonal considera a sazonalidade dentro de sua ordem sazonal de ARIMA e pode incluir variáveis indicadoras de observações atípicas, se forem identificadas. Diferentemente de um modelo ARIMA regular, um modelo ARIMA Sazonal é da forma _ARIMA(p,d,q)x(P,D,Q)m_, em que _P_, _D_ e _Q_ são os termos auto-regressivos, de diferenciação e de média móvel sazonais, e _m_ indica a frequência dos dados. Este modelo trata a sazonalidade considerando que ela é multiplicativa, ou seja, os padrões sazonais mudam ao longo do tempo, enquanto a sazonalidade aditiva (modelada através do ARIMA_SEASD) pressupõe que os padrões permanecem constantes.

### STL

A decomposição sazonal e de tendência usando Loess (STL) é um método para estimar padrões na variável de resposta. Uma decomposição de série temporal consiste em separar os efeitos nos dados em uma tendência, sazonalidade e um erro. Isso possibilita ver claramente cada um desses efeitos individualmente e identificar aspectos importantes dos dados. A decomposição STL estima esses componentes de forma iterativa, usando a interpolação de Loess para suavizar a estimativa dos componentes sazonais e encontrar a estimativa de tendência.