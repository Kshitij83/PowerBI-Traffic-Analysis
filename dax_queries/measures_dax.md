# Power BI DAX Measures for Traffic Analysis

## 1. Average Green Light Duration
Calculates the average duration of green lights across all intersections.
```DAX
Avg Green Light Duration = AVERAGE(Merge1[Green_Light_Duration])
```

## 2. Average Red Light Duration
Calculates the average duration of red lights across all intersections.
```DAX
Avg Red Light Duration = AVERAGE(Merge1[Red_Light_Duration])
```

## 3. Average Vehicles Per Hour
Finds the average number of vehicles passing through an intersection per hour.
```DAX
Avg Vehicles Per Hour = AVERAGE(Merge1[Vehicle_Count])
```

## 4. Peak Traffic Hour
Identifies the hour of the day with the highest traffic volume.
```DAX
Peak Traffic Hour = 
VAR MaxTraffic = MAXX(VALUES(Merge1[Hour]), SUM(Merge1[Vehicle_Count]))
RETURN
    FIRSTNONBLANK(
        FILTER(VALUES(Merge1[Hour]), SUM(Merge1[Vehicle_Count]) = MaxTraffic),
        0
    )
```

## 5. Red-Green Difference
Calculates the difference between total red light duration and total green light duration.
```DAX
Red-Green Difference = 
SUM(Merge1[Red_Light_Duration]) - SUM(Merge1[Green_Light_Duration])
```

## 6. Total Vehicles
Computes the total count of vehicles recorded in the dataset.
```DAX
Total Vehicles = SUM(Merge1[Vehicle_Count])
```

## 7. Vehicle Percentage
Determines the percentage of vehicles passing through each intersection relative to the total.
```DAX
Vehicle % = 
VAR TotalVehicles = CALCULATE(SUM(Merge1[Vehicle_Count]), ALL(Merge1))
RETURN
    DIVIDE(SUM(Merge1[Vehicle_Count]), TotalVehicles, 0)
```