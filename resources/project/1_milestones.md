---
title: Milestones
layout: default
parent: Project
grand_parent: Resources
nav_order: 2
---

## Project Milestones

Below are a high-level summary of the 4 milestones for the group project. Additional assignment instructions will be provided on Canvas.

### 1: Create an ERD and Database

In this assignment, you will assist the team and use your conceptual data modeling techniques to create an Entity-Relationship (ER) model in Crow’s Foot notation, representing the relationships between key entities. Additionally, you will define the cardinality and establish the correct relationships between tables to ensure the database is structured efficiently and logically. Once the model is established, you will create the necessary tables for the database in either PostgreSQL or SQLite, ensuring that each table includes appropriate data types, primary keys, foreign keys, and constraints. 

### 2: Transform and Load Database

In this assignment, you will transform and load the historical claims data from a raw denormalized state into the database created in milestone 1. Claims, driver, and vehicle information are all consolidated into a single row and will be expanded to the normalized tables. Historical claims data that precedes when additional claims tracking was implemented will be stored in single table to provide a longer historical of claims information for a policyholder.

### 3: Guided Analysis and Fraud Rule Identification

In this assignment, you will write SQL queries to answer a series of guided questions, similar to previous homework assignments. The goal of the project is to apply your analytical intuition and newly acquired SQL skills to explore historical data and identify potential fraud detection rules. This milestone focuses on getting the team started by identifying one possible rule that could be implemented for fraud detection. Given limited resources for the fraud investigation team, it is your responsibility to balance the risk between loss mitigation and false positives.

### 4: Present Your Analysis and Recommendations 

In this final assignment, you will create a technical presentation that summarizes your key findings and recommendations. Your fraud detection rules will be run on three months of synthetic claims data and fraud loss avoidances and false positive metrics will be evaluated.

{: .note }

The performance of your fraud detection rules will be used just for a friendly competition, but don’t worry—every team will walk away with some bonus points!