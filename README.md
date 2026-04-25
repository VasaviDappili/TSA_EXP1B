# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 21/04/2026

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on international airline passenger data
### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
### PROGRAM:
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose


data = pd.read_csv("C:/Users/admin/Downloads/Chocolate Sales (2).csv")

data.columns = data.columns.str.strip()

data['Date'] = pd.to_datetime(data['Date'], dayfirst=True)

data['Amount'] = data['Amount'].replace('[\$,]', '', regex=True).astype(float)

data.set_index('Date', inplace=True)

ts = data['Amount'].resample('M').mean().dropna()

ts_diff = ts - ts.shift(1)

result = seasonal_decompose(ts, model='additive', period=6)
ts_sea_diff = result.resid

ts_log = np.log(ts.replace(0, np.nan)).dropna()
ts_log_diff = ts_log - ts_log.shift(1)

result = seasonal_decompose(ts_log_diff.dropna(), model='additive', period=6)
ts_log_sea_diff = result.resid

plt.figure(figsize=(12,10))

plt.subplot(6,1,1)
plt.plot(ts)
plt.title("Original Time Series")

plt.subplot(6,1,2)
plt.plot(ts_diff)
plt.title("Differenced Series")

plt.subplot(6,1,3)
plt.plot(ts_sea_diff)
plt.title("Seasonal Adjusted")

plt.subplot(6,1,4)
plt.plot(ts_log)
plt.title("Log Transformed")

plt.subplot(6,1,5)
plt.plot(ts_log_diff)
plt.title("Log Differenced")

plt.subplot(6,1,6)
plt.plot(ts_log_sea_diff)
plt.title("Log Seasonal Adjusted")

plt.tight_layout()
plt.show()
```


### OUTPUT:

ORIGINAL TIME SERIES:
<img width="997" height="141" alt="image" src="https://github.com/user-attachments/assets/3e891f0e-5555-45a5-8c1b-8dc689a50ab9" />


DIFFERENCED SERIES:
<img width="991" height="138" alt="image" src="https://github.com/user-attachments/assets/e1e39b93-86ef-41be-a527-caaf8644c0fa" />


SEASONAL ADJUSTMENT:
<img width="991" height="136" alt="image" src="https://github.com/user-attachments/assets/f49c1493-8ff5-43c3-b01e-a35491addb5f" />


LOG TRANSFORMATION:
<img width="989" height="137" alt="image" src="https://github.com/user-attachments/assets/603334ef-dca5-4e49-ba4a-6893e29ecef5" />


LOG REGULAR DIFFERENCING:
<img width="986" height="138" alt="image" src="https://github.com/user-attachments/assets/aca1d79b-53ee-4b9c-954e-dd2db75a01ea" />


LOG SEASONAL ADJUSTMENT:
<img width="991" height="144" alt="image" src="https://github.com/user-attachments/assets/39f599d7-e492-41d8-93e9-3deba0895ba5" />


### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
