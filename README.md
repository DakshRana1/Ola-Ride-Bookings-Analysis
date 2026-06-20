🚖 Ola Ride Bookings Analysis
📌 Project Overview
This repository contains an end-to-end data analysis project focusing on Ola ride booking and cancellation patterns. By analyzing localized ride data over a one-month operational period, this project uncovers actionable insights regarding customer demand, vehicle utilization, revenue distribution, and operational inefficiencies (such as driver/customer cancellation drivers).

The goal is to assist decision-makers in optimizing driver allocation, reducing cancellation rates, and maximizing weekly booking values.

📂 Repository Structure
Plaintext


Ola-Ride-Bookings-Analysis/
│
├── Data/
│   ├── raw_bookings.csv          # Original uncleaned dataset
│   └── cleaned_bookings.xlsx     # Preprocessed data used for BI dashboards
│
├── SQL/
│   ├── database_schema.sql       # Database & table creation scripts
│   ├── data_cleaning.sql         # SQL validation & constraint checks
│   └── business_queries.sql      # Core queries addressing KPIs
│
├── Dashboards/
│   ├── Ola_Bookings_Analysis.twbx # Tableau Packaged Workbook (if using Tableau)
│   └── Ola_Bookings_Analysis.pbix # Power BI Dashboard file (if using Power BI)
│
└── README.md                     # Project documentation
🛠️ Technologies Used
Excel: Initial data cleaning, structural sanity checks, and schema validation.

SQL (MySQL Workbench): Heavy lifting for exploratory data analysis (EDA), generating summary metrics, and querying business-critical views.

Tableau / Power BI: Interactive dashboard creation to visualize multi-dimensional data models and KPIs.

📊 Dataset & KPI Constraints
The dataset spans over 100,000 unique booking entries with key fields including Booking ID, Booking Status, Customer ID, Vehicle Type (Auto, Mini, Prime Sedan, SUV, Bike), Pickup/Drop Locations, Cancelled Rides Reason, Customer/Driver Ratings, and Booking Value.

To mimic real-world operational health, the analysis benchmarks the data against the following industry targets:

Booking Success Rate: Kept at a baseline ~62%.

Customer Cancellations: Target capped below 7%.

Driver Cancellations: Target capped below 18%.

Incomplete Rides: Restricted to less than 6%.

🔍 Core Business Questions Answered via SQL
The SQL/business_queries.sql script resolves 10 major operational questions. Here are a few foundational examples:

1. Retrieve all successful bookings
SQL


CREATE VIEW Successful_Bookings AS
SELECT * 
FROM bookings 
WHERE Booking_Status = 'Success';
2. Find the average ride distance for each vehicle type
SQL


CREATE VIEW Avg_Distance_Per_Vehicle AS
SELECT Vehicle_Type, AVG(Ride_Distance) AS avg_distance 
FROM bookings 
GROUP BY Vehicle_Type;
3. Identify the Top 5 customers by total booking value
SQL


SELECT Customer_ID, SUM(Booking_Value) AS total_spent 
FROM bookings 
WHERE Booking_Status = 'Success'
GROUP BY Customer_ID 
ORDER BY total_spent DESC 
LIMIT 5;
4. Analyze main reasons for driver-led cancellations
SQL


SELECT Cancelled_Rides_by_Driver, COUNT(*) AS total_cancellations
FROM bookings
WHERE Booking_Status = 'Cancelled by Driver'
GROUP BY Cancelled_Rides_by_Driver
ORDER BY total_cancellations DESC;
🎛️ Dashboard Insights & Visualizations
The interactive dashboards break down the data into 4 major operational dimensions:

Overall Performance: Tracking total bookings, success rate vs. cancellation split, and localized demand metrics over time.

Vehicle Performance: Evaluating which segments (e.g., Prime Sedan vs. Ola Auto) drive the highest margins and average distances.

Revenue Analysis: Deep dive into payment processing metrics (UPI, Cash, Credit Card) and tracking the lifetime value (LTV) of top customer cohorts.

Cancellation Breakdown: Granular charts isolating precisely why drivers (e.g., "Personal/Car issues") and customers (e.g., "Change of plans") abandon rides.

🚀 How to Replicate This Project
Step 1: Database Setup
Open MySQL Workbench and connect to your instance.

Execute the SQL/database_schema.sql file to build your structure.

Import Data/raw_bookings.csv via the MySQL Table Data Import Wizard.

Step 2: Extract Insights
Run SQL/business_queries.sql to generate optimization metrics and create necessary relational views.

Step 3: BI Dashboard Exploration
Launch Tableau Desktop or Power BI Desktop.

Open the file located in the Dashboards/ directory.

Re-link the data source to your local SQL views or the clean xlsx sheet to explore custom metrics interactively.

🧑‍💻 Author
Daksh Rana - GitHub Profile

📄 License
This project is licensed under the MIT License - see the LICENSE file for details.
