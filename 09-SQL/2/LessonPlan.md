## 9.2: Advanced SQL Queries

### Overview

This lesson will introduce the students to additional features of the SQL language. The students will dive deeper into queries with aggregates, grouping, and ordering. Today's lesson will also cover subqueries, creating views, and how to combine both features.

### Class Objectives

By the end of today's class, the students will be able to:

* Create aggregate queries.

* Create subqueries to explore data further.

* Create views and run subqueries off of them.

---

### Instructor Notes

Today's lesson will mostly use imported datasets, so make sure students are comfortable importing data from CSV files. All schemas for the tables will be provided along with the CSV files. Students who don't have this data imported correctly will not be able to follow along with the lesson.

This lesson will build on what students learned in the previous class, and each activity will combine multiple SQL elements. Students who are new to SQL may struggle a bit, but many of the concepts are similar to those they have learned previously.

The TAs should be ready to help the students who are confused or who have not imported the data correctly.

---

### Class Slides

The slides for this lesson can be viewed on Google Drive here: [Lesson 9.2 Slides](https://docs.google.com/presentation/d/1CwQP2dKYZUkvG81Kbwva4s79ELukvJe7K52AnhygzGA/edit?usp=sharing).

To add the slides to the student-facing repository, download the slides as a PDF by navigating to File, selecting "Download as," and then choosing "PDF document." Then, add the PDF file to your class repository along with other necessary files. You can view instructions for this [here](https://docs.google.com/document/d/1XM90c4s9XjwZHjdUlwEMcv2iXcO_yRGx5p2iLZ3BGNI/edit).

**Note:** Editing access is not available for this document. If you wish to modify the slides, create a copy by navigating to File and selecting "Make a copy...".

---

### Time Tracker

| Start Time | Number | Activity                                           | Duration |
| ---------- | ------ | -------------------------------------------------- | -------- |
| 6:30 PM    | 1      | Instructor Do: Welcome Class                       | 0:05     |
| 6:35 PM    | 2      | Instructor Do: Import Data                         | 0:15     |
| 6:50 PM    | 3      | Instructor Do: Aggregate Functions, Aliases, and Grouping | 0:10     |
| 7:00 PM    | 4      | Students Do: Gregarious Aggregates                 | 0:15     |
| 7:15 PM    | 5      | Review: Gregarious Aggregates                      | 0:05     |
| 7:20 PM    | 6      | Instructor Do: Order By Aggregates                 | 0:10     |
| 7:30 PM    | 7      | Students Do: Movies Ordered By                     | 0:15     |
| 7:45 PM    | 8      | Review Movies Ordered By                           | 0:05     |
| 7:50 PM    | 9      | BREAK                                              | 0:15     |
| 8:05 PM    | 10     | Instructor Do: Introduction to Subqueries          | 0:10     |
| 8:15 PM    | 11     | Students Do: Subqueries                            | 0:15     |
| 8:30 PM    | 12     | Review: Subqueries                                 | 0:05     |
| 8:35 PM    | 13     | Instructor Do: Create Views                        | 0:10     |
| 8:45 PM    | 14     | Partner Do: A View with a Roomful of Queries       | 0:15     |
| 9:00 PM    | 15     | Review: A View with a Roomful of Queries           | 0:05     |
| 9:05 PM    | 16     | Instructor Do: Revisit Subqueries                  | 0:10     |
| 9:15 PM    | 17     | Students Do: Mine the Subquery                     | 0:10     |
| 9:25 PM    | 18     | Review: Mine the Subquery                          | 0:05     |
| 9:30 PM    |        | END                                                |          |

---

### 1. Instructor Do: Welcome Class (5 min)

Open the slideshow and welcome the students to class.

Explain that today's lesson will provide a more in-depth look at SQL's features. Students will work with imported tables to expand their SQL skills.

---

### 2. Instructor Do: Import Data (15 min)

**Corresponding Activity:** [01-Evr_Import_Data](Activities/01-Evr_Import_Data)

Continue through the slideshow.

Explain to the class that today's activities will require the students to import a few tables into a database. The data is taken from a popular [MySQL Database](https://dev.mysql.com/doc/sakila/en/). There is [another database](https://github.com/devrimgunduz/pagila) that is similar to Sakila, but it uses PostgreSQL. The students have two options for importing the tables. If anyone has issues with the schema option, direct them to the CSV option.

Compress the `Resources` folder and send it out to the class. This folder contains everything students need to upload the data.

#### Schema Option

Go through the following steps:

* From pgAdmin, create a database named `rental_db`.

* Open the Query Tool for the newly created `rental_db`.

* Copy [pagila-schema.sql](Activities/01-Evr_Import_Data/Resources/pagila-schema.sql) and run the code to create the needed tables.

* Copy [pagila-insert-data.sql](Activities/01-Evr_Import_Data/Resources/pagila-insert-data.sql). **Note:** This will take a few minutes due to the amount of data. As long as no errors pop up, the data will be uploaded.

If any students have issues uploading data this way, have them follow the CSV option.

#### CSV Option

Go through the following steps:

* From pgAdmin, create a database named `rental_db`.

* Open the Query Tool for the newly created `rental_db`.

* Copy [schema.sql](Activities/01-Evr_Import_Data/Resources/schema.sql) and run the code to create the needed tables.

* Right-click the **actor** table on the right-hand side, and then select **Import/Export**.

* Import `actor.csv`.

* Run `SELECT * FROM actor LIMIT 100;` to confirm that the import was successful.

    Optional: Right-click the **actor** table and view the first 100 rows to check that the data was imported correctly.

* Have the class repeat this process for the remaining tables.

While the data is being uploaded, the TAs should ask if any students need assistance with the upload process.

---

### 3. Instructor Do: Aggregate Functions, Aliases, and Grouping (10 min)

**Corresponding Activity:** [02-Ins_Aggregates](Activities/02-Ins_Aggregates)

Continue stepping through the slides to review the following:

* Similar to aggregates in Pandas, aggregate functions allow calculations on a set of values and return a singular value.

* Some of the most commonly used aggregates are `AVG`, `COUNT`, `MIN`, `MAX`, and `SUM`.

* Aggregates are often combined with `GROUP BY`, `HAVING`, and `SELECT`.

**File:** [aggregates_solution.sql](Activities/02-Ins_Aggregates/Solved/aggregates_solution.sql)

Select the `rental_db` database in pgAdmin and open a Query window.

Run `SELECT * FROM film;` and count the number of rows.

Run `SELECT COUNT(film_id) FROM film;` and explain the following:

* Using `COUNT()` is an easier way to count the rows.

* The `COUNT()` function is an aggregate.

    ![Count](https://static.bc-edx.com/data/dl-1-2/m9/lessons/2/img/9-2-Count.png)

Now that the number of `film_id` entries has been counted, it's easy to see a total of 1,000 films.

Note that the name of the field returned is `count bigint`, which doesn't describe the column accurately. Postgres has a way to change the column names and make them more descriptive.

Run the following:

  ```sql
  SELECT COUNT(film_id) AS "Total films"
  FROM film;
  ```

Explain the following:

* `AS 'Total films'` is a technique called *aliasing*.

* Aliasing creates an `alias`, or a new name, for the column.

* Using an alias does not change the table or the database in any way. Aliasing provides a convenient way to view a column or to create shortcuts for columns or other data.

    ![Total](https://static.bc-edx.com/data/dl-1-2/m9/lessons/2/img/9-2-Total.png)

The `COUNT()` function lets you know the number of movies, but it isn't informative enough when searching for the number of specific ratings, like G or PG-13. This is where `GROUP BY` comes into play.

Run the following code:

  ```sql
  SELECT rating, COUNT(film_id) AS "Total films"
  FROM film
  GROUP BY rating;
  ```

Explain the following:

* The `GROUP BY` method will first group by the column indicated.

* Aggregates are used to get the values for any columns not included in the `GROUP BY` clause.

* Here, the `COUNT()` function will count the `film_id` for each `rating`.

    ![Ratings](https://static.bc-edx.com/data/dl-1-2/m9/lessons/2/img/9-2-Ratings.png)

Explain that we can aggregate data in other ways besides counting. For example, *sum*, *average*, *min*, and *max* are all valid aggregate functions to apply to the data.

Ask the class how to query the average rental period for *all* movies. To demonstrate this, run the following query:

  ```sql
  SELECT AVG(rental_duration)
  FROM film;
  ```

To demonstrate how to add an alias to the `AVG()` function, run the following:

  ```sql
  SELECT AVG(rental_duration) AS "Average rental period"
  FROM film;
  ```

Put it all together by running the following query, showing how to `GROUP BY` rental duration, get the average `rental_rate`, and give it an alias.

  ```sql
  SELECT  rental_duration, AVG(rental_rate) AS "Average rental rate"
  FROM film
  GROUP BY rental_duration;
  ```

  ![Aggregate1](https://static.bc-edx.com/data/dl-1-2/m9/lessons/2/img/9-2-Aggregate1.png)

Ask a student to explain the query.

* Movies that can be rented for three days cost an average of $2.82 to rent. Movies that can be rented for four days cost an average of $2.97 to rent, and so on.

SQL can also return the rows that contain the minimum values and maximum values in a column using `MIN()` and `MAX()` respectively.

  ```sql
  -- Find the rows with the minimum rental rate
  SELECT  rental_duration, MIN(rental_rate) AS "Min rental rate"
  FROM film
  GROUP BY rental_duration;

  -- Find the rows with the maximum rental rate
  SELECT  rental_duration, MAX(rental_rate) AS "Max rental rate"
  FROM film
  GROUP BY rental_duration;
  ```

Mention that these aggregate functions calculate and retrieve data, but they do not *alter* the data. That is, they do not modify the database.

Explain that there are many other aggregate functions students can research. Send out [Postgres functions](https://www.tutorialspoint.com/postgresql/postgresql_useful_functions.htm) to the class for future reference.

---

### 4. Students Do: Gregarious Aggregates (15 min)

**Corresponding Activity:** [03-Stu_GregariousAggregates](Activities/03-Stu_GregariousAggregates)

Use the next few slides to go over this activity, where the students will practice writing queries with aggregate functions, with grouping, and with using aliases.

---

### 5. Review: Gregarious Aggregates (5 min)

Use the slideshow to review the activity.

**File**: [gregarious_aggregates_solution.sql](Activities/03-Stu_GregariousAggregates/Solved/gregarious_aggregates_solution.sql)

Review the solution in pgAdmin and explain the following:

* Postgres uses double quotes for table and column names and single quotes for string constants.

* `GROUP BY` is similar to the `groupby` operation in Pandas.

* `SELECT` without aggregates can only choose the columns in the `GROUP BY` clause.

Answer any questions before moving on.

---

### 6. Instructor Do: Order By Aggregates (10 min)

**Corresponding Activity:** [04-Ins_Order_By](Activities/04-Ins_Order_By)

Use the slides to help you demonstrate this module.

Explain that aggregate functions return the results in a random order. This can make it difficult to find the first and last or smallest and largest numerical results.

Open pgAdmin and explain the following:

* Postgres has a function called `ORDER BY` that will solve this issue. We add `ORDER BY` toward the end of a query and, by default, it will sort the results by ascending values.

    ```sql
    SELECT rental_rate, AVG(length) AS "avg length"
    FROM film
    GROUP BY rental_rate
    ORDER BY "avg length";
    ```

* Postgres will add a lot of numbers after the decimal. To reduce the numbers after the decimal, use `ROUND()`. This takes the parameters `ROUND(<value>, <number of decimal places>)`, which rounds the value down to the specified number of decimal places.

    ```sql
    SELECT rental_rate, ROUND(AVG(length),2) AS "avg length"
    FROM film
    GROUP BY rental_rate
    ORDER BY "avg length";
    ```

* The `ORDER BY` statement organizes by descending values if you add `DESC`.

    ```sql
    SELECT rental_rate, ROUND(AVG(length),2) AS "avg length"
    FROM film
    GROUP BY rental_rate
    ORDER BY "avg length" DESC;
    ```

* Top results can also be taken by limiting the amount returned using `LIMIT`.

    ```sql
    SELECT rental_rate, ROUND(AVG(length),2) AS "avg length"
    FROM film
    GROUP BY rental_rate
    ORDER BY "avg length" DESC
    LIMIT 5;
    ```

Answer any questions before moving on.

---

### 7. Students Do: Movies Ordered By (15 min)

**Corresponding Activity:** [05-Stu_Order_By](Activities/05-Stu_Order_By)

Use the slideshow to introduce this activity. You will use `ORDER BY` in combination with other SQL methods to query and order the tables.

---

### 8. Review Movies Ordered By (5 min)

**File:** [movies_ordered_by_solution.sql](Activities/05-Stu_Order_By/Solved/movies_ordered_by_solution.sql)

Utilize the slides to review the activity.

Open pgAdmin and demonstrate the solution, highlighting the following:

* We group the `actor` table by `first_name`, with an aggregate taking the count, and then we create an alias of `actor count`. Then we order the query in descending order by the count.

* Use the `ROUND` function to limit the results to two decimal places.

* Add `LIMIT 10` to the end of the query to return the top 10 results.

* For the bonus, a `JOIN` is needed to combine the `country` and `city` tables. We can then group and aggregate the return of the join. Finally, we sort the result by the count of countries in descending order.

---

### 9. BREAK (15 min)

---

### 10. Instructor Do: Introduction to Subqueries (10 min)

**Corresponding Activity:** [06-Ins_Subqueries](Activities/06-Ins_Subqueries)

Continue the slideshow to begin the discussion of subqueries. Explain that a **subquery** is nested inside a larger query.

Explain that there is often more than one way of accomplishing a task in SQL.

For example, suppose we want to view the inventory of a film called *Early Home*. One way to do this is to run several queries in succession. In the first query, we can search by the title and obtain its `film_id` number.

  ```sql
  SELECT title, film_id
  FROM film
  WHERE title = 'EARLY HOME';
  ```

* The `film_id` is 268. We can use this information to search for data in the `inventory` table:

    ```sql
    SELECT *
    FROM inventory
    WHERE film_id = 268;
    ```

    ![Subquery](https://static.bc-edx.com/data/dl-1-2/m9/lessons/2/img/9-2-subquery.png)

* There are two copies of this movie as indicated by two separate `inventory_id` numbers. Both are located in store number 2.

At this point, ask the class whether it might be possible to join these two queries into a single query. Then run the following query:

  ```sql
  SELECT i.inventory_id, i.film_id, i.store_id
  FROM inventory i
  JOIN film f
  ON (i.film_id = f.film_id)
  WHERE f.title = 'EARLY HOME';
  ```

The class should now begin to feel more comfortable with joins. Explain that we can retrieve the same information in a different way, using a tool called a subquery. Type the following query:

  ```sql
  SELECT *
  FROM inventory
  WHERE film_id IN
  (
    SELECT film_id
    FROM film
    WHERE title = 'EARLY HOME'
  );
  ```

This may look a bit confusing or intimidating at first. Start with the inner query:

  ```sql
  SELECT film_id
  FROM film
  WHERE title = 'EARLY HOME';
  ```

* This query will return a `film_id` of 268.

* The next (outer) query is now querying from the results of the inner query.

* A helpful way to think about this is that the inner query is creating a one-time temporary table, and the outer query is selecting from that temporary table.

To confirm the result is correct, plug 268 (the result of the subquery) into the parentheses to replace the subquery.

  ```sql
  SELECT *
  FROM inventory
  WHERE film_id IN (268);
  ```

This will get the same result as the previous join.

  ![subquery](https://static.bc-edx.com/data/dl-1-2/m9/lessons/2/img/9-2-subquery.png)

We have simplified the query by first running the nested subquery and then by plugging the results into the outer query.

Explain that Postgres doesn't necessarily run code in that order, but it helps us to reduce subqueries to basic queries as building blocks.

Send out this [link](https://sqlbolt.com/lesson/select_queries_order_of_execution), which explains the order of execution in SQL queries.

Mention that although we can often accomplish the same task using either joins or subqueries, joins tend to be faster.

Note that we used `SELECT *` in this activity. While it is fine to use the asterisk wildcard to return data for every column in a table during exploration, in production code, it is standard practice to specify the fields.

Answer any questions before moving on.

---

### 11. Students Do: Subqueries (15 min)

**Corresponding Activity:** [07-Stu_Subqueries](Activities/07-Stu_Subqueries)

Use the slides to give directions for this activity, in which the students will practice creating subqueries.

---

### 12. Review: Subqueries (5 min)

**File:** [stu_subqueries_solution.sql](Activities/07-Stu_Subqueries/Solved/stu_subqueries_solution.sql)

Use the slides to review the activity.

Review the solution in pgAdmin and explain the following:

* In the first query, we're seeking the name and ID number of cities from a given list:

    ```sql
    SELECT city, city_id
    FROM city
    WHERE city IN ('Qalyub', 'Qinhuangdao', 'Qomsheh', 'Quilmes');
    ```

* The second query is a subquery to select the `district`.

* This query will select the `district` where `city_id` is in the results from the first query.

    ```sql
    SELECT district
    FROM address
    WHERE city_id IN
    (
      SELECT city_id
      FROM city
      WHERE city IN ('Qalyub', 'Qinhuangdao', 'Qomsheh', 'Quilmes')
    );
    ```

* Because `district` is not available in the `city` table, we have to use the `city_id` from the `city` table. The `city_id` will now allow a connection between `district` and `city`.

* The bonus adds another level of subqueries. It requires querying information from the `city` table and then querying the `address` table. We can use that information to query the `customer` table.

    ```sql
    SELECT first_name, last_name
    FROM customer cus
    WHERE address_id IN
    (
      SELECT address_id
      FROM address a
      WHERE city_id IN
      (
        SELECT city_id
        FROM city
        WHERE city LIKE 'Q%'
      )
    );
    ```

---

### 13. Instructor Do: Create Views (10 min)

**Corresponding Activity:** [08-Ins_Create_Views](Activities/08-Ins_Create_Views)

Continue stepping through the slides to begin the discussion of views. Explain that a *view* in SQL is a virtual table that can be created from a single table, multiple tables, or another view.

This activity will be a pleasant interlude from some of the heavy lifting we have been doing in Postgres. It is not crucial, so feel free to tweak the length and content as you deem appropriate.

Up to this point, we have seen relatively long queries, especially those that involve joins and subqueries. There is a way to save a long query under a name and run that name as a shortcut.

Send out the following query and ask the students run it:

  ````sql
  SELECT s.store_id, SUM(amount) AS Gross
  FROM payment AS p
    JOIN rental AS r
    ON (p.rental_id = r.rental_id)
      JOIN inventory AS i
      ON (i.inventory_id = r.inventory_id)
        JOIN store AS s
        ON (s.store_id = i.store_id)
        GROUP BY s.store_id;
  ````

The query is used to monitor the total sales from each store, which is something a company executive would want to look up often. Notice that we use an alias to narrow table names down to a single letter. Instead of having to type this query, we can store it under a `view`:

  ```sql
  CREATE VIEW total_sales AS
  SELECT s.store_id, SUM(amount) AS Gross
  FROM payment AS p
  JOIN rental AS r
  ON (p.rental_id = r.rental_id)
    JOIN inventory AS i
    ON (i.inventory_id = r.inventory_id)
      JOIN store AS s
      ON (s.store_id = i.store_id)
      GROUP BY s.store_id;
  ```

Point out that the query is identical to the one above, except for the first line:

  ```sql
  CREATE VIEW total_sales AS
  ```

A `view` is created under the name `total_sales`. Created views are located on the left sidebar in pgAdmin.

  ![views](https://static.bc-edx.com/data/dl-1-2/m9/lessons/2/img/9-2-views.png)

The rest of the query follows `AS`.

Run the query. To execute this view, type the following:

  ```sql
  SELECT *
  FROM total_sales;
  ```

Simple! Ask a student to guess how we might delete a view.

  ```sql
  DROP VIEW total_sales;
  ```

For the remainder of the activity, have students create and drop their views.

---

### 14. Partner Do: A View with a Roomful of Queries (15 min)

**Corresponding Activity:** [09-Stu_View_Room_Queries](Activities/09-Stu_View_Room_Queries)

Using the slides, explain this activity, where the students will pair up and practice their join and subquery skills, as well as build out a view.

---

### 15. Review: A View with a Roomful of Queries (5 min)

**File:** [roomful_of_queries_solution.sql](Activities/09-Stu_View_Room_Queries/Solved/roomful_of_queries_solution.sql)

Use the slideshow to review the activity.

Review the code and explain the following:

* Two pieces of information are required in the query: (1) the title of a film and (2) the number of copies of the title in the system.

    ```sql
    SELECT title,
    (SELECT COUNT(inventory.film_id)
      FROM inventory
      WHERE film.film_id = inventory.film_id ) AS "Number of Copies"
    FROM film;
    ```

* Add `CREATE VIEW title_count AS` before the above query to create a view for the results.

* We can now query the newly created table view, `title_count`, to find which titles have 7 copies in the inventory.

    ```sql
    SELECT title, "Number of Copies"
    FROM title_count
    WHERE "Number of Copies" = 7;
    ```

---

### 16. Instructor Do: Revisit Subqueries (10 min)

**Corresponding Activity:** [10-Ins_Revist_Subquery](Activities/10-Ins_Revist_Subquery)

Continue the slideshow.

Up to this point, the subqueries we've seen have been relatively straightforward. In this activity, we will look at more complicated examples, but you can tell students not to worry. We can perform complexly nested subqueries using the same principles that we've already covered.

We begin with a question: How many people have rented the film *Blanket Beverly*?

To answer this question systematically, we must first identify the tables needed for our query by using an entity relationship diagram (ERD).

Send out the [ERD](http://www.postgresqltutorial.com/postgresql-sample-database/) link to the class. Tell the students to scroll down to the **DVD Rental ER Model**, and then explain the following:

* An ERD shows the connections between the tables.

* The schema makes it easier to identify the tables we need and the keys we will use to link our subqueries.

* We will dive deeper into these in the next lesson.

Tell students that we need to start with the table `customer` and end with the table `film`, since we are counting how many customers have rented this specific film.

Ask the class which tables and keys will serve as the intermediaries, or bridges, between these two tables. Then explain the following:

* Start with the `customer` table and examine its keys. A good place to look is the primary key, which in this table is `customer_id`.

* The `customer` table has a relationship with the `payment` table, which also contains the `customer_id`.

Begin a class discussion to determine how to formulate the rest of the subquery using the ERD. One solution could be the following:

* Connect the `payment` table with the `rental` table using the key `rental_id`, which these tables have in common.

* Connect to the `inventory` table using the key `inventory_id`.

* Connect the `film` table using the key `film_id`, which it has in common with the `inventory` table.

* In the last subquery, query the film title, BLANKET BEVERLY.

The sample query would be as follows:

  ```sql
  SELECT COUNT(*)
  FROM customer
  WHERE customer_id IN
  (
    SELECT customer_id
    FROM payment
    WHERE rental_id IN
  (
    SELECT rental_id
    FROM rental
    WHERE inventory_id IN
    (
      SELECT inventory_id
      FROM inventory
      WHERE film_id IN
      (
        SELECT film_id
        FROM film
        WHERE title = 'BLANKET BEVERLY'
      )
    )
  )
  );
  ```

`COUNT(*)` will count the number of rows, similar to how `SELECT *` will select all rows. The asterisk indicates *all*.

Run the query. It will return that 12 people have rented this film.

Explain that there are often multiple ways to find this result through different table relationships.

Answer any questions before moving on.

---

### 17. Students Do: Mine the Subquery (10 min)

**Corresponding Activity:** [11-Stu_Mine_the_Subquery](Activities/11-Stu_Mine_the_Subquery)

Use the slides to introduce this activity. The students will continue to practice subqueries while working individually or in pairs.

---

### 18. Review: Mine the Subquery (5 min)

**File**: [mine_the_subquery_solution.sql](Activities/11-Stu_Mine_the_Subquery/Solved/mine_the_subquery_solution.sql)

Utilize the slideshow to review the activity.

Review the solution to the activity and answer any questions that students have.

A possible solution to the first problem is as follows:

  ```sql
  SELECT first_name, last_name
  FROM actor
  WHERE actor_id IN
  (
    SELECT actor_id
    FROM film_actor
    WHERE film_id IN
    (
      SELECT film_id
      FROM film
      WHERE title = 'ALTER VICTORY'
    )
  );
  ```

* The best way to proceed is to start with the most specific piece of information and work your way up. In this case, the innermost subquery retrieves the `film_id` of the given film title.

* This information is used to retrieve the `actor_id`, which is then used to extract the names of the actors who appear in the film.

A possible solution to the second problem is as follows:

  ```sql
  SELECT title
  FROM film
  WHERE film_id
  IN (
    SELECT film_id
      FROM inventory
      WHERE inventory_id
      IN (
          SELECT inventory_id
          FROM rental
          WHERE staff_id
          IN (
                SELECT staff_id
                FROM staff
                WHERE last_name = 'Stephens' AND first_name = 'Jon'
              )
          )
    );
  ```

* Similar to the first problem, the query begins with the most specific piece of information and works its way up.

* We use the employee name to query the `staff_id`.

* We then use the `staff_id` to retrieve the `inventory_id` from rentals.

* Finally, we use the `inventory_id` to retrieve the `film_id`, which enables us to retrieve the relevant film titles.

Answer any questions before ending class.

---

### References

Oracle Corporation. (2019). Sakila Sample Database. Edited by Devrim Gündüz into Pagila. [Sakila Sample Database](https://github.com/devrimgunduz/pagila)

---

© 2022 edX Boot Camps LLC. Confidential and Proprietary. All Rights Reserved.
