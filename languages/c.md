## C Programming  

### Hello World!

```c
#include <stdio.h> // [Include libraries (standard input/output library)]
/*
|--------------------- [Return type is an integer(int), if not specified will default to int]
|   |----------------- [Function (main)]
|   |   |------------- [Argument list (none)]
V   V   V*/
int main()
{ //<---------- [Statements, braces({}) encapsulates a block of code but can be ommited if there is only a single line, each statement will have a statement terminator which is a semi-colon(;)]
    /*|*/  printf("Hello, World!\n");  // [Prints 'Hello, World!' to the console (display output)]
    /*|*/  return 0;                   // [Return value, signals successful completion of the program/end of the function (exit code 0)]
} //<-|
/*
`#include <stdio.h>`: This line is a preprocessor directive that includes the standard input/output library (stdio.h). It allows the program to use input/output functions like printf.
`int`: Return Type, the int before main() indicates that the function returns an integer value. The value returned from main() serves as an exit status code that is usually returned to the operating system to signal whether the program executed successfully or encountered an error.
`main()`: Declares the main function, which serves as the entry point of the program. All other functions in the program are typically called from main.
`printf("Hello, World!\n");`: The printf function is used to output the string "Hello, World!\n" to the console. The \n is an escape sequence representing a newline character, moving the cursor to the next line after printing.
`return 0;`: Return Value, this line marks the end of the main function and the program. It returns an exit status of 0 to the operating system, indicating successful execution.
*/
```

### Basic Syntax  
###### Comments  
```c  
 // This is a single-line comment  
  
 /* This is a  
    multi-line comment */  
```  
  
###### Variables  
- All variables must be declared before used, usually at the beginning of the function before any executable statements. A declaration announces the properties of the variables, it consists of a type name and a list of variables
```c  
// Declaration and initialization  
int x = 10;  
  
// Declaration without initialization  
float y;  
```  

 ###### Data Types  

| Data | Type | Description|  
|  --- | --- | --- |  
| int | Integer | Represents whole numbers without a fractional component |  
| float | Floating point number | Represents real numbers with a single-precision format |  
| double | Double precision floating point number | Represents real numbers with a double-precision format |  
| char | Character | Represents a single character, such as a letter or symbol (single byte) |  
| bool | Boolean | Represents a logical value, either true or false |  
| short | Short integer |  
| long | Long integer |  

 ###### Operators  
- Arithmetic Operators:

| Operator | Name | Description |   
|  --- | --- | --- |  
| + | Addition | Adds two operands |  
| - | Subtraction | Subtracts the right operand from the left operand |  
| * | Multiplication | Multiplies two operands |  
| / | Division | Divides the left operand by the right operand |  
| % | Modulus (remainder after division) | Computes the remainder after division of two operands |  

  - Assignment Operators:

| Operator | Name | Description |   
|  --- | --- | --- |  
| = | Assignment | Assigns a value to a variable |  
| += | Addition Assignment | Adds right operand to the left operand and assigns the result to the left operand |
| -= | Subtraction Assignment | Subtracts right operand from the left operand and assigns the result to the left operand |
| *= | Multiplication Assignment | Multiplies the left operand by the right operand and assigns the result to the left operand |
| /= | Division Assignment | Divides the left operand by the right operand and assigns the result to the left operand |
| %= | Modulus Assignment | Computes the modulus of the left operand with the right operand and assigns the result to the left operand |

  - Comparison Operators:

| Operator | Name | Description |   
|  --- | --- | --- |  
| == | Equality | Checks if two operands are equal |  
| != | Inequality | Checks if two operands are not equal |  
| < | Less than | Checks if the left operand is less than the right operand |  
| > | Greater than | Checks if the left operand is greater than the right operand |  
| <= | Less than or equal to | Checks if the left operand is less than or equal to the right operand |  
| >= | Greater than or equal to | Checks if the left operand is greater than or equal to the right operand |  

  - Increment and Decrement Operators

| Operator | Name | Description |   
|  --- | --- | --- |  
| ++ | Increment | Increments the value of a variable by 1 |
| -- | Decrement | Decrements the value of a variable by 1 |

  - Bitwise Shifters

| Operator | Name | Description |   
|  --- | --- | --- |  
| << | Left Shift | Shifts the bits of the left operand to the left by the number of positions specified by the right operand |
| >> | Right Shift | Shifts the bits of the left operand to the right by the number of positions specified by the right operand |

  - Bitwise Operators

| Operator | Name | Description |   
|  --- | --- | --- |  
| &  | Bitwise AND | Performs bitwise AND operation |
| \| | Bitwise OR | Performs bitwise OR operation |
| ^  | Bitwise XOR | Performs bitwise XOR (exclusive OR) operation |
| ~  | Bitwise NOT | Inverts the bits |

  - Logical Operators

| Operator | Name | Description |   
|  --- | --- | --- |  
| && | Logical AND | Performs logical AND operation |  
| \|\| |Logical OR | Performs logical OR operation |  
| ! | Logical NOT | Negates the value of a condition |  

- - -  
  
###### Control Structures  
- Conditional Statements  
```c  
if (condition) {  
    // code block to execute if condition is true  
} else if (anotherCondition) {  
    // code block to execute if anotherCondition is true  
} else {  
    // code block to execute if neither condition is true  
}  
```  
- Switch Statements  
```c  
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
```  
- For Loop  
```c  
for (initialization; condition; update) {  
    // code block to execute repeatedly while condition is true  
}  
```  
  
- While Loop  
```c  
while (condition) {  
    // code block to execute repeatedly while condition is true  
}  
```  
  
- Do-While Loop  
```c  
do {  
    // code block to execute at least once  
} while (condition);  
```  
  
- - -  
  
###### Functions  
```c  
// Function prototype  
returnType functionName(argumentType argumentName);  
  
// Function definition  
returnType functionName(argumentType argumentName) {  
    // code block to execute  
      return returnValue;  
}  
```  
  
- - -  
  
###### Arrays  
```c  
// Declaration and initialization  
int arrayName[size] = {value1, value2, value3};  
  
// Accessing elements  
int element = arrayName[index];  
```  
  
- - -  
  
##### Pointers  
```c  
// Declaration and initialization  
int *pointerName = &variableName;  
  
// Accessing value through pointer  
int value = *pointerName;`  
```  
- - -

###### Input/Output:  
- printf("Text");             // Prints text on the console  
- scanf("%d", &<variable>);   // Reads input from the user  

- - -

###### Memory Allocation:  
- malloc(size);     // Allocates a block of memory  
- calloc(n, size);  // Allocates an array of n elements, initialized to zero  
- free(pointer);    // Deallocates the memory block  

- - -

###### Preprocessor Directives:
- #include <header_file>     // Includes a header file  
- #define <macro_name> <value>   // Defines a macro  

- - -
