## 9.3: Data Modeling

### Overview

Today's lesson will focus on data modeling and best practices for designing a database. Students will learn how to normalize data and how tables in a database are related. They will also learn how to create visualizations of databases by using entity relationship diagrams (ERDs).

### Class Objectives

By the end of today's lesson, the students will be able to:

* Apply data modeling techniques to database design.

* Normalize data.

* Identify data relationships.

* Create visual representations of a database through ERDs.

---

### Instructor Notes

This lesson uses pure SQL mainly to supplement the ideas presented. If students continue to struggle with SQL basics, encourage them to practice on their own while still focusing on the concepts in this lesson.

The TAs should be ready to help explain and break down concepts for students struggling to grasp the material.

---

### Class Slides

The slides for this lesson can be viewed on Google Drive here: [Lesson 9.3 Slides](https://docs.google.com/presentation/d/1PT_MqFt4atL8E34a0HeiUME8Mq7BimiSmRzd-R6HXI8/edit?usp=sharing).

To add the slides to the student-facing repository, download the slides as a PDF by navigating to File, selecting "Download as," and then choosing "PDF document." Then, add the PDF file to your class repository along with other necessary files. You can view instructions for this [here](https://docs.google.com/document/d/1XM90c4s9XjwZHjdUlwEMcv2iXcO_yRGx5p2iLZ3BGNI/edit).

**Note:** Editing access is not available for this document. If you wish to modify the slides, create a copy by navigating to File and selecting "Make a copy...".

---

### Time Tracker

| Start Time | Number | Activity                                           | Duration |
| ---------- | ------ | -------------------------------------------------- | -------- |
| 6:30 PM    | 1      | Instructor Do: Welcome Class                       | 0:05     |
| 6:35 PM    | 2      | Instructor Do: Data Normalization                  | 0:15     |
| 6:50 PM    | 3      | Everyone Do: Pet Normalizer                        | 0:15     |
| 7:05 PM    | 4      | Instructor Do: Intro to Foreign Keys               | 0:15     |
| 7:20 PM    | 5      | Students Do: Foreign Keys                          | 0:15     |
| 7:35 PM    | 6      | Review: Foreign Keys                               | 0:05     |
| 7:40 PM    | 7      | Instructor Do: Intro to Data Relationships         | 0:15     |
| 7:55 PM    | 8      | Students Do: Data Relationships                    | 0:15     |
| 8:10 PM    | 9      | Review: Data Relationships                         | 0:05     |
| 8:15 PM    | 10     | BREAK                                              | 0:15     |
| 8:30 PM    | 11     | Instructor Do: Entity Relationship Diagrams        | 0:15     |
| 8:45 PM    | 12     | Everyone Do: Designing an ERD, Part 1              | 0:10     |
| 8:55 PM    | 13     | Everyone Do: Designing an ERD, Part 2              | 0:10     |
| 9:05 PM    | 14     | Instructor Do: Introduction to Unions              | 0:10     |
| 9:15 PM    | 15     | Everyone Do: Unions                                | 0:15     |
| 9:30 PM    |        | END                                                |          |

---

### 1. Instructor Do: Welcome Class (5 min)

Welcome the students and explain that today's lesson will dive into data modeling techniques such as normalization, relationships, and how to conceptualize database design by using ERDs.

Open the slideshow and use the slides to explain the class objectives.

---

### 2. Instructor Do: Data Normalization (15 min)

**Corresponding Activity:** [01-Ins_Data_Normalization](Activities/01-Ins_Data_Normalization)

Continue the slideshow and use the slides on data normalization to explain the following:

* **Data normalization** is the process of restructuring data to a set of defined "normal forms."

* The process of data normalization eliminates data redundancy and inconsistencies.

* We will cover the three main forms of normalization. Note that additional forms of normalization exist.

* In **first normal form**, or 1NF, each field in a row contains a single value, and each row is unique.

* In this example, each vehicle's data is listed in a single row. You can normalize the data into 1NF by creating a new row for each service performed.

* In **second normal form**, or 2NF, the data is already in 1NF. Additionally, all non-key columns are dependent on the primary key for the table.

* There are three tables in this example. The Customer table, the Vehicle table, and the Services table each use unique identifiers as IDs.

* **Transitive dependency** is a column value's reliance on another column through a third column. The transitive property states that if A implies (⟹) B, and B implies C, then we can infer that A implies C. Dependence means that one value relies on another, such as city on ZIP code or age on birthday.

* Consider the following columns in the Vehicle table: `VIN`, `Customer`, `Model`, and `Make`. `Customer` depends on `VIN`, and `Model` depends on `Customer`. So, `Make` depends on `Model`.

* **Third normal form**, or 3NF, has the data normalized to the second normal form and contains non-transitively dependent columns.

* In 3NF, we break the Vehicle table data into three tables: Vehicle, Make, and Model. Each of these tables has a primary key column.

* The previous Customer table's `ID` column depends on the Vehicles table’s `Customer ID` column, while the Model table's `Make` column depends on the Make table's `ID` column.

Note that the students may find 3NF a bit confusing. Encourage them to learn more about 3NF on their own. This lesson focuses mainly on 1NF and 2NF.

Slack out [Normalization.md](Activities/01-Ins_Data_Normalization/Solved/Normalization.md) as a cheat sheet for the students before moving on.

---

### 3. Everyone Do: Pet Normalizer (15 min)

**Corresponding Activity:** [02-Evr_Data_Normalization](Activities/02-Evr_Data_Normalization)

The students will practice their data normalization skills using the provided data.

Use this section as a guide while you work with the students to solve the problem together as a class.

Open [pets.csv](Activities/02-Evr_Data_Normalization/Resources/pets.csv) and explain the first step of normalization:

* Make sure multiple data points are not included in the same column. For columns containing multiple pets, we need to create a new row for each pet.

* The final product will look like [pets_cleaned.csv](Activities/02-Evr_Data_Normalization/Solved/pets_cleaned.csv).

Next, open [schema.sql](Activities/02-Evr_Data_Normalization/Solved/schema.sql) in pgAdmin. Go over the code and explain the following:

* Second normal form requires the data to already be in first normal form. We accomplished this in the previous step.

* All non-ID columns are dependent on the primary key.

* The `owners` table is dependent on the primary key and displays each owner once.

* Next, we create a `pet_names` table, with each pet given a name and two IDs: one unique `id` for the pet itself and an `owner_id` that will link each pet to its correct owner.

* Each table has values that depend on the primary key and are not repeated in the other table.

* Finally, we can join the two tables by connecting the `owners` table on `id` and the `pet_names` table on `owner_id`.

Explain the bonus section of the activity:

* We create a `service` table and insert the data, each with a unique `service_type` and `id`.

* Next, we create a new `pets_name_new` table and add a `service_id` for each animal.

* We can then join all three tables to replicate a view of the cleaned CSV.

---

### 4. Instructor Do: Intro to Foreign Keys (15 min)

**Corresponding Activity:** [03-Ins_Foreign_Keys](Activities/03-Ins_Foreign_Keys)

Utilize the slides to cover foreign keys.

Use the slideshow to explain the concept of foreign keys and how they are used to connect tables:

* A foreign key is a link between tables. The foreign key in the first table points to, or is linked to, the primary key in a second table.

* A foreign key also prevents invalid data from being entered into a column. The data being entered MUST be a value from the referenced column.

Send out [schema_solution.sql](Activities/03-Ins_Foreign_Keys/Solved/schema_solution.sql) for students to follow along. Review the code and explain the following steps:

* Create a table named `animals_all` and set the primary key to `id`, which will be auto-populated and incremented with each new entry.

    ```sql
    CREATE TABLE animals_all (
      id SERIAL PRIMARY KEY,
      animal_species VARCHAR(30) NOT NULL,
      owner_name VARCHAR(30) NOT NULL
    );
    ```

* Insert data into the `animals_all` table, and then run a `SELECT` query to double-check that data has been inserted.

    ```sql
    INSERT INTO animals_all (animal_species, owner_name)
    VALUES
    ("Dog", "Bob"),
    ("Fish", "Bob"),
    ("Cat", "Kelly"),
    ("Dolphin", "Aquaman");

    SELECT * FROM animals_all;
    ```

* The result of this `SELECT` statement is captured in the following image:

    ![animals table](https://static.bc-edx.com/data/dl-1-2/m9/lessons/3/img/9-3-Foreign_Keys1.png)

* Point out that we have created a new table, and its primary key is labeled `id`. The `id` will be unique to this table.

* Next, we will create a new table named `animals_location`. The `FOREIGN KEY (animal_id)` identifies the `animal_id` column as a foreign key.

* After the foreign key has been identified, `REFERENCES animals_all(id)` tells the table that `animal_id` references, or is linked to, the `id` column in the `animals_all` table.

    ```sql
    CREATE TABLE animals_location (
    id SERIAL PRIMARY KEY,
    location VARCHAR(30) NOT NULL,
    animal_id INTEGER NOT NULL,
    FOREIGN KEY (animal_id) REFERENCES animals_all(id)
    );
    ```

* We then populate the table with data and check it with a `SELECT ALL` query. The resulting rows are captured in the following image:

    ![animals_location table](https://static.bc-edx.com/data/dl-1-2/m9/lessons/3/img/9-3-Foreign_Keys2.png)

* Point out that while we have created a new table, where the primary key is labeled `id`, the same as in the animals_all table, the `id` in animals_location is unique to this table and has no relation to the previously created table.

* Remind the students that we use `NOT NULL` for columns that require a value. In this case, we use it for the foreign key `animal_id` because all animal locations must reference a row in the `animals_all` table.

Recap the following:

* The `id` column is the primary key of the `animals_all` table, while `animal_id` is a foreign key in the `animals_location` table.

* Both the `id` column in `animals_all` and the `animal_id` in `animals_location` are designed to contain the same data (the ID), even though the names are different.

* SQL will throw an error if an attempt is made to change an `id` in one table but not the other.

* You need to name foreign key columns appropriately to clarify the data they are referring to.

Students should now understand how to create foreign keys and how to use them to reference data in other tables. Provide the following example to illustrate the importance of foreign keys:

* Foreign keys allow tables to be consistent and avoid issues caused by inserting, deleting, or updating one table without making those same changes in the other tables.

* When you attempt to insert a row into the `animals_location` table with an `animal_id` that does not exist as an `id` in the `animals_all` table, SQL will return an error.

    ```sql
    INSERT INTO animals_location (location, animal_id)
    VALUES ('River', 5);
    ```

* Explain that the `animal_id` column is a foreign key that is assigned to the `id` column in the `animals_all` table. The `id` 5 doesn't exist in the `animals_all` table and therefore can't be referenced in the `animals_location` table.

* Next, insert a new row into `animals_all` that will have an `id` of 5. Now a row can be inserted into `animals_location` with an `id` of 5 because it corresponds with an `id` in the `animals_all` table.

    ```sql
    INSERT INTO animals_all (animal_species, owner_name)
    VALUES
      ('Fish', 'Dave');

    INSERT INTO animals_location (location, animal_id)
    VALUES
      ('River', 5);
    ```

* Check that the row was inserted using a `SELECT * FROM animals_location` query. The following image captures the result of this `SELECT` statement, which includes the new row:

    ![Foreign keys 3](https://static.bc-edx.com/data/dl-1-2/m9/lessons/3/img/9-3-Foreign_Keys3.png)

Answer any questions students have about foreign keys. Then ask students if they can think of other real-world cases in which the use of foreign keys makes sense. Here are two examples:

* States and countries in addresses: Tell students to think back to the `rental` database, where streets, addresses, cities, and countries were stored in different tables. So, for example, if a change occurs to the address of a customer, all information across all tables would need to change. This is called maintaining the *referential integrity*.

* ID number of employees: In a database where the ID number of an employee is used in multiple tables, what happens if the employee's ID number changes? The ID number would need to change across all the tables that contain it.

Emphasize that using foreign keys to build relationships across data is a feature of relational databases.

---

### 5. Students Do: Foreign Keys (15 min)

**Corresponding Activity:** [04-Stu_Foreign_Keys](Activities/04-Stu_Foreign_Keys)

Using the next slides, instruct the students on how to create tables with foreign keys.

---

### 6. Review: Foreign Keys (5 min)

Send out the solution file to the students:

**File**: [schema_solution.sql](Activities/04-Stu_Foreign_Keys/Solved/schema_solution.sql)

Use the slideshow to review the activity.

Create a database `business_DB` to use with this activity.

Open `schema.sql` in pgAdmin and review the code while explaining the following steps:

* Create a table named `customer`.

    ```sql
    CREATE TABLE customer (
        id SERIAL,
        first_name VARCHAR(30) NOT NULL,
        last_name VARCHAR(30) NOT NULL,
        PRIMARY KEY (id)
    );
    ```

* This inserts only `first_name` and `last_name` as values because the `id` will automatically be added.

* Create a table named `customer_email`.

    ```sql
    CREATE TABLE customer_email (
        id SERIAL,
        email VARCHAR(30) NOT NULL,
        customer_id INTEGER NOT NULL,
        PRIMARY KEY (id),
        FOREIGN KEY (customer_id) REFERENCES customer(id)
    );
    ```

* The `customer_id` is a foreign key that references the `id` of the `customer` table. All data inserted must have an `id` that is in the `customer` table.

* We also create the `customer_phone` table which references the same column as its foreign key:

    ```sql
    CREATE TABLE customer_phone (
        id SERIAL,
        phone VARCHAR(30) NOT NULL,
        customer_id INTEGER NOT NULL,
        PRIMARY KEY (id),
        FOREIGN KEY (customer_id) REFERENCES customer(id)
    );
    ```

* This inserts data into the “customer_phone” table. Like the “customer_email” table, the `customer_id` is a foreign key that references the `id` of the “customer” table.

To test if we have the correct foreign keys, we can attempt to insert a value with an `id` of 10. To so, **uncomment** the code:

  ```sql
  -- INSERT INTO customer_phone(customer_id, phone)
  -- VALUES
    -- (10, '555-444-3333');
  ```

Then run the `INSERT` statement. Explain:

* Running this  `INSERT` statement returns an error because that `id` does not exist in the `customer` table.

Finally, explain that all tables can be joined together by their respective IDs.

---

### 7. Instructor Do: Intro to Data Relationships (15 min)

**Corresponding Activity:** [05-Ins_Data_Relationships](Activities/05-Ins_Data_Relationships)

Continue stepping through the slideshow to accompany this portion of the lesson.

Send out the following files so students can follow along during the demonstration:

**Files:**

* [schema.sql](Activities/05-Ins_Data_Relationships/Solved/schema.sql)

* [data_relationships.sql](Activities/05-Ins_Data_Relationships/Solved/data_relationships.sql)

Refer back to the slides. Explain that we will now cover one-to-one, one-to-many, and many-to-many relationships between data, which is an essential part of data modeling.

Begin by discussing one-to-one relationships. This example uses members of the Simpson family to illustrate the concept.

In a one-to-one relationship, each name is associated with one and only one Social Security number. In other words, each item in a column is linked to only one item from another column.

  ![Images/one-to-one.png](https://static.bc-edx.com/data/dl-1-2/m9/lessons/3/img/9-3-one-to-one.png)

Next, discuss one-to-many relationships. We'll continue with our Simpsons example, but we will add Sherlock Holmes and his sidekick, Watson, to the database.

  ![Images/one-to-many1.png](https://static.bc-edx.com/data/dl-1-2/m9/lessons/3/img/9-3-one-to-many1.png)

* This example has two tables. The first table lists only addresses. The second table lists each person's Social Security number and address.

* As before, one Social Security number is unique to one individual.

Each individual has one address, but a single address can be shared between multiple individuals. The Simpson family has a shared address at `742 Evergreen Terrace`, while Sherlock and Watson share the `221B Baker Street` address.

* In a one-to-many relationship, the data from one table can be repeated for items in another table.

* Ask students to think of other examples of real-life, one-to-many relationships.

* One example is a purchase order with a company that sells online. Each order has a unique identifying number. A customer might be associated with multiple orders, but each order is associated with one and only one customer.

Next, discuss many-to-many relationships. Continuing with our Simpsons example, we see there are three children (Lisa, Bart, and Maggie), and two parents (Homer and Marge).

  ![Images/many-to-many1.png](https://static.bc-edx.com/data/dl-1-2/m9/lessons/3/img/9-3-many-to-many1.png)

In this case, there are two tables: one for children and another for parents.

Each child here has multiple parents, and each parent has multiple children. So, each child has a separate row for each parent and vice versa.

  ![Images/many-to-many2.png](https://static.bc-edx.com/data/dl-1-2/m9/lessons/3/img/9-3-many-to-many2.png)

Explain that many-to-many relationships require a separate table, called a *junction table*, to show the relationships.

* Ask the class what many-to-many relationships might be found in an online retailer database such as one for Amazon.

* A customer can order many different items, and many different customers can order each item.

Demonstrate the creation of a junction table in Postgres. First, open [schema.sql](Activities/05-Ins_Data_Relationships/Solved/schema.sql) and paste in the queries to create and insert into the `children` and `parents` tables. There are two separate tables, as captured in the following screenshots:

  ![Images/modeling01.png](https://static.bc-edx.com/data/dl-1-2/m9/lessons/3/img/9-3-modeling01.png)

  ![Images/modeling02.png](https://static.bc-edx.com/data/dl-1-2/m9/lessons/3/img/9-3-modeling02.png)

Now go through the junction table schema:

  ```sql
  CREATE TABLE child_parent (
    child_id INTEGER NOT NULL,
    FOREIGN KEY (child_id) REFERENCES children(child_id),
    parent_id INTEGER NOT NULL,
    FOREIGN KEY (parent_id) REFERENCES parents(parent_id),
    PRIMARY KEY (child_id, parent_id)
  );
  ```

* The `child_id` and `parent_id` columns are both linked to the previously created tables as foreign keys.

* Additionally, the primary key in this table is a **composite key** comprised of both the `child_id` and `parent_id` keys. This means that the unique identifier for a row is not a single column but instead is the composite of both columns. Setting this as a primary key, instead of creating a separate primary key, ensures that we do not include duplicate pairs of ids from their referenced tables.

Show the junction table:

  ![Images/modeling03.png](https://static.bc-edx.com/data/dl-1-2/m9/lessons/3/img/9-3-modeling03.png)

Finally, go through the `JOIN` query to display the data in full:

  ![Images/modeling04.png](https://static.bc-edx.com/data/dl-1-2/m9/lessons/3/img/9-3-modeling04.png)

  ```sql
  SELECT children.child_name, child_parent_junction.child_id,
  parents.parent_name, child_parent_junction.parent_id
  FROM children
  LEFT JOIN child_parent_junction
  ON child_parent.child_id = children.child_id
  LEFT JOIN parents
  ON child_parent_junction.parent_id = parents.parent_id;
  ```

* The `children` table has a left join with the junction table, with the results having a left join with the `parents` table.

Take a moment to summarize the major points of the activity:

* Data can be modeled as one-to-one, one-to-many, and many-to-many relationships.

* Many-to-many relationships require a junction table.

* Junction tables use foreign keys to reference the keys in the original tables.

---

### 8. Students Do: Data Relationships (15 min)

**Corresponding Activity:** [06-Stu_Data_Relationships](Activities/06-Stu_Data_Relationships)

Use the slides to present the activity.

In this activity, we will create table schemata for the students and available courses. Next, we will create a junction table to display all courses taken by students.

---

### 9. Review: Data Relationships (5 min)

Use the slideshow to review the activity.

Send out the following solution files to the students:

**Files:**

* [schema_solution.sql](Activities/06-Stu_Data_Relationships/Solved/schema_solution.sql)

* [stu_data_relationships_solution.sql](Activities/06-Stu_Data_Relationships/Solved/stu_data_relationships_solution.sql)

Explain that this activity requires creating separate tables for students and courses, and then creating a junction table to reflect the many-to-many relationship between the two tables.

Paste in the schemata for the `students` and `courses` tables and explain the following:

* Each table is given the ID as the primary key.

* We add fields for the required attributes for the table.

* We populate the tables with the `INSERT` queries and then display the tables. The following images capture the tables that result from the data we inserted from the solved `schema.sql` file:

    ![Images/modeling05.png](https://static.bc-edx.com/data/dl-1-2/m9/lessons/3/img/9-3-modeling05.png)

    ![Images/modeling06.png](https://static.bc-edx.com/data/dl-1-2/m9/lessons/3/img/9-3-modeling06.png)

Next, do the same for the junction table, named `student_courses_junction`, and explain the following:

  ```sql
  -- Create a junction table.
  CREATE TABLE student_courses_junction (
    student_id INTEGER NOT NULL,
    FOREIGN KEY (student_id) REFERENCES students(id),
    course_id INTEGER NOT NULL,
    FOREIGN KEY (course_id) REFERENCES courses(id),
    course_term VARCHAR NOT NULL,
    PRIMARY KEY (student_id, course_id)
  );
  ```

* The table takes both a `student_id` and a `course_id`, which are references to the previously created tables.

* Since `student_id` and `course_id` reference those tables, they become the foreign key.

* New student or course data cannot be inserted into the `student_courses_junction` table if it does not currently exist in the `students` or `courses` tables.

* This table bridges the two previous tables and shows all courses taken by each student.

* The primary key will be a composite of both IDs.

* Additionally, this table includes a new field, `course_term`, which is the term in which a course was taken by a student.

Query the table to display the result, which is captured in the following image:

  ![Images/modeling07.png](https://static.bc-edx.com/data/dl-1-2/m9/lessons/3/img/9-3-modeling07.png)

To reinforce the many-to-many relationship, point out that many students can take many courses.

For the bonus, briefly explain that two left joins can be performed to retrieve complete data on each student.

  ```sql
  SELECT s.id, s.last_name, s.first_name, c.id, c.course_name, j.course_term
  FROM students s
  LEFT JOIN student_courses_junction j
  ON s.id = j.student_id
  LEFT JOIN courses c
  ON c.id = j.course_id;
  ```

The following image captures the result of this code:

  ![Images/modelingfpng](https://static.bc-edx.com/data/dl-1-2/m9/lessons/3/img/9-3-modeling08.png)

---

### 10. BREAK (15 min)

---

### 11. Instructor Do: Entity Relationship Diagrams (15 min)

**Corresponding Activity:** [07-Ins_ERD](Activities/07-Ins_ERD)

Use the next few slides to present this part of the lesson.

Send out the following files so the students can follow along during this demonstration:

**Files:**

* [pagila-erd.png](https://static.bc-edx.com/data/dl-1-2/m9/lessons/3/img/9-3-pagila-erd.png)

* [conceptual_schema.txt](Activities/07-Ins_ERD/Solved/conceptual_schema.txt)

* [logical_schema.txt](Activities/07-Ins_ERD/Solved/logical_schema.txt)

* [physical_schema.txt](Activities/07-Ins_ERD/Solved/physical_schema.txt)

Revisit the slideshow and begin the discussion of entity relationship diagrams (ERDs). Explain the following points:

* An **entity relationship diagram**, or **ERD**, is a visual representation of entity relationships within a database.

* ERDs use certain notation to describe different parts of the diagram: Boxes represent Entities; ovals represent Attributes; and lines represent Relationships. Lines will contain differences, such as branching out, that represent different relationships. ERDs can contain more complicated information, but the basics will be the same.

    ![ERD example](https://static.bc-edx.com/data/dl-1-2/m9/lessons/3/img/9-3-erd_diagram.png)

* ERDs are commonly interchanged with the term **data model**, as an ERD describes the relationships of tables within a database and therefore describes a model of a potential database.

* An ERD defines entities, their attributes, and data types, and illustrates the overall design of a database.

* There are three types of ERDs or data models: **conceptual**, **logical**, and **physical**. As the following image demonstrates, a conceptual data model is the simplest form, describing only entity names and relationships; a logical database model further expands upon the conceptual data model by additionally describing attributes or column names as well as primary and foreign key definitions; a physical data expands upon the logical data model to additionally include column data types and specific naming conventions.

  ![conceptual-vs-logical-vs-physical](https://static.bc-edx.com/data/dl-1-2/m9/lessons/3/img/9-3-conceptual-vs-logical-vs-physical.png)

* Logical and physical models will also display the cardinality of the tables, or the direction and number of relationships in that direction, such as one-to-one, one-to-many, and many-to-many.

To break down these concepts further, discuss the following example.

* In a database, the table is an *entity*; the data contained within the table are *attributes*; and the data type specified could be one of many things, such as booleans, integers, or varying characters.

* In an ERD, the relationships between entities, or tables, are given a visual representation. This allows clear and concise joins between tables and a deeper understanding of the data contained within a database as a whole.

* ERDs are used both to document existing databases and to aid in the creation of new databases.

Open [Quick Database Diagrams (Quick DBD)](https://app.quickdatabasediagrams.com/#/), send the link to the students so they can follow along, and briefly explain its components.

  **Note:** If this is the first time you are visiting the site, exit from the tour and clear the text on the left. If the site requires a sign-in, use your GitHub account.

* The pane on the left of the window is where users insert the text to create the entities of a database.

* The blue text signifies the name of the table containing the entities in a database.

* The white pane to the right is where the diagram displays, based on the text entered in the left pane.

    ![QDB-demo.png](https://static.bc-edx.com/data/dl-1-2/m9/lessons/3/img/9-3-QDB-demo.png)

* Once you finalized a diagram, you can export it in many formats from the **Export** tab at the top of the page.

    ![QDB-export.png](https://static.bc-edx.com/data/dl-1-2/m9/lessons/3/img/9-3-QDB-export.png)

    **Note**: If you export the diagram as **PostgreSQL**, the table schemata can be automatically generated, but note that the exported sql syntax will be slightly different than the traditional SQL syntax taught in these activities.

With the design tool open in your browser, demonstrate how to create a simple conceptual ERD using the following text:

  ```sql
  Employee
  -

  Zipcode
  -

  Employee_Email
  -

  Owners
  -

  Estates
  -

  Estate_Type
  -

  Agents
  -

  Regions
  -

  Agent_Region_Junction
  -
  ```

The result should appear as follows:

  ![conceptual-erd.png](https://static.bc-edx.com/data/dl-1-2/m9/lessons/3/img/9-3-conceptual-ERD.png)

  **Note**: You can move the tables by clicking and dragging them in the browser.

Explain to the class that the conceptual data model contains entities, but does not yet describe any entity relationships. To create the relationships between tables, we use the `rel <entity-name>` syntax to create abstract relationships between tables.

  ```sql
  Employee
  rel Zipcode
  -

  Zipcode
  -

  Employee_Email
  rel Employee
  -

  Owners
  -

  Estates
  rel Owners
  rel Estate_Type
  rel Zipcode
  -

  Estate_Type
  -

  Agents
  -

  Regions
  -

  Agent_Region_Junction
  rel Agents
  rel Regions
  -
  ```

The results should now appear as follows:

  ![conceptual-data-model-entities](https://static.bc-edx.com/data/dl-1-2/m9/lessons/3/img/9-3-conceptual-data-model-entities.png)

Explain that we will need to add entity attributes, or columns, to the diagram to transition from the conceptual ERD to a logical ERD. Using the following lines, update your current entities with columns by using the Quick Database Diagrams tool.

  ```sql
  Employee
  rel Zipcode
  -
  employee_id
  name
  age
  address
  zip_code

  Zipcode
  -
  zip_code
  city
  state

  Employee_Email
  rel Employee
  -
  email_id
  employee_id
  email

  Owners
  -
  owner_id
  first_name
  last_name

  Estates
  rel Owners
  rel Estate_Type
  rel Zipcode
  -
  estate_id
  owner_id
  estate_type
  address
  zip_code

  Estate_Type
  -
  estate_type_id
  estate_type

  Agents
  -
  agent_id
  first_name
  last_name

  Regions
  -
  region_id
  region_name

  Agent_Region_Junction
  rel Agents
  rel Regions
  -
  agent_id
  region_id
  ```

The result should appear as follows:

  ![logical-erd-column-names](https://static.bc-edx.com/data/dl-1-2/m9/lessons/3/img/9-3-logical-erd-column-names.png)

Explain that the data model now contains column names but is not yet a full-fledged logical data model because we have a bit more work to do:

* We need to continue to add in the foreign key relationships to represent the types of entity relationships in the diagram.

* Next, we define the primary keys for the tables. At this point, the `rel <entity-name>` syntax only describes abstract relationships between tables.

We can define primary and foreign keys in the online diagram tool by using the `PK` and `FK` syntax after the attribute names of a table.

  ```sql
  Employee
  -
  employee_id PK
  name
  age
  address
  zip_code FK
  ```

The following syntax points the foreign key definition to the specific column of another table.

  ```sql
  Employee
  -
  employee_id PK
  name
  age
  address
  zip_code FK - Zipcode.zip_code
  ```

In the line containing `FK -`, the hyphen signifies a one-to-one relationship between the `Employee` and `Zipcode` tables, where each ZIP code in the `Employee` table is linked to one ZIP code in the `Zipcode` table.

Many types of relationships between entities can be illustrated with various symbols.

  ```text
  - - one TO one
  -< - one TO many
  >-< - many TO many
  -0 - one TO zero or one
  0- - zero or one TO one
  0-0 - zero or one TO zero or one
  -0< - one TO zero or many
  >0- - zero or many TO one
  ```

As an example, the `Employee_Email` table has a many-to-one relationship with the `Employee` table via the common employee_id (an employee can have multiple email addresses). Therefore, the symbol describing the relationship is `>-`.

  ```sql
  Employee_Email
  -
  email_id PK
  employee_id FK >- Employee.employee_id
  email
  ```

The complete schema for the logical data model should be as follows:

  ```sql
  Employee
  -
  employee_id PK
  name
  age
  address
  zip_code FK - Zipcode.zip_code

  Zipcode
  -
  zip_code PK
  city
  state

  Employee_Email
  -
  email_id PK
  employee_id FK >- Employee.employee_id
  email

  Owners
  -
  owner_id PK
  first_name
  last_name

  Estates
  -
  estate_id PK
  owner_id FK - Owners.owner_id
  estate_type FK - Estate_Type.estate_type_id
  address
  zip_code FK - Zipcode.zip_code

  Estate_Type
  -
  estate_type_id PK
  estate_type

  Agents
  -
  agent_id PK
  first_name
  last_name

  Regions
  -
  region_id PK
  region_name

  Agent_Region_Junction
  -
  agent_id FK >- Agents.agent_id
  region_id FK >- Regions.region_id
  ```

In addition, with the added primary keys and foreign key relationships, the diagram should now look like the following image.

  ![logical-erd.png](https://static.bc-edx.com/data/dl-1-2/m9/lessons/3/img/9-3-logical-ERD.png)

To transition the logical data model to a physical data model, we'll add data types to each of the columns. Using the following lines, update your current entities with data types using the Quick Database Diagrams tool.

```sql
# Physical

Employee
-
employee_id INT PK
name VARCHAR(255)
age INT
address VARCHAR(255)
zip_code INT FK - Zipcode.zip_code

Zipcode
-
zip_code INT PK
city VARCHAR(255)
state VARCHAR(255)

Employee_Email
-
email_id INT PK
employee_id INT FK >- Employee.employee_id
email VARCHAR(255)

Owners
-
owner_id INT PK
first_name VARCHAR(255)
last_name VARCHAR(255)

Estates
-
estate_id INT PK
owner_id INT FK - Owners.owner_id
estate_type VARCHAR(255) FK - Estate_Type.estate_type_id
address VARCHAR(255)
zip_code INT FK - Zipcode.zip_code

Estate_Type
-
estate_type_id VARCHAR(255) PK
estate_type VARCHAR(255)

Agents
-
agent_id INT PK
first_name VARCHAR(255)
last_name VARCHAR(255)

Regions
-
region_id INT PK
region_name VARCHAR(255)

Agent_Region_Junction
-
agent_id INT FK >- Agents.agent_id
region_id INT FK >- Regions.region_id
```

Point out that the diagram is very similar to the logical data model. However, the diagram now lists data types and shows more relationships, such as `region_id`'s many-to-one relationship with `Regions.region_id`.

  ![physical-erd.png](https://static.bc-edx.com/data/dl-1-2/m9/lessons/3/img/9-3-physical-erd.png)

If students need a refresher on data relationships, direct them to the documentation on the Quick Database Diagrams website following these steps.

Click the Docs tab at the top of the page.

  ![docs.png](https://static.bc-edx.com/data/dl-1-2/m9/lessons/3/img/9-3-docs.png)

Select Relationships from the dropdown menu. This pane provides an explanation of relationships and their symbols.

  ![relationships.png](https://static.bc-edx.com/data/dl-1-2/m9/lessons/3/img/9-3-relationships.png)

Send out [pagila-erd.png](https://static.bc-edx.com/data/dl-1-2/m9/lessons/3/img/9-3-pagila-erd.png) to the class and open it on your computer. Point out how each table has a connection to at least one other table. For example:

* The `customer` and `customer_list` tables both contain `customer id` values.

* The `customer` table and `staff` table both contain `staff id` values.

Understanding where and how entities are related allows developers to create more cohesive join operations.

---

### 12. Everyone Do: Designing an ERD, Part 1 (10 min)

**Corresponding Activity:** [08-Evr_Designing_ERD](Activities/08-Evr_Designing_ERD)

Continue the slideshow to present this activity.

In this scenario, students will create a conceptual ERD for a gym owner.

Use this section as a guide while you work with the students to solve the problem together as a class.

Open the [Quick Database Diagrams (Quick DBD)](https://app.quickdatabasediagrams.com/#/) webpage and demonstrate the solution, using the code in the `schema.txt` file. Live code while explaining the following:

* A conceptual diagram contains only basic information, such as the names of the tables and their attributes.

* The output generated via creating a diagram looks similar to when we write code. For example, in the following image, `Gym` followed by the hyphen creates the table name within the diagram.

    ```sql
    Gym
    -
    ID INTEGER PK
    Gym_Name VARCHAR
    Address VARCHAR
    City VARCHAR
    Zipcode VARCHAR
    ```

* Transitioning a conceptual diagram to a logical diagram requires more information. We define data types and establish primary keys by adding ID rows to the tables, such as in the `Trainers` table:

    ```sql
    Trainers
    -
    ID INTEGER PK
    First_Name VARCHAR
    Last_Name VARCHAR
    ```

    **Note**: Remember that the `PK` acronym stands for primary key.

Copy and paste the remaining text from `schema.txt` to create the additional tables. The final product should appear as follows:

  ![The logical ERD for the gym ](https://static.bc-edx.com/data/dl-1-2/m9/lessons/3/img/9-3-logical_gym_erd.png)

Ask the students if they created any other tables or connections, as there are many possible solutions in addition to those included here.

Answer any questions before moving on.

---

### 13. Everyone Do: Designing an ERD, Part 2 (10 min)

**Corresponding Activity:** [09-Evr_ERD](Activities/09-Evr_ERD)

Continue the slideshow to present this activity.

In this activity, the students will further improve on the ERD by creating a physical ERD.

Use this section as a guide while you work with the students to solve the problem together as a class.

Open the [Quick Database Diagrams (Quick DBD)](https://app.quickdatabasediagrams.com/#/) webpage. Copy and paste the solution using the code in the `schema_solution.txt` file and explain the following:

* Transitioning a logical ERD to a physical ERD involves adding appropriate entities to tables and mapping their relationships.

* For example, in the `Members` table, we added several rows to demonstrate data relationships. We added a row named `Gym_ID` as a foreign key (`FK`), establishing a one-to-many relationship by using the `>-` symbol.

* We also created a row containing the `Trainer_ID` to demonstrate the one-to-many relationship between the members and trainers. While one member will have no more than one trainer, one trainer may instruct many members.

    ```sql
    Gym_ID INTEGER FK >- Gym.Gym_ID
    Trainer_ID INTEGER FK >- Trainers.Trainer_ID
    ```

* The `Trainers` table also has a one-to-many relationship (`>-`), which we created by adding a `Gym_ID` row to the table. While a trainer will be employed at a single gym, the gym will employ many trainers.

    ```sql
    Gym_ID INTEGER FK >- Gym.Gym_ID
    ```

* In the `Payments` table, we demonstrate a one-to-one relationship (`-`) by adding a `Member_ID` row and linking it to the `Members` table.

    ```sql
    Member_ID INTEGER FK - Members.Member_ID
    ```

* Export the schema  in PostgreSQL format and open it in VS Code.

Return to pgAdmin in the browser and create a new database called `gym`.

* Open a query tool and paste in the newly downloaded SQL code to create the tables defined in the diagram.

* Execute the code, and then check the table creation using a `SELECT` statement for each table.

    ```sql
    SELECT * FROM Trainers;
    SELECT * FROM Members;
    SELECT * FROM Gym;
    SELECT * FROM Payments;
    ```

Answer any questions before moving on.

---

### 14. Instructor Do: Introduction to Unions (10 min)

**Corresponding Activity:** [10-Ins_Unions](Activities/10-Ins_Unions)

Present this portion of the lesson by continuing through the slideshow.

**Note:** Unions are perhaps a less crucial topic than some others covered in this lesson, so adjust the timing as you see fit.

For this first example, we will once again use the `pagila` database.

Remind the students that when we perform joins, we bring columns from separate tables side by side.

Explain that we can also stack data vertically through an operation called `UNION`.

Demonstrate how to get results from two tables without using joins.The process requires running two different queries:

  ```sql
  SELECT actor_id AS id, first_name
  FROM actor
  WHERE actor_id between 1 and 5;
  ```

  ```sql
  SELECT customer_id AS id, first_name
  FROM customer
  WHERE customer_id between 6 and 10;
  ```

Explain that with unions these two queries can be combined. Demonstrate a simple union with the following code:

  ```sql
  SELECT actor_id AS id, first_name
  FROM actor
  WHERE actor_id between 1 and 5

  UNION

  SELECT customer_id AS id, first_name
  FROM customer
  WHERE customer_id between 6 and 10;
  ```

  ![union](https://static.bc-edx.com/data/dl-1-2/m9/lessons/3/img/9-3-Union1.png)

Explain that, by default, Postgres excludes duplicate entries from the result. Run the [schema.sql](Activities/10-Ins_Unions/Solved/schema.sql) in pgAdmin to load the example. Then run the following to show two separate queries:

  ```sql
  -- Union of toys and game types
  SELECT toy_id AS id, type
  FROM toys;
  ```

  ```sql
  SELECT game_id AS id, type
  FROM games;
  ```

Then run `UNION` to show combined results.

  ```sql
  -- Union of toys and game types
  SELECT toy_id AS id, type
  FROM toys

  UNION

  SELECT game_id AS id, type
  FROM games;
  ```

Explain that there are only four rows of data because the duplicates that fit the criteria are dropped. In cases where we want to display all duplicate entries, we can use the keywords `UNION ALL`.

  ```sql
  -- Include duplicate rows
  SELECT toy_id AS id, type
  FROM toys

  UNION ALL

  SELECT game_id AS id, type
  FROM games;
  ```

Answer any questions before moving on to the activity.

---

### 15. Everyone Do: Unions (15 min)

**Corresponding Activity:** [11-Evr_Unions](Activities/11-Evr_Unions)

Use the slides to introduce this activity.

This activity will allow the students to practice with unions by combining data from multiple tables without the use of joins.

Use this section as a guide while you work with the students to solve the problem together as a class.

The first problem simply requires the union of the `COUNT` of rows from `city` and `country`.

  ```sql
  SELECT COUNT(*)
  FROM city
  UNION
  SELECT COUNT(*)
  FROM country;
  ```

The second problem requires a bit more work. In the proposed solution, customer IDs from the `customer` and `customer_list` tables are brought together with `UNION ALL`.

  ```sql
  SELECT customer_id
  FROM customer
  WHERE address_id IN
  (
    SELECT address_id
    FROM address
    WHERE city_id IN
    (
      SELECT city_id
      FROM city
      WHERE city = 'London'
    )
  )
  UNION ALL
  SELECT id
  FROM customer_list
  WHERE city = 'London';
  ```

* We can narrow Customer IDs from `customer_list` with `WHERE city = 'London'`.

* To retrieve customer IDs from the `customer` table, perform subqueries across `address` and `city` tables.

---

© 2022 edX Boot Camps LLC. Confidential and Proprietary. All Rights Reserved.
