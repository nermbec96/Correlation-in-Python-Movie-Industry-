![Correlation_in_Python_using_Movie_Industry](https://user-images.githubusercontent.com/127342647/236885499-1746fcd9-8f78-4fb1-8945-5ac291814b78.png)


In this project I explored correlation between defferent caterories in Movie Industry. For this project I used few Python libraries pandas,  numpy, seaborn, matplotlib.

## Project Goals 

Main project goal was to find the strongest correaltion bettween defferent caterories.
My expectations was that the **gross earnings** and **budget** are the categories that will be correlated.

## Project challenges,conclusion and summary
- One of challanges I face in this project is I needed to find out how to includes all categories, and put them together in correlation pairs. I did that by converting non numberic categriies into numeric categroies.
- The conclusion I came  is that as I expected  **gross earnings** and **budget** are the categories that are hight correlated. but another category emerged to be also highly correlated  and that is **buget** .
### Summary:
- Import libraries and dataset
- Cleaning data
- Using different plots to find correlation 
- Converting non numberized columns in numerized columns 
- Finding high correalted pairs

## Projec tHighlights
### Import libraries and dataset
```bash
import pandas as pd
import numpy as np
import seaborn as sns

import matplotlib.pyplot as plt
import matplotlib.mlab as mlab
import matplotlib
plt.style.use('ggplot')
from matplotlib.pyplot import figure
```
```bash
movies_df = pd.read_csv(r'/Users/nerminbecirovic/Downloads/movies.csv')
movies_df.head()
```
<img width="1296" alt="Screenshot 2023-05-08 at 1 15 57 PM" src="https://user-images.githubusercontent.com/127342647/236888265-e69a3238-2525-4f22-b979-1c85b4347c7a.png">

### Removing missing data, changing data type for columns, looking for any duplicates  

```bash
#Removig missing data
movies_df = movies_df.dropna(axis=0, how='any')
#Cheacking angain for a missing data 
for col in movies_df.columns:
    pct_missing = np.mean(movies_df[col].isnull())
    print('{} - {}%'.format(col,pct_missing))
```
```bash
#Chaning data type
movies_df['budget'] = movies_df['budget'].astype('int64')
movies_df['gross'] = movies_df['gross'].astype('int64')
movies_df['votes'] = movies_df['votes'].astype('int64')
movies_df['runtime'] = movies_df['runtime'].astype('int64')
```
```bash
#Drop any duplicates 
movies_df = movies_df.drop_duplicates()
movies_df.head()
```
<img width="1309" alt="Screenshot 2023-05-08 at 1 27 00 PM" src="https://user-images.githubusercontent.com/127342647/236890558-41b435f1-82e8-4f93-937c-20d82b2e3f1b.png">

### Visualization helps to better undestend data

```bush
#Plot budget vs gross using seaborn, so we can see regression 
sns.regplot(x = 'budget', y = 'gross',data = movies_df,line_kws = {'color':'green'})
plt.title('Budget vs Gross Earnings regression line')
plt.show()
```
<img width="1024" alt="Screenshot 2023-05-08 at 1 32 37 PM" src="https://user-images.githubusercontent.com/127342647/236891588-bc752e02-4938-4b6d-95b0-583a129af0af.png">

### Converting non numberized columns in numerized columns and making heatmap to visualize correaltion

```bush
movies_df_numerized = movies_df
for col_name in movies_df_numerized:
    if (movies_df_numerized[col_name].dtype == 'object'):
        movies_df_numerized[col_name] =  movies_df_numerized[col_name].astype('category')
        movies_df_numerized[col_name] =  movies_df_numerized[col_name].cat.codes
movies_df_numerized
```
<img width="978" alt="Screenshot 2023-05-08 at 1 38 20 PM" src="https://user-images.githubusercontent.com/127342647/236892693-d8067acd-f6ff-42fb-8858-c13651ee59e9.png">

```bush
correlation_matrix = movies_df_numerized.corr(method = 'pearson')
sns.heatmap(correlation_matrix,annot = True)
plt.title('Correlation Matrix for Numeric Features')
plt.xlabel('Movie Features')
plt.ylabel('Movie Features')
plt.show()
```
<img width="977" alt="Screenshot 2023-05-08 at 1 40 16 PM" src="https://user-images.githubusercontent.com/127342647/236893081-790f63ab-45df-4e5b-a9d6-3aa20f5006cd.png">

### Finding for the hightest correaltion between categries

 ```bush
 corr_pairs = correlation_matrix.unstack()
sorted_pairs = corr_pairs.sort_values()
sorted_pairs
```
```bush
hight_sorted_pairs = sorted_pairs[(sorted_pairs) > 0.5]
hight_sorted_pairs
```
<img width="281" alt="Screenshot 2023-05-08 at 1 45 39 PM" src="https://user-images.githubusercontent.com/127342647/236894818-b59bdf3d-f5ff-4471-bd39-87de143823ad.png">

## See full project 
[Correlation in Python](https://github.com/nermbec96/Correlation-in-Python-Movie-Industry-/blob/main/Correlation%20in%20Python%20using%20Movie%20Industry%20dataset.ipynb)

## Author

- [@octokatherine](https://github.com/nermbec96)












