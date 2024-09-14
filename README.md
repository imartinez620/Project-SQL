# Project-SQL

## Project Overview
Build a SQL database for a university that manages students, courses, professors, and grades.

## Project Technical Requirements
### The project needs to contain the following technical features:
- Build a database with the following tables: Students, Courses, Professors, Grades
- Foreign key relationships between the tables
- Create a script that populates all of the database tables with sample data
- SQL query scripts for:
    - The average grade that is given by each professor
    - The top grades for each student
    - Sort students by the courses that they are enrolled in
    - Create a summary report of courses and their average grades, sorted by the most challenging course (course with the lowest average grade) to the easiest course
    - Finding which student and professor have the most courses in common


## Submission options: 
Push all scripts to a single Github repository and submit the link to a Mentor through the support app. If you're not familiar with Github, create a separate gist for all of the scripts and submit the gist through the support app.

- Crea el espacio de trabajo
- 
CREATE SCHEMA `bottega_university`;

- Crea la tabla students
- 
CREATE TABLE `bottega_university`.`students` (
  `students_id` INT NOT NULL AUTO_INCREMENT,
  `students_name` VARCHAR(80) NOT NULL,
  `students_email` VARCHAR(80) NOT NULL,
  PRIMARY KEY (`students_id`),
  UNIQUE INDEX `users_id_UNIQUE` (`students_id` ASC) VISIBLE,
  UNIQUE INDEX `students_email_UNIQUE` (`students_email` ASC) VISIBLE);

- Crea la tabla courses
- 
CREATE TABLE `bottega_university`.`courses` (
  `courses_id` INT NOT NULL AUTO_INCREMENT,
  `courses_name` VARCHAR(120) NOT NULL,
  `professors_id` INT NOT NULL,
  PRIMARY KEY (`courses_id`),
  UNIQUE INDEX `courses_id_UNIQUE` (`courses_id` ASC) VISIBLE,
  UNIQUE INDEX `courses_name_UNIQUE` (`courses_name` ASC) VISIBLE);

- Crea la tabla professors
- 
CREATE TABLE `bottega_university`.`professors` (
  `professors_id` INT NOT NULL AUTO_INCREMENT,
  `professors_name` VARCHAR(80) NOT NULL,
  `professors_email` VARCHAR(80) NOT NULL,
  PRIMARY KEY (`professors_id`),
  UNIQUE INDEX `professors_id_UNIQUE` (`professors_id` ASC) VISIBLE,
  UNIQUE INDEX `professors_mail_UNIQUE` (`professors_email` ASC) VISIBLE);

- Crea la tabla grades
- 
CREATE TABLE `bottega_university`.`grades` (
  `grades_id` INT NOT NULL AUTO_INCREMENT,
  `course_id` INT NOT NULL,
  `students_id` INT NOT NULL,
  `nota` DECIMAL(4,2) NULL,
  PRIMARY KEY (`grades_id`),
  UNIQUE INDEX `grades_id_UNIQUE` (`grades_id` ASC) VISIBLE);
  
