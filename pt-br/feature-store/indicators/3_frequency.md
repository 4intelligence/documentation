# Entendendo as Frequências

Nessa seção, vamos abordar como a Feature Store organiza os dados de acordo com a sua periodicidade e como funcionam as agregações temporais.

## O que é a frequência de uma série?

A Feature Store é uma base de dados composta por séries temporais e cada série temporal é caracterizada por uma frequência.

Para entender o conceito de frequência em séries temporais, imagine que você tenha registrado diariamente a [temperatura média](https://4casthub.ai/feature-store/indicators/BRMTG0003) em sua cidade ao longo de um ano, criando uma lista ordenada cronologicamente das temperaturas. Essa lista de temperaturas forma uma série temporal. A frequência dessa série temporal é diária, pois você registrou a temperatura todos os dias.

Em termos simples, a frequência de uma série temporal representa o intervalo de tempo entre cada registro de dados, o que nos permite entender a regularidade das observações ao longo do tempo.

## Feature Store disponibiliza série em quais frequências?

Você encontrará séries em frequência anual, trimestral, mensal, semanal e até diária na Feature Store.

Além de disponibilizar a frequência original do indicador, ou seja, a frequência em que o dado bruto é gerado, a Feature Store dispõe de rotinas automatizadas para construir agregações temporais a partir desse dado bruto. Isso significa que a Feature Store disponibiliza todas frequências possíveis para cada indicador.

## Como é feita agregação temporal de uma série?

Voltando ao exemplo das temperaturas médias registradas, imagine que você deseja identificar os meses em que sazonalmente registram-se temperaturas mais altas, o que pode ser difícil de visualizar com dados diários. Para fazer isso, você pode calcular a média das temperaturas registradas em cada mês, e então criar uma nova lista ordenada cronologicamente com um registro por mês. Nesse caso, a série de temperatura média passa de uma frequência diária para mensal através do cálculo do valor médio.

Em resumo, para agregar temporalmente uma série, é preciso definir qual é a o cálculo que irá condensar as informações das observações da frequência original para a frequência que queremos atingir.

Na Feature Store, quando a frequência é acompanhada pela indicação de um cálculo, como média ou soma, isso indica que a agregação foi construída automaticamente pelos nossos sistemas para facilitar sua análise. A agregação oferece uma visão mais abrangente das tendências e simplifica a compreensão do comportamento dos dados ao longo do tempo.

<style>
blue4i {
  color: #4C94FF;
}
</style>

<blue4i>**Agora que você entende sobre indicadores, regiões e frequência, você está pronto para mergulhar em nossos tratamentos de dados. Confira no próximo artigo!**</blue4i>