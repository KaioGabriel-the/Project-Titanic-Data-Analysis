# 🧠 Laboratório de Ciência de Dados: Modelos no Titanic

Este diretório (`models/`) contém um pipeline de Machine Learning focado em diferentes abordagens fundamentais para o conjunto de dados do Titanic. O objetivo deste projeto não é apenas rodar um único modelo de previsão de sobrevivência, mas explorar um ecossistema completo de Machine Learning, servindo como um excelente "laboratório" prático de análise de dados.

## Por que este notebook existe?

O notebook `titanic_models.ipynb` foi estruturado para cobrir os principais tipos de tarefas em Ciência de Dados. As escolhas de modelo refletem um conhecimento bem estabelecido para níveis iniciantes a intermediários, compondo um pipeline coeso:

1. **Regressão Logística (Classificação)**
   - **O que faz:** Estima a probabilidade de um passageiro sobreviver com base em suas características.
   - **Por que existe:** É o coração das previsões de classificação. Permite o ajuste do limiar (threshold) — por exemplo, ajustando acima de 0.5 para equilibrar *Recall* (pegar mais sobreviventes) e *Precision* (evitar alarmes falsos).

2. **Regressão Linear (Regressão)**
   - **O que faz:** Tenta traçar a linha de melhor ajuste para prever variáveis numéricas contínuas.
   - **Por que existe:** Muito útil para aprendizado e para tentar prever variáveis como a Tarifa ou a Idade. Contudo, é importante notar que o problema do Titanic não é muito linear, o que serve como um ótimo ponto de reflexão e aprendizado prático sobre as limitações do modelo.

3. **Isolation Forest (Detecção de Outliers)**
   - **O que faz:** Isola pontos anômalos no conjunto de dados, como passagens caríssimas ou idades atípicas para a classe social.
   - **Por que existe:** Funciona incrivelmente bem de forma automática e sem necessidade de muitos ajustes. Aplicar detecção de anomalias enriquece o projeto e eleva o nível técnico do portfólio.

4. **K-Means (Clusterização/Agrupamento)**
   - **O que faz:** Agrupa passagens ou indivíduos em conjuntos semelhantes (ex: ricos com altas chances de sobrevivência, ou famílias numerosas).
   - **Por que existe:** Sobe o nível do projeto introduzindo aprendizado não-supervisionado. Mostra habilidade com padronização de dados (necessária para K-Means) e uso do método do cotovelo para definir o número ideal de agrupamentos (K).

---

> **Resumo:** Este repositório de modelos demonstra que construir projetos de dados vai muito além de treinar apenas um preditor: **trata-se de construir um pipeline de análise completo.**
