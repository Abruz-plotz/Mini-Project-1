# Student Performance & Engagement Analysis in an Online Course 
<br><br>
## Part A :- Introduction of dataset.

   
This dataset showcases the activities and engagement patterns of students enrolled in various online courses in a single platform. It contains raw and inconsistent information about student activity.It is cleaned and analyzed using Microsoft Excel for data preparation and Power BI for building an interactive dashboard that highlights learner progress, attendance, and feedback. 
   
**A glimse of original dataset is :- 🔴🔴** 
       
   ![Result](https://raw.githubusercontent.com/Abruz-plotz/Mini-Project-1/main/Images/Excel_Unprocessed.png)

To View the full dataset :-
<br><br>

## Part B: Excel :- Data preprocessing using Excel 

**After Pre-Processing 🔴🔴**
   
   ![Result](https://raw.githubusercontent.com/Abruz-plotz/Mini-Project-1/main/Images/Excel_After.png)

### The Approach 🟧🟧:-

**BI) Dealing with inconsistencies** :-  
1) Converted 'Time_Spent' values into hours (handle "30 mins", "1.5", etc) using find and replace method.
2) Split each session attended by students from the Session_Attendance column using Text to Columns with a **comma (,)** as the delimiter.
3) Filtered out invalid email entries since email is the main identification for online students 

**BII) Dealing with null**             
1) Fixed invalid/missing 'Age' entries using mean/median imputation.

   <pre>               =IF(OR([@Age]=0,ISBLANK([@Age])),ROUND(AVERAGE(FILTER(F2:F1144,F2:F1144<>0)),0),[@Age]) 
   </pre>

**BIII) Dealing with duplicates**      
    Identified duplicates and removed it using remove duplicates

**BIV)	Create new columns:**	         
*1)*  Created **Performance column** and added a flag for "High Performer": Completed == Yes and Rating ≥ 4.

<pre>                  =IF(AND([@Completed]="Yes",[@[Feedback_Rating]]>3),"High Performer",
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

 Created interactive dashboards to provide a clear overview of key metrics and uncover actionable insights. To veiw the complete PBI file, download using:-
 [Download Power BI (.pbix) file](https://github.com/Abruz-plotz/Mini-Project-1/blob/main/Mini%20Project%20PBI.pbix)
 Some glimses of the dashboards are provided below.

### The Approach 🟧🟧:-

**CI) Tools used for dashboard** :-

1) **Bar & Column Charts** – Visualized Students by Course Category and Completion Rate by Country.
2) **Slicers & Filters** – Integrated by Course Category, Country, and Experience Level for interactive exploration.
3) **Line & Area Charts** – Displayed enrollment trends over time.   

    ![Result](https://raw.githubusercontent.com/Abruz-plotz/Mini-Project-1/main/Images/PBI%201.png)

4) **Matrix Tables** – Analyzed feedback ratings per course to evaluate completion rate and average time spent per learner.
    ![Result](https://raw.githubusercontent.com/Abruz-plotz/Mini-Project-1/main/Images/PBI%202.png)

5) **Scatter Plot Visualization** – Highlighted correlation between Feedback Rating and Progress (%), grouped by performance level.
6) **KPI Cards** – Total Students, Average Progress, Average Rating, and Course Completion Rate.
    ![Result](https://raw.githubusercontent.com/Abruz-plotz/Mini-Project-1/main/Images/PBI%203.png)


7) **Drill-through Pages** – Enabled user navigation to detailed student-level performance insights.

    ![Result](https://raw.githubusercontent.com/Abruz-plotz/Mini-Project-1/main/Images/PBI%204.png)
   

**CII) New Column using DAX:-**

Using DAX formula, we create a summary table by course category, showing how students perform and engage in each course. It calculates enrollments, completions, completion rate, total and average time spent, and each course’s share of total study time, helping to evaluate overall learning performance and effort distribution.

   ![Result](https://raw.githubusercontent.com/Abruz-plotz/Mini-Project-1/main/Images/PBI_Dax.png)


CIII)**Interactive Dashboards** :- The interaction helps users to find direct patters and answers there 



## Part D : Summary and Feedback**

Summarizes feedback ratings per course in a detailed matrix view.
Displays overall course completion rate (46.99%) against a goal of 100%.
Includes a completion rate vs. average time spent comparison for each course category.
Key insight: Data Science and Design courses show strong engagement but moderate completion.

🔵 3. Rating vs. Progress and KPI Cards

Insight: High performers maintain progress above 70% with ratings ≥4; low performers cluster around lower progress percentages.
