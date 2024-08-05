# Student Survey Analysis (How is Music Related to Academics?)
## Project Team

*   Jonathan Darius
*   Ynah Novilla
*   Adreyan Distor
*   Ojasvi Godha


Project for Data Analysis Methods class. Used various types of data visulizations to understand data, and utilized hypothesis testing to answer our questions 
# Libraries

# Our Data
*  It was provided to us by our teacher after a survey was conducted, and shared with to 100's of different students
## The data we extracted from it 
  * What is your current class standing?
  * What is your gender?
  * What is your GPA?
  * What is your current class standing?
  * What is your major?
  * Why did you choose to major in this field? Select all that apply.
  * What is your favorite area of Computer Science?
  * How many Computer Science related events (e.g., hackathons, programming competitions, etc.) have you been to since Fall 2022?
  * How do you perceive your overall performance in math and science courses?
  * Do you listen to music while you do homework?
  * Which of the following genres do you listen to the majority of the time?
  * How many years have you been involved with music (playing instruments, singing, composing, etc.)?
  * Do you think that the mental processes involved in music (e.g., rhythm, pattern recognition) are related to those in math and science?
  * Do you play an instrument?
  * If you play an instrument, what instrument do you play?
  * What CS-related field do you prefer?
  * What is your least favorite part of Computer Science?
# Data Cleaning
What we did first was we filled in all the rows with missing values
```python
df['Music_Years'] = df['Music_Years'].fillna('0').astype(float)
df.loc[:,'GPA'] = cleaned_df.loc[:,'GPA'].fillna(0)
df.loc[:,'Perceived_Performance'] = cleaned_df.loc[:,'Perceived_Performance'].fillna(0)
df.loc[:,'GPA'] = cleaned_df.loc[:,'GPA'].fillna(0)
df.loc[df['Music&HW'].isnull() == True, 'Music&HW'] = 'No'
df['Instrument'] = df['Instrument'].str.replace('None','NaN')
df['Preferred_Genre'] = df['Preferred_Genre'].str.replace('None','NaN')
```
We unified certain responses into one category. 
For example we converted "computer science" and "csba" into "Computer Science"
```python
df.loc[df['Major'].str.lower().str.find('computer science') != -1, 'Major'] = 'CS'
df.loc[df['Major'].str.lower().str.find('computer science') != -1, 'Major'] = 'CS'
df.loc[df['Major'].str.lower().str.find('csba') != -1, 'Major'] = 'CS'
df.loc[df['Major'].str.lower().str.find('encs') != -1, 'Major'] = 'CS'
df.loc[df['Major'].str.lower().str.find('data science') != -1, 'Major'] = 'DS'
df.loc[df['Major'].str.lower().str.find('dtse') != -1, 'Major'] = 'DS'

df.loc[df['Major'].str.lower().str.find('dtse') != -1, 'Major'] = 'DS'

df.loc[df['Major'] == 'DS', 'Major'] = 'Data Science'
df.loc[df['Major'] == 'CS', 'Major'] = 'Computer Science'

df.loc[df['Preferred_CS_Field'].str.find('AI') != -1, 'Preferred_CS_Field'] = 'Artificial Intelligence/Machine Learning'
df.loc[df['Least_Fav_Area'].str.find('AI') != -1, 'Preferred_CS_Field'] = 'Artificial Intelligence/Machine Learning'
``` 
We converted strings to numbers
```python
df['Music_Years'] = df['Music_Years'].str.replace('Seven', '7', regex=True)
df['Music_Years'] = df['Music_Years'].str.replace('[^0-9.]', '', regex=True)
df.loc[df['Music_Years'] == '', 'Music_Years'] = '0'
``` 


# EDA
### Finding the correlation between GPA and Percieved Performance
![image](https://github.com/AdreyanDistor/Student-Survey-Analysis/assets/117056281/ff8b84e6-0761-42d6-92a7-9bb1d454ae1a)

**Observation:** When first looking at the data, we can compare the gpa and the perceived performance in stem classes to see if there are any discrepancies in their official gpa and their reported perceived performance. When comparing the results on the heatmap with the table, we can see that there is a higher concentration of people with higher GPA and Perceived Performance. This means that the data is aligining how we want it to and the metrics seem to match up. The heat map shows visually that most of the sample have both higher GPA and higher perceived performance in general
### GPA based on listening to music while doing hw
![image](https://github.com/AdreyanDistor/Student-Survey-Analysis/assets/117056281/7478867e-b5aa-4a5b-b708-df5e077d1850)

**Observation:** When looking at the bar graph, we can see that as the GPA increases, both the amount of people who listen to music and don’t listen to music start to increase. We can also observe that the amount of people who DO listen to music while they do their homework is nearly double than those who don’t listen to music. We can see from this data that more people listen to music than those who do not listen to music. However, like the previous graph, we cannot make any conclusions on correlation or affect that music as on GPA because this simply displays the count of students that fall into each category
### Percieved Performance by GPA
![image](https://github.com/AdreyanDistor/Student-Survey-Analysis/assets/117056281/aa174e3f-b79e-4769-96f8-446b4a0fe5c6)

**Observation:** This stacked bar graph shows the different preferred genres student listen to based on their GPA. With this we can see the types of music that appear most in each GPA section. For example, in the GPA group 3.5-5 pop is most common, but in the 3-3.5 section, R&B has the highest value. On the other hand, there is not much data that can be used from the this graph becuase this graph simply diplays the count of different genres in a given GPA section, we cannot make any assumptions on performance or correlation with this data.

### Proportions of Music and HW
![image](https://github.com/AdreyanDistor/Student-Survey-Analysis/assets/117056281/308c3303-02dd-4e1c-8490-b5c7319f9885)

**Observation:** The given pie chart displays the distribution of students that listen to music as they do homework. We can see that the majority of students do listen to music while the rest are evenly divided between not listening at all and listening to music sometimes.

### Percieved Performance for Different Groups
![image](https://github.com/AdreyanDistor/Student-Survey-Analysis/assets/117056281/2009fc11-1835-4955-8bc8-effa9124587d)

**Observation:** For this graphic, we decided to compare Perceived Performance and whether or not they listen to music. Each of the 3 box plots seem to be identical, except for the middle box plot that has a minimum value 0 (*this data point is relating to someone who did not respond to any questions pretaining to their academic performance*). In terms of the Interquartile ranges, they all seem to fall into the same amount of perceived performance amongst the “Yes”, “No”, “Sometimes” options. The maximum ranges all seem to be the same as well.
### Mean Percieved Performance by Instrument
![image](https://github.com/AdreyanDistor/Student-Survey-Analysis/assets/117056281/37c5fe9c-1c1d-4153-b447-e74bb9b80168)

**Observation:** In this visualization, we wanted to compare the Mean Perceived Performance and the different types of instruments. A surprising statistic is that amongst all of the instruments we see that the mean perceived performance is between 3.5 and 4, with a standard deviation of plus or minus 1. This shows the relationship between the mean of the perceived performance and how it relates amongst all of the instruments that people play.

### Proportion of HW with music based on major
![image](https://github.com/AdreyanDistor/Student-Survey-Analysis/assets/117056281/6ae845d7-4d50-4d7c-8805-f634a4cc05d1)

**Observation:** For this visualization we wanted to show the proportion of who listens to music while they do their homework compared to different majors. Each value on the graph corresponds to the percentage of participants in a given major. When first looking at the graph, we can see that ~16% of Data Science participants don't listen to music while doing homework, while ~61% prefer to listen to music while doing homework. When looking at the Data Science portion, we can see that Neurosciencem, Telecomunications Engineering, and Biology majors, don't listen to music. This is due to the fact each of tehse majors only make up, 1% of the total participants. The two largest groups of participants do not share a similar percentage. However, the majority of both groups listen to music while doing homework

### Mean of Percieved Performance by Class Standing
![image](https://github.com/AdreyanDistor/Student-Survey-Analysis/assets/117056281/bbada917-5685-41a4-ad07-29276c3163dd)

**Observation:** Given this waterfall chart, we can see that at the Freshman Standing we have a mean perceived performance of 4.0, Sophomore we have 3.6, Junior we have 3.9, Senior we have 3.6, finally at the graduate level we have 4.2. At the very end we have the net summary of all the mean values, but if we use this to calculate the average mean value we get an average mean of 3.88 in overall perceived performance. We can say that the “typical” mean perceived performance is 3.88 which gives us insight to how the sample feels about their performance regardless of whether or not they listen to music or not.

### Major by Percieved Performance
![image](https://github.com/AdreyanDistor/Student-Survey-Analysis/assets/117056281/e0ae3f5a-8615-4814-a6f7-e43def137e81)

**Observation:** In this graph we are showing the comparison between the samples' majors and also their percieved performance. We depict this using violin chart, the black bar in the middle shows the quartile range (i.e. the variance), the width of the violin shape indicates frequency. The white dot indicates the mean value of percieved perforamcne and the straight black line indicates that there is only one particpant of that major and it shows their percieved score. When looking at computer science we can see that the percieved performance varies between 3 and 4 and the same applies to Data Science majors. The mean percieved performance is 4 for all majors except, Telecommunication systems, Biochemistry, Comp E, and Telecommunications engineering. A suprising finding is that there is a higher frequency of participants with a mean percieved performance of 4, for Data Science Majors, while the frequency is lower for computer science majors. There is also a relativley high frequency of those of a percieved performance of 3 for data science majors. Another thing to point out is that someone that didn't disclose any of their academic data set their percieved performance to 0, which in turn dragged the violin plot.


# Hypotheses and Correlation Analysis
## Hypothesis 1: There is a correlation between the type of music you listen to and your favorite area of computer science
**Null Hypothesis:** There is no correlation between the type of music people listen to and their favorite area of computer science. They are independent of one another.
### Preferred Genre Correlation Matrix
![image](https://github.com/AdreyanDistor/Student-Survey-Analysis/assets/117056281/246e64aa-8608-42c2-9a25-ccd2e4d4a0af)
## **Hypothesis #2:** There is a correlation between GPA and whether or not they play an instrument.
**Null Hypothesis:** There is no correlation between GPA and whether or not they play an instrument. They are independent from one another.
``` python
df_wo0 = df[df['GPA'] != '0']
df_woNAN = df[df['Play_Instrument'] != 'NaN']

gpa_instrument_table = pd.crosstab(df_wo0['GPA'], df_woNAN['Play_Instrument'])
gpa_instrument_table
```
![image](https://github.com/user-attachments/assets/fb02955b-bb5f-4486-960c-bd0c4cf49a3f)

Conclusion:
Not correlation was found

**(i)** The test I will be using is Chi Squared Analysis. Chi Squared Analysis will help indicate whether or not there IS a correlation and to see if our hypothesis holds:
```python
#(ii) Performing the Analysis
chi2, p, dof, expected = chi2_contingency(gpa_instrument_table)

# Display the results
print("\nChi-squared Statistic:", chi2)
print("P-value:", p)
print("Degrees of Freedom:", dof)
# Chi-squared Statistic: 2.3575285958061074
# P-value: 0.5015896219883991
# Degrees of Freedom: 3

from scipy.stats import chi2_contingency, chi2
chi2.ppf(0.5015896219883991, 3)
#ouput: 2.3744398120911736
```
**Our Observation:** Given that our chi squared value of 2.3575285958061074 scores below our threshold value of 0.5015896219883991, we reject our hypothesis. This means that there is NO correlation between students who play instruments and their GPA. Those variables are independent from one another.



## **Hypothesis #3:**

**Our Hypothesis**: There is a correlation between percieved overall performance and those who listen to music while they do their homework.

**Null Hypothesis**: There is no correlation between percieved performance and those who listen to music while they do their homework. They are independent from one another.

```python
perceivedPerformace_HW_table = pd.crosstab(df['Perceived_Performance'], df['Music&HW'])
perceivedPerformace_HW_table
```
![image](https://github.com/user-attachments/assets/bc7180fd-1a4b-48ca-84a4-63cb8745c65d)

```python
#(ii) Performing the Analysis
chi2, p, dof, expected = chi2_contingency(perceivedPerformace_HW_table)

# Display the results
print("\nChi-squared Value:", chi2)
print("P-value:", p)
print("Degrees of Freedom:", dof)

# Chi-squared Value: 9.42384362795695
# P-value: 0.3078113270342382
# Degrees of Freedom: 8

chi2.ppf(0.6603925485744833, 6)
#6.801373325168482
```

**Our Observation:** Given that our chi squared value of 4.120358188252812 scores below our threshold value of 6.801373325168482, we reject our hypothesis. This means that there is NO correlation between students' percieved performance and their GPA. Those variables are independent from one another.


# Conclusion
We analyzed a lot of different aspects with the data we collected from the data we collected. In our data exploration, we gathered that the majority of students do listen to music while they do homework, however there doesn't seem to be a direct correlation between whether they listen to music and their performance in classes, nor is their any correlation between listening to music and how students feel about their own performance. There also wasn't any correlation between preferred genres of music to listen while working and GPA. We did find, however, that the data proves the assumption that people with higher GPA seem to have more confidence in their performance.

For our 3 hypothesis, after testing our data, we have determined that there is no correlation between preferred CS field and preferred music genre, between GPA and whether they played an instrument, nor between students' percieved performance and their GPA.

## Improvement
Proper handling of missing and NA values.
