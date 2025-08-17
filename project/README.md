# 📊 Wake County Public School System (WCPSS) Analysis: Area-Wise, Status-Wise performance

This project analyzes the academic performance of elementary schools across different cities in Wake County, North Carolina and also based on Magnet status within the Wake County using publicly available data.

---

## 📌 Objective

To compare school performance area-wise, magnet-status wise and understand how factors such as:
- **Grade-Level Proficiency (GLP%)**
- **Economically Disadvantaged Students (FR%)**
- **Limited English Proficiency (LEP%)**
- **Special needs students (SWD)**

influence academic outcomes.



##  Data Sources

-  [WCPSS School Data Portal](https://www.wcpss.net/Page/32560)
-  [NC School Report Cards](https://ncreports.ondemand.sas.com/src)
-  [2023-24 School Assessment and Other Indicators](https://www.dpi.nc.gov/districts-schools/accountability-and-testing/school-accountability-and-reporting/accountability-data-sets-and-reports)
-  [2023-24 District Facts Report by Year](https://www.wcpss.net/domain/22671)
- Public datasets scraped or downloaded from town and state education data sources.

## Tools I Used
- For my deep dive into the WCPSS data, I harnessed the power of several key tools:

  *Python: The backbone of my analysis, allowing me to analyze the data and find critical insights.I also used the following Python libraries:
  *Pandas Library: This was used to analyze the data.
  *Matplotlib Library: I visualized the data.
  *Seaborn Library: Helped me create more advanced visuals.
  *Statsmodels Library : Helped me check the correlation between grade level proficiency and Magnet status of a school with confounding factors like the Free/Reduced lunch% and limited English proficiency
  *Scipy Library : Helped me check Spearman correlations 
  *Jupyter Notebooks: The tool I used to run my Python scripts which let me easily include my notes and analysis.
  *Visual Studio Code: My go-to for executing my Python scripts.
  *Git & GitHub: Essential for version control and sharing my Python code and analysis, ensuring collaboration and project tracking.

## Methodology

- Cleaned and filtered elementary school data by:
  - Creating dataframes by reading data from the above mentiones sources
  - Checking for duplicates using df.duplicated()
  - Checking for null values and dropping if any using df.dropna()
  - Dropping irrelevant columns using df.drop(columns=['list_of_columns_to_drop'])
  - Created new column based on magnet status for easy grouping based on magnet status
  - Checked for data consistency across all columns and converted numeric kind of data into numeric type after stripping % inorder to perform numeric aggregation function
   (Ex : df['glp_pct']=df['glp_pct'].str.strip('%').astype(float))
   (Ex : df_dis['glp_pct']=pd.to_numeric(df_dis['glp_pct'],errors='coerce'))
  - Merging data from various dataframes to form a dataframe containing all relevant data  needed for further analysis
  - Grouped and aggregated data based on magnet status, Cities inside the Wake county

### The Analysis

Each Jupyter notebook for this project is aimed at investigating specific aspects of overall End of Grade performance using Grade Level Proficiency as a measure. Here’s how I approached each question:

## 1. Do elemenatry schools with Magnet status perform better than schools with Non-magnet status ?

To find the answer I first grouped schools based on the magnet and non-magnet status and found the mean Grade level proficiency % for all subjects.
[View my notebook with detailed steps here]: (project\Magnet_vs_NonMagnet.ipynb)

## Results
![Magnet vs Non Magnet Performance across all Subjects](output\Average_GLP_Magnet_vs_NonMagnet.png)

  ## Findings:
   - Initial analysis showed Magnet school's performance was lower than Non-Magnet schools across all subjects.
   - This leads to questions like : 
        * Despite the popular opinion that Magnet schools are better why are the results showing a different story? 
        * What impact do factors like the number of students that are economically disadvantaged and limited English proficiency in each school have on the overall performance?

   - To answer these questions used the statsmodel library and used an Ordinary Least Square Regression model to understand the relationship between different variables like how magnet status, % free/reduced lunch (FR), and % limited English proficient (LEP) affect GLP%

   
    OLS R-squared: 0.844  
    Key predictor: % Economically Disadvantaged (FR) → Strong negative impact on GLP%  
    Magnet status → Not statistically significant after controlling for FR and LEP

 # Key takeaways 
    * The strongest predictor of low GLP% is free/reduced lunch percentage.
    * Being a magnet school doesn’t have a statistically significant effect after   controlling for demographics.

## 2. How do schools perform area-wise inside of Wake county?

To find answers, I grouped the schools area-wise and compared their mean GLP%(grade-level) for overall EOG. 

[View my notebook for area-wise Analysis](project\Area_wise_EDA.ipynb)


  # Findings
   City-wise Summary
    *Holly Springs stands out with:
    *Highest average GLP% (over 80%)
    *Lowest FR% (around 16%)
   This suggests a strong inverse correlation between economic disadvantage and academic performance.
    *Apex, Cary, and Morrisville also show strong performance metrics.
    *Zebulon and Knightdale report lower GLP% and higher FR%, indicating potential areas for targeted support.

![Area wise GLP% comparision for all students in EOG](output\GLP_area_wise.png)

 ## Correlation Analysis
    Spearman correlation between GLP% and FR%: -0.88
    Spearman correlation between GLP% and LEP%: -0.71

    This indicates a strong negative association between socioeconomic disadvantage or language barriers and student proficiency.

![Area wise GLP% comparison for students from disadvantaged economic background and limited English proficiency](output\Grade_proficiency_areawise.png)
![Spearman correlation regression plot](output\GLP_FR_LEP_areawise.png)

## 3. How do AIG students' performance impact the overall GLP%?

    Performed Spearman and pearson correlation on % OF AIG students and GLP% on all schools
    Correlation between GLP% and AIG count: 0.86
    The results suggest a strong positive correlation, indicating that schools with higher percentages of academcally intellectual gifted (AIG) students tend to have higher Grade-Level Proficiency percentages.

[View my notebook for analysis](project\AIG_students_Analysis.ipynb)

## Results 

![AIG vs GLP](output\AIG_GLP.png)
![Correlation between AIG% and GLP%](output\correlation_AIG_GLP.png)

## 4.How performace of school varies based on calendar type?
     Perfomed independent t-test to compare performance between traditional calendar and year-round
     t-test gave a t-statistic of -1.11 with a p-value of 0.27, meaning the observed difference in glp_pct between                Traditional and Year-Round schools is not statistically significant. In other words, we cannot conclude that one             calendar type systematically outperforms the other in student proficiency outcomes.


### Future Work
    Expand analysis to middle and high schools
    Factor in school size, ELL/special ed populations
    Use multivariate regression to control for multiple variables
    Analyze year-over-year trends to assess improvement.
    Map schools geographically to explore spatial performance patterns.


**Akshatha Nakshatri**  
Aspiring Data/Business Analyst | Former Senior Software Engineer 

