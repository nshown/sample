# 10.1: Introduction to SQLAlchemy

## Overview

Today's lesson introduces the students to the SQLAlchemy library for Python.

## Class Objectives

By the end of this lesson, the students will be able to:

* Connect to a SQL database by using SQLAlchemy.

* Perform basic SQL queries by using `engine.execute()`.

* Create Python classes and objects.

* Create, read, update, and delete data from a SQL database by using SQLAlchemy's object-relational mapper (ORM).

---

### Instructor Notes

In this module, we introduce the `sqlalchemy` library. This curriculum has been tested with Python 3.10, but updates to packages and variances in student machines can still cause conflicts to occur. If a student has an error that you believe to be related to Python 3.10, at your discretion you can instruct them to create a new environment using a different Python version. If you believe that an update has introduced a bug at a curriculum level, attempt to find a suitable workaround for the moment and submit a report using the Boot Camp Feedback Form.

* This first day of SQLAlchemy includes a lot of material that the students will need for the homework assignment, while the second day contains more complex activities for the students to use as practice. Feel free to mix up the timing and/or activities for these two lessons to ensure that the students feel comfortable with the SQLAlchemy library and that they are having an enjoyable experience.

* Have the student's check if they have `sqlalchemy` installed in their `dev` environment by running `conda list sqlalchemy` in the command line. If they don't have `sqlalchemy` installed then have them install it by running `conda install -c anaconda sqlalchemy` on their command line.

---

### Class Slides

* The slides for this lesson can be viewed on Google Drive here: [Lesson 10.1 slides](https://docs.google.com/presentation/d/1Kzy8x2YbCo2vcl3C1EJGL6uAd-4oWfIKZ1yKd13prK8/edit?usp=sharing).

* To add the slides to the student-facing repository, download the slides as a PDF by navigating to File, selecting "Download as," and then choosing "PDF document." Then, add the PDF file to your class repository along with other necessary files. You can view instructions for this [here](https://docs.google.com/document/d/1XM90c4s9XjwZHjdUlwEMcv2iXcO_yRGx5p2iLZ3BGNI/edit?usp=sharing).

* **Note:** Editing access is not available for this document. If you wish to modify the slides, create a copy by navigating to File and selecting "Make a copy...".

---

### Time Tracker

| Start Time | Number | Activity                                           | Duration |
| ---------- | ------ | -------------------------------------------------- | -------- |
| 6:30 PM    | 1      | Instructor Do: Welcome Class                       | 0:05     |
| 6:35 PM    | 2      | Partners Do: Looking into SQLAlchemy               | 0:05     |
| 6:40 PM    | 3      | Instructor Do: Introduction to SQLAlchemy          | 0:05     |
| 6:45 PM    | 4      | Instructor Do: Building a SQLAlchemy Connection    | 0:10     |
| 6:55 PM    | 5      | Students Do: Ice Cream Connection                  | 0:10     |
| 7:05 PM    | 6      | Review: Ice Cream Connection                       | 0:05     |
| 7:10 PM    | 7      | Instructor Do: SQLAlchemy and Pandas               | 0:05     |
| 7:15 PM    | 8      | Students Do: Read All the SQL                      | 0:10     |
| 7:25 PM    | 9      | Review: Read All the SQL                           | 0:05     |
| 7:30 PM    | 10     | Instructor Do: Preview SQLAlchemy with Classes     | 0:05     |
| 7:35 PM    | 11     | BREAK                                              | 0:15     |
| 7:50 PM    | 12     | Instructor Do: A Schooling on Classes              | 0:10     |
| 8:00 PM    | 13     | Students Do: Surfer Class                          | 0:15     |
| 8:15 PM    | 14     | Review: Surfer Class                               | 0:05     |
| 8:20 PM    | 15     | Instructor Do: A Method to the Classes             | 0:05     |
| 8:25 PM    | 16     | Students Do: Surfer Class Extended                 | 0:10     |
| 8:35 PM    | 17     | Review: Surfer Class Extended                      | 0:05     |
| 8:40 PM    | 18     | Everyone Do: Back to the SQL                       | 0:20     |
| 9:00 PM    | 19     | Students Do: Surfing SQL                           | 0:20     |
| 9:20 PM    | 20     | Review: Surfing SQL                                | 0:10     |
| 9:30 PM    |        | END                                                |          |

---

### 1. Instructor Do: Welcome Class (5 min)

Welcome the students back to another fun-filled week of SQL. This week, the class will use Python to interact with SQL databases.

Open the slides and cover the following points:

* Explain that this week's class will take what we learned last week using SQL and combine it with our favorite programming language, Python.

* Introduce today’s class objectives:

  * Connect to a SQL database with SQLAlchemy.

  * Perform a SQL query with SQLAlchemy.

  * Create Python classes and objects.

  * Use a Python class to model a SQL table.

---

### 2. Partners Do: Looking into SQLAlchemy (5 min)

* Use the slides and cover the following points:

* Before delving into SQLAlchemy as a class, have the students break into groups of two or three to research the following questions:

  * What is an ORM?

  * What are the benefits of using an ORM?

  * What are some of the disadvantages of using an ORM?

* After 3 minutes, have the students come back together to answer the preceding questions.

  * Advantages of using an ORM for SQL databases include the following:

    * The ability to work across different SQL dialects by using the same basic Python query

    * The ability to create command line interfaces that allow users to construct SQL queries without needing to know the language.

  * A disadvantage is that ORMs are like a new dialect of a language, so you have to learn how to use them. Also, they may reduce control or ability to optimize a query.

---

### 3. Instructor Do: Introduction to SQLAlchemy (5 min)

* Use the slides and cover the following talking points:

* Explain that SQLAlchemy is a Python library designed to work with SQL databases.

  * SQLAlchemy bridges the differences among the various SQL dialects.

  * A single Python script that uses SQLAlchemy can perform the same query across the different SQL dialects, such as PostgreSQL, SQLite, and MySQL.

* Send out the link to the [SQLAlchemy](https://www.sqlalchemy.org/features.html) features page, and tell the students that they can refer to this page if they are interested in just how flexible and robust `SQLAlchemy` can be.

* Explain that SQLAlchemy can query a SQL database with SQL or Python:

  * The first query is a simple “select all” query: `SELECT * FROM icecreamstore;`

  * The second queries a database called `BaseballPlayer` that is imported into Python.

  * `player.name_given` uses the dot notation. We will return to what this means and how it is used in our discussion of Python classes and SQLAlchemy ORM.

* Send the class the link to the [SQLAlchemy documentation](http://docs.sqlalchemy.org/en/latest/dialects).

  * The page lists SQL dialects that are compatible with SQLAlchemy.

  * On the left side of the page, the students can find the complete documentation of the SQLAlchemy library.

  * The students should consult this documentation to clarify any questions that they may have. They should be able to fix most bugs this way.

---

### 4. Instructor Do: Building a SQLAlchemy Connection (10 min)

**Corresponding Activity:** [01-Ins_BasicSQL_Connection](Activities/01-Ins_BasicSQL_Connection/)

* Use the slides and cover the following points:

* Let the class know that, for today's lesson, they will only be working with SQLite databases.

  * SQLite is a SQL dialect that shares much of the same syntax as PostgreSQL, but it is entirely serverless.

  * How can a database be serverless? Well, SQLite reads and writes directly to ordinary disk files, which can in turn be stored on a computer's hard drive. This makes it much easier to use to perform tests and share between users.

  * Have the students check if they have `sqlalchemy` installed in their `dev` environment by running `conda list sqlalchemy` in the command line. If they don't have `sqlalchemy` installed then have them install it by running `conda install -c anaconda sqlalchemy` on their command line.

* Open [read_census_data_solution.ipynb](Activities/01-Ins_BasicSQL_Connection/Solved/read_census_data_solution.ipynb) within Jupyter notebook, and go through the code with the class.

  * To use SQLAlchemy, we must import certain modules from the library. For example, to create a connection to a SQL database, we need to import the `create_engine` module.

  * After importing all of the necessary libraries/modules, we can finally create the connection engine by using the `create_engine()` method and passing in a connection string, as in the following code:

    ```python
    # Create an engine that can talk to the database
    engine = create_engine(f"sqlite:///{database_path}")
    ```

  * Connection strings can also include the database username, password, or database name. The students can refer to the SQLAlchemy documentation to determine how to connect to other databases, but today's class will focus on SQLite.

* Once we’ve created a connection engine, we can use `engine.execute()` to run SQL commands from our Python script. To do so, pass the code to run into the method as a string, and SQLAlchemy will pass the request onto the database. Note that in SQLAlchemy 2.0 (released 2023-01-26), raw SQL queries must be wrapped by the sqlalchemy.text function.

  * For example, to collect all of the data stored within a table on a database, pass `text(SELECT * FROM <Tablename>)` into the `engine.execute()` method, as in the following image:

    ![Engine Execute](https://static.bc-edx.com/data/dl-1-2/m10/lessons/1/img/01-Connections_Execute.png)

  * Point out how the data returned in [read_census_data_solution.ipynb](Activities/01-Ins_BasicSQL_Connection/Solved/read_census_data_solution.ipynb) is stored in a variable and then looped through to print out the rows from `Census_Data`.

* Answer any questions before moving on.

---

### 5. Students Do: Ice Cream Connection (10 min)

**Corresponding Activity:** [02-Stu_IceCream_Connection](Activities/02-Stu_IceCream_Connection/)

You may use the slides to accompany this activity.

In this activity, the students will be creating and connecting to a new database using SQLAlchemy. They will then read in the data by using `engine.execute()`.

---

### 6. Review: Ice Cream Connection (5 min)

Open [ice_cream_connector_solution.ipynb](Activities/02-Stu_IceCream_Connection/Solved/ice_cream_connector_solution.ipynb) within Jupyter notebook, and go through the code line by line, answering whatever questions the students may have and make sure to cover the following points:

* To retrieve all the records we use the following code:

  ```python
  # Query All Records in the the Database
  query = text("SELECT * FROM icecreamstore;")
  data = engine.execute(query)
  for record in data:
      print(record)
  ```

  * The output is as follows:

    ```text
    (1, 'Vanilla', 150, 2.0)
    (2, 'Chocolate', 125, 2.0)
    (3, 'Bubblegum', 95, 2.5)
    (4, 'Mint Chocolate Chip', 100, 2.5)
    (5, 'Strawberry', 75, 2.0)
    (6, 'Cookies and Cream', 100, 2.5)
    (25, 'testflavor', 5, 0.5)
    ```

* To retrieve the ice cream flavors that cost more than `2.0` we use the following code:

  ```python
  # Query Using a Filter
  query = text("SELECT * FROM icecreamstore WHERE Price > 2.0;")
  data = engine.execute()
  for record in data:
      print(record)
  ```

* Running the query returns the following data:

    ```text
    (3, 'Bubblegum', 95, 2.5)
    (4, 'Mint Chocolate Chip', 100, 2.5)
    (6, 'Cookies and Cream', 100, 2.5)
    ```

* Data Source: Mockaroo, LLC. (2021). Realistic Data Generator. [https://www.mockaroo.com/](https://www.mockaroo.com/)

---

### 7. Instructor Do: SQLAlchemy and Pandas (5 min)

**Corresponding Activity:** [03-Ins_Read_SQL](Activities/03-Ins_Read_SQL)

Use the slides and cover the following points:

* One of the most impressive aspects of SQLAlchemy is how it integrates with Pandas.

* After creating the engine and connection to our SQL database, we can use Pandas to query the database and store the records in a DataFrame.

* Open [Intro_SQL_Pandas_solution.ipynb](Activities/03-Ins_Read_SQL/Solved/Intro_SQL_Pandas_solution.ipynb) within Jupyter notebook, and demonstrate how this is done.

  * By creating a connection to a database using SQLAlchemy, Pandas can use that engine to pull data directly into a DataFrame with the `pd.read_sql()` method.

  * When using the `pd.read_sql()` method, a query string and a connection variable must be passed through. The query string uses SQL syntax to query the database, as captured in the following code, while the connection variable can be declared by using `engine.connect()`.

    ```python
    # Query All Records in the the Database
    data = pd.read_sql("SELECT * FROM Census_Data", conn)
    ```

  * Although SQL can always be used for basic analysis, it is often easier to use Pandas for exploratory analysis and data wrangling.

* Answer any questions before moving on.

---

### 8. Students Do: Read All the SQL (10 min)

**Corresponding Activity:** [04-Stu_Read_All_The_SQL](Activities/04-Stu_Read_All_The_SQLs/)

* You may use the slides to accompany this activity.

* In this activity, the students will query an external server by using Pandas and SQLAlchemy as they work to create new DataFrames based on U.S. Census data.

* Data Source: [US Census Data](https://www.census.gov/developers/).

---

### 9. Review: Read All the SQL (5 min)

Open [Read_All_The_SQLs_solution.ipynb](Activities/04-Stu_Read_All_The_SQLs/Solved/Read_All_The_SQLs_solution.ipynb) within Jupyter notebook, and go through the code line by line, answering any questions the students may have.


---

### 10. Instructor Do: Preview SQLAlchemy with Classes (5 min)

**Corresponding Activity:** [05-Ins_Preview_SQL_Alchemy](Activities/05-Ins_Preview_SQL_Alchemy/)

Use the slides and cover the following talking points:

* So far, the class has been using SQLAlchemy in ways that make it work similarly to SQL. It takes in strings of SQL code and then performs tasks; however, this is not how it is used in most cases.

* Classes are essentially blueprints for Python objects; they allow developers to create organized variables with keys, values, and methods on the fly.

* In the case of SQLAlchemy, we can use classes to make a table blueprint and update the SQL schema.

* Open [SQL_Alchemy_classes_solution.ipynb](Activities/05-Ins_Preview_SQL_Alchemy/Solved/SQL_Alchemy_classes_solution.ipynb) within an Jupyter notebook, and point out how different this code looks compared to the scripts they’ve written so far.

  * First, we import different dependencies as capture by the following code:

    ```python
    # Import the dependencies.
    from sqlalchemy import create_engine
    from sqlalchemy import Column, Integer, String, Float
    from sqlalchemy.ext.declarative import declarative_base
    Base = declarative_base()
    ```

    * When we create the table in the next line of code we will need to define the data types for each column, hence we are importing the following methods: `Column, Integer, String, Float`.

  * Then, we create the two classes, one for each table, as captured by the following code:

     ```python
    # Create a Dog Class for the table.
    class Dog(Base):
        __tablename__ = 'dog'
        id = Column(Integer, primary_key=True)
        name = Column(String(255))
        color = Column(String(255))
        age = Column(Integer)

    # Create a Cat Class for the table.
    class Cat(Base):
        __tablename__ = 'cat'
        id = Column(Integer, primary_key=True)
        name = Column(String(255))
        color = Column(String(255))
        age = Column(Integer)
    ```


  * Point out that it is important for students to understand that SQLAlchemy uses Python classes as its primary means to communicate and make changes to SQL databases. This is what makes SQLAlchemy an ORM—it uses objects to map changes to SQL tables/databases.

  * Run through the remaining code to demonstrate how to add data to each table.

* Let the students know that it is normal to feel intimidated by SQLAlchemy at first. Thankfully, in this lesson, we’ll examine how the library functions, and the whole instructional team will be there to support them as they build their skills with this ORM.

---

### 11. BREAK (15 min)

---

### 12. Instructor Do: A Schooling on Classes (10 min)

**Corresponding Activity:** [06-Ins_Classes](Activities/06-Ins_Classes/)

* Use the slides and cover the following points:

* Once everyone has returned from their break, let the class know that they will now be given a crash course in object-oriented programming.

  * **Object-oriented programming (OOP)** is a style of coding based on the concept of "objects." These objects may contain data, often known as **attributes**, and functions, often known as **methods**.

  * Python is a class-based programming language. This means that objects can be created according to user-created blueprints, thus allowing developers to rapidly create objects of similar structure/purpose but different values.

* Open [dog_class_solution.ipynb](Activities/06-Ins_Classes/Solved/dog_class_solution.ipynb) within Jupyter notebook, and go through the code line by line.

  * To define a class in Python, we simply type `class <ClassName>():`

  * The line `def __init__(self):` is a special method called a **class constructor** that Python calls every time a new instance of the class is created.

  * The parameters declared within `__init__` &mdash; excluding "self" &mdash; must be passed whenever we want to create a new instance of the class. This is because each object's values will be defined by these parameters, as capture in the following code:

    ```python
    # Define a class
    class Dog():

      # Utilize the Python constructor to initialize the object
      def __init__(self, name, color):
          self.name = name
          self.color = color
    ```

  * To create an instance of a class, call the class by using the class name, and pass in whatever arguments its `__init__` method accepts.

  * Users can then access the object's attributes using dot operators with the object. So, in order to call the `name` attribute of an object, we would use `object.name`, as capture in the following code:

    ```python
    # Create an instance of a class
    dog = Dog('Fido', 'brown')

    # Print the object's attributes
    print(dog.name)
    print(dog.color)
    ```

* Go over this code one more time, answering any questions the students may have. Once everyone is comfortable with Python classes, proceed to the next activity.

---

### 13. Students Do: Surfer Class (15 min)

**Corresponding Activity:** [07-Stu_Surfer_Class](Activities/07-Stu_Surfer_Class/)

* You may use the slides to accompany this activity.

* In this activity, the students will create their own classes in Python. More specifically, they will create a `Surfer` class, which they will use throughout the rest of today's lesson.

---

### 14. Review: Surfer Class (5 min)

Open [surfer_class_solution.ipynb](Activities/07-Stu_Surfer_Class/Solved/surfer_class_solution.ipynb) in Jupyter notebook, and go through the code with the class line by line, answering any questions the students may have.

---

### 15. Instructor Do: A Method to the Classes (5 min)

**Corresponding Activity:** [08-Ins_Classes_With_Methods](Activities/08-Ins_Classes_With_Methods/)

Use the slides and cover the following points:

Open [lasses_with_methods_solution.ipynb](Activities/08-Ins_Classes_With_Methods/Solved/classes_with_methods_solution.ipynb) within Jupyter notebook, and go through the code line by line, answering any questions the students may have.

* Creating and attaching methods to Python classes is also easy to accomplish, thus allowing developers to attach regularly used functions to objects of similar types.

* Adding methods to a class is very similar to the `__init__` method discussed earlier: define the function using `def`, provide it with a name, and then pass a list of parameters &mdash; including self &mdash; into the parentheses that follow as captured by the following code:

  ```python
  # Define the Film class
  class Film():

  # A required function to initialize the class object
  def __init__(self, name, length, release_year, language):
      self.name = name
      self.length = length
      self.release_year = release_year
      self.language = language
  ```

* Then, we create a object for the class as follows:

  ```python
  # An object belonging to the Film class
  star_wars = Film("Star Wars", 121, 1977, "English")
  ```

* Next, we define the `Expert()` class as captured by the following code:

  ```python
  # Define the Expert class
  class Expert():

    # A required function to initialize the class object
    def __init__(self, name):
      self.name = name

    # A method that takes another object as its argument
    def boast(self, obj):

        # Print out Expert object's name
        print("Hi. My name is", self.name)

        # Print out the name of the Film class object
        print("I know a lot about", obj.name)
        print("It is", obj.length, "minutes long")
        print("It was released in", obj.release_year)
        print("It is in", obj.language)
  ```

  * The `Expert()` class takes one attribute; `name`. And, has contains another method, `boast()` that takes an `obj`.  We run this method by using the instance of a created object, then use dot notation to reference the method. For example, `doggy.printHello()` would run the `printHello()` method for the `doggy` object. In our case we are using, `obj.name`, `obj.length`, `obj.release_year`, and `obj.language`.

* Then, we create an object belonging to the `Expert` class as follows:

  ```python
  # An object belonging to the Expert class
  superfan = Expert("George Lucas")
  ```

* Finally, we call the object of the `boast()` method in the `Expert()` class using dot notation and pass in the object of the `Film()` class as captured in the following code:

  ```python
  superfan.boast(star_wars)
  ```

* The `boast()` method contained within the `Expert` class takes in the `star_wars` attribute belonging to the `Film()` class and then prints out some statements based on its contents as follows:

  ```text
  Hi. My name is George Lucas
  I know a lot about Star Wars
  It is 121 minutes long
  It was released in 1977
  It is in English
  ```

* Answer any questions before moving on.

---

### 16. Students Do: Surfer Class Extended (10 min)

**Corresponding Activity:** [09-Stu_Surfer_Class_Extended](Activities/09-Stu_Surfer_Class_Extended/)

* You may use the slides to accompany this activity.

* The class will now be reworking their Surfer script from earlier as they add in methods to perform specific tasks.

---

### 17. Review: Surfer Class Extended (5 min)

Open [surfer_extended_solution.ipynb](Activities/09-Stu_Surfer_Class_Extended/Solved/surfer_extended_solution.ipynb) in Jupyter notebook, and go through the code with the class line by line, answering any questions the students may have.

---

### 18. Everyone Do: Back to the SQL (20 min)

**Corresponding Activity:** [10-Ins_SQL_Alchemy_Revisited](Activities/10-Ins_SQL_Alchemy_Revisited/)

* You may use the slides to accompany the beginning of this activity.

* Now that everyone has an understanding of how to create and use Python classes, it’s time to dive back into SQLAlchemy and its class-based methodology.

* For this activity, start with a blank Jupyter notebook, and have the class follow along. By the end of the activity, everyone should have code that looks similar to the code in [Alchemy_annotated_solution.ipynb](Activities/10-Ins_SQL_Alchemy_Revisited/Solved/Alchemy_annotated_solution.ipynb).

* As with most Python code that uses external libraries, the first step is to import the desired modules.

  * `create_engine` allows SQLAlchemy to create connections to SQL databases.

  * `declarative_base` allows SQLAlchemy to convert the classes created in Python to SQL tables.

  * The different data types used in SQL must also be imported into Python from SQLAlchemy. These data types are then used when creating class fields to state what data types each column in the SQL table should contain.

    ```python
    # Dependencies
    # ----------------------------------
    # Imports the method used for connecting to DBs
    from sqlalchemy import create_engine

    # Imports the methods needed to abstract classes into tables
    from sqlalchemy.ext.declarative import declarative_base

    # Allow us to declare column types
    from sqlalchemy import Column, Integer, String, Float
    ```

* The classes created using SQLAlchemy's "Base" class will serve as the anchor points for SQL tables.

  * When creating classes to be used with SQLAlchemy, a `__tablename__` field must be declared and provided with the name of a table. If the table exists, any new objects created will be added into the existing table. If the table does not yet exist, a new table will be created based on the class's fields.

  * Each field of a SQLAlchemy class must be declared as a column, and the data type of the field must also be provided.

  * A primary key can also be set by using the `primary_key` value and setting it to either `True` or `False`, as in the following code:

    ```python
    # Sets an object to utilize the default declarative base in SQLAlchemy
    Base = declarative_base()

    # Creates Classes which will serve as the anchor points for our Tables
    class Dog(Base):
        __tablename__ = 'dog'
        id = Column(Integer, primary_key=True)
        name = Column(String(255))
        color = Column(String(255))
        age = Column(Integer)

    class Cat(Base):
        __tablename__ = 'cat'
        id = Column(Integer, primary_key=True)
        name = Column(String(255))
        color = Column(String(255))
        age = Column(Integer)
    ```

  * Creating instances of SQLAlchemy classes is almost identical to creating regular Python objects, as captured in the following code. It is not necessary to declare fields explicitly within the constructor, but it is a common practice.

    ```python
    # Calls the Pet Constructors to create "Dog" and "Cat" objects
    dog = Dog(name='Rex', color='Brown', age=4)
    cat = Cat(name='Felix', color='Gray', age=7)
    ```

* After the SQLAlchemy classes have been made, they can be created on the SQL database by creating a connection engine and then calling `Base.metadata.create_all(engine)`.

  * The `create_all` code looks through the Python script and checks if the declared classes exist within the database that we are connecting to. If they do not yet exist, the tables will be created at this time, as in the following code:

    ```python
    # Create Database Connection
    # ----------------------------------
    # Creates a connection to our DB
    engine = create_engine("sqlite:///pets.sqlite")
    conn = engine.connect()

    # Create a "Metadata" Layer That Abstracts our SQL Database
    # ----------------------------------
    # Create (if not already in existence) the tables associated with our classes.
    Base.metadata.create_all(engine)
    ```

* SQLAlchemy functions like Git in that new rows of data can be added and changed within a SQL table.

  * A SQLAlchemy session is created with the `Session` module and bound to the connection engine.

  * New rows of data can then be staged by creating a new instance of a SQLAlchemy class and passing them into `session.add()` as a parameter.

  * When all of the desired changes have been made, use `session.commit()` to push them up to the database, as in the following code:

    ```python
    # Session is a temporary binding to our DB
    from sqlalchemy.orm import Session
    session = Session(bind=engine)

    # Add Records to the Appropriate DB
    # ----------------------------------
    # Use the SQL ALchemy methods to run simple "INSERT" statements using the classes and objects
    session.add(dog)
    session.add(cat)
    session.commit()
    ```

* Go through the code as many times as needed to ensure that the class fully understands how to use SQLAlchemy to add new data/tables to a SQL database.

  * Also feel free to point out how simple it is to collect all the data from a SQL table by using SQLAlchemy.

  * Use `session.query()`, and pass in the class or table we want to query as a parameter. The returned data can then be looped through and printed to the terminal, as in the following code:

    ```python
    # Perform a simple query of the database
    dog_list = session.query(Dog)
    for doggy in dog_list:
        print(doggy.name)

    cat_list = session.query(Cat)
    for kitty in cat_list:
        print(kitty.name)
    ```

* Once the students seem comfortable with the script they have just written, go through it one final time and have them describe to you what each line does. When you reach the end of the script, move on to the next activity.

---

### 19. Students Do: Surfing SQL (20 min)

**Corresponding Activity:** [11-Stu_Surfer_SQ](Activities/11-Stu_Surfer_SQL/)

* You may use the slides to accompany this activity.

* In this activity, the students will test their SQLAlchemy skills. Specifically, they’ll turn their `Surfer` class that they created earlier into a new table on a SQL database while also creating a new `Board` class.


---

### 20. Review: Surfing SQL (10 min)

Open [surfer_SQL_solution.ipynb](Activities/11-Stu_Surfer_SQL/Solved/surfer_SQL_solution.ipynb) within Jupyter notebook, and go through the code with the class line by line, answering any questions the students may have.

---

© 2022 edX Boot Camps LLC. Confidential and Proprietary. All Rights Reserved.
