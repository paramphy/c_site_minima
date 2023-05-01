---
title: "Matrix operations"
categories:
  - matrix
tags:
  - matrix
  - data
  - structure
toc: true
---
## Problem in section "Matrix Operations" no. 1
Write a C++ program to evaluate the sum, difference and product of two given matrices of order N X N.

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
    cout << "Input the dimentsion of the matrix\n";
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
    if (a.m == b.m && a.n == b.n)
    {
        for (i = 0; i < a.m; i++)
        {
            for (j = 0; j < a.n; j++)
            {
                c.mat[i][j] = a.mat[i][j] + b.mat[i][j];
            }
        }
        return (c);
    }
    else
    {
        cout << "The matrices dont have the same dimensions. Please try again.\n";
    }
}
// Matrix subtraction function
matrix2d subtmat(matrix2d a, matrix2d b)
{
    int i, j;
    matrix2d c;
    if (a.m == b.m && a.n == b.n)
    {
        for (i = 0; i < a.m; i++)
        {
            for (j = 0; j < a.n; j++)
            {
                c.mat[i][j] = a.mat[i][j] - b.mat[i][j];
            }
        }
        return (c);
    }
    else
    {
        cout << "The matrices dont have the same dimensions. Please try again.\n";
    }
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

    if (a.n == b.m)
    {
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
    else
    {
        cout << "The matrices dont have the appropriate dimensions. Please try again.\n";
    }
}
// Main function
int main()
{
    matrix2d a, b, c, d, e;
    a = matin();
    b = matin();
    matout(a);
    matout(b);
    c = addmat(a, b);
    cout << "Result of addition\n";
    matout(c);
    d = subtmat(a, b);
    cout << "Result of subtraction\n";
    matout(d);
    e = multmat(a, b);
    cout << "Result of multiplication\n";
    matout(e);
}

```

### Output
```
Input the dimentsion of the matrix
Input m = 2
Input n = 3
Input the matrix elements
Input the element a[1][1] = 1
Input the element a[1][2] = 5
Input the element a[1][3] = 4
Input the element a[2][1] = 6
Input the element a[2][2] = 8
Input the element a[2][3] = 4
Input the dimentsion of the matrix
Input m = 3
Input n = 2
Input the matrix elements
Input the element a[1][1] = 5
Input the element a[1][2] = 4 
Input the element a[2][1] = 8
Input the element a[2][2] = 1
Input the element a[3][1] = 5
Input the element a[3][2] = 6
Output matrix
1       5       4
6       8       4

Output matrix
5       4
8       1
5       6

The matrices dont have the same dimensions. Please try again.
Result of addition
Output matrix
5       4
8       1
5       6
```
```
