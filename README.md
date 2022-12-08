# Mysql Workshop

This workshop is designed to build your confidence in querying data using SQL.

## Set up

We will be working with the dataset in the `init.sql` file. This file contains a set of SQL commands that will create a set of tables and fill them with data. We will connect to the mysql server running locally on our individual computers and tell it to run the file.

## Loading the file

Please download the init.sql file.

Now import the init.sql into your database.

## Schema diagrams

Here are the schema diagrams to help:

### Authors
Column | Type | Modifiers
--- | --- | ---
id | integer | not null default
first_name | character varying(100) | not null
surname | character varying(100) | not null
location | character varying(100) |

### Books

Column | Type | Modifiers
--- | --- | ---
id | integer | not null default
name | character varying(100) | not null
release_date | date | not null
publisher_id | integer | foreign key (publishers.id)

### Publishers

Column | Type | Modifiers
--- | --- | ---
id | integer | not null default
name | character varying(100) | not null

### Book Authors

Column | Type | Modifiers
--- | --- | ---
book_id | integer | foreign key (books.id)
author_id | integer | foreign key (authors.id)


## The challenges

Please don't feel that you have to get through all of them or be able to answer them all right away! The idea is to introduce you to the kind of queries we do regularly with SQL.

### Introductory

These challenges cover the basics of SQL: selects, joins and conditions.

#### 1. Find the first name and surname of every author

##### Expected result

first_name |    surname
--- | ---
Sharon     | Smith
Ted        | Burns
Stephen    | Wistle
Amanda     | Bertwistle
David      | Grewal
John       | White
Paul       | Hallam-Wistle
Paul       | Jones

#### 2. Sort everyone by surname and find the first three

##### Expected result

id | first_name |  surname   | location
--- | --- | --- | ---
4 | Amanda     | Bertwistle | Nazareth
2 | Ted        | Burns      | London
5 | David      | Grewal     |

#### 3. Find everyone who has a location specified

##### Expected result

id | first_name |    surname    | location
--- | --- | --- | ---
1 | Sharon     | Smith         | Nazareth
2 | Ted        | Burns         | London
4 | Amanda     | Bertwistle    | Nazareth
6 | John       | White         | London
7 | Paul       | Hallam-Wistle | London
8 | Paul       | Jones         | Nazareth

#### 4. Find everyone who is not in Nazareth (including nulls)

##### Expected result

id | first_name |    surname    | location
--- | --- | --- | ---
2 | Ted        | Burns         | London
3 | Stephen    | Wistle        |
5 | David      | Grewal        |
6 | John       | White         | London
7 | Paul       | Hallam-Wistle | London

#### 5. Find everyone with 'Wistle' in their surname (bonus points for case insensitivity)

##### Expected result

id | first_name |    surname    | location
--- | --- | --- | ---
3 | Stephen    | Wistle        |
4 | Amanda     | Bertwistle    | Nazareth
7 | Paul       | Hallam-Wistle | London

#### 6. Find the name of the publisher who released 'Python Made Easy'

##### Expected result

'No Starch Press'

#### 7. Find all the books published by 'No Starch Press'

##### Expected result

name | name
--- | ---
No Starch Press | Python Made Easy
No Starch Press | JavaScript: The Really Good Parts

#### 8. Show a list of every book and their authors
Note: Only one author per row, so the book's name may need to be repeated.

##### Expected result

name | first_name | surname
--- | --- | ---
Python Made Easy                  | Sharon     | Smith
Python Made Easy                  | David      | Grewal
Python Made Easy                  | Amanda     | Bertwistle
SQL: Part 2                       | Sharon     | Smith
JavaScript: The Really Good Parts | Stephen    | Wistle
JavaScript: The Really Good Parts | David      | Grewal
Java in Japanese                  | Paul       | Jones
Java in Japanese                  | Ted        | Burns
Java in Japanese                  | Stephen    | Wistle
Java in Japanese                  | David      | Grewal
Java in Japanese                  | Amanda     | Bertwistle
Elm Street                        | David      | Grewal
Elm Street                        | John       | White
Elm Street                        | Sharon     | Smith
CSS: Cansei                       | Amanda     | Bertwistle
CSS: Cansei                       | Paul       | Hallam-Wistle
Ruby Gems                         | Ted        | Burns
Ruby Gems                         | Paul       | Hallam-Wistle
C++                               | Paul       | Jones
C++                               | John       | White
C++                               | David      | Grewal
C++                               | Sharon     | Smith
CoffeeScript in Java              | Paul       | Hallam-Wistle
CoffeeScript in Java              | Stephen    | Wistle
Swift in 10 Days                  | Stephen    | Wistle
Swift in 10 Days                  | David      | Grewal

#### 9. Find all the books that Ted Burns authored

##### Expected result

'Java in Japanese' and 'Ruby Gems'

### Intermediate

These slightly trickier challenges will require you to use [aggregate functions](https://www.postgresql.org/docs/9.6/static/tutorial-agg.html) and/or [subqueries](https://www.tutorialspoint.com/postgresql/postgresql_sub_queries.htm).

#### 10. Find everyone who wrote at least three books

##### Expected result

first_name |    surname
--- | ---
Paul       | Hallam-Wistle
David      | Grewal
Sharon     | Smith
Amanda     | Bertwistle
Stephen    | Wistle

#### 11. Order the publishers by the number of books they have published.

##### Expected result

name | count
--- | ---
McGraw-Hill              |     4
The Big Publishing House |     3
No Starch Press          |     2
Mega Corp Ltd            |     1

#### 12. Find all books released after 1st Jan 1996, ordered by the number of people who wrote them.

##### Expected result

name | count
--- | ---
Java in Japanese     |     5
C++                  |     4
Elm Street           |     3
Swift in 10 Days     |     2
CoffeeScript in Java |     2
Ruby Gems            |     2

#### 13. What's the highest number of authors per book? The lowest?

##### Expected results

Highest: 'Java in Japanese' (5 authors)

Lowest: 'SQL: Part 2' (1 author)

#### 14. Who wrote the most books? How many did they write?

##### Expected result

David Grewal, 6
