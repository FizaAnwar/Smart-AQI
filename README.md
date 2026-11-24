# 🌫️ Smart AQI Predictor

A machine-learning dashboard that forecasts the **next 72 hours of air quality (US AQI)** for **Islamabad**, using live air-quality and weather data.

🔗 **Live app:** [smartaqipredictor.streamlit.app](https://smartaqipredictor.streamlit.app/)

---

## Features

- **Live 72-hour forecast** starting from the current hour, refreshed hourly
- **Current AQI** with category and health guidance
- **Model comparison** (Ridge, Random Forest, LSTM) using MAE and RMSE
- **Random Forest feature importance**
- **Forecast explorer** with a table and CSV download
- **Automatic fallback** to the saved forecast file if the live data source is unavailable

## How it works

1. **Data:** hourly AQI and weather are downloaded from the free [Open-Meteo](https://open-meteo.com/) Air Quality and Weather APIs (no API key needed).
2. **Features (18):** weather variables (temperature, humidity, precipitation, pressure, wind speed and direction), time features (hour, day of week, month, weekend flag), AQI lags (1, 3, 6, 12, 24 h), and 6 h / 24 h rolling statistics.
3. **Forecasting:** the Random Forest predicts one hour ahead, and each prediction is fed back in as input for the next hour, repeated 72 times.
4. **Dashboard:** built with Streamlit and Plotly.

## AQI categories

| AQI | Category |
|---|---|
| 0–50 | Good |
| 51–100 | Moderate |
| 101–150 | Unhealthy for Sensitive Groups |
| 151–200 | Unhealthy |
| 201–300 | Very Unhealthy |
| 301+ | Hazardous |

## Project structure

```
smart-aqi/
├── app/            # Streamlit dashboard (app.py)
├── data/           # Processed data and saved predictions
├── model/          # Trained models (Random Forest, Ridge, LSTM scaler)
├── notebooks/      # 01_EDA.ipynb – exploratory data analysis
├── src/            # Training, comparison and forecasting scripts
├── requirements.txt
└── README.md
```

## Run locally

```bash
git clone https://github.com/FizaAnwar/smart-aqi.git
cd smart-aqi

python3 -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate

pip install -r requirements.txt
streamlit run app/app.py
```

## Tech stack

Python · Streamlit · scikit-learn · pandas · NumPy · Plotly · Open-Meteo API

## Limitations

- Forecasts are statistical estimates, not official air-quality advisories.
- Models were trained on a limited period of data, so accuracy may drop as seasons change. Retrain periodically on recent data.
- Because each hour feeds the next, errors can build up toward the end of the 72-hour window.

## Author

**Fiza Anwar** · [@FizaAnwar](https://github.com/FizaAnwar)
