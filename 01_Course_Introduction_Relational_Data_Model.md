# CMU Database Systems - 01 Course introduction & Relational Data Model (Fall 2018)

## Today's Agenda
* Wait List
* Overview
* Course Logistics
* Relational Model
* Relational Algebra

## Course Overview
This course is on the design and implementation of disk-oriented database management systems.

Not a course on how to use a database to build applications or how to administer a database.

Build database systems in C++. That's what we're doin.

## Course Outline

* Relational Databases
* Storage
* Execution
* Concurrency Control
* Recovery
* Distributed Databases
* Potpourri

## Textbook
[Database System Concepts - 6th Edition - Silberschatz, Korth, Sudarshan](https://www.amazon.com/Database-Concepts-Abraham-Silberschatz-Professor/dp/0073523321)

## Course Rubric
* Homeworks (15%)
* Projects (45%)
* Midterm Exam (20%)
* Final Exam (20%)
* Extra Credit (+10%)

# Actual Notes

1. Database
	* Organized collection of inter-related data that models some aspect of the real-world.
	* Databases are core components of most computer applications.

2. Database Examples
	* Create a database that models a digital music store to keep track of artists and albums.

	* Things we need to store:
		* Information about Artists
		* What Albums those Artists released

3. Flat File Strawman
Store our database as comma-seperated value (CSV) files that we manage in our own code.
* Use a seperate file per entity.
* The application has to parse the files each time they want to read/update records.

Ex: Create a database that models a digital music store:

Artist(name, year, country):
"Wu Tang Clan", 1992, "USA"
"Notorious BIG", 1992, "USA"
"Ice Cube", 1989, "USA"

Album(name, artist, year):
"Enter the Wu Tang", "Wu Tang Clan", 1993
"St. Ides Mix Tape", "Wu Tang Clan", 1994

To find when Ice Cube release his music:
```python3
for line in file:
	record = parse(line)
	if "Ice Cube" == record[0]:
		print(int(record[1]))
```

Problems:
* Bad. Slow and Bad.
* How do you find a particular reord?
* What if we now want to create a new application that uses the same database?
* What if two threads try to write to the same file at the same time?
* How do we ensure that the artist is the same for each album entry?
What if somebody overrites the album year with an invalid sgring?
How do we store that there were multiple artists on an album?
* What happens if the machine crashes while our program is updating a record?
* What if we want to replicate the database on multiple machines for high availability?

4. Database Management System
A **DBMS** is a software that allows applicatoins to store and analyze information in a database.

A general-purpose DBMS is designed to allow the definition, creation, querying, update, and administration of databases.

**Early DBMSs**
Database applications were difficult to build and maintain.
Tight coupling between logical and physical layers.
You have to (roughly) know what queries your app would execute before you deployed the database.

5. Relational Model
	* Proposed in 1970 by Ted Codd.
Database abstraction to avoid this maintenance:
	* Store database in simple data structures (relations).
	* Access data through high-level language.
	* Physical storage left up to implementation.

6. Data Models
	* A data model is a collection of concepts for describing the data in a database.
	* A schema is a description of a particular collection of data, using a given data model.

Data models:
* Relational
* Key/Value
* Graph
* Document
* Column-family
* Array/Matrix
* Hierarchical
* Network

## Relational Model
* Structure: The definition of relations and their contents
* Integrity: Ensure the database's contents satisfy constraints.
* Manipulations: How to access and modify the database's contents.

A **relation** is an unordered set that contains the relationship of attributes that represent entites.

A **tuple** is a set of attribute values also known as its domain) in he relation..
* Values are (normally) atomic/scalar.
* The special value NULL is a member of every domain.

### Relational Model: Primary Keys
A relation's primary key uniquely identifies a single tuple.
Some DBMSs automatically create an  internal primary key if you don't define one.
Auto-generation of unique integer primary keys:
* SEQUENCY (SQL:2003)
* AUTO_INCREMENT (MySQL)

### Relational Model: Foerign Keys

A **foreign key** specifies that an attribute from one relation has to map to a tuple in another relation.

## Data Manipulation Languages (DML)

How to store and retrieve information from a database.

* Procedural:
	* The query specifies the (high-level) strategy the DBMS should use to find the desirec result.
* Non-Procedural:
	* The query specifies only what data is wanted, and not how to find it.

## Relational Algebra

Fundamental operations to retrieve and manupulate tuples in a relation.
* Based on set algebra.

Each operator takes one or more relations as its inputs and outputs a new relation.
* We can "chain" operators together to create more complex operations.

Operations:
* σ Select
* ∏ Projection
* U Union
* ∩ Intersection
* - Difference

#### Relational Algebra: Select
Choose a subset of the tuples from a relation that satisfies a selection predicate.
* Predicate acts as a filter to retain only tuples that fulfill its qualifying requirement.
* Can combine muiple predicates using conjunctions / disjunctions.
Syntax sigma sub predicate(R)

#### Relational Algebra: Projection
Generate a relation with tuples that contains only the specified attributes.
* Can rearrange attributes' ordering
* Can manipulate the values.
Syntax: pi sub A1, A2, ..., An (R)


#### Relational Algebra: Union
Generate a relation that contains all tuples that appear in either only one or both of the input relations.
Syntax: (R U S)

#### Relational Algebra: Intersection
Generate a relation that contains only the tuples that appear in both of the input relations.
Syntax: (R ∩ S)

#### Relational Algebra: Difference
Generate a relation that contains oly the tuples that appear in the first and not the second of the input relations.
Syntax: (R - S)
SQL: Except.

#### Relational Algebra: Product

Generate a relation that contains all possible combinations of tuples from the input relations.

Syntax (R x S)

Shows up in testing. Cartesian product.
SQL: CROSS JOIN

#### Relational Algebra: Join

Generate a relation that contains all tuples that area a combination of two tuples (one from each input relation) with a comon values) for one or more attributes.

Syntax: (R  S)

#### Relational Algebra: Extra Operators:
* Rename
* Assignment
* Duplicate Elimination
* Aggregation
* Sorting
* Division

#### Relational Model: Queries
The relational model is independent of any query language implementaiton.
**SQL** is the *de facto* standard.
















