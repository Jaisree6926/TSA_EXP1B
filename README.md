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
    plt.plot(sales_data['sales_log'], label='Log of Sales')
    plt.legend(loc='best')
    plt.title('Log Transformation')
    plt.xlabel('Date')
    plt.ylabel('Log(Sales)')
    
    plt.subplot(4, 1, 3)
    plt.plot(sales_data['sales_log_diff'], label='Diff(Log(Sales))')
    plt.legend(loc='best')
    plt.title('First Difference of Log Sales')
    plt.xlabel('Date')
    plt.ylabel('Diff(Log(Sales))')
    
    plt.subplot(4, 1, 4)
    plt.plot(sales_data['sales_log_seasonal_diff'], label='Seasonal Diff of Differenced Log Sales')
    plt.legend(loc='best')
    plt.title('Seasonal Differencing of Differenced Log Sales (Weekly)')
    plt.xlabel('Date')
    plt.ylabel('SDiff(RDiff(Log(Sales)))')
    
    plt.tight_layout()
    plt.show()
   


### OUTPUT:

**Original Sales Data:**

<img width="1322" height="269" alt="Screenshot (189)" src="https://github.com/user-attachments/assets/d2e79d20-8bc1-41e6-9ec4-4da3fd39daa3" />


**Log Transformation:**

<img width="1351" height="274" alt="Screenshot (190)" src="https://github.com/user-attachments/assets/7c715721-d1e6-465e-9f27-ea6f8145a301" />


**First difference of log sales:**

<img width="1333" height="277" alt="Screenshot (191)" src="https://github.com/user-attachments/assets/76aac7ae-0eee-4467-b5fa-534ad8eed581" />


**seasonal differences of Differenced log sales (weekly)**

<img width="1385" height="251" alt="Screenshot (194)" src="https://github.com/user-attachments/assets/77c305ed-33d8-4798-81df-e3615da8dfb8" />



### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
