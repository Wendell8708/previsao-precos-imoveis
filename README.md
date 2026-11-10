# 🏠 Previsão de Preços de Imóveis na Califórnia

Projeto de Machine Learning que prevê o valor médio de imóveis na Califórnia a partir de dados socioeconômicos e geográficos, comparando modelos de regressão.

## Mapa de Preços
<img width="826" height="687" alt="image" src="https://github.com/user-attachments/assets/7454d31d-4409-4fdd-90cf-75df5ab28167" />


## 🎯 Objetivo

Construir e avaliar modelos capazes de estimar o preço médio dos imóveis de uma região, entendendo quais fatores mais influenciam esse valor.

## 📊 Dados

- **Fonte:** [California Housing Dataset](https://scikit-learn.org/stable/modules/generated/sklearn.datasets.fetch_california_housing.html), do censo dos EUA de 1990, disponível no scikit-learn
- **Tamanho:** 20.640 regiões e 8 variáveis
- **Alvo:** `MedHouseVal`, o valor médio dos imóveis (em US$ 100 mil)

| Variável | Descrição |
|---|---|
| MedInc | Renda média da região |
| HouseAge | Idade média dos imóveis |
| AveRooms | Média de cômodos por domicílio |
| AveBedrms | Média de quartos por domicílio |
| Population | População da região |
| AveOccup | Média de moradores por domicílio |
| Latitude / Longitude | Localização geográfica |

## 🔍 Análise exploratória

- **A renda é o fator mais ligado ao preço**, com correlação de 0,69. As demais variáveis têm correlação linear fraca.
- **A localização importa muito, mas de forma não linear.** Latitude e longitude têm correlação quase nula com o preço, mas o mapa mostra que os imóveis mais caros se concentram no litoral (São Francisco e Los Angeles). A correlação de Pearson só capta relações lineares, e o efeito da localização acontece em "manchas".
- **O dataset limita os preços a US$ 500 mil.** Todo imóvel acima desse valor foi registrado como 5.0.

## 🤖 Modelagem

1. Divisão treino/teste (80/20, `random_state=123`)
2. Padronização com `StandardScaler`, ajustado apenas no treino para evitar *data leakage*
3. Treinamento e comparação de três modelos

## 📈 Resultados

| Modelo | RMSE | MAE | R² |
|---|---|---|---|
| **Random Forest** | **0,499** | **0,324** | **0,813** |
| Gradient Boosting | 0,518 | 0,360 | 0,798 |
| Regressão Linear | 0,720 | 0,526 | 0,610 |

## Previsto x Real
<img width="661" height="691" alt="image" src="https://github.com/user-attachments/assets/1f09a8d3-bc44-4c03-83f7-fabde70a187c" />


## 💡 Conclusões

- O **Random Forest** teve o melhor desempenho: R² de 0,81 e erro médio (RMSE) de cerca de **US$ 50 mil**, contra US$ 72 mil da Regressão Linear.
- Modelos baseados em árvores capturam relações não lineares, como o efeito da localização, que a regressão linear não consegue representar.
- O teto de US$ 500 mil aparece como uma faixa vertical no gráfico de previsto x real e aumenta o erro nas regiões mais caras.

## 🚀 Próximos passos

- Ajustar hiperparâmetros (GridSearchCV)
- Remover ou tratar os registros limitados em 5.0
- Criar novas variáveis (ex.: distância até o litoral)
- Disponibilizar o modelo em um app interativo com Streamlit

## 🛠️ Tecnologias

Python · pandas · NumPy · scikit-learn · Matplotlib · Jupyter

## ▶️ Como executar

```bash
pip install pandas numpy scikit-learn matplotlib jupyter
jupyter notebook aimodel.ipynb
```

---

Desenvolvido por **Wendell Junior**
