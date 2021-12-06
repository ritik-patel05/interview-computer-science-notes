### Database
A database is an organized collection of data stored and accessed electronically from a computer system.

### Database Management System (DBMS)
It is the software that interacts with the end users, applications and the database itself to capture and analyze the data.

Enables users to define, create, maintain and control access to the database.

Example: MySQL, PostgreSQL.

### Functionality Or Advantages of DBMS
1. Data storage, retrieval and update
2. User accessible catalog or data dictionary describing the metadata
3. Support for transactions and concurrency
4. Facilities for recovering the database should it become damaged
5. Support for authorization of access and update of data
6. Access support from remote locations
7. Enforcing constraints to ensure data in the database abides by certain rules

### Keys
##### 1. Super Key: 
Set of attributes(columns) that uniquely identify each tuple(rows) of a relation.
##### 2. Candidate Key:
A minimal super key. 
Example, consider we identified super key as:
* Super Key: {ABCD, ABC, ABD, BCD, AB, BC, CD}
* Candidate Key: {AB,BC, CD} => because, minimal 2 columns can uniquely identify rows in a table.  
##### 3. Primary Key:
One of the candidate keys
##### 4. Foreign Key:
* A foreign key is a set of attributes in a table that refers to the primary key of another table.
* It links these two tables.
* Parent(Referenced) Table and Child(Referencing) Table.
##### Prime attributes
The attributes which are in atleast one candidate key.

### Referential integrity

An example of a database that has not enforced referential integrity. In other words there is a foreign key value with no corresponding primary key value in the referenced table.
![Referential_integrity_broken](https://user-images.githubusercontent.com/67374176/144797070-f81ebaf4-40da-4c02-860b-3714e19a83e8.png)

* A property of data stating that all its references are valid.
* When a foreign key value is used it must reference a valid, existing primary key in the parent table or it can contain null values.
* For instance, deleting a record that contains a value referred to by a foreign key in another table would break referential integrity. 
* Some relational database management systems (RDBMS) can enforce referential integrity, normally either by deleting the foreign key rows as well to maintain integrity, or by returning an error and not performing the delete.

##### 1. CASCADE
Whenever rows in the parent (referenced) table are deleted (or updated), the respective rows of the child (referencing) table with a matching foreign key column will be deleted (or updated) as well. This is called a cascade delete (or update).

##### 2. RESTRICT
A value cannot be updated or deleted when a row exists in a referencing(child) table that references the value in the referenced(parent) table.

##### 3. SET NULL, SET DEFAULT
The value of the affected referencing attributes is changed to NULL for SET NULL, and to the specified default value for SET DEFAULT during DELETE or UPDATE.

### Database Normalization

##### Why/Need?
* To reduce data redundancy and improve data integrity.

* When an attempt is made to modify (update, insert into, or delete from) a table, the following undesirable side-effects may arise if the table is not sufficiently normalized.

1. Update anamoly
![560px-Update_anomaly svg](https://user-images.githubusercontent.com/67374176/144800950-f38a8574-ddec-4c5b-93d9-963a3d834ecb.png)
Employee 519 is shown as having different addresses on different records.
2. Insertion anamoly
![560px-Insertion_anomaly svg](https://user-images.githubusercontent.com/67374176/144800945-ea2f213c-955d-4662-9396-7816241ee396.png)
Until the new faculty member, Dr. Newsome, is assigned to teach at least one course, their details cannot be recorded.
3. Deletion anamoly
![560px-Deletion_anomaly svg](https://user-images.githubusercontent.com/67374176/144800938-e21b2df6-73a9-4c93-b8e7-a4a7bc18fcca.png)
All information about Dr. Giddens is lost if they temporarily ceases to be assigned to any courses.

##### Normal Forms
* Most 3NF relations are free of insertion, updation, and deletion anomalies.

1. 1NF: First Normal Form
Atomic columns (cells cannot have tables as values)
2. 2NF: Second Normal Form
1NF + All the non prime attributes should be fully functional dependent on candidate key.
3. 3NF: Third Normal Form
2NF and,
For every functional dependency, X -> A, at least one of the following holds: X is a super key or every element of A \ X, the set difference between A and X, is a prime attribute.

##### Examples

###### Table not in 1NF :
![Table not in 1NF](https://user-images.githubusercontent.com/67374176/144809444-d9febd17-024a-43c0-a4d2-b97377d12ef4.png)

###### Converting table to 1NF :
![Converting table to 1NF](https://user-images.githubusercontent.com/67374176/144809191-766aabc8-0d72-480f-a7ec-e7ecf8d17425.jpg)


###### Table in 1NF but not in 2NF :
![table in 1NF but not in 2NF](https://user-images.githubusercontent.com/67374176/144807470-f6d0d5df-4158-4363-a01e-8918d693b660.jpg)
The relation is not in 2NF. {Manufacturer, Model} is a candidate key, and Manufacturer country is dependent on a proper subset of it: Manufacturer.

###### Converting Table to 2NF :
![Converting table to 2NF](https://user-images.githubusercontent.com/67374176/144807993-10b5cdcd-b9ca-4ec9-861b-70d6adb664cc.jpg)

###### Table in 2NF but not in 3NF :
![Table in 2NF but not in 3NF](https://user-images.githubusercontent.com/67374176/144806499-c9bda141-e0a0-480a-b890-bee98a66e050.png)
The fact that Winner's date of birth is functionally dependent on Winner makes the table vulnerable to logical inconsistencies, as there is nothing to stop the same person from being shown with different dates of birth on different records.

###### Converting table from 2NF to 3NF :
It is necessary to split table into two.
![Converting table from 2NF to 3NF](https://user-images.githubusercontent.com/67374176/144806782-4fa25c86-19d1-4817-8eb0-1294077f2618.png)

### ACID  (atomicity, consistency, isolation, durability)
* It is a set of properties of database transactions intended to guarantee data validity despite errors, power failures, and other mishaps.
* A *Transaction* represents any change in the database.

1. Atomicity: The series of database operations in transaction will either all occur or none will occur.
2. Consistency (Correctness): Any transaction must change affected data only in allowed ways. i.e. any data written must be valid according to all defined rules, constraints, cascades, triggers.
3. Isolation:
* Transactions are often executed *concurrently*(e.g., multiple transactions reading and writing to a table at the same time). 
* Isolation ensures that concurrent execution of transactions leaves the database in the same state that would have been obtained if the transactions were executed sequentially.
4. Durability: 
* Durability guarantees that once a transaction has been committed, it will remain committed even in the case of a system failure (e.g., power outage or crash).
* This usually means that completed transactions are recorded in non-volatile memory.

