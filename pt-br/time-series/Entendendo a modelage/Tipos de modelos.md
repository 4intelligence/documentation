## Explorador de modelos

ARIMA - Breve Descrição (Incluindo Parâmetros) 

ARIMA é um acrônimo para modelo de Média Móvel Integrada Autoregressiva. Esse modelo permite a influência dos valores passados das variáveis dependentes nos valores presentes, também conhecida como autocorrelação. Portanto, ele é aplicado para estimar modelos dinâmicos. Podemos dividir o ARIMA em três partes: i) parte autoregressiva (AR); ii) parte de média móvel (MA); e iii) parte de integração. Geralmente, o ARIMA(p,d,q) pode ser expresso na função abaixo:  

onde p é a ordem da parte autoregressiva (), q é a ordem da parte de média móvel (), d é a ordem de integração da série, ou seja, o número de diferenças necessárias para tornar a série temporal estacionária, e e são os parâmetros do modelo. O intercepto, representado por c na equação, também é chamado de "drift" (desvio) neste modelo. A parte de média móvel (MA) representa a autocorrelação nos resíduos, que, se não for controlada, pode enviesar a estimativa dos parâmetros. O ARIMA também pode incluir variáveis exógenas para aumentar o poder de previsão. Quando isso acontece, o ARIMA é conhecido como ARIMAX. 

Para realizar a estimativa e a previsão, o FaaS aplica um modelo de regressão com erros ARMA que estima as duas equações:  

Na primeira equação, são estimados os parâmetros das variáveis exógenas (impactos) e, na segunda equação, é controlada a autocorrelação dos resíduos, que pode prejudicar a estimativa dos erros padrão dos parâmetros. Ambos os métodos, ARIMA e regressão com erros ARMA, são semelhantes e não há diferença em sua capacidade de previsão, mas o último tem a vantagem de manter a interpretação dos parâmetros estimados, como em regressões comuns (não dinâmicas). 

Combinação de Modelos - Breve Descrição (Incluindo Parâmetros)  

Conforme o nome sugere, os métodos de combinação de previsões combinam valores previstos por diferentes modelos, seja linearmente ou usando técnicas mais sofisticadas, para gerar novas previsões. Atualmente, é testada a combinação dos 10 melhores modelos de acordo com o critério de acurácia escolhido pelo usuário (como o "MAPE"), de modo que os modelos 1 e 2 sejam combinados e métricas sejam calculadas, depois 1, 2 e 3 são combinados, e assim por diante. Todos os métodos são executados para cada combinação. Para cada técnica, é escolhida a combinação com o melhor critério escolhido pelo usuário. 

Para simplificar a explicação dos métodos usados, eles foram divididos em 3 blocos: A) Métodos Simples; B) Métodos de Regressão; C) Abordagem de Autovetores; 

A) Métodos Simples 

Bates/Granger (1969) - comb_BG Ideia principal: ponderar as previsões usando o inverso do erro médio quadrado da previsão (média da diferença ao quadrado entre a previsão e os valores reais). 

Combinação de Previsão de Classificação Inversa - comb_invW Ideia principal: Classificar o modelo com a menor previsão de erro quadrado médio como 1, o segundo menor como 2, etc. Em seguida, pegar a classificação inversa e verificar seu peso dividindo a classificação inversa pela soma das classificações inversas. 

Combinação de Previsão Mediana - comb_MED Ideia principal: Usar a mediana das previsões em cada ponto no tempo. 

Combinação de Previsão Média Simples - comb_SA Ideia principal: Usar a média das previsões em cada ponto no tempo. 

Combinação de Previsão Média Aparada - comb_TA Ideia principal: Aparar um número desejado de modelos com base na classificação (MAE, MAPE ou RMSE) e tirar a média da previsão. Atualmente, é usado o RMSE. 

Combinação de Previsão Média Winsorizada - comb_WA Ideia principal: Usar a média winsorizada das previsões em cada ponto no tempo. A ideia da média winsorizada é substituir os valores mais altos e mais baixos pelas observações mais próximas. 

Combinação de Previsão Newbold/Granger (1974) - comb_NG Ideia principal: Semelhante a "4) Combinação de Previsão Padrão de Autovetor", mas impondo a restrição linear e'w = 1, onde 'e' é um vetor de uns. 

B) Métodos de Regressão 

Combinação de Previsão de Mínimos Quadrados Ordinários - comb_OLS Ideia principal: O método OLS executa um modelo linear simples com interceptação usando as previsões como regressores e os valores reais como variável dependente. 

Combinação de Previsão de Mínimos Quadrados Restritos - comb_CLS Ideia principal: Funciona como combinações de previsão de mínimos quadrados ordinários, mas adiciona restrições: (1) os pesos devem ser não negativos; (2) os pesos devem somar um; 

Combinação de Previsão de Desvio Absoluto Mínimo - comb_LAD Ideia principal: Funciona de forma semelhante a uma combinação por meio de mínimos quadrados ordinários, mas minimiza o valor absoluto dos erros em vez de erros ao quadrado. Este método é mais robusto a valores atípicos, pois a magnitude da penalização é menor do que erros ao quadrado. 

C) Abordagem de Autovetores 

Combinação de Previsão Padrão de Autovetor - comb_EIG1 Ideia principal: Minimizar o erro médio quadrado de previsão (v) por meio de uma combinação linear (w'((vv’)*w, onde w é o vetor de peso). Se a restrição imposta for do formato w'w = 1, a solução é encontrar o menor autovetor, que por sua vez está associado ao menor autovalor. 

Combinação de Previsão de Autovetor com Correção de Viés - comb_EIG2 Ideia principal: Muito semelhante a 1), mas agora cada vetor de erro de previsão é subtraído de sua média, eliminando possíveis vieses. 

Combinação de Previsão de Autovetor Aparada - comb_EIG3 Ideia principal: Muito semelhante a 1), mas pré-seleciona os melhores modelos que entrarão na combinação de acordo com um critério de otimização: MAE, MAPE ou RMSE, e mantém o número de modelos definidos pelo algoritmo de otimização incorporado. Atualmente, é usado o RMSE. 

Combinação de Previsão de Autovetor com Viés Aparado - comb_EIG4 Ideia principal: Combina 2 e 3. 

 

Elementary - Breve Descrição (Incluindo Parâmetros)  

Atualmente, existem três tipos distintos de modelos elementares: o STL, o modelo ARIMA com variáveis indicadoras sazonais aditivas (ARIMA_SEASD) e o modelo Arima Sazonal (ARIMA_SEASM), que trata a sazonalidade de forma multiplicativa. Os modelos elementares recebem esse nome porque incluem apenas informações sobre a própria variável de resposta, sem a inclusão de quaisquer variáveis explicativas, exceto aquelas que consideram sazonalidade ou observações atípicas. 

ARIMA_SEASD Os modelos ARIMA com variáveis indicadoras sazonais aditivas e de observações atípicas têm a mesma estrutura descrita na seção ARIMA, onde as variáveis indicadoras são incluídas no modelo como variáveis explicativas. As variáveis indicadoras sazonais são incluídas considerando a frequência dos dados. Por exemplo, para um conjunto de dados mensal, são incluídas variáveis que indicam o mês do ano; para bimestral, são incluídas variáveis indicadoras do bimestre. Para um conjunto de dados diário, por outro lado, são adicionados dois conjuntos de variáveis indicadoras: aqueles que consideram o dia da semana e outros para o mês do ano. A ordem ótima dos termos ARIMA é identificada considerando todo o conjunto de dados de modelagem. 

ARIMA_SEASM O modelo Arima Sazonal considera a sazonalidade dentro de sua ordem sazonal de arima e pode incluir variáveis indicadoras de observações atípicas, se forem identificadas. Diferentemente de um modelo ARIMA regular, um modelo Arima Sazonal é da forma ARIMA(p,d,q)x(P,D,Q)m, onde P, D e Q são os termos auto-regressivos, de diferenciação e de média móvel sazonais, e m indica a frequência dos dados. Este modelo trata a sazonalidade considerando que ela é multiplicativa, ou seja, os padrões sazonais mudam ao longo do tempo, enquanto a sazonalidade aditiva (modelada através do ARIMA_SEASD) pressupõe que os padrões permanecem constantes. 

STL A decomposição sazonal e de tendência usando Loess (STL) é um método para estimar padrões na variável de resposta. Uma decomposição de série temporal consiste em separar os efeitos nos dados em uma tendência, sazonalidade e um erro. Isso possibilita ver claramente cada um desses efeitos individualmente e identificar aspectos importantes dos dados. A decomposição STL estima esses componentes de forma iterativa, usando a interpolação de Loess para suavizar a estimativa dos componentes sazonais e encontrar a estimativa de tendência. 

  

Regressão Regularizada - Breve Descrição (Incluindo Parâmetros)  

As regressões regularizadas são métodos projetados para reduzir os coeficientes em direção a zero, penalizando coeficientes maiores na função de perda. A ideia é que esse tipo de modelo generalize melhor, uma vez que cada regressor contribui um pouco para o resultado, obtendo resultados mais "suaves". As regularizações podem ser do tipo L1 (Lasso) ou L2 (Ridge), com o ElasticNet combinando ambos. 

Os tipos L1 e L2 impõem uma penalização na função de perda, que é proporcional ao tamanho dos coeficientes absolutos para L1 e quadrático para L2. O modelo Lasso representa a regularização L1 e o Ridge L2, sendo que o Lasso pode reduzir os coeficientes a zero, e o Ridge pode reduzi-los em direção a zero, mas nunca alcançando-o completamente. Há um parâmetro, lambda, que controla o grau dessa penalidade; se ele tender ao infinito, os coeficientes se moverão em direção a zero. 

O ElasticNet combina L1 e L2 e possui um parâmetro adicional, "alpha", que é uma espécie de peso dado para L1, com seu peso "correspondente" proporcional a 1 - alpha para L2. 

 
Random Forest - Breve Descrição (Incluindo Parâmetros)  

Random Forests, ou florestas de decisão aleatória, é um modelo proposto por Ho em 1995 com base em árvores de decisão. Ele visa resolver o problema de árvores de decisão que não generalizam bem para novos dados (overfitting), criando um conjunto de várias árvores usando um método chamado bagging (agregação bootstrap). 

O método funciona extraindo subamostras de recursos do conjunto de dados original e treinando diferentes árvores com essas subamostras. Os resultados de cada árvore são então combinados para problemas de regressão (como é o caso para previsão de séries temporais) ou obtém-se a maioria dos votos para classificação. 

Sendo um modelo não paramétrico, o Random Forest não possui parâmetros, mas sim hiperparâmetros, dentre os quais testamos dois: 

mtry: número de preditores amostrados para divisão em cada nó; 

ntree: número de árvores a serem geradas. 

Parte superior do formulário 

 
Informação do Modelo - Valor p do Teste de Ljung-Box  

O teste de Ljung-Box é um teste estatístico desenvolvido por Ljung e Box para avaliar a correlação das variáveis com seus valores passados (conhecida como autocorrelação). Ele testa se existe autocorrelação na série temporal até um atraso escolhido pelo usuário. No FaaS, o atraso escolhido é de um período, ou seja, ele testa se o resíduo do modelo possui autocorrelação com seu período passado mais recente. O valor p do teste de Ljung-Box é uma maneira mais simples de interpretar os resultados. Ele varia de 0 a 1 e há um limiar comum nas ciências sociais: se o valor p for menor que 0,05, podemos dizer que a autocorrelação é significativa. Caso contrário, se for maior que 0,05, não há autocorrelação significativa. 

 

 

Informação do Modelo - Ordem ARIMA  

Como mencionado no tópico "ARIMA", podemos dividir o ARIMA em três partes: i) a parte autoregressiva (AR); ii) a parte de integração e; iii) a parte de média móvel (MA). Essas partes formam a ordem ARIMA (p, d, q), onde p é a ordem da parte AR, ou seja, p é o número de entradas anteriores usadas para prever o próximo valor, d é a ordem de integração da série, ou seja, o número de diferenças necessárias para tornar a série temporal estacionária, e q é a ordem da parte MA. 

Informação do Modelo - Transformação  

'Ajuste', como o nome sugere, mostra todas as transformações aplicadas ao conjunto de dados usado nesse modelo. Atualmente, existem dois tipos possíveis de transformações a serem usadas: log e diferenciação, que podem ser aplicados independentemente ou ao mesmo tempo. Se 'Log' for mostrado como uma transformação, significa que essa transformação foi aplicada a todas as variáveis em que foi possível (não é possível aplicar a transformação log em variáveis que assumem valores menores ou iguais a 0, variáveis que foram identificadas como categóricas ou que têm um prefixo 'z_' em seus nomes). Se '1Diff' ou '2Diff' for mostrado como uma transformação, significa que os dados foram diferenciados quantas vezes indicadas pelo número, enquanto '1 Seas Diff' indica que uma diferenciação sazonal de ordem 1 foi aplicada aos dados. Também é possível encontrar 'mixed' como uma transformação para modelos de combinação. Uma transformação mista indica que modelos com diferentes transformações foram combinados e, portanto, a transformação final aplicada aos dados é mista. 

Verificar Resíduos - Resíduos  

A seção de verificação de resíduos contém informações sobre os resíduos dos modelos. Os resíduos são a diferença entre os valores originais da série temporal e as previsões. O gráfico de Resíduos mostra essas diferenças para cada observação. 

Verificar Resíduos - ACF  

O Gráfico ACF (Função de Autocorrelação Automática, também chamado de correlograma) mostra a correlação de uma série de dados com ela mesma com um atraso k que se refere à ordem de correlação, ou seja, no atraso 2 representamos a correlação da série no tempo t com ela mesma no tempo t-2. 

No gráfico ACF, o eixo vertical indica o valor de autocorrelação e o eixo horizontal o atraso. A linha tracejada indica o intervalo de confiança onde o valor de autocorrelação é significativamente zero ou diferente de zero. Se o valor de autocorrelação estiver dentro dos limites do intervalo de confiança, podemos dizer que não há autocorrelação. No entanto, se os valores estiverem fora dos limites, a autocorrelação é significativamente diferente de zero. 

Para os resíduos, pressupõe-se que eles não são autocorrelacionados, porque se houver autocorrelação nos resíduos, algumas informações relevantes não capturadas pelo modelo estão contidas neles. 

Parte superior do formulário 

Verificar Resíduos - Histograma  

 

Apresenta, em um histograma, a distribuição dos erros de previsão (resíduos), obtidos pela subtração dos valores previstos do modelo ajustado dos valores originais da série temporal. Deve frequentemente seguir uma distribuição normal. 

Dados Reais vs. Ajuste do Modelo - Ajuste  

A seção Dados Reais vs. Ajuste do Modelo é composta por gráficos de linha que representam os dados reais, também chamados de dados históricos, e os dados estimados pelo modelo ajustado. A linha contínua representa os dados históricos da série temporal e a linha tracejada representa os dados estimados. 

Dados Reais + Previsão - Ajustado Sazonal  

A seção Dados Reais + Previsão apresenta gráficos de linha que representam os dados históricos e a previsão estimada para o modelo selecionado. Esta seção também mostra os dados históricos e a projeção ajustada sazonalmente. 

Decomposição: Principais Componentes Os componentes de decomposição representam a participação deles na variação da série. Suponha que tenha sido observada uma variação de 2% em uma série, a decomposição dividirá literalmente esse efeito em todos os elementos do modelo, totalizando 2%. Alguns deles têm nomes específicos:  

• sum_do: Soma dos efeitos dos indicadores de outliers isolados e interagindo com outras variáveis;  

• sum_season: Soma dos efeitos sazonais isolados e interagindo com outros efeitos sazonais;  

• sum_eps: A soma do erro "puro" do modelo, ou seja, a parte não explicada do modelo e sua interação com outras variáveis;  

• not_explained: O erro de aproximação da metodologia de decomposição (quando a variável dependente é transformada em log);  

• persistence: A soma de todos os componentes autoregressivos e de média móvel;  

• <variável>: Efeitos com outros nomes de variáveis representam sua própria parte na explicação da decomposição; 

Decomposição: Trimestral/Anual (QoQ/ YoY)  

A ideia principal de acumular efeitos ao longo de trimestres e anos é atenuar efeitos isolados e compreender os principais impulsionadores das mudanças na série avaliada. Utilizando essa visualização, o usuário pode entender como as mudanças de um trimestre para outro ou de um ano para o próximo são explicadas através da perspectiva do modelo. Para acumular ao longo de um trimestre ou ano, é necessário definir se a série é do tipo fluxo ou estoque. A série de estoque é caracterizada por medidas feitas em um ponto específico no tempo, por exemplo, a população; enquanto o fluxo é medido ao longo de um período. Isso muda principalmente a base de comparação e como ela se acumula ao longo do tempo.  

Painel de Determinantes: Números e Cores  

O painel de determinantes mostra os valores estatísticos e a significância das variáveis independentes em diferentes modelos. As cores no painel se referem à significância da variável em um modelo específico, sendo que as variáveis mais significativas estão em vermelho, enquanto as menos significativas estão em azul. O valor de significância varia entre 0 e 1. Os números no painel de variáveis são os parâmetros ou coeficientes estimados em cada modelo para cada uma das variáveis fornecidas. Na área de métricas, as métricas MAPE, WMAPE, MPE, RMSE, MASE e MASEs são exibidas para cada modelo. 

Painel de Determinantes: Colunas e Linhas  

As colunas no painel de determinantes estão relacionadas a cada um dos primeiros N modelos, onde o valor de N é selecionado em um menu suspenso. O painel é dividido em duas seções diferentes, ambas compartilham as mesmas colunas, mas na primeira, o painel de variáveis, as linhas são variáveis independentes que foram selecionadas em pelo menos um dos modelos. A segunda é a seção de métricas, onde as linhas são as diferentes métricas avaliadas pela plataforma.  

Validação Cruzada - Janelas  

A seção de janelas de validação cruzada apresenta as previsões do modelo com os dados reais para cada uma das janelas definidas ao criar o trabalho de modelagem. Para cada janela, o modelo foi treinado com dados históricos e, portanto, as previsões para cada janela são como se fossem dados fora da amostra. Acompanhando as previsões e os valores reais estão as métricas de precisão, calculadas com base nos resultados de cada janela. Elas são agregadas com base no critério escolhido (média ou mediana) e o número de valores em cada janela é definido pelo Horizonte de Previsão definido. 

Parte superior do formulário 

Modelo em Produção - Coeficientes e Variáveis - Impactos Potenciais  

Quando um modelo ARIMA é enviado para 'Modelo em Produção', a aba 'Impactos Potenciais' mostra os coeficientes (x) associados a algumas das variáveis explicativas usadas neste modelo. Abaixo, podemos ver a interpretação deles, dependendo do tipo de transformação aplicada: 

Se tanto as variáveis de resposta quanto as variáveis explicativas forem transformadas em log, a interpretação do coeficiente é que ao aumentar 1% da variável explicativa, há um aumento esperado de x% na variável de resposta. 

Se nenhuma transformação for aplicada, a interpretação do coeficiente é que ao aumentar 1 unidade da variável explicativa, há um aumento esperado de x unidades na variável de resposta. Os 'Impactos Potenciais' mostram apenas o efeito de variáveis explicativas que nossa plataforma permite simular, ou seja, variáveis que são consideradas categóricas dentro do nosso pipeline e as variáveis para as quais não é possível aplicar log (assumindo valores menores ou iguais a 0) não serão mostradas nesta aba.  

Modelo em Produção - Choques e Variações 

Parte superior do formulário 
