# Modelagem de Dados - Tabelas Dimensionais

Este arquivo descreve as tabelas dimensionais adicionadas para suportar análises no Power BI.

## Tabelas criadas

- `calendario.csv` (nível de data)  
  Campos: `Date`, `Year`, `MonthNumber`, `MonthName`, `Quarter`, `YearMonth`  
  Observação: contém todas as datas presentes em `vendas.csv`. Para um calendário completo, recomendo gerar via Power Query (M) com intervalo extendido.

- `produtos.csv`  
  Campos: `ProductID`, `Produto`, `Categoria`, `Marca`, `Subcategoria`

- `vendedores.csv`  
  Campos: `VendedorID`, `Vendedor`, `Regiao_Principal`, `Email`

- `regioes.csv`  
  Campos: `RegiaoID`, `Regiao`, `Pais`

- `categorias.csv`  
  Campos: `CategoriaID`, `Categoria`, `Descricao`

## Relacionamentos sugeridos (Power BI)

- `calendario[Date] (1) -> (N) vendas[Data]`
- `produtos[Produto] (1) -> (N) vendas[Produto]`  (ou usar `ProductID` se preferir chave numérica)
- `vendedores[Vendedor] (1) -> (N) vendas[Vendedor]` (ou `VendedorID`)
- `regioes[Regiao] (1) -> (N) vendas[Regiao]`
- `categorias[Categoria] (1) -> (N) vendas[Categoria]`

Recomendações:
- Use chaves numéricas (ID) para relacionamentos quando possível; isso melhora performance.
- Crie relações de direção única de dimensão -> fatos.
- Sincronize slicers entre páginas conforme necessário.

## Como carregar no Power BI
1. Em Power BI Desktop, clique em `Obter Dados` → `Texto/CSV` e selecione cada arquivo em `dados/`.
2. Ajuste tipos (Data, Número, Texto) na tela de Transformação.
3. Em `Modelagem`, ajuste nomes e crie relacionamentos conforme sugerido.

---
Arquivo gerado automaticamente — revise e ajuste IDs/nomeclaturas se necessário.
