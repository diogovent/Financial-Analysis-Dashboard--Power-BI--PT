# 💰 Financial-Analysis-Dashboard--Power-BI (PT)

> Análise financeira de receitas e despesas de uma empresa ao longo de 2019, 2020 e 2022, com foco na margem de lucro e evolução por componente.

---

## 📌 Índice

- Sobre o Projeto
- Objetivos da Análise
- Ferramentas Utilizadas
- Estrutura do Dataset
- Dashboard
- Medidas DAX
- Principais Conclusões
- Como Visualizar

---

## 📁 Sobre o Projeto

Este projeto consiste numa análise financeira baseada em dados mensais de **receitas e despesas** de uma empresa, abrangendo os anos de **2019, 2020 e 2022**.

O objetivo principal é compreender a evolução financeira da empresa, identificar os componentes com maior peso nas receitas e despesas, e acompanhar a margem de lucro ao longo do tempo.

---

## 🎯 Objetivos da Análise

- Acompanhar a evolução total de receitas e despesas por ano
- Identificar os componentes de receita e despesa com maior peso
- Calcular e monitorizar a margem de lucro
- Comparar o desempenho financeiro entre os três anos disponíveis

---

## 🛠️ Ferramentas Utilizadas

| Ferramenta | Utilização |
|---|---|
| **Power BI Desktop** | Construção do dashboard e visualizações |
| **DAX** | Criação de medidas calculadas |
| **Excel (.xlsx)** | Fonte dos dados financeiros |

---

## 📂 Estrutura do Dataset

O ficheiro `DadosFinanceiros.xlsx` contém dados mensais organizados da seguinte forma:

| Coluna | Descrição |
|---|---|
| `Tipo` | Receita ou Despesa |
| `Componente` | Categoria específica (ex: Vendas, Salários) |
| `Jan-Dez 2019` | Valores mensais de 2019 |
| `Jan-Dez 2020` | Valores mensais de 2020 |
| `Jan-Dez 2022` | Valores mensais de 2022 |

### Componentes de Receita

| Componente | Total (3 anos) |
|---|---|
| Vendas | 1.359.336,00 € |
| Licenciamento | 232.200,00 € |
| Aluguéis | 119.175,00 € |
| Publicidade | 78.978,00 € |
| Investimentos | 68.800,00 € |
| Franquias | 61.600,00 € |
| **Total Receitas** | **1.920.089,00 €** |

### Componentes de Despesa

| Componente | Total (3 anos) |
|---|---|
| Administrativo | 462.000,00 € |
| Tecnologia | 277.000,00 € |
| Salários | 241.000,00 € |
| Impostos | 70.000,00 € |
| Segurança | 51.600,00 € |
| Marketing | 51.317,00 € |
| **Total Despesas** | **1.152.917,00 €** |

---

## 📊 Dashboard

![Dashboard Preview](https://github.com/diogovent/Financial-Analysis-Dashboard--Power-BI--PT/blob/main/Dashboard.png)

O dashboard apresenta os seguintes visuais:

**KPIs no topo:**
- **Total de Receitas:** 1,92M €
- **Total de Despesas:** 1,15M €
- **Margem de Lucro:** 39,96%

**Visuais incluídos:**
- **Top Segments (IA)** — segmentação automática por valor médio, identificando 7 segmentos distintos
- **Total de Receitas por Componente** — gráfico de barras horizontais ordenado por valor
- **Total de Despesas por Componente** — gráfico de linhas/área com linha de despesa média (192.152,83 €)
- **Tabela resumo por ano** — comparação de receitas e despesas por componente em 2019, 2020 e 2022

---

## 🧮 Medidas DAX

Total de Receitas:
```dax
Total_Receitas =
CALCULATE(
    SUM('DadosFinanceiros'[Valor]),
    'DadosFinanceiros'[Tipo] = "Receitas"
)
```

Total de Despesas:
```dax
Total_Despesas =
CALCULATE(
    SUM('DadosFinanceiros'[Valor]),
    'DadosFinanceiros'[Tipo] = "Despesas"
)
```

Margem de Lucro:
```dax
Margem_Lucro =
DIVIDE(
    [Total_Receitas] - [Total_Despesas],
    [Total_Receitas]
)
```

Lucro Total:
```dax
Lucro_Total = [Total_Receitas] - [Total_Despesas]
```

Despesa Média por Componente:
```dax
Despesa_Media =
CALCULATE(
    AVERAGEX(
        VALUES('DadosFinanceiros'[Componente]),
        CALCULATE(SUM('DadosFinanceiros'[Valor]))
    ),
    'DadosFinanceiros'[Tipo] = "Despesas"
)
```

---

## 🔍 Principais Conclusões

1. **As Vendas dominam as receitas** — representam mais de 70% do total de receitas (1,36M em 1,92M)

2. **A margem de lucro é saudável** — 39,96% indica que por cada euro de receita, quase 40 cêntimos ficam como lucro

3. **O Administrativo é a maior despesa** — representa 40% do total de despesas (462K em 1,15M)

4. **Crescimento consistente das receitas** — de 560K em 2019 para 755K em 2022, um crescimento de ~35%

5. **As despesas também cresceram** — de 287K em 2019 para 495K em 2022, pelo que a gestão de custos é um ponto a monitorizar

6. **Salários com crescimento acentuado** — passaram de 40K em 2019 para 124K em 2022, reflexo de crescimento da equipa

---

## 📌 Como Visualizar

1. Faz o download do ficheiro `.pbix` disponível neste repositório
2. Abre no **Power BI Desktop** (gratuito)
3. O ficheiro de dados `DadosFinanceiros.xlsx` está incluído no repositório

Ou então pode aceder por este link: https://app.powerbi.com/groups/me/reports/f1b1659c-e50e-4b8c-88be-ebcefc530607?pbi_source=desktop
---

## 👤 Autor

Desenvolvido como projecto de análise de dados para portfólio pessoal.

[![LinkedIn](https://www.linkedin.com/in/diogo-ventura-4981bb254/)
[![GitHub](https://github.com/diogovent)
