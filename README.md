# Analysis and Forecasting of HBO Max Content

An analytical project focused on examining the dynamics of the HBO/HBO Max film and series library using time series models.

---

## About the Project

The aim of this project is to analyze the historical release trends of the HBO platform and to build a mathematical **ARIMA (AutoRegressive Integrated Moving Average)** model that enables forecasting the number of new titles in the coming years.

The project combines elements of:
- Data engineering  
- Descriptive statistics  
- Machine learning (time series analysis)

The motivation behind this project was personal interest in streaming platforms as a form of entertainment, along with curiosity about available data and whether future content production trends can be predicted.

---

## Dataset

The dataset comes from Kaggle:

https://www.kaggle.com/datasets/thedevastator/hbo-and-hbo-max-content-dataset/data

It provides a comprehensive overview of HBO and HBO Max content libraries, including metadata for thousands of productions.

### Features:
- **title** – Full name of the film or series  
- **type** – Content classification (Movie or TV series)  
- **year** – Year of release  
- **imdb_score & imdb_votes** – Popularity and rating indicators  
- **genres** – Thematic categories  
- **rating** – Age classification  

---

## Technologies Used

- Python 3.x  
- Pandas & NumPy – data processing  
- Matplotlib & Seaborn – data visualization  
- Statsmodels – statistical analysis (ADF test, ACF/PACF, ARIMA)  
- Scikit-learn – model evaluation (MAE, RMSE, MAPE)  

---

## Workflow

### 1. Data Preparation and Cleaning
- Loaded data from `HBO_Content.csv` and `HBO_MAX_Content.csv`  
- Filled missing values in the `type` column (default: "Movie")  
- Merged datasets and removed duplicates  
- Converted data into a time series with a yearly index  

### 2. Exploratory Data Analysis (Stationarity)
- Identified a strong upward trend after 2010  
- Performed **ADF test** → data was non-stationary  
- Applied:
  - Log transformation  
  - Differencing (1st and 2nd order)  

### 3. ARIMA Modeling
- Used **ACF** and **PACF** plots  
- Optimized model using **AIC criterion**  
- Selected model: **ARIMA(2,1,2)**  
- Split data:
  - Training set: 80%  
  - Test set: 20%  

### 4. Model Evaluation
- Residual diagnostics (white noise, normality)  
- Error metrics:
  - MAE  
  - RMSE  
  - MAPE  

---

## Results & Insights

- **Rapid growth** in content production after 2010  
- **Model accuracy**: ARIMA(2,1,2) correctly captures trend direction  
- **Mean reversion** observed in long-term forecasts (typical for ARIMA)  
- **Confidence intervals (95%)** provide optimistic and pessimistic scenarios  

---

## Project Structure
- projekt_analiza_hbomax.py # Analysis script
- HBO_Content.csv # HBO dataset
- HBO_MAX_Content.csv # HBO Max dataset
- README.md # Project documentation

## ▶️ How to Run

### 1. Install dependencies
```bash
pip install pandas matplotlib seaborn statsmodels scikit-learn
```
### 2. Run the script
```bash
python projekt_analiza_hbomax.py
```
