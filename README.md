# 🚗 Car Evaluation Dataset — Classificação com Machine Learning (Avaliação de Modelos)

## 📌 Visão Geral

Este projeto tem como objetivo aplicar técnicas de Machine Learning para prever a categoria de aceitação de um carro com base em suas características estruturais e de segurança.

O problema é tratado como uma tarefa de **classificação multiclasse**, onde o modelo deve classificar o carro em:

- unacc (inaceitável)
- acc (aceitável)
- good (bom)
- vgood (excelente)

---

## 🎯 Objetivo

Analisar e comparar diferentes modelos de Machine Learning para identificar qual apresenta melhor desempenho na classificação de carros, considerando também o impacto de desbalanceamento das classes.

---

## 📊 Dataset

- Fonte: [UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/19/car+evaluation)
- Tipo: Dados categóricos
- Variáveis: preço, manutenção, número de portas, capacidade de pessoas, segurança, entre outras

---

## 🔍 Análise Exploratória (EDA)

Foram realizadas as seguintes etapas:

- Visualização inicial dos dados (`head`, `shape`)
- Verificação de tipos de dados (`info`)
- Identificação de valores nulos (`isnull`)
- Análise de distribuição das variáveis (`value_counts`)
- Avaliação da distribuição da variável alvo

### ⚠️ Observação importante:
O dataset apresenta **desbalanceamento significativo**, com predominância da classe *unacc*.

---

## 🔄 Pré-processamento

- Conversão de variáveis categóricas para numéricas utilizando **Label Encoding**
- Separação entre variáveis independentes (X) e variável alvo (y)
- Divisão dos dados em treino e teste (80/20)

---

## 🧠 Modelos Testados

### 📌 Regressão Logística (Baseline)
- Acurácia aproximada: ~68%
- Desempenho fraco em classes minoritárias
- Modelo simples, usado como baseline
  

| Classe | Precision | Recall | F1-score | Support |
|--------|----------|--------|----------|----------|
| 0      | 0.32     | 0.16   | 0.21     | 77       |
| 1      | 0.00     | 0.00   | 0.00     | 15       |
| 2      | 0.73     | 0.95   | 0.83     | 237      |
| 3      | 0.50     | 0.06   | 0.11     | 17       |

---

### 🌳 Random Forest
- Acurácia aproximada: ~96%
- Bom desempenho geral
- Melhor equilíbrio entre classes
- Reduziu impacto do desbalanceamento


| Classe | Precision | Recall | F1-score | Support |
|--------|----------|--------|----------|----------|
| 0      | 0.94     | 0.94   | 0.94     | 77       |
| 1      | 0.91     | 0.67   | 0.77     | 15       |
| 2      | 0.99     | 1.00   | 0.99     | 237      |
| 3      | 0.79     | 0.88   | 0.83     | 17       |

---

### ⚖️ Técnicas de Balanceamento
- Random Forest + Oversampling
  - Accuracy: ~0.97

    | Classe | Precision | Recall | F1-score | Support |
    |--------|----------|--------|----------|----------|
    | 0      | 0.91     | 0.97   | 0.94     | 77       |
    | 1      | 0.91     | 0.67   | 0.72     | 15       |
    | 2      | 1.00     | 1.00   | 1.00     | 237      |
    | 3      | 0.75     | 0.88   | 0.81     | 17       |

  Observações
    - A acurácia aumentou levemente
    - Recall da classe 1 não melhorou
    - Indica que oversampling não resolveu o problema principal
  
- Random Forest + SMOTE
  - Accuracy: ~0.97
 
    | Classe | Precision | Recall | F1-score | Support |
    |--------|----------|--------|----------|----------|
    | 0      | 0.91     | 0.97   | 0.94     | 77       |
    | 1      | 0.91     | 0.60   | 0.72     | 15       |
    | 2      | 1.00     | 1.00   | 1.00     | 237      |
    | 3      | 0.75     | 0.88   | 0.81     | 17       |

     Observações
      - SMOTE não trouxe melhorias significativas
      - Em alguns casos, piorou o recall da classe minoritária
      - Mantém performance semelhante ao modelo original

📌 Resultado:
- Pequenas variações na acurácia
- Sem melhora significativa no recall das classes minoritárias

---

### 🚀 XGBoost
- Acurácia: ~98.5%
- Melhor desempenho geral
- Excelente performance nas classes minoritárias
- Modelo mais robusto entre os testados

| Classe | Precision | Recall | F1-score | Support |
|--------|----------|--------|----------|----------|
| 0      | 0.99     | 0.99   | 0.99     | 77       |
| 1      | 1.00     | 0.80   | 0.89     | 15       |
| 2      | 1.00     | 1.00   | 1.00     | 237      |
| 3      | 0.80     | 0.94   | 0.86     | 17       |

---

### ⚖️ SVM
- Acurácia: ~89%
- Baixo desempenho na classe minoritária
- Sensível ao desbalanceamento dos dados
- Desempenho inferior aos modelos baseados em árvores

| Classe | Precision | Recall | F1-score | Support |
|--------|----------|--------|----------|----------|
| 0      | 0.70     | 0.90   | 0.78     | 77       |
| 1      | 0.00     | 0.00   | 0.00     | 15       |
| 2      | 0.97     | 0.95   | 0.96     | 237      |
| 3      | 0.93     | 0.82   | 0.88     | 17       |

---

## 📊 Comparação Final dos Modelos

| Modelo               | Desempenho |
|---------------------|------------|
| Regressão Logística | Baixo      |
| Random Forest       | Bom        |
| XGBoost             | Excelente  |
| SVM                 | Fraco      |

---

## 🏁 Conclusão

Os modelos baseados em árvores, especialmente o **XGBoost**, apresentaram o melhor desempenho neste problema de classificação.

Modelos lineares e baseados em margem (como Regressão Logística e SVM) tiveram dificuldades em lidar com o desbalanceamento e a complexidade dos dados.

---

## 🧠 Principais Aprendizados

- Importância da análise de distribuição da variável alvo
- Impacto do desbalanceamento em modelos de classificação
- Diferença de comportamento entre tipos de modelos
- Nem sempre balanceamento melhora o desempenho
- Modelos baseados em árvores tendem a performar melhor em dados tabulares categóricos

---

## 🛠️ Tecnologias Utilizadas

- Python
- Pandas
- Scikit-learn
- XGBoost
- Google Colab


---

## 📌 Autor

Projeto desenvolvido para prática de Machine Learning e comparação de modelos em dados categóricos.
