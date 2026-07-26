# Retail Performance Analytics: Da Transação ao Insight Executivo

**Um projeto documentado de Business Intelligence que transforma transações brutas de varejo em uma visão de performance executiva confiável e auditada.**

Este projeto analisa o dataset *UCI Online Retail* utilizando **Python, SQL e Power BI**. O trabalho abrange desde a auditoria da fonte, limpeza orientada a regras de negócio, reconciliação de KPIs entre linguagens, análise de comportamento de clientes e produtos, até a modelagem dimensional e design de dashboard executivo.

---

### 📊 [CLIQUE AQUI PARA ACESSAR O DASHBOARD INTERATIVO](https://retail-performance-pbip.ai.studio/)

---

## 🛠️ Tech Stack e Habilidades
Este repositório demonstra competências de **Analytics Engineering** e **Business Intelligence** de ponta a ponta:

- **Python (Pandas, Matplotlib, Seaborn):** Processamento de dados (ETL), limpeza técnica orientada a regras de negócio e análise exploratória (EDA).
- **SQL (SQLite):** Reconciliação de métricas, agregações complexas e validação da "Fonte Única da Verdade" (Single Source of Truth).
- **Power BI (DAX, Star Schema, PBIP):** Modelagem dimensional avançada, cálculos de inteligência temporal e design de dashboard focado em UX executiva.
- **Engenharia Analítica:** Documentação de modelos de dados, dicionário de métricas e scripts de validação automatizados.

> O projeto Power BI (formato PBIP) está incluído no repositório. Cada KPI publicado foi reconciliado com o dataset processado para garantir a integridade total dos dados.

## Status do Projeto

| Workstream (Frente de Trabalho) | Status |
|---|---|
| Entendimento dos dados (Data understanding) | Completo |
| Limpeza e validação de dados | Completo |
| Análise de negócio com Python | Completo |
| Reconciliação via SQL | Completo |
| Especificação de KPI e modelo semântico | Completo |
| Visão geral executiva no Power BI | Completo |
| Projeto PBIP com controle de versão | Completo |
| Páginas de detalhe: Cliente, Produto e Qualidade | Especificado para a próxima iteração |
| Refresh final do Power BI Desktop | Completo |

## Resultados Executivos

O dataset analítico contém vendas de varejo concluídas após a remoção de descrições ausentes, registros duplicados, quantidades não positivas e preços unitários negativos.

| KPI | Resultado Verificado | Definição |
|---|---:|---|
| **Sales (Vendas)** | **£10,642,110.80** | Soma de `Quantity × UnitPrice` |
| **Orders (Pedidos)** | **20,134** | Contagem distinta de números de faturas concluídas |
| **Identified customers** | **4,339** | Contagem distinta de IDs de clientes (não nulos) |
| **Products sold** | **3,925** | Stock codes distintos em vendas concluídas |
| **Average order value (AOV)** | **£528.56** | Receita total dividida pelo total de pedidos |
| **Countries (Países)** | **38** | Países distintos presentes nas transações |

Estas métricas utilizam uma população limpa consistente de **525.460 linhas de transação**. As contagens da fonte original (541.909 linhas) são mantidas apenas para análise de qualidade e não são misturadas aos KPIs de vendas.

## Perguntas de Negócio Respondidas

1. Qual é a performance geral do negócio em faturamento e volume?
2. Como as vendas e o valor médio do pedido (AOV) mudam ao longo do tempo?
3. Quais mercados (países) mais contribuem para a receita?
4. Quais clientes geram o maior valor para a empresa?
5. Quais produtos físicos lideram as vendas após a separação de taxas operacionais?
6. Quais limitações da fonte de dados afetam a interpretação dos resultados?

## Fluxo Analítico (Workflow)

```mermaid
flowchart TD
    A[UCI source workbook] --> B[Auditoria de Fonte e Qualidade]
    B --> C[Regras de Limpeza (Business-led)]
    C --> D[Reconciliação Python e SQL]
    D --> E[Modelo Semântico Power BI]
    E --> F[Relatório Executivo e Validação]
