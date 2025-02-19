
# 🚦 PowerBI Traffic Analysis  

This repository contains a **Power BI dashboard** for analyzing urban traffic patterns. The analysis focuses on **traffic flow, signal durations, vehicle distribution, and peak traffic hours** to provide data-driven insights for traffic optimization.  

## 📊 Dashboard Overview  

### 🔹 Key Features:  
- **Traffic Distribution by Intersections**: Identifies the busiest intersections.  
- **Traffic Flow by Hour**: Visualizes vehicle count variations throughout the day.  
- **Vehicle Distribution by Type**: Shows the percentage split between different vehicle types.  
- **Green & Red Light Duration Comparison**: Highlights variations in signal timings across intersections.  
- **Peak Traffic Hours**: Determines the hours with the highest congestion.  

## 🔍 Inferences  

- **Intersection 4** had the highest vehicle count, indicating heavy congestion.  
- **Intersection 3** had the highest negative disparity between red and green light durations (longer red light times), causing potential bottlenecks.  
- **Intersection 7** had the highest positive disparity (longer green light times), allowing for smoother traffic flow.  
- **Suggested Optimization**:  
  - Balance red and green light durations between **Intersection 3 and 7** to redistribute traffic flow.  
  - Increase green light duration slightly at **Intersection 3** to reduce congestion.  
  - Adjust timings at **Intersection 4** based on vehicle density to improve overall flow.  

## 🛠️ DAX Queries Used  

The following **DAX measures** were used to derive key insights:  

```DAX
Avg Green Light Duration = AVERAGE(Merge1[Green_Light_Duration])
Avg Red Light Duration = AVERAGE(Merge1[Red_Light_Duration])
Avg Vehicles Per Hour = AVERAGE(Merge1[Vehicle_Count])

Peak Traffic Hour = 
VAR MaxTraffic = MAXX(VALUES(Merge1[Hour]), SUM(Merge1[Vehicle_Count]))
RETURN
    FIRSTNONBLANK(
        FILTER(VALUES(Merge1[Hour]), SUM(Merge1[Vehicle_Count]) = MaxTraffic),
        0
    )

Red-Green Difference = 
SUM(Merge1[Red_Light_Duration]) - SUM(Merge1[Green_Light_Duration])

Total Vehicles = SUM(Merge1[Vehicle_Count])

Vehicle % = 
VAR TotalVehicles = CALCULATE(SUM(Merge1[Vehicle_Count]), ALL(Merge1))
RETURN
    DIVIDE(SUM(Merge1[Vehicle_Count]), TotalVehicles, 0)
```  

## 📂 Repository Structure  

```
📂 PowerBI-Traffic-Analysis  
│── 📁 Reports  
│   ├── Traffic flow analysis template.pbit  
│   ├── Traffic flow analysis (Power BI).pbix  
│   ├── Traffic flow analysis report.pdf  
│  
│── 📁 Screenshots  
│   ├── modelView/dataStructure.jpg  
│   ├── reportView/page1.jpg  
│   ├── reportView/page2.jpg  
│   ├── reportView/page3.jpg  
│   ├── reportView/page4.jpg  
│  
│── 📁 dax_queries  
│   ├── measures_dax.md  
│  
│── 📄 README.md  
│── 📄 .gitignore  
```  

## 🔗 How to Use  

1. Clone the repository:  
   ```sh
   git clone https://github.com/Kshitij83/PowerBI-Traffic-Analysis.git
   ```  
2. Open the **Power BI** file (`.pbix`) to explore the dashboard.  
3. Modify or extend the analysis using the provided **DAX queries**.  

## 📧 Contact  

For any queries or contributions, feel free to connect!  

---
