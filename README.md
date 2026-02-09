# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 9.2.2026

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


data = pd.read_csv('/content/global_sports_footwear_sales_2018_2026.csv')


data['order_date'] = pd.to_datetime(data['order_date'])


data = data.groupby('order_date')['final_price_usd'].sum().to_frame()


data['final_price_usd'] = data['final_price_usd'] - data['final_price_usd'].shift(1)


result = seasonal_decompose(
    data['final_price_usd'].dropna(),
    model='additive',
    period=12)

data['final_price_usd'] = result.resid


data['final_price_usd'] = np.log(data['final_price_usd'].abs() + 1)


data['final_price_usd'] = data['final_price_usd'] - data['final_price_usd'].shift(1)


result = seasonal_decompose(
    data['final_price_usd'].dropna(),
    model='additive',
    period=12
)
data['final_price_usd'] = result.resid


plt.figure(figsize=(16, 16))

plt.subplot(6, 1, 1)
plt.plot(data['final_price_usd'], label='Original')
plt.legend(loc='best')
plt.title('Original Data')
plt.xlabel('order_date')
plt.ylabel('final_price_usd')

plt.subplot(6, 1, 2)
plt.plot(data['final_price_usd'], label='Regular Difference')
plt.legend(loc='best')
plt.title('Regular Differencing')
plt.xlabel('order_date')
plt.ylabel('Differenced final_price_usd')

plt.subplot(6, 1, 3)
plt.plot(data['final_price_usd'], label='Seasonal Adjustment')
plt.legend(loc='best')
plt.title('Seasonal Adjustment')
plt.xlabel('order_date')
plt.ylabel('Seasonally Adjusted final_price_usd')

plt.subplot(6, 1, 4)
plt.plot(data['final_price_usd'], label='Log Transformation')
plt.legend(loc='best')
plt.title('Log Transformation')
plt.xlabel('order_date')
plt.ylabel('Log(final_price_usd)')

plt.subplot(6, 1, 5)
plt.plot(data['final_price_usd'], label='Log + Regular Differencing')
plt.legend(loc='best')
plt.title('Log Transformation and Regular Differencing')
plt.xlabel('order_date')
plt.ylabel('RDiff(Log(final_price_usd))')

plt.subplot(6, 1, 6)
plt.plot(data['final_price_usd'], label='Log + Regular + Seasonal Diff')
plt.legend(loc='best')
plt.title('Log Transformation, Regular & Seasonal Differencing')
plt.xlabel('order_date')
plt.ylabel('SDiff(RDiff(Log(final_price_usd)))')

plt.tight_layout()
plt.show()


data.plot(kind='line', title='Final Price USD Time Series')
plt.show()
```
### OUTPUT:
<img width="1648" height="277" alt="image" src="https://github.com/user-attachments/assets/e09bb2cd-7e83-4bbc-b5ba-faed67ec1e4e" />




### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
