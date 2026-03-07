# Working with Numeric Data Types

## Overview

In this lab, I explored Python's core numeric data types by working through practical exercises in the AWS Cloud9 IDE. I learned how to use the Python shell for immediate execution, and then progressed to writing Python scripts that demonstrated the characteristics of integers, floating-point numbers, complex numbers, and Boolean values. By the end of this lab, I could confidently work with Python's numeric type system and understand how each type stores and represents data.

## Topics Covered

- Executing Python commands in the interactive shell
- Performing arithmetic operations (addition, subtraction, multiplication, division)
- Declaring and assigning variables
- Using built-in functions (`print()`, `type()`, `str()`)
- Understanding the `int` data type for whole numbers
- Understanding the `float` data type for decimal numbers
- Understanding the `complex` data type for imaginary numbers
- Understanding the `bool` data type and its relationship to integers

## Introducing the Technologies

### AWS Cloud9 IDE
AWS Cloud9 is a cloud-based integrated development environment that runs in the browser. It provides a full terminal, file editor, and debugger—everything I needed to write and execute Python code without any local setup.

### Python Built-in Functions
Python provides several standard functions for working with data:

| Function | Purpose | Example |
|----------|---------|---------|
| `print()` | Output values to the console | `print(myValue)` |
| `type()` | Return the data type of an object | `type(myValue)` |
| `str()` | Convert a value to a string | `str(42)` returns `"42"` |

### Python Numeric Data Types

| Data Type | Description | Example | Use Case |
|-----------|-------------|---------|----------|
| `int` | Whole numbers (positive, negative, zero) | `1`, `-5`, `0` | Counting, indexing |
| `float` | Numbers with decimal points | `3.14`, `-0.5`, `2.0` | Measurements, calculations |
| `complex` | Numbers with real and imaginary parts | `5j`, `3+4j` | Advanced mathematics |
| `bool` | True or False values (1 or 0) | `True`, `False` | Conditional logic |

## Tasks

### Task 1: Set Up the Cloud9 Environment

1. I accessed the AWS Cloud9 IDE through the AWS Management Console
2. I created a new Python file from the template menu by selecting **File > New From Template > Python File**
3. I removed the sample boilerplate code
4. I saved the file with a descriptive name (`numeric-data.py`) in the `/home/ec2-user/environment` directory
5. I opened a new terminal session by clicking the **+** icon and selecting **New Terminal**

✅ **Task complete:** Cloud9 environment was ready with a Python file and terminal session.

### Task 2: Use the Python Shell

I opened the interactive Python shell by entering the command:

```bash
python3
```

I then executed several arithmetic operations to understand how Python handles basic math:

| Operation | Command | Result |
|-----------|---------|--------|
| Addition | `2 + 2` | `4` |
| Subtraction | `4 - 2` | `2` |
| Multiplication | `2 * 2` | `4` |
| Division | `4 / 2` | `2.0` |

📝 **Note:** Division in Python 3 always returns a float, even when dividing evenly.

I exited the shell by entering:

```bash
quit()
```

✅ **Task complete:** Successfully performed arithmetic operations in the Python interactive shell.

### Task 3: Work with the int Data Type

I wrote the following code to my Python file to explore integers:

```python
print("Python has three numeric types: int, float, and complex")

myValue=1
print(myValue)
print(type(myValue))
print(str(myValue) + " is of the data type " + str(type(myValue)))
```

I saved the file and executed it by clicking the **Run** button in the IDE. The output confirmed:

```
Python has three numeric types: int, float, and complex
1
<class 'int'>
1 is of the data type <class 'int'>
```

I could also run the script from the terminal:

```bash
python3 numeric-data.py
```

💭 **Consider:** Variables are like labeled boxes—the label (`myValue`) stays the same, but I can store different types of data in it.

✅ **Task complete:** Successfully created and ran a Python script demonstrating the `int` data type.

### Task 4: Work with the float Data Type

I added the following code to my Python file:

```python
myValue=3.14
print(myValue)
print(type(myValue))
print(str(myValue) + " is of the data type " + str(type(myValue)))
```

I saved and ran the file. The output now included:

```
3.14
<class 'float'>
3.14 is of the data type <class 'float'>
```

⚠️ **Caution:** The `int` data type only stores whole numbers. To work with decimal values, I must use `float`.

✅ **Task complete:** Successfully demonstrated the `float` data type with decimal numbers.

### Task 5: Work with the complex Data Type

I added the following code to my Python file to work with complex numbers:

```python
myValue=5j
print(myValue)
print(type(myValue))
print(str(myValue) + " is of the data type " + str(type(myValue)))
```

I saved and ran the file. The output included:

```
5j
<class 'complex'>
5j is of the data type <class 'complex'>
```

📝 **Note:** Complex numbers in Python use `j` to represent the imaginary unit (equivalent to `i` in mathematics). The format can be `5j` (purely imaginary) or `3+4j` (real and imaginary parts).

✅ **Task complete:** Successfully demonstrated the `complex` data type.

### Task 6: Work with the bool Data Type

I added the following code to my Python file:

```python
myValue=True
print(myValue)
print(type(myValue))
print(str(myValue) + " is of the data type " + str(type(myValue)))

myValue=False
print(myValue)
print(type(myValue))
print(str(myValue) + " is of the data type " + str(type(myValue)))
```

I saved and ran the file. The final output was:

```
Python has three numeric types: int, float, and complex
1
<class 'int'>
1 is of the data type <class 'int'>
3.14
<class 'float'>
3.14 is of the data type <class 'float'>
5j
<class 'complex'>
5j is of the data type <class 'complex'>
True
<class 'bool'>
True is of the data type <class 'bool'>
False
<class 'bool'>
False is of the data type <class 'bool'>
```

💭 **Consider:** The `bool` data type is technically a subset of `int` in Python—`True` equals `1` and `False` equals `0`. While other languages treat it as a separate type, Python implements it as a "fake" data type.

✅ **Task complete:** Successfully demonstrated all Python numeric data types, including `bool`.

## Conclusion

I successfully completed this lab and achieved the following:

- ✅ Executed Python commands interactively in the shell
- ✅ Performed arithmetic operations and understood operator behavior
- ✅ Created and ran Python scripts in the Cloud9 IDE
- ✅ Worked with variables and understood the `type()` function
- ✅ Mastered the `int` data type for whole numbers
- ✅ Mastered the `float` data type for decimal numbers
- ✅ Mastered the `complex` data type for imaginary numbers
- ✅ Mastered the `bool` data type for True/False values
- ✅ Used string concatenation with `str()` to format output

This lab provided a foundational understanding of Python's numeric type system, which is essential for writing robust data processing and mathematical programs.

## Additional Resources

- [Python Official Documentation](https://docs.python.org/3/)
- [Python Data Types](https://docs.python.org/3/library/stdtypes.html)
- [AWS Cloud9 User Guide](https://docs.aws.amazon.com/cloud9/latest/user-guide/)
- [AWS Training and Certification](https://aws.amazon.com/training/)
