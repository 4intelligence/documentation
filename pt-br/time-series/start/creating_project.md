# Criando um projeto

## Requisitos do arquivo de dados

- Por favor, certifique-se que seu arquivo de dados atende aos seguintes requisitos:
- A primeira linha deve conter os nomes das colunas
- O arquivo deve ter no mínimo duas colunas: uma coluna de data e uma coluna numérica com variável alvo/dependente
- Coluna de data:
   - Deve conter apenas uma observação por data (por exemplo, o conjunto de dados não deve ter duas linhas com observação para janeiro de 2020)
   - Aceitamos as seguintes frequências: diária, semanal, quinzenal, mensal, bimestral, trimestral, semestral e anual
   - Dependendo da frequência, o arquivo precisa de um determinado número de dados históricos para a variável dependente (número de linhas excluindo o período de projeção)

Diário |	Semanal |	Quinzenal |	Mensal |	Bimestral |	Trimestral |	Semestral |	Anual
180 |	52 |	24 |	36 |	24 |	24 |	24 |	12

- Opcional: Colunas extras com variáveis preditivas/explicativas (apenas numéricas)

## Variáveis 

### Variáveis explicativas  

Variáveis explicativas (também chamadas de variáveis preditoras, regressores ou x) são usadas para prever ou explicar as variações que ocorrem na variável dependente (ou variável alvo). Com base na relação estimada entre essas variáveis, o analista pode compreender correlações e realizar previsões. Como exemplo, suponhamos que estamos interessados em prever o consumo de energia (variável dependente) em uma determinada cidade. As possíveis variáveis explicativas poderiam ser: número de pessoas residentes nesta cidade, temperatura máxima e mínima. 

### Variável dependente  

A variável dependente (também chamada de variável alvo, resultado ou y) é a variável de saída em um experimento, ou simplesmente a variável de interesse no modelo. 

Frequência dos Dados - Conceito + não mais do que 1 observação por período de frequência  

O algoritmo identifica automaticamente a frequência dos dados no conjunto de dados. A frequência dos dados é definida de acordo com a diferença (medida em dias) entre os valores da coluna de datas. Para uma sequência de datas dada, o algoritmo calcula a diferença entre elas e calcula a mediana. Se, por exemplo, o valor mediano estiver dentro do intervalo [20, ..., 31], o código assume que os dados têm frequência mensal. Uma vez determinada a frequência, é possível verificar se há mais de uma linha para cada período de frequência. Por exemplo, para uma frequência mensal, o algoritmo não permitirá duas linhas com dias diferentes no mesmo mês. 

### Número mínimo de pontos de dados por frequência  

Dependendo da frequência dos dados fornecidos, o algoritmo precisa de uma certa quantidade de pontos de dados válidos (número de linhas) para realizar a modelagem e fornecer os melhores resultados possíveis. Observe que algumas das linhas originais podem ser descartadas antes deste momento, se faltarem dados (por exemplo, excesso de valores ausentes), reduzindo assim o número de pontos de dados válidos. Após a remoção, o conjunto de dados deve ter pelo menos o número mínimo de pontos de dados exibido na tabela abaixo por frequência. Uma tabela contendo o número mínimo de pontos de dados por frequência pode ser vista abaixo: 


