 ### C Programming

##### Basic Syntax
- Comments
 // This is a single-line comment

 /* This is a
    multi-line comment */
- Variables

    // Declaration and initialization
    int x = 10;

    // Declaration without initialization
    float y;
- Data Types
|Data Type| Description|
| --- | --- | --- |
    |int| Integer
    |float| Floating point number
    |double|  Double precision floating point number
    |char|  Character
    |bool|  Boolean
    |Operators|
    |Operator|  Description
    |=| Assignment|
    |+| Addition|
    |-| Subtraction|
    |*| Multiplication|
    |/| Division|
    |%| Modulus| (remainder after division)
    |==|  Equality|
    |!=|  Inequality|
    |<| Less than|
    |>| Greater than|
    |<=|  Less than or equal to|
    |>=|  Greater than or equal to|
    |&&|  Logical AND|
    |` 
    |!| Logical NOT|
    Control Structures
    Conditional Statements
    c
    Copy code
    if (condition) {
        // code block to execute if condition is true
    } else if (anotherCondition) {
        // code block to execute if anotherCondition is true
    } else {
        // code block to execute if neither condition is true
    }
    Loops
    For Loop
    c
    Copy code
    for (initialization; condition; update) {
        // code block to execute repeatedly while condition is true
    }
    While Loop
    c
    Copy code
    while (condition) {
        // code block to execute repeatedly while condition is true
    }
    Do-While Loop
    c
    Copy code
    do {
        // code block to execute at least once
    } while (condition);
    Switch Statements
    c
    Copy code
    switch (expression) {
        case value1:
            // code block to execute if expression equals value1
                break;
                  case value2:
                      // code block to execute if expression equals value2
                          break;
                            default:
                                // code block to execute if expression does not equal any specified value
                                    break;
    }
    Functions
    c
    Copy code
    // Function prototype
    returnType functionName(argumentType argumentName);

    // Function definition
    returnType functionName(argumentType argumentName) {
        // code block to execute
          return returnValue;
    }
    Arrays
    c
    Copy code
    // Declaration and initialization
    int arrayName[size] = {value1, value2, value3};

    // Accessing elements
    int element = arrayName[index];
    Pointers
    c
    Copy code
    // Declaration and initialization
    int *pointerName = &variableName;

    // Accessing value through pointer
    int value = *pointerName;`



