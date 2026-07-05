# Istanbul Urban Renewal Management System (IURMS)

## Project Overview
This project features a comprehensive "Urban Renewal Database Management System" designed to manage the end-to-end urban renewal processes of buildings that are at risk of earthquakes or have reached the end of their structural lifespan on a digital platform. The system manages the entire pipeline, starting from the initial application by the building owner(s). Ultimately, the system integrates the structural details of the buildings, risk reports, ownership rates, and transformation projects executed by contractor firms into a single, centralized hub.

## Core Functional Features
* **Basic Record Keeping:** Storing fundamental building records on a district basis, including location, construction year, and the number of floors.
* **Structural Data Logging:** Recording the structural details of buildings, such as soil type, foundation type, and the materials used.
* **Inspection & Risk Tracking:** Tracking the inspection reports assigned to buildings and the subsequent risk assessments generated from these reports.
* **Ownership Management:** Managing multiple owners within a single building along with their respective ownership rates.
* **Project & Contractor Matching:** Matching the transformation projects of buildings entering the demolition or reconstruction phase with the contractors undertaking these projects.

## Logical Database Architecture
The designed E-R model clearly illustrates the relationships and cardinality constraints among the entities to resolve the complex structure of the urban renewal process:

* **1:N Relationships:** Each district can contain multiple buildings. A single building may have multiple historical inspection reports or transformation project records.
* **1:1 Relationships:** A building can have only one set of structural details and one valid risk assessment.
* **M:N Relationships:** Since a building can have multiple owners and a single owner can possess shares in multiple buildings, this relationship has been resolved by introducing the `building_owners` bridge table. Similarly, the relationship between transformation projects and contractors has been normalized using the `project_contractors` table.

## Key SQL Implementations
The repository includes physical database scripts with robust constraints like:

```sql
CHECK (risk_score >= 0 AND risk_score <= 100)
```

and features diverse analytical queries:

* **Data Manipulation:** Scripts to insert new building evaluations, update project statuses, and clean up erroneous inspection reports.
* **Relational Joins:** Linking `districts` and `buildings` tables to list address information alongside localized district names.
* **Advanced Analytics:** Utilizing `GROUP BY`, `HAVING`, and aggregation functions like `AVG()` to identify high-priority districts with an average risk score higher than 50.
* **Nested Subqueries:** Filtering structural data by isolating buildings that currently lack a recorded risk assessment.
