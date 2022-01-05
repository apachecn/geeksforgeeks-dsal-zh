# c++中的 Pi(π)举例

> 原文:[https://www.geeksforgeeks.org/pi-in-c-with-examples/](https://www.geeksforgeeks.org/pi-in-c-with-examples/)

在这篇文章中，我们将讨论一些在 C++中用来推导**π(T1)**值的数学函数。

**方法一:**使用 [acos()功能](https://www.geeksforgeeks.org/acos-function-in-c-stl/):
T5】进场:

1.  π的值使用 [acos()函数](https://www.geeksforgeeks.org/acos-function-in-c-stl/)计算，该函数返回一个介于**[-π，π]**之间的数值。
2.  因为使用 **acos(0.0)** 将返回**π/2**的值。因此要得到**π**的值:

    ```
    double pi = 2*acos(0.0);

    ```

3.  现在由上述方程得到的值估计为:

    ```
    printf("%f\n", pi);

    ```

下面是上述方法的实现:

```
// C++ program for the above approach

#include "bits/stdc++.h"
using namespace std;

// Function that prints the
// value of pi
void printValueOfPi()
{

    // Find value of pi using
    // acos() function
    double pi = 2 * acos(0.0);

    // Print value of pi
    printf("%f\n", pi);
}

// Driver Code
int main()
{
    // Function that prints
    // the value of pi
    printValueOfPi();
    return 0;
}
```

**Output:**

```
3.141593

```