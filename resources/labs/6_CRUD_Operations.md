---
title: CRUD Operations
layout: default
parent: Labs
grand_parent: Resources
nav_order: 1
---

# CRUD Operations Lab

## Part 1: Create University Database

In this lab, you will work with a group of 4-5 students and create the `university` database discussed in previous lecture materials. The day [4_Create_Database](../demos/4_Create_Database.html) demo will be useful for the `CREATE TABLE` statements for all 4 tables.

{: .important }

Be sure to define all `PRIMARY KEY`, `FOREIGN KEY` and `CHECK` constraints in your `CREATE TABLE` statements because several tasks require you to validate these constraints. Also, the `fee` column should be removed from the `course` table since that was just used as an example in the lecture.

**All tasks for the lab do NOT need to be completed during class.** However, please make sure to submit your work in progress before the end of class for the lab attendance portion of the grade (5 points). You can complete the remaining tasks at home before the late submission deadline (Friday 11:59 PM). Although this is an in class group exercise, each member must submit their own PDF version of the Google Doc template on Canvas/Gradescope.

## Part 2: Update Database

### Create `student` records for your group

Create `INSERT INTO` statements for the `student` table and update the database for everyone in your group.

### Create `course` records for your group

Here are `INSERT INTO` statements for the courses offered this Fall. The Spring schedule has not been released yet but discuss with your group the courses that everyone will be taking in the Spring and write additional `INSERT INTO` statements for those courses. Please refer to this [page](https://catalogs.sandiego.edu/graduate/courses/msba/) for MSBA course numbers.

``` sql
INSERT INTO course (course_num, title, credits) 
VALUES(	502, 'Analytics Programming I',  2);
INSERT INTO course (course_num, title, credits) 
VALUES(	503, 'Analytics Programming II', 2);
INSERT INTO course (course_num, title, credits) 
VALUES(	501, 'Applied Statistics',  2);
INSERT INTO course (course_num, title, credits) 
VALUES(	504, 'Data Management', 2);
INSERT INTO course (course_num, title, credits) 
VALUES(	507, 'Data for Social Good', 3);
INSERT INTO course (course_num, title, credits) 
VALUES(	500, 'Intro to Data Analytics',  2);
INSERT INTO course (course_num, title, credits) 
VALUES(	505, 'Interactive Data Visualization', 3);
INSERT INTO course (course_num, title, credits) 
VALUES(	506, 'Prescriptive Analytics',  2);  
```

### Create `class_schedule` records for the Fall and Spring

Here is one `INSERT INTO` statement for our class.

``` sql
INSERT INTO class_schedule (section_num, course_num, course_section, start_date, end_date, instructor) 
VALUES(	1666, 504, '01', '2024-09-03', '2024-10-22', 'Young');
```
Use the USD Course Search [page](https://usdssb.sandiego.edu/prod/usd_course_query.p_start) to lookup the remaining Fall schedule to create the additional insert statements. Use the `CRN` for the `section_num` column in our database. Since the Spring schedule has not been released yet, you can estimate the start and end dates, use TBD for the instructor, and create your own **artificial key** for the `section_num` that does not violate the PK.

{: .note }

Professor Young will be teaching MSBA 511 in the Spring.

### Create `enrollment` records for your group.

Create `INSERT INTO` statements for the `enrollment` table and update the database for everyone in your group.

## Part 3: Final Tasks

To get credit for this lab, you will need to complete the following tasks and copy/paste screenshots in the [Lab1_CRUD_Operations_Template](https://docs.google.com/document/d/1yB5FklY8NQ7PfBeGQaAwfbpH2XyS3rzmamuvkEodeQ8/edit?usp=sharing). Make sure to Make a copy of the template to your Google Drive or download as a Microsoft Word (.docx) file.

{: .tip }

You can split up these 10 tasks between your group for faster completion.

### Task 1

Write a `SELECT` statement to display all columns and rows in the `student` table.

### Task 2

Write a `SELECT` statement to display all columns and all rows in the `course` table.

### Task 3

Write a `SELECT` statement to display all columns and all rows in the `class_schedule` table.

### Task 4

Write an `INSERT INTO` statement for a duplicate course in the `course` table.

### Task 5

Write an `UPDATE` statement on the `course` table that violates the `CHECK` constraint on the `credits` column.

### Task 6

Write a `DELETE` statement for the `student` table for a student that is already enrolled in a course.

### Task 7

Write a `DELETE` statement for the `course` table for a course that is already on the class schedule.

### Task 8

Write an `INSERT INTO` statement for `enrollment` table for an unknown course section.

### Task 9

Write an `INSERT INTO` statement for the `enrollment` table for a student that is already enrolled in the course section.

### Task 10

Run the following SQL to get the final summary output of your University database tables.

``` sql
SELECT
  s.student_id,
  s.last_name as student_last_name,
  s.first_name as student_first_name,
  s.email_address as student_email,
  c.course_num,
  c.title as course_title,
  cs.course_section,
  cs.start_date as course_start_date,
  cs.end_date as course_end_date,
  c.credits,
  cs.instructor
FROM student s
INNER JOIN enrollment e ON s.student_id = e.student_id
INNER JOIN class_schedule cs ON e.section_num = cs.section_num
INNER JOIN course c ON cs.course_num = c.course_num;
```

## Submission

Submit the completed [Lab1_CRUD_Operations_Template](https://docs.google.com/document/d/1yB5FklY8NQ7PfBeGQaAwfbpH2XyS3rzmamuvkEodeQ8/edit?usp=sharing) as a PDF document on Canvas/Gradescope.


