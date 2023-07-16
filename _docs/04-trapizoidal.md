---
title: "Trapizoidal Method"
permalink: /numerical/trapizoidal/
last_modified_at: 2023-07-16
redirect_from:
  - /theme-setup/
toc: true
sidebar:
  nav: "numerical"
---
In numerical analysis, Trapezoidal method is a technique for evaluating definite integral. This method is also known as Trapezoidal rule or Trapezium rule.

This method is based on Newton's Cote Quadrature Formula and Trapezoidal rule is obtained when we put value of n = 1 in this formula.

## Algorithm of Trapezoidal

1. Start
2. Define function f(x)
3. Read lower limit of integration, upper limit of integration and number of sub interval
4. Calcultae: step size = (upper limit - lower limit)/number of sub interval
5. Set: integration value = f(lower limit) + f(upper limit)
6. Set: i = 1
7. If i > number of sub interval then goto 
8. Calculate: k = lower limit + i * h
9. Calculate: Integration value = Integration Value + 2* f(k)
10. Increment i by 1 i.e. i = i+1 and go to step 7
11. Calculate: Integration value = Integration value * step size/2 
12. Display Integration value as required answer
13. Stop

## C++ Code
### Problem 1
Solve the following integration using Trapezoidal method

$$\int_0^{\pi} sin(x)dx$$

```c++
#include <iostream>
#include <cmath>
using namespace std;

double func(double x)
{
    return (sin(x));
}

int main()
{
    double a, b, h, sum = 0, I;
    int i;
    cout << "Input the lower limit of integration: ";
    cin >> a;
    cout << "Input the upper limit of integration: ";
    cin >> b;
    cout << "Input the step size: ";
    cin >> h;
    float n = (b - a) / h;

    for (i = 1; i < (n - 1); i++)
    {
        sum = sum + func(a + i * h);
    }
    I = (h * 1.0 / 2) * (func(a) + func(b) + 2 * sum);
    cout << "The value of the integration: " << I << endl;
}
```
### Output and commands
```
Input the lower limit of integration: 0
Input the upper limit of integration: 3.14
Input the step size: 0.001
The value of the integration: 2
```
