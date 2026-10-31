[← Voltar ao README Principal](../README.md)

# 🧠 Laboratório de Ciência de Dados: Modelos no Titanic

Este diretório contém o pipeline de Machine Learning e modelagem estatística implementado no notebook [`titanic_models.ipynb`](titanic_models.ipynb). 

O propósito deste módulo transcende a simples predição de sobrevivência: trata-se de um laboratório abrangente que explora **quatro paradigmas essenciais de Ciência de Dados** utilizando os dados processados do Titanic ([`titanic_dashboard.csv`](../titanic_dashboard.csv)).

---

## 🧭 Estrutura do Módulo

```text
models/
├── README.md               # Documentação técnica e resultados dos modelos
└── titanic_models.ipynb    # Notebook interativo contendo pipelines, treinos e avaliações
```

---

## 🔬 Pipeline de Machine Learning

Para garantir reprodutibilidade e evitar vazamento de dados (*data leakage*), o fluxo segue as melhores práticas da indústria:

```mermaid
flowchart TD
    A[titanic_dashboard.csv] --> B[Seleção de Features & One-Hot Encoding]
    B --> C[Divisão Train / Val / Test (60% / 20% / 20%)]
    C --> D[StandardScaler ajustado no Treino]
    D --> E1[1. Regressão Logística - Classificação]
    D --> E2[2. Regressão Linear - Regressão & Coeficientes]
    B --> E3[3. Isolation Forest - Detecção de Anomalias]
    B --> E4[4. K-Means - Clusterização & Método do Cotovelo]
```

### Divisão dos Dados (Split 60 / 20 / 20)
- **Conjunto de Treino (60%)**: ~534 amostras para ajuste de pesos e parâmetros.
- **Conjunto de Validação (20%)**: ~178 amostras para calibração de hiperparâmetros e análise de limiares.
- **Conjunto de Teste (20%)**: ~179 amostras intocadas para avaliação de generalização final.

### Normalização
- Aplicação de `StandardScaler` ajustado **estritamente sobre o conjunto de treino** e aplicado aos conjuntos de validação e teste para variáveis numéricas contínuas (`Age`, `Fare`).

---

## 📊 Modelos Implementados e Resultados

### 1. Regressão Logística (Classificação Supervisionada)

- **Objetivo**: Estimar a probabilidade de sobrevivência ($P(Y=1|X)$) e classificar os passageiros.
- **Configuração**: `solver='lbfgs'`, `C=1.0`, penalização `L2`, `max_iter=1000`.
- **Desempenho**:
  - **Acurácia na Validação**: **~79,78%**
  - **Acurácia no Teste Final**: **~81,01%**
  - **Relatório de Classificação (Conjunto de Teste)**:
    - Classe 0 (Não sobreviveu): Precisão **0,83** | Recall **0,85** | F1-Score **0,84** (Suporte: 105)
    - Classe 1 (Sobreviveu): Precisão **0,78** | Recall **0,76** | F1-Score **0,77** (Suporte: 74)
- **Matriz de Confusão (Teste)**:
  - Verdadeiros Negativos (VN): **89**
  - Falsos Positivos (FP): **16**
  - Falsos Negativos (FN): **18**
  - Verdadeiros Positivos (VP): **56**
- **Ajuste de Limiar (*Threshold Tuning*)**: O notebook explora como a variação do limiar de decisão acima ou abaixo de `0.5` permite calibrar o compromisso entre *Recall* (resgatar o maior número possível de sobreviventes) e *Precision* (evitar falsos alarmes).

---

### 2. Regressão Linear (Modelagem Contínua & Discussão de Limitações)

- **Objetivo**: Ajustar uma função linear aos atributos dos passageiros para prever o desfecho contínuo.
- **Métricas na Validação**:
  - **Mean Squared Error (MSE)**: `0.1463`
  - **R² Score**: `0.3727`
- **Interpretação dos Coeficientes**:
  - **Intercepto ($\beta_0$)**: `+0.5936`
  - **`Sex_female`**: `+0.4834` (forte peso positivo para sobrevivência)
  - **`Pclass`**: `-0.1792` (forte peso negativo: classes numericamente maiores diminuem a chance)
  - **`Age`**: `-0.0303` (leve impacto negativo)
  - **`Fare`**: `+0.0071`
  - **`Embarked_C`**: `+0.1121`
  - **`Embarked_Q`**: `-0.0078`
  - **`IsAlone`**: `-0.0463`
- **Reflexão Crítica**: Destaca por que a regressão linear comum não é a abordagem ideal para probabilidades delimitadas entre 0 e 1, evidenciando a necessidade teórica de modelos logísticos/sigmoides.

---

### 3. Isolation Forest (Detecção de Outliers e Anomalias)

- **Objetivo**: Detectar perfis atípicos e transações anômalas no conjunto de dados sem supervisão de rótulo.
- **Configuração**: `contamination=0.05` (5%), `n_estimators=150`, `bootstrap=True`, `random_state=42`.
- **Resultados**:
  - **Dados Normais**: ~846 passageiros (95%)
  - **Outliers Detectados**: ~45 passageiros (5%)
- **Padrões dos Outliers**: Identificação automática de passagens com tarifas extraordinariamente altas (`Fare > 250`), passageiros idosos em classes econômicas e configurações familiares incomuns.

---

### 4. K-Means (Agrupamento / Aprendizado Não-Supervisionado)

- **Objetivo**: Segmentar passageiros em perfis comportamentais e socioeconômicos homogêneos.
- **Pré-processamento**: Imputação e padronização completa de todas as variáveis com `StandardScaler`.
- **Método do Cotovelo (*Elbow Method*)**:
  - Avaliação da Inércia (Soma dos Erros Quadráticos) para $K \in [1, 9]$.
  - Ponto de inflexão ótimo identificado em **$K = 3$**.
- **Perfis dos Clusters Formados ($K=3$)**:
  - **Cluster 0**: Passageiros da 3ª classe, com tarifas baixas e predominantemente desacompanhados.
  - **Cluster 1**: Passageiros da 1ª classe, tarifas elevadas, alta concentração de passageiros resgatados.
  - **Cluster 2**: Passageiros de perfis intermediários (2ª classe e famílias com crianças/jovens).

---

## 📋 Resumo Comparativo das Abordagens

| Abordagem | Algoritmo | Tipo de Aprendizado | Função Principal | Resultado / Métrica Chave |
| :--- | :--- | :--- | :--- | :--- |
| **Classificação** | Regressão Logística | Supervisionado | Predição binária da sobrevivência | **81,01% Acurácia** no Teste |
| **Regressão** | Regressão Linear | Supervisionado | Avaliação de pesos lineares das variáveis | MSE: `0.1463`, R²: `0.3727` |
| **Anomalias** | Isolation Forest | Não-Supervisionado | Isolamento de passageiros com padrões atípicos | **45 outliers** detectados (5%) |
| **Clusterização** | K-Means | Não-Supervisionado | Segmentação de grupos socioeconômicos | **$K=3$ clusters** via Elbow Method |

---

## 🛠️ Tecnologias e Bibliotecas

- **Python 3.10+**
- **Scikit-Learn**:
  - Modelos: `LogisticRegression`, `LinearRegression`, `IsolationForest`, `KMeans`
  - Pré-processamento e Métricas: `train_test_split`, `StandardScaler`, `confusion_matrix`, `classification_report`, `mean_squared_error`, `r2_score`
- **Pandas**: Estruturação dos dados e One-Hot Encoding
- **Matplotlib & Seaborn**: Curvas de cotovelo, matrizes de confusão e gráficos de dispersão

---

## 🚀 Como Executar

1. Instale as bibliotecas necessárias:
   ```bash
   pip install scikit-learn pandas matplotlib seaborn
   ```
2. Inicie o notebook:
   ```bash
   jupyter notebook models/titanic_models.ipynb
   ```
3. Execute as células sequencialmente. Certifique-se de que o arquivo [`titanic_dashboard.csv`](../titanic_dashboard.csv) esteja disponível no diretório raiz do projeto.

