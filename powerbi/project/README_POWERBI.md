# Power BI Project — Retail Performance Analytics

## Como Abrir

1. Instale o Power BI Desktop (versão gratuita em powerbi.microsoft.com).
2. Clone este repositório.
3. Execute os notebooks na ordem para gerar `data/processed/retail_clean.parquet`.
4. Abra `RetailPerformanceAnalytics.pbip` no Power BI Desktop.
5. Clique em "Atualizar" para carregar os dados processados.

## Estrutura do Projeto PBIP

```
powerbi/project/
├── RetailPerformanceAnalytics.pbip          # Arquivo de entrada do projeto
└── RetailPerformanceAnalytics.Report/
    ├── report.json                          # Definição das páginas e fonte de dados
    └── dax_measures.json                    # Todas as medidas DAX versionadas
```

## Páginas

| Página | Conteúdo Principal |
|---|---|
| Executive Overview | £10.642.110,80 de faturamento, 20.134 pedidos, mapa de 38 países |
| Análise de Clientes e Produtos | Pareto de 3.925 SKUs, LTV de 4.339 clientes |
| Qualidade e Integridade | Reconciliação £0,00 entre Python, DuckDB, SQLite e BigQuery |

## Medidas DAX

Todas as medidas estão documentadas em `dax_measures.json` com campo `page` indicando em qual página cada medida é usada.
