# 10.2: Advanced Usage of the SQLAlchemy ORM

## Overview

* Today's lesson introduces the students to the finer details of working with the SQLAlchemy ORM, including how to create complex queries, update rows, perform joins, and use ORM methods to perform queries.

## Class Objectives

* By the end of this lesson, the students will be able to:

* Use the SQLAlchemy ORM to create classes that model tables.

* Perform database CRUD operations by using the SQLAlchemy ORM.

* Reflect existing databases.

* Use the SQLAlchemy Inspector to view table names in the database.

* Plot query results from the ORM.

* Run a t-test to validate differences in means.

---

### Instructor Notes

* This second day of SQLAlchemy will focus on CRUD using SQLAlchemy's ORM.  If some students feel that they are struggling to keep up, reassure them that they will be getting plenty of practice performing basic tasks with this library.


---

### Class Slides

* The slides for this lesson can be viewed on Google Drive here: [Lesson 10.2 slides](https://docs.google.com/presentation/d/1nWkJnbud_mOkulclYs-u7P5LpEMGr0gThW2cLaLEX8I/edit?usp=sharing).

* To add the slides to the student-facing repository, download the slides as a PDF by navigating to File, selecting "Download as," and then choosing "PDF document." Then, add the PDF file to your class repository along with other necessary files. You can view instructions for this [here](https://docs.google.com/document/d/1XM90c4s9XjwZHjdUlwEMcv2iXcO_yRGx5p2iLZ3BGNI/edit?usp=sharing).

* **Note:** Editing access is not available for this document. If you wish to modify the slides, create a copy by navigating to File and selecting "Make a copy...".

---

### Time Tracker

| Start Time | Number | Activity                                           | Duration |
| ---------- | ------ | -------------------------------------------------- | -------- |
| 6:30 PM    | 1      | Instructor Do: Welcome Class                       | 0:05     |
| 6:35 PM    | 2      | Instructor Do: SQLAlchemy Queries in Action        | 0:15     |
| 6:50 PM    | 3      | Students Do: Sunny Hours Search                    | 0:20     |
| 7:10 PM    | 4      | Review: Sunny Hours Search                         | 0:10     |
| 7:20 PM    | 5      | Instructor Do: Updating and Deleting Rows          | 0:10     |
| 7:30 PM    | 6      | Partners Do: CRUD Database                         | 0:20     |
| 7:50 PM    | 7      | Review: CRUD Database                              | 0:05     |
| 7:55 PM    | 8      | BREAK                                              | 0:15     |
| 8:10 PM    | 9      | Instructor Do: Reflection with SQL                 | 0:10     |
| 8:20 PM    | 10     | Students Do: Demographics Reflection with SQL      | 0:20     |
| 8:40 PM    | 11     | Review: Demographics Reflection with SQL           | 0:10     |
| 8:50 PM    | 12     | Instructor Do: SQLAlchemy Inspection               | 0:10     |
| 9:00 PM    | 13     | Students Do: Salary Exploration                    | 0:20     |
| 9:20 PM    | 14     | Review: Salary Exploration                         | 0:10     |
| 9:30 PM    |        | END                                                |          |

---

### 1. Instructor Do: Welcome Class (5 min)

* Welcome the class to their second day of SQLAlchemy. Today's class will focus on performing specific SQL tasks using SQLAlchemy's ORM. If some students feel that they are struggling to keep up, reassure them that they will be getting plenty of practice performing basic tasks with this library.

* Open the slides, and cover the following points:

* Explain that today's class will cover a deeper dive into SQLAlchemy functionality, with particular focus on how to characterize and query databases.

* Go over the following class objectives for today:

  * Use SQLAlchemy ORM to model tables.

  * Perform CRUD with SQLAlchemy.

  * Reflect existing databases with SQLAlchemy.

  * Plot query results from SQLAlchemy ORM.

  * Run a t-test to validate differences in means.

---

### 2. Instructor Do: SQLAlchemy Queries in Action (15 min)

**Corresponding Activity:** [01-Ins_Basic_Querying](Activities/01-Ins_Basic_Querying/)

Use the slides and introduce the activity. Be sure to cover the following points:

* Crafting SQLAlchemy queries is much easier than we might first expect. To prove this point, we will work with more realistic datasets today.

* Mention to the class that our first database contains over 1,000 rows of data that can be searched through.

* Explain that in this activity, we will demonstrate how SQLAlchemy can be used in conjunction with SciPy to perform analysis on a dataset.

  * For students who are pursuing a career in data science, it’s important to practice this workflow on their own&mdash;the process of querying data, analyzing the output, making a hypothesis, and then running a statistical test is a cornerstone of data science.

   * For those who are not pursuing a career in data science, this workflow demonstrates how SQLAlchemy can interface with another common Python library using queried objects.

* Ask the students if they recall how to query a database using SQLAlchemy.

* Remind them that there are two basic ways to query a database in SQLAlchemy&mdash;with SQL statements and with Python objects.

* In the previous class, we discussed that Python objects are preferred for interacting with a database in SQLAlchemy.

Open [basic_querying_solution.ipynb](Activities/01-Ins_Basic_Querying/Solved/basic_querying_solution.ipynb) within Jupyter notebook, and go through the code with the class.

* After we setup the database and create the connection we query the database for all of the records in the `BaseballPlayer` table, using `session.query()` and pass through the SQLAlchemy class associated with the table as a parameter, as shown in the following code:

  ```python
  # Print all of the player names in the database
  players = session.query(BaseballPlayer)
  for player in players:
    print(player.name_given)
  ```

* Then , to create a query that looks into a specific column and selects only the data that passes a logic test, use the `session.query(<SQL Class>).filter()` method. When using this method, employ dot notation to pass the class and column to query, then follow this with the test to perform, as in the following code:

  ```python
  # Find the number of players from the USA
  usa = session.query(BaseballPlayer).\
      filter(BaseballPlayer.birth_country == 'USA').count()
  print(f"There are {usa} players from the USA")

  # Find those players who were born before 1990
  born_before_1990 = session.query(BaseballPlayer).\
      filter(BaseballPlayer.birth_year < 1990).count()
  print(f"{born_before_1990} players were born before 1990")
  ```

* We can filter the table on multiple columns using the `filter()` method for each logic test as parameters, as shown in the following code:

  ```python
  # Find those players from the USA who were born after 1989
  born_after_1989 = session.query(BaseballPlayer).\
      filter(BaseballPlayer.birth_year > 1989).filter(BaseballPlayer.birth_country == "USA").\
      count()
  print(f"{born_after_1989} USA players were born after 1989")
  ```

* Explain that the second part of the notebook asks the following question:

  * Is the height difference, if any, between players born before 1940 and those born in or after 1940 statistically significant?

  * The following code retrieves all players born before and after 1940:

  ```python
  # Filter for players born before 1940, and for players born in or after 1940
    born_before_1940_height = session.query(BaseballPlayer).\
      filter(BaseballPlayer.birth_year < 1940)

    born_after_1940_height = session.query(BaseballPlayer).\
        filter(BaseballPlayer.birth_year >= 1940)
  ```

  * These variables are assigned to SQLAlchemy objects; each must be iterated upon to create a usable Python list.

* Briefly mention the following data-wrangling step for filtering out non-integers from the lists:

  ```python
  # Filter out null values from lists
  pre_1940_height_list = []
  for player in born_before_1940_height:
      if type(player.height) == int:
          pre_1940_height_list.append(player.height)

  post_1940_height_list = []
  for player in born_after_1940_height:
      if type(player.height) == int:
          post_1940_height_list.append(player.height)
  ```

  * Only values whose type is `int` are appended to the list of player heights.

* Explain that the `scipy` module is used to calculate the mean height of each group, as in the following code:

  ```python
  # Average height for pre-1940 players
  mean(pre_1940_height_list)
  # Average height for post-1940 players
  mean(post_1940_height_list)
  ```

  * The difference in mean height between the two groups is over two inches.

* Ask the students the following questions:

  * What is a t-test?

  * What is a t-test used for?

* Explain that the t-test is a statistical test used to determine the likelihood that the difference in the means between two groups is statistically significant.

  * The paired t-test compares the means of the _same_ group at different points in time: for example, mean blood pressure in patients before and after medication.

  * The unpaired t-test compares the means of two different groups: for example, the mean annual spending on dining out among Minnesotans versus Texans.

* Ask the class which t-test would be appropriate to determine whether there's a statistically significant difference between the mean height of baseball players born before 1940 and those born in or after 1940.

  * The comparison here is between two different groups of people; therefore, the unpaired t-test is appropriate.

* Remind the students that an unpaired (independent) t-test is run using `scipy.stats` to compare the means of two groups, as in the following code:

  ```python
  # Unpaired (independent) t-test
  stats.ttest_ind(post_1940_height_list, pre_1940_height_list)
  ```

  * It returns a very small p-value that has been rounded down to zero, indicating that the difference between the two means is statistically significant.

* Answer any questions before moving on.

---

### 3. Students Do: Sunny Hours Search (20 min)

**Corresponding Activity:** [02-Stu_Sunny_Hours](Activities/02-Stu_Sunny_Hours/)

* You may use the slides to accompany this activity.

* In this activity, the students will create a Python script that can search through the provided SQL file of data on hours of sunshine in cities throughout the world.

* Data Sources:

  * Kaggle (2022). Sunshine Duration by City. Data provided by Kaggle. [https://www.kaggle.com/datasets/prasertk/sunshine-duration-by-city/metadata](https://www.kaggle.com/datasets/prasertk/sunshine-duration-by-city/metadata)

  * Wikipedia (2022). List of cities by sunshine duration. Data provided by Wikipedia. [https://en.wikipedia.org/wiki/List_of_cities_by_sunshine_duration](https://en.wikipedia.org/wiki/List_of_cities_by_sunshine_duration)


---

### 4. Review: Sunny Hours Search (10 min)

* First, open the [README.md](Activities/02-Stu_Sunny_Hours/README.md) file and show students the schema of the SQL database.

  ```sql
  CREATE TABLE sunshine (
      id INTEGER PRIMARY KEY,
      Country TEXT,
      City TEXT,
      Jan REAL,
      Apr REAL,
      Jul REAL,
      Oct REAL,
      Year REAL
  );
  ```

* Discuss the following points about the SQL database:

  * This table schema will be transformed into a Python class.

  * The table name is `sunshine`.

  * The `id` column is the primary key, and has the Integer data type.

  * The `Country` and `City` columns have the TEXT data type.

  * The rest of the columns have the REAL data type, which corresponds to numbers.

* Open the solution in [sunny_hours_solution.ipynb](Activities/02-Stu_Sunny_Hours/Solved/sunny_hours_solution.ipynb).

* Explain that we can create a Python class to represent each row in the SQL database:

  ```python
  # Create your Sunshine class
  class Sunshine(Base):
      __tablename__ = 'sunshine'
      id = Column(Integer, primary_key=True)
      Country = Column(String)
      City = Column(String)
      Jan = Column(Float)
      Apr = Column(Float)
      Jul = Column(Float)
      Oct = Column(Float)
      Year = Column(Float)
  ```

* Discuss the following points about the Sunshine class:

  * `class Sunshine(Base)` uses SQLAlchemy's `declaratative_base` to create a Python class.

  * The `__tablename__` is the name of the SQL table.

  * The `id` column is specified to contain integers, and is also designated as the primary key of the table.

  * The `Country` and `City` columns contain the String data type.

  * The rest of the columns, since they are temperature readings, will contain floating point numbers, otherwise known as decimals. In SQLAlchemy, this will be the Float data type.

* Explain that we next query the entire database:

  * `sunshine` is the variable assigned to the entire database, which we will query in Python.

  * A `session` represents the interaction between the Python program and the SQL database.

    ```python
    # Create a session query.
    sunshine = session.query(Sunshine)
    ```

* Explain that we can print out the entire database:

  ```python
  # Print all observations
  for city in sunshine:
      print(f"{city.id}, {city.Country}, {city.City}, {city.Jan}, {city.Apr}, {city.Jul}, {city.Oct}, {city.Year}")
  ```

* All the columns of each row are printed.

* Explain that the next query returns the total number of cities, or rows, in the database.

  * The `distinct()` method excludes duplicate rows.

  * The `count()` method returns the number of rows from the database.

    ```python
    # Find the total number of cities in the database
    total_count = session.query(Sunshine).distinct().count()
    print(total_count)
    ```

* Explain that the next query returns the number of results from Canada.

   The `filter_by` method is used to specify the value of the `Country` column.

    ```python
    # Find the total number of observed cities in Canada
    canadian_cities = session.query(Sunshine).\
        filter_by(Country='Canada').count()
    print(canadian_cities)
    ```

* Next, explain that cities that receive 3700 or more hours of sunshine per year are retrieved.

   The `filter` method is used to filter for rows whose `Year` value is 3700 or greater.

    ```python
    # Find the number of cities whose yearly sunshine equals or exceeds 3700 hours
    over_3700_hours_count = session.query(Sunshine).\
        filter(Sunshine.Year >= 3700).count()
    print(over_3700_hours_count)
    ```

* Explain that the cities from the preceding query can be printed:

  ```python
  # Print the cities that have a total yearly sunshine of 3700 hours or greater
  over_3700_hours = session.query(Sunshine).\
      filter(Sunshine.Year >= 3700)

  # Print the city name, country, January sunny hours, and yearly sunny hours
  # of all cities that have 3700 or greater hours of sunshine in a year.
  for city in over_3700_hours:
      print(city.Country, city.City, city.Year)
  ```

* Explain that a similar logic as above can be used to count cities that receive 300 or more hours of sunshine in January, and to print the cities.

  ```python
  # Find the number of cities whose January sunshine equals or exceeds 300 hours
  sunny_january_count = session.query(Sunshine).\
      filter(Sunshine.Jan >= 300).count()

  # Find cities whose January sunshine equals or exceeds 300 hours
  sunny_january_cities = session.query(Sunshine).\
      filter(Sunshine.Jan >= 300)

  # Print the city name, country, January sunny hours, and yearly sunny hours
  # of all cities that have 300 or greater hours of sunshine in January.
  for city in sunny_january_cities:
      print(city.Country, city.City, city.Jan, city.Year)
  ```

* Explain that, again, we can use similar logic to count and identify cities in the United States that receive 2500 or fewer hours of sunshine in a year.

  ```python
  # Find cities in the United States whose yearly sunshine is 2500 hours or fewer.
  overcast_cities_count = session.query(Sunshine).\
      filter(Sunshine.Country == 'United States').\
      filter(Sunshine.Year <= 2500).count()

  print(overcast_cities_count)

  overcast_cities = session.query(Sunshine).\
      filter(Sunshine.Country == 'United States').\
      filter(Sunshine.Year <= 2500)

  # Retrieve the city name and yearly sunny hours of cities in the United States
  # that receive 2500 hours or fewer of sunshine per year
  for city in overcast_cities:
      print(city.City, city.Year)
  ```

* Lastly, remind students to close the SQLAlchemy session when they're finished.

  ```python
  session.close()
  ```

---

### 5. Instructor Do: Updating and Deleting Rows (10 min)

**Corresponding Activity:** [03-Ins_Basic_Updating](Activities/03-Ins_Basic_Updating/)

Use the slides and introduce the next activity. Be sure to cover the following points:

* So far, the students have learned how to create and read data from a SQL database by using SQLAlchemy. Now, they’ll continue their way through the CRUD acronym and learn how to update the data.

Open [basic_updating_solution.ipynb](Activities/03-Ins_Basic_Updating/Solved/basic_updating_solution.ipynb) within an Jupyter notebook, run the code to set up the table and database and add data to the table. Then, go through the code with the class to show them how to update and delete data from the table while explaining the following:

* Performing updates is as simple as creating a query for the row(s) to modify and then altering the returned object(s) in the desired way.

* Make sure to point out that `.first()` is used to restrict the query to the first match. Without this additional method, the changes will not be made.

* Since the record already exists within the external database, there is no need to perform a `session.add()`. Instead, we only need to use `session.commit()` to update the rows in the table, as in the following image:

  ![Updating Rows](https://static.bc-edx.com/data/dl-1-2/m10/lessons/2/img/04-Updating_SingleUpdate.png)

* Deleting rows is also an extension of SQLAlchemy's querying functionality.

  * Perform a query to locate the row to delete, and then add the `.one()` method onto the end of the query statement to return one result.

  * To perform this modification, we'll use the `deleted` attribute.

  * Make sure to use `session.commit()` for the delete to take effect, as in the following image:

  ![Deleting Rows](https://static.bc-edx.com/data/dl-1-2/m10/lessons/2/img/04-Updating_Delete.png)

  * Querying the table once more will show that Marshmallow has been removed.

* Finally, close the session with `session.close()`.

* Answer any questions before moving on.

---

### 6. Partners Do: CRUD Database (20 min)

**Corresponding Activity:** [04-Par_CRUD_DB](Activities/04-Par_CRUD_DB/)

* You may use the slides to accompany this activity.

* In this activity, pairs of students will be tasked with creating a new SQLite database for travel destinations. They will need to create a table, add rows into the table, update values in rows, and, finally, delete a row from the database.

---

### 7. Review: CRUD Database (5 min)

* Open the solution in [CRUD_DB_solution.ipynb](Activities/04-Par_CRUD_DB/Solved/CRUD_DB_solution.ipynb), and go through the code line by line, explaining each cell as you progress through the notebook.

---

### 8. BREAK (15 min)

---

### 9. Instructor Do: Reflection with SQL (10 min)

**Corresponding Activity:** [05-Ins_Reflection](Activities/05-Ins_Reflection/)

Use the slides to introduce the next activity. Be sure to cover the following points:

* Point out that, as data analysts, developers often need to analyze already-existing data sources. This would mean having to manually create SQLAlchemy classes according to a table's columns every single time.

* Thankfully, SQLAlchemy provides tools for automatically creating ORM classes from an existing database.

  * Explain that these tools will load the data from an existing database and use that data to infer how to write ORM classes for use "automagically."

  * Explain that this process is called **reflection**.

Open [reflection_solution.ipynb](Activities/05-Ins_Reflection/Solved/reflection_solution.ipynb) within Jupyter notebook, and explain that reflecting an existing database is a simple four-step process:

* Step 1: First, import `automap_base` from the SQLAlchemy library.

* Step 2: Then, create an `engine` against the existing database that should be reflected.

* Step 3: Next, create a `Base` by calling `Base = automap_base()`.

* Step 4: Finally, call `Base.prepare` with `autoload_with=engine` as its parameter, where `engine` is what we created in Step 2.

* The following image contains the code for these four steps:

* The following is the code for these four steps:

  ```python
  # Python SQL toolkit and Object Relational Mapper
  import sqlalchemy
  from sqlalchemy.ext.automap import automap_base
  from sqlalchemy.orm import Session
  from sqlalchemy import create_engine

  # Create engine using the `dow.sqlite` database file
  engine = create_engine("sqlite:///../Resources/dow.sqlite")

  # Declare a Base using `automap_base()`
  Base = automap_base()

  # Use the Base class to reflect the database tables
  Base.prepare(autoload_with=engine)
  ```

* Point out that `automap_base` is similar to `declarative_base` but creates a different `Base` class with additional features:

  * In particular, the class returned by `automap_base` has a `prepare` method, which will "automagically" reflect the data in an existing database.

* Explain that it is possible to view the “automagically” generated ORM classes by examining `Base.classes.keys()`.

  * Point out that, by default, these keys will share the name of the underlying database tables that they represent.

  * Explain that it is possible to access these classes via dot notation, `<ExampleClassName> = Base.classes.<ExampleClassName>`.

* Explain that, after the database has been reflected, the autogenerated ORM classes can be used just like developers would use custom classes.

  * Demonstrate that, just as before, it is possible to interact with the database using these autogenerated classes in conjunction with a `session`, as in the following image:

    ![Utilizing Reflections](https://static.bc-edx.com/data/dl-1-2/m10/lessons/2/img/06-Reflections_UsingReflectedTables.png)

* Data Source: Brown, Michael. (2013). Weekly Dow Jones Index Data. 10.13140/2.1.2729.4409.

* Answer any questions before moving on.

---

### 10. Students Do: Demographics Reflection with SQL (20 min)

**Corresponding Activity:** [06-Stu_Reflecting_On_SQL](Activities/06-Stu_Reflecting_On_SQL/)

* You may use the slides to accompany this activity.

* Students will now practice how to reflect existing databases using SQLAlchemy and a SQLite table with demographic data, as captured in the following image:

  ![Reflecting on SQL Output](https://static.bc-edx.com/data/dl-1-2/m10/lessons/2/img/07-ReflectingOnSQL_Output.png)

* Data Source: Brown, Michael. (2013). Weekly Dow Jones Index Data. 10.13140/2.1.2729.4409.

---

### 11. Review: Demographics Reflection with SQL (10 min)

Open [demographics_reflection_solution.ipynb](Activities/06-Stu_Reflecting_On_SQL/Solved/demographics_reflection_solution.ipynb), within Jupyter notebook, and go through the code line by line, explaining the following points:

* `Base` is instantiated with `automap_base` as opposed to `declarative_base`. `Base.prepare()` is then called, passing the SQL connection engine as part of the keyword argument `autoload_with=engine` to create a reflection of the existing database.

* A list of all of the reflected tables can be collected using `Base.classes.keys()`.

* The class associated with a given table can be collected by referencing the appropriate property within `Base.classes`, as captured in the following image:

  ```python
  # Create engine using the `demographics.sqlite` database file
  engine = create_engine("sqlite:///../Resources/demographics.sqlite")

  # Declare a Base using `automap_base()`
  Base = automap_base()

  # Use the Base class to reflect the database tables
  Base.prepare(autoload_with=engine)

  # Print all of the classes mapped to the Base
  Base.classes.keys()
  ```

  ```text
  ['demographics']
  ```

  ```python
  # Assign the demographics class to a variable called `Demographics`
  Demographics = Base.classes.demographics
  ```

* For the bonus, `group_by` allows us to "collapse" results that share a certain column value, and then `count` can be used to count the number of rows returned by the query.

* The query first creates a set for each demographic location that appears within the database; it then counts the number of sets returned and yields the number of unique locations represented in the database, as captured in the following image:

  ![Counting Uniques](https://static.bc-edx.com/data/dl-1-2/m10/lessons/2/img/07-ReflectingOnSQL_Unique.png)

* Answer any questions before moving on.

---

### 12. Instructor Do: SQLAlchemy Inspection (10 min)

**Corresponding Activity:** [07-Ins_Inspection](Activities/07-Ins_Inspection/)

* Reflecting a database to collect the classes stored within is a start, but it does not provide users with any real knowledge on what information is being stored.

  * To collect that kind of information, developers would want to look into the columns for a table and their associated data types.

* The creators of SQLAlchemy thankfully understood that this would be something users would want from the library, so they created an inspector tool.

  * The inspector tool allows SQLAlchemy developers to look through a connected database and explore its contents.

  * Unlike session queries, the inspector is primarily used to look up tables, columns, and data types. To look up specific values stored in a table, queries should be used.

Open [Dow_inspector_solution.ipynb](Activities/07-Ins_Inspection/Solved/Dow_inspector_solution.ipynb) within Jupyter notebook, and go over the code line by line.

* The `inspect` module for SQLAlchemy can be imported into a script alongside the `create_engine` module.

* To create an inspector, create a variable and set it equal to `inspect(engine)`. This variable can then be used to inspect elements within the connected database.

* To get the names of tables stored within the connected database, use `inspector.get_table_names()`, as in the following image:

  ![Inspector Made](https://static.bc-edx.com/data/dl-1-2/m10/lessons/2/img/08-Exploration_Inspector.png)

* To collect the columns in a table from the connected database, use `inspector.get_columns(<Table Name>)`, and pass the name of the table through as a parameter.

* Simply loop through the columns collected, and it is then possible to print out their names and type using `column["name"]` and `column["type"]`, as in the following image:

  ![Column Info](https://static.bc-edx.com/data/dl-1-2/m10/lessons/2/img/08-Exploration_ColumnInfo.png)

* Answer any questions before moving on.

---

### 13. Students Do: Salary Exploration (20 min)

**Corresponding Activity:** [08-Stu_Salary_Exploration](Activities/08-Stu_Salary_Exploration/)

* You may use the slides to accompany this activity.

* The students will now take some time to create an inspector and search through a SQLite database of San Francisco salaries.

* Data Source: DataSF. (2022). OpenData. Employee Compensation, City Management and Ethics. Data provided by SF Controller's Office. [https://data.sfgov.org](https://data.sfgov.org/City-Management-and-Ethics/Employee-Compensation/88g8-5mnd).

---

### 14. Review: Salary Exploration (10 min)

Open [salary_exploration_solution.ipynb](Activities/08-Stu_Salary_Exploration/Solved/salary_exploration_solution.ipynb), within Jupyter notebook, and go through the code line by line, answering any questions the students may have.


—--

© 2022 edX Boot Camps LLC. Confidential and Proprietary. All Rights Reserved.
