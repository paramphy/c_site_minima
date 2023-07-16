---
title: "Errors"
permalink: /docs/errors/
last_modified_at: 2023-04-17
redirect_from:
  - /theme-setup/
toc: true
---
In C or C++, we face different kinds of errors. These errors can be categorized into five different types. These are like below −

- Syntax Error
- Run-Time Error
- Linker Error
- Logical Error
- Semantic Error

Let us see these errors one by one −

## Syntax error
This kind of errors are occurred, when it violates the rule of C++ writing techniques or syntaxes. This kind of errors are generally indicated by the compiler before compilation. Sometimes these are known as compile time error.

In this example, we will see how to get syntax error if we do not put semicolon after one line.
### Example
```c++
#include<stdio.h>
main() {
   printf("Hello World")
}
```
#### Output

```
Error] expected ';' before '}' token
```

## Runtime error

This kind of errors are occurred, when the program is executing. As this is not compilation error, so the compilation will be successfully done. We can check this error if we try to divide a number with 0.

### Example

```c++
#include<stdio.h>
main() {
   int x = 52;
   int y = 0;
   printf("Div : %f", x/y);
}
```
#### Output
```
Program crashes during runtime.
```

## Linker error

This kind of errors are occurred, when the program is compiled successfully, and trying to link the different object file with the main object file. When this error is occurred, the executable is not generated, For example some wrong function prototyping, incorrect header file etc. If the main() is written as Main(), this will generate linked error.

### Example
```c++
#include<stdio.h>
main() {
   int x = 52;
   int y = 0;
   printf("Div : %f", x/y);
}
```
#### Output

```
C:\crossdev\src\mingw-w64-v3-git\mingw-w64-crt\crt\crt0_c.cundefined reference to `WinMain'
```
## Logical error

Sometimes, we may not get the desired output. If the syntax and other things are correct, then also, we may not get correct output due to some logical issues. These are called the logical error. Sometimes, we put a semicolon after a loop, that is syntactically correct, but will create one blank loop. In that case, it will show desired output.
### Example
```c++
#include<stdio.h>
main() {
   int i;
   for(i = 0; i<5; i++); {
      printf("Hello World");
   }
}
```
#### Output

Here we want the line will be printed five times. But only one time it will be printed for the block of code.

## Semantic error

This kind of error occurs when it is syntactically correct but has no meaning. This is like grammatical mistakes. If some expression is given at the left side of assignment operator, this may generate semantic error.

### Example
```c++
#include<stdio.h>

main() {
   int x, y, z;
   x = 10;
   y = 20;
   x + y = z;
}
```
#### Output
```
[Error] lvalue required as left operand of assignment
```