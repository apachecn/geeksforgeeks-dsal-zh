# STD::bit _ or c++示例

> 原文:[https://www.geeksforgeeks.org/stdbit_or-in-c-with-examples/](https://www.geeksforgeeks.org/stdbit_or-in-c-with-examples/)

**位或**是 C++中的一个内置函数，用于执行 **[位或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)** ，并在其参数上应用**位或**运算后返回结果。

**头文件:**

```
#include <functional.h>

```

**模板类:**

```
template <class T> struct bit_or;

```

**参数:**它接受一个参数 **T** ，这是函数调用要比较的参数类型。

**注意:**

1.  Objects of this class can be used in standard algorithms, such as [transformation](https://www.geeksforgeeks.org/transform-c-stl-perform-operation-elements/) or accumulation.
2.  The function ('operator ()') returns the **bit or** of its parameter.

我们必须包含库**【函数】**和**【算法】**来分别使用 bit_or 和 transform()。

下面是 C++中**位 _ 或**的图示:

**问题 1:**

```
// C++ program to show the
// functionality of bit_or

#include <algorithm> // to include transform
#include <functional> // to include bit_or
#include <iostream>
#include <iterator>
using namespace std;

int main()
{
    // declaring the values
    int xyz[] = { -7, 2, 5, 100, 1029 };
    int abc[] = { -4, 0, 5, 1, 1 };
    int n = 5;
    // defining results
    int results[n];

    // transform is used to apply
    // bitwise_or on the arguments
    transform(xyz, end(xyz), abc,
              results, bit_or<int>());

    // printing the resulting array
    cout << "Results:";
    for (const int& x : results)
        cout << ' ' << x;

    return 0;
}
```

**输出:**

```
Results: -3 2 5 101 1029

```

> **某些点要记住**
> 
> 1.  The bit _ or result of a number with **zero enters the number itself.**
> 2.  The bitwise OR of two **identical numbers** is also equal to the number itself.
> 3.  If the number is **odd** , its bit_or and 1 will produce the same number.
> 4.  If the number is even , its bit_or and 1 will always produce **"number+1"**

**问题 2:**

```
// C++ program to show the
// functionality of bit_or

#include <algorithm>
#include <functional>
#include <iostream>
#include <iterator>
using namespace std;

int main()
{
    // declaring the values
    // in form of hexadecimals
    int xyz[] = { 0, 1100 };
    int abc[] = { 0xf, 0xf };

    // defining results
    int results[2];

    // transform is used to apply
    // bitwise_or on the arguments
    transform(xyz, end(xyz), abc,
              results, bit_or<int>());

    // printing the resulting array
    cout << "Results:";
    for (const int& x : results)
        cout << ' ' << x;

    return 0;
}
```

**输出:**

```
Results: 15 1103

```

**参考:**T2】https://en.cppreference.com/w/cpp/utility/functional/bit_or