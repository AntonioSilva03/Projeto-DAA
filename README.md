# Projeto-DAA - Previsão de Progressão de MCI para AD

Este repositório reúne o relatório e os artefatos relativos ao projeto desenvolvido para a cadeira de Dados e Aprendizagem Automática (DAA) no Mestrado em Engenharia Informática – 2024/2025, com foco na previsão da progressão de Déficit Cognitivo Leve (MCI) para Doença de Alzheimer (AD).

O trabalho é dividido em duas tarefas fundamentais:

- **Tarefa de Análise e Validação**: Exploração, análise e tratamento dos datasets.

- **Tarefa de Competição**: Desenvolvimento e otimização de modelos de Machine Learning para realizar a previsão, com avaliação de desempenho por meio de métricas (accuracy, precision, F1-score) e benchmarks na plataforma Kaggle.

## Introdução

O projeto tem como objetivo desenvolver modelos de Machine Learning capazes de prever, com sucesso, a progressão de MCI para AD. A partir de características radiômicas obtidas em imagens de ressonância magnética, foram explorados dois conjuntos de dados:

- **DSHippo (Hipocampo)**: Supostamente com maior relevância preditiva devido à importância do hipocampo na memória.

- **DSOcc (Lobo Occipital)**: Incluído para comparação, mas demonstrou desempenho inferior na previsão.

A hipótese central é que o dataset do hipocampo é o mais adequado para a previsão, dado o seu potencial preditivo.

## Metodologia

Para conduzir o estudo, foi adotada a metodologia **SEMMA** (Sample, Explore, Modify, Model, Assess):

- **Sample**: Seleção de amostras representativas dos datasets.

- **Explore**: Realização de análises estatísticas e comparativas dos dados (ex.: distribuições de idade, sexo e transições).

- **Modify**: Tratamento dos dados, incluindo remoção de colunas desnecessárias, normalização e transformação dos dados.

- **Model**: Desenvolvimento de múltiplos modelos de aprendizagem supervisionada.

- **Assess**: Avaliação dos modelos com métricas como accuracy, precision e F1-score, utilizando GridSearchCV para otimização dos hiperparâmetros.

## Análise e Exploração dos Datasets
- Comparação Inicial:

  - Ambos os datasets (DSHippo e DSOcc) contêm 305 pacientes e apresentam o mesmo número de colunas, embora com diferenças significativas nos valores, exceto em algumas variáveis (ex.: ID, imagem, transição e sexo).

- Estatísticas Exploratórias:

  - Idade (Age): Distribuição semelhante entre treino e teste, concentrada entre 56 e 90 anos.
  
  - Sexo (Sex): Predominância do mesmo sexo em determinadas transições.
  
  - Transição (Transition): Evidenciou-se que a classe CN-CN é a mais representada, enquanto CN-MCI aparece em menor quantidade, o que dificulta a previsão.

## Tratamento dos Dados
- Remoção de Colunas Desnecessárias:

  - Foram eliminadas colunas com valores únicos ou redundantes e todas as colunas do tipo object (exceto a variável target “Transition”).

- Normalização:

  - Utilizou-se o MinMaxScaler para normalizar as variáveis numéricas entre 0 e 1, facilitando o desempenho dos modelos, principalmente os baseados em ensemble.

- Redução de Dimensionalidade:

  - RFECV: Para eliminação iterativa de features irrelevantes.

  - PCA: Para transformar as features selecionadas em componentes principais, reduzindo de cerca de 1650 (hipocampo) para 90 componentes e similarmente para o dataset occipital.
 
## Modelos Desenvolvidos
Foram implementados e otimizados diversos modelos de Machine Learning:

- Decision Tree Classifier (DTC)

- Random Forest Classifier (RFC)

- Support Vector Machine (SVM)

- Gradient Boost Classifier (GBC)

- XGBoost Classifier (XGBC)

- Multi-Layer Perceptron Classifier (MLP)

- Stacking Classifier (STC): Com diferentes configurações utilizando múltiplos modelos base.

- Max Voting Classifier (MVC): Modelo ensemble que combina as previsões por votação ponderada.

Cada modelo passou por um processo extenso de otimização de hiperparâmetros por meio de GridSearchCV, com random seed fixo (2023) para consistência.

## Resultados e Análise Crítica
- Dataset Hipocampo (DSHippo):

  - Os modelos atingiram accuracies locais de até 0.56.
  
  - Destaca-se a melhor performance do SVM no Kaggle (F1-macro de 0.47565), embora com sinais de overfitting.

- Dataset Occipital (DSOcc):

  - Apresentou resultados significativamente inferiores, confirmando a hipótese de que o hipocampo é o dataset mais relevante para esta tarefa.

- Insights dos Modelos Ensemble:

  - Técnicas como Stacking e Max Voting demonstraram melhorar a robustez das previsões, apesar de desafios na transição MCI-AD e na baixa representatividade de CN-MCI.

- Observações Gerais:

  - A combinação de RFECV e PCA foi crucial para reduzir a dimensionalidade e melhorar a performance dos modelos.

  - O uso extensivo de GridSearch permitiu uma escolha mais assertiva dos hiperparâmetros, mesmo com o custo computacional elevado.

## Conclusão e Recomendações
- Conclusões:

  - O dataset do hipocampo é comprovadamente mais adequado para a previsão da progressão de MCI para AD que o dataset do occipital.
  
  - Técnicas de pré-processamento (remoção de colunas, normalização, RFECV e PCA) melhoraram significativamente a qualidade dos dados e o desempenho dos modelos.
  
  - Apesar dos desafios de overfitting e da baixa representatividade em algumas classes, os modelos ensemble se mostraram promissores.

- Recomendações Futuras:

  - Aumento da Base de Dados: Coletar mais amostras, especialmente para transições menos representadas (ex.: CN-MCI, MCI-AD).

  - Modelos Avançados: Investigar o uso de redes neurais profundas ou métodos híbridos.

  - Cross-Validation Robusta: Implementar métodos mais robustos (por exemplo, stratified cross-validation) para reduzir overfitting.

  - Integração de Dados Clínicos: Incluir informações clínicas adicionais para enriquecer as features e melhorar a predição.
