# Retail Performance Analytics: Da Transação ao Insight Executivo

**Case de Analytics Engineering com reconciliação ponta a ponta entre Python, SQL, BigQuery, DuckDB e Power BI — os mesmos £10.642.110,80 de faturamento validados em quatro camadas independentes.**

O projeto analisa o dataset *UCI Online Retail* cobrindo o ciclo completo: diagnóstico de qualidade da fonte, higienização orientada a regras de negócio, reconciliação de KPIs entre camadas, análise de LTV e mix de produtos, modelagem dimensional Star Schema e dashboards executivos em Power BI e Looker Studio.

---

[![Power BI](https://img.shields.io/badge/Power_BI-Dashboard_Executivo-F2C811?logo=powerbi&logoColor=black)](powerbi/project/)
[![Looker Studio](https://img.shields.io/badge/Looker_Studio-Painel_Web-4285F4?logo=googleanalytics&logoColor=white)](https://lookerstudio.google.com/)
[![BigQuery](https://img.shields.io/badge/BigQuery-Data_Warehouse-4285F4?logo=googlebigquery&logoColor=white)](https://cloud.google.com/bigquery)
[![DuckDB](https://img.shields.io/badge/DuckDB-Analytical_Queries-FDD835?logo=duckdb&logoColor=black)](https://duckdb.org/)
[![Python](https://img.shields.io/badge/Python-3.11-blue?logo=python)](https://www.python.org/)
[![SQL](https://img.shields.io/badge/SQL-SQLite-lightgrey?logo=sqlite)](https://www.sqlite.org/)
[![Pytest](https://img.shields.io/badge/Pytest-Integrity_Checks-green?logo=pytest)](https://docs.pytest.org/)

---

## Resultados Auditados

Base higienizada de **525.460 linhas**. O volume original (541.909) é mantido separado para fins de auditoria. Todos os KPIs foram reconciliados em Python, SQL (SQLite + BigQuery) e Power BI — os valores abaixo fecham nas quatro ferramentas.

| KPI | Resultado | Definição |
|---|---:|---|
| **Faturamento (Sales)** | **£10.642.110,80** | Soma de `Quantity × UnitPrice` na base limpa |
| **Volume de Pedidos** | **20.134** | Faturas únicas finalizadas |
| **Clientes Ativos** | **4.339** | Clientes com `CustomerID` identificado |
| **Mix de Produtos** | **3.925** | SKUs distintos com giro confirmado |
| **Ticket Médio (AOV)** | **£528,56** | Faturamento total / volume de pedidos |
| **Mercados Ativos** | **38** | Países com transações concluídas |

---

## Stack Técnico

| Camada | Tecnologia | Função no Projeto |
|---|---|---|
| Extração e EDA | Python (Pandas, Matplotlib, Seaborn) | ETL, higienização por regras de negócio, análise exploratória |
| Consultas Analíticas Leves | DuckDB | Queries SQL direto no Parquet sem servidor externo |
| Auditoria Local | SQL (SQLite) | Reconciliação de faturamento e validação de lógica de négócio |
| Data Warehouse | BigQuery | Modelo dimensional carregado na nuvem, fonte única de verdade |
| BI Corporativo | Power BI (DAX, Star Schema, PBIP) | Relatório executivo com inteligência de tempo, versionado via Git |
| BI Web Público | Looker Studio | Painel publicado na web, conectado ao BigQuery, sem instalação |
| Governança | Documentação de linhagem | Dicionário de medidas, scripts de auditoria, versionamento PBIP |

---

## Status do Projeto

| Frente de Trabalho | Status |
|---|---|
| Mapeamento e Diagnóstico de Dados | Completo |
| Higienização e Saneamento da Base | Completo |
| Análise de Negócio (Python) | Completo |
| Consultas Analíticas com DuckDB | Completo |
| Reconciliação Python vs SQL vs BigQuery | Completo |
| Modelagem Semântica e Especificação de KPIs | Completo |
| Dashboard Executivo Power BI (3 páginas) | Completo |
| Painel Looker Studio (Web) | Completo |
| Versionamento PBIP | Completo |
| Homologação Final (Power BI Desktop) | Completo |
| Deep Dive: Clientes, Produtos e Qualidade | Próxima Iteração |

---

## Pipeline de Inteligência

```mermaid
flowchart TD
    A[Dataset Original — UCI Online Retail] --> B[Diagnóstico de Qualidade e Gaps]
    B --> C[Higienização por Regras de Negócio]
    C --> D1[DuckDB — Queries Analíticas Locais]
    C --> D2[SQLite — Reconciliação Local]
    D1 --> E[BigQuery — Data Warehouse na Nuvem]
    D2 --> E
    E --> F1[Power BI — Dashboard Executivo]
    E --> F2[Looker Studio — Painel Web Público]
```

---

## Reconciliação Entre Camadas

O ponto de diferenciação técnico do projeto: o mesmo KPI de faturamento foi calculado de forma independente em quatro ambientes e o delta final em todas as comparações foi **£0,00**.

| Camada | Faturamento Calculado | Delta vs Python |
|---|---:|---:|
| Python (Pandas) | £10.642.110,80 | — |
| DuckDB (Parquet) | £10.642.110,80 | £0,00 |
| SQL (SQLite) | £10.642.110,80 | £0,00 |
| BigQuery (Data Warehouse) | £10.642.110,80 | £0,00 |

Essa reconciliação elimina o risco de divergência entre o dado apresentado em dashboard e o dado real de negócio.

---

## Higienização e Integridade de Dados

| Estágio | Linhas | Delta |
|---|---:|---:|
| Base Original (Raw) | 541.909 | — |
| Base Higienizada (Final) | 525.460 | −16.449 |

A régua de higienização foi conservadora para garantir o rigor das métricas sem eliminar faturamento legítimo:

- **Registros sem descrição:** Excluídos como ruído operacional sem valor comercial rastreável.
- **Duplicatas exatas:** Removidas para evitar inflação do GMV.
- **Quantidades negativas ou nulas:** Fora da visão de vendas concluídas; mantidas em tabela de auditoria.
- **Preços negativos (estornos):** Tratados como ajustes contábeis e segregados do faturamento bruto.
- **Clientes anônimos (`CustomerID` nulo):** Incluídos no faturamento global, excluídos das métricas de comportamento de base.

---

## Dashboard Executivo Power BI

O arquivo está em `powerbi/project/` no formato **PBIP** (Power BI Project), compatível com versionamento Git. Para abrir, instale o Power BI Desktop e clique no arquivo `.pbip`. O modelo usa Star Schema com tabelas `fact_sales`, `dim_customer`, `dim_product`, `dim_date` e `dim_country`.

### Página 1 — Executive Overview

Visão consolidada para consumo executivo: faturamento, volume, ticket médio, distribuição geográfica e tendência mensal.

| Visual | Medida DAX | Lógica |
|---|---|---|
| Card Faturamento | `Total Sales` | `SUMX(fact_sales, fact_sales[Quantity] * fact_sales[UnitPrice])` |
| Card Volume de Pedidos | `Total Orders` | `DISTINCTCOUNT(fact_sales[InvoiceNo])` |
| Card Ticket Médio | `AOV` | `DIVIDE([Total Sales], [Total Orders])` |
| Card Clientes Ativos | `Active Customers` | `DISTINCTCOUNT(fact_sales[CustomerID])` |
| Gráfico Temporal | `Monthly Sales` | `CALCULATE([Total Sales], DATESMTD(dim_date[Date]))` |
| Mapa por País | `Sales by Country` | `CALCULATE([Total Sales], ALLEXCEPT(dim_country, dim_country[Country]))` |

### Página 2 — Análise de Clientes e Produtos

Curva de Pareto por receita, LTV por cliente e giro de SKUs. O Reino Unido é tratado separadamente nos filtros de mercado geográfico.

| Visual | Medida DAX | Lógica |
|---|---|---|
| Top 10 Clientes | `Customer LTV` | `CALCULATE([Total Sales], ALLEXCEPT(dim_customer, dim_customer[CustomerID]))` |
| Curva ABC de Produtos | `Product Revenue Share` | `DIVIDE([Total Sales], CALCULATE([Total Sales], ALL(dim_product)))` |
| Acumulado Pareto | `Cumulative Share` | `CALCULATE([Product Revenue Share], FILTER(ALLSELECTED(dim_product), [Total Sales] >= EARLIER([Total Sales])))` |
| Frequência de Compra | `Avg Purchase Frequency` | `DIVIDE([Total Orders], [Active Customers])` |
| Faturamento Ex-UK | `Sales Ex-UK` | `CALCULATE([Total Sales], dim_country[Country] <> "United Kingdom")` |
| Share Internacional | `International Share` | `DIVIDE([Sales Ex-UK], [Total Sales])` |

### Página 3 — Qualidade e Integridade de Dados

Painel de transparência técnica. Mostra a reconciliação entre Python, SQL e Power BI, com o delta de cada camada exibido como visual de auditoria.

| Visual | Medida DAX | Lógica |
|---|---|---|
| Linhas Removidas | Estático | 16.449 (calculado no ETL Python) |
| Taxa de Aproveitamento | `Data Yield` | `DIVIDE(525460, 541909)` = 96,96% |
| Receita Anônima | `Anonymous Sales` | `CALCULATE([Total Sales], ISBLANK(dim_customer[CustomerID]))` |
| Delta Reconciliação | `SQL vs Python Delta` | Diferença entre soma Python e consulta SQL — target: £0,00 |
| Crescimento YoY | `YoY Sales Growth` | `DIVIDE([Total Sales] - [LY Sales], [LY Sales])` |

### Como Abrir e Atualizar o Dashboard

```bash
# 1. Clone o repositório
git clone https://github.com/Nayanearaujo/Retail-Performance-Analytics.git

# 2. Gere a base higienizada localmente
pip install -r requirements.txt
jupyter nbconvert --to notebook --execute notebooks/01_Data_Understanding.ipynb
jupyter nbconvert --to notebook --execute notebooks/02_Data_Cleaning.ipynb

# 3. Abra o Power BI Desktop, navegue até powerbi/project/ e clique no .pbip

# 4. Clique em "Atualizar" para reprocessar os dados com a base local
```

> O modelo usa caminhos relativos. Mantenha a estrutura de pastas do repositório para que a atualização funcione sem reconfiguração manual.

---

## Painel Looker Studio (Web)

Versão pública do relatório executivo, conectada diretamente ao BigQuery. Acessível via browser, sem necessidade de instalação de software.

- **Fonte de dados:** tabela `fact_sales` no BigQuery, particionada por mês de fatura
- **Atualização:** automática ao recarregar a página, refletindo qualquer nova carga no BigQuery
- **Páginas disponíveis:** Faturamento por Período, Top Países (Ex-UK), Top Produtos e Clientes

---

## Insights de Interpretação

- **Efeito Sazonal (Dez/2011):** A base encerra em 09/12/2011. Dezembro aparece como mês parcial e não representa queda de faturamento — é corte de fonte, não perda de tração. O dashboard sinaliza isso com anotação direta no gráfico temporal.
- **Concentração UK:** O Reino Unido representa 84,6% do faturamento. Os mercados internacionais são analisados em escala separada para evitar distorção visual nos rankings.
- **Receita Operacional:** Taxas de frete (`POSTAGE`) e ajustes manuais geram receita contábil mas não são produtos. Foram isolados para não contaminar o ranking de performance de mercadorias.

![Tendência mensal de vendas com o período parcial de dezembro/2011 sinalizado](images/monthly_sales_validated.png)

![Mercados internacionais por faturamento, excluindo o Reino Unido](images/international_market_sales.png)

---

## Estrutura do Repositório

```text
Retail-Performance-Analytics/
├── data/
│   ├── raw/                  # Dados brutos originais (UCI)
│   └── processed/            # Base higienizada gerada localmente
├── docs/                     # Modelo de dados e especificações técnicas
├── images/                   # Gráficos de evidência e assets do README
├── notebooks/                # ETL, Análise e Reconciliação
├── powerbi/
│   ├── dax/                  # Medidas DAX versionadas por página
│   ├── project/              # Arquivo PBIP (Power BI Project)
│   └── theme/                # Style Guide visual do relatório
├── scripts/                  # Validação de métricas e geração de assets
└── tests/                    # Testes de integridade da base
```

---

## Roteiro de Notebooks

| Notebook | Objetivo |
|---|---|
| `01_Data_Understanding.ipynb` | Diagnóstico de integridade, cancelamentos e cobertura da fonte |
| `02_Data_Cleaning.ipynb` | Aplicação das regras de negócio para saneamento da base |
| `03_business_analysis.ipynb` | Extração de insights de vendas, clientes, produtos e tempo |
| `04_SQL_Analysis.ipynb` | Reconciliação dos KPIs via SQL: auditoria técnica ponta a ponta |

---

## Como Reproduzir

```bash
# Instalar dependências
pip install -r requirements.txt

# Executar notebooks na ordem
jupyter lab

# Validar métricas e gerar assets de documentação
python scripts/validate_retail_metrics.py
python scripts/generate_documentation_assets.py
python -m pytest -q
```

---

## Ferramentas

Python · Pandas · Matplotlib · Seaborn · DuckDB · SQLite · SQL · BigQuery · Looker Studio · Power BI · Power Query · DAX · GitHub

---

## Fonte e Licença

- **Dataset:** UCI Online Retail, Daqing Chen — [doi:10.24432/C5BW33](https://doi.org/10.24432/C5BW33), licença CC BY 4.0.
- **Código e documentação:** [MIT License](LICENSE).

Desenvolvido por `Nayane Araujo`
