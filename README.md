# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on international airline passenger data
### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
### PROGRAM:

    import pandas as pd
    import numpy as np
    import matplotlib.pyplot as plt
    
    # Load your CSV file
    data = pd.read_csv(r'C:\Users\admin\OneDrive\Desktop\9. Sales-Data-Analysis.csv', parse_dates=['Date'], dayfirst=True)
    
    # -- 1. Aggregate daily sales for time series analysis --
    # The column 'Quantity' gives the sales figure for each transaction
    daily_sales = data.groupby('Date')['Quantity'].sum().sort_index()
    sales_data = daily_sales.to_frame(name='sales')
    
    # -- 2. Log transformation (avoid log(0)) --
    sales_data['sales_log'] = np.log(sales_data['sales'].clip(lower=1))
    
    # -- 3. Regular differencing --
    sales_data['sales_log_diff'] = sales_data['sales_log'].diff()
    
    # -- 4. Seasonal differencing (weekly seasonality: period=7) --
    sales_data['sales_log_seasonal_diff'] = sales_data['sales_log_diff'].diff(7)
    
    # -- 5. Plotting --
    plt.figure(figsize=(10, 10))
    
    plt.subplot(4, 1, 1)
    plt.plot(sales_data['sales'], label='Original Sales Data')
    plt.legend(loc='best')
    plt.title('Original Sales Data')
    plt.xlabel('Date')
    plt.ylabel('Sales')
    
    plt.subplot(4, 1, 2)
    plt.plot(sales_data['sales_log'], label='Regular Difference')
    plt.legend(loc='best')
    plt.title('Regular Difference')
    plt.xlabel('Date')
    plt.ylabel('Log(Sales)')
    
    plt.subplot(4, 1, 3)
    plt.plot(sales_data['sales_log_diff'], label='Diff(Log(Sales))')
    plt.legend(loc='best')
    plt.title('Seasonal Adjustment')
    plt.xlabel('Date')
    plt.ylabel('Diff(Log(Sales))')
    
    plt.subplot(4, 1, 4)
    plt.plot(sales_data['sales_log_seasonal_diff'], label='Log Transformation')
    plt.legend(loc='best')
    plt.title('Log Transformation')
    plt.xlabel('Date')
    plt.ylabel('SDiff(RDiff(Log(Sales)))')
    
    plt.tight_layout()
    plt.show()
    
    plt.figure(figsize=(12, 6))
    plt.plot(sales_data['sales'], label='Original Sales', alpha=0.7)
    plt.plot(sales_data['sales_log'], label='Log Sales', alpha=0.7)
    plt.plot(sales_data['sales_log_diff'], label='Diff(Log Sales)', alpha=0.7)
    plt.plot(sales_data['sales_log_seasonal_diff'], label='Seasonal Diff(Diff(Log Sales))', alpha=0.7)
    plt.title('Overview of Sales Data Transformations')
    plt.xlabel('Date')
    plt.ylabel('Value')
    plt.legend(loc='best')
    plt.grid(True)
    plt.show()
   


### OUTPUT:

**Original Sales Data:**
<img width="1293" height="332" alt="Screenshot (2)" src="https://github.com/user-attachments/assets/cbeba13c-e3fe-493c-a7b7-06ed445bf0c3" />


**Regular Difference:**

<img width="1324" height="301" alt="Screenshot (3)" src="https://github.com/user-attachments/assets/3c7c94a0-b537-4911-b842-733f3a0267f1" />


**Seasonal Adjustment:**


<img width="1304" height="310" alt="Screenshot (4)" src="https://github.com/user-attachments/assets/f3a9024d-6be4-4b7a-8fab-c88f2deed932" />


**Log Transformation**

<img width="1312" height="318" alt="Screenshot (5)" src="https://github.com/user-attachments/assets/63d6db51-ae53-48bc-bcde-c9ef64b451da" />

**Overview of Sales Data Transformations:**

<img width="1320" height="715" alt="Screenshot (6)" src="https://github.com/user-attachments/assets/4740af37-7dbe-4173-bfe9-6b4bb089dcc5" />


### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
