---
title: Create Database
layout: default
parent: Demos
grand_parent: Resources
nav_order: 2
---

# Create Database

## Overview
In this demo, we will create the simplified version of the University database discussed in the day 1_Introduction lecture. We will be using DB Browser for SQLite. Click here to go to the DB Browser downloads page and follow the instructions to install the application for your operating system.

{: .note }

As always, certain aspects of this example have been abbreviated for the purposes of this lab exercise. The scenario is not intended to represent a complete depiction of a real-world university.

## Introduction to SQLite
SQLite is a small and efficient SQL database engine. It is often used for small and embedded databases because it doesn't require a separate server process and is easy to integrate into applications. The entire database including all of the tables, indices, and the data itself is stored in the .db file on your computer. SQLite is highly portable and lightweight, since it has no external dependencies and is used in mobile apps, desktop software, and even in some web apps.

## Create Database
Open DB Browser and click on the New Database. Browse to the desired destination on your computer, name the new database university and click on Save. You can click on Cancel on the popup window to Edit table definition.

## Option 1 - Create Table SQL Statements
In this option, we will be writing the SQL statements to create tables named `student`, `course`, `class_schedule`, and `enrollment`.

### Create the `student` Table
Click on the Execute SQL tab and SQL 1 tab. Copy the SQL code below and paste into the new query tab.

``` sql
CREATE TABLE student (
  student_id int NOT NULL, 
  last_name varchar(25) NOT NULL, 
  first_name varchar(25) NOT NULL, 
  email_address varchar(50) NOT NULL, 
  CONSTRAINT student_pk PRIMARY KEY(student_id)
);
```
Click on the blue triangle to execute the code to create the new table.

💡 Tip: Use ctrl-enter on Windows or command-enter on Mac as a shortcut to execute code in DB Browser. For the rest of this lab, we will simply just say to execute the code and you can use the method that you prefer.

{: .warning }

If you attempt to run the CREATE TABLE more than once, you will get an Execution error because the table already exists. We will discuss ways to avoid these errors later in this lab.

### Create the `course` Table
Copy the SQL code below and paste below the `CREATE TABLE student` code.

``` sql
CREATE TABLE course (
  course_num int NOT NULL,
  title varchar(50) NOT NULL,
  credits int NOT NULL CHECK (credits > 0),
  fee decimal(10,2) NOT NULL,
  CONSTRAINT course_pk PRIMARY KEY(course_num)
);
```
Select only the code to create the `course` table and execute the code to create the new table.

{: .note }

Most database tools allow you to execute only the selected code in this way.

### Create the `class_schedule` Table
Copy the SQL code below and paste below the `CREATE TABLE course` code.

``` sql
CREATE TABLE class_schedule (
  section_num int NOT NULL, 
  course_num int NOT NULL, 
  course_section char(2) NOT NULL, 
  start_date date NOT NULL, 
  end_date date NOT NULL, 
  instructor varchar(50) NOT NULL, 
  CONSTRAINT class_schedule_pk PRIMARY KEY(section_num), 
  CONSTRAINT class_schedule_course_fk FOREIGN KEY (course_num) REFERENCES course(course_num)
);
```
Select only the code to create the `class_schedule` table and execute the code to create the new table.

### Create the `enrollment` Table
Copy the SQL code below and paste below the `CREATE TABLE class_schedule` code.

``` sql
CREATE TABLE enrollment (
  student_id int NOT NULL, 
  section_num int NOT NULL, 
  CONSTRAINT enrollment_pk PRIMARY KEY (student_id, section_num), 
  CONSTRAINT enroll_student_fk FOREIGN KEY (student_id) REFERENCES student(student_id), 
  CONSTRAINT enroll_course_fk FOREIGN KEY (section_num) REFERENCES class_schedule(section_num)
);
```
Select only the code to create the `enrollment` table and execute the code to create the new table.

### Add Drop Table Statements
Copy the SQL code below and paste at the top above the `CREATE TABLE student` code.

``` sql
DROP TABLE IF EXISTS enrollment;
DROP TABLE IF EXISTS class_schedule;
DROP TABLE IF EXISTS course;
DROP TABLE IF EXISTS student;
```
These statements will drop all of the tables if they already exist.

{: .note }

SQLite does not enforce referential integrity constraints on `DROP TABLE` statements but most other DBMS such as PostgreSQL do. Dropping the tables in this order resolves potential errors related to `FOREIGN KEY` constraints.

## Option 2 - ERD with Export SQL
Many web apps such as [QuickDBD](https://app.quickdatabasediagrams.com/) allow you to draw database diagrams by typing using proprietary syntax. In addition, you want to pick an app that also offers export functionality to automatically generate your `CREATE TABLE` statements.

### Create New Diagram

1. Go to [QuickDBD)](https://app.quickdatabasediagrams.com/).

Click on File -> Load Sample Diagram to load the sample to familiar

{: .note }

Creating an account with QuickDBD will allow you to save your diagram as well as share and collaborate with others. A Pro Account is required to save more than one diagram but you can always save the diagram code to your computer and paste into a blank diagram as needed.










