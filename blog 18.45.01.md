Blog Title: "Analyzing IT Professionals: Insights from a Survey"
Introduction
I'm  exploring the skills, preferences, and educational backgrounds of IT professionals through a survey. I'm trying to extrapolate some useful insights for strategic decisions related to hiring, training, and personnel development.

Data Understanding
i'm taking the data from survey_results_public in .csv format.
Some of these data are null so i needed to cleaning the file in some points of the code.

Loading and Exploring the Data
I've created a load_data function to upload the data.


# Display the first few rows of the dataset
print(df.head())
Exploratory Data Analysis
Visualizing IT Professionals' Skills
Create visualizations to represent the distribution of skills among IT professionals. You can use bar charts, pie charts, or any other suitable visualizations. Ensure that the visuals are labeled appropriately.

# Question 1: 

## How many respondents are there for each country?
respondents_by_country = df['Country'].value_counts()

## Display the results as a bar chart
plt.figure(figsize=(12, 6))
respondents_by_country[:15].plot(kind='bar', color='skyblue')
plt.title('Number of Respondents by Country (Top 15)')
plt.xlabel('Country')
plt.ylabel('Number of Respondents')
plt.show()

# Question 2: Bar chart of Gender analysis.
##  What are the gender the respondents?
gender = df['Gender'].str.split(';', expand=True).stack().value_counts()

## Display the results as a bar chart
plt.figure(figsize=(12, 6))
gender[:15].plot(kind='bar', color='lightgreen')
plt.title('Gender (Top 15)')
plt.xlabel('Gender')
plt.ylabel('Number of Respondents')
plt.show()


# Question 3:  Pie chart of educational qualifications
## new df
df_HighestEducationParents = df.dropna(subset=['HighestEducationParents'])

## Count of 'HighestEducationParents'
count_by_HighestEducationParents = df_HighestEducationParents['HighestEducationParents'].value_counts()

## Reset index
count_by_HighestEducationParents = count_by_HighestEducationParents.reset_index()
count_by_HighestEducationParents.columns = ['HighestEducationParents', 'Count']

## Plot the graph with hue and legend=False
plt.figure(figsize=(14, 7))
sns.barplot(x='HighestEducationParents', y='Count', data=count_by_HighestEducationParents, hue='HighestEducationParents', palette='pastel', legend=False)
plt.title('Distribution of Respondents by Highest Education of Parents')
plt.xlabel('Highest Education of Parents')
plt.ylabel('Number of Respondents')
plt.xticks(rotation=45, ha='right')  
plt.show()

# Question 4: Most used Programming Languages
## new df
programming_languages = df['HaveWorkedLanguage'].str.split(';', expand=True).stack()

## Counting the Occurrence of Each Programming Language
languages_count = programming_languages.value_counts()

## Define a threshold
threshold = 5000

## Identify languages below the threshold
languages_below_threshold = languages_count[languages_count < threshold].index

## Create a new entry 'Others' and sum the counts for languages below the threshold
languages_count['Others'] = languages_count[languages_below_threshold].sum()

## Remove individual languages below the threshold
languages_count = languages_count.drop(index=languages_below_threshold)

## Display the results as a bar chart
plt.figure(figsize=(12, 6))
languages_count.plot(kind='bar', color='skyblue')
plt.title('Distribution of Programming Languages Used by Respondents (Threshold: {} occurrences)'.format(threshold))
plt.xlabel('Programming Language')
plt.ylabel('Number of Respondents')
plt.show()


# Conclusion
Summarize the key takeaways from your analysis. Reinforce the importance of the insights gained and how they can contribute to decision-making in the IT domain.

# Closing
Thanks for the interest any kind of comments or suggestions are apprecciate.

# Further Reading
None

# GitHub Repository
https://github.com/samusam91/project1