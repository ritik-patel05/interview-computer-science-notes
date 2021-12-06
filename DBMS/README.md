## Database
A database is an organized collection of data stored and accessed electronically from a computer system.

## Database Management System (DBMS)
It is the software that interacts with the end users, applications and the database itself to capture and analyze the data.

Enables users to define, create, maintain and control access to the database.

Example: MySQL, PostgreSQL.

## Functionality Or Advantages of DBMS
1. Data storage, retrieval and update
2. User accessible catalog or data dictionary describing the metadata
3. Support for transactions and concurrency
4. Facilities for recovering the database should it become damaged
5. Support for authorization of access and update of data
6. Access support from remote locations
7. Enforcing constraints to ensure data in the database abides by certain rules

## Keys
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

## Referential integrity

An example of a database that has not enforced referential integrity. In other words there is a foreign key value with no corresponding primary key value in the referenced table. <br/>
<img src="https://user-images.githubusercontent.com/67374176/144797070-f81ebaf4-40da-4c02-860b-3714e19a83e8.png" width="300" height="250"> <br/>

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

## Database Normalization

##### Why/Need?
* To reduce data redundancy and improve data integrity.

* When an attempt is made to modify (update, insert into, or delete from) a table, the following undesirable side-effects may arise if the table is not sufficiently normalized.

1. Update anamoly <br/>
<img src="https://user-images.githubusercontent.com/67374176/144832326-72e492b6-4340-4d52-a1b1-0d966998de0e.png" width="800" height="200" /> <br/>
Employee 519 is shown as having different addresses on different records.
2. Insertion anamoly<br/>
<img src="https://user-images.githubusercontent.com/67374176/144832323-a96e04c8-1f91-4976-b0c5-83ee25785aa9.png" width="800" height="200"  /> <br/>
Until the new faculty member, Dr. Newsome, is assigned to teach at least one course, their details cannot be recorded.
3. Deletion anamoly <br/>
<img src="https://user-images.githubusercontent.com/67374176/144832317-8c7975b2-533a-4e23-b7f8-6d7cbc74c504.png" width="800" height="200" /> <br/>
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

### Examples

###### Table not in 1NF :
<img src="https://user-images.githubusercontent.com/67374176/144809444-d9febd17-024a-43c0-a4d2-b97377d12ef4.png" width="800" height="300" />

###### Converting table to 1NF :
<img src="https://user-images.githubusercontent.com/67374176/144809191-766aabc8-0d72-480f-a7ec-e7ecf8d17425.jpg" width="800" height="300" />

###### Table in 1NF but not in 2NF :
<img src="https://user-images.githubusercontent.com/67374176/144807470-f6d0d5df-4158-4363-a01e-8918d693b660.jpg" width="800" height="300" /> <br/>
The relation is not in 2NF. {Manufacturer, Model} is a candidate key, and Manufacturer country is dependent on a proper subset of it: Manufacturer.

###### Converting Table to 2NF :
<img src="https://user-images.githubusercontent.com/67374176/144807993-10b5cdcd-b9ca-4ec9-861b-70d6adb664cc.jpg" width="200" height="300" />

###### Table in 2NF but not in 3NF :
<img src="https://user-images.githubusercontent.com/67374176/144806499-c9bda141-e0a0-480a-b890-bee98a66e050.png" width="800" height="200" /> <br/>
The fact that Winner's date of birth is functionally dependent on Winner makes the table vulnerable to logical inconsistencies, as there is nothing to stop the same person from being shown with different dates of birth on different records.

###### Converting table from 2NF to 3NF :
It is necessary to split table into two. <br/>
<img src="https://user-images.githubusercontent.com/67374176/144806782-4fa25c86-19d1-4817-8eb0-1294077f2618.png" width="800" height="200" />

## ACID  (atomicity, consistency, isolation, durability)
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

## Why is concurrency control needed?
* If concurrent transactions with interleaving operations are allowed in an uncontrolled manner, many problems can occur such as,
1. The lost update problem
A second transaction writes a second value of a data-item on top of a first value written by a first concurrent transaction. Hence, the first value is lost to the other transactions running concurrently which need, by their precedence, to read the first value.
2. The dirty read problem
Transactions read a value written by a transaction that has been later aborted. Hence, the reading transactions end with incorrect results.
3. The incorrect summary problem
While one transaction takes a summary(e.g., sum of values) over the values of all the instances of a repeated data-item, a second transaction updates some instances of that data-item.

Most high performance transactional systems need to run transactions concurrently to meet their performance requirements. Hence, we require Concurrency Control Mechanisms.

## Concurrency Control Mechanisms
1. Optimistic
* While running, transactions use data resources without acquiring locks on those resources. Before committing, each transaction verifies that no other transaction has modified the data it has read. If the check reveals conflicting modifications, the committing transaction rolls back and can be restarted.
* Used in databases having low *data contention*(multiple processes competing for access to the same data block at the same time, e.g., frequent updates, index or table scans)
* If contention for data resources is frequent, the cost of repeatedly restarting transactions hurts performance significantly, in which case other concurrency methods may be better suited. However, locking-based ("pessimistic") methods also can deliver poor performance because locking can drastically limit effective concurrency even when deadlocks are avoided.
2. Pessimistic
The system assumes the wost - it assumes that two or more users will want to update the same record at the same time, and then prevents that possibility by locking the record, no matter how unlikely conflicts actually are.
The locks are placed as soon as any piece of the row is accessed, making it impossible for two or more users to update the row at the same time. 
Depending on the lock mode *(shared, exclusive, or update)*, other users might be able to read the data even though a lock has been placed.  

## Locks
* A lock is a mechanism for preventing two or more users from doing conflicting operations at the same time.
* If all are read only operations, then no conflict.
* If all are write only operations, then no conflict.
* Row-level locks: are placed on single records (rows) that the statements in a transaction define. The locks are placed as soon as any piece of the row is accessed.
* Table-level locks: they prevent concurrent users from making schema changes (DDL operations) simultaneously or while records within the table are being changed.
e.g., if you are updating a customer’s home phone number, you do not want another user to drop the telephone number column at the same time. If the other user was allowed to drop the telephone number column before you were finished, your transaction would try to write an updated telephone number to a column that no longer exists, thus resulting in data corruption.

## Lock Modes
1. SHARED
Row-level shared locks allow multiple users to read data, but do not allow any users to change that data.
Multiple users can hold shared locks simultaneously.
Table-level shared locks allow multiple users to perform read and write operations on the table, but do not allow any users to perform DDL operations.

2. EXCLUSIVE
An exclusive lock allows only one user/connection to update a particular piece of data (insert, update, and delete).
When one user has an exclusive lock on a row or table, no other lock of any type may be placed on it.

3. UPDATE
Update locks are always row-level locks.
When a user accesses a row with the SELECT... FOR UPDATE statement, the row is locked with an update mode lock.
This means that no other user can read or update the row and ensures the current user can later update the row.
You can acquire an update lock on a record that already has a shared lock, but you cannot acquire a shared lock on a record that already has an update lock. Because an update lock prevents subsequent read locks, it is easier to convert the update lock to an exclusive lock.
Shared and exclusive locks cannot be mixed. If User1 has an exclusive lock on a record, User2 cannot get a shared lock or an exclusive lock on that same record.

## Methods for concurrency control
### Two-phase Locking(2PL)
is a concurrency control method that guarantees serializability(if its outcome is equal to the outcome of its transaction executed serially.)

Two major types of locks are used:

* Write-lock (exclusive lock) is associated with a database object by a transaction (Terminology: "the transaction locks the object," or "acquires lock for it") before writing (inserting/modifying/deleting) this object.
* Read-lock (shared lock) is associated with a database object by a transaction before reading (retrieving the state of) this object.

Compatability(Two transactions, ig ):
has read-lock(i): need read-lock(j) (yes)
has read-lock(i): need write-lock(j) (no, hence make edge Ti->Tj in precedence graph) 
has write-lock(i): need write-lock(j) (no, Ti->Tj)
has write-lock(i): need read-lock(j) (no, Ti->Tj)

*"no"* indicates incompatibility, i.e, a case when a lock of the first type (in left column) on an object blocks a lock of the second type (in top row) from being acquired on the same object (by another transaction). An object typically has a queue of waiting requested (by transactions) operations with respective locks. 

### Serialization (Conflict serializable) graph checking
Checking for cycles in the schedule's graph and breaking them by aborts.

The schedule S is serializable if and only if the *precedence graph* has no cycles. if T1 and T2 constitute a cycle, then it is not(conflict) serializable.

## References
Portions of this note is taken from Wikipedia, support.unicomsi.com