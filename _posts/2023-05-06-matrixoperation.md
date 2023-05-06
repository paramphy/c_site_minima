---
title: "Matrix Operations"
categories:
  - matrix
tags:
  - matrix
  - structure
  - function
toc: true
---
## Problem in section "Matrix Operations" no. 1

Write a programme to add, subtract and multiply two $N\times N$ matrices.

## Answer

### Code

```c++
#include <iostream>

using namespace std;

// Matrix structure definition
struct matrix2d
{
    float mat[100][100];
    int m, n;
};

// Matrix input function
matrix2d matin()
{
    matrix2d a;
    cout << "Input the dimension of the matrix\n";
    cout << "Input m = ";
    cin >> a.m;
    cout << "Input n = ";
    cin >> a.n;

    int i, j;
    cout << "Input the matrix elements\n";
    for (i = 0; i < a.m; i++)
    {
        for (j = 0; j < a.n; j++)
        {
            cout << "Input the element a[" << i + 1 << "][" << j + 1 << "] = ";
            cin >> a.mat[i][j];
        }
    }
    return (a);
}

// Matrix output function
int matout(matrix2d a)
{
    int i, j;
    cout << "Output matrix\n";
    for (i = 0; i < a.m; i++)
    {
        for (j = 0; j < a.n; j++)
        {
            cout << a.mat[i][j] << "\t";
        }
        cout << endl;
    }
    cout << endl;
    return (0);
}
// Matrix addition function
matrix2d addmat(matrix2d a, matrix2d b)
{
    int i, j;
    matrix2d c;
    c.m = a.m;
    c.n = a.n;
    for (i = 0; i < a.m; i++)
    {
        for (j = 0; j < a.n; j++)
        {
            c.mat[i][j] = a.mat[i][j] + b.mat[i][j];
        }
    }
    return (c);
}

// Matrix subtraction function
matrix2d subtmat(matrix2d a, matrix2d b)
{
    int i, j;
    matrix2d c;

    c.m = a.m;
    c.n = a.n;
    for (i = 0; i < a.m; i++)
    {
        for (j = 0; j < a.n; j++)
        {
            c.mat[i][j] = a.mat[i][j] - b.mat[i][j];
        }
    }
    return (c);
}
// Matrix multiplication function
matrix2d multmat(matrix2d a, matrix2d b)
{
    int i, j, k;
    matrix2d c;
    for (i = 0; i < a.m; i++)
    {
        for (j = 0; j < b.n; j++)
        {
            c.mat[i][j] = 0;
        }
    }
    c.m = a.m;
    c.n = b.n;
    for (i = 0; i < a.m; i++)
    {
        for (j = 0; j < b.n; j++)
        {
            for (k = 0; k < a.n; k++)
            {
                c.mat[i][j] = c.mat[i][j] + a.mat[i][k] * b.mat[k][j];
            }
        }
    }
    return (c);
}
// Main function
int main()
{
    matrix2d a, b, c, d, e;
    a = matin();
    b = matin();
    matout(a);
    matout(b);
    if (a.m == b.m && a.n == b.n)
    {
        c = addmat(a, b);
        cout << "Result of addition\n";
        matout(c);
    }
    else
    {
        cout << "The matrices dont have the appropriate dimensions. Please try again.\n";
    }
    if (a.m == b.m && a.n == b.n)
    {
        d = subtmat(a, b);
        cout << "Result of subtraction\n";
        matout(d);
    }
    else
    {
        cout << "The matrices dont have the appropriate dimensions. Please try again.\n";
    }
    if (a.n == b.m)
    {
        e = multmat(a, b);
        cout << "Result of multiplication\n";
        matout(e);
    }
    else
    {
        cout << "The matrices dont have the appropriate dimensions. Please try again.\n";
    }
}
```


### Output
```
Input the dimension of the matrix
Input m = 3
Input n = 3
Input the matrix elements
Input the element a[1][1] = 5
Input the element a[1][2] = 4
Input the element a[1][3] = 5
Input the element a[2][1] = 4
Input the element a[2][2] = 2
Input the element a[2][3] = 5
Input the element a[3][1] = 2
Input the element a[3][2] = 5
Input the element a[3][3] = 5
Input the dimension of the matrix
Input m = 3
Input n = 3
Input the matrix elements
Input the element a[1][1] = 5
Input the element a[1][2] =
4
Input the element a[1][3] = 8
Input the element a[2][1] = 5
Input the element a[2][2] = 1
Input the element a[2][3] = 5
Input the element a[3][1] = 5
Input the element a[3][2] = 2
Input the element a[3][3] = 8
Output matrix
5       4       5
4       2       5
2       5       5

Output matrix
5       4       8
5       1       5
5       2       8

Result of addition
Output matrix
10      8       13
9       3       10
7       7       13

Result of subtraction
Output matrix
0       0       -3
-1      1       0
-3      3       -3

Result of multiplication
Output matrix
70      34      100
55      28      82
60      23      81
```
