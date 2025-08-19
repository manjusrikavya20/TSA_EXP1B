# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 19/08/2025

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

data = pd.read_csv('airpassengers.csv')

data['Month'] = pd.to_datetime(data['Month'])
data.set_index('Month', inplace=True)

data['passengers_diff'] = data['#Passengers'] - data['#Passengers'].shift(1)

result = seasonal_decompose(data['#Passengers'], model='additive', period=12)
data['passengers_sea_diff'] = result.resid

data['passengers_log'] = np.log(data['#Passengers'])

data['passengers_log_diff'] = data['passengers_log'] - data['passengers_log'].shift(1)

result = seasonal_decompose(data['passengers_log_diff'].dropna(), model='additive', period=12)
data['passengers_log_seasonal_diff'] = result.resid

plt.figure(figsize=(16, 18))

plt.subplot(6, 1, 1)
plt.plot(data['#Passengers'], label='Original')
plt.legend(loc='best')
plt.title('ORIGINAL')

plt.subplot(6, 1, 2)
plt.plot(data['passengers_diff'], label='Regular Differencing')
plt.legend(loc='best')
plt.title('REGULAR DIFFERENCING')

plt.subplot(6, 1, 3)
plt.plot(data['passengers_sea_diff'], label='Seasonal Adjustment')
plt.legend(loc='best')
plt.title('SEASONAL ADJUSTMENT')

plt.subplot(6, 1, 4)
plt.plot(data['passengers_log'], label='Log Transformation')
plt.legend(loc='best')
plt.title('LOG TRANSFORMATION')

plt.subplot(6, 1, 5)
plt.plot(data['passengers_log_diff'], label='Log Transformation + Regular Differencing')
plt.legend(loc='best')
plt.title('LOG TRANSFORMATION + REGULAR DIFFERENCING')

plt.subplot(6, 1, 6)
plt.plot(data['passengers_log_seasonal_diff'], label='Log Transformation + Regular & Seasonal Differencing')
plt.legend(loc='best')
plt.title('LOG TRANSFORMATION + REGULAR & SEASONAL DIFFERENCING')

plt.tight_layout()
plt.show()
```

### OUTPUT:

<img width="1515" height="287" alt="image" src="https://github.com/user-attachments/assets/ec10899e-334e-4bc2-877e-c716aecda125" />

REGULAR DIFFERENCING:

<img width="1489" height="281" alt="image" src="https://github.com/user-attachments/assets/c6ff524f-4c68-4919-973d-88d4d2f89c59" />

SEASONAL ADJUSTMENT:

<img width="1505" height="281" alt="image" src="https://github.com/user-attachments/assets/c04ef72f-100c-4157-a7ce-c27c67a2b746" />

LOG TRANSFORMATION:

<img width="1505" height="281" alt="image" src="https://github.com/user-attachments/assets/fdf2760f-47a2-472c-a5c1-9f24eff33f32" />

LOG TRANSFORMATION AND REGULAR DIFFERENCING:

<img width="1499" height="281" alt="image" src="https://github.com/user-attachments/assets/e804832b-3208-4ebc-acf3-e2107ef300e6" />

LOG TRANSFORMATION + REGULAR & SEASONAL DIFFERENCING:

<img width="1520" height="303" alt="image" src="https://github.com/user-attachments/assets/fe896a7c-8d8e-49cb-912b-eecd57562a80" />

### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
