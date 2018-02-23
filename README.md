# HackerCamp-Summer-2018-Submission---Analytics-
Innovaccer

Hi! My name is Kartikeya Chouhan. I am a B.Tech undergraduate from IIT Roorkee.
Below is the Python 3.6 code to solve the Analytics Assignent.

# importing the necessary Libraries
import numpy as np
import pandas as pd

#reading the csv file

headings  = ['Last_name', 'Date_of_birth', 'Gender', 'First_name']
data = pd.read_csv('D:/ML/Deduplication Problem - Sample Dataset.csv', names = headings, skiprows = 1)

# defining a fuction to sort and remove dupicate names through dictionary
def sort_remove(data):
    
    # adding a new colums to sort and remove duplicate
    data['Full_name'] = data['First_name'] + data['Last_name'] + data['Date_of_birth']
    
    output = {}
    
    # using the new column as key to form the dictionary with the
    # values of original dataset
    
    for i in range(0, 103):
        
        a = data.loc[i]
        
        key = a[4]
        value = np.array(a[0:4])
        
        if key not in output:
            output[key] = []
            output[key].append(value)
    
    # getting the dataframe out of the dictionary
    uni = pd.DataFrame(output).transpose()
    
    j = 0
    for k in headings:
        uni[k] = [uni.iloc[i,0][j] for i in range(0,62)]
        j += 1

    del uni[0]
    
    uni.index = range(62)
    
    return uni

# calling the sort_remove function
uni = sort_remove(data)
uni.tail()
