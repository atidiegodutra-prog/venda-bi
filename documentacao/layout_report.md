# Layout sugerido para o PBIX (mapeamento de visuais por página)

Este arquivo descreve quais visuais criar em cada página e quais medidas/campos usar.

Página 1 — Visão Geral
- Top area (linha): 4 cartões KPI
  - `Total Vendas` (medida)
  - `Total Quantidade` (medida)
  - `Ticket Médio` (medida)
  - `% Meta Atingida` (medida)
- Centro esquerdo: Gráfico de Linha
  - Eixo: `Calendario[Data]`
  - Valores: `Total Vendas` (série atual) e `Vendas Mês Anterior` (opcional como linha de comparação)
- Centro direito: Mapa (Filled Map ou Shape Map)
  - Local: `Vendas[Regiao]`
  - Valor: `Total Vendas`
- Inferior: Barras horizontais (Top 5 Produtos)
  - Eixo: `Vendas[Produto]`
  - Valores: `Total Vendas`
  - Top N filter: 5

Slicers (sempre visível): `Calendario[NomeMes]` (mês/ano), `Regiao`, `Categoria`, `Vendedor`, `Status`

Página 2 — Análise Regional
- Mapa grande: Vendas por `Regiao`
- Tabela / Matrix: `Regiao`, `Total Vendas`, `Quantidade`, `Ticket Médio`, `Rank Regiao`
- Gráfico de Colunas empilhadas: Regiao x Categoria (valor empilhado)
- Decomposition Tree: alvo `Total Vendas`, explicar por `Regiao` → `Categoria` → `Produto`

Página 3 — Análise de Produtos
- Gráfico de Colunas: `Categoria` vs `Total Vendas`
- Top N (barra horizontal): `Produto` vs `Total Vendas`
- Scatter (Dispersão): X=`Quantidade média por venda`, Y=`Ticket Médio`, Size=`Total Vendas`, Color=`Categoria`
- Tabela detalhada: `Produto`, `Categoria`, `Total Vendas`, `Quantidade`, `% do Total`

Página 4 — Performance Vendedores
- Barras horizontais: `Vendedor` vs `Total Vendas` (ordenado desc)
- Tabela detalhada por vendedor: `Total Vendas`, `Quantidade`, `Ticket Médio`, `% Meta Atingida`, `Diferença Meta`
- KPI Cards individuais: slicer por `Vendedor` para ver seus KPIs

Formato e configurações recomendadas
- Tema: Definir cores base da marca se houver
- Número: Formato monetário `R$` para medidas financeiras
- Rótulos: Exibir valores nos topo das barras para Top N
- Drilldown: Ativar hierarquia de Calendario (Ano>Trimestre>Mês>Dia)

Exportar layout
- Use este mapa para montar manualmente no Power BI Desktop
- Se quiser, gero um checklist imprimível com passos exatos para cada visual (campos + propriedades)
