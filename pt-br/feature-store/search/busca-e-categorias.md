# Pesquisando por indicadores

Nesta seção, vamos abordar como você pode pesquisar dados na Feature Store para encontrar os indicadores que você procura.

Se você não está muito familiarizado com termos técnicos e siglas usadas para nomear os indicadores, sugerimos que comece sua exploração pela Feature Store com a ajuda do Chat 4i. O [artigo anterior](/help-center/feature-store/search/chat-4i.md) aborda como encontrar indicadores e acessar conhecimento técnico de forma simples e dinâmica utilizando o Chat4i.

Por outro lado, se você já tem uma ideia clara do indicador que deseja incluir em suas análises baseadas em dados, há três formas de buscar por ele: (1) exploração de país e categorias, (2) pesquisa por palavras-chave e (3) pesquisa pelo código do indicador.

**1) Exploração através dos filtros país e categoria**

-   A Feature Store organiza todos os dados por país e em categorias e subcategorias, tornando mais fácil encontrar indicadores relacionados a temas específicos ou dados setoriais. Você pode usar as opções de filtro disponíveis na aba "Filtrar pesquisa" para refinar a lista de indicadores com base no país e na categoria desejada. 

-   Quando você acessa a Feature Store, verá uma lista de indicadores relacionados ao Brasil sem filtros de categoria. Para explorar indicadores de outros países, basta selecionar o país desejado na aba "Filtrar pesquisa". Para explorar categorias específicas relacionadas ao país selecionado, basta clicar na categoria desejada.

-   A Feature Store possui 8 categorias principais, cada uma com várias subcategorias. As categorias incluem Atividade Econômica, Controles (especialmente úteis para usuários do nosso motor de modelagem), Crédito, Dados Ambientais, Dados Climáticos, Finanças Públicas, Mercado Financeiro e de Capitais, e Setor Externo.

-   **Dicas**: O número entre parênteses ao lado de categoria e subcategoria indica quantos indicadores fazem parte delas. Você pode reverter a seleção de filtros de país e categoria clicando em "Limpar filtros".


**2) Pesquisa por palavras-chave**

-   Para encontrar de forma rápida os indicadores que você procura na Feature Store, busque por palavras-chave que se relacionem com o nome do indicador. Você pode buscar por "Juros" para encontrar a [Taxa Selic](https://stg4ch.4casthub.ai/feature-store/indicators/BRINR0010), que é taxa de juros de referência da economia brasileira, ou pode buscar pela sigla "Selic", jargão popular entre os agentes do mercado.
-  **Dica** Você também consegue utilizar a pesquisa para encontrar todos os indicadores que vêm da mesma fonte primária. No exemplo abaixo, procuramos todos os indicadores da categoria Finanças Públicas, cuja fonte primária é o Tesouro Nacional.

![](https://raw.githubusercontent.com/4intelligence/documentation/main/pt-br/feature-store/search/img/busca_palavra.png)

**3) Pesquisa pelo código do indicador**

-   Todo indicador da Feature Store possui um código único de nove dígitos que o identifica de forma exclusiva. Esse código está visível na URL da página do indicador. Dê uma olhada nos últimos 9 caracteres que aparecem no na caixa de texto no topo do seu navegador, esse é o seu código.
-   Você consegue encontrar um indicador pesquisando pelo seu código único de nove dígitos. Por exemplo, para encontrar o [Produto Interno Bruto (PIB) com metodologia 4intelligence](https://4casthub.ai/feature-store/indicators/BRGDP0081) na Feature Store, digite 'BRGDP0081' na caixa de pesquisa. O indicador será o primeiro resultado da busca.

![](https://raw.githubusercontent.com/4intelligence/documentation/main/pt-br/feature-store/search/img/busca_codigo.png)

**Atenção**: A pesquisa, seja por palavras-chave ou código de nove dígitos, é específica ao país e à categoria em que você está navegando. Certifique-se de selecionar corretamente esses dois campos antes de iniciar sua pesquisa.

<style>
blue4i {
  color: #4C94FF;
}
</style>
<blue4i>**Comece a explorar os indicadores agora! Qual categoria de indicadores você gostaria de explorar primeiro?**</blue4i>