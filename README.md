<div align="center">

# PM2.5 Forecast & Health Risk — Brazilian Metropolis

**End-to-end ML pipeline forecasting hourly PM2.5 concentrations and classifying public-health risk for the next 24 hours across 10 Brazilian cities.**

*English* · [Português](#-português)

</div>

> 🇧🇷 **Português:** pipeline completo de Machine Learning que prevê concentrações horárias de PM2.5 e classifica o risco à saúde (baixo, médio, alto) nas próximas 24 horas em 10 grandes cidades brasileiras. Usa APIs públicas, validação temporal, XGBoost otimizado com Optuna e interpretabilidade com SHAP.

## About

The project collects current public air-quality and weather data, engineers causal features, and trains regression and classification models to anticipate pollution peaks. It runs entirely in **Google Colab** — no local directory structure is required.

### Objectives

- Collect up-to-date atmospheric and meteorological data
- Predict PM2.5 for every horizon between 1 and 24 hours
- Classify risk as low, medium or high
- Identify potential pollution spikes in advance
- Produce information useful for health alerts and public policy
- Demonstrate a reproducible, executable Data Science pipeline

### Cities monitored

| City | State | City | State |
|---|---|---|---|
| São Paulo | SP | Recife | PE |
| Rio de Janeiro | RJ | Manaus | AM |
| Brasília | DF | Curitiba | PR |
| Belo Horizonte | MG | Porto Alegre | RS |
| Salvador | BA | Fortaleza | CE |

## Data sources

**Open-Meteo Air Quality API** — PM2.5, PM10, nitrogen dioxide, ozone, carbon monoxide, sulphur dioxide.

**Open-Meteo Weather API** — temperature, relative humidity, precipitation, pressure, cloud cover, wind speed and direction.

All requests include timeouts, response validation, automatic retries and explicit connection-failure handling.

## Pipeline architecture

```
Public APIs → Collection & validation → Cleaning & audit → Temporal/spatial EDA
  → Causal feature engineering → Temporal validation
      ├── Regression (PM2.5, 1–24 h)   └── Risk classification (low/medium/high)
                → SHAP & error analysis → Operational forecast
                → Alerts, dashboard & drift monitoring
```

### Feature engineering

- **Temporal:** hour, weekday, month, day of year, weekend flag, cyclic sine/cosine encoding, horizon hour and weekday
- **PM2.5 history:** lags of 1, 3, 6, 12, 24, 48, 72 and 168 hours; moving averages of 3, 6, 12, 24, 72 and 168 hours; moving standard deviations; 3 h and 24 h changes; PM2.5/PM10 ratio; robust extreme-concentration indicators
- **Meteorology & pollutants:** temperature and its trends, humidity and its trends, precipitation, pressure, cloud cover, wind speed, circular wind direction, other pollutant concentrations

Every historical feature is computed **causally**, using only information available at forecast time.

## Models

| Model | Role |
|---|---|
| **Persistence** | baseline — future concentration equals current |
| **Random Forest** | reference tree-based model capturing non-linear relations |
| **XGBoost** | primary regressor, hyperparameters tuned with Optuna |
| **XGBoost Classifier** | multiclass risk model with balanced class weights |

### Temporal validation

Random splits are deliberately **not** used, since they would let future information leak into training:

- Holdout on the 14 most recent days
- Four temporal validation folds, 7 days each
- 24-hour safety gap between train and validation
- Cities and horizons from the same instant grouped together
- Preprocessing fitted separately inside each fold

### Metrics

- **Regression:** MAE, RMSE, R², error per horizon, error per city, forecast bias, underestimation rate
- **Classification:** accuracy, balanced accuracy, F1 macro, F1 weighted, multiclass ROC-AUC, precision/recall per class, confusion matrix

Results are computed during execution because they depend on the query date and current API responses.

## Interpretability & monitoring

**SHAP** explains the XGBoost behaviour: global feature importance, impact direction, beeswarm plot, local explanation of the most severe alert and a waterfall plot breaking down positive and negative contributions.

**Population Stability Index (PSI)** compares the last 7 days with the reference history to detect drift:

| PSI | Interpretation |
|---|---|
| < 0.10 | stable |
| 0.10 – 0.25 | moderate drift — investigate |
| > 0.25 | significant drift — revalidate, possibly retrain |

## Tech stack

`Python` · `pandas` · `NumPy` · `requests` · `scikit-learn` · `XGBoost` · `Optuna` · `SHAP` · `Plotly` · `Matplotlib` · `Seaborn` · Google Colab

Reproducibility uses a global `SEED = 42`; results may still vary because of continuously updating APIs, library versions, atmospheric model changes and internal parallelisation.

## Limitations

Air-quality data are gridded atmospheric estimates and do not substitute certified surface stations. The recent history does not represent full annual seasonality; events such as fires, construction and traffic changes are not modelled directly; uncertainty intervals are empirical; and the project's risk thresholds are **operational, not diagnostic**.

## Responsible use

This is an analytical and educational tool. Its forecasts must **not** be used in isolation for medical, regulatory or emergency decisions. Official alerts should combine certified monitoring stations, expert assessment, health-authority protocols, meteorological and epidemiological evidence, and clear communication of uncertainty.

## 🇧🇷 Português

- **O que é:** pipeline de ML para prever PM2.5 horário (1–24 h) e classificar risco à saúde nas próximas 24 h em 10 capitais brasileiras.
- **Dados:** Open-Meteo Air Quality + Weather APIs, com timeout, validação, retentativas e tratamento de falhas.
- **Modelos:** persistência (baseline), Random Forest, XGBoost com Optuna e classificador XGBoost multiclasse com pesos balanceados.
- **Validação:** estritamente temporal — holdout de 14 dias, 4 folds, intervalo de segurança de 24 h e agrupamento por instante.
- **Interpretabilidade:** SHAP (importância global, beeswarm, waterfall, explicação local do alerta mais severo) e monitoramento de drift com PSI.
- **Como rodar:** abra o notebook no Google Colab e execute as células em ordem; nenhuma estrutura local é necessária.
- **Uso responsável:** ferramenta analítica e educacional — não substitui estações regulatórias, orientação médica nem protocolos oficiais.

> 📄 A documentação técnica detalhada (metodologia completa, métricas, limitações e uso responsável) está em [`DOCUMENTACAO_TECNICA.md`](DOCUMENTACAO_TECNICA.md).

## Author

[Vitoria AYRES](https://github.com/vitoriaayres)
