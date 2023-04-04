# Battery-Capacity-estimation-Linear-regression-model

Here we have used the cumulative current method in discharge state to  estimate capacity for training dataset.

We have employed regression models to predict capacity.


Since the data used in the project is proprietary, we can't share it here. But you can use publicly available data.

[NASA Battery Data](https://www.nasa.gov/content/prognostics-center-of-excellence-data-set-repository)



# Data Description

The data contained battery charge and discharge data for four cells.

Cell_Id
- 005
- 006
- 007
- 018

To perform EDA, we first separated cells based on their unique cell ids.


# Feature selection

Since the original correlation between given(dataset) variables and capacity is very low, we had to create different features that made use of battery voltage and battery temperature.

Since current is constant in the discharge cycle, features relating to current are neglected 


# Capacity Calculation

If capacity is not specifically mentioned in the data, the code below can be used to calculate

```
#function to calculate capacity of each cell at each cycle
def capacity_calculation(dataframe):
    dataframe['q']=(dataframe['current_measured'] * (dataframe['time'].shift() - dataframe['time'])).cumsum()
    capacity = dataframe['q'].max() / 3600
    
    return capacity
    
```

### The data given to us showed a negative current in discharge.
So, we used cumsum.max to arrive at the value.
Based on the current sign, max() or min() can be selected alternatively.





# Model, Results

We checked different regression models and finally selected the elastic-net model.


![predicted_plots_corrected](https://user-images.githubusercontent.com/102144072/229741488-9acf9ffa-5f50-4da0-b8e0-150e4e88ee92.png)

### Final plots


![Final_output](https://user-images.githubusercontent.com/102144072/229743837-8f39d6b6-933f-4f28-864c-24539bf6f51a.png)

![cell_6](https://user-images.githubusercontent.com/102144072/229744363-cf5e4412-e19c-4787-947a-3f131fd867f9.png)


![cell_7](https://user-images.githubusercontent.com/102144072/229744443-49198898-2758-4a57-a972-49b1cf6e421c.png)

![cell_18](https://user-images.githubusercontent.com/102144072/229744476-a9b20bb8-10d3-46d2-a85c-e4031649a886.png)






