# Comparação de Algoritmos de Aprendizado Supervisionado para Predição de Diabetes

Comparação experimental entre quatro algoritmos de classificação — **KNN**, **SVM**, **Árvore de Decisão** e **MLP** — aplicados à predição de diabetes a partir de indicadores de saúde comportamentais (dataset BRFSS 2015).

Este repositório acompanha o artigo *"Comparação de Algoritmos de Aprendizado Supervisionado Aplicados à Predição de Diabetes"*, submetido ao **III Simpósio Jornadas de Aprendizagem e Inteligência Artificial** (Centro Universitário SENAI Paraná, Edital nº 16/2026), e disponibiliza o código-fonte completo para fins de reprodutibilidade.

## Dataset

- **Fonte:** [Diabetes Health Indicators Dataset](https://www.kaggle.com/datasets/alexteboul/diabetes-health-indicators-dataset) (Kaggle), derivado do *Behavioral Risk Factor Surveillance System* (BRFSS 2015).
- **Registros:** 253.680 | **Atributos:** 21 + variável-alvo (binária: diabético / não diabético).
- **Desbalanceamento:** ~86% negativos vs. ~14% positivos.

O dataset não é versionado neste repositório (ver `.gitignore`); o script baixa o arquivo automaticamente via `gdown` a partir de um link público do Google Drive.

## Metodologia

1. **Pré-processamento:** imputação de valores ausentes, codificação one-hot de variáveis nominais, padronização de variáveis numéricas.
2. **Divisão dos dados:** holdout em treino (70%), validação (10%) e teste (20%).
3. **Balanceamento:** SMOTE (*Synthetic Minority Over-sampling Technique*) aplicado no pipeline de treino de todos os modelos.
4. **Modelos treinados:**
   - K-Nearest Neighbors (k=5, threshold ajustado a 0,65)
   - Support Vector Machine (LinearSVC + calibração de probabilidade)
   - Árvore de Decisão (max_depth=10, min_samples_leaf=20)
   - Multi-Layer Perceptron (camadas ocultas 64/32, ativação ReLU)
5. **Avaliação:** acurácia, precisão, recall e F1-score na validação; avaliação final no conjunto de teste restrita ao modelo de melhor desempenho (SVM).

As métricas completas, gráficos e a discussão crítica dos resultados — incluindo as limitações metodológicas do experimento (ausência de estratificação, SMOTE não padronizado entre modelos, ausência de busca de hiperparâmetros via GridSearchCV, entre outras) — estão detalhadas no artigo científico.

## Estrutura do repositório

```
diabetes-classificacao-ml/
├── notebook/
│   ├── comparacao_algoritmos_diabetes.py     # script original (formato Colab)
│   └── comparacao_algoritmos_diabetes.ipynb  # mesmo conteúdo, em notebook Jupyter
├── requirements.txt
├── LICENSE
└── README.md
```

## Como executar

```bash
git clone https://github.com/cabral-e/diabetes-classificacao-ml.git
cd diabetes-classificacao-ml
pip install -r requirements.txt
jupyter notebook notebook/comparacao_algoritmos_diabetes.ipynb
```

O notebook é autocontido: basta executar as células em ordem. O download do dataset é automático.

## Origem do código

O experimento foi originalmente desenvolvido em grupo (Trabalho Prático da disciplina de Aprendizado de Máquina Supervisionado, 2026.2BI, Grupo 7). Esta versão foi organizada, documentada e disponibilizada por **Edgar de Oliveira Cabral Filho** como material de apoio ao artigo científico de sua autoria individual submetido ao III Simpósio de IA.

## Citação

Se este código for útil em outro trabalho, considere citar o artigo correspondente:

> CABRAL FILHO, Edgar de Oliveira. *Comparação de Algoritmos de Aprendizado Supervisionado Aplicados à Predição de Diabetes*. III Simpósio Jornadas de Aprendizagem e Inteligência Artificial, Centro Universitário SENAI Paraná, 2026.

## Licença

Distribuído sob licença MIT — ver [LICENSE](LICENSE).
