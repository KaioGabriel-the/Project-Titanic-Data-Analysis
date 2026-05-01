# **Análise Exploratória de Dados do Dataset Titanic**

## **Resumo**

Este estudo apresenta uma análise exploratória de dados (EDA) aplicada ao dataset Titanic, com o objetivo de identificar os principais fatores que influenciaram a sobrevivência dos passageiros. Foram realizadas etapas de pré-processamento, engenharia de atributos, análise estatística e visualizações gráficas. Os resultados indicam que variáveis como sexo, classe social e presença de familiares tiveram impacto significativo na probabilidade de sobrevivência, enquanto a idade apresentou influência moderada.

---

## **1. Introdução**

O naufrágio do Titanic é um dos eventos históricos mais estudados em ciência de dados, sendo amplamente utilizado para análise preditiva e exploração de padrões. Este trabalho busca compreender quais características dos passageiros influenciaram suas chances de sobrevivência, utilizando técnicas de análise exploratória de dados.

---

## **2. Metodologia**

O processo de análise foi dividido em cinco etapas principais:

### **2.1 Importação dos Dados**

Os dados foram carregados em um DataFrame utilizando a biblioteca Pandas, contendo variáveis como idade, sexo, classe, tarifa e status de sobrevivência.

---

### **2.2 Limpeza e Pré-processamento**

Nesta etapa, foram realizadas transformações para preparar os dados para análise:

* Conversão de variáveis categóricas em numéricas utilizando One-Hot Encoding (ex: sexo e porto de embarque).
* Remoção de colunas irrelevantes.
* Conversão de valores booleanos para inteiros.

---

### **2.3 Engenharia de Atributos**

Foram criadas novas variáveis para enriquecer a análise:

* **FamilySize**: soma do número de familiares a bordo.
* **IsAlone**: variável binária indicando se o passageiro estava sozinho.
* **AgeGroup**: categorização da idade em faixas (criança, adolescente, adulto, meia-idade e idoso).

---

### **2.4 Análise Exploratória de Dados (EDA)**

Foram utilizadas estatísticas descritivas e agrupamentos (`groupby`) para identificar padrões entre variáveis e a sobrevivência.

---

### **2.5 Visualização de Dados**

Gráficos foram gerados com as bibliotecas Seaborn e Matplotlib, incluindo:

* Gráficos de contagem
* Gráficos de barras
* Heatmap de correlação
* Histogramas e boxplots

---

## **3. Resultados**

A análise revelou os seguintes padrões:

### **3.1 Taxa Geral de Sobrevivência**

Apenas aproximadamente **38,38%** dos passageiros sobreviveram ao desastre.

---

### **3.2 Influência do Sexo**

Observou-se uma diferença significativa entre os sexos:

* Mulheres: aproximadamente **74%** sobreviveram
* Homens: aproximadamente **19%** sobreviveram

Isso sugere a aplicação do protocolo de prioridade para mulheres e crianças.

---

### **3.3 Influência da Classe Social**

A classe do passageiro apresentou forte relação com a sobrevivência:

* 1ª classe: maior taxa de sobrevivência (~63%)
* 3ª classe: menor taxa (~24%)

Esse resultado evidencia a influência de fatores socioeconômicos.

---

### **3.4 Influência da Presença de Familiares**

A variável *IsAlone* indicou que:

* Passageiros acompanhados tiveram maior taxa de sobrevivência (~50%)
* Passageiros sozinhos tiveram menor taxa (~30%)

Isso sugere que a presença de familiares pode ter contribuído para melhores chances de resgate.

---

### **3.5 Influência da Idade**

A idade apresentou impacto moderado:

* Crianças tiveram maior taxa de sobrevivência (~53%)
* Idosos apresentaram menor taxa (~22%)

Apesar disso, a idade não se mostrou um fator tão determinante quanto sexo e classe social.

---

### **3.6 Análise de Correlação**

O mapa de correlação indicou que:

* A variável sexo feminino possui forte correlação positiva com sobrevivência.
* A classe social possui correlação negativa (quanto menor a classe, menor a chance de sobreviver).
* Estar sozinho também apresenta correlação negativa.

---

## **4. Discussão**

Os resultados confirmam padrões históricos conhecidos, como a priorização de mulheres e crianças e a influência de fatores socioeconômicos no acesso aos botes salva-vidas. Além disso, a análise mostra que a estrutura familiar teve papel relevante, possivelmente devido à cooperação entre passageiros.

---

## **5. Conclusão**

Este estudo demonstrou que a sobrevivência no Titanic foi influenciada principalmente por:

* Sexo (mulheres tiveram maior chance de sobrevivência)
* Classe social (passageiros de classes mais altas tiveram vantagem)
* Presença de familiares (acompanhamento aumentou a probabilidade de sobrevivência)

A idade apresentou influência secundária, indicando maior proteção a crianças, mas não sendo um fator determinante isolado.

---

## **6. Trabalhos Futuros**

Para aprofundar a análise, recomenda-se:

* Aplicação de modelos de machine learning para previsão de sobrevivência
* Análise de interação entre variáveis (ex: sexo + classe)
* Tratamento mais avançado de dados ausentes
* Testes estatísticos para validação dos insights

---

## **Palavras-chave**

Análise de Dados, Titanic, Machine Learning, EDA, Visualização de Dados
