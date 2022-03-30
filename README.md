# School District Analysis
Module 4 PyCity Schools with Pandas

## Overview of the School District Analysis
A school board employee has given us the following tasks to analyise a set of data in a school district with a school that is suspected of altering testing data. The suspect data will be removed, specifically the Math and Reading test scores for the 9th graders at Thomas High School, and the impact on the overall data will be analysed.This is to test our knowledge from learning python and pandas.

1. How is the district summary affected when the suspect data is removed?
2. How is the school summary affected when the suspect data is removed?
3. How does replacing the ninth graders’ math and reading scores affect Thomas High School’s performance relative to the other schools?
4. How does replacing the ninth-grade scores affect the following:
   - Math and Reading scores by grade
   - Scores by school spending
   - Scores by school size
   - Scores by school type

## School District Analysis
The initial ask for this analysis was to clean the 'error' data from the data set. Specifically, they asked us to clean the testing scores for math and reading in the 9th grade at Thomas High School. Then averages and percentages were adjusted for the remaining number of students tested. This was done with the following steps:
- Using a `.loc()` function, the data containing "Thomas High School" (in the school_name column), "9th" (in the grade column) and the whole reading score column (and math score in the second string of code) was selected and the values were repaced with NaN (Not a Number). This removes the 'error' data in the scores with-out setting the scores to 0. 
  - `student_data_df.loc[(student_data_df["grade"] == "9th") & 
                    (student_data_df["school_name"] == "Thomas High School") &
                    (student_data_df["reading_score"] > 0), "reading score"] = np.nan
  - `student_data_df.loc[(student_data_df["grade"] == "9th") & 
                    (student_data_df["school_name"] == "Thomas High School") &
                    (student_data_df["math_score"] > 0), "math score"] = np.nan
- Using a `.loc()` function and a `.count()` function, the total students that contain the data "Thomas High School", and "9th" are counted.
  - `THS_9th_students = school_data_complete_df.loc[(school_data_complete_df["school_name"]== "Thomas High School") 
                                                     & (school_data_complete_df["grade"]=="9th"),"student_name"].count()
print(THS_9th_students)`
- Using a `.count()` function, the total number of students are counted across the whole data set.
  - `student_count = school_data_complete_df["Student ID"].count()`
- Seting the new count of students, that will be used in all subsequent calculations of averages and percentages. The total number of students, minus the suspect names, is equal to the new student count.
  - `new_total_student_count = student_count - THS_9th_students
print(new_total_student_count)`

Now that the 'error' data has been removed and the new count of students has been counted, the analysis of how this has affected the total outcomes can be seen below.
1. How is the district summary affected?
   -  The Average Math Score decreased by .1, the Average Reading Score stayed the same, the percentage of students Passing Math decreased by .2%, the percentage of students Passing Reading increased by .1%. The percentage of students passing both Math and Reading decreased by .3%. The adjusted summary is the upper graphic, and the original is the lower.
![modified summary](https://user-images.githubusercontent.com/99200831/160882818-da3a587b-256a-4575-91b0-e08b57b25fe2.png)
![original summary](https://user-images.githubusercontent.com/99200831/160882887-9063f329-71bc-4dc7-b910-b9ed1f7a37b6.png)
2. How is the school summary affected?
   - The modified summary shows that with-in Thomas High School, the Average Math Score decreased by .06, the Average Reading Score increased by .05, the percentage of students Passing Math decreased by .09%, the percentage of students Passing Reading decreased by .29%, and the percentage of students Passing both Math and Reading decreased by .31%. The adjusted summary is the upper graphic, and the original is the lower graphic.
![modified school summary 2](https://user-images.githubusercontent.com/99200831/160882970-c9c471e1-fe4a-4c4f-9c1b-de3968e155bd.png)
![original school summary](https://user-images.githubusercontent.com/99200831/160882995-b9fca297-8a74-4cbe-8f68-4c53a0b026e5.png)
3. How does replacing the ninth graders’ math and reading scores affect Thomas High School’s performance relative to the other schools?
- Removing the 9th graders' scores did not affect the performance of Thomas High School in a very large degree. It is still in the second best school by overall passing percentage. However this is only the case if the scores are compared against the number of the valid test scores (just the 10th, 11th and 12th grade students.)
- If the scores were to be calculated against the total number of the students attending Thomas High School (including the 9th graders), the change is is pretty large. The precentage of students passing any subject and overall, is decreased by around 30%, and Thomas High School moves from the second best school by overall passing to the third worst. 
4. How does replacing the ninth-grade scores affect the following:
   - Math and Reading scores by grade
   - the values for 9th graders are NaN and not 0, so it does not affect the scores.
![math score by grade](https://user-images.githubusercontent.com/99200831/160884479-de4a6ca7-c8e2-42c4-b19b-89a3aaca8ee4.png)
![reading score by grade](https://user-images.githubusercontent.com/99200831/160884851-fa765366-0320-4b49-bd47-34590b3b4eb4.png)
   - Scores by school spending
     - Removing the 9th grade scores does not affect the data. Thomas High School falls into the $630-$644 per student spending range, and  the percentage of students passing reading, along with, the percentage of students passing both math and reading decrease by .1%. 
![school spending adjusted](https://user-images.githubusercontent.com/99200831/160884800-9c029344-b62d-4d68-a6df-258892c2bb2f.png)
![school spending original](https://user-images.githubusercontent.com/99200831/160884830-38952e66-0e29-417c-9218-da9289af35a4.png)
   - Scores by school size
     - Removing the 9th grade scores does not affect this data either. Thomas High School falls into the Medium (1000-2000) school size range, and the percentage of the students passing reading decreases by .1%.
![school size adjusted](https://user-images.githubusercontent.com/99200831/160885406-a59d9e54-60b6-468c-9f55-4ceccc18b840.png)
![school size original](https://user-images.githubusercontent.com/99200831/160885420-c98bc573-7ddc-47ef-9b43-cd5a5301a598.png)
   - Scores by school type
     - Thomas High School is a charter school. Across all charter schools, the data is unaffected by removing the scores of the 9th graders.
 ![charter adjusted](https://user-images.githubusercontent.com/99200831/160885865-7abe2c79-bf9a-47f8-8f4c-97a9fc122e7f.png)
![charter orig](https://user-images.githubusercontent.com/99200831/160885889-92029047-68fe-416a-aa4c-a92bc17a1b12.png)

## Summary
Removing the 9th graders test scores did not impact the overall scores in the district, about .4% of a percentage point. The sample size is too large for the removal of the 9th graders to make a noticeable dent. It did, however, affect Thomas High Schools' percentage scores, but not by much. It is still not representing the whole story to the school board and can probably cause trouble down the road in further analysis regarding these sorts of scores.
