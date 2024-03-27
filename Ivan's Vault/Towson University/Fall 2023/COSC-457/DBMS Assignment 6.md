>Course: COSC457-101 – Database Management Systems
>Assignment#6 SQL script
>Due Date: Dec 7, 2023, 11:59pm
>Name: Ivan Goncharuk

### Queries for questions 1-10
```python
queries = {
    "1": (
        "Get supplier names and numbers for all suppliers who supplied part P3 and whose name begins with the letter A.",
        """
        SELECT S.S_NAME, S.S_NUM
        FROM S
        JOIN JPS ON S.S_NUM = JPS.S_NUM
        JOIN P ON JPS.P_NUM = P.P_NUM
        WHERE P.P_NUM = 'p3' AND S.S_NAME LIKE 'A%'
        """,
    ),
    "2": (
        "Get supplier names for suppliers who supplied for job J2. (Use a nested query)",
        """
        SELECT DISTINCT S.S_NAME
        FROM S
        WHERE S.S_NUM IN (
            SELECT JPS.S_NUM
            FROM JPS
            WHERE JPS.J_NUM = 'j2'
        )
        """,
    ),
    "3": (
        "Get supplier names for suppliers who supplied parts for jobs only in Athens. (Use a nested query)",
        """
        SELECT S.S_NAME
        FROM S
        WHERE S.S_NUM IN (
            SELECT JPS.S_NUM
            FROM JPS
            JOIN J ON JPS.J_NUM = J.J_NUM
            WHERE J.CITY = 'Athens'
            EXCEPT
            SELECT JPS.S_NUM
            FROM JPS
            JOIN J ON JPS.J_NUM = J.J_NUM
            WHERE J.CITY != 'Athens'
        )
        """,
    ),
    "4": (
        "Get part names for parts that are not supplied for job J3. (Use a nested query)",
        """
        SELECT P.PNAME
        FROM P
        WHERE P.P_NUM NOT IN (
            SELECT JPS.P_NUM
            FROM JPS
            WHERE JPS.J_NUM = 'j3'
        )
        """,
    ),
    "5": (
        "Which city has the most suppliers? (Use a nested query)",
        """
        SSELECT CITY
        FROM (
	        SELECT CITY, COUNT(*) AS SUPPLIER_COUNT
	        FROM S
	        GROUP BY CITY
		) AS CITY_COUNTS
		ORDER BY SUPPLIER_COUNT DESC
		LIMIT 1
        """,
    ),
    "6": (
        "Calculate each supplier's total sales quantity and get the salesperson's name if the salesperson supplies parts more than 1000 units in total.",
        """
        SELECT S.S_NAME, SUM(JPS.QTY) AS TOTAL_SALES
        FROM S
        JOIN JPS ON S.S_NUM = JPS.S_NUM
        GROUP BY S.S_NUM
        HAVING TOTAL_SALES > 1000
        """,
    ),
    "7": (
        "Increase the status values of suppliers by 5 who are located in Paris.",
        """
        UPDATE S SET STATUS = STATUS + 5 WHERE CITY = 'Paris';
        """,
        "SELECT * FROM S WHERE CITY = 'Paris';",
    ),
    "8": (
        "Change the name to 'Hammer' of parts that are Red and located in London and whose name was Screw.",
        """
        UPDATE P SET PNAME = 'Hammer' WHERE COLOR = 'Red' AND CITY = 'London' AND PNAME = 'Screw';
        """,
        "SELECT * FROM P WHERE COLOR = 'Red' AND CITY = 'London';",
    ),
    "9": (
        "Delete all jobs in Rome and all corresponding part shipments.",
        """
        DELETE FROM JPS WHERE J_NUM IN (SELECT J_NUM FROM J WHERE CITY = 'Rome');
        DELETE FROM J WHERE CITY = 'Rome';
        """,
        "SELECT * FROM J;",
    ),
    "10": (
        "Smith moved to Adam's location. Please update Smith's city but do not use the city name directly.",
        """
        UPDATE S
        SET CITY = (
            SELECT CITY
            FROM S
            WHERE S_NAME = 'Adams'
        )
        WHERE S_NAME = 'Smith'
        """,
        "SELECT * FROM S;",
    ),
}

```

### Results
1. Get supplier names and numbers for all suppliers who supplied part P3 and whose name begins with letter A.
	- `('Adams', 's5')`
2. Get supplier names for suppliers who supplied for job J2. (Use a nested query)
	- `('Jones',)`
	- `('Blake',)`
	- `('Adams',)`
3. Get supplier names for suppliers who supplied parts for jobs only in Athens. (Use a nested query)
	- `('Smith',)`
4. Get part names for parts that are not supplied for job J3. (Use a nested query)
	- `('Nut',)`
	- `('Bolt',)`
	- `('Screw',)`
	- `('Cam',)`
5. Which city has the most suppliers? (Use a nested query)
	- `('London',)`
6. Calculate each supplier's total sales quantity and get the sales person's name if the sales person supplies parts more than 1000 units in total.
	- `('Jones', 3200)`
	- `('Adams', 3100)`
7. Description: Increase the status values of suppliers by 5 who are located in Paris.
```
+-------+--------+--------+-------+
| S_NUM | S_NAME | STATUS |  CITY |
+-------+--------+--------+-------+
|   s2  | Jones  |   15   | Paris |
|   s3  | Blake  |   35   | Paris |
+-------+--------+--------+-------+
```
8. Change the name to 'Hammer' of parts that are Red and located in London and whose name was Screw.
```
+-------+--------+-------+--------+--------+
| P_NUM | PNAME  | COLOR | WEIGHT |  CITY  |
+-------+--------+-------+--------+--------+
|   p1  |  Nut   |  Red  |   12   | London |
|   p4  | Hammer |  Red  |   14   | London |
|   p6  |  Cog   |  Red  |   19   | London |
+-------+--------+-------+--------+--------+
```
9. Delete all jobs in Rome and all corresponding part shipments.
```
+-------+----------+--------+
| J_NUM |  JNAME   |  CITY  |
+-------+----------+--------+
|   j1  |  Sorter  | Paris  |
|   j3  |  Reader  | Athens |
|   j4  | Console  | Athens |
|   j5  | Collator | London |
|   j6  | Terminal |  Oslo  |
|   j7  |   Tape   | London |
+-------+----------+--------+
```
10. Smith moved to Adam's location. Please update Smith's city but do not use the city name directly.
```
+-------+--------+--------+--------+
| S_NUM | S_NAME | STATUS |  CITY  |
+-------+--------+--------+--------+
|   s1  | Smith  |   20   | Athens |
|   s2  | Jones  |   15   | Paris  |
|   s3  | Blake  |   35   | Paris  |
|   s4  | Clark  |   20   | London |
|   s5  | Adams  |   30   | Athens |
+-------+--------+--------+--------+
```


### Driver Code
```python
import sqlite3

class DataBaseClient:
    def __init__(self):
        self.conn = sqlite3.connect("db/new_database.db")
        self.cursor = self.conn.cursor()

    def execute_query(self, query):
        """Execute a single query that does not require parameters."""
        try:
            self.cursor.execute(query)
            self.conn.commit()
            print("Query executed successfully")
        except sqlite3.Error as e:
            print(f"An error occurred: {e.args[0]}")

    def execute_query_with_params(self, query, params):
        try:
            self.cursor.execute(query, params)
            self.conn.commit()
            print("Data inserted successfully for: ", params)
        except sqlite3.IntegrityError as ie:
            print(f"Integrity error occurred during insert: {ie}")
        except sqlite3.Error as e:
            print(f"An error occurred during insert: {e.args[0]}")

    def query_data(self, query):
        """Query data from the database and return the results."""
        try:
            self.cursor.execute(query)
            results = self.cursor.fetchall()
            return results
        except sqlite3.Error as e:
            print(f"An error occurred: {e.args[0]}")
            return None

    def confirm_insertion(self, table_name):
        """Function to verify that the data has been inserted"""
        self.cursor.execute(f"SELECT * FROM {table_name}")
        rows = self.cursor.fetchall()
        if rows:
            print(f"{len(rows)} rows present in {table_name}")
        else:
            print(f"No data present in {table_name}")

    # ----------------------------------------------------------------------------------------------------

    def insert_j(self, j_num, jname, city):
        query = """INSERT INTO J (J_NUM, JNAME, CITY) VALUES (?, ?, ?)"""
        params = (j_num, jname, city)
        self.execute_query_with_params(query, params)

    # Function to insert into P table
    def insert_p(self, p_num, pname, color, weight, city):
        query = """INSERT INTO P (P_NUM, PNAME, COLOR, WEIGHT, CITY) VALUES (?, ?, ?, ?, ?)"""
        params = (p_num, pname, color, weight, city)
        self.execute_query_with_params(query, params)

    # Function to insert into S table
    def insert_s(self, s_num, s_name, status, city):
        query = """INSERT INTO S (S_NUM, S_NAME, STATUS, CITY) VALUES (?, ?, ?, ?)"""
        params = (s_num, s_name, status, city)
        self.execute_query_with_params(query, params)

    # Function to insert into JPS table
    def insert_jps(self, s_num, p_num, j_num, qty):
        query = """INSERT INTO JPS (S_NUM, P_NUM, J_NUM, QTY) VALUES (?, ?, ?, ?)"""
        params = (s_num, p_num, j_num, qty)
        self.execute_query_with_params(query, params)

    def create_tables(self):
        create_table_statements = [
            """CREATE TABLE J (
                J_NUM VARCHAR(10),
                JNAME VARCHAR(15),
                CITY VARCHAR(15),
                PRIMARY KEY (J_NUM)
            )""",
            """CREATE TABLE P (
                P_NUM VARCHAR(10),
                PNAME VARCHAR(15),
                COLOR VARCHAR(10),
                WEIGHT DECIMAL(5, 2),
                CITY VARCHAR(15),
                PRIMARY KEY (P_NUM)
            )""",
            """CREATE TABLE S (
                S_NUM VARCHAR(10),
                S_NAME VARCHAR(15),
                STATUS INT,
                CITY VARCHAR(15),
                PRIMARY KEY (S_NUM)
            )""",
            """CREATE TABLE JPS (
                S_NUM VARCHAR(10),
                P_NUM VARCHAR(10),
                J_NUM VARCHAR(10),
                QTY INT,
                PRIMARY KEY (S_NUM, P_NUM, J_NUM),
                FOREIGN KEY (S_NUM) REFERENCES S(S_NUM),
                FOREIGN KEY (P_NUM) REFERENCES P(P_NUM),
                FOREIGN KEY (J_NUM) REFERENCES J(J_NUM)
            )""",
        ]

        for statement in create_table_statements:
            self.execute_query(statement)

    def populate_db(self):
        # Populate with new data
        j_data = [
            ("j1", "Sorter", "Paris"),
            ("j2", "Punch", "Rome"),
            ("j3", "Reader", "Athens"),
            ("j4", "Console", "Athens"),
            ("j5", "Collator", "London"),
            ("j6", "Terminal", "Oslo"),
            ("j7", "Tape", "London"),
        ]
        p_data = [
            ("p1", "Nut", "Red", 12, "London"),
            ("p2", "Bolt", "Green", 17, "Paris"),
            ("p3", "Screw", "Blue", 17, "Rome"),
            ("p4", "Screw", "Red", 14, "London"),
            ("p5", "Cam", "Blue", 12, "Paris"),
            ("p6", "Cog", "Red", 19, "London"),
        ]
        s_data = [
            ("s1", "Smith", 20, "London"),
            ("s2", "Jones", 10, "Paris"),
            ("s3", "Blake", 30, "Paris"),
            ("s4", "Clark", 20, "London"),
            ("s5", "Adams", 30, "Athens"),
        ]
        jps_data = [
            ("s1", "p1", "j4", 700),
            ("s2", "p3", "j1", 400),
            ("s2", "p3", "j2", 200),
            ("s2", "p3", "j3", 200),
            ("s2", "p3", "j4", 500),
            ("s2", "p3", "j5", 600),
            ("s2", "p3", "j6", 400),
            ("s2", "p3", "j7", 800),
            ("s2", "p5", "j2", 100),
            ("s3", "p3", "j1", 200),
            ("s3", "p4", "j2", 500),
            ("s4", "p6", "j3", 300),
            ("s4", "p6", "j7", 300),
            ("s5", "p1", "j4", 100),
            ("s5", "p2", "j2", 200),
            ("s5", "p2", "j4", 100),
            ("s5", "p3", "j4", 200),
            ("s5", "p4", "j4", 800),
            ("s5", "p5", "j4", 400),
            ("s5", "p5", "j5", 500),
            ("s5", "p5", "j7", 100),
            ("s5", "p6", "j2", 200),
            ("s5", "p6", "j4", 500),
        ]

        try:
            self.conn.execute("BEGIN TRANSACTION;")
            for j in j_data:
                self.insert_j(*j)
            for p in p_data:
                self.insert_p(*p)
            for s in s_data:
                self.insert_s(*s)
            for jps in jps_data:
                self.insert_jps(*jps)
            self.conn.commit()
        except sqlite3.Error as e:
            self.conn.rollback()
            print(f"Error: {e.args[0]}")

    def print_table_structure(self):
        for table_name in ["J", "P", "S", "JPS"]:
            self.cursor.execute(f"PRAGMA table_info({table_name})")
            info = self.cursor.fetchall()
            print(f"Structure of {table_name}:", info)

    def main(self):
        database_client = DataBaseClient()
        database_client.create_tables()
        database_client.print_table_structure()
        database_client.populate_db()

        # Close the connection
        database_client.conn.close()

if __name__ == "__main__":
    DataBaseClient().main()

```