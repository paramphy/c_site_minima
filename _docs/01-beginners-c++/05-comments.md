---
title: "Comments"
permalink: /docs/comments/
last_modified_at: 2023-02-08
redirect_from:
  - /theme-setup/
toc: true
---
Program comments are explanatory statements that you can include in the C++ code. These comments help anyone reading the source code. All programming languages allow for some form of comments.

C++ supports single-line and multi-line comments. All characters available inside any comment are ignored by C++ compiler.

C++ comments start with /* and end with */. For example −

```c++
/* This is a comment */

/* C++ comments can also
   * span multiple lines
*/
```

A comment can also start with //, extending to the end of the line. For example −

```c++
#include <iostream>
using namespace std;

main() {
   cout << "Hello World"; // prints Hello World
   
   return 0;
}
```

When the above code is compiled, it will ignore // prints Hello World and final executable will produce the following result −

```
Hello World
```
Within a /* and */ comment, // characters have no special meaning. Within a // comment, /* and */ have no special meaning. Thus, you can "nest" one kind of comment within the other kind. For example −

```c++
/* Comment out printing of Hello World:

cout << "Hello World"; // prints Hello World

*/
```
## Why use Comments?

If we write comments on our code, it will be easier for us to understand the code in the future. Also, it will be easier for your fellow developers to understand the code.

**Note:** Comments shouldn't be the substitute for a way to explain poorly written code in English. We should always write well-structured and self-explanatory code. And, then use comments.

As a general rule of thumb, use comments to explain Why you did something rather than How you did something, and you are good.