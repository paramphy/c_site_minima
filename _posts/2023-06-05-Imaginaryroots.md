---
title: "Imaginary roots using Newton-Raphson method"
categories:
  - root
tags:
  - root
  - structure
  - function
toc: true
---
## Problem related to imaginary root findings using Newton Raphson method

Find the roots and draw the corresponding fractal of the following equations

$$x^2+1=0$$

$$x^3+1=0$$

$$x^4+1=0$$

## Answer

### Code

```c++
#include <iostream>
#include <cmath>
#include <fstream>

using namespace std;

// x,y,itr structure definition
struct imaginary
{
    float x, y;
    int itr;
};

// Function to calculate real part of the equation
float g(float x, float y)
{
    return (x * x - y * y + 1.0);
}

// Function to calculate imaginary part of the equation
float h(float x, float y)
{
    return (2.0 * x * y);
}

// Function to calculate differential(wrt x) of real part of the equation
float dgx(float x, float y)
{
    return (2.0 * x);
}

// Function to calculate differential(wrt y) of real part of the equation
float dgy(float x, float y)
{
    return (-2.0 * y);
}

// Function to calculate differential(wrt x) of imaginary part of the equation
float dhx(float x, float y)
{
    return (2.0 * y);
}

// Function to calculate differential(wrt y) of imaginary part of the equation
float dhy(float x, float y)
{
    return (2.0 * x);
}

imaginary img_roots(float x0, float y0)
{
    imaginary roots;
    int i = 0;
    float denom, del_x, del_y;
    denom = dgx(x0, y0) * dhy(x0, y0) - dgy(x0, y0) * dhx(x0, y0);
    if (denom == 0)
        cout << "Please change the initial guess values" << endl;
    else
    {
        do
        {
            denom = dgx(x0, y0) * dhy(x0, y0) - dgy(x0, y0) * dhx(x0, y0);
            del_x = (dgy(x0, y0) * h(x0, y0) - g(x0, y0) * dhy(x0, y0)) * 1.0 / denom;
            del_y = (g(x0, y0) * dhx(x0, y0) - dgx(x0, y0) * h(x0, y0)) * 1.0 / denom;
            x0 = x0 + del_x;
            y0 = y0 + del_y;
            i++;
            // Condition to break the iteration after 100 iterations
            if (i > 100)
                break;
        } while (abs(g(x0, y0)) > 0.00000001 && abs(h(x0, y0)) > 0.00000001);
    }
    roots.x = x0;
    roots.y = y0;
    roots.itr = i;
    return (roots);
}
// Main code

int main()
{
    float x, y;
    imaginary roots;
    ofstream fout;
    fout.open("n=2-data.dat");
    for (x = -2; x < 2; x = x + 0.005)
    {
        for (y = -2; y < 2; y = y + 0.005)
        {
            roots = img_roots(x, y);
            fout << x << "\t" << y << "\t" << roots.x << "\t" << roots.y << "\t" << roots.itr << endl;
        }
    }

    cout << "Data is written" << endl;
}
```
### For x^3 +1 = 0 the function section changes to

```c++
// Function to calculate real part of the equation
float g(float x, float y)
{
    return (x*x*x*x-y*y*y*y-6*x*x*y*y+1);
}

// Function to calculate imaginary part of the equation
float h(float x, float y)
{
    return (-4*x*y*y*y+4*x*x*x*y);
}

// Function to calculate differential(wrt x) of real part of the equation
float dgx(float x, float y)
{
    return (4*x*x*x-12*x*y*y);
}

// Function to calculate differential(wrt y) of real part of the equation
float dgy(float x, float y)
{
    return (4*y*y*y-12*x*x*y);
}

// Function to calculate differential(wrt x) of imaginary part of the equation
float dhx(float x, float y)
{
    return (-4*y*y*y-12*x*x*y);
}

// Function to calculate differential(wrt y) of imaginary part of the equation
float dhy(float x, float y)
{
    return (4*x*x*x-12*x*y*y);
}
```
### For x^4+1=0 case the function section changes to 

```c++
// Function to calculate real part of the equation
float g(float x, float y)
{
    return (x * x * x * x + y * y * y * y - 6 * x * x * y * y + 1);
}

// Function to calculate imaginary part of the equation
float h(float x, float y)
{
    return (-4 * x * y * y * y + 4 * x * x * x * y);
}

// Function to calculate differential(wrt x) of real part of the equation
float dgx(float x, float y)
{
    return (4 * x * x * x - 12 * x * y * y);
}

// Function to calculate differential(wrt y) of real part of the equation
float dgy(float x, float y)
{
    return (4 * y * y * y - 12 * x * x * y);
}

// Function to calculate differential(wrt x) of imaginary part of the equation
float dhx(float x, float y)
{
    return (-4 * y * y * y + 12 * x * x * y);
}

// Function to calculate differential(wrt y) of imaginary part of the equation
float dhy(float x, float y)
{
    return (4 * x * x * x - 12 * x * y * y);
}
```
### Output

$$x^2+1=0$$

![](../../assets/images/imaginary-roots-2.png)

$$x^3+1=0$$

![](../../assets/images/imaginary-roots-3.png)

$$x^4+1=0$$

![](../../assets/images/imaginary-roots-4.png)
