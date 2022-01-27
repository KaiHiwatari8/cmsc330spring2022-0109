# Discussion 1 - Friday, January 28<sup>th</sup>

## Introduction (5 minutes)



1. Welcome to CMSC330!
2. Tips for getting a good grade in 330:
    1. Start projects early! Roughly 40% of your grade is projects. Some individual projects may be worth as much as 8%, which means if you get 50/100 on the project, you're already losing half a letter grade! Conversely, you can excel at projects and really boost your grade.
    2. Use previous quizzes and exams. They are up on the course website and they're highly representative of all the quizzes and exams we'll have this semester.
    3. Come to class and discussion. We'll be showing some really cool examples.
    4. Please ask us conceptual questions in office hours. TAs love getting questions like "I don't understand X, could you clarify it for me please?".
    5. You may attend any discussion that you want. 
3. Often, students run into similar problems, or have similar questions. Make sure to check Piazza before coming to office hours for answers to your questions. Use the Piazza search bar before posting a new question.
4. Project deadlines are available on the website and on the project READMEs
5. Earlier yesterday we posted a note on Piazza (@113) detailing how we will be grading projects for this class. There are more details on the note so please check that out, but basically it will be your responsibility to check that the grade you have on ELMS is the correct one. We may make mistakes with project gradinng, so just be aware of ensuring your grade is what you are expecting.

## What is CMSC330? (5 minutes)



* The goal is to develop tools that make programming easier - to abstract away the technicalities of the machine so application development is quicker
* This involves understanding some type of language, and converting that into machine-understandable terminology
    * Combines ideas from linguistics and logic, among other fields
* How do we approach this? 
    * Two case studies of languages (Ruby and OCaml), each of which has different strengths, weaknesses, and uses. Key idea is to know when to use what type of language
    * Understand what goes on under the hood of programming languages (PL); how do PLs understand programs (parsing) and perform execution based on this (operational semantics, lambda calculus)
    * Look to the future of programming languages (Rust); what problems are there, and how can we tackle them? 

## Problem Solving Exercise (30 minutes)

&lt;Database exercise from Fall 2021> 

Keep the following parts: 



1. Tuple Init, getData, numTuples
2. Table: Initialize, insertTuple
3. New method for Table: numRowsWhere, which counts the number of rows where a particular column = some value 

In the introduction, add an example of a table: 
 

## Introduction

We created a Ruby exercise which has you work with some of the features you learned about in class. The focus here is on the problem solving process itself, and particularly the following steps: 



1. Problem Understanding: can you break down a set of instructions into manageable tasks
2. Algorithmic Planning: can you develop pseudocode or a sketch of the code 
3. Implementation and information retrieval: can you implement the solution, and more importantly, find resources to help you (documentation) when stuck

We'll walk you through some of these steps for some parts of the problem, and have you work your own way through others. 

We will be implementing a simple database using Ruby data structures to store the data. A database is used to store data in an ordered manner, and an example is shown above. A database consists of a set of columns (in this case name and age), and some number of tuples (in this case, 4 tuples). Each tuple has a value for each column; for example, the first tuple in the database, (A,22), corresponds to a datapoint with name A and age 22. In particular, we plan to implement features for the database so users can read and write data. 

An example of a table is below: 
Name | Age | 

---------------------

A    |  22        

B    |  23       

C    |  24          

D    |  21   

## Part 1: `Tuple`

A `Tuple` represents a single entry, in a table.  The methods below will be implemented in the `Tuple` class in [disc1.rb](src/disc1.rb).

#### `initialize(data)`

- **Type**: `(Array) -> _`
- **Description**: Given an array of values for the tuple, store them in the `Tuple` object in any way you would like.  You should perform any initialization steps for the `Tuple` instance here.  The return value of this function does not matter.
- **Examples**:
  ```ruby
  t = Tuple.new(["a", 1, "b", 2])
  t = Tuple.new([])                # Tuples may be empty 
  ```

#### `getData(index)`

- **Type**: `(Integer) -> Object`
- **Description**: Return the data at a particular index of a `Tuple` (indexed starting at 0).  If the provided index exceeds the largest index in the tuple, return `nil`.
- **Assumptions**: `index` is non-negative.
- **Examples**:
  ```ruby
  t = Tuple.new(["a", 1, "b", 2])
  t.getData(0)                     # Returns "a"
  t.getData(4)                     # Returns nil
  ```

#### `self.getNumTuples(n)`

- **Type**: `(Integer) -> Integer`
- **Description**: Return the number of `Tuple`s of size `n` that have ever been created.  Hint: you should use a static variable to keep track of this.
- **Examples**:
  ```ruby
  Tuple.getNumTuples(3)         # Returns 0
  t = Tuple.new(["a", 1, "b"])
  t = Tuple.new(["a", 1, "b"])
  Tuple.getNumTuples(3)         # Returns 2
  t = Tuple.new([3])
  Tuple.getNumTuples(3)         # Returns 2
  ```
  
## Part 2: `Table`
A `Table` represents a collection of tuples.  The methods below will be implemented in the `Table` class in [disc1.rb](src/disc1.rb).

#### `initialize(column_names)`

- **Type**: `(Array) -> _`
- **Description**: Given an array of column names for the `Table`, store them in the object in any way you would like. You should perform any initialization steps for the `Table` instance here.  The return value of this function does not matter.
- **Assumptions**: The elements in `column_names` will be unique.
- **Examples**: 
  ```ruby
  t = Table.new(["c0", "c1", "c2"])
  t = Table.new([])
  ```

#### `insertTuple(tuple)`

- **Type**: `(Tuple) -> boolean`
- **Description**: Insert a `Tuple` into the `Table`.  Note that the number of entries in the `Tuple` must match the number of columns in the `Table`.  If this is not the case, make no changes to the `Table` and return `false`.  If the sizes match, insert the `Tuple` and return `true`.
- **Examples**:
  ```ruby
  table = Table.new(["a", "b"])
  x = Tuple.new([0, 1])
  y = Tuple.new([3, "y"])
  z = Tuple.new([1, 2, 3])

  table.insertTuple(x)  # Returns true
  table.insertTuple(y)  # Returns true
  table.insertTuple(z)  # Returns false (sizes do not match)
  ```

#### `numRowsWhere`

- **Type**: `(String,'t) -> Integer`
- **Description**: Given a column name and a value, find the number of rows where the value for the column matches the given value. 
- **Examples**
  ```ruby 
    table = Table.new(["a", "b"])
    x = Tuple.new([0, 1])
    y = Tuple.new([3,,1])
    z = Tuple.new([3,,4])
    table.insertTuple(x)
    table.insertTuple(y)
    table.insertTuple(z)
    table.numRowsWhere("b",1) # 2 
  ```


**Debugging Exercise (10 minutes) **

We'll show you a few tips on how to debug issues when/if you run into issues with your projects. We'll make some small modifications to our code so it doesn't run, then go through techniques to find the error, such as: 



1. Creating test cases
2. Finding where the error occurs 
3. Fixing the error

Emphasize the problem solving process as much as possible; if they can learn to tackle projects + debug themselves, then they'll be better off for projects 
