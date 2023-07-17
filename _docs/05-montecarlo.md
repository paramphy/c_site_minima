---
title: "Monte Carlo Method"
permalink: /numerical/montecarlo/
last_modified_at: 2023-07-16
redirect_from:
  - /theme-setup/
toc: true
sidebar:
  nav: "numerical"
---
Monte Carlo simulation can be used to estimate the area under a curve by randomly generating points within a bounding rectangle that encloses the curve. The number of points that fall within the area under the curve is counted, and the ratio of this count to the total number of points generated is used to estimate the area under the curve. The more points generated, the more accurate the estimate will be. This method is particularly useful when the function defining the curve is difficult or impossible to integrate analytically.

## Algorithm of Monte Carlo method
1. Randomly generate points within a bounding rectangle that encloses the curve.
2. Count the number of points that fall within the area under the curve.
3. Use the ratio of this count to the total number of points generated to estimate the area under the curve.
4. Generate more points for a more accurate estimate.
5. This method is useful when the function defining the curve is difficult or impossible to integrate analytically.

## C++ Code
### Problem 1
Use the Monte Carlo Method of integration to find the area of a circle.

```c++
#include <iostream>
#include <cstdlib>
#include <ctime>
#include <fstream>
#include <cmath>

using namespace std;
int main()
{
    float x, y, a, b, n, r, nprime = 0, area;
    int i;
    srand(time(0));
    cout << "Enter the radious of the circle: ";
    cin >> r;
    cout << "Enter the value of N (total no. of points): ";
    cin >> n;
    ofstream allout("alldata.txt");
    ofstream cirout("cirdata.txt");
    for (i = 0; i <= n; i++)
    {
        x = r * (1 - 2.0 * rand() / RAND_MAX);
        y = r * (1 - 2.0 * rand() / RAND_MAX);
        allout << x << "\t" << y << endl;
        if ((x * x + y * y) < r * r)
        {
            nprime++;
            cirout << x << "\t" << y << endl;
        }
    }
    area = 4 * r * r * (nprime / n);
    cout << "Area of the circle: " << area << endl;
    cout << "Number of point generated: " << n << endl;
    cout << "Number of point inside circle: " << nprime << endl;
}
```
### Output and commands
```
Enter the radious of the circle: 1
Enter the value of N (total no. of points): 100000
Area of the circle: 3.14112
Number of point generated: 100000
Number of point inside circle: 78528
```
![](../../assets/images/circle-monte.png)

### Problem 2
Use the Monte Carlo Method of integration to find the area of an ellipse.

```c++
#include <iostream>
#include <cstdlib>
#include <ctime>
#include <fstream>
#include <cmath>

using namespace std;
int main()
{
    float x, y, a, b, n, nprime = 0, area;
    int i;
    srand(time(0));
    cout << "Enter the long arm of the ellipse: ";
    cin >> a;
    cout << "Enter the short arm of the ellipse: ";
    cin >> b;
    cout << "Enter the value of N (total no. of points): ";
    cin >> n;
    ofstream allout("alldata.txt");
    ofstream cirout("cirdata.txt");
    for (i = 0; i <= n; i++)
    {
        x = a * (1 - 2.0 * rand() / RAND_MAX);
        y = b * (1 - 2.0 * rand() / RAND_MAX);
        allout << x << "\t" << y << endl;
        if (((x * x) / (a * a) + (y * y) / (b * b)) < 1)
        {
            nprime++;
            cirout << x << "\t" << y << endl;
        }
    }
    area = 4 * a * b * (nprime / n);
    cout << "Area of the elipse: " << area << endl;
    cout << "Number of point generated: " << n << endl;
    cout << "Number of point inside ellipse: " << nprime << endl;
    cout << "Actual value of the area(4*pi*a*b): " << 3.14 * a * b << endl;
}
```
### Output and commands
```
Enter the long arm of the ellipse: 2
Enter the short arm of the ellipse: 1
Enter the value of N (total no. of points): 100000
Area of the ellipse: 6.3004
Number of point generated: 100000
Number of point inside ellipse: 78755
Actual value of the area(4*pi*a*b): 6.28
```
![](../../assets/images/ellipse-monte.png)