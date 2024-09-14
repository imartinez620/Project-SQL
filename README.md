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

- **Crea el espacio de trabajo**
  
CREATE SCHEMA `bottega_university`;

- **Crea la tabla students**
  
CREATE TABLE `bottega_university`.`students` (
  `students_id` INT NOT NULL AUTO_INCREMENT,
  `students_name` VARCHAR(80) NOT NULL,
  `students_email` VARCHAR(80) NOT NULL,
  PRIMARY KEY (`students_id`),
  UNIQUE INDEX `users_id_UNIQUE` (`students_id` ASC) VISIBLE,
  UNIQUE INDEX `students_email_UNIQUE` (`students_email` ASC) VISIBLE);

- **Crea la tabla courses**
  
CREATE TABLE `bottega_university`.`courses` (
  `courses_id` INT NOT NULL AUTO_INCREMENT,
  `courses_name` VARCHAR(120) NOT NULL,
  `professors_id` INT NOT NULL,
  PRIMARY KEY (`courses_id`),
  UNIQUE INDEX `courses_id_UNIQUE` (`courses_id` ASC) VISIBLE,
  UNIQUE INDEX `courses_name_UNIQUE` (`courses_name` ASC) VISIBLE);

- **Crea la tabla professors**
  
CREATE TABLE `bottega_university`.`professors` (
  `professors_id` INT NOT NULL AUTO_INCREMENT,
  `professors_name` VARCHAR(80) NOT NULL,
  `professors_email` VARCHAR(80) NOT NULL,
  PRIMARY KEY (`professors_id`),
  UNIQUE INDEX `professors_id_UNIQUE` (`professors_id` ASC) VISIBLE,
  UNIQUE INDEX `professors_mail_UNIQUE` (`professors_email` ASC) VISIBLE);

- **Crea la tabla grades**
  
CREATE TABLE `bottega_university`.`grades` (
  `grades_id` INT NOT NULL AUTO_INCREMENT,
  `course_id` INT NOT NULL,
  `students_id` INT NOT NULL,
  `nota` DECIMAL(3,2) NULL,
  PRIMARY KEY (`grades_id`),
  UNIQUE INDEX `grades_id_UNIQUE` (`grades_id` ASC) VISIBLE);

  

- **Relacion de la tabla cursos con la de profesores**

ALTER TABLE `bottega_university`.`courses` 
ADD INDEX `professors_id_idx` (`professors_id` ASC) VISIBLE;
;
ALTER TABLE `bottega_university`.`courses` 
ADD CONSTRAINT `professors_id`
  FOREIGN KEY (`professors_id`)
  REFERENCES `bottega_university`.`professors` (`professors_id`)
  ON DELETE NO ACTION
  ON UPDATE NO ACTION;

- **Relacion de la tabla grades con la de students y courses**

ALTER TABLE `bottega_university`.`grades` 
ADD INDEX `course_id_idx` (`course_id` ASC) VISIBLE,
ADD INDEX `students_id_idx` (`students_id` ASC) VISIBLE;
;
ALTER TABLE `bottega_university`.`grades` 
ADD CONSTRAINT `course_id`
  FOREIGN KEY (`course_id`)
  REFERENCES `bottega_university`.`courses` (`courses_id`)
  ON DELETE NO ACTION
  ON UPDATE NO ACTION,
ADD CONSTRAINT `students_id`
  FOREIGN KEY (`students_id`)
  REFERENCES `bottega_university`.`students` (`students_id`)
  ON DELETE NO ACTION
  ON UPDATE NO ACTION;

  

- **Script para insertar datos**
  
-- **Insertar 30 estudiantes**

INSERT INTO `bottega_university`.`students` (`students_name`, `students_email`)
VALUES
('John Doe', 'john.doe@example.com'),
('Jane Smith', 'jane.smith@example.com'),
('Michael Johnson', 'michael.johnson@example.com'),
('Emily Davis', 'emily.davis@example.com'),
('Daniel Brown', 'daniel.brown@example.com'),
('Jessica Williams', 'jessica.williams@example.com'),
('David Jones', 'david.jones@example.com'),
('Laura Garcia', 'laura.garcia@example.com'),
('James Martinez', 'james.martinez@example.com'),
('Mia Rodriguez', 'mia.rodriguez@example.com'),
('Sophia Lee', 'sophia.lee@example.com'),
('Lucas White', 'lucas.white@example.com'),
('Oliver Harris', 'oliver.harris@example.com'),
('Ethan Clark', 'ethan.clark@example.com'),
('Charlotte Lewis', 'charlotte.lewis@example.com'),
('Henry Walker', 'henry.walker@example.com'),
('Amelia Young', 'amelia.young@example.com'),
('Ava King', 'ava.king@example.com'),
('Liam Scott', 'liam.scott@example.com'),
('Emma Green', 'emma.green@example.com'),
('Benjamin Hall', 'benjamin.hall@example.com'),
('Evelyn Adams', 'evelyn.adams@example.com'),
('Grace Nelson', 'grace.nelson@example.com'),
('Lucas Carter', 'lucas.carter@example.com'),
('Emily Mitchell', 'emily.mitchell@example.com'),
('Daniel Perez', 'daniel.perez@example.com'),
('Sophia Hill', 'sophia.hill@example.com'),
('Mason Baker', 'mason.baker@example.com'),
('Ella Wright', 'ella.wright@example.com'),
('Isabella Torres', 'isabella.torres@example.com');

-- **Insertar 5 profesores**

INSERT INTO `bottega_university`.`professors` (`professors_name`, `professors_email`)
VALUES
('Professor Smith', 'prof.smith@example.com'),
('Professor Johnson', 'prof.johnson@example.com'),
('Professor Davis', 'prof.davis@example.com'),
('Professor Lee', 'prof.lee@example.com'),
('Professor Martinez', 'prof.martinez@example.com');

-- **Insertar 5 asignaturas**

INSERT INTO `bottega_university`.`courses` (`courses_name`, `professors_id`)
VALUES
('Mathematics', 1),
('Physics', 2),
('Computer Science', 3),
('History', 4),
('Chemistry', 5);

-- **Insertar notas**

INSERT INTO `bottega_university`.`grades` (`course_id`, `students_id`, `nota`)
VALUES
-- **Matemáticas (course_id 1)**

(1, 1, 8.75), (1, 2, 9.2), (1, 3, 7.12), (1, 4, 9.89), (1, 5, 6.54),
(1, 6, 8.35), (1, 7, 7.92), (1, 8, 9.13), (1, 9, 8.45), (1, 10, 7.72),
(1, 11, 9.67), (1, 12, 6.94), (1, 13, 8.21), (1, 14, 9.35), (1, 15, 7.60),
(1, 16, 9.44), (1, 17, 8.51), (1, 18, 7.38), (1, 19, 8.98), (1, 20, 9.12),
(1, 21, 7.86), (1, 22, 8.79), (1, 23, 7.33), (1, 24, 9.55), (1, 25, 6.95),
(1, 26, 9.12), (1, 27, 8.34), (1, 28, 7.58), (1, 29, 9.88), (1, 30, 8.65),

-- **Física (course_id 2)**

(2, 1, 9.12), (2, 2, 8.75), (2, 3, 7.95), (2, 4, 9.47), (2, 5, 6.86),
(2, 6, 9.33), (2, 7, 8.44), (2, 8, 7.98), (2, 9, 9.00), (2, 10, 8.13),
(2, 11, 9.25), (2, 12, 7.88), (2, 13, 8.63), (2, 14, 7.95), (2, 15, 9.76),
(2, 16, 8.42), (2, 17, 9.78), (2, 18, 8.11), (2, 19, 9.88), (2, 20, 7.60),
(2, 21, 8.35), (2, 22, 9.56), (2, 23, 7.54), (2, 24, 9.25), (2, 25, 8.02),
(2, 26, 9.45), (2, 27, 7.63), (2, 28, 8.97), (2, 29, 9.11), (2, 30, 8.55),

-- **Ciencias de la Computación (course_id 3)**

(3, 1, 8.99), (3, 2, 9.15), (3, 3, 7.86), (3, 4, 9.05), (3, 5, 6.54),
(3, 6, 8.67), (3, 7, 9.22), (3, 8, 7.75), (3, 9, 8.43), (3, 10, 7.89),
(3, 11, 9.05), (3, 12, 7.99), (3, 13, 8.66), (3, 14, 9.35), (3, 15, 8.72),
(3, 16, 9.46), (3, 17, 7.84), (3, 18, 9.25), (3, 19, 8.51), (3, 20, 9.89),
(3, 21, 8.10), (3, 22, 9.77), (3, 23, 8.55), (3, 24, 9.24), (3, 25, 8.66),
(3, 26, 9.10), (3, 27, 8.77), (3, 28, 9.48), (3, 29, 7.65), (3, 30, 9.55),

-- **Historia (course_id 4)**

(4, 1, 9.30), (4, 2, 8.05), (4, 3, 9.95), (4, 4, 7.62), (4, 5, 8.54),
(4, 6, 9.00), (4, 7, 8.77), (4, 8, 9.12), (4, 9, 7.99), (4, 10, 8.14),
(4, 11, 9.55), (4, 12, 7.72), (4, 13, 8.63), (4, 14, 9.30), (4, 15, 7.45),
(4, 16, 8.99), (4, 17, 7.88), (4, 18, 9.42), (4, 19, 8.67), (4, 20, 9.95),
(4, 21, 9.31), (4, 22, 7.84), (4, 23, 8.43), (4, 24, 9.12), (4, 25, 8.97),
(4, 26, 9.08), (4, 27, 8.65), (4, 28, 9.33), (4, 29, 7.44), (4, 30, 9.70),

-- **Química (course_id 5)**

(5, 1, 8.60), (5, 2, 9.15), (5, 3, 7.95), (5, 4, 9.22), (5, 5, 6.33),
(5, 6, 9.25), (5, 7, 8.44), (5, 8, 9.15), (5, 9, 7.94), (5, 10, 8.89),
(5, 11, 9.33), (5, 12, 7.55), (5, 13, 8.44), (5, 14, 9.06), (5, 15, 7.74),
(5, 16, 8.45), (5, 17, 9.69), (5, 18, 8.23), (5, 19, 9.34), (5, 20, 7.55),
(5, 21, 8.99), (5, 22, 9.71), (5, 23, 8.65), (5, 24, 7.89), (5, 25, 9.10),
(5, 26, 9.58), (5, 27, 7.74), (5, 28, 8.34), (5, 29, 9.13), (5, 30, 8.66);


  

