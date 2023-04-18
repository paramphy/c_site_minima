---
title: "Butterfly Curve"
categories:
  - plotting
tags:
  - plotting
  - data
  - function
toc: true
---
## Problem in section "Preparing a Data file and Plotting" no. 4
Write a program in C++ to tabulate the values of X(t) and Y(t):

$$X(t) = r(t)cos(t)$$

$$Y(t) = r(t)sin(t)$$

$$r(t) = e^{cos(t)}-2cos(4t)+sin^5(\frac{t}{12})$$

at the equally spaced time intervals $$\delta t$$ for $$-T<=t<=T$$, where $$\delta t$$ and $$T$$ are to be treated as inputs. Plot $$X(t)$$ vs. $$Y(t)$$.

## Answer

### Code

```c++
#include <iostream>
#include <cmath>
#include <fstream>

using namespace std;

double rfunc(double t)
{
    double r;
    r = exp(cos(t)) - 2*cos(4 * t) + pow(sin(t / 12), 5);
    return (r);
}
double xfunc(double t)
{
    double x;
    x = rfunc(t) * cos(t);
    return (x);
}
double yfunc(double t)
{
    double y;
    y = rfunc(t) * sin(t);
    return (y);
}

int main()
{
    float t, i, deltaT, T;
    cout << "Input the value of T = ";
    cin >> T;
    cout << "Input the value of delT = ";
    cin >> deltaT;
    ofstream fileout;
    fileout.open("butterfly.dat");

    for (i = -T; i < T; i = i + deltaT)
    {
        fileout << i << "\t" << xfunc(i) << "\t" << yfunc(i) << endl;
    }
    cout << "Calculations are done and the generated data is stored in 'butterfly.dat'";
}
```

#### Gnuplot command
```
gnuplot> plot 'butterfly.dat' u 2:3 w l p
```
### Output
```
Input the value of T = 63
Input the value of delT = 0.01
Calculations are done and the generated data is stored in 'butterfly.dat'
```

![](../../assets/images/butterfly.png)
