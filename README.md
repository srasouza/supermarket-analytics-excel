# 📊 Projeto de Tratamento de Dados e Analytics no Excel

Este repositório contém o projeto de limpeza, padronização e análise visual de uma base de dados de vendas de supermercado, desenvolvido **100% no Microsoft Excel**.

## 📁 Estrutura do Repositório e Download dos Arquivos

Para visualizar ou descarregar os arquivos oficiais deste projeto, aceda aos links abaixo diretamente no repositório:

*   **📂 Arquivo Original (Dados Brutos):** [`data/raw/base_original.xlsx`](https://github.com/srasouza/supermarket-analytics-excel/tree/a0594060252cfb6f93a8b198a51b82ab71611b8f/dados/raw) — *Contém os dados concentrados em uma única coluna, com cabeçalhos em inglês e formatação regional norte-americana.*
*   **📂 Arquivo Tratado (Base Final + Dashboard):** [`data/processed/base_tratada_final.xlsx`](https://github.com/srasouza/supermarket-analytics-excel/tree/a0594060252cfb6f93a8b198a51b82ab71611b8f/dados/raw) — *Contém a base limpa, traduzida, com novas métricas calculadas e a aba de relatórios com os gráficos.*

*   ## 🛠️ Etapas do Tratamento e Padronização dos Dados

O tratamento dos dados foi realizado no Microsoft Excel, com o objetivo de organizar a estrutura da base, padronizar os nomes das colunas e adequar os formatos dos dados para posterior análise.

### 1. Separação dos dados em colunas
Inicialmente, os dados estavam concentrados em uma única coluna. Os campos eram separados pelo caractere vírgula (,), porém o Excel ainda não os apresentava individualmente.
*   **Solução:** Foi realizada a separação do conteúdo em colunas utilizando o recurso **Texto para Colunas**, indicando a vírgula como delimitador.

### 2. Padronização dos nomes das colunas
Os títulos originais em inglês foram traduzidos e padronizados para o português:

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
*   **Data Pedido (Correção Cronológica):** Apresentava o layout norte-americano (Mês/Dia/Ano). Utilizou-se o assistente **Texto para Colunas**, configurando a propriedade de Data sob a matriz de leitura **MDY**. Isto forçou a conversão exata para o padrão nacional de **Data abreviada** (Dia/Mês/Ano).
*   **Moeda:** As colunas *Vendas* e *Lucro* foram formatadas como **Moeda (R$)**.

### 4. Tratamento da coluna Desconto
A coluna apresentava valores com ponto decimal (ex: 0.12, 0.18).
1.  Utilizou-se a função **Substituir** para trocar o ponto (.) pela vírgula (,).
2.  A coluna foi formatada como **Porcentagem** (ex: `0,12` → `12%`).

### 5. Tradução e Localização de Categorias e Regiões
Utilizando a ferramenta **Substituir** e o auxílio temporário da função `ÚNICO` para mapeamento, os dados foram traduzidos:
*   **Regiões:** *North* → Norte (1), *South* → Sul (1.619), *West* → Oeste (3.203), *East* → Leste (2.848).
*   **Categorias:** *Oil & Masala* → Óleos e Especiarias, *Beverages* → Bebidas, *Food Grains* → Grãos e Cereais, *Fruits & Veggies* → Frutas e Legumes, *Bakery* → Padaria, *Eggs, Meat & Fish* → Ovos, Carnes e Peixes (*Snacks* mantido original).
*   **Subcategorias:** 23 subcategorias foram integralmente mapeadas e localizadas (ex: *Masalas* → Temperos, *Soft Drinks* → Refrigerantes). Os termos *Chocolates* e *Cookies* foram mantidos por ampla compreensão no mercado brasileiro.

### 6. Qualidade dos Dados (Duplicadas e Nulos)
*   **Remover Duplicadas:** Nenhuma linha duplicada foi encontrada. Cada linha representa uma transação única.
*   **Dados Ausentes:** Uma busca minuciosa com o recurso **Ir para Especial > Em branco** confirmou que a base possui **100% dos registros preenchidos** (zero lacunas).

### 7. Criação de Novas Variáveis
*   **Preço com Desconto:** Criada a coluna `J` com a fórmula `=H2-(H2*I2)` para calcular o faturamento real líquido em reais.
*   **Ano:** Criada coluna `G` para auxiliar com a função `=ANO()` para viabilizar o agrupamento temporal.

---

## 📈 Análise Visual e Criação de Gráficos (Dashboard)

Na nova aba `graficos`, foram gerados relatórios visuais gerenciais baseados em Tabelas Dinâmicas:

1.  **Faturamento por Região (Gráfico de Rosca):** Ilustra a participação de mercado. O *Oeste* lidera com R$ 3.719.836,08, seguido pelo *Leste* com R$ 3.282.291,46.
2.  **Faturamento por Categoria (Gráfico de Pizza):** Mede o desempenho por setor. As vendas são equilibradas, lideradas por *Ovos, Carnes e Peixes* (R$ 1.751.440,33) e *Snacks* (R$ 1.741.607,19).
3.  **Ranking Top Clientes:** Filtro avançado configurado para exibir apenas os 5 maiores compradores em ordem decrescente de receita.
4.  **Evolução Anual (Vendas vs. Lucro):** Gráfico de colunas agrupadas demonstrando crescimento consistente entre 2015 e 2018:
    *   **2015:** Faturamento R$ 2.298.854,44 | Lucro R$ 752.529,11
    *   **2018:** Faturamento R$ 3.855.027,83 | Lucro R$ 1.244.182,88

*Nota de Design: As legendas nativas foram limpas e reconstruídas manualmente com Formas e Caixas de Texto para garantir um visual Clean e profissional.*
