# Computer Science Notes for Summer 2017

## Table of Contents
<!-- MarkdownTOC -->

- General Topics of CS
    - 
    - ASCII
    - Binary
    - Hexadecimal
    - Recursion
    - Call Stack
- Programming Languages
    - Java
    - C
    - Python
    - JavaScript
    - Lisp
- Object Oriented Programming
- Data Structures
- Algorithms
    - Computational Complexity

<!-- /MarkdownTOC -->


## General Topics of CS

### 

### ASCII

### Binary

### Hexadecimal

#### Introduction
The number system that we currently use is base 10 which represents number 0 to 9. Any numbers greater than 9 uses the concept of placeholder values. Computers instead binary numbers (0 or 1) to represent data. It's difficult to read binary numbers so hexadecimal makes this easier. 

Hexadecimal is a base 16 system (0-9, A-F) where each hexadecimal digit corresponds to an arragement of 4 binary digits (16 combinations). 

|Decimal|Binary|Hexadecimal|
|---|---|---|
|0   |0000   |0   |
|1   |0001   |1   |
|2   |0010   |2   |
|3   |0011   |3   |
|4   |0100   |4   |
|5   |0101   |5   |
|6   |0110   |6   |
|7   |0111   |7   |
|8   |1000   |8   |
|9   |1001   |9   |
|10  |1010   |A   |
|11  |1011   |B   |
|12  |1100   |C   |
|13  |1101   |D   |
|14  |1110   |E   |
|15  |1111   |F   |

In a programming language, you need to explicitly state that you're looking at a hexadecimal number. Most programming languages require you to append 0x in front of the number to state that its a hexadecimal number. Hexadecimal numbers are important to understand since most lower level languages use them in terms of memory addresses. 

#### Conversions

In grade school, we learned that each column of a decimal number corresponds to a power of 10. An example of this is if we show how we can break down this number. 

|Decimal Number|10 ** 2|10 ** 1|10**0|
|---|---|---|---|
|397|3|9|7|
| |300|90|7|

Adding up the final row gives you 300 + 90 + 7 which is 397. We can apply a similar process to hexadecimal numbers for the number 0xADC. 

|Hexadecimal Number|16 ** 2|16 ** 1|16**0|
|---|---|---|---|
|0xADC|10|13|12|
| |2560|208|12|

Adding up the final row gives us 2560 + 208 + 12 = 2780. Going from decimal to hexadecimal is a bit more complicated but isn't that important since binary -> hexadecimal is more useful. However, a process similar to binary -> hexadecimal explained in the binary section above can be used.

When we're looking at binary to hexadecimal, group four binary digits and use the mapping to convert the 4 binary digits to hexadecimal. The same process can be applied when we're looking at hexadecimal to binary. 

### Recursion

Recursion is a method of programming where a function invokes or executes itself to provide an elegant solution. All recursive functions need to meet two cases:
- Base case: terminates the recursive function when condition is met
- Recursive case: recursion will occur

### Call Stack

Each time a function is called, the system sets memory aside for that function and this chunk of memory is usually called a stack frame which lives on the stack. If the main function calls func1() which then calls func2(), all three functions will be on the stack. The most recently called function is always at the top of the stack (active frame). If a new function is called, that will be pushed onto the stack and when a function finishes its work (returns), it'll be popped off the stack and return access to the next frame on the stack and this next frame will pick up from when it called the popped function. 

When a recursive function is called, each recursive function call will be pushed onto the stack. When the base case is met, the recursive function will sequentially pop off each stack frame returning a value to the next stack frame. 

## Programming Languages

### Java

### C

#### Data Types

In C, data types have different memory sizes

| Data Type | Size (bytes) |
|---|---|
|int | 4 |
|char | 1 |
|float| 4|
|double|8|
|long long| 8|
|char*, int*, etc| 4 or 8|

The last line is 4 or 8 because it depends if its a 32 bit system or 64 bit system. That's how much memory you could there


#### Pointers

Pointers in C provide a different way to share data among data structures and functions. C usually passes data by value which is a copy of the data (exception is arrays) but the use of pointers actually allows us to pass the actual variable itself instead of a copy. Copies of values dont allow us to properly modify values using functions. Pointers and computer memory are heavily interrelated. 

Data storage typically occurs on HDD's or SSD's but manipulation of data can only occur in RAM so data must be moved there. Memory can be seen as a big array of byte sized cells and each cell has a memory access. 

When we declare a variable, the system will choose a space in memory that is equivalent to the data type. So if we declare an int variable, it will give us 4 bytes of memory. 

A key point (hah) is that all pointers are essentially addresses. The first lines initializes a variable k to the value of 5 with a memory address that is assigned by the system. 

```c
int k = 5; 
int* pk; 
pk = &k;
```

The second line gives an overview on declaring a pointer. int* pk means that we are declaring a pointer pk where the address of pk will contain a value of type int. pk = &k assigns the pointer pk the memory address of k (& is memory address of variable k). Using this concept, we're essentially passing a memory address of a value to a specific function instead of passing the value which is a copy to the function. 


One way to create a pointer is similar to the code segment above by extracting the address of a variable which already exists using the address extraction operator(&). If x is an int-type variable, then &x is a pointer-to-int whose value is the address of x. 

Dereferencing is the way to modify the location to which a pointer points to. The derefencing operator is (*) which accesses the data at the memory location allowing us to manipulate it.  If we have a pointer to char pc, then *pc is the dereferencing operator which gives us the data stored at memory address inside variable pc. 

The NULL pointer points to nothing in C. It's important to always set a pointer to NULL if not immediately initializing the pointer. The default value of a pointer is not NULL. Attempting to dereference a NULL pointer will return a segmentation fault. This is good since we don't want to accidentally derefence a memory location with data we shouldn't be accessing. 

```c
int* p;
```

This line declares a pointer p which is an address and it point to a value of type int. You can derefence p with the * operator. The *s can be part of both the data type as well as the pointer name. 

```c
pk = &k;
*pk = 35;
```

If we assume the value of k is the same as it was originally. The first line says that pk gets the address of k and points there. Then go to the address that is pointed to by pk and change the value to 35. 

#### File Pointers

Files are useful to get input from files and also write to files to maintain relevant information. Working with files in C is done by file pointers (FILE*). File manipulation functions are in stdio.h and FILE* is the parameter to all the functions except for fopen() which is used to create a file pointer.
```c
FILE* ptr = fopen("file1.txt", "r");
```
The second argument of fopen could writing(w), reading(r), appending(a) which will start writing from the end of the file instead of writing which overwrites all previous written information. 
```c
fclose(ptr);
```
Fclose() cloeses the file. 

Read the stdio.h documentation for more functions on files such as fgetc(), fputc(), fread(). 

#### Arrays

In C, arrays must have a fixed size when declaring an array so the computer system knows how much memory to assign for the variable. All elements of the array must be of the same type. 

Key: There is no string in C. This is actually a char* which is a pointer to the beginning of the array whose values are characters. 

#### Dynamic Memory Allocation
Dynamic memory allocation provides access to memory that is allocated while the program is running using pointers. This memory comes from the heap whereas previously, memory came from the stack. The stack and heap are generally part of the same section of memory but different terms. 

The function used for malloc(bytes) will return a pointer to the memory or return NULL if memory couldnt be provided. 

```c
// Single Integer declarations
int x; // static declaration
int *px = malloc(sizeof(int)); // dynamic declaration of memory with size of a single int

// Array Declarations
float stack_array[x]; // Static declaration
float* heap_array = malloc(x * sizeof(float)); // Dynamic declaration which allocates x * float size memory
```

With static memory, all of the memory that was used on the stack as part of a function gets returned once you're done with the function. However, in dynamic memory, the memory is not returned once finished with the function which can result in memory leak. Free() can free any memory that is dynamically assigned. 

#### Structures

Structures allow us to group variables of different data types into a single variable name. A simple syntax example of structure is
```c
struct car {
    int year;
    char model[10];
    char plate[7];
    int odometer;
    double engine_size;
};
```
The variables inside the car struct are fields or members of the struct. 
Structures are usually defined in a header file (.h) which can then be included into your main file. The dot operator is used to access the members of the struct. 

```c
struct car mycar; // variable declaration of type struct

// field accessing
mycar.year = 2011;
mycar.odometer = 50505;
```

Structures can have memory dynamically allocated to them instead of statically allocated. 

```c
// variable declaration using malloc
struct car *mycar = malloc(sizeof(struct car));

// field accessing
(*mycar).year = 2011;
(*mycar).odometer = 50505;
```

The last two lines shows how to access a field using dynamically allocated memory or a pointer. There is a far more efficient way to access the field which is by using the arrow operator (->). 

```c
// Arrow operator
mycar->year = 2011;
mycar->odometer = 50505;
```

The arrow operator first dereferences the pointer on the left side of the operator and then accesses the field on the right side of the operator. 

#### Custom Data Types

It's possible to define custom data types at the top of .c or .h files using the typedef keyword. Typedef redefines a new custom data keyword. 

```c
typedef char* string; // Redefines a char* pointer to a string

typedef struct car {
    int year;
    char model[10];
    char plate[7];
    int odometer;
    double engine_size;
}
car_t;
// Above is essentially equivalent but we've also defined the structure within
typedef struct car car_t;
```

Creating a custom data type using typedef for a struct simplifies the initialization process. An example is

```c
// No typedef used
struct car mycar;

// Typedef used
car_t mycar;
```

### Python

### JavaScript

### Lisp

## Object Oriented Programming

## Data Structures

## Algorithms

### Computational Complexity

Computational Complexity is used to determine how an algorithm will scale with very large input data. The worst case scenario of an algorithm is known as Big O notation. You can measure an algorithm by its ability to measure how it handles inputs. It's more important to care about the tendency of an algorithm and not the exact function associated with the algorithm. This tendency is defined by the highest order term since the lower order terms are not as effective with very large inputs. 

Common Big O complexity:
- O(1): constant time
- O(log n): logarithmic time
- O(n): linear time
- O(n log n): linearithmic time
- O(n**2): quadratic time
- O(n**c): polynomial time
- O(c**n): exponential time
- O(n!): factorial time
- O(infinity): infinite time