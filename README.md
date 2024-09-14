
---

# Traffic_Prediction

## Project Overview

This project focuses on predicting traffic volume using environmental and temporal features, such as temperature, weather conditions, and time of day. The aim is to build a simple and effective predictive model to assist with traffic management and planning.

## Dataset

The dataset used includes traffic volume data with key features:

- Temperature (K)
- Rainfall and snowfall (mm)
- Cloud cover (%)
- Time-related features (hour, day of the week, month)
- Traffic volume (target variable)

## Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/Kel-sie/traffic_prediction.git
   ```

2. Navigate to the project directory:

   ```bash
   cd Traffic_Prediction
   ```

3. Install the required Python packages:

   ```bash
   pip install -r requirements.txt
   ```

4. Ensure Jupyter Notebook is installed:

   ```bash
   pip install notebook
   ```

## Usage

To run the project, you need to open the Jupyter notebook and follow the steps for data exploration and prediction:

1. Launch Jupyter Notebook:

   ```bash
   jupyter notebook
   ```

2. Open the notebook named `Traffic_Prediction.ipynb` to see the following:

- **Data Cleaning**: Fixing missing values and adjusting incorrect values.
- **Feature Engineering**: Creating new features like `hour`, `dayofweek`, and `month` from the datetime column.
- **Exploratory Data Analysis**: Visualizing traffic volume distributions based on weather, time, and other factors.
- **Model Building**: Predicting traffic volume based on processed features.

## Key Code Highlights

### Data Exploration:

Plot of traffic volume by day of the week:

```python
sns.barplot(y="traffic_volume", x="dayofweek", data=df.groupby('dayofweek')['traffic_volume'].median().to_frame().reset_index())
plt.title('Median Hourly Traffic Volume by Day')
```

### Data Cleaning:

Adjusted incorrect weather values (e.g., implausibly high rainfall amounts):

```python
df.loc[df['rain_1h']>250, 'rain_1h'] = df['rain_1h']/100
```

Fixed missing or zero temperature values by replacing them with averages of nearby values:

```python
df.loc[(df['date_time'].dt.to_period('D')=='2014-02-02') & (df['temp']==0), 'temp'] = (255.37+255.62)/2
```

### Traffic Analysis:

Example plot of traffic volume by cloud cover:

```python
sns.barplot(y="traffic_volume", x="clouds_all", data=df.groupby('clouds_all')['traffic_volume'].mean().to_frame().reset_index())
plt.title('Traffic Volume by Cloud Cover')
```

## Results

### Key Insights:

- Traffic volume is influenced by **time of day** (peak during morning and evening rush hours).
- Weather conditions like **rain** and **snow** have an observable but moderate impact on traffic volume.
- **Clear weather** (no clouds) tends to have higher, more consistent traffic.

## Contributing

If you'd like to contribute, feel free to fork the repository, submit issues, or open pull requests.

## License


---
