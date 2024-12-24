**Background:**  
  - **Wilted Lotus** is a resort-style hotel in Orlando, Florida, known for affordable pricing and proximity to theme parks.  
  - Recent guest complaints regarding room cleanliness have tarnished the hotel’s reputation, impacting revenue and employee morale.  

**Project Goals:**  

  - Develop a relational database to improve **operational efficiency** and address issues impacting room readiness.  
  - Provide management with insights to identify key problem areas and optimize resource allocation.  

**Relational Database Development:**  
  - Centralized data for **7 entities**: guest stays, customer service staff, management staff, rooms, laundry crew, housekeepers, and suppliers.  
  - Designed relationships to ensure transparency and streamline decision-making.
 
![Conceptual Model ER Diagram](Conceptual%20Model%20ER%20Diagram.png)

## SQL Queries and Insights for Wilted Lotus

### Query 1 - Feedback Scores Based on Season
- **Objective**: Identify seasonal patterns in guest satisfaction scores to improve resource allocation.
- **Findings**:
  - Summer had the lowest average scores for housekeeping and laundry services.
  - Suggests summer-specific hiring to address increased demand during peak travel season.
- **Output**: Average scores for housekeeping, laundry, and customer service by season.
- **SQL Code**:
 
  SELECT 'Fall' AS Season, AVG(hkScore) AS avg_hkScore, AVG(LScore) AS avg_LScore, AVG(servScore) AS avg_servScore
  FROM Guest_stay
  WHERE MONTH(CheckIn) IN (9, 10, 11)
  UNION
  SELECT 'Winter' AS Season, AVG(hkScore), AVG(LScore), AVG(servScore)
  FROM Guest_stay
  WHERE MONTH(CheckIn) IN (12, 1, 2)
  UNION
  SELECT 'Spring', AVG(hkScore), AVG(LScore), AVG(servScore)
  FROM Guest_stay
  WHERE MONTH(CheckIn) IN (3, 4, 5)
  UNION
  SELECT 'Summer', AVG(hkScore), AVG(LScore), AVG(servScore)
  FROM Guest_stay
  WHERE MONTH(CheckIn) IN (6, 7, 8);

**Visualized Feedback Scores in R**

![Feedback_Scores_By_Season](Feedback_Scores_By_Season.png)

### Query 2- Feedback Scores for Repeat Customers vs Non-repeat

The primary goal for our database is to increase the efficiency of Wilted Lotus and consequently improve guest satisfaction. One way to effectively evaluate overall guest satisfaction is by looking at feedback scores. Ultimately, however, Wilted Lotus would want to see managerial improvements result in not just improved feedback scores but also more satisfied guests returning and staying again. Successful customer retention would incentivize the hotel to continually improve efficiency since that would provide a stable base of customers to earn revenue from.

- **SQL Code**:
  SELECT AVG(hkScore) AS Housekeeping_Score_Avg, 
       AVG(LScore) AS Laundry_Score_Avg, 
       AVG(servScore) AS Customer_Service_Avg, 
       SUM(hkScore + LScore + servScore) / (COUNT(*)*3) AS All_Score_Avg,
       IF(guestID IN(SELECT guestID FROM guest_stay GROUP BY guestID HAVING COUNT(DISTINCT tripID)>1), "Y", "N") AS Repeat_Customer
FROM guest_stay
GROUP BY Repeat_Customer
ORDER BY Repeat_Customer;


**Outcomes:**  
  - Enabled identification of trends contributing to unclean rooms, such as staffing shortages or supply mismanagement.  
  - Improved resource allocation by pinpointing high-impact issues, like increasing housekeeper staff during peak seasons.  
  - Enhanced communication across staff roles by providing a **singular reference system** for customer and supplier information.  

**Business Recommendations:**  
  - Hire seasonal housekeepers during high-demand periods to meet turnover demands.  
  - Focus on ensuring sufficient supply orders are placed in advance to avoid disruptions.  
  - Reduce error in decision-making through actionable insights provided by the database.  

### Welcome to my portfolio!  
This project highlights how a well-designed relational database can solve real-world business problems in the competitive hospitality industry.  
