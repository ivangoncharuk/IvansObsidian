#fall2023 #COSC-457 

**LECTURE 2**

- Data abstraction:
	- refers to the suppression of...

- **Data Model**: A collection of concepts to describe the structure of a database, and certain constraints that the database should obey.
- **Data Model Operations**: Operations for specifying database retrievals and updates by referring to the concepts of the data model. 

Operations on the data model may include:
	- basic operations
	- user-defined operations
		- inserts, delete, modify, or retrieve
	- `COMPUTE_GPA` in `STUDENT` object

- Data Model Example: ![[data_model_example_hospital.png]]

## Categories of data models
- **Conceptual** (`high-level`, `semantic`) **datamodels**: provide concepts that are close to the way many users perceive data (also called entity-based or object-based models.)
- **Implementation** (`representational`) **data models**: provide concepts that fall between the above two, balancing user views with some computer storage details.
- **Physical** (`low-level`, `internal`) **data models**: provide concepts that describe details of how data is stored in the computer.
 
## History of Data Models
- Relational Model: proposed in 1970 by E.F. Codd (IBM)
- first commercial system in 1981-82
- Now in several commercial products
	- DB2, Oracle, SQL Server, Sybase, Informix

## Hierarchical Model
- Advantages:
- Disadvantages:

## Network Model
- Advantages:
- Disadvantages:

## Schemas versus Instances
- **Database Schema**: The description of a database.
- **Schema Diagram**: A diagrammatic display of a database schema
- **Schema Construct**: A component of the schema or an object within the schema, e.g., STUDENT, COURSE.
- **Database Instance**: The actual data stored in a database at a particular moment in time. Also called database state (or occurrence)

- **Database State**: Refers to the content of a database at a moment in time.
- **Initial Database State**: Refers to the database when it is loaded.
- **Valid State**: A state that satisfies the structure and constraints of the database.

## Three-Schema Architecture
- Proposed to support DBMS characteristics of:
	- Program-data independence.
	- Support of multiple views of the data.
- **Internal Schema**: at the internal level to describe physical storage and access paths. Typically uses a physical data model.
- Conceptual Schema: 
- External Schemas
- **Mapping**: among schema levels are needed to transform requests and data. 

[[Database Management System]] Languages explained in this lecture