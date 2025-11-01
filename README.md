# Student Performance & Engagement Analysis in an Online Course 
<br><br>
## Part A: Data preprocessing using Excel 

**AI) Dealing with inconsistencies** :-  
1) Converted 'Time_Spent' values into hours (handle "30 mins", "1.5", etc) using find and replace method.
2) Split each session attended by students from the Session_Attendance column using Text to Columns with a comma (,) as the delimiter.
3) Filtered out invalid email entries since email is the main identification for online students 

**AII) Dealing with null**             
1) Fixed invalid/missing 'Age' entries using mean/median imputation.
 ***{IF(OR([@Age]=0,ISBLANK([@Age])),ROUND(AVERAGE(FILTER(F2:F1144,F2:F1144<>0)),0),[@Age])}***

**AIII) Dealing with duplicates**      
    Identified duplicates and removed it using remove duplicates

**AIV)	Create new columns:**	         
1)  Created performance column and added a flag for "High Performer": Completed == Yes and Rating ≥ 4.

2)  Created new column Experience_Level (based on age: Student, Early Career, etc.)
                                        
   <pre> ```excel =IF(AND([@Age]>=18,[@Age]<=22),"Student", 
                   IF(AND([@Age]>=23,[@Age]<=30),"Early Career", 
                   IF(AND([@Age]>=31,[@Age]<=40),"Mid Career", 
                   IF(OR([@Age]=0,ISBLANK([@Age]),[@Age]<18),"Unknown","Senior")))) ``` </pre>

3)  Created new column based on Engagement Level (based on Time Spent + Progress) 

    ***{(Decimal progress X 10) + Time Spent(Hours)}***



## Part 2: Power BI – Advanced Dashboard Tasks

Multi-page dashboard:
•	Overview Page (KPIs, summary)
•	Category Analysis
•	Engagement Heatmap

KPI Cards:
•	Total Students, Avg. Progress, Avg. Rating
•	Course Completion Rate
Bar/Column Charts:
•	Students by Course Category
•	Completion rate by Country
Matrix Table:
•	Cross-tab: Course vs. Feedback Rating
Line/Area Chart:
•	Enrollment trend by month
 Custom Measures (DAX):
•	Completion % by Category
•	Avg. Time Spent per Category
•	Correlation between Progress and Rating (scatter plot)
Drill-through to student details from summary cards.
Use slicers: Course Category, Country, Experience Level

**Tables Used**
- `Students` → Student ID, Name, Country, Course, Join Date, Completed (Yes/No)
- `Courses` → Course ID, Course Name, Category
- `Enrollment` → Enrollment ID, Student ID, Course ID, Year

**Key Measures (DAX)**
- Total Students = COUNT(Student[ID])
- Completion % = DIVIDE(COUNTROWS(FILTER(Student, Student[Completed]="Yes")), COUNTROWS(Student))
- Yearly Join Trend = COUNTROWS(Student)

**Relationships**
- Students[Student ID] → Enrollment[Student ID]
- Courses[Course ID] → Enrollment[Course ID]
