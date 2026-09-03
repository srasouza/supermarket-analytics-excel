<img width="800" height="288" alt="image" src="https://github.com/user-attachments/assets/7b97b542-2995-4976-b774-3f6d7af26402" />

# Projeto de Tratamento de Dados e Analytics no Excel

Este repositório contém o projeto de limpeza, padronização e análise visual de uma base de dados de vendas de supermercado, desenvolvido **100% no Microsoft Excel**.

## Origem dos Dados
A base de dados utilizada neste projeto foi extraída do **Kaggle**: 
[Supermart Grocery Sales - Retail Analytics Dataset](https://www.kaggle.com/datasets/mohamedharris/supermart-grocery-sales-retail-analytics-dataset). 
O dataset original contém o histórico de transações de vendas de uma rede de supermercados no estado de Tamil Nadu, Índia.

## Estrutura do Repositório e Download dos Arquivos

Para visualizar ou descarregar os arquivos oficiais deste projeto, aceda aos links abaixo diretamente no repositório:

*   **Arquivo Original (Dados Brutos):** [`data/raw/base_original.xlsx`](https://github.com/srasouza/supermarket-analytics-excel/tree/a0594060252cfb6f93a8b198a51b82ab71611b8f/dados/raw) — *Contém os dados concentrados em uma única coluna, com cabeçalhos em inglês e formatação regional norte-americana.*
*   **Arquivo Tratado (Base Final + Dashboard):** [`data/processed/base_tratada_final.xlsx`](https://github.com/srasouza/supermarket-analytics-excel/tree/a0594060252cfb6f93a8b198a51b82ab71611b8f/dados/raw) — *Contém a base limpa, traduzida, com novas métricas calculadas e a aba de relatórios com os gráficos.*

*   ## Etapas do Tratamento e Padronização dos Dados

O tratamento dos dados foi realizado no Microsoft Excel, com o objetivo de organizar a estrutura da base, padronizar os nomes das colunas e adequar os formatos dos dados para posterior análise.

### 1. Separação dos dados em colunas
Inicialmente, os dados estavam concentrados em uma única coluna. Os campos eram separados pelo caractere vírgula (,), porém o Excel ainda não os apresentava individualmente.
*   **Solução:** Foi realizada a separação do conteúdo em colunas utilizando o recurso **Texto para Colunas**, indicando a vírgula como delimitador.

### 2. Padronização dos nomes das colunas
Os títulos originais em inglês foram traduzidos e padronizados para o português usando o Google Translate e a ferramenta `Substituir`:

| Nome original | Nome utilizado |
| :--- | :--- |
| Order ID | ID Pedido |
| Customer Name | Nome Cliente |
| Category | Categoria |
| Sub Category | Sub Categoria |
| City | Cidade |
| Order Date | Data Pedido |
| Region | Região |
| Sales | Vendas |
| Discount | Desconto |
| Profit | Lucro |
| State | Estado |

### 3. Adequação dos tipos de dados
*   **Texto:** As colunas *ID Pedido, Nome Cliente, Categoria, Sub Categoria, Cidade, Região e Estado* foram alteradas para o formato **Texto**.
*   **Data Pedido (Correção Cronológica):** Apresentava o layout norte-americano (Mês/Dia/Ano). Utilizou-se o assistente **Texto para Colunas**, configurando a propriedade de Data sob a matriz de leitura **MDA**. Isto forçou a conversão exata para o padrão nacional de **Data abreviada** (Dia/Mês/Ano).
*   **Moeda:** As colunas *Vendas* e *Lucro* foram formatadas como **Moeda (R$)**.

### 4. Tratamento da coluna Desconto
A coluna apresentava valores com ponto decimal (ex: 0.12, 0.18).
1.  Utilizou-se a função **Substituir** para trocar o ponto (.) pela vírgula (,).
2.  A coluna foi formatada como **Porcentagem** (ex: `0,12` → `12%`).

### 5. Tradução e Localização de Categorias e Regiões
Utilizando a ferramenta **Substituir** e o auxílio temporário da função `ÚNICO` para mapeamento, os dados foram traduzidos:
*   **Regiões:**

| Valor original | Valor padronizado | Nº de substituições |
| -------------- | ----------------- | ------------------: |
| North          | Norte             |                   1 |
| South          | Sul               |               1.619 |
| West           | Oeste             |               3.203 |
| East           | Leste             |               2.848 |

*   **Categorias:**

|  Categoria original | Categoria padronizada | Nº de substituições |
| ------------------ | --------------------- | ------------------: |
| Oil & Masala       | Óleos e Especiarias   |               1.361 |
| Beverages          | Bebidas               |               1.400 |
| Food Grains        | Grãos e Cereais       |               1.398 |
| Fruits & Veggies   | Frutas e Legumes      |               1.418 |
| Bakery             | Padaria               |               1.413 |
| Snacks             | Snacks                |                   — |
| Eggs, Meat & Fish  | Ovos, Carnes e Peixes |               1.490 |

*   **Subcategorias:** Os termos *Chocolates* e *Cookies* foram mantidos por ampla compreensão no mercado brasileiro.
*   
| Subcategoria original | Subcategoria padronizada | Nº de substituições |
| :--- | :--- | :---: |
| Masalas | Temperos | 463 |
| Health Drinks | Bebidas Saudáveis | 719 |
| Atta & Flour | Farinhas | 353 |
| Fresh Vegetables | Vegetais Frescos | 354 |
| Organic Staples | Alimentos Orgânicos | 372 |
| Fresh Fruits | Frutas Frescas | 369 |
| Biscuits | Biscoitos | 459 |
| Cakes | Bolos | 452 |
| Chocolates | Chocolates | — |
| Eggs | Ovos | 379 |
| Cookies | Cookies | — |
| Chicken | Frango | 348 |
| Edible Oil & Ghee | Gordura Vegetal e Manteiga | 451 |
| Mutton | Carne de Carneiro | 394 |
| Soft Drinks | Refrigerantes | 681 |
| Dals & Pulses | Grãos e Lentilhas | 343 |
| Organic Vegetables | Vegetais Orgânicos | 347 |
| Noodles | Macarrão | 495 |
| Organic Fruits | Frutas Orgânicas | 348 |
| Fish | Peixe | 369 |
| Spices | Especiarias | 447 |
| Rice | Arroz | 330 |
| Breads & Buns | Pães e Pãezinhos | 502 |

### 6. Qualidade dos Dados (Duplicadas e Nulos)
*   **Remover Duplicadas:** Nenhuma linha duplicada foi encontrada. Cada linha representa uma transação única.
*   **Dados Ausentes:** Uma busca minuciosa com o recurso **Ir para Especial > Em branco** confirmou que a base possui **100% dos registros preenchidos** (zero lacunas).

### 7. Criação de Novas Variáveis
*   **Preço com Desconto:** Criada a coluna `J` com a fórmula `=H2-(H2*I2)` para calcular o faturamento real líquido em reais.
*   **Ano:** Criada coluna `G` com a fórmula `=ANO(F2)` para auxiliar com a função `=ANO()` para viabilizar o agrupamento temporal.

---

## Análise Visual e Criação de Gráficos (Dashboard)

Na nova aba `graficos`, foram gerados relatórios visuais gerenciais baseados em Tabelas Dinâmicas:

1.  **Faturamento por Região (Gráfico de Rosca):** Ilustra a participação de mercado. O *Oeste* lidera com R$ 3.719.836,08, seguido pelo *Leste* com R$ 3.282.291,46.
   <img width="800" height="400" alt="grafico_rosca" src="https://github.com/user-attachments/assets/71be6871-a3b4-4dd7-b1cb-d1ac907f7811" />

2.  **Faturamento por Categoria (Gráfico de Pizza):** Mede o desempenho por setor. As vendas são equilibradas, lideradas por *Ovos, Carnes e Peixes* (R$ 1.751.440,33) e *Snacks* (R$ 1.741.607,19).
   <img width="800" height="400" alt="grafico pizza" src="https://github.com/user-attachments/assets/feb09641-1bc5-43c4-8f6a-8d980a0ecd42" />

3.  **Ranking Top 5 Clientes (Gráfico de Barras):** Filtro avançado configurado  a partir do recurso nativo de Filtros de Valores da Tabela Dinâmica, configurando a opção Cinco Primeiros restrita aos dados superiores do faturamento líquido que foram adicionalmente ordenados de forma decrescente (do maior para o menor valor), permitindo a imediata identificação dos clientes estratégicos que geram maior receita para o negócio. Neste caso os 5 maiores compradores em ordem decrescente de receita.
   <img width="800" height="400" alt="grafico_barras" src="https://github.com/user-attachments/assets/5a94b329-bc5d-45e6-817f-9e05fe1115d5" />
   
4.  **Evolução Anual (Vendas vs. Lucro - Gráfico de Barras Duplas):** Gráfico de colunas agrupadas demonstrando crescimento consistente entre 2015 e 2018:
    *   **2015:** Faturamento R$ 2.298.854,44 | Lucro R$ 752.529,11
    *   **2018:** Faturamento R$ 3.855.027,83 | Lucro R$ 1.244.182,88
   <img width="800" height="400" alt="grafico_barra_duplas" src="https://github.com/user-attachments/assets/0f65540d-bc49-429a-919c-e2530d4d91c5" />

*Nota de Design: As legendas nativas foram limpas e reconstruídas manualmente com Formas e Caixas de Texto para garantir um visual Clean e profissional.*
