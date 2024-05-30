# Creating and Manipulating a Database
![Dark Purple Technical Roadmap Brainstorm(6)](https://github-production-user-asset-6210df.s3.amazonaws.com/132176058/239705696-658cf34a-e3ca-4ed4-86ba-8db62b39e989.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAVCODYLSA53PQK4ZA%2F20240530%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20240530T200837Z&X-Amz-Expires=300&X-Amz-Signature=d7cd31bc2bd33d782096855aafad011043a823e93581e1b92e966af64f05c670&X-Amz-SignedHeaders=host&actor_id=40529647&key_id=0&repo_id=643298404)

## Introduction
The purpose of these scenarios are to assess my proficiency in using SQL by building a simple database and query it to extract information from it. I will create tables and relationships among them, in addition to the necessary keys and indexes. Then, the next step will be to populate the database with suitable data. When my database is ready, I will write SQL queries to retrieve information. 

Note: This assignment was created with MySQL in mind. Therefore, dates, numbers, etc. have been set up with that tool in mind. 
Upon completion of this project, we will have created:

    -Write SQL queries to create tables
    -Write SQL queries to create relationships among tables
    -Identify indexes and create them in a database
    -Write queries to extract important information from a database 

## Objective 

This project evaluates my understanding of SQL syntax, query construction, and data retrieval techniques by simulating a scenario.

These scenarios serve as a practical demonstration of my SQL skills, showcasing my ability to write SQL queries to create tables, write SQL queries to create relationships among tables, identify indexes and create them in a database, and write queries to extract important information from a database . It showcases my competence in utilizing SQL as a versatile tool for querying and analyzing data, enabling me to extract valuable insights and draw informed conclusions.

## Prompt
We will build a database for a public library. This database is aimed to collect and analyze information about the clients' reading interests. The project concentrates only on books and the clients' interests in books. The analyses that will result from this project will be used by the library's management to decide on the future purchasing policy. 

A. Write the SQL statements in order to create the tables for the database. Use the Entity Relationship Diagram (ERD) of the database shown in Figure 1. For simplicity, we are assuming in this project that a book cannot be written by more than one author. You need to create the tables as well as the required constraints, including the keys (primary and foreign), and the relationships between tables. 

![sqlA](https://github.com/JosephBrides/Creating-Manipulating-a-Database/assets/40529647/cece2ef8-d80b-4a65-9f96-86aebabcc24b)

B. Populate your database with the sample set of data given to you in the tables below the assignment prompts.

C. Write the following queries to retrieve the information detailed below. As you work on these queries, create indexes that will increase your queries' performance.
   
    -Display all contents of the Clients table
    -First names, last names, ages and occupations of all clients
    -First and last names of clients that borrowed books in March 2018
    -First and last names of the top 5 authors clients borrowed in 2017
    -Nationalities of the least 5 authors that clients borrowed during the years 2015-2017
    -The book that was most borrowed during the years 2015-2017
    -Top borrowed genres for client born in years 1970-1980
    -Top 5 occupations that borrowed the most in 2016
    -Average number of borrowed books by job title
    -Create a VIEW and display the titles that were borrowed by at least 20% of clients
    -The top month of borrows in 2017
    -Average number of borrows by age
    -The oldest and the youngest clients of the library
    -First and last names of authors that wrote books in more than one genre 

## Author Table:

![Author Table](https://github.com/JosephBrides/Creating-Manipulating-a-Database/assets/40529647/13bb3458-4b5a-45b1-9ae5-5f790f987160)

## Book Table:

![Book Table](https://github.com/JosephBrides/Creating-Manipulating-a-Database/assets/40529647/be17592d-c4b5-4b45-8a64-27efef3e20b9)

## Client table:

![Client Table](https://github.com/JosephBrides/Creating-Manipulating-a-Database/assets/40529647/5640fde9-c554-454f-8e94-c01ba7f07010)

## Borrower table 

![Borrower table](https://github.com/JosephBrides/Creating-Manipulating-a-Database/assets/40529647/0a937184-df11-4fdc-8873-beba642b4a0d)


## Part A: Creating tables

First, I will write the SQL statements creating tables for the database using the ERD diagram portrayed in the prompt. This will include the required primary and foreign key restraints and relationships between tables. The CREATE tables wll look like this:

    CREATE TABLE Author (
        AuthorID INT PRIMARY KEY,
        AuthorFirstName VARCHAR(255),
        AuthorLastName VARCHAR(255),
        AuthorNationality VARCHAR(255)
    );

    CREATE TABLE Book (
        BookID INT PRIMARY KEY,
        BookTitle VARCHAR(255),
        Genre VARCHAR(255),
        AuthorID INT,
        FOREIGN KEY (AuthorID) REFERENCES Author(AuthorID)
    );

    CREATE TABLE Client (
        ClientID INT PRIMARY KEY,
        ClientFirstName VARCHAR(255),
        ClientLastName VARCHAR(255),
        ClientDOB YEAR,
        Occupation VARCHAR(255)
    );

    CREATE TABLE Borrower (
       BorrowID INT PRIMARY KEY,
       ClientID INT,
       BookID INT,
       BorrowDate DATE,
       FOREIGN KEY (ClientID) REFERENCES Client(ClientID),
       FOREIGN KEY (BookID) REFERENCES Book(BookID)
    );


## Part B: Populate

Here I will continue populating the database with the data given in the tables. Here are the results for each table.

Author Table: 
        
        
        INSERT INTO Author (AuthorID, AuthorFirstName, AuthorLastName, AuthorNationality)
        VALUES 
        (1, 'Sofia', 'Smith', 'Canada'),
        (2, 'Maria', 'Brown', 'Brazil'),
        (3, 'Elena', 'Martin', 'Mexico'),
        (4, 'Zoe', 'Roy', 'France'),
        (5, 'Sebastian', 'Lavoie', 'Canada'),
        (6, 'Dylan', 'Garcia', 'Spain'),
        (7, 'lan', 'Cruz', 'Mexico'),
        (8, 'Lucas', 'Smith', 'USA'),
        (9, 'Fabian', 'Wilson', 'USA'),
        (10, 'Liom', 'Taylor', 'Canada'),
        (11, 'William', 'Thomas', 'Great Britain'),
        (12, 'Logan', 'Moore', 'Canada'),
        (13, 'Oliver', 'Martin', 'France'),
        (14, 'Alysha', 'Thompson', 'Canada'),
        (15, 'Isabelle', 'Lee', 'Canada'),
        (16, 'Emily', 'Clark', 'USA'),
        (17, 'John', 'Young', 'China'),
        (18, 'David', 'Wright', 'Canada'),
        (19, 'Thomas', 'Scott', 'Canada'),
        (20, 'Helena', 'Adams', 'Canada'),
        (21, 'Sofia', 'Carter', 'USA'),
        (22, 'Liam', 'Parker', 'Canada'),
        (23, 'Emily', 'Murphy', 'USA');


Book Table:


                INSERT INTO Book (BookID, BookTitle, AuthorID, Genre)
        VALUES 
        (1, 'Build your database system', 1, 'Science'),
        (2, 'The red wall', 2, 'Fiction'),
        (3, 'The perfect match', 3, 'Fiction'),
        (4, 'Digital Logic', 4, 'Science'),
        (5, 'How to be a great lawyer', 5, 'Law'),
        (6, 'Manage successful negotiations', 6, 'Society'),
        (7, 'Pollution today', 7, 'Science'),
        (8, 'A gray park', 2, 'Fiction'),
        (9, 'How to be rich in one year', 8, 'Humor'),
        (10, 'Their bright fate', 9, 'Fiction'),
        (11, 'Black lines.', 10, 'Fiction'),
        (12, 'History of theater', 11, 'Literature'),
        (13, 'Electrical transformers.', 12, 'Science'),
        (14, 'Build your big data system.', 1, 'Science'),
        (15, 'Right and left', 13, 'Children'),
        (16, 'Programming using Python', 1, 'Science'),
        (17, 'Computer networks', 14, 'Science'),
        (18, 'Performance evaluation', 15, 'Science'),
        (19, 'Daily exercise', 16, 'Well being.'),
        (20, 'The silver uniform', 17, 'Fiction'),
        (21, 'Industrial revolution', 18, 'History'),
        (22, 'Green nature', 19, 'Well being.'),
        (23, 'Perfect football', 20, 'Well being'),
        (24, 'The chocolate love', 21, 'Humor'),
        (25, 'Director and leader', 22, 'Society'),
        (26, 'Play football every week', 20, 'well being'),
        (27, 'Maya the bee', 13, 'Children'),
        (28, 'Perfect rugby', 20, 'Well being'),
        (29, 'The end', 23, 'Fiction'),
        (30, 'Computer security', 1, 'Science'),
        (31, 'Participate', 22, 'Society'),
        (32, 'Positive figures', 3, 'Fiction');



Borrower Table:


            INSERT INTO Borrower (BorrowID, ClientID, BookID, BorrowDate)
        VALUES 
        (1, 35, 17, '2016-07-20'),
        (2, 1, 3, '2017-04-19'),
        (3, 42, 8, '2016-10-03'),
        (4, 62, 16, '2016-04-05'),
        (5, 53, 13, '2017-01-17'),
        (6, 33, 15, '2015-11-26'),
        (7, 40, 14, '2015-01-21'),
        (8, 64, 2, '2017-09-10'),
        (9, 56, 30, '2017-08-02'),
        (10, 23, 2, '2018-06-28'),
        (11, 46, 19, '2015-11-18'),
        (12, 61, 20, '2015-11-24'),
        (13, 58, 7, '2017-08-17'),
        (14, 46, 16, '2017-02-12'),
        (15, 80, 21, '2018-03-18'),
        (16, 51, 23, '2015-09-01'),
        (17, 49, 18, '2015-07-28'),
        (18, 43, 18, '2015-11-04'),
        (19, 30, 2, '2018-08-10'),
        (20, 48, 24, '2015-05-13'),
        (21, 71, 1, '2016-09-05'),
        (22, 35, 3, '2016-07-03'),
        (23, 57, 1, '2015-03-17'),
        (24, 23, 25, '2017-08-16'),
        (25, 20, 12, '2018-07-24'),
        (26, 25, 7, '2015-01-31'),
        (27, 72, 29, '2016-04-10'),
        (28, 74, 20, '2017-07-31'),
        (29, 53, 14, '2016-02-20'),
        (30, 32, 10, '2017-07-24'),
        (31, 12, 15, '2018-04-25'),
        (32, 77, 13, '2017-06-09'),
        (33, 30, 4, '2017-10-24'),
        (34, 37, 24, '2016-01-14'),
        (35, 27, 26, '2017-06-05'),
        (36, 1, 16, '2018-05-06'),
        (37, 21, 9, '2016-03-19'),
        (38, 69, 28, '2017-03-29'),
        (39, 17, 19, '2017-03-14'),
        (40, 8, 9, '2016-04-22'),
        (41, 63, 18, '2015-01-25'),
        (42, 65, 20, '2016-10-10'),
        (43, 51, 19, '2015-07-28'),
        (44, 23, 12, '2017-01-25'),
        (45, 17, 4, '2017-04-18'),
        (46, 68, 5, '2016-09-06'),
        (47, 46, 13, '2017-09-30'),
        (48, 15, 13, '2017-07-05'),
        (49, 11, 19, '2017-12-14'),
        (50, 78, 15, '2017-01-26'),
        (51, 47, 9, '2015-03-03'),
        (52, 68, 1, '2016-05-26'),
        (53, 37, 26, '2017-02-06'),
        (54, 48, 27, '2015-12-30'),
        (55, 9, 21, '2017-10-21'),
        (56, 29, 8, '2018-04-01'),
        (57, 64, 18, '2017-08-29'),
        (58, 61, 26, '2018-02-21'),
        (59, 39, 28, '2016-07-26'),
        (60, 73, 18, '2018-08-22'),
        (61, 11, 13, '2018-01-17'),
        (62, 45, 6, '2016-07-20'),
        (63, 33, 13, '2018-03-18'),
        (64, 10, 17, '2016-06-08'),
        (65, 28, 18, '2017-02-17'),
        (66, 51, 3, '2016-12-09'),
        (67, 29, 2, '2015-09-18'),
        (68, 28, 30, '2017-09-14'),
        (69, 74, 20, '2015-12-12'),
        (70, 15, 22, '2015-01-14'),
        (71, 57, 8, '2017-08-20'),
        (72, 2, 5, '2015-01-18'),
        (73, 74, 12, '2018-04-14'),
        (74, 51, 10, '2016-02-25'),
        (75, 25, 17, '2015-02-24'),
        (76, 45, 21, '2017-02-10'),
        (77, 27, 25, '2016-08-03'),
        (78, 32, 28, '2016-06-15'),
        (79, 71, 21, '2017-05-21'),
        (80, 75, 26, '2016-05-03'),
        (81, 56, 32, '2015-12-23'),
        (82, 26, 32, '2015-05-16'),
        (83, 66, 32, '2015-05-30'),
        (84, 57, 18, '2017-09-15'),
        (85, 40, 15, '2016-09-02'),
        (86, 65, 4, '2017-08-17'),
        (87, 54, 7, '2015-12-19'),
        (88, 29, 4, '2017-07-22'),
        (89, 44, 9, '2017-12-31'),
        (90, 56, 31, '2015-06-13'),
        (91, 17, 4, '2015-04-01'),
        (92, 35, 16, '2018-07-19'),
        (93, 22, 18, '2017-06-22'),
        (94, 39, 24, '2015-05-29'),
        (95, 63, 14, '2018-01-20'),
        (96, 53, 21, '2016-07-31'),
        (97, 40, 9, '2016-07-10'),
        (98, 52, 4, '2017-04-05'),
        (99, 27, 20, '2016-09-04'),
        (100, 72, 29, '2015-12-06'),
        (101, 49, 16, '2017-12-19'),
        (102, 6, 12, '2016-12-04'),
        (103, 74, 31, '2016-07-27'),
        (104, 48, 32, '2016-06-29'),
        (105, 69, 2, '2016-12-27'),
        (106, 60, 32, '2017-10-29'),
        (107, 45, 22, '2017-06-12'),
        (108, 42, 15, '2017-05-14'),
        (109, 79, 8, '2016-10-13'),
        (110, 70, 18, '2016-12-04'),
        (111, 34, 8, '2016-03-06'),
        (112, 43, 1, '2015-05-14'),
        (113, 42, 32, '2016-04-20'),
        (114, 67, 5, '2017-03-06'),
        (115, 80, 25, '2015-06-23'),
        (116, 54, 11, '2017-05-03'),
        (117, 34, 28, '2017-08-30'),
        (118, 65, 20, '2017-08-26'),
        (119, 61, 19, '2018-01-05'),
        (120, 38, 12, '2018-01-17'),
        (121, 51, 4, '2016-05-13'),
        (122, 7, 16, '2016-03-17'),
        (123, 46, 16, '2016-11-25'),
        (124, 75, 30, '2018-08-12'),
        (125, 72, 32, '2015-03-12'),
        (126, 44, 17, '2015-06-15'),
        (127, 68, 15, '2016-02-21'),
        (128, 21, 1, '2016-06-19'),
        (129, 14, 25, '2016-10-10'),
        (130, 68, 21, '2016-05-27'),
        (131, 35, 20, '2015-03-19'),
        (132, 16, 27, '2016-08-08'),
        (133, 79, 8, '2016-10-13'),
        (134, 14, 17, '2018-04-28'),
        (135, 29, 28, '2018-03-11'),
        (136, 41, 4, '2018-08-08'),
        (137, 42, 3, '2016-02-23'),
        (138, 45, 3, '2017-07-10'),
        (139, 36, 16, '2018-07-19'),
        (140, 36, 30, '2015-08-07'),
        (141, 54, 32, '2018-03-14'),
        (142, 61, 15, '2017-03-28'),
        (143, 1, 13, '2018-05-17'),
        (144, 43, 1, '2015-05-14'),
        (145, 37, 14, '2015-07-30'),
        (146, 62, 17, '2015-09-19'),
        (147, 50, 22, '2016-12-02'),
        (148, 45, 1, '2016-07-24'),
        (149, 32, 17, '2018-03-10'),
        (150, 13, 28, '2016-02-14'),
        (151, 15, 9, '2018-08-11'),
        (152, 10, 19, '2018-08-29'),
        (153, 66, 3, '2016-11-27'),
        (154, 68, 29, '2017-07-12'),
        (155, 21, 14, '2018-06-27'),
        (156, 35, 9, '2016-01-22'),
        (157, 17, 24, '2016-08-25'),
        (158, 40, 21, '2015-07-09'),
        (159, 1, 24, '2016-03-28'),
        (160, 70, 27, '2015-07-10'),
        (161, 80, 26, '2016-04-24'),
        (162, 29, 5, '2015-10-18'),
        (163, 76, 12, '2018-04-25'),
        (164, 22, 4, '2016-12-24'),
        (165, 2, 2, '2017-10-26'),
        (166, 35, 13, '2016-02-28'),
        (167, 40, 8, '2017-10-02'),
        (168, 68, 9, '2016-01-03'),
        (169, 32, 5, '2016-11-13'),
        (170, 34, 17, '2016-09-15'),
        (171, 34, 16, '2018-04-13'),
        (172, 80, 30, '2016-10-13'),
        (173, 20, 32, '2015-11-17'),
        (174, 36, 10, '2017-09-01'),
        (175, 78, 12, '2018-06-27'),
        (176, 57, 8, '2016-03-22'),
        (177, 75, 11, '2017-06-27'),
        (178, 71, 10, '2015-08-01'),
        (179, 48, 22, '2015-09-29'),
        (180, 19, 16, '2016-02-21'),
        (181, 79, 30, '2018-08-20'),
        (182, 70, 13, '2016-09-16'),
        (183, 30, 6, '2017-02-10'),
        (184, 45, 12, '2017-10-12'),
        (185, 30, 27, '2016-11-23'),
        (186, 26, 3, '2016-08-13'),
        (187, 66, 6, '2017-01-14'),
        (188, 47, 15, '2016-02-10'),
        (189, 53, 30, '2018-08-08'),
        (190, 80, 16, '2016-03-31'),
        (191, 70, 13, '2018-02-03'),
        (192, 14, 25, '2016-03-27'),
        (193, 46, 22, '2016-01-13'),
        (194, 30, 32, '2015-08-06'),
        (195, 60, 14, '2016-11-27'),
        (196, 14, 13, '2018-05-23'),
        (197, 71, 15, '2016-06-22'),
        (198, 38, 21, '2015-12-27'),
        (199, 69, 30, '2017-04-29'),
        (200, 49, 31, '2018-06-03'),
        (201, 28, 28, '2015-05-29'),
        (202, 49, 3, '2016-08-30'),
        (203, 75, 1, '2015-10-29'),
        (204, 78, 3, '2017-05-12'),
        (205, 43, 18, '2015-03-25'),
        (206, 27, 21, '2016-02-22'),
        (207, 64, 22, '2015-04-03'),
        (208, 21, 11, '2017-12-09'),
        (209, 66, 29, '2016-12-20'),
        (210, 45, 13, '2017-04-15'),
        (211, 48, 30, '2015-01-31'),
        (212, 20, 25, '2017-12-20'),
        (213, 41, 20, '2018-01-29'),
        (214, 51, 12, '2015-07-05'),
        (215, 5, 1, '2015-04-12'),
        (216, 40, 3, '2018-02-24'),
        (217, 79, 4, '2018-06-27'),
        (218, 15, 10, '2016-11-01'),
        (219, 42, 22, '2016-12-28'),
        (220, 17, 9, '2018-01-29'),
        (221, 38, 13, '2016-05-09'),
        (222, 79, 2, '2017-12-06'),
        (223, 74, 3, '2015-12-07'),
        (224, 46, 8, '2016-06-05'),
        (225, 78, 22, '2018-08-11'),
        (226, 45, 2, '2015-04-20'),
        (227, 72, 31, '2015-11-11'),
        (228, 18, 17, '2015-03-21'),
        (229, 29, 3, '2017-08-13'),
        (230, 66, 11, '2018-06-05'),
        (231, 38, 16, '2016-04-28'),
        (232, 26, 2, '2016-10-23'),
        (233, 32, 1, '2017-10-31'),
        (234, 62, 14, '2017-07-25'),
        (235, 12, 4, '2015-07-08'),
        (236, 38, 32, '2015-02-24'),
        (237, 29, 16, '2016-07-28'),
        (238, 36, 25, '2017-05-07'),
        (239, 76, 7, '2015-06-13'),
        (240, 28, 16, '2016-08-15'),
        (241, 60, 13, '2016-08-26'),
        (242, 8, 3, '2017-07-28'),
        (243, 25, 1, '2016-07-30'),
        (244, 62, 29, '2018-08-24'),
        (245, 51, 8, '2016-09-01'),
        (246, 27, 23, '2015-02-08'),
        (247, 69, 12, '2018-06-25'),
        (248, 51, 12, '2015-07-04'),
        (249, 7, 4, '2015-05-01'),
        (250, 31, 15, '2017-10-29'),
        (251, 14, 23, '2015-01-15'),
        (252, 14, 1, '2018-05-21'),
        (253, 39, 25, '2015-12-26'),
        (254, 79, 24, '2016-05-31'),
        (255, 40, 15, '2016-03-18'),
        (256, 51, 13, '2018-04-13'),
        (257, 61, 1, '2015-02-11'),
        (258, 15, 24, '2018-03-02'),
        (259, 10, 22, '2018-01-21'),
        (260, 67, 10, '2017-07-08'),
        (261, 79, 1, '2016-12-11'),
        (262, 19, 32, '2016-05-04'),
        (263, 35, 11, '2017-08-01'),
        (264, 27, 13, '2017-12-15'),
        (265, 30, 22, '2015-12-22'),
        (266, 1, 1, '2015-06-26'),
        (267, 70, 9, '2016-03-20'),
        (268, 56, 18, '2016-01-29'),
        (269, 13, 19, '2015-03-06'),
        (270, 61, 2, '2016-06-18'),
        (271, 47, 13, '2017-09-18'),
        (272, 30, 22, '2016-02-19'),
        (273, 18, 22, '2016-12-31'),
        (274, 34, 29, '2017-10-27'),
        (275, 32, 21, '2015-06-03'),
        (276, 9, 28, '2016-03-30'),
        (277, 62, 24, '2015-03-23'),
        (278, 44, 22, '2017-04-29'),
        (279, 27, 5, '2015-03-25'),
        (280, 61, 28, '2017-07-14'),
        (281, 5, 13, '2016-12-04'),
        (282, 43, 19, '2018-03-15'),
        (283, 34, 19, '2016-06-05'),
        (284, 35, 5, '2018-02-19'),
        (285, 13, 12, '2016-09-23'),
        (286, 74, 18, '2016-12-26'),
        (287, 70, 31, '2017-08-15'),
        (288, 42, 17, '2016-06-15'),
        (289, 51, 24, '2018-07-30'),
        (290, 45, 30, '2015-01-15'),
        (291, 70, 17, '2017-10-07'),
        (292, 77, 7, '2017-01-06'),
        (293, 74, 25, '2015-09-25'),
        (294, 47, 14, '2018-02-01'),
        (295, 10, 2, '2017-04-18'),
        (296, 16, 21, '2016-10-03'),
        (297, 48, 5, '2016-09-17'),
        (298, 72, 3, '2017-02-10'),
        (299, 26, 23, '2016-03-01'),
        (300, 49, 23, '2016-10-25');



Client Table: 

        
        INSERT INTO Client (ClientID, ClientFirstName, ClientLastName, ClientDOB, Occupation)
        VALUES 
        (1, 'Kaiden', 'Hill', '2006', 'Student'),
        (2, 'Alina', 'Morton', '2010', 'Student'),
        (3, 'Fania', 'Brooks', '1983', 'Food Scientist'),
        (4, 'Courtney', 'Jensen', '2006', 'Student'),
        (5, 'Brittany', 'Hill', '1983', 'Firefighter'),
        (6, 'Max', 'Rogers', '2005', 'Student'),
        (7, 'Margaret', 'McCarthy', '1981', 'School Psychologist'),
        (8, 'Julie', 'McCarthy', '1973', 'Professor'),
        (9, 'Ken', 'McCarthy', '1974', 'Securities Clerk'),
        (10, 'Britany', 'O Quinn', '1984', 'Violinist'),
        (11, 'Conner', 'Gardner', '1998', 'Licensed Massage Therapist'),
        (12, 'Mya', 'Austin', '1960', 'Parquet Floor Layer'),
        (13, 'Thierry', 'Rogers', '2004', 'Student'),
        (14, 'Eloise', 'Rogers', '1984', 'Computer Security Manager'),
        (15, 'Gerard', 'Jackson', '1979', 'Oil Exploration Engineer'),
        (16, 'Randy', 'Day', '1986', 'Aircraft Electrician'),
        (17, 'Jodie', 'Page', '1990', 'Manufacturing Director'),
        (18, 'Coral', 'Rice', '1996', 'Window Washer'),
        (19, 'Ayman', 'Austin', '2002', 'Student'),
        (20, 'Jaxson', 'Austin', '1999', 'Repair Worker'),
        (21, 'Joel', 'Austin', '1973', 'Police Officer'),
        (22, 'Alina', 'Austin', '2010', 'Student'),
        (23, 'Elin', 'Austin', '1962', 'Payroll Clerk'),
        (24, 'Ophelia', 'Wolf', '2004', 'Student'),
        (25, 'Eliot', 'McGuire', '1967', 'Dentist'),
        (26, 'Peter', 'McKinney', '1968', 'Professor'),
        (27, 'Annabella', 'Henry', '1974', 'Nurse'),
        (28, 'Anastasia', 'Baker', '2001', 'Student'),
        (29, 'Tyler', 'Baker', '1984', 'Police Officer'),
        (30, 'Lilian', 'Ross', '1983', 'Insurance Agent'),
        (31, 'Thierry', 'Arnold', '1975', 'Bus Driver'),
        (32, 'Angelina', 'Rowe', '1979', 'Firefighter'),
        (33, 'Marcia', 'Rowe', '1974', 'Health Educator'),
        (34, 'Martin', 'Rowe', '1976', 'Ship Engineer'),
        (35, 'Adeline', 'Rowe', '2005', 'Student'),
        (36, 'Colette', 'Rowe', '1963', 'Professor'),
        (37, 'Diane', 'Clark', '1975', 'Payroll Clerk'),
        (38, 'Caroline', 'Clark', '1960', 'Dentist'),
        (39, 'Dalton', 'Clayton', '1982', 'Police Officer'),
        (40, 'Steve', 'Clayton', '1990', 'Bus Driver'),
        (41, 'Melanie', 'Clayton', '1987', 'Computer Engineer'),
        (42, 'Alana', 'Wilson', '2007', 'Student'),
        (43, 'Carson', 'Byrne', '1995', 'Food Scientist'),
        (44, 'Conrad', 'Byrne', '2007', 'Student'),
        (45, 'Ryan', 'Porter', '2008', 'Student'),
        (46, 'Elin', 'Porter', '1978', 'Computer Programmer'),
        (47, 'Tyler', 'Harvey', '2007', 'Student'),
        (48, 'Arya', 'Harvey', '2008', 'Student'),
        (49, 'Serena', 'Harvey', '1978', 'School Teacher'),
        (50, 'Lilly', 'Franklin', '1976', 'Doctor'),
        (51, 'Mai', 'Franklin', '1994', 'Dentist'),
        (52, 'John', 'Franklin', '1999', 'Firefighter'),
        (53, 'Judy', 'Franklin', '1995', 'Firefighter'),
        (54, 'Katy', 'Lloyd', '1992', 'School Teacher'),
        (55, 'Tamara', 'Allen', '1963', 'Ship Engineer'),
        (56, 'Maxim', 'Lyons', '1985', 'Police Officer'),
        (57, 'Allan', 'Lyons', '1983', 'Computer Engineer'),
        (58, 'Marc', 'Harris', '1980', 'School Teacher'),
        (59, 'Elin', 'Young', '2009', 'Student'),
        (60, 'Diana', 'Young', '2008', 'Student'),
        (61, 'Diane', 'Young', '2006', 'Student'),
        (62, 'Alana', 'Bird', '2003', 'Student'),
        (63, 'Anna', 'Becker', '1979', 'Security Agent'),
        (64, 'Katie', 'Grant', '1977', 'Manager'),
        (65, 'Joan', 'Grant', '2010', 'Student'),
        (66, 'Bryan', 'Bell', '2001', 'Student'),
        (67, 'Belle', 'Miller', '1970', 'Professor'),
        (68, 'Peggy', 'Stevens', '1990', 'Bus Driver'),
        (69, 'Steve', 'Williamson', '1975', 'HR Clerk'),
        (70, 'Tyler', 'Williamson', '1999', 'Doctor'),
        (71, 'Izabelle', 'Williamson', '1990', 'Systems Analyst'),
        (72, 'Annabel', 'Williamson', '1960', 'Cashier'),
        (73, 'Mohamed', 'Waters', '1966', 'Insurance Agent'),
        (74, 'Marion', 'Newman', '1970', 'Computer Programmer'),
        (75, 'Ada', 'Williams', '1986', 'Computer Programmer'),
        (76, 'Sean', 'Scott', '1983', 'Bus Driver'),
        (77, 'Farrah', 'Scott', '1974', 'Ship Engineer'),
        (78, 'Christine', 'Lambert', '1973', 'School Teacher'),
        (79, 'Alysha', 'Lambert', '2007', 'Student'),
        (80, 'Maia', 'Grant', '1984', 'School Teacher');


The Libraries Database results:


            CREATE DATABASE  IF NOT EXISTS `library` /*!40100 DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_0900_ai_ci */ /*!80016 DEFAULT ENCRYPTION='N' */;
        USE `library`;
        -- MySQL dump 10.13  Distrib 8.0.34, for Win64 (x86_64)
        --
        -- Host: localhost    Database: library
        -- ------------------------------------------------------
        -- Server version	8.1.0
        
        /*!40101 SET @OLD_CHARACTER_SET_CLIENT=@@CHARACTER_SET_CLIENT */;
        /*!40101 SET @OLD_CHARACTER_SET_RESULTS=@@CHARACTER_SET_RESULTS */;
        /*!40101 SET @OLD_COLLATION_CONNECTION=@@COLLATION_CONNECTION */;
        /*!50503 SET NAMES utf8 */;
        /*!40103 SET @OLD_TIME_ZONE=@@TIME_ZONE */;
        /*!40103 SET TIME_ZONE='+00:00' */;
        /*!40014 SET @OLD_UNIQUE_CHECKS=@@UNIQUE_CHECKS, UNIQUE_CHECKS=0 */;
        /*!40014 SET @OLD_FOREIGN_KEY_CHECKS=@@FOREIGN_KEY_CHECKS, FOREIGN_KEY_CHECKS=0 */;
        /*!40101 SET @OLD_SQL_MODE=@@SQL_MODE, SQL_MODE='NO_AUTO_VALUE_ON_ZERO' */;
        /*!40111 SET @OLD_SQL_NOTES=@@SQL_NOTES, SQL_NOTES=0 */;
        
        --
        -- Table structure for table `author`
        --
        
        DROP TABLE IF EXISTS `author`;
        /*!40101 SET @saved_cs_client     = @@character_set_client */;
        /*!50503 SET character_set_client = utf8mb4 */;
        CREATE TABLE `author` (
          `AuthorID` int NOT NULL,
          `AuthorFirstName` varchar(255) DEFAULT NULL,
          `AuthorLastName` varchar(255) DEFAULT NULL,
          `AuthorNationality` varchar(255) DEFAULT NULL,
          PRIMARY KEY (`AuthorID`)
        ) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
        /*!40101 SET character_set_client = @saved_cs_client */;
        
        --
        -- Dumping data for table `author`
        --
        
        LOCK TABLES `author` WRITE;
        /*!40000 ALTER TABLE `author` DISABLE KEYS */;
        INSERT INTO `author` VALUES (1,'Sofia','Smith','Canada'),(2,'Maria','Brown','Brazil'),(3,'Elena','Martin','Mexico'),(4,'Zoe','Roy','France'),(5,'Sebastian','Lavoie','Canada'),(6,'Dylan','Garcia','Spain'),(7,'lan','Cruz','Mexico'),(8,'Lucas','Smith','USA'),(9,'Fabian','Wilson','USA'),(10,'Liom','Taylor','Canada'),(11,'William','Thomas','Great Britain'),(12,'Logan','Moore','Canada'),(13,'Oliver','Martin','France'),(14,'Alysha','Thompson','Canada'),(15,'Isabelle','Lee','Canada'),(16,'Emily','Clark','USA'),(17,'John','Young','China'),(18,'David','Wright','Canada'),(19,'Thomas','Scott','Canada'),(20,'Helena','Adams','Canada'),(21,'Sofia','Carter','USA'),(22,'Liam','Parker','Canada'),(23,'Emily','Murphy','USA');
        /*!40000 ALTER TABLE `author` ENABLE KEYS */;
        UNLOCK TABLES;
        
        --
        -- Table structure for table `book`
        --
        
        DROP TABLE IF EXISTS `book`;
        /*!40101 SET @saved_cs_client     = @@character_set_client */;
        /*!50503 SET character_set_client = utf8mb4 */;
        CREATE TABLE `book` (
          `BookID` int NOT NULL,
          `BookTitle` varchar(255) DEFAULT NULL,
          `Genre` varchar(255) DEFAULT NULL,
          `AuthorID` int DEFAULT NULL,
          PRIMARY KEY (`BookID`),
          KEY `AuthorID` (`AuthorID`),
          CONSTRAINT `book_ibfk_1` FOREIGN KEY (`AuthorID`) REFERENCES `author` (`AuthorID`)
        ) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
        /*!40101 SET character_set_client = @saved_cs_client */;
        
        --
        -- Dumping data for table `book`
        --
        
        LOCK TABLES `book` WRITE;
        /*!40000 ALTER TABLE `book` DISABLE KEYS */;
        INSERT INTO `book` VALUES (1,'Build your database system','Science',1),(2,'The red wall','Fiction',2),(3,'The perfect match','Fiction',3),(4,'Digital Logic','Science',4),(5,'How to be a great lawyer','Law',5),(6,'Manage successful negotiations','Society',6),(7,'Pollution today','Science',7),(8,'A gray park','Fiction',2),(9,'How to be rich in one year','Humor',8),(10,'Their bright fate','Fiction',9),(11,'Black lines.','Fiction',10),(12,'History of theater','Literature',11),(13,'Electrical transformers.','Science',12),(14,'Build your big data system.','Science',1),(15,'Right and left','Children',13),(16,'Programming using Python','Science',1),(17,'Computer networks','Science',14),(18,'Performance evaluation','Science',15),(19,'Daily exercise','Well being.',16),(20,'The silver uniform','Fiction',17),(21,'Industrial revolution','History',18),(22,'Green nature','Well being.',19),(23,'Perfect football','Well being',20),(24,'The chocolate love','Humor',21),(25,'Director and leader','Society',22),(26,'Play football every week','well being',20),(27,'Maya the bee','Children',13),(28,'Perfect rugby','Well being',20),(29,'The end','Fiction',23),(30,'Computer security','Science',1),(31,'Participate','Society',22),(32,'Positive figures','Fiction',3);
        /*!40000 ALTER TABLE `book` ENABLE KEYS */;
        UNLOCK TABLES;
        
        --
        -- Table structure for table `borrower`
        --
        
        DROP TABLE IF EXISTS `borrower`;
        /*!40101 SET @saved_cs_client     = @@character_set_client */;
        /*!50503 SET character_set_client = utf8mb4 */;
        CREATE TABLE `borrower` (
          `BorrowID` int NOT NULL,
          `ClientID` int DEFAULT NULL,
          `BookID` int DEFAULT NULL,
          `BorrowDate` date DEFAULT NULL,
          PRIMARY KEY (`BorrowID`),
          KEY `ClientID` (`ClientID`),
          KEY `BookID` (`BookID`),
          CONSTRAINT `borrower_ibfk_1` FOREIGN KEY (`ClientID`) REFERENCES `client` (`ClientID`),
          CONSTRAINT `borrower_ibfk_2` FOREIGN KEY (`BookID`) REFERENCES `book` (`BookID`)
        ) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
        /*!40101 SET character_set_client = @saved_cs_client */;
        
        --
        -- Dumping data for table `borrower`
        --
        
        LOCK TABLES `borrower` WRITE;
        /*!40000 ALTER TABLE `borrower` DISABLE KEYS */;
        INSERT INTO `borrower` VALUES (1,35,17,'2016-07-20'),(2,1,3,'2017-04-19'),(3,42,8,'2016-10-03'),(4,62,16,'2016-04-05'),(5,53,13,'2017-01-17'),(6,33,15,'2015-11-26'),(7,40,14,'2015-01-21'),(8,64,2,'2017-09-10'),(9,56,30,'2017-08-02'),(10,23,2,'2018-06-28'),(11,46,19,'2015-11-18'),(12,61,20,'2015-11-24'),(13,58,7,'2017-08-17'),(14,46,16,'2017-02-12'),(15,80,21,'2018-03-18'),(16,51,23,'2015-09-01'),(17,49,18,'2015-07-28'),(18,43,18,'2015-11-04'),(19,30,2,'2018-08-10'),(20,48,24,'2015-05-13'),(21,71,1,'2016-09-05'),(22,35,3,'2016-07-03'),(23,57,1,'2015-03-17'),(24,23,25,'2017-08-16'),(25,20,12,'2018-07-24'),(26,25,7,'2015-01-31'),(27,72,29,'2016-04-10'),(28,74,20,'2017-07-31'),(29,53,14,'2016-02-20'),(30,32,10,'2017-07-24'),(31,12,15,'2018-04-25'),(32,77,13,'2017-06-09'),(33,30,4,'2017-10-24'),(34,37,24,'2016-01-14'),(35,27,26,'2017-06-05'),(36,1,16,'2018-05-06'),(37,21,9,'2016-03-19'),(38,69,28,'2017-03-29'),(39,17,19,'2017-03-14'),(40,8,9,'2016-04-22'),(41,63,18,'2015-01-25'),(42,65,20,'2016-10-10'),(43,51,19,'2015-07-28'),(44,23,12,'2017-01-25'),(45,17,4,'2017-04-18'),(46,68,5,'2016-09-06'),(47,46,13,'2017-09-30'),(48,15,13,'2017-07-05'),(49,11,19,'2017-12-14'),(50,78,15,'2017-01-26'),(51,47,9,'2015-03-03'),(52,68,1,'2016-05-26'),(53,37,26,'2017-02-06'),(54,48,27,'2015-12-30'),(55,9,21,'2017-10-21'),(56,29,8,'2018-04-01'),(57,64,18,'2017-08-29'),(58,61,26,'2018-02-21'),(59,39,28,'2016-07-26'),(60,73,18,'2018-08-22'),(61,11,13,'2018-01-17'),(62,45,6,'2016-07-20'),(63,33,13,'2018-03-18'),(64,10,17,'2016-06-08'),(65,28,18,'2017-02-17'),(66,51,3,'2016-12-09'),(67,29,2,'2015-09-18'),(68,28,30,'2017-09-14'),(69,74,20,'2015-12-12'),(70,15,22,'2015-01-14'),(71,57,8,'2017-08-20'),(72,2,5,'2015-01-18'),(73,74,12,'2018-04-14'),(74,51,10,'2016-02-25'),(75,25,17,'2015-02-24'),(76,45,21,'2017-02-10'),(77,27,25,'2016-08-03'),(78,32,28,'2016-06-15'),(79,71,21,'2017-05-21'),(80,75,26,'2016-05-03'),(81,56,32,'2015-12-23'),(82,26,32,'2015-05-16'),(83,66,32,'2015-05-30'),(84,57,18,'2017-09-15'),(85,40,15,'2016-09-02'),(86,65,4,'2017-08-17'),(87,54,7,'2015-12-19'),(88,29,4,'2017-07-22'),(89,44,9,'2017-12-31'),(90,56,31,'2015-06-13'),(91,17,4,'2015-04-01'),(92,35,16,'2018-07-19'),(93,22,18,'2017-06-22'),(94,39,24,'2015-05-29'),(95,63,14,'2018-01-20'),(96,53,21,'2016-07-31'),(97,40,9,'2016-07-10'),(98,52,4,'2017-04-05'),(99,27,20,'2016-09-04'),(100,72,29,'2015-12-06'),(101,49,16,'2017-12-19'),(102,6,12,'2016-12-04'),(103,74,31,'2016-07-27'),(104,48,32,'2016-06-29'),(105,69,2,'2016-12-27'),(106,60,32,'2017-10-29'),(107,45,22,'2017-06-12'),(108,42,15,'2017-05-14'),(109,79,8,'2016-10-13'),(110,70,18,'2016-12-04'),(111,34,8,'2016-03-06'),(112,43,1,'2015-05-14'),(113,42,32,'2016-04-20'),(114,67,5,'2017-03-06'),(115,80,25,'2015-06-23'),(116,54,11,'2017-05-03'),(117,34,28,'2017-08-30'),(118,65,20,'2017-08-26'),(119,61,19,'2018-01-05'),(120,38,12,'2018-01-17'),(121,51,4,'2016-05-13'),(122,7,16,'2016-03-17'),(123,46,16,'2016-11-25'),(124,75,30,'2018-08-12'),(125,72,32,'2015-03-12'),(126,44,17,'2015-06-15'),(127,68,15,'2016-02-21'),(128,21,1,'2016-06-19'),(129,14,25,'2016-10-10'),(130,68,21,'2016-05-27'),(131,35,20,'2015-03-19'),(132,16,27,'2016-08-08'),(133,79,8,'2016-10-13'),(134,14,17,'2018-04-28'),(135,29,28,'2018-03-11'),(136,41,4,'2018-08-08'),(137,42,3,'2016-02-23'),(138,45,3,'2017-07-10'),(139,36,16,'2018-07-19'),(140,36,30,'2015-08-07'),(141,54,32,'2018-03-14'),(142,61,15,'2017-03-28'),(143,1,13,'2018-05-17'),(144,43,1,'2015-05-14'),(145,37,14,'2015-07-30'),(146,62,17,'2015-09-19'),(147,50,22,'2016-12-02'),(148,45,1,'2016-07-24'),(149,32,17,'2018-03-10'),(150,13,28,'2016-02-14'),(151,15,9,'2018-08-11'),(152,10,19,'2018-08-29'),(153,66,3,'2016-11-27'),(154,68,29,'2017-07-12'),(155,21,14,'2018-06-27'),(156,35,9,'2016-01-22'),(157,17,24,'2016-08-25'),(158,40,21,'2015-07-09'),(159,1,24,'2016-03-28'),(160,70,27,'2015-07-10'),(161,80,26,'2016-04-24'),(162,29,5,'2015-10-18'),(163,76,12,'2018-04-25'),(164,22,4,'2016-12-24'),(165,2,2,'2017-10-26'),(166,35,13,'2016-02-28'),(167,40,8,'2017-10-02'),(168,68,9,'2016-01-03'),(169,32,5,'2016-11-13'),(170,34,17,'2016-09-15'),(171,34,16,'2018-04-13'),(172,80,30,'2016-10-13'),(173,20,32,'2015-11-17'),(174,36,10,'2017-09-01'),(175,78,12,'2018-06-27'),(176,57,8,'2016-03-22'),(177,75,11,'2017-06-27'),(178,71,10,'2015-08-01'),(179,48,22,'2015-09-29'),(180,19,16,'2016-02-21'),(181,79,30,'2018-08-20'),(182,70,13,'2016-09-16'),(183,30,6,'2017-02-10'),(184,45,12,'2017-10-12'),(185,30,27,'2016-11-23'),(186,26,3,'2016-08-13'),(187,66,6,'2017-01-14'),(188,47,15,'2016-02-10'),(189,53,30,'2018-08-08'),(190,80,16,'2016-03-31'),(191,70,13,'2018-02-03'),(192,14,25,'2016-03-27'),(193,46,22,'2016-01-13'),(194,30,32,'2015-08-06'),(195,60,14,'2016-11-27'),(196,14,13,'2018-05-23'),(197,71,15,'2016-06-22'),(198,38,21,'2015-12-27'),(199,69,30,'2017-04-29'),(200,49,31,'2018-06-03'),(201,28,28,'2015-05-29'),(202,49,3,'2016-08-30'),(203,75,1,'2015-10-29'),(204,78,3,'2017-05-12'),(205,43,18,'2015-03-25'),(206,27,21,'2016-02-22'),(207,64,22,'2015-04-03'),(208,21,11,'2017-12-09'),(209,66,29,'2016-12-20'),(210,45,13,'2017-04-15'),(211,48,30,'2015-01-31'),(212,20,25,'2017-12-20'),(213,41,20,'2018-01-29'),(214,51,12,'2015-07-05'),(215,5,1,'2015-04-12'),(216,40,3,'2018-02-24'),(217,79,4,'2018-06-27'),(218,15,10,'2016-11-01'),(219,42,22,'2016-12-28'),(220,17,9,'2018-01-29'),(221,38,13,'2016-05-09'),(222,79,2,'2017-12-06'),(223,74,3,'2015-12-07'),(224,46,8,'2016-06-05'),(225,78,22,'2018-08-11'),(226,45,2,'2015-04-20'),(227,72,31,'2015-11-11'),(228,18,17,'2015-03-21'),(229,29,3,'2017-08-13'),(230,66,11,'2018-06-05'),(231,38,16,'2016-04-28'),(232,26,2,'2016-10-23'),(233,32,1,'2017-10-31'),(234,62,14,'2017-07-25'),(235,12,4,'2015-07-08'),(236,38,32,'2015-02-24'),(237,29,16,'2016-07-28'),(238,36,25,'2017-05-07'),(239,76,7,'2015-06-13'),(240,28,16,'2016-08-15'),(241,60,13,'2016-08-26'),(242,8,3,'2017-07-28'),(243,25,1,'2016-07-30'),(244,62,29,'2018-08-24'),(245,51,8,'2016-09-01'),(246,27,23,'2015-02-08'),(247,69,12,'2018-06-25'),(248,51,12,'2015-07-04'),(249,7,4,'2015-05-01'),(250,31,15,'2017-10-29'),(251,14,23,'2015-01-15'),(252,14,1,'2018-05-21'),(253,39,25,'2015-12-26'),(254,79,24,'2016-05-31'),(255,40,15,'2016-03-18'),(256,51,13,'2018-04-13'),(257,61,1,'2015-02-11'),(258,15,24,'2018-03-02'),(259,10,22,'2018-01-21'),(260,67,10,'2017-07-08'),(261,79,1,'2016-12-11'),(262,19,32,'2016-05-04'),(263,35,11,'2017-08-01'),(264,27,13,'2017-12-15'),(265,30,22,'2015-12-22'),(266,1,1,'2015-06-26'),(267,70,9,'2016-03-20'),(268,56,18,'2016-01-29'),(269,13,19,'2015-03-06'),(270,61,2,'2016-06-18'),(271,47,13,'2017-09-18'),(272,30,22,'2016-02-19'),(273,18,22,'2016-12-31'),(274,34,29,'2017-10-27'),(275,32,21,'2015-06-03'),(276,9,28,'2016-03-30'),(277,62,24,'2015-03-23'),(278,44,22,'2017-04-29'),(279,27,5,'2015-03-25'),(280,61,28,'2017-07-14'),(281,5,13,'2016-12-04'),(282,43,19,'2018-03-15'),(283,34,19,'2016-06-05'),(284,35,5,'2018-02-19'),(285,13,12,'2016-09-23'),(286,74,18,'2016-12-26'),(287,70,31,'2017-08-15'),(288,42,17,'2016-06-15'),(289,51,24,'2018-07-30'),(290,45,30,'2015-01-15'),(291,70,17,'2017-10-07'),(292,77,7,'2017-01-06'),(293,74,25,'2015-09-25'),(294,47,14,'2018-02-01'),(295,10,2,'2017-04-18'),(296,16,21,'2016-10-03'),(297,48,5,'2016-09-17'),(298,72,3,'2017-02-10'),(299,26,23,'2016-03-01'),(300,49,23,'2016-10-25');
        /*!40000 ALTER TABLE `borrower` ENABLE KEYS */;
        UNLOCK TABLES;
        
        --
        -- Table structure for table `client`
        --
        
        DROP TABLE IF EXISTS `client`;
        /*!40101 SET @saved_cs_client     = @@character_set_client */;
        /*!50503 SET character_set_client = utf8mb4 */;
        CREATE TABLE `client` (
          `ClientID` int NOT NULL,
          `ClientFirstName` varchar(255) DEFAULT NULL,
          `ClientLastName` varchar(255) DEFAULT NULL,
          `ClientDOB` year DEFAULT NULL,
          `Occupation` varchar(255) DEFAULT NULL,
          PRIMARY KEY (`ClientID`)
        ) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
        /*!40101 SET character_set_client = @saved_cs_client */;
        
        --
        -- Dumping data for table `client`
        --
        
        LOCK TABLES `client` WRITE;
        /*!40000 ALTER TABLE `client` DISABLE KEYS */;
        INSERT INTO `client` VALUES (1,'Kaiden','Hill',2006,'Student'),(2,'Alina','Morton',2010,'Student'),(3,'Fania','Brooks',1983,'Food Scientist'),(4,'Courtney','Jensen',2006,'Student'),(5,'Brittany','Hill',1983,'Firefighter'),(6,'Max','Rogers',2005,'Student'),(7,'Margaret','McCarthy',1981,'School Psychologist'),(8,'Julie','McCarthy',1973,'Professor'),(9,'Ken','McCarthy',1974,'Securities Clerk'),(10,'Britany','O Quinn',1984,'Violinist'),(11,'Conner','Gardner',1998,'Licensed Massage Therapist'),(12,'Mya','Austin',1960,'Parquet Floor Layer'),(13,'Thierry','Rogers',2004,'Student'),(14,'Eloise','Rogers',1984,'Computer Security Manager'),(15,'Gerard','Jackson',1979,'Oil Exploration Engineer'),(16,'Randy','Day',1986,'Aircraft Electrician'),(17,'Jodie','Page',1990,'Manufacturing Director'),(18,'Coral','Rice',1996,'Window Washer'),(19,'Ayman','Austin',2002,'Student'),(20,'Jaxson','Austin',1999,'Repair Worker'),(21,'Joel','Austin',1973,'Police Officer'),(22,'Alina','Austin',2010,'Student'),(23,'Elin','Austin',1962,'Payroll Clerk'),(24,'Ophelia','Wolf',2004,'Student'),(25,'Eliot','McGuire',1967,'Dentist'),(26,'Peter','McKinney',1968,'Professor'),(27,'Annabella','Henry',1974,'Nurse'),(28,'Anastasia','Baker',2001,'Student'),(29,'Tyler','Baker',1984,'Police Officer'),(30,'Lilian','Ross',1983,'Insurance Agent'),(31,'Thierry','Arnold',1975,'Bus Driver'),(32,'Angelina','Rowe',1979,'Firefighter'),(33,'Marcia','Rowe',1974,'Health Educator'),(34,'Martin','Rowe',1976,'Ship Engineer'),(35,'Adeline','Rowe',2005,'Student'),(36,'Colette','Rowe',1963,'Professor'),(37,'Diane','Clark',1975,'Payroll Clerk'),(38,'Caroline','Clark',1960,'Dentist'),(39,'Dalton','Clayton',1982,'Police Officer'),(40,'Steve','Clayton',1990,'Bus Driver'),(41,'Melanie','Clayton',1987,'Computer Engineer'),(42,'Alana','Wilson',2007,'Student'),(43,'Carson','Byrne',1995,'Food Scientist'),(44,'Conrad','Byrne',2007,'Student'),(45,'Ryan','Porter',2008,'Student'),(46,'Elin','Porter',1978,'Computer Programmer'),(47,'Tyler','Harvey',2007,'Student'),(48,'Arya','Harvey',2008,'Student'),(49,'Serena','Harvey',1978,'School Teacher'),(50,'Lilly','Franklin',1976,'Doctor'),(51,'Mai','Franklin',1994,'Dentist'),(52,'John','Franklin',1999,'Firefighter'),(53,'Judy','Franklin',1995,'Firefighter'),(54,'Katy','Lloyd',1992,'School Teacher'),(55,'Tamara','Allen',1963,'Ship Engineer'),(56,'Maxim','Lyons',1985,'Police Officer'),(57,'Allan','Lyons',1983,'Computer Engineer'),(58,'Marc','Harris',1980,'School Teacher'),(59,'Elin','Young',2009,'Student'),(60,'Diana','Young',2008,'Student'),(61,'Diane','Young',2006,'Student'),(62,'Alana','Bird',2003,'Student'),(63,'Anna','Becker',1979,'Security Agent'),(64,'Katie','Grant',1977,'Manager'),(65,'Joan','Grant',2010,'Student'),(66,'Bryan','Bell',2001,'Student'),(67,'Belle','Miller',1970,'Professor'),(68,'Peggy','Stevens',1990,'Bus Driver'),(69,'Steve','Williamson',1975,'HR Clerk'),(70,'Tyler','Williamson',1999,'Doctor'),(71,'Izabelle','Williamson',1990,'Systems Analyst'),(72,'Annabel','Williamson',1960,'Cashier'),(73,'Mohamed','Waters',1966,'Insurance Agent'),(74,'Marion','Newman',1970,'Computer Programmer'),(75,'Ada','Williams',1986,'Computer Programmer'),(76,'Sean','Scott',1983,'Bus Driver'),(77,'Farrah','Scott',1974,'Ship Engineer'),(78,'Christine','Lambert',1973,'School Teacher'),(79,'Alysha','Lambert',2007,'Student'),(80,'Maia','Grant',1984,'School Teacher');
        /*!40000 ALTER TABLE `client` ENABLE KEYS */;
        UNLOCK TABLES;
        
        --
        -- Temporary view structure for view `popularbooks`
        --
        
        DROP TABLE IF EXISTS `popularbooks`;
        /*!50001 DROP VIEW IF EXISTS `popularbooks`*/;
        SET @saved_cs_client     = @@character_set_client;
        /*!50503 SET character_set_client = utf8mb4 */;
        /*!50001 CREATE VIEW `popularbooks` AS SELECT 
         1 AS `BookTitle`*/;
        SET character_set_client = @saved_cs_client;
        
        --
        -- Final view structure for view `popularbooks`
        --
        
        /*!50001 DROP VIEW IF EXISTS `popularbooks`*/;
        /*!50001 SET @saved_cs_client          = @@character_set_client */;
        /*!50001 SET @saved_cs_results         = @@character_set_results */;
        /*!50001 SET @saved_col_connection     = @@collation_connection */;
        /*!50001 SET character_set_client      = utf8mb4 */;
        /*!50001 SET character_set_results     = utf8mb4 */;
        /*!50001 SET collation_connection      = utf8mb4_0900_ai_ci */;
        /*!50001 CREATE ALGORITHM=UNDEFINED */
        /*!50013 DEFINER=`root`@`localhost` SQL SECURITY DEFINER */
        /*!50001 VIEW `popularbooks` AS select `book`.`BookTitle` AS `BookTitle` from (`book` join `borrower` on((`book`.`BookID` = `borrower`.`BookID`))) group by `book`.`BookID` having (count(distinct `borrower`.`ClientID`) >= (0.2 * (select count(0) from `client`))) */;
        /*!50001 SET character_set_client      = @saved_cs_client */;
        /*!50001 SET character_set_results     = @saved_cs_results */;
        /*!50001 SET collation_connection      = @saved_col_connection */;
        /*!40103 SET TIME_ZONE=@OLD_TIME_ZONE */;
        
        /*!40101 SET SQL_MODE=@OLD_SQL_MODE */;
        /*!40014 SET FOREIGN_KEY_CHECKS=@OLD_FOREIGN_KEY_CHECKS */;
        /*!40014 SET UNIQUE_CHECKS=@OLD_UNIQUE_CHECKS */;
        /*!40101 SET CHARACTER_SET_CLIENT=@OLD_CHARACTER_SET_CLIENT */;
        /*!40101 SET CHARACTER_SET_RESULTS=@OLD_CHARACTER_SET_RESULTS */;
        /*!40101 SET COLLATION_CONNECTION=@OLD_COLLATION_CONNECTION */;
        /*!40111 SET SQL_NOTES=@OLD_SQL_NOTES */;
        
        -- Dump completed on 2024-02-07  0:12:34



    



## Part C: Writing Queries

Next, I will write the specific queries to get the information they are asking for.

        -- 1. Display all contents of the Clients table
        SELECT * FROM Client;

        -- 2. First names, last names, ages and occupations of all clients
        SELECT 
            ClientFirstName, 
            ClientLastName, 
            YEAR(CURDATE()) - CAST(ClientDOB AS UNSIGNED) AS Age, 
            Occupation 
        FROM 
            Client;

        -- 3. First and last names of clients that borrowed books in March 2018
        SELECT ClientFirstName, ClientLastName
        FROM Client
        JOIN Borrower ON Client.ClientID = Borrower.ClientID
        WHERE MONTH(BorrowDate) = 3 AND YEAR(BorrowDate) = 2018;

        -- 4. First and last names of the top 5 authors clients borrowed in 2017
        SELECT AuthorFirstName, AuthorLastName
        FROM Author
        JOIN Book ON Author.AuthorID = Book.AuthorID
        JOIN Borrower ON Book.BookID = Borrower.BookID
        WHERE YEAR(BorrowDate) = 2017
        GROUP BY Author.AuthorID
        ORDER BY COUNT(*) DESC
        LIMIT 5;

        -- 5. Nationalities of the least 5 authors that clients borrowed during years 2015–2017
        SELECT AuthorNationality
        FROM Author
        JOIN Book ON Author.AuthorID = Book.AuthorID
        JOIN Borrower ON Book.BookID = Borrower.BookID
        WHERE YEAR(BorrowDate) BETWEEN 2015 AND 2017
        GROUP BY Author.AuthorID
        ORDER BY COUNT(*) ASC
        LIMIT 5;

        -- 6. The book that was most borrowed during years 2015–2017
        SELECT BookTitle
        FROM Book
        JOIN Borrower ON Book.BookID = Borrower.BookID
        WHERE YEAR(BorrowDate) BETWEEN 2015 AND 2017
        GROUP BY Book.BookID
        ORDER BY COUNT(*) DESC
        LIMIT 1;

        -- 7. Top borrowed genres for client born in years 1970–1980
        SELECT Genre
        FROM Book
        JOIN Borrower ON Book.BookID = Borrower.BookID
        JOIN Client ON Borrower.ClientID = Client.ClientID
        WHERE YEAR(ClientDOB) BETWEEN 1970 AND 1980
        GROUP BY Genre
        ORDER BY COUNT(*) DESC
        LIMIT 1;

        -- 8. Top 5 occupations that borrowed most in 2016
        SELECT Occupation
        FROM Client
        JOIN Borrower ON Client.ClientID = Borrower.ClientID
        WHERE YEAR(BorrowDate) = 2016
        GROUP BY Occupation
        ORDER BY COUNT(*) DESC
        LIMIT 5;

        -- 9. Average number of borrowed books by job title
        SELECT Occupation, AVG(NumBorrowed) as AvgBorrowed
        FROM (
            SELECT Occupation, COUNT(*) as NumBorrowed
            FROM Client
            JOIN Borrower ON Client.ClientID = Borrower.ClientID
            GROUP BY Client.ClientID
        ) as T
        GROUP BY Occupation;

        -- 10. Create a VIEW and display titles were borrow by at least %20 percent client
        CREATE VIEW PopularBooks AS
        SELECT BookTitle
        FROM Book
        JOIN Borrower ON Book.BookID = Borrower.BookID
        GROUP BY Book.BookID
        HAVING COUNT(DISTINCT ClientID) >= 0.2 * (SELECT COUNT(*) FROM Client);
        SELECT * FROM PopularBooks;

        -- 11. The top month borrows in year
        SELECT MONTH(BorrowDate) as Month, COUNT(*) as NumBorrowed
        FROM Borrower
        GROUP BY Month
        ORDER BY NumBorrowed DESC
        LIMIT 1;

        -- 12. Average number borrows by age
        SELECT YEAR(CURDATE()) - YEAR(ClientDOB) AS Age, AVG(NumBorrowed) as AvgBorrowed
        FROM (
            SELECT ClientDOB, COUNT(*) as NumBorrowed
            FROM Client
            JOIN Borrower ON Client.ClientID = Borrower.ClientID
            GROUP BY Client.ClientID
        ) as T
        GROUP BY Age;

        -- 13. The oldest youngest client library
        SELECT ClientFirstName, ClientLastName, ClientDOB
        FROM Client
        ORDER BY ClientDOB
        LIMIT 1;
        SELECT ClientFirstName, ClientLastName, ClientDOB
        FROM Client
        ORDER BY ClientDOB DESC
        LIMIT 1;

        -- 14. First last name author wrote book more than one genre
        SELECT AuthorFirstName, AuthorLastName
        FROM Author
        JOIN Book ON Author.AuthorID = Book.AuthorID
        GROUP BY Author.AuthorID
        HAVING COUNT(DISTINCT Genre) > 1;








