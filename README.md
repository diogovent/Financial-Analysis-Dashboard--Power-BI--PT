# 💰 Financial-Analysis-Dashboard--Power-BI (PT)

> Análise financeira de receitas e despesas de uma empresa ao longo de 2019, 2020 e 2022, com foco na margem de lucro e evolução por componente.

---

## 📌 Índice

- Sobre o Projeto
- Objetivos da Análise
- Ferramentas Utilizadas
- Estrutura do Dataset
- Tratamento dos Dados
- Dashboard
- Medidas DAX
- Principais Conclusões
- Recomendações
- Como Visualizar

---

## 📁 Sobre o Projeto

Este projeto consiste numa análise financeira baseada em dados mensais de **receitas e despesas** de uma empresa, abrangendo os anos de **2019, 2020 e 2022**, não existe dados de 2021, infelizmente não encontrei a razão do porquê.

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
## 📂 Tratamento dos Dados

Antes de ter feito as medidas e analisar os dados precisei fazer um tratamento dos mesmo no Power BI para isso tive de acerder ao Power Query e vieram desta forma:

![Dashboard Preview](https://github.com/diogovent/Financial-Analysis-Dashboard--Power-BI--PT/blob/main/1.png)

Para resolver este problema precisei primeiro transformar o a primeira linha como o nome das colunas e mudar o tipo de coluna (em algumas) de texto para número decimal:

![Dashboard Preview](https://github.com/diogovent/Financial-Analysis-Dashboard--Power-BI--PT/blob/main/2.png)

Por ultimo precisei de criar uma coluna de "Datas" e outra de "Valor" sendo esta a única que tive de escrever um código próprio , uma vez que não havia uma maneira rápida de resolver o problema:

```dax
    = Table.UnpivotOtherColumns(#"Tipo Alterado1", {"Tipo", "Componente"}, "Data", "Valor")
```

Depois disto foi só passar a coluna de "Datas" que estava para texto transformei no tipo data:

![Dashboard Preview](https://github.com/diogovent/Financial-Analysis-Dashboard--Power-BI--PT/blob/main/3.png)

---

## 📊 Dashboard

![Dashboard Preview](https://github.com/diogovent/Financial-Analysis-Dashboard--Power-BI--PT/blob/main/Dashboard.png)

O dashboard apresenta os seguintes visuais:

**KPIs no topo:**
- **Total de Receitas:** 1,92M €
- **Total de Despesas:** 1,15M €
- **Margem de Lucro:** 39,96%

**Visuais incluídos:**
- **Top Segments (IA)** — Segmentação automática por valor médio, identificando 7 segmentos distintos
- **Total de Receitas por Componente** — Gráfico de barras horizontais que mostra que o principal componente é o da receita são as "Vendas" com acerca de 1.359 Milhões € (70,8%)
- **Total de Despesas por Componente** — Gráfico de linhas/área com uma linha de despesa média (192.152,83 €) e vemos que o principal componente das despesas
é o "Administrativo" que representa acerca de 40,1%
- **Tabela Resumo por Ano** — Comparação de receitas e despesas por componente em 2019, 2020 e 2022, não existe dados de 2021, por ter usado
o tipo de gráfico "Matriz" os totais da parte debaixo do gráfico representam o total da movimentação e não o lucro que a empresa teve

---

## 🧮 Medidas DAX

Total de Receitas:
```dax
Total de Receitas = CALCULATE(SUM(DadosFinanceiros[Valor]),DadosFinanceiros[Tipo]="Receitas")
```

Total de Despesas:
```dax
Total de Despesas = CALCULATE(SUM(DadosFinanceiros[Valor]),DadosFinanceiros[Tipo]="Despesas")
```

Margem de Lucro:
```dax
Margem de Lucro = DIVIDE([Lucro], [Total de Receitas], 0)
```

Lucro Total:
```dax
Lucro = [Total de Receitas] - [Total de Despesas]
```

---

## 🔍 Principais Conclusões

1. **As Vendas Dominam as Receitas** — Representam mais de 70% do total de receitas (1,36M em 1,92M)

2. **A Margem de Lucro é Saudável** — 39,96% indica que por cada euro de receita, quase 40 cêntimos ficam como lucro

3. **O Administrativo é a Maior Despesa** — Representa 40% do total de despesas (462K em 1,15M)

4. **Crescimento Consistente das Receitas** — Dos 560K em 2019 para 755K em 2022, um crescimento de ~35%

5. **As Despesas também Cresceram** — De 287K em 2019 para 495K em 2022, pelo que a gestão de custos é um ponto a monitorizar

6. **Salários com Crescimento Acentuado** — Passaram de 40K em 2019 para 124K em 2022, reflexo de crescimento da equipa

---

## 💡 Recomendações

1. **Controlar o Crescimento das Despesas**
    As despesas estão a crescer mais rápido que as receitas, o que está a pressionar a margem, então recomendo:
       Implementar medidas de controlo de custos, especialmente nas áreas com maior peso como o administrativo, para evitar a redução da rentabilidade
   
2. **Monitorizar a Margem de Lucro ao Longo do Tempo**
   A margem global é boa, mas tem tendência de queda, então recomendo:
       Criar acompanhamento regular da margem de lucro (mensal ou trimestral) para identificar desvios e agir atempadamente

3. **Reduzir Dependência das Vendas**
    As vendas representam mais de 70% das receitas → risco de concentração, então recomendo:
       Diversificar fontes de receita, reforçando áreas como licenciamento ou investimentos para tornar o negócio mais equilibrado

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
