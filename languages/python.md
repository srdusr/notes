## Python Programming  
#### Index
Info


#### Documentation
- Official Python Documentation:  
```html
https://docs.python.org  
```
- Unoffical cheatsheets:
```html
https://www.pythoncheatsheet.org
```

- Download docs to use offline  
  - Download offical docs  
  ```bash
  $ curl -OJL https://docs.python.org/3/archives/python-3.9.7-docs-html.tar.bz2
  $ tar -xvf python-3.9.7-docs-html.tar.bz2
  ```
  - After extraction, can navigate to the extracted directory and open the index.html file in a web browser to access the offline Python documentation.  
  - or to generate the documentation for a specific Python module or package, use the following command:  
  ```bash
  $ pydoc -w <module_name>

  ```
> NOTE: Replace <module_name> with the name of the module or package for which to generate documentation. For example, to generate documentation for the os module, can use: `pydoc -w os`. Additionally can use the `-p` option with pydoc to launch a local web server and view the documentation in the web browser. For example: `pydoc -p 5000`. This command will start a web server on port 5000, and can access the documentation by opening the browser and navigating to `http://localhost:5000`.

- To view documentation in vim  
```editorconfig
:help python
```
- - -
#### Info
- Python is an interpreted language, which means it is not compiled but executed line by line.
- Python uses indentation (usually four spaces) to define code blocks. Indentation is important for the structure and readability of code but does greatly effect how the interpreter/runner will run it.
- Follow proper code formatting by using consistent indentation and line breaks.
- Statements are terminated with a newline. However, can use a backslash `\` to continue a statement to the next line.
- Use parentheses to group expressions and clarify the order of operations.
- Use appropriate spacing around operators and after commas to enhance readability.
- Python follows the "PEP 8" style guide, which suggests guidelines for writing Python code. Some key points include:
    - Use descriptive variable and function names.
    - Use lowercase letters with words separated by underscores for variable and function names aka snake_case (e.g., my_variable, my_function).
    - Use uppercase letters with words separated by underscores for constants (e.g., MY_CONSTANT).
    - Use spaces around operators and after commas (e.g., x = 5 + 2, my_function(arg1, arg2)).
    - Limit line length to 79 characters.
- Python supports both single-quoted `'` and double-quoted `"` strings. Consitency is important.
- Python uses zero-based indexing for lists, tuples, and strings. The first element is accessed with index 0.
- Python allows for multiple assignment in a single line, e.g., x, y = 10, 20.
- Avoid using single-character variable names, except in cases where the purpose is clear (e.g., loop counters).
- Follow the DRY (Don't Repeat Yourself) principle and avoid duplicating code. Instead, use functions or loops to encapsulate and reuse code.
- Use built-in functions and libraries whenever possible to leverage existing functionality and improve code efficiency.
- Use meaningful names for variables, functions, and classes that reflect their purpose and intent.
- Use snake_case naming convention for functions, variables, and modules (e.g., my_function, my_variable, my_module.py).
- Use CamelCase naming convention for classes (e.g., MyClass).
- Use a consistent naming convention for constants, such as using uppercase letters with underscores (e.g., MAX_VALUE).
- Avoid using global variables whenever possible, as they can lead to code complexity and make debugging difficult.
- Avoid unnecessary or excessive code comments that only restate the code itself.
- Package Manger
- Virtual Environments
> NOTE: Use virtual environments to distinguish/seperate dependencies between various projects
- A few popular options
  - venv
  - virtualenv (Simple option, this can bring portability to the code and maintain old packages as well.)
  ```bash
  $ virtualenv -p /usr/bin/python3 <env_name>
  $ source yourenv/bin/activate
  $ pip install package-name
  ```
  > NOTE: This environment <env_name> will setup pip to install packages only into this environment, not to the entire system.
  - conda
  - poetry (better option to manage application from start to finish. It is a much better option than requirements.txt + setup.py.)

- - -
#### Setup
- Download and install pip globally
```bash
$ curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
$ python get-pip.py
$ pip --version
```
- Virtual Environments
- - -
#### Basic Syntax
###### Comments
- Python uses the `#` symbol to denote single-line comments.
```python
# This is a single-line comment
```
- Use docstrings (multi-line comments enclosed in triple quotes) to provide documentation for functions, classes, and modules.
```python
"""
This is a
multi-line comment
"""
```
- Use meaningful comments to explain the purpose and functionality of your code.

###### Variables  
- Python has no mandatory declaration of variables. Variables are created when a value is assigned to them.
- Python is case-sensitive (e.g., variable and Variable are different).
- Python uses the `None` value to represent the absence of a value or a null value.
- Python has a dynamic type system, meaning you can reassign variables to different types.

- Declaration and initialization
x = 10

- Declaration without initialization
y = None

###### Data Types
| Data | Type | Description |
|  --- | --- | --- |  
| int | Integer | Represents whole numbers without a fractional component |
| float | Float | Represents real numbers with a single-precision format |
| str | String | Represents a sequence of characters |
| bool | Boolean | Represents a logical value, either True or False |
| list | List | Represents an ordered, mutable collection of elements |
| tuple | Tuple | Represents an ordered, immutable collection of elements |
| dict | Dictionary | Represents a collection of key-value pairs |
| set | Set | Represents an unordered collection of unique elements |

###### Arithmetic Operators
| Operator | Name | Description |
|  --- | --- | --- |  
| x `+` y | Addition | |
| x `-` y | Subtraction | |
| x `*` y | Multiplication | |
| x `/` y | Division | |
| x `%` y | Modulus | |
| x `**` y | Exponentiation | |
| x `//` y | Integer Division | |

###### String Operations
```python
string = "Hello, World!"
len(string)            # Length of string
string.upper()         # Convert to uppercase
string.lower()         # Convert to lowercase
string.strip()         # Remove whitespace
string.split(",")      # Split by comma
```

###### Control Flow  
- Conditional Statements
```python
if condition:
    # Code to execute if condition is true
elif another_condition:
    # Code to execute if another_condition is true
else:
    # Code to execute if neither condition is true
```
- Loops
  - For Loop
  ```python
  for item in iterable:
      # Code to execute for each item in iterable
  ```
  - While Loop
  ```python
  while condition:
      # Code to execute while condition is true
  ```

###### Functions  

```python
def function_name(parameter1, parameter2):
    # Code to execute
    return <result>  # Optional return statement
```

###### Data Structures

- Lists (arrays)
```python
my_list = [1, 2, 3, 4, 5]

my_list.append(6)      # Add item to the end of the list
my_list.insert(0, 0)   # Insert item at a specific index
my_list.remove(3)      # Remove item from the list
my_list.pop()          # Remove and return the last item
my_list.sort()         # Sort the list
```
- Tuples

- Dictionaries
```python
my_dict = {"key1": "value1", "key2": "value2"}

my_dict["key3"] = "value3"  # Add a new key-value pair
del my_dict["key2"]        # Delete a key-value pair
my_dict.keys()             # Get all keys
my_dict.values()           # Get all values
my_dict.items()            # Get all key-value pairs
```

- Sets
```python
my_set = {1, 2, 3}

my_set.add(4)      # Add an element to the set
my_set.remove(3)   # Remove an element from the set
```

- - -
#### Advanced Concepts

- - -
