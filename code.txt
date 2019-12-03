import numpy as np
import pandas as pd
from apyori import apriori
import os
os.chdir("C:/Users/Shalini.M/.spyder-py3")
xls_file = pd.ExcelFile('AP_Python1_Final_mycopy.xlsx')
df = xls_file.parse('Sheet1')

unique_cases=list(df.CASE_KEY.unique())

records = []
for i in range(len(unique_cases)):
    file=unique_cases[i]
    temp=df[df.CASE_KEY==file]
    temp_list=list(temp.ACTIVITY_EN)
    x=list(temp["Payment Status"].unique())
    temp_list.extend(x)
    records.append(temp_list)

association_rules = apriori(records, min_support=0.0000001)
association_results = list(association_rules)

print(len(association_results))
print(association_results[34])

for item in association_rules:

    # first index of the inner list
    # Contains base item and add item
    pair = item[2][0][1]
    items = [x for x in pair]
    if items[0]=='Early Payments':
        LHS=item[2][0][0]
        LHS=[x for x in LHS]
        print(LHS)
        print(item[0])
    #second index of the inner list
        print("Support: " + str(item[1]))

    #third index of the list located at 0th
    #of the third index of the inner list

        print("Confidence: " + str(item[2][0][2]))
        print("Lift: " + str(item[2][0][3]))
        print("=====================================")