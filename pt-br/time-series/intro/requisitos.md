# Requisitos do arquivo de dados

Nessa seção, vamos abordar os requisitos do arquivo de dados para um projeto de séries temporais. 

## Arquivo

Certifique-se de que seu arquivo de dados atende aos seguintes requisitos:

- A primeira linha deve conter os nomes das colunas;
- O arquivo deve ter no mínimo duas colunas: uma coluna de data e uma coluna numérica com variável alvo/dependente;
- Mantenha o período de projeção desejado com as datas sinalizadas e com linhas vazias para a variável alvo/dependente.

Acesse o [arquivo de exemplo](https://storage.googleapis.com/bkt-prod-4casthub/datasets/dataset-pt.xlsx) onde se deseja projetar a variável "abcr_leves" e as demais variáveis presentes são utilizadas como explicativas. 

## Informação de data

Certifique-se das informações de data do seu arquivo: 

- Deve conter apenas uma observação por data (por exemplo, o conjunto de dados na frequência mensal não deve ter duas linhas com observação para janeiro de 2020);
- Aceitamos as seguintes frequências: diária, semanal, quinzenal, mensal, bimestral, trimestral, semestral e anual.

Dependendo da frequência, o arquivo precisa de um determinado número de dados históricos para a variável dependente (número de linhas excluindo o período de projeção):

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

## Variáveis explicativas

Opcionalmente, o seu arquivo pode conter colunas extras com variáveis preditivas/explicativas. 

- Garanta que essas colunas tenham apenas informações numéricas. 

