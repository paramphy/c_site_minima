---
title: "Multi function least squared fit"
categories:
  - fitting
tags:
  - fitting
  - structure
  - function
toc: true
---
## Problem in section "Matrix Operations" no. 1

Fit a given data to three different functions

$$y = mx +c$$

$$y = Ae^{nx}$$

$$y = Ax^n$$

## Answer

### Code

```c++
#include <iostream>
#include <fstream>
#include <cmath>

using namespace std;

// Parameter structure defination
struct parameters
{
    float a, c;
};

// Data structure defination
struct data
{
    int n;
    float x[100], y[100];
};

// Least squred fit function
parameters leastsqfit(data dataarray)
{
    int i;
    parameters params;
    float sumx = 0, sumy = 0, sumxy = 0, sumx2 = 0;
    for (i = 0; i < dataarray.n; i++)
    {
        sumx = sumx + dataarray.x[i];
        sumy = sumy + dataarray.y[i];
        sumxy = sumxy + dataarray.x[i] * dataarray.y[i];
        sumx2 = sumx2 + dataarray.x[i] * dataarray.x[i];
    }
    params.a = (dataarray.n * sumxy - sumx * sumy) / (dataarray.n * sumx2 - sumx * sumx);
    params.c = (sumy - params.a * sumx) / dataarray.n;
    return (params);
}

// Exponential fit function
parameters expfit(data dataarray)
{
    int i;
    parameters params;
    for (i = 0; i < dataarray.n; i++)
    {
        dataarray.y[i] = log(dataarray.y[i]);
    }
    params = leastsqfit(dataarray);
    params.c = exp(params.c);
    return (params);
}
// Ax^n fit function
parameters axnfit(data dataarray)
{
    int i;
    parameters params;
    for (i = 0; i < dataarray.n; i++)
    {
        dataarray.x[i] = log(dataarray.x[i]);
        dataarray.y[i] = log(dataarray.y[i]);
    }
    params = leastsqfit(dataarray);
    params.c = exp(params.c);
    return (params);
}

// Main function
int main()
{
    int i;
    data dataarray;
    parameters params;
    cout << "Data will be read from fitdata.dat file\n";
    ifstream fin;
    fin.open("fitdata.dat");
    fin >> dataarray.n;
    cout << "Number of data pairs = "<<dataarray.n << endl;
    for (i = 0; i < dataarray.n; i++)
    {
        fin >> dataarray.x[i] >> dataarray.y[i];
    }
    params = leastsqfit(dataarray);
    cout << "a = " << params.a << "\t"
         << "c = " << params.c << endl;
    params = expfit(dataarray);
    cout << "m = " << params.a << "\t"
         << "A = " << params.c << endl;
    params = axnfit(dataarray);
    cout << "n = " << params.a << "\t"
         << "A = " << params.c << endl;
}
```


### Output
**Input file fitdata.dat**
```
11
0.1   5
1   6
2   8
3   10
4   15
5   19
6   21
7   25
8   31
9   35
10  40
```

```
Data will be read from fitdata.dat file
Number of data pairs = 11
a = 3.61938     c = 1.41565
m = 0.216212    A = 5.35779
n = 0.474721    A = 9.10746
```
![](../../assets/images/leastsqured-fit.png)
