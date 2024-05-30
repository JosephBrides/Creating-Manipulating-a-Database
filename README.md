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








