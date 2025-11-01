# Student Performance & Engagement Analysis in an Online Course 
<br><br>
## Part A :- Introduction of dataset.

   
This dataset showcases the activities and engagement patterns of students enrolled in various online courses in a single platform. It contains raw and inconsistent information about student activity.It is cleaned and analyzed using Microsoft Excel for data preparation and Power BI for building an interactive dashboard that highlights learner progress, attendance, and feedback. 
   
**A glimse of original dataset is :- 🔴🔴** 
       
        ![Result](https://raw.githubusercontent.com/Abruz-plotz/Mini-Project-1/main/Images/Excel_Unprocessed.png)

To View the full dataset :-
<br><br>

## Part B: Excel :- Data preprocessing using Excel 

**Glimse:- After Pre-Processing 🔴🔴**
   
   ![Result](https://raw.githubusercontent.com/Abruz-plotz/Mini-Project-1/main/Images/Excel_After.png)

### What all we did 🟧🟧:-

**BI) Dealing with inconsistencies** :-  
1) Converted 'Time_Spent' values into hours (handle "30 mins", "1.5", etc) using find and replace method.
2) Split each session attended by students from the Session_Attendance column using Text to Columns with a **comma (,)** as the delimiter.
3) Filtered out invalid email entries since email is the main identification for online students 

**BII) Dealing with null**             
1) Fixed invalid/missing 'Age' entries using mean/median imputation.

   <pre>                  IF(OR([@Age]=0,ISBLANK([@Age])),ROUND(AVERAGE(FILTER(F2:F1144,F2:F1144<>0)),0),[@Age]) 
   </pre>

**BIII) Dealing with duplicates**      
    Identified duplicates and removed it using remove duplicates

**BIV)	Create new columns:**	         
*1)*  Created **Performance column** and added a flag for "High Performer": Completed == Yes and Rating ≥ 4.

<pre>                    =IF(AND([@Completed]="Yes",[@[Feedback_Rating]]>3),"High Performer",
                   IF(AND([@Completed]="Yes",[@[Feedback_Rating]]<=3),"Low Performer","Not Completed"))         
</pre>
      
*2)*  Created new column **Experience_Level** (based on age: Student, Early Career, etc.)
                                        
   <pre>                  =IF(AND([@Age]>=18,[@Age]<=22),"Student", 
                   IF(AND([@Age]>=23,[@Age]<=30),"Early Career", 
                   IF(AND([@Age]>=31,[@Age]<=40),"Mid Career",  
                   IF(OR([@Age]=0,ISBLANK([@Age]),[@Age]<18),"Unknown","Senior"))))   </pre>

*3)*  Created new column based on **Engagement Level** (based on Time Spent + Progress) 

    <pre>   (Decimal progress X 10) + Time Spent(Hours)  </pre>


<br><br>
## Part C: Power BI :– Advanced Dashboard creation using PBI

 **Glimse:- 🔴🔴**

   ![Result](https://raw.githubusercontent.com/Abruz-plotz/Mini-Project-1/main/Images/PBI%201.png)

##### What all we did 🟧🟧:-

**CI) Multi-page dashboard** :-
1) Created dashboards for Overview Page (KPIs, summary),Category Analysis,Engagement Heatmaps
2) KPI Cards for Total Students, Avg. Progress, Avg. Rating, Course Completion Rate
3) Bar/Column Charts for Students by Course Category, Completion rate by Country
4) Matrix Table: Cross-tab: Course vs. Feedback Rating
5) Line/Area Chart for Enrollment trend by month Custom Measures (DAX) for Completion % by Category,Avg. Time Spent per Category,Correlation between Progress and Rating (scatter plot)
6) Drill-through to student details from summary cards.
7) Use slicers: Course Category, Country, Experience Level

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
