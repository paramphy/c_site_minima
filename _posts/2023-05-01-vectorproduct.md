---
title: "Vector products and vector identities"
categories:
  - vector
tags:
  - vector
  - structure
  - function
toc: true
---
## Problem in section "Vector and Tensor Operations" no. 3
Write a C++ programme to implement dot product, cross product, scalar-triple product and vector triple-product of any given three dimensional vectors. Also proof the vector triple product identity
$$(\vec A \times\vec B \times \vec C) + (\vec C \times\vec A \times \vec B)+(\vec B \times\vec C \times \vec A)=0$$

## Answer

### Code

```c++
#include <iostream>
using namespace std;

// Vector structure definition
struct vector
{
    float i, j, k;
};

// Dot product function
float dot(vector x, vector y)
{
    float z;
    z = x.i * y.i + x.j * y.j + x.k * y.k;
    return (z);
}
// Cross product function
vector cross(vector x, vector y)
{
    vector z;
    z.i = (x.j * y.k) - (x.k * y.j);
    z.j = (x.k * y.i) - (x.i * y.k);
    z.k = (x.i * y.j) - (x.j * y.i);
    return (z);
}
// Vector triple product function
vector vectripleproduct(vector a, vector b, vector c)
{

    vector z;
    z = cross(a, cross(b, c));
    return z;
}
// Scalar triple product function
float scaltripleproduct(vector a, vector b, vector c)
{

    float z;
    z = dot(a, cross(b, c));
    return z;
}
// Vector output function
int vecout(vector a)
{
    cout << a.i << "i\t" << a.j << "j\t" << a.k << "k\n";
    return (0);
}
// Vector input function
vector vecin()
{
    vector a;
    cout << "Enter the components of the vector\n";
    cout << "1st component : ";
    cin >> a.i;
    cout << "2nd component : ";
    cin >> a.j;
    cout << "3rd component : ";
    cin >> a.k;
    return (a);
}
vector vecsum(vector a, vector b)
{
    vector c;
    c.i = a.i + b.i;
    c.j = a.j + b.j;
    c.k = a.k + b.k;
    return (c);
}
// Main function
int main()
{
    struct vector a, b, c, e, g;
    float f;
    cout << "First vector\n";
    a = vecin();
    cout << "Second vector\n";
    b = vecin();
    cout << "Third vector\n";
    c = vecin();
    f = scaltripleproduct(a, b, c);
    cout << "\nResult of the scalar triple product\n";
    cout << f;
    e = vectripleproduct(a, b, c);
    cout << "\nResult of the vector triple product\n";
    vecout(e);
    cout << "\nResult of the vector triple product identity\n";
    g = vecsum(vecsum(vectripleproduct(a, b, c), vectripleproduct(c, a, b)), vectripleproduct(b, c, a));
    vecout(g);
}
```


### Output
```
First vector
Enter the components of the vector
1st component : 5
2nd component : 8
3rd component : 2
Second vector
Enter the components of the vector
1st component : 4
2nd component : 7
3rd component : 6
Third vector
Enter the components of the vector
1st component : 5
2nd component : 2
3rd component : 4

Result of the scalar triple product
138
Result of the vector triple product
-244i   167j    -58k

Result of the vector triple product identity
0i      0j      0k
```
