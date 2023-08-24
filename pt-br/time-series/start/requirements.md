# Requisitos do arquivo de dados

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
