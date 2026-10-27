<br>

### Table: Authors

```
CREATE TABLE Authors (
    authorid INT,
    authorf_name VARCHAR(50),
    authorl_name VARCHAR(50),
    birthyear INT
);
```

```
INSERT INTO Authors (authorid, authorf_name, authorl_name, birthyear)
VALUES
    (101, 'F. Scott', 'Fitzgerald', 1896),
    (102, 'Harper', 'Lee', 1926),
    (103, 'J.R.R.', 'Tolkien', 1892),
    (104, 'George', 'Orwell', 1903);
```

### Table: Books

```
CREATE TABLE Books (
    bookid INT,
    title VARCHAR(100),
    genre VARCHAR(50),
    price DECIMAL(5, 2),
    authorid INT
);
```

```
INSERT INTO Books (bookid, title, genre, price, authorid)
VALUES
    (1, 'The Great Gatsby', 'Fiction', 14.50, 101),
    (2, 'To Kill a Mockingbird', 'Fiction', 12.75, 102),
    (3, 'The Hobbit', 'Fantasy', 19.50, 103),
    (4, '1984', 'Dystopian', 16.25, 104);
```

### Equi-Join Example

- Perform an Equi-Join to retrieve information about books and their corresponding author details
- based on the equality of the AuthorID columns.

```
SELECT 
    Books.BookID, 
    Books.Title, 
    Books.Genre, 
    Books.Price, 
    Authors.AuthorF_Name, 
    Authors.AuthorL_Name, 
    Authors.BirthYear
FROM Books
JOIN Authors 
ON Books.AuthorID = Authors.AuthorID;
```

**OUTPUT**:  
| bookid | title                | genre     | price | authorf_name | authorl_name | birthyear |
|--------|---------------------|-----------|-------|--------------|--------------|-----------|
| 1      | The Great Gatsby     | Fiction   | 14.50 | F. Scott     | Fitzgerald   | 1896      |
| 2      | To Kill a Mockingbird| Fiction   | 12.75 | Harper       | Lee          | 1926      |
| 3      | The Hobbit           | Fantasy   | 19.50 | J.R.R.       | Tolkien      | 1892      |
| 4      | 1984                 | Dystopian | 16.25 | George       | Orwell       | 1903      |

### True Theta Join Example

- Use a Theta Join to retrieve book and author information based on a join condition
- that involves a comparison operator other than equality.

```
SELECT 
    Books.BookID, 
    Books.Title, 
    Books.Genre, 
    Books.Price,
    Authors.AuthorF_Name,
    Authors.AuthorL_Name,
    Authors.BirthYear
FROM Books
JOIN Authors 
ON Books.Price > Authors.BirthYear;  
```

- This query retrieves records where the price of a book is greater than the birth year of the author.

Another Theta Join Example with filtering

- Retrieve books with price conditions as part of the join itself (beyond equality).

```
SELECT 
    Books.BookID, 
    Books.Title, 
    Books.Genre, 
    Books.Price,
    Authors.AuthorF_Name,
    Authors.AuthorL_Name,
    Authors.BirthYear
FROM Books
JOIN Authors 
ON Books.AuthorID = Authors.AuthorID
WHERE Books.Price > 15.00;  
```

**OUTPUT**:  
| bookid | title     | genre    | price | authorf_name | authorl_name | birthyear |
|--------|-----------|----------|-------|--------------|--------------|-----------|
| 3      | The Hobbit| Fantasy  | 19.50 | J.R.R.       | Tolkien      | 1892      |
| 4      | 1984      | Dystopian| 16.25 | George       | Orwell       | 1903      |
