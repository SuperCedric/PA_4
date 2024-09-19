<a name="top"></a>

# PA 4: DATA WRANGLING AND DATA VISUALIZATION #
This repository includes my solution to the two given problems involving the pandas, matplotlib, and seaborn libraries. Respectively, the first and second problem are named _Problem 1_ and _Problem 2_.

### GIVEN PROBLEMS ###
#### 1. ECE Board Exam Problem ####
  - In this problem, we are tasked to use data wrangling and data visualization techniques by creating dataframes named `Instru` and `Mindy`.
    - Instru must have the titles `Name`, and `GEAS`, wherein they only show data where `Electronics` is greater than 70 and that their track is Instrumentation and are from Luzon.
    - Mindy must have the titles `Name`, `Track`, and `Electronics`, wherein they only show the data with an average score of greater than 55, from Mindanao, and is Female.
### 2. Visualization Problem ###
  - In this problem, we are tasked to create a visualization that shows how the different features contribute to average grade.

## DEPENDENCIES ##
Importing the pandas, matplotlib, and seaborn library is crucial in order to use its functions.
```
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```

## LOADING OF board2.xlsx ##
To read the `xlsx` file, the function `pd.read_excel()` must be used. This data will be used for both problems.

```python
#read the given excel file named df
df = pd.read_excel('board2.xlsx')
#print the dataframe for verification
df
```

## OUTPUT ##
![image](https://github.com/user-attachments/assets/5e3463f8-ee5c-4b98-bf10-914010bd22a5)

  - Notes
      - Ensure that the file `board2.xlsx` is in the correct directory before running the script.

## 1️⃣ ECE BOARD EXAM PROBLEM ##
The goal for this problem is to load the data into a pandas dataframe and perform data wrangling techniques.

### INSTRU DATAFRAME ###
### DOCUMENTATION ###
This python script filters and selects specific rows and columns from the `board2.xlsx` dataframe based on given conditions. The resulting DataFrame, `Instru`, containts information relevant to the 'Instrumentation' track, with high electronics scores and a specific hometown. 

## CODE ##
```python
#Using and operators to assign the correct rows of data to be put in the Instru dataframe
Instru = df[(df['Track'] == 'Instrumentation')
        &(df['Electronics'] > 70)
        &(df['Hometown'] == 'Luzon')]
#Assign the needed column titles to the Instru dataframe
Instru = Instru[['Name','GEAS','Electronics']]
#Print the dataframe to double check for any logical errors
Instru
```

## OUTPUT ##
![image](https://github.com/user-attachments/assets/5444533c-f408-4021-a330-75810d1d3c52)

## MINDY DATAFRAME ##
### DOCUMENTATION ###
This script filters the `board2.xlsx` dataframe to select rows of data for female students from "Mindanao" and calculates the average of their scores in the ECE board exam. The resulting dataset is cleaned by removing rows with averages below a threshold and outputs the relevant columns.

## CODE ##
```python
#Using and operators to assign the correct rows of data to be put in the Mindy dataframe
Mindy = df[(df['Hometown'] == 'Mindanao')
        &(df['Gender'] == 'Female')].copy()
#Calculate the average of their scores and append it to the Mindy dataframe
Mindy['Average'] = Mindy[['Math','GEAS','Electronics','Communication']].mean(axis=1)
#Remoove any average values less than 55
Mindy = Mindy[Mindy['Average'] >= 55]
#Store the correct columns to be outputted
Mindy = Mindy[['Name','Track','Electronics','Average']]
#Print the dataframe to double check for any logical errors
print(Mindy)
```

## OUTPUT ##
![image](https://github.com/user-attachments/assets/dc24f50d-eb5c-43ba-a9c7-0b377f5d70fc)


## 2️⃣ VISUALIZATION PROBLEM ##
To create the graphs, we must use data visualization techniques using the `matplotlib` library and the `seaborn` library.

### CALCULATION FOR AVERAGE SCORES ###
## DOCUMENTATION ##
Before creating the graphs, we must find the average scores and append it into another column in the dataframe so we can use it to visualize the data.
## CODE ##
```python
#get the average score of each exam-taker to use as data.
df['Average'] = df[['Math','GEAS','Electronics','Communication']].mean(axis=1)
```

### AVERAGE SCORES BY GENDER ###
## DOCUMENTATION ##
This script creates a violin plot that visualized the distribution of average grades by gender. Using `matplotlib` and `seaborn`, the plot provides insight into the spread and density of the average scores for male and female studednts, while adjusting the aesthetics of the graph for clarity and appeal.
## CODE ##
```python
#create the figure size and layout of the graph
plt.figure(figsize=(10,10))
#create the subplots
plt.subplot(2, 2, 1)
#create the actual violinplot using the data from the dataframe by labelling the x axis as the gender and the y axis as their average scores
sns.violinplot(x='Gender', y='Average', data=df)
#create the title of the graph
plt.title('Average Grades by Gender')
#automatically adjust the spacing between subplots and change the color style for aesthetics
plt.tight_layout()
sns.set(style='darkgrid')
```
## OUTPUT ##
![data1_pa4](https://github.com/user-attachments/assets/0f9d0c0c-3d4e-4678-adaa-0549d2219fbf)

### AVERAGE SCORES BY TRACK ###
## DOCUMENTATION ##
This script creates a violin plot that visualized the distribution of average grades by track. Using `matplotlib` and `seaborn`, the plot provides insight into the spread and density of the average scores for male and female studednts, while adjusting the aesthetics of the graph for clarity and appeal.
## CODE ##
```python
#create the figure size and layout of the graph
plt.figure(figsize=(10,10))
#create the subplots 
plt.subplot(2,2,2)
#create the actual violinplot using the data from the dataframe by labelling the x axis as the track and the y axis as their average scores
sns.violinplot(x='Track', y='Average', data=df)
#create the title of the graph
plt.title('Average Grades by Track')
#automatically adjust the spacing between subplots and change the color style for aesthetics
plt.tight_layout()
sns.set(style='darkgrid')
```
## OUTPUT ##
![data2_pa4](https://github.com/user-attachments/assets/aa6ecadc-8bdc-405b-93e4-8ea603d19c83)

### AVERAGE SCORES BY HOMETOWN ###
## DOCUMENTATION ##
This script creates a violin plot that visualized the distribution of average grades by hometown. Using `matplotlib` and `seaborn`, the plot provides insight into the spread and density of the average scores for male and female studednts, while adjusting the aesthetics of the graph for clarity and appeal.
## CODE ##
```python
#create the figure size and layout of the graph
plt.figure(figsize=(10,10))
#create the subplots 
plt.subplot(2,2,3)
#create the actual violinplot using the data from the dataframe by labelling the x axis as the Hometown and the y axis as their average scores
sns.violinplot(x='Hometown', y ='Average', data=df)
#create the title of the graph
plt.title('Average Grades by Hometown')
#automatically adjust the spacing between subplots and change the color style for aesthetics
plt.tight_layout()
sns.set(style='darkgrid')
```
## OUTPUT ##
![data3_pa4](https://github.com/user-attachments/assets/559b33a8-7420-4494-a474-8e06e6c92564)

## BUILT WITH ##
  - Jupyter Notebook

## LIBRARIES USED ##
  - PYTHON
    - Pandas
    - Matplotlib
    - Seaborn

## AUTHOR ##
  - Cedric Kurt Taguba - [@SuperCedric](https://github.com/SuperCedric)

<p align="right">(<a href="#top">[🔼GO TO TOP]</a>)</p>
