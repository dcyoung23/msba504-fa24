---
layout: default
title: "Assignments"
nav_order: 3
has_toc: false
permalink: /assignments/
---

## Assignment Breakdown

| **Assignment** | **Code `.yaml`** | **Document** `.pdf` |  **Question Based** |  **Collaboration**  | 
|:--------------:|:----------------:|:-------------------:|:-------------------:|
| Homework 1     | ✗                | ✓                  | ✗                   | 3-4 ✓               | 
| Homework 2     | ✓                | ✓                  | ✗                   | 1-2 ✓               |
| Homework 3     | ✓                | ✗                  | ✗                   | 1-2 ✓               |
| Homework 4     | ✓                | ✗                  | ✗                   | 1-2 ✓               |
| Homework 5     | ✓                | ✗                  | ✗                   | 1-2 ✓               |
| Lab 1          | ✗                | ✓                  | ✗                   | 4-5 ✓               |
| Lab 2          | ✓                | ✗                  | ✗                   | 1-2 ✓               |
| Lab 3          | ✓                | ✗                  | ✗                   | 2-3 ✓               |
| Quiz 1         | ✗                | ✗                  | ✓                   | ✗                   |
| Quiz 2         | ✗                | ✗                  | ✓                   | ✗                   |
| Quiz 3         | ✗                | ✗                  | ✓                   | ✗                   |
| Final Exam     | ✓                | ✗                  | ✓                   | ✗                   |
| Project 1      | ✓                | ✓                  | ✗                   | 2-3 ✓               |
| Project 2      | ✓                | ✗                  | ✗                   | 2-3 ✓               |
| Project 3      | ✓                | ✗                  | ✗                   | 2-3 ✓               |
| Project 4      | ✓                | ✓                  | ✗                   | 2-3 ✓               |


- **Code `.yaml`** file templates are used for each assignment that requires a code submission. This formatting allows for autograder functionality without requiring the submission of separate query files for every question. 
- **Document (.pdf)** files are used for free-form responses/images based on assignment instructions. 
- **Question Based**: Quizzes/Exams will have True/False, multiple choice, and matching questions completed on Canvas.
- **Collaboration** indicates the number of students permitted when collaboration is permitted for the assignment.

## Code Assignments

Autograder functionality on Gradescope is utilized for homework assignments 3-5 and group project assignment 3. This enables immediate grading of your code based assignments.

{: .highlight }
The autograder functionality is new so if you encounter any issues submitting your assignments, please notify the professor via email. Any bugs related to the autograder will be resolved ASAP and will not impact your assignment grades.

**Steps for Submission**:
1. **Download the Assignment Files**: All homework and group project assignment files will be provided on Canvas.
2. **Input Your Answers**: Populate the `.yaml` file with your responses for each respective question.
3. **Formatting Reference**: See the example `answer.yaml` file below to understand the required format. Critical components include the use of the "pipe" character for multiline strings and proper indentation. Incorrect formatting can result in the autograder misreading your submission.

```yaml
- question: 1
  answer: |
    SELECT * FROM student;

- question: 2
  answer: |
    INSERT INTO student (student_id, last_name, first_name, email_address) VALUES 
    (100001, 'Doe', 'Jane','jane.doe@domain.edu');
```
**Additional Formatting Notes**:
- The `.yaml` file will be provided complete with all of the required questions for the assignment. 
- Do **NOT** modify the "question" sections in the `.yaml` file.
- Do **NOT** change the name of the `.yaml` file provided for the assignment.
- To ensure accurate formatting, edit/paste your code into a text editor that supports `.yaml` files.

**Submitting Your Work**:
- Before submission, validate your file with a `.yaml` file [checker](https://yamlchecker.com/).
- Upload your completed `.yaml` file to Gradescope.
- You can re-submit your assignment multiple times before the due date.

{: .tip }

The `.yaml` file provided for the assignment will share the same file name as other assignments. Recommend you create a folder structure on your computer for each assignment to keep the assignment files organized.
