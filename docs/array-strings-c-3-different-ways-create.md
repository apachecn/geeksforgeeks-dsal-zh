# c++中的字符串数组(5 种不同的创建方式)

> 原文:[https://www . geesforgeks . org/array-strings-c-3-differential-way-create/](https://www.geeksforgeeks.org/array-strings-c-3-different-ways-create/)

在 C 和 C++中，字符串是一维字符数组，而 C 中的字符串数组是二维字符数组。有许多方法可以声明它们，这里给出了一些有用的方法。

## **1。使用指针:**

我们通过创建指针数组来创建字符串数组。

这是 C 和 C++都支持的。

## CPP

```
// C++ program to demonstrate array of strings using
// 2D character array
#include <iostream>

int main()
{
    // Initialize array of pointer
    const char *colour[4] = { "Blue", "Red",
                             "Orange", "Yellow" };

    // Printing Strings stored in 2D array
    for (int i = 0; i < 4; i++)
        std::cout << colour[i] << "\n";

    return 0;
}
```

**输出:**

```
Blue
Red
Orange
Yellow
```