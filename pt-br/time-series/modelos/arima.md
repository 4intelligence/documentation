# ARIMA

ARIMA é um acrônimo para modelo de Média Móvel Integrada Autoregressiva. Esse modelo permite a influência dos valores passados das variáveis dependentes nos valores presentes, também conhecida como autocorrelação. Portanto, ele é aplicado para estimar modelos dinâmicos. Podemos dividir o ARIMA em três partes: i) parte autoregressiva (AR); ii) parte de média móvel (MA); e iii) parte de integração. Geralmente, o ARIMA(p,d,q) pode ser expresso na função abaixo:

![](https://raw.githubusercontent.com/4intelligence/documentation/main/pt-br/time-series/modelagem/img/form_arima1.png)

em que _p_ é a ordem da parte autoregressiva (AR), _q_ é a ordem da parte de média móvel (MA), _d_ é a ordem de integração da série, ou seja, o número de diferenças necessárias para tornar a série temporal estacionária, e _e_ são os parâmetros do modelo. O intercepto, representado por _c_ na equação, também é chamado de "drift" (desvio) neste modelo. A parte de média móvel (MA) representa a autocorrelação nos resíduos, que, se não for controlada, pode enviesar a estimativa dos parâmetros. O ARIMA também pode incluir variáveis exógenas para aumentar o poder de previsão. Quando isso acontece, o ARIMA é conhecido como ARIMAX.

Para realizar a estimativa e a previsão, o motor de modelagem aplica um modelo de regressão com erros ARMA que estima as duas equações:

![](https://raw.githubusercontent.com/4intelligence/documentation/main/pt-br/time-series/modelagem/img/form_arima2.png)

Na primeira equação, são estimados os parâmetros das variáveis exógenas (impactos) e, na segunda equação, é controlada a autocorrelação dos resíduos, que pode prejudicar a estimativa dos erros padrão dos parâmetros. Ambos os métodos, ARIMA e regressão com erros ARMA, são semelhantes e não há diferença em sua capacidade de previsão, mas o último tem a vantagem de manter a interpretação dos parâmetros estimados, como em regressões comuns (não dinâmicas).

