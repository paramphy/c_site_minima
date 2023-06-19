---
title: "Eular's method"
permalink: /numerical/eulars-method/
last_modified_at: 2023-06-19
redirect_from:
  - /theme-setup/
toc: true
sidebar:
  nav: "numerical"
---
The Euler’s method is a first-order numerical procedure for solving ordinary differential equations (ODE) with a given initial value.

## Methodology

Let’s start with a general first order IVP (Initial Value Problem)

$$\frac{dy}{dt}=f(t,y) \space\space where \space\space y(t_0)=y_0$$

We will use the derivative at first point to guess the value of the second point using the following equations

$$\frac{dy}{dt}_{t=t_0}=f(t_0,y_0)$$

$$y=y_0+f(t_0,y_0)(t-t_0)$$

same process can be repeated to get the next value fro the previous one. 

## Algorithm

1. define $f(t,y)$.
2. input the initial values $t_0, y_0$.
3. input step size, $h$ and the number of steps, $n$.
4. for $j$ from 1 to n do
   - $m = f(t_0,y_0)$
   - $y_1 = y_0+h*m$
   - $t_1=t_0+h$
   - print $t_1$ and $y_1$
   - $t_0=t_1$
   - $y_0=y_1$
5. end. 

## C++ Code
For the differential equation

$$\frac{dy}{dx}=y$$

where $y=1$ at $x=0$

```c++
#include <iostream>
#include <fstream>

using namespace std;

// Defination of the function dy/dx
double f(double x, double y)
{
    return (y);
}

// Main function
int main()
{
    double x0, y0, xn, h;
    int i, n;
    ofstream fileout;
    fileout.open("euler.dat");
    cout << "Enter the initial values." << endl;
    cout << "Enter the value of x0: ";
    cin >> x0;
    cout << "Enter the value of y0: ";
    cin >> y0;
    cout << "\nEnter the value of xn: ";
    cin >> xn;
    cout << "Enter the value of n: ";
    cin >> n;
    h = (xn - x0) / n;
    // Calculation of the values x,y
    for (i = 0; i < n; i++)
    {
        fileout << x0 << "  " << y0 << endl;
        y0 = y0 + (h * f(x0, y0));
        x0 = x0 + h;
    }
}
```
### Output and commands
```
Enter the initial values.
Enter the value of x0: 0
Enter the value of y0: 1

Enter the value of xn: 2
Enter the value of n: 100
```
### Output plot
#### gnuplot code
```
gnuplot> plot "euler.dat" w p
gnuplot> replot exp(x)
```
![](../../assets/images/eulars-method-dif=y.png)
