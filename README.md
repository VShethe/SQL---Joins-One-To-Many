
# SQL: Joins-One To Many 





## Table of Content


**1. SQL: One To Many **
 - Joins.sql 
 - INNER_JOIN.sql
 - LEFT_JOIN.sql
 - RIGHT_JOIN.sql
 - DELETE_CASCADE.sql
 - One_To_Many_Exercise.sql
## Project Description

**Joins-One To Many:**

    CREATE DATABASE school;
![1](https://user-images.githubusercontent.com/128286364/233338674-2ca2da74-5477-48b9-96e6-21750d977aac.png)
![4](https://user-images.githubusercontent.com/128286364/233338923-d9583bdb-8e68-40a4-a24a-6b4842545f64.png)

    CREATE TABLE students (
        id INT AUTO_INCREMENT PRIMARY KEY,
        first_name VARCHAR(100)
    );
![students](https://user-images.githubusercontent.com/128286364/233338977-dc54049e-b6e5-4167-a470-abac609c589b.png)
![3](https://user-images.githubusercontent.com/128286364/233339063-2e44571f-cabc-4359-bf38-e525dcce762f.png)
    
    
    CREATE TABLE papers (
        title VARCHAR(100),
        grade INT,
        student_id INT,
        FOREIGN KEY (student_id) 
            REFERENCES students(id)
            ON DELETE CASCADE
    );
![papers](https://user-images.githubusercontent.com/128286364/233338766-667fcc24-b83c-4170-98b3-c17dd5f86557.png)
![2](https://user-images.githubusercontent.com/128286364/233339027-6cac540a-880f-4c94-9d45-199415ea9075.png)

    SELECT
        first_name,
        title,
        grade
    FROM students
    JOIN papers
    ON students.id = papers.student_id
    ORDER BY grade DESC;
![5](https://user-images.githubusercontent.com/128286364/233339368-b521b6b8-3771-4df3-a7a0-38f57b76d6a4.png)

    SELECT
        first_name,
        IFNULL(title, 'MISSING'),
        IFNULL(grade, '0')
    FROM students
    LEFT JOIN papers
    ON students.id = papers.student_id;
![6](https://user-images.githubusercontent.com/128286364/233339412-bdb72242-6c67-43ae-b468-7b3776aff32b.png)

    SELECT
        first_name,
        IFNULL(AVG(grade), 0) AS average
    FROM students
    LEFT JOIN papers
    ON students.id = papers.student_id
    GROUP BY students.id
    ORDER BY average DESC;
![7](https://user-images.githubusercontent.com/128286364/233339467-d0003387-a2a3-42fa-9dcc-38d32d2dc16e.png)


    SELECT
    first_name,
    IFNULL(AVG(grade), 0) AS average,
	CASE
	    WHEN Avg(grade) IS NULL THEN 'FAILING' 
        WHEN Avg(grade) >= 75 THEN 'PASSING' 
        ELSE 'FAILING'
	END AS passing_status
    FROM students
	LEFT JOIN papers
        ON students.id = papers.student_id
    GROUP BY students.id
    ORDER BY average DESC;
![8](https://user-images.githubusercontent.com/128286364/233339551-d9a7ab8e-d400-4c30-8800-996748f651f8.png)
  
   
## Installation

To run the program

mysq-ctl cli;
