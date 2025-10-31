# Student Performance & Engagement Analysis in an Online Course 
### Part 1: Excel – Advanced Cleaning Tasks

1.	Convert 'Time_Spent' values into hours (handle "30 mins", "1.5", etc.).
2.	Fix invalid/missing 'Age' entries using mean/median imputation.

3.	Extract total sessions attended from the Session_Attendance column.
4.	Filter out invalid email entries and identify duplicates.
5.	Add a flag for "High Performer": Completed == Yes and Rating ≥ 4.
6.	Create new columns: Experience_Level (based on age: Student, Early Career, etc.) Engagement Level (based on Time Spent + Progress)



### Part 2: Power BI – Advanced Dashboard Tasks
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
