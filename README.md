# 🌱 Análise da Pegada de Carbono por Setor Industrial

Este projeto analisa a **pegada de carbono (Product Carbon Footprints - PCFs)** de produtos registrados por diversas empresas, com foco na comparação entre diferentes grupos industriais.

## 📊 Objetivo

Utilizar dados públicos da [Carbon Catalogue](https://www.nature.com/articles/s41597-022-01178-9) para:
- Identificar o número de empresas únicas em cada setor.
- Calcular a pegada de carbono total de cada grupo industrial.
- Filtrar os dados para o ano mais recente disponível.
- Ordenar os resultados pelos setores com maior emissão total.

## 🧮 Fonte de Dados

Os dados vêm de uma tabela chamada `product_emissions`, com a seguinte estrutura:

| Coluna                         | Tipo     | Descrição                                         |
|-------------------------------|----------|--------------------------------------------------|
| `id`                          | VARCHAR  | Identificador único do produto                   |
| `year`                        | INT      | Ano de referência dos dados                      |
| `product_name`                | VARCHAR  | Nome do produto                                  |
| `company`                     | VARCHAR  | Empresa fabricante                               |
| `country`                     | VARCHAR  | País de origem                                   |
| `industry_group`              | VARCHAR  | Grupo industrial do produto                      |
| `weight_kg`                   | NUMERIC  | Peso do produto em kg                            |
| `carbon_footprint_pcf`        | NUMERIC  | Pegada de carbono (CO₂ equivalente)              |
| `upstream_percent_total_pcf` | VARCHAR  | % das emissões na fase anterior à produção       |
| `operations_percent_total_pcf`| VARCHAR | % das emissões na fase de produção/operação      |
| `downstream_percent_total_pcf`| VARCHAR | % das emissões após a produção/distribuição      |

## 🧠 Etapas da Análise

1. **Importação dos dados** via `pandas` e criação de uma base SQLite em memória.
2. **Consulta SQL** para agrupar os dados por setor (`industry_group`), contar empresas únicas e somar a pegada de carbono.
3. Filtragem para o **ano mais recente** com:
   ```sql
   WHERE year IN (SELECT MAX(year) FROM ...)

    Ordenação dos resultados em ordem decrescente de emissões totais.

✅ Resultado Esperado
industry_group	num_companies	total_industry_footprint
Materials	3	107129.0
Capital Goods	2	94942.7
Technology Hardware & Equipment	4	21865.1
Food, Beverage & Tobacco	1	3161.5
Commercial & Professional Services	1	740.6
Software & Services	1	690.0
🛠️ Tecnologias Utilizadas

    Python 3

    pandas

    SQLite (via sqlite3)

    Google Colab / Jupyter Notebook

📁 Como Executar

    Clone o repositório ou abra o notebook no Google Colab.

    Certifique-se de ter o pandas e sqlite3 disponíveis.

    Execute as células em ordem para carregar os dados, montar o banco e gerar os resultados.

📌 Observações

    O DataFrame final gerado pela consulta foi nomeado como carbon_emissions_by_industry, conforme exigido na tarefa.

    As somas da pegada de carbono são arredondadas para uma casa decimal com ROUND(SUM(...), 1).

📚 Referência

    The Carbon Catalogue - Nature Scientific Data (2022)