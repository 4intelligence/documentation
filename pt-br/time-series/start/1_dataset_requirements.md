# Requisitos do arquivo de dados

Certifique-se que seu arquivo de dados atende aos seguintes requisitos:

- A primeira linha deve conter os nomes das colunas
- O arquivo deve ter no mínimo duas colunas: uma coluna de data e uma coluna numérica com variável alvo/dependente
- Coluna de data:
   - Deve conter apenas uma observação por data (por exemplo, o conjunto de dados não deve ter duas linhas com observação para janeiro de 2020)
   - Aceitamos as seguintes frequências: diária, semanal, quinzenal, mensal, bimestral, trimestral, semestral e anual
   - Dependendo da frequência, o arquivo precisa de um determinado número de dados históricos para a variável dependente (número de linhas excluindo o período de projeção)

Frequência  | Mínimo de pontos de data
:---:       | :---:
Diário      | 180 
Semanal     | 52 
Quinzenal   | 24 
Mensal      | 36 
Bimestral   | 24 
Trimestral  | 24 
Semestral   | 24
Anual       | 12 

- Opcional: Colunas extras com variáveis preditivas/explicativas (apenas numéricas)