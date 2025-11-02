# Student Performance & Engagement Analysis in an Online Course 
<br>
<details>
     <summary> <h1> Part A :- Introduction of dataset </h1></summary>
   
<!--## Part A :- Introduction of dataset.-->

   
This dataset showcases the activities and engagement patterns of students enrolled in various online courses in a single platform. It contains raw and inconsistent information about student activity.It is cleaned and analyzed using Microsoft Excel for data preparation and Power BI for building an interactive dashboard that highlights learner progress, attendance, and feedback. 
   
**A glimse of original dataset is :- 🔴🔴** 
       
   ![Result](https://raw.githubusercontent.com/Abruz-plotz/Mini-Project-1/main/Images/Excel_Unprocessed.png)

To View the full dataset :- [Original dataset](https://github.com/Abruz-plotz/Mini-Project-1/blob/main/Uncleaned%20data.csv)
<br>
</details>
<details>
     <summary> <h1> Part B :- Excel :<br> Data preprocessing using Excel  </h1></summary>
     
<!--## Part B:- Excel : Data preprocessing using Excel--> 

To download and view the data preprocessing, go to 
[Download Excel(.xlxs) file](https://github.com/Abruz-plotz/Mini-Project-1/blob/main/Mini%20Project%20Excel.xlsx)

**After Pre-Processing 🔴🔴**
   
   ![Result](https://raw.githubusercontent.com/Abruz-plotz/Mini-Project-1/main/Images/Excel_After.png)

### BI) Dealing with inconsistencies  

***(1)*** Converted 'Time_Spent' values into hours (handle "30 mins", "1.5", etc) using find and replace method.
***(2)*** Split each session attended by students from the Session_Attendance column using Text to Columns with a **comma (,)** as the delimiter.
***(3)*** Filtered out invalid email entries since email is the main identification for online students 

### BII) Dealing with null
     
 Fixed invalid/missing 'Age' entries using mean/median imputation.

   <pre>               =IF(OR([@Age]=0,ISBLANK([@Age])),ROUND(AVERAGE(FILTER(F2:F1144,F2:F1144<>0)),0),[@Age]) 
   </pre>

### BIII) Dealing with duplicates    
    Identified duplicates and removed it using remove duplicates

### BIV) Create new columns	         

***(1)***  Created **Performance column** and added a flag for "High Performer": Completed == Yes and Rating ≥ 4.

<pre>                  =IF(AND([@Completed]="Yes",[@[Feedback_Rating]]>3),"High Performer",
                   IF(AND([@Completed]="Yes",[@[Feedback_Rating]]<=3),"Low Performer","Not Completed"))         
</pre>
      
***(2)***  Created new column **Experience_Level** (based on age: Student, Early Career, etc.)
                                        
   <pre>                  =IF(AND([@Age]>=18,[@Age]<=22),"Student", 
                   IF(AND([@Age]>=23,[@Age]<=30),"Early Career", 
                   IF(AND([@Age]>=31,[@Age]<=40),"Mid Career",  
                   IF(OR([@Age]=0,ISBLANK([@Age]),[@Age]<18),"Unknown","Senior"))))   </pre>

***(3)***  Created new column based on **Engagement Level** (based on Time Spent + Progress) 

    <pre>   (Decimal progress X 10) + Time Spent(Hours)  </pre>
</details>

<details>
     <summary> <h1> Part C :- Power BI : Advanced Dashboard creation using PBI </h1></summary>

<!--## Part C: Power BI :– Advanced Dashboard creation using PBI-->

 Created interactive dashboards to provide a clear overview of key metrics and uncover actionable insights. To veiw the complete PBI file, download using:-
 [Download Power BI (.pbix) file](https://github.com/Abruz-plotz/Mini-Project-1/blob/main/Mini%20Project%20PBI.pbix)

 
 Some glimses of the dashboards are provided below.

### CI) Tools used for dashboard

***(1)*** **Bar & Column Charts** – Visualized Students by Course Category and Completion Rate by Country.<br>
***(2)*** **Slicers & Filters** – Integrated by Course Category, Country, and Experience Level for interactive exploration.<br>
***(3)*** **Line & Area Charts** – Displayed enrollment trends over time.<br>   

![Result](https://raw.githubusercontent.com/Abruz-plotz/Mini-Project-1/main/Images/PBI%201.png)
<br><br>
***(4)*** **Matrix Tables** – Analyzed feedback ratings per course to evaluate completion rate and average time spent per learner.<br><br>
    ![Result](https://raw.githubusercontent.com/Abruz-plotz/Mini-Project-1/main/Images/PBI%202.png)
<br><br>
***(5)*** **Scatter Plot Visualization** – Highlighted correlation between Feedback Rating and Progress (%), grouped by performance level.
***(6)*** **KPI Cards** – Total Students, Average Progress, Average Rating, and Course Completion Rate.<br><br>
    ![Result](https://raw.githubusercontent.com/Abruz-plotz/Mini-Project-1/main/Images/PBI%203.png)
<br><br>

***(7)*** **Drill-through Pages** – Enabled user navigation to detailed student-level performance insights.

    ![Result](https://raw.githubusercontent.com/Abruz-plotz/Mini-Project-1/main/Images/PBI%204.png)
   
<br><br>
### CII) New Column using DAX

Using DAX formula, we create a summary table by course category, showing how students perform and engage in each course. It calculates enrollments, completions, completion rate, total and average time spent, and each course’s share of total study time, helping to evaluate overall learning performance and effort distribution.

   ![Result](https://raw.githubusercontent.com/Abruz-plotz/Mini-Project-1/main/Images/PBI_Dax.png)

<br><br>
### CIII) Interactive Dashboards  

The dashboard enables users to explore data dynamically and identify patterns directly through interaction.
For instance, to view students from the US who did not complete their courses, users can simply click on the respective column in the clustered bar chart.
This interaction instantly updates all visuals — showing the trend of such students over the years, their distribution across different courses, and the corresponding KPI highlighting 62 students in total.
This interactivity provides a clear, data-driven view of completion trends and category-wise performance at a glance.
  
   ![Result](https://raw.githubusercontent.com/Abruz-plotz/Mini-Project-1/main/Images/PBI%201_2nd.png)

</details>

<details>
     <summary> <h1> Part D :- Conclusion </h1></summary>

<!--## Part D : Conclusion-->

### DI)The Summary 

***(1)*** **Data Preparation** -  Cleaned and standardized student-level data (1,143 records) by fixing missing values, standardizing categories, and creating derived fields such as Experience Level, Engagement Score, and Performance Tag using logical IF conditions.

***(2)*** **Course Enrollment & Completion**-Web Development and Design attracted the highest enrollments (249 and 228 students).
Average overall course-completion rate ≈ 47 %, indicating that more than half of the enrolled learners dropped out before finishing.
Business courses showed the lowest completion (≈ 46 %), while Design performed best (≈ 49 %).

***(3)*** **Geographical Distribution**- Students from India (186 completed) and UK (143 completed) formed the largest active groups.
The U.S. and Canada had moderate participation but higher non-completion percentages.Country-level insights suggest regional differences in engagement behaviour.

***(4)*** **Engagement & Performance Patterns**- Average Progress = 50 % Average Feedback Rating = 3.0 / 6.
A positive correlation exists between Progress % and Feedback Rating — students who completed courses tend to provide higher ratings.
Using DAX segmentation, learners were grouped as High Performer, Low Performer, or Not Completed, helping pinpoint improvement areas.

***(5)*** **Temporal Trends**- Enrollment remained steady across 2022 – 2025 with visible seasonal peaks, implying marketing cycles or course-launch periods affect registrations.

***(6)*** **Interactive Dashboard Insights** - Filtering by country or category instantly updates KPIs to display relevant completion counts and time-spent patterns.
Example: selecting US – Not Completed filters visuals to 62 students distributed almost evenly across all courses.
Summarizes feedback ratings per course in a detailed matrix view. 
Drill-through pages reveal individual learner details and engagement heatmaps for deeper exploration.

***(7)*** **Time Spent Analysis (DAX Metrics)**-Average time spent per student ≈ 338 hours across all categories.
Web Development learners invested the most time (~367 h, 21 % share).
Despite higher effort, completion rates remained below 50 %, suggesting potential content or engagement issues.

### DII)The Insights

***(1)*** High enrollment does not guarantee high completion — targeted retention strategies are needed.<br>
***(2)*** Engagement levels correlate strongly with feedback ratings, validating user-experience influence.<br>
***3)*** Regional differences highlight the need for localized learning support.<br>
***4)*** The Power BI dashboard allows non-technical stakeholders to explore these insights dynamically.<br>
***(5)*** Data Science and Design courses show strong engagement but moderate completion.Hence,Learners are actively participating but not up to completing the course.<br>

### DIII) Action Plan

***(1)*** Use dashboards to monitor trends in dropout reasons and identify which modules consistently drive disengagement.
***(2)*** Provide dedicated helpdesk support and knowledge base articles for technical or content-related queries.
</details>
