## Arrays
### Declaration
```cpp
// Declaring an array that holds 10 integers
int array[10];

// To access a specific element in an array you
// use an index to define which position in the array
// you want the access the value of
// An index is a sequential value that starts with 0
array[0] // Access the first element of an array
array[2] // Access the third element of an array

// To assign a value to a specific position in the array
array[2] = 5; // Assign value 2 to the third element of the array
```
### Looping through an array and printing its values
```cpp
int array[5] = {1, 2, 3, 4, 5};

for (int index = 0; index < 5; index++) {
    printf("%d, ", array[index]); // Output: 1, 2, 3, 4, 5, 
}
```
### Arrays can have different types
```cpp
float array1[5] = {1.0, 2.0, 3.0, 4.0, 5.0};
double array2[5] = {1.0, 2.0, 3.0, 4.0, 5.0};
char array3[5] = {"h", "e", "l", "l", "o"};
```
An array of characters can also be called a ***string***
### Important points
- You can not change the size of an array after declaration
---
## Strings
A string is an array of characters with a specific size
```cpp
char buffer[50] = "Hello world!";
```
Consider a buffer that can hold up to 5 bytes
```cpp
char buffer[5];
```
The previous statements reserves 5 bytes in the memory that contains only null characters

| 0 | 1 | 2 | 3 | 4 |
|---|---|---|---|---|
| '\0' | '\0' | '\0' | '\0' | '\0' |

a buffer (string) can be assigned a value using the `strcpy`  function, but to do that we must first include the `string.h` library
```cpp
#include <string.h>
```
```cpp
strcpy(buffer, "hell");
```
| 0 | 1 | 2 | 3 | 4 |
|---|---|---|---|---|
| 'h' | 'e' | 'l' | 'l' | '\0' |

The structure of `strcpy` function is as follows
```
strcpy ( dest, src )
```
where src is the source of what will be copied
and dest is the destination to replace the value with

### How to define an array of strings
We must use a 2D array
```cpp
// Define an array that can hold 3 buffers of size 50
char arrayOfStrings[3][50];
char pokemons[3][50] = {
    "pikachu",
    "charzard",
    "squirtle"
};
```
### Looping through an array of strings and printing their values
```cpp
// By using %s as a formatter for printf
for (int i = 0; i < 3; i++) {
    printf("%s\n", pokemons[i]);
}
// By using %c as a formatter for printf
for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 50; j++) {
        printf("%c", pokemons[i][j]);
        if (pokemons[i][j] == '\0') break;
    }
    printf("\n");
}
```

### Concatenating two strings
To concatenate two strings, `strcat` is used, where the first argument is the destination buffer, and the second argument is the source buffer
```cpp
char str1[50] = "Hello";
char str2[50] = " World!";

strcat(str1, str2) // str1 becomes "Hello World!"
```

### Comparing two strings
To compare between two strings (for ordering purposes for example), we use `strcmp` function
```cpp
char str1[3] = "AAA";
char str2[3] = "BBB";

strcmp(str1, str2); // -1
strcmp(str2, str1); // 1
strcmp(str1, str1); // 0
```

### Important points
- All functionalities of an array applies to strings
- Once the value of a string is assigned, its value can only be changed by using `strcpy` function

---
## Pointers
Pointers are variales that hold the address of another variable in the memory
```cpp
int* integerPointer;
float* floatPointer;
char* charPointer;
```
To assign the address of a variable to a pointer, we use the `&` operator
```cpp
int x = 5;

int* px = &x;
```
Here, `px` is a pointer that points to `x`
```cpp
printf("%p", px); // Prints the address of x
printf("%d", *px); // Prints the value of x (what px points to)
```
To get the value that the pointer points to, we use the `*` operator
### Using pointers with arrays
```cpp
int sequence[5] = {1, 2, 3, 4, 5};
int* current = sequence;
```
#### Why don't we use `&` with arrays?
In essence, arrays are pointers, so the variable `sequence` is actually a special pointer that points to multiple memory cells (addresses) that are reserved for the array, so if we use `&` with an array like the following
```cpp
int* current = &sequence;
```
This way, we are actually pointing `current` to the address of the pointer to the array, not the array itself

So, when we declare it like the following
```cpp
int sequence[5] = {1, 2, 3, 4, 5};
int* current = sequence;
```
This way, we are making `current` point to the first element of the array

To print the value that `current` points to, we use the `*` operator
```cpp
printf("%d", *current) // Output: 1
```

### Moving the pointer through an array
To move the pointer, we can just add the value of movement to it
```cpp
// To change what current points to, just increment the address by how much you want to move it
current += 2;
printf("%d", *current); // Output: 3
// To use the value of a specific sequence element without changing what current points to
printf("%d", *(current + 2)); // Output: 3
```
### Using pointers in strings
The same idea applies to strings (since they are an array of characters)
```cpp
// Printing a string using pointers
char buffer[50] = "Hello world";
char* current = buffer;

while (*current != '\0') {
    printf("%c", *current);
    current++;
}
```
```cpp
// Printing a string without spaces
char buffer[50] = "Hello world";
char* current = buffer;

while (*current != '\0') {
    if (*current != ' ')
        printf("%c", *current);
    current++;
}
```

### Important points
- When an `if` statement doesn't define its scope, the scope of the `if` statement is the next statement only

---
## Structs
Structs are a way to group similar data attributes together in one data structure
```cpp
// Declaring a struct
struct Pokemon {
    int level;
    char name[50];
}

// Declaring a new variable of type Pokemon
struct Pokemon newPokemon;
// Or
Pokemon newPokemon;
```
To access any attribute of the struct, we use the `.` (dot) operator
```cpp
newPokemon.level = 5;
strcpy(newPokemon.name, "Charzard");
```
The attributes of a struct can be treated as normal variables, and all functionalities are applied to it

---
## Functions
Functions are groups of statements that perform a specific task
```cpp
// This function prints "Hello"
void sayHello() {
    printf("Hello");
}
```
Sometimes, functions can return a specific value back to its caller
```cpp
int returnTwo() {
    return 2;
}
float returnTwoWithFloatingPoint() {
    return 2.0;
}
```
And to call a function, we just write its name with the paranthesis `()`
```cpp
sayHello();
returnTwo();
returnTwoWithFloatingPoint();
```
To make use of the returned value of a function (if any), we can either store it in a variable, or use it immediately somewhere
```cpp
int returnedValue = returnTwo();
// returnedValue is now 2
float returnedFloatValue = returnTwoWithFloatingPoint();
// returnedFloatValue is now 2.0
```
The return type `void` is similar to `null` in the sense that it doesn't contain a value, whereas `null` can be described as a value, `void` is described as no value

Even when `void` is used as a return type, we can still use `return` to end the function execution
```cpp
void voidFunction() {
    return; // Note that no value is returned
}
```
Functions can have arguments that are passed on function call (from the outside)
```cpp
float circleArea(float r) {
    return 3.14 * ((r / 2) ** 2);
}
float squareArea(float width, float height) {
    return width * height;
}

float circle = circleArea(30);
float area = squareArea(12, 8);
```
Imagine using structs with functions
```cpp
struct Rectangle {
    float width;
    float height;
}

float rectArea(struct Rectangle rect) {
    return rect.width * rect.height;
}

// ⬇️ in main

struct Rectangle rect;
rect.width = 20;
rect.height = 10;

float area = rectArea(rect);
```

## Exercises

### E1
Replace comments with the correct segments of code
```cpp
// Prints the value of str
void printMessage(char* str) {
    while(*str != '\0') {
        // ???
        str++;
    }
}
```
```cpp
void main() {
    // squaredSequence must have he following values
    // 1, 4, 9, 16, 25, ..., n^2
    // where n = 1, 2, 3, 4, ..., 30
    int squaredSequence[30];

    for (int i = 1; i <= 30; i++) {
        // ???
    }
}
```
```cpp
void main() {
    // Print the buffer without vowel letters (a, e, o, u, i)
    char buffer[100] = "Hello world";
    char* current = buffer;

    while (current != '\0') {
        // ??? (Multiple statements)
    }
}
```
