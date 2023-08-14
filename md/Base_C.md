C language basics
================

## **Table of contents**
* [Data types and operators](#data type and operator)
     * [variable name](#variable name)
     * [data type](#data type)
     * [type conversion](#type conversion)
     * [Bit Operations](#Bit Operations)
* [array and pointer](#array and pointer)
     * [pointer-base](#pointer-base)
     * [various types of pointers](#various types of pointers)
     * [two-dimensional array and pointer](#two-dimensional array and pointer)
     * [Application of function pointer - callback](#Application of function pointer - callback)
* [struct](#struct)
     * [struct](#struct)
     * [byte alignment](#byte alignment)
     * [typedef](#typedef)
     * [Differences between structures and unions](#Differences between structures and unions)
     * [Application example of structure](#Application example of structure)
* [Macro definition and preprocessor] (#Macro definition and preprocessor)
     * [define](#define)
     * [FILE CONTAINS](#FILE CONTAINS)
     * [macro replacement](#macro replacement)
     * [macro function](#macro function)
     * [Condition contains](#Condition contains)
* [variable modifier](#variable modifier)
     * [const](#const)
     * [static](#static)
     * [volatile](#volatile)
     * [register](#register)

## **Data types and operators**
### variable name
* The variable name is composed of letters and numbers, and must start with a letter, and the underscore _ is regarded as a letter.
* Use lowercase for variables and uppercase for constants.

### type of data  
* C language only provides the following data types

|Type|Description|
|:-----|:----|
|char |Character type: occupies one byte|
|int |Integer, usually reflecting the most natural length of an integer on the machine|
|float |single-precision floating point|
|double|double-precision floating-point type|


* short and long
     The short and int types must be at least 16 bits, and the long type must be at least 32 bits, and the short type must not be longer than the int type, and the int type must not be shorter than long.
The length of each data on a typical 32-bit processor is as follows:

|Type|16-bit platform (Bytes)|32-bit platform (Bytes)|64-bit platform (Bytes)|
|:-------:|:-:|:-:|:-:|
|char |1|1|1|
|short |2|2|2|
|int |2|4|4|
|long |4|4|8|
|long long|8|8|8|
|float |4|4|4|
|double |8|8|8|


* unsigned and signed
     unsigned: unsigned number, encoding range 0 to (2^w - 1)
     signed (default): complement encoding, encoding range -(2^(w-1)) to (2^(w-1)-1)

* enumeration constant
The enumeration starts from zero by default, the second is 1, and increments in turn
```C
enum {
     NO,
     YES
}
```

## Type Conversion
* In the arithmetic operation expression, the low type will be converted to the high type
**priority**
     ![](https://img-blog.csdn.net/20170616200811277?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvUUNaVFpTV1QzNTc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve /70/gravity/SouthEast)
* In the assignment operator, the value of the expression on the right is automatically and implicitly converted to the value of the variable on the left
* In the transfer of parameters in the function call, the system implicitly converts the actual parameter into the type of the formal parameter and assigns it to the formal parameter
* When the function has a return value, the system implicitly converts the value of the return expression to the return value type

## bitwise operations
|operator|action|
|:-----:|:-----:|
| & |Bitwise AND|
| \| |Bitwise OR|
|^ |Bitwise XOR|
| << |move left|
| \>> |shift right|
| ~ |Bitwise inversion|

* Common skills
1. Get the specified bit of a number
```C
     unsigned char a = 0xF3;
     a &= 0x0F;//take the lower 4 bits
```
2. For a certain position of the data 1
```C
     unsigned char a = 0xF3;
     a |= 0x08;//The 4th position is 1
```
3. For a position of data 0
```C
     unsigned char a = 0xF3;
     a &= ~0x08;//4th position 0
```
4. A certain 1 position is 0 or 1
```
     #define setbit(X,Y) X |= (1<<Y)
     #define clrbit(X,Y) X &= ~(1<<Y)
```

## **Arrays and pointers**
### Pointer Basics
* Pointer: **The pointer is the address of the program data in the memory, and the pointer variable is the variable used to save these addresses. The memory space occupied by the pointer variable is related to the system, which is sizeof(void*)**

### Various types of pointers
```C
     int *p; //pointer to int
     int **p; //Double pointer, pointing to a pointer of type int
     int *p[10]; //Array of pointers, the elements of the array are pointers to int type
     int (*p)[10]; //Array pointer, pointing to an array containing 10 int elements
     int *fun(void); //fun function, the parameter is void, and the return value is a pointer to int type
     int (*fun)(void);//function pointer, pointing to a function whose parameter is void and the return value is int
```

### Two-dimensional array and pointer
* Base
   * Multidimensional arrays are essentially simulated by one-dimensional arrays
   * The array name is a constant, representing the first address of the first element of the array
   * The array is arranged continuously, for example: a[2][3] is equivalent to *(*(a+2)+3)
   * Perform the address operation (&) on the array name, the type is an array type, for example: int a[2][3];int (*p)[2][3] = &a;
   * The sizeof operation is performed on the array name, and the return value is the size of the entire array.
   * When an array is used as a function parameter, it will degenerate into a pointer.

* example
```C
     int a[2][3]={{1,2,3},{a,b,c}};
     int (*p)[3] = a; //a is the first address of the first element of the two-dimensional array, pointing to an array containing 3 int elements.
     int (*p1)[2][3] = &a; //take the address of a, which represents the address type of a two-dimensional array, that is, int (*)[2][3];
     int *p2 = a[0]; //a[0] is equivalent to a one-dimensional array name, that is, the address of the first element
     int (*p3)[3] = &a[0]; // Take the address of the one-dimensional array name, which means the address type of the one-dimensional array, that is, int (*)[3];
     int *p4 = &a[0][0]; // take the address of int type
     int p5 = a[0][0]; //int type
```

### Application of function pointer - callback
     * Callback definition: The provider provides the corresponding method. When a specific event or condition occurs, the other party calls it. In C language, it is realized by passing a function pointer as a parameter.
     * example
         * Sort

## **Structure**
### Structure
* Definition: A structure is a collection of one or more variables, which can be of different types.
* General form:
```C
     struct Student
     {
         int age;
         char* name;
     };
```
* Three definition methods
```C
     //Define the structure class line first, then define the structure variable
     struct Student
     {
         int age;
         char* name;
     };
     struct Student Bob;
    
     //Define structure type and variable at the same time
     struct Student
     {
         int age;
         char *name;
     }Bob;
    
     //Directly define the structure variable
     structure
     {
         int age;
         char *name;
     }Bob;
     //The structure type does not allocate memory, but the structure variable allocates memory.
```
### byte alignment
* Definition: In modern computers, various types of data are arranged in the memory space according to certain rules, rather than sequentially discharged one by one.
* meaning
     * Different hardware handles storage space differently, and some platforms can only read specific types of data from specific addresses.
     * Reasonable memory alignment can improve access efficiency.
* The principle of structure alignment
     * **Specify the alignment value, subject to the specified alignment value**
     * **The first address of the structure variable can be divisible by the size of its widest basic type member**
     * **The offset of each member of the structure relative to the first address of the structure is an integer multiple of the size of the member**
     * **The total size of the structure is an integer multiple of the size of the widest basic type member of the structure**
eg:
```C
     typedef struct{
         char a;
         short b;
         char c;
         int d;
         char e[3];
     }T_Test;
     sizeof(T_Test);//16
     Offset a = 0 b = 2
             c = 4 d = 8
             e[1] = 12
```
* Change the alignment manually
     * #pragma pack(n): The compiler aligns with n bytes
     * #pragma pack(): The compiler cancels the custom byte alignment


### typedef
* Definition and function
A typedef declaration does not essentially create a new type, it just adds a new name to an existing type. Similar to #define, but the typedef is interpreted by the compiler.
* Common method
```C
     //portability requirements
     typedef unsigned char INT8U;
     typedef signed char INT8S;
                 ...
     //struct
     typedef struct tnode
     {
         char *name;
         struct tnode *left;
         struce tnode *right;
     }Treenode;//Treenode structure
     typedef struct tnode * Treeptr;//Treeptr: pointer to Treenode structure
     //function pointer
     typedef void* (*Fun)(void*);//Fun: a function pointer type whose return value is void* and whose parameter is void*.
```
### [Bit Field](https://blog.csdn.net/lovecodeless/article/details/23270911 "Bit Field Blog")
* definition
     If space resources are precious, bit fields can be used instead of flag bit sets, and multiple data can be stored in one machine word.
```C
     structure
     {
unsigned a:20;
unsigned: 0; //0 field, indicating that the next bit field is on the next machine word boundary
unsigned c:2;
     }flags;
```
* Precautions
     * Bit fields can only use three types: int, unsigned int, and signed int.
     * Bit fields need to pay attention to the range of use, the number of digits determines the range
     * The bit field is accessed through the number, such as flags.a, the bit field has no independent address, cannot be accessed, and cannot be operated by sizeof
     * Bit fields are stored in machine words in the order of declaration. Bit fields cannot be stored across machine words. If there is insufficient space in the previous machine word, all the fields are stored in the next machine word.

### The difference between structure and union
* the difference
     * In a structure, each member variable has its own memory space, and the total length of a structure variable is the sum of the lengths of each member.
     * In a union, each member variable shares a section of memory space, and the length of a union variable is equal to the longest length of each member.
     * In a union, only one member can be assigned a value at a time. After assigning a value to it, the value of the original member will become invalid.


### Application example of structure
* linked list
* queue
* stack
* Binary tree

## **Macro definition and preprocessor**
### Definition
     * The preprocessor is a separate first step in the compilation process
     * The macro is just a simple replacement in the C preprocessing stage
### The file contains
`#include " "`
`#include<>`

### Macro Replacement
`#define name replace_text`
     * identifier alias
```C
     #define BUFFER_SIZE 1024
     //Macro body needs to add a backslash at the end of the line \
     #define NUMBERS 1,\
                     2,\
                     3
```
### macro function
`A macro with parentheses after the macro name is considered a macro function, and the macro function will be expanded during the preprocessing stage. Compared with ordinary functions, the execution efficiency will be improved, but the code size is large, there is no syntax check, and it is more dangerous`

     * Pay attention to the problem: complete replacement, no grammar check, please pay attention to the following situations
         1. Operator priority, complete replacement, it is best to add parentheses such as `#define ADD(x,y) ((x)+(y))`
         2. Semicolon engulfment: When macro functions use loops, it is recommended to use do while instead of for and while;
         3. The macro parameter is called repeatedly. If the macro function is like `#define min(X,Y) ((X) < (Y) ? (X) : (Y))`, then call `min(x+y,foo( z))`, it will be expanded into `((x+y) < (foo(z)) ? (x+y) : (foo(z))), foo function is executed twice,
         4. For recursive calls to itself, the macro will only expand once. If `#define foo(4+foo)`, `foo` expands to `4+foo`, foo will not be recognized.
        
### Condition contains
     * Avoid repeated inclusion of header files
     `#ifndef XXX_H`
     `#define XXX_H`
     * Conditional compilation, macros can be used to adapt to multiple environments, and DEBUG can be configured
```C
     //conditional compilation
     #define CPU_A
     //#define CPU_B
     #if define CPU_A
         CPU_A(XXXXX);
     #elif define CPU_B
         CPU_B(XXXXX);
     #else
         CPU_O(XXXXX);
     #endif
     //DEBUG
     #define DEBUG
     #if define DEBUG
         DEBUG(XXXXX);
     #endif
```

## **variable modifiers**
### const
     * Definition: The keyword const is used to define constants. If a variable is modified by const, its value cannot be modified.
     * advantage
         * It can protect the modified variables to prevent accidental modification and increase the robustness of the program.
         * Compiler optimization (saved in the symbol table) to improve efficiency
     * Typical usage
         * Modifies local variables, and the value of n cannot be changed.
         `const int n = 5;`
         `int const n = 5;`
         * Modify the constant string to ensure that when s[1] is assigned a value, an error will be reported when compiling.
         `const char* s = "abcdefg;"`
         * Constant pointer: the content pointed to by the pointer is constant
         `const int *p;`
         `int const *p;`
             * The constant pointer cannot change the value of the variable through this pointer, but the value of the variable can be changed in other ways
             * The content pointed to by the constant pointer cannot be changed, but the value of the pointer itself can be changed.
            
             ```C
                 int a = 1;
                 int b = 2
                 const int *p = &a;
                 a = 3;
                 p = &b;
             ```
         * Pointer constant: The pointer itself is constant and cannot point to other addresses.
         `int *const p;`
             * The address pointed by the pointer constant itself cannot be changed, but the value in the address can be changed
            
             ```C
                 int a = 0;
                 int *const p = &a;
                 *p = 5;
             ```
         * A constant pointer pointing to a constant: the pointer itself cannot be modified, and the value pointed to cannot be modified, but the value of the variable can be changed through other pointers
             `const int *const p`
            
         * Modification parameters
             * Prevent the content pointed to by the pointer from being modified
             `void cmp(const char *s1, const char *s2)`
             * Prevent modification of the address pointed to by the pointer
             `void swap(int *const p1,int *const p2)`
         * Modified return value: If the return value is a constant pointer, it can only be assigned to a constant pointer of the same type.
         `const char * GetString(void);`
         * Modify all variables: prevent global variables from being modified.
        

### static
     * Modify local variables
         * Local variables modified by static are not placed in the stack memory, but placed in the static storage area. So it will not be released with the end of the function call.
         * static local variables will only be initialized at the first time, and can only be initialized once, if not initialized, it will default to 0;
     * Modify global variables and functions
         * Global variables and functions modified by static can only be accessed in the current source file, which can hide data and reduce system coupling.
    
###volatile
     * A variable modified by volatile means that it will reload data directly from memory instead of copying the content from the register.
     * In some cases, the value of the variable may be changed unexpectedly, such as the variable in the interrupt or the value of the hardware register, but due to compiler optimization, the program may still read the copy in the register, in order to ensure that each read and write Both are read from the source address and need to be modified with volatile.
### register
     * The data is directly stored in the register. When it needs to be accessed, it does not need to be addressed in the RAM. The direct register addressing is fast and can improve the operating efficiency.
     * The data is placed in the register, and the address (&) operation cannot be performed on the register variable.

    
  



