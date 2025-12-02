# Guia de Configuração - Dashboard de Vendas Power BI

## 📋 Visão Geral
Dashboard completo para análise de vendas com foco em performance, regiões, produtos e vendedores.

## 🚀 Como Importar os Dados

### Passo 1: Preparar o Power BI
1. Abra o Power BI Desktop
2. Clique em "Obter Dados" → "Texto/CSV"
3. Navegue até `/dados/vendas.csv` e selecione

### Passo 2: Configurar o Modelo de Dados
1. Na aba "Transformação", verifique os tipos de dados:
   - **Data**: Data/Hora
   - **Quantidade**: Número Inteiro
   - **Preco_Unitario**: Número Decimal
   - **Valor_Total**: Número Decimal

2. Clique em "Fechar e Aplicar"

### Passo 3: Criar a Tabela de Calendário
Adicione esta consulta M em "Obter Dados" → "Consulta em Branco":

```
let
    MinData = Date.From(List.Min(#"Vendas"[Data])),
    MaxData = Date.From(List.Max(#"Vendas"[Data])),
    ListaDatas = List.Dates(MinData, Number.From(MaxData - MinData) + 1, #duration(1, 0, 0, 0)),
    Tabela = Table.FromList(ListaDatas, Splitter.SplitByNothing(), {"Data"}, null, ExtraValues.Error),
    TipoAlterado = Table.TransformColumnTypes(Tabela,{{"Data", type date}})
in
    TipoAlterado
```

## 📊 Estrutura do Dashboard Recomendada

### Página 1: Visão Geral
- **Cartão 1**: Total de Vendas (Valor)
- **Cartão 2**: Total de Vendas (Quantidade)
- **Cartão 3**: Ticket Médio
- **Cartão 4**: % da Meta Atingida
- **Gráfico de Linha**: Vendas por Data
- **Gráfico de Colunas**: Top 5 Produtos
- **Mapa**: Vendas por Região

### Página 2: Análise Regional
- **Tabela**: Regiões com Total, Quantidade, Ticket Médio
- **Gráfico de Pizza**: Distribuição por Região
- **Gráfico de Barras**: Vendedores por Região

### Página 3: Análise de Produtos
- **Gráfico de Colunas**: Vendas por Categoria
- **Tabela**: Produtos com Ranking
- **Gráfico de Dispersão**: Quantidade vs Valor

### Página 4: Performance de Vendedores
- **Tabela**: Vendedores com Total, Média, Quantidade
- **Gráfico de Barras**: Top Vendedores
- **Cartões**: KPIs por Vendedor (slicer)

## 🔧 Medidas DAX Essenciais

Copie todas as medidas do arquivo `modelos/medidas_dax.txt` para o seu modelo.

### Passos:
1. Clique em "Nova Medida" no Power BI
2. Cole o código DAX
3. Pressione Enter
4. Repita para todas as medidas

## 📈 Segmentadores (Slicers) Recomendados

- **Período**: Mês/Ano (em todas as páginas)
- **Região**: Filtro por região
- **Categoria**: Filtro por categoria de produto
- **Vendedor**: Filtro por vendedor
- **Status**: Filtro por status da venda

## 💾 Boas Práticas

1. **Formatação de Números**:
   - Valores monetários: R$ #.##0,00
   - Percentuais: 0,00%
   - Inteiros: #.##0

2. **Cores Consistentes**:
   - Verde: Crescimento/Positivo
   - Vermelho: Queda/Negativo
   - Azul: Neutro/Info

3. **Relacionamentos**:
   - Vendas[Data] → Calendario[Data]
   - Vendas[Vendedor] → Tabela de Vendedores (criar)
   - Vendas[Regiao] → Tabela de Regiões (criar)

4. **Atualizar Dados**:
   - Coloque o arquivo `vendas.csv` em um local compartilhado
   - Configure atualização agendada no Power BI Service

## 🎨 Dicas de Design

- Use tema consistente (Tema claro ou escuro)
- Máximo 3-4 visualizações por página
- Ordene os segmentadores logicamente
- Use espaços em branco para respiração visual
- Coloque KPIs principais no topo

## 📝 Próximos Passos

1. Adicionar dados históricos (últimos 12 meses)
2. Criar projeções com análise de tendências
3. Implementar decomposição de valores
4. Configurar alertas para metas não atingidas
5. Publicar no Power BI Service para compartilhamento

---
**Criado em**: Dezembro de 2025
**Versão**: 1.0
