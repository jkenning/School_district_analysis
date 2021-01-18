# Title

Analysis of data from a school district consisting of ~39,000 students across 15 schools to determine patterns in overall performance.

## Overview of Project

The project scenario involves the analysis, reporting, and presentation of all standardized test data for a city school district. Data on student funding, their standardized test scores (including math and reading scores), and additional information about the schools they attend is aggregated to showcase trends in performance. 

Key Deliverables:

* High level overview table of the district's key metrics
* Overview table for key metrics for each school
* Tables presenting the following metrics:
    - Top 5 and bottom performing schools based on pass rate
    - Average math score for students in each grade level at each school
    - Average reading score for students in each grade level at each school
    - School performance based on budget per student
    - School performance based on school size
    - School performance based on the type of school

### Purpose

The aim is to provide insights about performance trends and patterns found in the student test data across different schools. These insights can be used to inform discussions and strategic decisions at the school and district level, including determining school budgets and priorities going forward.

## Data Preparation and Initial Analysis

The software used for this project was Python 3.7.9 and Jupyter Notebook 6.1.4. A development environment was created to run this version of Python and packages via Anaconda 1.10. Before starting the analysis, the data had to be loaded from two seperate .csv files (for school and student data respectively), formatted for analysis, and cleaned. These initial tasks are summarized below:

- Imported school and student data files and inspected
- Read the data and store in a Pandas DataFrame
- Determined if there were missing values in the data
- Made a list of prefixes and suffixes and removed from student data
- Combined school and student data into a single data set

A series of analyses was performed that met the key deliverables for the project (outlined previously), found in [PyCitySchools.ipynb]().

## Impact of Removing Dishonest Grades from the Analysis

As a result of academic dishonesty, some of the student grades have been altered and must be removed in order to uphold testing standards and the relaibility of the results. Specifically, the reading and maths grades for Thomas High School were removed and the analysis re-done, while keeping the rest of the data intact. Therefore, it is important to examine how these changes may affect the overall analysis and results. The modified data and re-performed analysiscan be found in [PyCitySchools_Challenge.ipynb]()

`# Step 2. Use the loc method on the student_data_df to select all the reading scores from the 9th grade at Thomas High School and replace them with NaN.
student_data_df.loc[(student_data_df["grade"] == "9th") & (student_data_df["school_name"] == "Thomas High School"), "reading_score"] = np.nan`

Figure 1. Code used to replace reading and math grades for 9th grade at Thomas High School

![](https://github.com/jkenning/School_district_analysis/blob/main/Resources/Images/check_for_NaNs.png)

Figure 2. Resultant DataFrame with reading and math score for the affected grade replaced by "NaN" values

**How is the district summary affected?**

Comparing the district summaries from before and after the Thomas High School 9th grade results were removed, there is fairly negligible change to the average scores and pass percentages. The Average math score fell from 79 to 78.9 and the percent passing math fell from 75% to 74.8% as a result. There was even less change in the reading results, with percent passing falling from 85.8% to 85.7%. Overall pass percentage fell from 65.2% to 64.9%. This is because the number of students removed from the data set is only around 400 out of a total >39,000 student population.

![](https://github.com/jkenning/School_district_analysis/blob/main/Resources/Images/district_summary_before.png)

Figure 3. District summary prior to removing Thomas High School 9th grade scores

![](https://github.com/jkenning/School_district_analysis/blob/main/Resources/Images/district_summary_after.png)

Figure 4. District summary after removing Thomas High School 9th grade scores


**How is the school summary affected?**

As data was only removed from one high school, it is not surprising that for the summary data at the school level only the results for Thomas High School were impacted by the changes. The impact on average scores at Thomas High School was fairly negligible however the % of students that passed math, reading, and overall dropped more noticeably:

- Thomas High School average math scores decreased slightly from 83.42 to 83.35
- Thomas High School average reading scores increased slightly from 83.85 to 83.99
- Thomas High School percent passing for math from 93.27% to 66.91%
- Thomas High School percent passing for reading from 97.31% to 69.66%
- Thomas High School percent passing overall from 90.95% to 65.08%

![](https://github.com/jkenning/School_district_analysis/blob/main/Resources/Images/school_summary_original.png)

Figure 5. School summary prior to removing Thomas High School 9th grade scores

![](https://github.com/jkenning/School_district_analysis/blob/main/Resources/Images/school_summary_challenge.png)

Figure 6. District summary after removing Thomas High School 9th grade scores

The school summary DataFrame was then updated using just the 10-12th graders from Thomas High School. This produced results that were much more similar to those from the original analysis (<1% change).

![](https://github.com/jkenning/School_district_analysis/blob/main/Resources/Images/school_summary_challenge_2.png)

Figure 7. District summary for 10th - 12th grades at Thomas High School

**How does replacing the ninth graders’ math and reading scores affect Thomas High School’s performance relative to the other schools?**

Based on the analysis, it appears that despite the marginal decrease in reported results, the impact of removing the the 9th grade has not impacted the ranking of Thomas High School based on overall percentage pass rate. 

![](https://github.com/jkenning/School_district_analysis/blob/main/Resources/Images/top_schools_original.png)

Figure 8. School rankings for top five schools by percentage overall pass rate prior to removing Thomas High School 9th grade scores

![](https://github.com/jkenning/School_district_analysis/blob/main/Resources/Images/high_low_performing_schools.png)

Figure 9. School rankings by percentage overall pass rate after removing Thomas High School 9th grade scores

**How does replacing the ninth-grade scores affect additional factors**

* There are no changes to the average math and reading score by grade except that the 9th grade results for Thomas High School are now missing from the data frame and replaced by 'NaN'
* There are no noticeable changes to the scores by school spending (<.1%)
* There is a very small decrease (<.1%) in percentage passing for math, reading, and overall only for medium size schools (Thomas High School is in this category)
* There are only very small decreases (<.1%>) for average scores and percentage passing only for charter schools (Thomas High School is in this category)

## Summary

Four changes to the school district analysis after the reading and math scores have been replaced results in:

* A decrease in the percentage passing rate for math
* A decrease in the percentage passing rate for reading
* A decrease in the percentage passing rate overall
* The results when Thomas High School results use 10th, 11th, 12th grades are however largely similar in most respects
