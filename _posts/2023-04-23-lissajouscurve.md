---
title: "Lissajous Curve"
categories:
  - plotting
tags:
  - plotting
  - data
  - function
toc: true
---
## Problem in section "Preparing a Data file and Plotting" no. 4
Write a program in C++ to tabulate the value of the following trigonometric functions:

$$X(t) = A_X cos(2f_Xt)$$

$$Y(t) = A_Y sin(2f_Yt + \phi)$$

$$Z(t) = X(t)+Y(t)$$

at the equally spaced times $$t=n\delta t$$, with n = 0,. . . , N. Take the parameters $$f_X, f_Y, A_X, A_Y, \phi, \delta t, and N$$ as inputs and write the outputs X(t), Y(t) and Z(t) in a file.
- Plot $$X(t) vs. Y(t)$$. Give graphical evidancees in support of the fact that closed curves are obtained for rational $$\frac{f_X}{f_Y}$$.
- Plot $$Z(t) vs. t$$ and demonstrate the phenomenon of beats by taking $$f_X \approx f_Y$$.

## Answer

### Code

```c++
#include <iostream>

#include <cmath>

#include <fstream>

using namespace std;

// Defination of Z(t)
double Xfunc(double t, double Ax, double fx)
{
    double X;
    X = Ax * cos(2 * fx * t);
    return (X);
}

// Defination of Y(t)
double Yfunc(double t, double Ay, double fy, double phi)
{
    double Y;
    Y = Ay * sin(2 * fy * t + phi);
    return (Y);
}

// Defination of Z(t)
double Zfunc(double t, double Ax, double fx, double Ay, double fy, double phi)
{
    double Z;
    Z = Xfunc(t, Ax, fx) + Yfunc(t, Ay, fy, phi);
    return (Z);
}

int main()
{
    double t, i, Ax, Ay, fx, fy, phi, delt, N;
    ofstream fileout;
    fileout.open("lissajous.dat");
    cout << "Input the values of Ax and Ay = ";
    cin >> Ax >> Ay;
    cout << "Input the values of fx and fy = ";
    cin >> fx >> fy;
    cout << "Input the values of phi, delta t and N = ";
    cin >> phi >> delt >> N;

    for (i = 0; i < N; i = i + delt)
    {
        fileout << i << "\t" << Xfunc(i, Ax, fx) << "\t" << Yfunc(i, Ay, fy, phi) << "\t" << Zfunc(i, Ax, fx, Ay, fy, phi) << endl;
    }
    cout << "The generated data in written in lissajous.dat" << endl;
}

```

#### Gnuplot command
```
gnuplot> plot "lissajous.dat" u 2:3 w lp
gnuplot> plot "lissajous.dat" u 1:4 w lp
```
### Output
```
Input the values of Ax and Ay = 1
1
Input the values of fx and fy = 1
1
Input the values of phi, delta t and N = 0
0.01
10
```

![](../../assets/images/lissajous-1-1-1-1-0.png)

```
Input the values of Ax and Ay = 1
1
Input the values of fx and fy = 1
1.1
Input the values of phi, delta t and N = 0
0.01
100
The generated data in written in lissajous.dat
```
![](../../assets/images/lissajousZt-1-1-1-1.1-0.png)