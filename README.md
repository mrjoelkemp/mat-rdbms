Relational Database in Matlab 
==========
Author: Joel KempProject: Database Systems 1 Final Project, Fall 2011, CCNY
#### Introduction

This text-based, relational database management system was build purely in Matlab r2011b.

The system can be launched via the rdbms.m file. The function `rdbms()` is the entry point to the application.

Alternatively, you can look at screenshots of the running application in the `screens/` folder.

#### Architecture

The system maintains a save-file that holds a recent copy of the database after any major operations. The save file is located in the root directory of the source code.

The architecture of the system is broken down into the following main sections: 

1. Define Table: allows the user to define new tables that will be managed by a collection of tables.

2. Extend Table: allows the user to define constraints (boolean conditions, functional dependencies, multi value dependencies, and keys) and tuples for any table in the DB.

3. Modify Table: allows a user to perform a plethora of set (table) operations (union, difference, intersection, cross-join, etc).

4. Delete Table: allows a user to delete any table in the DB.

#### Data Structures

*Table*:

* name: The name of the table
* schema: TreeMap of attribute to datatype associations.
* constraints: A list of constraints (fd, mvd, conditions, keys). See `constraint.m` for the exact structure.

*Constraint*:

* conditions: List of boolean conditions
* fds: List of functional dependencies
* mvds: List of multi-value dependencies
* keys: List of attribute keys

*Dependency*: Represents a functional dependency or multi-value dependency

* lhs: The left hand attribute (or attributes) of the dependency
* rhs: The right hand attribute (or attributes)
 * Note: multiple attributes on the RHS are converted to two or more simpler dependencies.
 
*Condition*: Represents a single condition. Can be "chained" using boolean **AND** or **OR**.

* lhs: Attribute
* operator: `<, >, ==, <>, <=, >=`
* rhs: Int of String value

Tuples:
Tuples did not have a pre-defined structure, however, a table's list of tuples was represented as a dynamic structure. Each tuple's structure was defined at runtime and used runtime-variable indexing to store the tuple values. The key to this schema is the table's schema (attribute -> datatype pairing).

#### Implementation Remarks

**Matlab lacks strings!**
Unfortunately, Matlab does not support strings natively. This constraint imposes impractical design decisions – almost always necessitating the use of (fragile) cell matrices to hold collections of variable-length strings. Cell matrices were heavily used in this system, although, there are places (namely, the storage of FD's and MVD's) that should have used a structure array for a more reliable implementation.

**Helpers were made global when necessary!**
 
 The directory structure for the project's source contains subdirectories. These subdirectories primary group the functions associated with a particular section of the system. In Matlab, in order for functions to be accessible to other functions (in different files), the functions need to defined in separate M-files.
 
 The M-files in the subdirectories are made available on the Matlab path at runtime.
 
 Only those functions that needed to be global were made so. Hence, there are certain files (`constraints.m` for example) that are rather large and could be cleaned up by migrating code to separate files.





