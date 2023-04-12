---
layout: post
author: Angel
date: 2023-03-14T22:50:11-05:00
title: "Hands-on with Python"
tags: ["python", "programming", "devops", "git", "github", "automation", "html", "css", "javascript", "web framework", "webapp"]
description:
showToc: true
TocOpen: false
hidemeta: false
comments: true
disableHLJS: false # to disable highlightjs
disableShare: true
hideSummary: false
searchHidden: false
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
UseHugoToc: false
draft: false
---

[Python](https://www.python.org/) is a high-level, interpreted programming language that is widely used for web development, data analysis, artificial intelligence, and other applications. 

It has a clean syntax and is easy to learn, making it a great choice for beginners as well as experienced developers.

Here's a quick overview from [Fireship.io](https://fireship.io/).

{{< ytlazy x7X9w_GIm1s >}}


## Overview

### Variables and Data Types

In Python, variables are used to store values such as numbers, strings, and other data types. 

To assign a value to a variable, you simply use the "=" sign. 

For example, to assign the value 5 to a variable called "x", you would write:

```python
x = 5
```

Python has several built-in data types:
- integers (whole numbers)
- floats (decimal numbers)
- booleans (represent `True` or `False`)
- strings (used to represent text)
- lists (used to store collections of values)

```python
# Examples of data types in Python
a = 5         # integer
b = 3.14      # float
c = True      # boolean
d = "Hello"   # string
e = [1, 2, 3] # list
```

### Control Flow

Control flow refers to the way that a program executes its instructions based on certain conditions. 

Python uses `if-else` statements and `loops` to control the flow of a program.

An `if-else` statement is used to execute certain code if a certain condition is met, and other code if it is not. 

For example:

```python
x = 5
if x > 10:
    print("x is greater than 10")
else:
    print("x is less than or equal to 10")
```

A `loop` is used to repeat a certain block of code a certain number of times, or until a certain condition is met. 

For example:

```python
# While loop
i = 0
while i < 5:
    print(i)
    i += 1

# For loop
for i in range(5):
    print(i)
```

### Functions

Functions are used to group together a certain block of code that can be called and executed multiple times throughout a program. 

A `function` can take in certain parameters and can return a certain value. 

Example:

```python
# Function that adds two numbers
def add_numbers(x, y):
    return x + y

result = add_numbers(3, 4)
print(result)
```

Output:

```python
7
```

### Modules

Modules are used to group together certain functions and variables that can be imported and used in other Python programs. 

Python has a large number of built-in modules that provide useful functionality, such as the `math` module for performing mathematical calculations. 

You can also create your own modules to organize your code and make it more reusable.

Example:

```python
import math

x = math.sqrt(25)
print(x)
```

Output:

```python
5
```

## Web Frameworks

Frameworks provide a set of libraries and tools to help developers build web applications more quickly and easily, typically by provideing a set of features, such as routing, templating, database integration, and security, that are common to most web applications

### Flask

[Flask](https://palletsprojects.com/p/flask/) is one of the popular web frameworks for building web applications in Python, it is lightweight, flexible and provides tools and libraries for handling HTTP requests, rendering templates, managing sessions, and interacting with databases.

### Django

[Django](https://www.djangoproject.com/), on the other hand, is a full-stack framework, meaning it provides many similar built-in tools and features as Flask, but includes more, it is usually better suited for building large, complex web applications with a lot of functionality.

### Other Notable Frameworks

- [Pyramid](https://trypyramid.com/)
- [CherryPy](https://cherrypy.dev/)
- And a lot [more](https://www.geeksforgeeks.org/top-7-python-frameworks-to-learn-in-2022/)...

## Package Management

The [Python Package Index (PyPI)](https://pypi.org/) is a repository of software for the Python programming language.

PyPI helps you find and install software developed and shared by the Python community. You can [learn more about installing packages](https://packaging.python.org/installing/) on the PyPi packaging documentation. 

## Build a Simple Calculator

Now that we have covered some of the basics of Python, let's create a simple calculator program. 

We'll create a program that will take in two numbers and perform simple operations on them, such as addition, subtraction, multiplication, or division.

### Create Your Python File

1. Create a `.py` file, in this case, we can call it `simple_calculator.py`.
2. Copy and paste the following code:

```python
# define a function for each operation
def add(x, y):
    return x + y

def subtract(x, y):
    return x - y

def multiply(x, y):
    return x * y

def divide(x, y):
    if y != 0:
        return x / y
    else:
        return "Error: Division by zero"

# get input from the user
x = float(input("Enter the first number: "))
y = float(input("Enter the second number: "))

# display menu of available operations
print("Select operation:")
print("1. Add")
print("2. Subtract")
print("3. Multiply")
print("4. Divide")

# get user's choice of operation
choice = input("Enter choice (1/2/3/4): ")

# perform the selected operation
if choice == '1':
    print(x, "+", y, "=", add(x, y))
elif choice == '2':
    print(x, "-", y, "=", subtract(x, y))
elif choice == '3':
    print(x, "*", y, "=", multiply(x, y))
elif choice == '4':
    print(x, "/", y, "=", divide(x, y))
else:
    print("Invalid input")
```

This should give us a simple calculator we can play around with, it utilizes Python's built-in calculator module, which means we don't have to define all the operators and such.

### Run

```sh
python simple_calculator.py
```

You'll be prompted to enter a `first number` and a `second number`, then from there you can select which operation to perform on these two numbers.

It would look something like this:

```sh
Enter the first number: 254
Enter the second number: 127
Select operation:
1. Add
2. Subtract
3. Multiply
4. Divide
Enter choice (1/2/3/4): 3
254.0 * 127.0 = 32258.0
```

Awesome! Now you've built yourself a handy calculator in Python that works in your CLI!

## Build a Calculator App for the Web Using Flask

What we'll do next is re-create the calculator app in the web browser and we'll utilize Flask to run this calculator as a web app, giving us more of a graphical way to interact with it.

### Install Flask

```sh
pip install Flask
```

### Create Your Python File

Create your python file, in this case, we can call it `web_calculator.py`, but you can name it anything you want.

```python
from flask import Flask, request, render_template

app = Flask(__name__)

@app.route("/")
def home():
    return render_template("index.html")

@app.route("/calculate", methods=["POST"])
def calculate():
    operation = request.form["operation"]
    x = float(request.form["x"])
    y = float(request.form["y"])
    result = None

    if operation == "add":
        result = x + y
    elif operation == "subtract":
        result = x - y
    elif operation == "multiply":
        result = x * y
    elif operation == "divide":
        if y != 0:
            result = x / y
        else:
            result = "Error: Division by zero"

    return render_template("index.html", result=result)

if __name__ == "__main__":
    app.run(debug=True)
```

Here, we have defined two routes. The first route, "/", displays a simple HTML form that allows the user to input two numbers and select an operation. 

The second route, "/calculate", is called when the form is submitted and performs the selected operation on the two numbers.


### Build the HTML file

1. Create an `index.html` to include our new code for the calculator app.
2. Create a folder titled `templates`, and move your `index.html` file into it.

```html
<!DOCTYPE html>
<html>
<head>
    <title>Calculator</title>
</head>
<body>
    <h1>Calculator</h1>

    <form method="post" action="/calculate">
        <label for="x">Num #1:</label>
        <input type="number" name="x" required>

        <label for="y">Num #2:</label>
        <input type="number" name="y" required>

        <br>

        <label for="operation">Operation:</label>
        <select name="operation">
            <option value="add">Add</option>
            <option value="subtract">Subtract</option>
            <option value="multiply">Multiply</option>
            <option value="divide">Divide</option>
        </select>

        <br><br>

        <input type="submit" value="Calculate">
    </form>

    {% if result %}
        <h2>Result: {{ result }}</h2>
    {% endif %}
</body>
</html>
```


### Run

```
python web_calculator.py
``` 

This will start a local web server that you can access in your web browser at:

```
http://localhost:5000
```
Now you've set up a simple calculator with Python and Flask that runs on the browser!

![img](/images/python/img1.webp)

#### Add In Some CSS (Optional)

If you wish to make the design of the calculator look a bit nicer, you could write up a `css` file for it.

1. In the same directory as your `.py`, create a folder titled `static`.
2. Inside this folder create your `css` file, you can call it `style.css`.

You can use the template below to give the web app a material design look:

```css
/* Set the font family and size */
body {
  font-family: Roboto, sans-serif;
  font-size: 16px;
}

/* Add padding to the body */
body {
  padding: 24px;
}

/* Center the calculator heading */
h1 {
  text-align: center;
}

/* Add some margin between form elements */
form {
  margin-top: 16px;
  margin-bottom: 16px;
}

/* Style the input fields */
input[type="number"] {
  border: none;
  border-bottom: 1px solid #ccc;
  outline: none;
  padding: 8px;
  font-size: 16px;
}

/* Style the select element */
select {
  border: none;
  border-bottom: 1px solid #ccc;
  outline: none;
  padding: 8px;
  font-size: 16px;
}

/* Style the submit button */
input[type="submit"] {
  background-color: #2196F3;
  color: white;
  border: none;
  padding: 8px 16px;
  font-size: 16px;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}

input[type="submit"]:hover {
  background-color: #1976D2;
}

/* Style the result heading */
h2 {
  text-align: center;
}
```

Now make sure to go back to your `index.html` file and link the newly created `style.css` by adding it inside of the `<head>`.

```html
<link rel="stylesheet" type="text/css" href="{{ url_for('static', filename='style.css') }}">
```

You should now see your calculator with a more polished look:

![img](/images/python/img6.webp)

That's it! You now have a simple calculator web app that you can use to perform calculations in your web browser.

You can always use your built-in calculator on your system, but we all know it's not as cool as one that we can build!

### Quick Tip

If you wish to version control your code after building such an awesome app, check out how to use [Git](/posts/2023-03/getting-started-with-git/) and push it to a central source like [GitHub](https://github.com). 

Fore example, you can always check out the [code](https://github.com/netsparse/python-web-calc) for this project.

## Conclusion

Overall, Python is awesome and helpful because it is versatile, easy-to-learn, and has a thriving community that supports its development and growth. 

Its many benefits make it an excellent choice for anyone who wants to learn a powerful and widely-used programming language and build potentially cool stuff with it.

## Learn More
- [Official Documentation](https://docs.python.org/3/index.html)
- [Python Library Reference](https://docs.python.org/3/library/index.html)
- [Python Tutorial](https://docs.python.org/3/tutorial/index.html)

### Additional
- [Python 4 Everybody (PY4E)](https://www.py4e.com/lessons)
- Al Sweigart's [Automate The Boring Stuff with Python](https://automatetheboringstuff.com/)
- [Fireship.io](https://fireship.io/lessons/code-this-not-that-python-edition/)
- [Python Open Source CS Degree GitHub Resource](https://github.com/ForrestKnight/open-source-cs-python)
- [OSSU CS](https://github.com/ossu/computer-science)
- [David Beazley's Python Course](https://dabeaz-course.github.io/practical-python/)
- [Full Stack Python](https://www.fullstackpython.com/)
- [YouTube (Corey Schafer)](https://m.youtube.com/playlist?list=PL-osiE80TeTt2d9bfVyTiXJA-UTHn6WwU)
