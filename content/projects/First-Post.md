---
title: "Comprehensive School Database System"
date: 2022-04-09T23:30:00+03:00
draft: false
toc: true
tags:
  - Database Design
  - SQL
  - Oracle
  - Education Technology
  - SQL*Plus
---

## Project Overview

As one of my first significant projects, I designed and implemented a comprehensive database system for a school environment using Oracle SQL. This project aimed to create a robust, scalable database that could efficiently manage various aspects of school operations, including student information, course management, employee data, library resources, and academic performance tracking.

## Key Features

- Comprehensive data model covering multiple school domains
- Complex relationships between entities (e.g., students, courses, employees, library)
- Implementation of various constraints to ensure data integrity
- Use of advanced SQL features like cascading deletes and virtual columns

## Technology Used

- **Oracle SQL**: Used for designing and implementing the database schema, including tables, relationships, and constraints.
- **SQL*Plus**: Utilized as the primary command-line interface for interacting with the Oracle database, executing SQL scripts, and testing queries.

## Database Schema

The database consists of 17 interconnected tables, each serving a specific purpose in the school's data ecosystem. Here's a high-level overview of the main entities and their relationships:

```mermaid
%%{init: {'theme': 'dark', 'themeVariables': { 'fontSize': '16px' }, 'flowchart': {'width': 1200, 'height': 800}}}%%
erDiagram
    Employee ||--o{ Emp_phone : has
    Employee ||--o{ Teacher : is_a
    Employee ||--o{ IT_Worker : is_a
    Employee ||--o{ Cleaning_Staff : is_a
    Employee ||--o{ librarian : is_a
    librarian ||--o{ lib_managers : manages
    Library ||--o{ lib_managers : managed_by
    Library ||--o{ Books : contains
    Library ||--o{ Members : has
    Students ||--o{ Members : is_a
    Students ||--o{ Enrollment : enrolls
    courses ||--o{ Enrollment : has
    Students ||--o{ Grades : receives
    courses ||--o{ Grades : has
    Students ||--o{ Exams : takes
    courses ||--o{ Exams : has
    Students ||--o{ Legal_Guardian : has
    Legal_Guardian ||--|| LG_Info : details
    LG_Info ||--o{ LG_Phones : has
    Teacher ||--o{ Class : teaches
    courses ||--o{ Class : taught_in
    Rooms ||--o{ Class : hosts

    Employee {
        NUMBER SSN
        NUMBER Emp_ID
        VARCHAR2 Fname
        VARCHAR2 Minit
        VARCHAR2 Lname
        CHAR Sex
        DECIMAL Salary
        VARCHAR2 Email
        DATE Bdata
        NUMBER Super_ID
    }

    Students {
        NUMBER Stud_SSN
        VARCHAR2 Fname
        VARCHAR2 Minit
        VARCHAR2 Lname
        DATE Bdata
        VARCHAR2 Stud_Address
        VARCHAR2 Email
    }

    courses {
        NUMBER Course_ID
        VARCHAR2 Course_Name
        VARCHAR2 Prerequisite
    }

    Library {
        NUMBER Lib_ID
        VARCHAR2 Lib_Name
    }

    Rooms {
        NUMBER Room_No
        NUMBER Floor_No
        NUMBER Capacity
    }

    Grades {
        NUMBER Stud_SSN
        NUMBER Course_ID
        VARCHAR2 Quarter
        NUMBER Behavior
        NUMBER Attendance
        NUMBER Year_Works
        NUMBER final_mark
    }
```

This Entity-Relationship Diagram (ERD) provides a visual representation of the database structure. It shows the main entities and their relationships, with detailed attributes for key tables.

## Technical Highlights

1. **Hierarchical Employee Structure**: Implemented using self-referencing foreign keys in the Employee table.

2. **Specialized Employee Types**: Used separate tables (Teacher, IT_Worker, etc.) linked to the main Employee table, demonstrating the concept of table inheritance.

3. **Grade Calculation**: Utilized Oracle's virtual column feature to automatically calculate final marks based on behavior, attendance, and year work.

```sql
final_mark number GENERATED ALWAYS AS ((Behavior/10) + (Attendance/10) + Year_Works) virtual
```

4. **Data Integrity**: Implemented various constraints including primary keys, foreign keys, and cascading deletes to maintain referential integrity.

5. **Complex Relationships**: Managed many-to-many relationships, such as between students and courses, using junction tables (e.g., Enrollment).

## Challenges and Solutions

1. **Challenge**: Designing a flexible structure for different types of employees.
   **Solution**: Implemented a general Employee table with specialized tables for different roles, allowing for easy addition of new employee types in the future.

2. **Challenge**: Ensuring data consistency across related tables.
   **Solution**: Utilized cascading deletes to automatically remove related records when a parent record is deleted, maintaining database integrity.

3. **Challenge**: Efficiently calculating student grades.
   **Solution**: Implemented a virtual column for final_mark, reducing the need for complex queries or application-level calculations.

## Lessons Learned

- The importance of thorough planning in database design
- Practical application of normalization principles
- Balancing between normalization and query performance
- The power of constraints in maintaining data integrity
- Real-world application of advanced SQL features

## Future Enhancements

- Implement more complex queries for generating reports (e.g., student performance analytics)
- Add indexing strategies to optimize query performance
- Develop a front-end application to interact with the database
- Implement additional security measures like row-level security and data encryption

## Conclusion

This project was a significant learning experience in database design and SQL. It provided hands-on experience with complex relationships, constraints, and advanced SQL features. The resulting database system forms a solid foundation for a school management system, demonstrating my ability to design and implement complex data structures.