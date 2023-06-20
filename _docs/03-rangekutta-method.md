---
title: "Range Kutta method"
permalink: /numerical/rangekutta-method/
last_modified_at: 2023-06-20
redirect_from:
  - /theme-setup/
toc: true
sidebar:
  nav: "numerical"
---

## Methodology
### 1st order Range-Kutta method

$$y_1=y_0+hf(x_0,y_0)$$

this is equivalent to Euler's method.

### 2nd order Range-Kutta method

$$y_1=y_0+\frac{1}{2}(k_1+k_2)$$

where,

$$k_1=hf(x_0,y_0)$$

$$k_2=hf(x_0+h, y_0+k_1)$$

### 3rd order Range-Kutta method

$$y_1=y_0+\frac{1}{6}(k_1+4k_2+k_3)$$

where,

$$k_1=hf(x_0,y_0)$$

$$k_2=hf(x_0+h/2,y_0+k_1/2)$$

$$k_3=hf(x_0+h,y_0+2k_2-k_1)$$

### 4th order Range-Kutta method

$$y_1=y_0+\frac{1}{6}(k_1+2k_2+2k_3+k_4)$$

where,

$$k_1=hf(x_0,y_0)$$

$$k_2=hf(x_0+h/2,y_0+k_1/2)$$

$$k_3=hf(x_0+h/2,y_0+k_2/2)$$

$$k_4=hf(x_0+h,y_0+k_3)$$

## Algorithm for 4th order RK method

1. define $f(t,y)$.
2. input the initial values $t_0, y_0$.
3. input step size, $h$ and the number of steps, $n$.
4. for $j$ from 1 to n do
   - calculate $k_1, k_2, k_3, k_4$
   - calculate $y_1 = y_0+h/6*(k_1+2*k_2+2*k_3+k_4)$
   - $t_1=t_0+h$
   - print $t_1$ and $y_1$
   - $t_0=t_1$
   - $y_0=y_1$
5. end. 

## C++ Code
### Problem 1
For the differential equation

$$\frac{dy}{dx}=y$$

where $y=1$ at $x=0$

```c++
#include <iostream>
#include <cmath>
#include <fstream>

using namespace std;

// Definition of the function dy/dx
double f(double x, double y)
{
    return (y);
}

int main()
{
    double x0, xn, yn, y0, k1, k2, k3, k4, h;
    int i, n;
    // Input the inital values
    cout << "Input the initial values." << endl;
    cout << "Input the value of x0: ";
    cin >> x0;
    cout << "Input the value y0: ";
    cin >> y0;
    cout << "Input the value xn: ";
    cin >> xn;
    cout << "Input the step value h: ";
    cin >> h;

    ofstream fileout;
    fileout.open("rk.dat");

    n = (xn - x0) / h;

    // Calculation of yn using 4th order RK method
    for (i = 0; i < n; i++)
    {

        k1 = h * f(x0, y0);
        k2 = h * f(x0 + h / 2, y0 + k1 / 2);
        k3 = h * f(x0 + h / 2, y0 + k2 / 2);
        k4 = h * f(x0 + h, y0 + k3);

        yn = y0 + (1.0 / 6) * (k1 + 2 * k2 + 2 * k3 + k4);
        y0 = yn;
        x0 = x0 + h;

        fileout << x0 << "\t" << yn << endl;
    }
}
```
### Output and commands
```
Input the initial values.
Input the value of x0: 0
Input the value y0: 1
Input the value xn: 2
Input the step value h: 0.01
```
### Output plot
#### gnuplot code
```
gnuplot> plot "rk.dat" w p
gnuplot> replot exp(x)
```
![](../../assets/images/rk-method-prob-1.png)

