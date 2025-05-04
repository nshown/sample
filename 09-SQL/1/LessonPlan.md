## 9.1: Introduction to SQL

### Overview

In today's class, the students will be introduced to SQL databases and will learn how to create tables and simple queries.

### Class Objectives

By the end of this lesson, the students will be able to:

* Install and run Postgres and pgAdmin on their computers.

* Create a database and tables using pgAdmin.

* Define SQL data types, primary keys, and unique values.

* Load CSV files into a database and query the data.

* Articulate the four basic functions of persistent storage (CRUD) and apply this set of functions to a database.

* Combine data from multiple tables using JOINs.

---

### Instructor Notes

**Important:** If you did not have students install PostgreSQL and pgAdmin last week, make sure to to direct them to the installation instructions on Canvas for this week's module. The students should install both before class begins.

Today's class will be challenging. In this lesson, a series of activities will introduce students to programming with SQL using Postgres and pgAdmin. The pace of today's class will be quick as students absorb learning a new UI and programming language simultaneously.

Because the lesson introduces more than one new concept, check in with the students during student activities to assist those who appear frustrated or stuck. Some students may already have experience with SQL. Embrace these students' knowledge of the language and have them assist the students who are not yet familiar with SQL.

This lesson introduces new content rapidly. The students may express frustration at learning a new interface and programming language simultaneously. Explain to them that SQL experience is highly prized, and the steep learning curve is well worth the effort.

---

### Class Slides

The slides for this lesson can be viewed on Google Drive here: [Lesson 9.1 Slides](https://docs.google.com/presentation/d/1xcx3d0LDS3Cq0LRbdPs7wiwT_Vg4qgoKJWzuM74Nyl8/edit?usp=sharing).

To add the slides to the student-facing repository, download the slides as a PDF by navigating to File, selecting "Download as," and then choosing "PDF document." Then, add the PDF file to your class repository along with other necessary files. You can view instructions for this [here](https://docs.google.com/document/d/1XM90c4s9XjwZHjdUlwEMcv2iXcO_yRGx5p2iLZ3BGNI/edit).

**Note:** Editing access is not available for this document. If you wish to modify the slides, create a copy by navigating to File and selecting "Make a copy...".

---

### Time Tracker

| Start Time | Number | Activity                                           | Duration |
| ---------- | ------ | -------------------------------------------------- | -------- |
| 6:30 PM    | 1      | Instructor Do: Welcome Class                       | 0:05     |
| 6:35 PM    | 2      | Instructor Do: Introduction to SQL                 | 0:05     |
| 6:40 PM    | 3      | Everyone Do: Create a Database                     | 0:05     |
| 6:45 PM    | 4      | Instructor Do: Create a Table                      | 0:10     |
| 6:55 PM    | 5      | Students Do: Creating Tables                       | 0:15     |
| 7:10 PM    | 6      | Review: Creating Tables                            | 0:05     |
| 7:15 PM    | 7      | Instructor Do: The Value of Unique Values          | 0:05     |
| 7:20 PM    | 8      | Students Do: Making and Using an ID                | 0:10     |
| 7:30 PM    | 9      | Review: Making and Using an ID                     | 0:10     |
| 7:40 PM    | 10     | BREAK                                              | 0:15     |
| 7:55 PM    | 11     | Instructor Do: Import Data                         | 0:10     |
| 8:05 PM    | 12     | Students Do: Hide and Seek                         | 0:10     |
| 8:15 PM    | 13     | Review: Hide and Seek                              | 0:05     |
| 8:20 PM    | 14     | Instructor Do: CRUD                                | 0:05     |
| 8:25 PM    | 15     | Students Do: Using CRUD                            | 0:20     |
| 8:45 PM    | 16     | Review: Using CRUD                                 | 0:05     |
| 8:50 PM    | 17     | Instructor Do: Joins                               | 0:15     |
| 9:05 PM    | 18     | Partner Do: Joining Bird Bands                     | 0:20     |
| 9:25 PM    | 19     | Review: Joining Bird Bands                         | 0:05     |
| 9:30 PM    |        | END                                                |          |

---

### 1. Instructor Do: Welcome Class (5 min)

Open the slideshow to welcome students to this lesson.

Welcome students to class and congratulate them on making it through the project week. They have come very far since the beginning of the course and should feel proud of what they have accomplished so far!

Explain the learning outcomes for the SQL unit and today's class objectives.

Tell the students that today's lesson will introduce them to one of the most popular programming languages for working with databases: SQL. SQL programmers are in high demand, so this is an important language to understand. SQL allows us to manipulate and mine data and access large amounts of data with ease.

---

### 2. Instructor Do: Introduction to SQL (5 min)

Before starting the lesson's activities, use the slideshow to go over the purpose of SQL.

* SQL (often pronounced "sequel") stands for Structured Query Language. It is a powerful tool that enables programmers to create, populate, manipulate, and access databases. It also provides an easy method for dealing with server-side storage.

* Data using SQL is stored in tables on the server, much like spreadsheets you would create in Microsoft Excel. This makes the data easy to visualize and search.

* PostgreSQL (usually referred to as "Postgres") is an object-relational database system that uses the SQL language.

* pgAdmin is the management tool used for working with Postgres. It simplifies creation, maintenance, and use of database objects.

---

### 3. Everyone Do: Create a Database (5 min)

Begin by verifying that all students have successfully installed pgAdmin and Postgres. Everyone should have completed this step prior to today's class.

Continue through the slideshow to show the students how to create a database in pgAdmin.

* Open pgAdmin in a new browser window and ensure that everyone is able to follow along and view their new server in the browser.

    ![browser-view.png](https://static.bc-edx.com/data/dl-1-2/m9/lessons/1/img/9-1-browser-view.png)

Demonstrate the steps to create a database using pgAdmin.

* In the pgAdmin editor, right-click the newly established server to create a new database.

* From the menu, select **Create**, and then select **Database** to create a new database.

    ![create_database.png](https://static.bc-edx.com/data/dl-1-2/m9/lessons/1/img/9-1-create_database.png)

* Enter **animals_db** as the database name. Make sure the owner is set as **postgres** (default setting), and then click **Save**.

    ![animals_db.png](https://static.bc-edx.com/data/dl-1-2/m9/lessons/1/img/9-1-animals_db.png)

At this point, show students that there is a new database listed in the left-hand menu. Explain that the new database, `animals_db`, is not yet connected to the server. Clicking on the database will create a connection to Postgres.

  ![new_db.png](https://static.bc-edx.com/data/dl-1-2/m9/lessons/1/img/9-1-new_db.png)

Answer any questions before moving on.

---

### 4. Instructor Do: Create a Table (10 min)

**Corresponding Activity:** [02-Ins_Creating_Tables](Activities/02-Ins_Creating_Tables)

Now that there is a database on the server, it's time to dig into SQL and start creating tables within the new database!

Utilize the next few slides to assist the students in understanding how to create tables in SQL.

From the left-hand menu in pgAdmin, right-click **animals_db** and select **Query Tool**.

  **Note:** You can also select **Query Tool** from the Tools drop-down menu at the top of the screen. (See second screenshot below.)

  ![query_tool.png](https://static.bc-edx.com/data/dl-1-2/m9/lessons/1/img/9-1-query_tool.png)

  ![tools_dropdown.png](https://static.bc-edx.com/data/dl-1-2/m9/lessons/1/img/9-1-tool_dropdown.png)

Explain to students that this is how to access the code editor.

Type the following lines of code, explaining each line:

  ```sql
  CREATE TABLE people (
    name VARCHAR(30) NOT NULL,
    has_pet BOOLEAN DEFAULT false,
    pet_type VARCHAR(10) NOT NULL,
    pet_name VARCHAR(30),
    pet_age INT
  );
  ```

* `CREATE TABLE people (<COLUMNS>);` creates a table called `people` with the columns listed within the parentheses.

* `name VARCHAR(30) NOT NULL` creates a `name` column that holds character strings of up to 30 characters and will not allow null fields.

* The `NOT NULL` constraint requires the name field to have a value specified.

* `pet_type VARCHAR(10) NOT NULL` creates a `pet_type` in the same manner as the `name` column is created. The only difference is the number of characters allowed in the column.

* `has_pet BOOLEAN DEFAULT false` creates a `has_pet` column that holds either true or false values. Here the default value is set as false.

* `pet_name VARCHAR(30)` creates a `pet_name` column that holds character strings of up to 30 characters and will allow null fields.

* `pet_age INT` creates a `pet_age` column that holds whole numbers.

* **Note:** Be sure to point out the semicolon at the end of the statement, which tells pgAdmin that this line of code has concluded.

After reviewing the code, click the play icon to run the script.

  ![lightning_bolt.png](https://static.bc-edx.com/data/dl-1-2/m9/lessons/1/img/9-1-lightning_bolt.png)

Point out that the Messages tab at the bottom of the screen that says "CREATE TABLE" was returned successfully.

Next, demonstrate that the structure of a "people" table can be visualized by typing and running `SELECT * FROM people;` below the table creation code in the query editor.

When we run all the code, including the SELECT statement, in the query editor again we get an error message: `ERROR:  relation "people" already exists`.

* Explain that SQL data is persistent. It is not deleted or overwritten when identical commands are run unless specifically commanded. This means that when a database or table is created with a name identical to one that already exists, an error will occur telling the user that the database or table already exists.

* Ask the class how to avoid this kind of error. The students may respond that they can simply delete the offending line of code and then run the commands again. Explain that while this method would work, deleting working code is not a best practice.

* Show the class an alternative method: Highlight the lines of code to run, and then click the play icon to run only the highlighted selection. This method of running SQL code is preferable to deleting previous code.

    ![Select.png](https://static.bc-edx.com/data/dl-1-2/m9/lessons/1/img/9-1-Select.png)

* Explain that using the asterisk in the `SELECT * FROM people;` statement tells pgAdmin to select all fields from the table.

* In the future, the students will be able to view the structure of their table and all of the values contained within it by using this same line of code.

Type the following code while explaining what it does line by line.

  ```sql
  INSERT INTO people (name, has_pet, pet_type, pet_name, pet_age)
  VALUES ('Jacob', true, 'dog', 'Misty', 10),
    ('Ahmed', true, 'rock', 'Rockington', 100),
    ('Peter', true, 'cat', 'Franklin', 2),
    ('Dave', true, 'dog', 'Queso', 1);

  SELECT *
  FROM people;
  ```

* This code operates as it reads: it inserts data into the `people` table and then specifies the columns in which data will be entered.

* The `VALUES` line places the data contained in the parentheses into the corresponding columns listed after the `INSERT INTO` statement.

* Single quotation marks must be used for insert strings; otherwise, an error will result.

* Values are added as a tuple in the exact order as the table schema. If a value is not present, then `NULL` or empty quotes can be used to avoid errors.

* Commas separate each row of tuples that are inserted into the table so that multiple rows may be inserted in a single query. A missing comma at the end of a tuple will produce an error.

Use the following code to query the table, extracting only the `pet_name`.

  ```sql
  SELECT pet_name
  FROM people;
  ```

* Explain that specifying a column name in the `SELECT` statement will return only the data contained in that field.

Filter the queried data to display only dogs younger than 5.

  ```sql
  SELECT pet_type, pet_name
  FROM people
  WHERE pet_type = 'dog'
  AND pet_age < 5;
  ```

Explain the following points:

* The `SELECT` clause can specify more than one column.

* Data is filtered by using additional clauses such as `WHERE` and `AND`.

* The `WHERE` clause will extract only the data that meets the condition specified. `AND` adds a second condition to the original clause, further refining the query.

* Note that unlike in Python where comparisons are done with a double equals (`==`) sign, in SQL only a single equal sign is used.

---

### 5. Students Do: Creating Tables (15 min)

**Corresponding Activity:** [03-Stu_Creating_Tables](Activities/03-Stu_Creating_Tables)

Continue through the slides to present this activity to the class.

In this activity, students will use pgAdmin to recreate and query a table from an image provided.

---

### 6. Review: Creating Tables (5 min)

Use the slideshow to assist you in reviewing the activity.

You may open the following file to copy the solution SQL code when reviewing this activity:

  **File:** [stu_creating_tables_solution.sql](Activities/03-Stu_Creating_Tables/Solved/stu_creating_tables_solution.sql)

Create a new database named `city_info` in pgAdmin. Then use the query tool to copy and paste, or live code, the solution from `stu_creating_tables_solution.sql`.

* Remind the students that they must specify the data type for each column when creating a new table.

    ```sql
    CREATE TABLE cities (
      city VARCHAR(30) NOT NULL,
      state VARCHAR(30) NOT NULL,
      population INT
    );
    ```

Insert multiple rows of data into the new table.

* Point out to students that each column is specified in the `INSERT INTO` clause, and the values are inserted in the same order.

* To make the code easier to read, we should place each row of values on its own line, separated by a comma.

    ```sql
    INSERT INTO cities (city, state, population)
    VALUES ('Alameda', 'California', 79177),
      ('Mesa', 'Arizona', 496401),
      ('Boerne', 'Texas', 16056),
      ('Anaheim', 'California', 352497),
      ('Tucson', 'Arizona', 535677),
      ('Garland', 'Texas', 238002);
    ```

Create a query to view the data using the `SELECT` clause.

  ```sql
  SELECT *
  FROM cities;
  ```

* Point out the syntax here. Even though the code can fit on a single line, it's good practice to split it up over two lines instead. This makes the code easier to read when more advanced queries are created.

Using the `SELECT` clause again, query the data to return only the cities in the table.

  ```sql
  SELECT city
  FROM cities;
  ```

Explain to students that the first bonus question incorporates a `WHERE` clause, which further filters the data.

* The `WHERE` clause is used to search for specific data within a database. In this case, we are extracting only the records that meet the specified condition.

* In the line `WHERE state = 'Arizona';` we are specifying Arizona in the state column.

    ```sql
    SELECT city, state
    FROM cities
    WHERE state = 'Arizona';
    ```

Demonstrate the solution to the second bonus question.

* Point out to students that the `WHERE` clause is highly customizable, such as with the use of the `<` operator.

    ```sql
    SELECT *
    FROM cities
    WHERE population < 100000;
    ```

Go through the solution to the third and final bonus question.

* Explain to students that queries can be filtered even further with the `AND` clause. This clause allows users to specify more than one condition in their query.

    ```sql
    SELECT *
    FROM cities
    WHERE population < 100000
    AND state = 'California';
    ```

Answer any questions before moving on.

---

### 7. Instructor Do: The Value of Unique Values (5 min)

**Corresponding Activity:** [04-Ins_Values_of_Uniques](Activities/04-Ins_Values_of_Uniques)

Use the slides to introduce the class to Unique Values.

**File:** [values_of_uniques_solution.sql](Activities/04-Ins_Values_of_Uniques/Solved/values_of_uniques_solution.sql)

Using the `people` table from the `animals_db` database, insert the duplicate data below into the table and then visualize the table with the new information.

  ```sql
  INSERT INTO people (name, has_pet, pet_type, pet_name, pet_age)
  VALUES ('Ahmed', true, 'rock', 'Rockington', 100);

  SELECT *
  FROM people;
  ```

* Duplicate data is a real-world occurrence (and an eyesore). Demonstrate how to remove the rows containing the string `Ahmed` in the `name` column.

    ```sql
    DELETE FROM people
    WHERE name = 'Ahmed';
    ```

* The duplicate was deleted, but so was the original row. That's a little annoying. Make sure the class understands why this happened.

* Because the name Ahmed appears twice in the table, SQL assumes that the user wants to delete every column containing that name. SQL doesn't understand that the user only wants to remove the duplicate row.

* To prevent this kind of thing from occurring, programmers will often create a column that automatically populates each new row with unique data. This allows them to select and modify that row more easily.

Remove the `people` table by running the following line of code:

  ```sql
  -- Delete the table "people"
  DROP TABLE people;
  ```

Copy the following code from the `values_of_uniques.sql` file and paste it in the pgAdmin editor.

  ```sql
  -- Re-create the table "people" within animals_db
  CREATE TABLE people (
    id SERIAL PRIMARY KEY,
    name VARCHAR(30) NOT NULL,
    has_pet BOOLEAN DEFAULT false,
    pet_type VARCHAR(10) NOT NULL,
    pet_name VARCHAR(30),
    pet_age INT
  );

  -- Insert data into the table
  INSERT INTO people (name, has_pet, pet_type, pet_name, pet_age)
  VALUES ('Jacob', true, 'dog', 'Misty', 10),
    ('Ahmed', true, 'rock', 'Rockington', 100),
    ('Ahmed', true, 'rock', 'Rockington', 100),
    ('Peter', true, 'cat', 'Franklin', 2),
    ('Dave', true, 'dog', 'Queso', 1),
    ('Dave', true, 'dog', 'Pringles', 7);

  -- Query all fields from the table
  SELECT *
  FROM people;
  ```

* Explain that a *primary key* uniquely identifies a row.

* `SERIAL` generates a new value for each inserted record in the table. By default, the starting value is 1, and it will increase by 1 for each new record. When using `SERIAL` with our unique `PRIMARY KEY`, we automatically get unique, incrementing values for each table row.

* Point out that because values will automatically increment, each row's ID is guaranteed to be unique. This ensures that SQL does not identify and update the wrong row when CRUD—Create, Read, Update, Delete—statements are implemented.

* Point out that the `INSERT` statements have not changed, as they do not need to insert data specifically into the `id` column. SQL automatically provides a value for this column, fulfilling the uniqueness constraint by automatically incrementing the last value used as an ID.

* The data type for the `id` column is automatically assigned as an integer.

One entry in the table is incorrect: one of the Daves has the wrong `pet_name` and `pet_age`. We need to update the `pet_name` from Pringles to Rocket and the `pet_age` from 7 to 8.

* To avoid issues with updating multiple rows, it's best to update by ID. First, query by name to find the ID for the row we want to update.

    ```sql
    SELECT id, name, pet_name, pet_age
    FROM people
    WHERE name = 'Dave';
    ```

* This will return all rows that contain the name Dave, including the `id`, `pet_name`, and `pet_age` columns.

* Next, we can select and update the `pet_name` from Pringles to Rocket and the `pet_age` from 7 to 8 based on the row's unique ID.

    ```sql
    UPDATE people
    SET has_pet = true, pet_name = 'Rocket', pet_age = 8
    WHERE id = 6;
    ```

* Note that, similar to a query, the `WHERE` statement is used to pinpoint the data we want to change. In this case, the `id` column is used to select the unique row we want to affect.

* Duplicate data is also easier to remove with the use of a unique ID. Using the following code, remove the duplicate data.

    ```sql
    DELETE FROM people
    WHERE id = 3;
    ```

* This does precisely what was desired: duplicate data is deleted, and original data is preserved.

Answer any remaining questions before moving on.

---

### 8. Students Do: Making and Using an ID (10 min)

**Corresponding Activity:** [05-Stu_Making_IDs](Activities/05-Stu_Making_IDs)

Continue the slideshow to present this activity to the class.

In this activity, students will recreate a table and then query, insert, and update data.

---

### 9. Review: Making and Using an ID (10 min)

Use the slideshow to assist you in reviewing the activity.

**File:** [making_ids_solution.sql](Activities/05-Stu_Making_IDs/Solved/making_ids_solution.sql)

Open `making_ids_solution.sql` and copy the code into pgAdmin.

Go over the lines of code used to create the ID and set the ID as the primary key. Make sure the class understands how this works, and explain how useful this will be for the upcoming homework assignment.

Review how to create a new column using the `ALTER TABLE` and `ADD COLUMN` statements. Explain that adding the column name and data type is completed in the same manner as creating a new table.

Answer any questions before moving on.

---

### 10. BREAK (15 min)

---

### 11. Instructor Do: Import Data (10 min)

**Corresponding Activity:** [06-Ins_Importing_Data](Activities/06-Ins_Importing_Data)

Using the slides, introduce the section on how to import data to the class.

Send out the following files for the students who want to follow along during the demonstration:

So far, the class has created their own tables and values manually using SQL code. As one might imagine, this process can be tedious when translating large datasets from external sources. Thankfully, pgAdmin includes a built-in import tool that can take CSV files and easily import the data into tables.

Return to pgAdmin and create a new database called `Miscellaneous_DB`.

Open the CSV file within an integrated development environment (IDE), such as Excel, to show the dataset that will be imported. Be sure to point out that the first row of this dataset includes headers.

* Open a query tool within `Miscellaneous_DB` and create a table named `fauna_vertabrate`.

* Using the code from `importing_data_solution.sql`, create the columns necessary to import the data. Point out that the columns created match the data in the CSV file.

* Once the table and columns have been created, right-click **Miscellaneous_DB** from the left-hand menu and select **Refresh**.

* Scroll down to Schemas and expand that menu, and then expand the Tables menu, as captured in the following image:

    ![table-expand.png](https://static.bc-edx.com/data/dl-1-2/m9/lessons/1/img/9-1-table-expand.png)

* Right-click the new table and select **Import/Export** from the menu, as captured in the following image:

    ![import-export.png](https://static.bc-edx.com/data/dl-1-2/m9/lessons/1/img/9-1-import-export.png)

In the Options tab, complete the following steps:

* Slide the Import/Export tab to **Import**.

* Click on the dot menu to navigate to the `Fauna_Vertabrate.csv` file on your computer.

* Slide the Header tab to **Yes**.

* Select the comma from the drop-down menu to set it as the Delimiter.

* Leave the other fields as they are, and then click **OK**.

* These settings are captured in the following image:

    ![import.png](https://static.bc-edx.com/data/dl-1-2/m9/lessons/1/img/9-1-import.png)

In the query tool, rerun `SELECT * FROM fauna_vertabrate` to verify that data has been imported.

Let the class know that the bigger a dataset is, the longer it will take for pgAdmin to import values.

Data Source: City of Perth/Data WA (2021). Fauna Vertebrate. [https://catalogue.data.wa.gov.au/dataset/perth-fauna-vertabrate](https://catalogue.data.wa.gov.au/dataset/perth-fauna-vertabrate)

---

### 12. Students Do: Hide and Seek (10 min)

**Corresponding Activity:** [07-Stu_Hide_and_Seek](Activities/07-Stu_Hide_and_Seek)

Use the next few slides to present this activity to the class.

In this activity, students will create a new table and import data from a CSV file.

Data Source: Krisztian Balog, Filip Radlinski and Alexandros Karatzoglou from Google LLC (2021). SoftAttributes: Relative movie attribute dataset for soft attributes. [https://github.com/google-research-datasets/soft-attributes](https://github.com/google-research-datasets/soft-attributes).

---

### 13. Review: Hide and Seek (5 min)

Utilize the slides to assist you in reviewing the activity.

Send out the solution file to students:

  **File:** [hide_and_seek_solution.sql](Activities/07-Stu_Hide_and_Seek/Solved/hide_and_seek_solution.sql)

Open pgAdmin and paste the code from `hide_and_seek_solution.sql` into the editor. Explain the following:

* To view a range of data, we can use a combination of `WHERE` and `AND` statements.

* To collect data that exists in either one column or another, we include the `OR` statement in the query.

Go through the solutions to the bonus questions, touching on the following point:

* `AND` statements can be used more than once for more specific results.

Answer any questions before moving on.

---

### 14. Instructor Do: CRUD (5 min)

Use the slides to introduce CRUD to the class.

Return to the slideshow and explain CRUD operations.

* CRUD, while an unusual acronym, stands for a set of operations that are used throughout programming: Create, Read, Update, and Delete.

Engage the class in a discussion by asking them to provide examples of CRUD operations.

The students have already used each of these operations during the course. They have:

* Created data in a table with the `INSERT` statement.

* Read data by using `SELECT`.

* Updated a table's data by using `UPDATE`.

* Deleted data via `DELETE`.

Introduce the class to an additional method of reading the data: wildcards.

* A wildcard is a character that takes the place of one or more characters in a query. For SQL, there are two options: percentage sign (%) and underscore (_).

* The keyword `LIKE` indicates the use of a wildcard in a query.

* The percentage sign (%) signifies that zero, one, or multiple characters will be substituted in a query.

    * For example, in the query `WHERE last_name LIKE 'Will%';` all names in the database beginning with "Will" are returned, no matter the length.

* When using the underscore as a wildcard, only a single character is replaced in the query.

* In the line `WHERE first_name LIKE '_an';`, only three-lettered names ending with "an" will be returned.

Answer any questions before moving on.

---

### 15. Students Do: Using CRUD (20 min)

**Corresponding Activity:** [08-Stu_CRUD](Activities/08-Stu_CRUD)

Use the slideshow to present this activity to the class.

In this activity, students will use CRUD operations (Create, Read, Update, Delete) on the provided data.

Let the class know that they will be using the `WHERE` clause in this activity.

This activity will require students to conduct some research. Links are provided to help them search for solutions to problems they are likely to encounter.

Data Sources:

* Institut Penyelidikan Keselamatan Jalan Raya Malaysia (MIROS). General Road Accident Statistics in Malaysia. [https://www.data.gov.my/data/en_US/dataset/general-road-accident-statistics-in-malaysia](https://www.data.gov.my/data/en_US/dataset/general-road-accident-statistics-in-malaysia)

* Royal Malaysian Police (PDRM). Road Accident Statistics by Type of Accident and Injury. [https://www.data.gov.my/data/ms_MY/dataset/statistik-kemalangan-jalan-raya-mengikut-jenis-kemalangan-dan-kecederaan](https://www.data.gov.my/data/ms_MY/dataset/statistik-kemalangan-jalan-raya-mengikut-jenis-kemalangan-dan-kecederaan)
-- N.B.: This dataset has been translated from Malay and had columns removed.

---

### 16. Review: Using CRUD (5 min)

Use the slideshow to assist you in reviewing the activity.

**Files:**

* [schema.sql](Activities/08-Stu_CRUD/Resources/schema.sql)

* [using_crud_solution.sql](Activities/08-Stu_CRUD/Solved/using_crud_solution.sql)

* [mys_road_accidents.csv](Activities/08-Stu_CRUD/Resources/mys_road_accidents.csv)

* [mys_accidents_by_state.csv](Activities/08-Stu_CRUD/Resources/mys_accidents_by_state.csv)

Create a new database, `Malaysia`, and open a query tool and copy and paste the code from `schema.sql` to create two new tables named `road_accidents` and `accidents_by_state`. Go over the following steps and details:

* Refresh the table list.

* Then import the data from `mys_road_accidents.csv` into the `road_accidents` table.

* Next, import the data from `mys_accidents_by_state.csv` into the `accidents_by_state` table.

* Open the solution file `using_crud_solution.sql` to copy the SQL into the query tool and demonstrate the code, covering the following points:

    * The data for all years, except 2017, that don’t have missing values in `road_accidents` table are deleted from the `accidents_by_state` table.

    * In the SELECT statement, multiple columns can be summed.

    * Values can be inserted into the table, even though not every value is filled out.

    * Finally, select all values in the `road_accidents` table to show the newly updated and inserted data.

* Send out the solution file and answer any questions the students may have before moving on.

---

### 17. Instructor Do: Joins (15 min)

**Corresponding Activity:** [09-Ins_Joins](Activities/09-Ins_Joins)

Continue through the slideshow to introduce joins to the class.

Send out the following files for the students who want to follow along with hands-on experience during the demonstration:

**Files:**

* [joins_solution.sql](Activities/09-Ins_Joins/Solved/joins_solution.sql)

* [names.csv](Activities/09-Ins_Joins/Resources/names.csv)

* [commodity.csv](Activities/09-Ins_Joins/Resources/commodity.csv)

Students may recall working with merges and joins to combine datasets during the Pandas module. While SQL is a vastly different language than Python, it also includes the functionality to merge tables.

Create two new tables in `Miscellaneous_DB` in pgAdmin named `names` and `commodity`.

* Copy the code from `joins.sql` to create the tables, and then import the corresponding data from `names.csv` and `commodity.csv`.

* Remember to refresh the database. Newly created tables will not immediately appear.

* Point out that both tables have matching values within the `dep_id` column of the `names` table and the `dep_id` column of the `commodity` table.

* Because there are common values, it is possible to join these tables together. For example:

    ```sql
    INNER JOIN commodity ON
    commodity.dep_id=names.dep_id;
    ```

* From the `joins.sql` file, copy and paste the code for performing an `inner join` on the two tables:

    ```sql
    SELECT names.name, commodity.commod, commodity.commod_tp, commodity.commod_group
    FROM names
    INNER JOIN commodity ON
    commodity.dep_id=names.dep_id;
    ```

* Note: Some students may have advanced knowledge of SQL queries and use aliases in their solutions. Using aliases is not necessary for today's activities, but they will be covered more comprehensively in the next unit.

    ```sql
    -- Advanced INNER JOIN solution
    SELECT n.name, c.commod, c.commod_tp, c.commod_group
    FROM names as n
    INNER JOIN commodity as c ON
    c.dep_id=n.dep_id;
    ```

* Point out one significant difference between SQL joins and Python joins: in SQL joins, the columns that should be viewed after the join must be declared in the initial `SELECT` statement. This is demonstrated in the following image, which is a screenshot of the first 10 rows of the returned columns (`name`, `commod`, `commod_tp`, and `commod_group`):

    ![inner-join.png](https://static.bc-edx.com/data/dl-1-2/m9/lessons/1/img/9-1-inner-join.png)

There are five primary types of joins that can be used with PostgreSQL:

* `INNER JOIN` returns records that have matching values in both tables.

* `LEFT JOIN` returns all records from the left table and the matched records from the right table.

* `RIGHT JOIN` returns all records from the right table and the matched records from the left table.

* `CROSS JOIN` returns records that match every row of the left table with every row of the right table. This type of join has the potential to make very large tables.

* `FULL OUTER JOIN` places null values within the columns that do not match between the two tables, after an inner join is performed.

Send out the link to this explanation of Postgres [joins](https://www.tutorialspoint.com/postgresql/postgresql_using_joins.htm) for students to study.

Demonstrate a couple of different joins that can be performed. Then answer any questions before moving on to the next activity.

Data Source: McFaul, E.J., Mason, G.T., Ferguson, W.B., and Lipin, B.R., 2000, U.S. Geological Survey mineral databases. [https://mrdata.usgs.gov/mrds/](https://mrdata.usgs.gov/mrds/), specifically [rdbms-tab.zip](https://mrdata.usgs.gov/mrds/rdbms-tab.zip)

---

### 18. Partner Do: Joining Bird Bands (20 min)

**Corresponding Activity:** [10-Par_Joins](Activities/10-Par_Joins)

Use the slides to present this activity to the class.

In this activity, the students will use joins to learn more about North American bird banding.

Data Source: Celis-Murillo, A., Malorodova, M., and Nakash, E., 2020, North American Bird Banding Program Dataset 1960-2020 retrieved 2020-06-26: U.S. Geological Survey data release, [https://doi.org/10.5066/P9R1L6Q7](https://doi.org/10.5066/P9R1L6Q7). (Specifically files NABBP_2020_grp_06.csv [reduced in pandas] and NABBP_Lookups_2020.zip)

---

### 19. Review: Joining Bird Bands (5 min)

Use the slides to assist you in reviewing the activity.

Send out the solution file to the students:

**File:** [joining_bird_bands_solution.sql](Activities/10-Par_Joins/Solved/joining_bird_bands_solution.sql)

Since there are eight tables to load for this exercise, you may wish to load them prior to the review with students and focus more on the join queries. Using the schema.sql file and the query tool, create eight new tables named `bird_bands`, `age`, `band_type`, `bird_status`, `country_state`, `event_type`, `extra_info` and `sex` using the data in the corresponding CSV files.

Open `joining_bird_bands_solution.sql` and copy the code. Then open a new query tool and paste the solution into the editor. Review the solution and explain the following:

* Since the selected data comes from more than one table, the naming convention is `table_name.column_name`. Alternatively, aliases may be used for `table_name`.

* We need to determine which table to select from and which table to `INNER JOIN` with. Remember, the inner join only selects data that has matching values in both tables.

* Finally, we will determine the key both tables will join on. For example, to join the two tables by using the `id` (which in this case uses a label with the word `code`) and an `INNER JOIN`, select the data columns to be viewed from both tables, and then specify which columns the tables will be connected by.

* Repeat the previous two steps for any additional tables to be joined on.

    ```sql
    SELECT bird_bands.band,
      bird_bands.event_date,
      bird_bands.species_name,
      age.age_description,
      sex.sex_description
    FROM bird_bands
    INNER JOIN age ON
    bird_bands.age_code = age.age_code
    INNER JOIN sex ON
    bird_bands.sex_code = sex.sex_code;
    ```

* In the solution to the second question, discuss how the results can be limited with a `WHERE` clause, and demonstrate how using aliases for table names can shorten the code.

    ```sql
    SELECT b.band,
      b.event_date,
      b.species_name,
      bt.band_type_description,
      bs.bird_status_description,
      a.age_description,
      s.sex_description
    FROM bird_bands as b
    INNER JOIN band_type as bt ON
    b.band_type_code = bt.band_type_code
    INNER JOIN bird_status as bs ON
    b.bird_status = bs.bird_status
    INNER JOIN age as a ON
    b.age_code = a.age_code
    INNER JOIN sex as s ON
    b.sex_code = s.sex_code
    WHERE sex_description != 'Unknown';
    ```

Answer any questions before ending class.

---

© 2022 edX Boot Camps LLC. Confidential and Proprietary. All Rights Reserved.
