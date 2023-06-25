---
title: "Bisection method for root finding"
permalink: /numerical/bisection/
last_modified_at: 2023-02-02
redirect_from:
  - /theme-setup/
toc: true
sidebar:
  nav: "numerical"
---
In Mathematics, the Bisection Method is a straightforward method used to find numerical solutions of an equation with one unknown variable.

## Definition
This method is a root-finding method that applies to any continuous functions with two known values of opposite signs. It is a very simple but cumbersome method. The interval defined by these two values is bisected and a sub-interval in which the function changes sign is selected. This sub-interval must contain the root. These two steps are repeatedly executed until the root is in the form of the required precision level. This method is also called as interval halving method, the binary method, or the dichotomy method.

## Methodology
Let $f(x)$ be a continuous function defined on an interval $[a,b]$ where $f(a)$ and $f(b)$ have opposite signs. Bisection method is applicable for solving the equation $f(x)=0$ for a real variable $x$. At each step, the interval is divided into two parts/halves by computing the midpoint, $c=(a+b)/2$, and the value of $f(c)$ at that point. Unless the root is c, there are two possibilities: $f(a)$ and $f(c)$ have opposite signs and bracket a root, $f(c)$ and $f(b)$ have opposite signs and bracket a root. One of the sub-intervals is chosen as the new interval to be used in the next step. This process is carried out again and again until the interval is sufficiently small. If $f(a)$ and $f(c)$ have opposite signs, then the value of $b$ is replaced by $c$. If $f(b)$ and $f(c)$ have opposite signs, then the value of a is replaced by c. In the case that $f(c)=0$, c will be taken as the solution and the process stops.
![](../../assets/images/bisection.png)

## Algorithm
1. define $f(t,y)$.
2. input the terminal $x$ values $a, b$.
3. while $f(x)>0$
   - define $c ← (a + b)/2$
   - if $sign(f(c)) = sign(f(a))$ 
   - then $a ← c$ else $b ← c$
4.  end. 

## Code
```c++
#include <iostream>
#include <cmath>

using namespace std;

// Definition of the function
float func(float x)
{
    float y;
    y = x * x - 5 * x + 6;
    return (y);
}

int main()
{
    float a, b, x;
    int i = 0;
    cout << "Input the range of values to search = ";
    cin >> a >> b;

    // bisection method
    do
    {
        if (func(a) * func(b) > 0 || func(a) * func(b) == 0)
        {
            cout << "Please give a different range\n";
            break;
        }
        else if (func(a) * func(b) < 0)
        {
            x = (a + b) / 2;
            if (func(x) * func(a) < 0)
            {
                b = x;
            }
            else
            {
                a = x;
            }
        }
        i++;
        // cout << i << "\t" << x << endl;
    } while (abs(a - b) > 0.00001);
    cout << "The root is = " << x << endl;
    cout << "The number of iteration used = " << i << endl;
}
```
### Output
```
Input the range of values to search = 2.5
5
The root is = 3
The number of iteration used = 18
```
