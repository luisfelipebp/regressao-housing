# Análise de Preços de Casas na Califórnia

**Fonte dos Dados:** [California Housing Prices](https://www.kaggle.com/datasets/camnugent/california-housing-prices/data)

## Visão Geral do Projeto

Este projeto tem como objetivo realizar uma análise exploratória e construir modelos de regressão para prever os preços de casas na Califórnia. O conjunto de dados utilizado é baseado nos dados do censo de 1990 e contém informações sobre diversas características das residências em diferentes distritos da Califórnia.

A análise busca entender como fatores como localização, número de cômodos, idade da casa, proximidade do oceano e renda média da vizinhança influenciam o valor mediano das casas. Diversos algoritmos de machine learning são aplicados e comparados, tanto com quanto sem transformação logarítmica da variável alvo, para determinar o modelo com melhor desempenho na previsão dos preços.

## Etapas do projeto 

O notebook Jupyter (`regressao_housing.ipynb`) está estruturado da seguinte forma:

1.  **Introdução:** Apresentação do problema e dos objetivos do projeto.
2.  **Carregamento e Exploração Inicial dos Dados:**
    * Importação das bibliotecas necessárias.
    * Análise exploratória inicial.
3.  **Visualização dos Dados:**
    * Criação de gráficos para entender as distribuições das variáveis e as relações entre elas.
    * Análise da correlação entre as features e a variável alvo (preço da casa).
4.  **Pré-processamento dos Dados:**
    * Tratamento de valores ausentes.
    * **Transformação de variáveis:**
        * Aplicação de log para normalizar a distribuição do preço.
        * Uso dos dados sem transformação logarítmica da variável alvo.
    * Transformação de variáveis categóricas com OneHotEncoder (`ocean_proximity`).
5.  **Modelagem Preditiva:**
    * Implementação e treinamento de diversos modelos de regressão. Para cada modelo, foram testadas duas abordagens:
        * Com transformação logarítmica em variavéis com outliers significativos e na variável alvo.
        * Sem transformação logarítmica.
    * Modelos incluem:
        * XGBoost
        * CatBoost
        * LightGBM
        * Random Forest
        * Redes Neurais
        * Suporte Vector Regression (SVR)
        * Árvore de Decisão
        * Regressão linear múltipla
        * Regressão linear
    * Avaliação dos modelos utilizando métricas como R² (coeficiente de determinação) e RMSE (Raiz do Erro Quadrático Médio) tanto nos dados de treino quanto nos de teste.
    * Uso de validação cruzada para uma avaliação mais robusta do desempenho dos modelos.
6.  **Comparação e Análise dos Resultados:**
    * Tabelas comparativas do desempenho dos diferentes modelos para ambas as abordagens (com e sem transformação log).
    * Discussão sobre os resultados obtidos, destacando os modelos com melhor performance e o impacto da transformação logarítmica.
7.  **Conclusões:**
    * Resumo das principais descobertas.
    * Potenciais próximos passos e melhorias.
    * 
### Resultados com Transformação Logarítmica na Variável Alvo

A performance foi medida principalmente pelo R² e RMSE na escala original dos preços, com validação cruzada para R².

| Modelo                              | Score Treino/Teste | RMSE      | Validação Cruzada |
| :---------------------------------- | :----------------- | :-------- | :---------------- |
| Regressão com CatBoost              | 90.46%, 82.63%     | 47108.39  | 83.89%            |
| Regressão com XGBoost               | 93.52%, 83.04%     | 47585.61  | 83.60%            |
| Regressão com Light GBM             | 89.69%, 82.61%     | 48169.02  | 83.22%            |
| Regressão com Redes Neurais         | 85.54%, 80.04%     | 51628.53  | 64.35%            |
| Regressão com Random Forest         | 83.50%, 76.68%     | 55804.85  | 77.66%            |
| Regressão por Vetores de Suporte    | 76.56%, 75.43%     | 57289.15  | 75.82%            |
| Regressão com Árvore de Decisão     | 76.58%, 68.94%     | 64410.91  | 70.04%            |
| Regressão Linear Múltipla           | 64.32%, 64.95%     | 68420.36  | 64.35%            |
| Regressão Linear Simples (Latitude) | 2%, 2%             | 114380.97 | N/A               |
| Regressão Linear Simples (Population)| 0%, 0%             | 115566.47 | N/A               |

### Resultados da Regressão (Modelos com Transformação Logarítmica na Variável Alvo)

Resultados para modelos treinados com a variável alvo transformada por logaritmo. O RMSE é apresentado tanto na escala logarítmica quanto na escala original (revertida) para facilitar a comparação.

| Modelo                                      | Score Treino/Teste | RMSE (Escala Log) | RMSE (Escala Original) | Validação Cruzada |
| :------------------------------------------ | :----------------- | :---------------- | :--------------------- | :---------------- |
| Regressão com XGBoost (Log)                 | 94.44%, 84.42%     | 0.2250            | 48525.80               | 84.68%            |
| Regressão com CatBoost (Log)                | 91.93%, 84.57%     | 0.2240            | 48555.92               | 84.81%            |
| Regressão com Light GBM (Log)               | 91.48%, 84.37%     | 0.2254            | 48634.16               | 84.63%            |
| Regressão com Random Forest (Log)           | 89.84%, 81.13%     | 0.2477            | 53617.64               | 79.42%            |
| Regressão com Redes Neurais (Log)           | 87.14%, 80.92%     | 0.2490            | 54673.18               | 62.16%            |
| Regressão por Vetores de Suporte (Log)      | 80.36%, 78.68%     | 0.2631            | 56203.58               | 78.93%            |
| Regressão com Árvore de Decisão (Log)       | 82.26%, 73.82%     | 0.2917            | 61990.82               | 74.14%            |
| Regressão Linear Múltipla (Log)             | 68.55%, 69.23%     | 0.3162            | 67060.30               | 68.69%            |
| Regressão Linear Simples (Latitude - Log)   | 3%, 3%             | 0.5591            | 118614.58              | N/A               |
| Regressão Linear Simples (Population - Log) | 0%, 9%             | 0.5702            | 20089.30               |  N/A              |
