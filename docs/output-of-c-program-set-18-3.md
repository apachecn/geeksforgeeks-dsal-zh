# 用 C++打印 1 到 100，不带循环和递归

> 原文:[https://www.geeksforgeeks.org/output-of-c-program-set-18-3/](https://www.geeksforgeeks.org/output-of-c-program-set-18-3/)

我们可以使用下面讨论的三种方法在不使用循环和递归的情况下打印 1 到 100:

**1)** [**模板元编程**](https://www.geeksforgeeks.org/template-metaprogramming-in-c/)**:**c++中的模板允许非数据类型也作为参数。非数据类型意味着值，而不是数据类型。

**例:**

## CPP

```
// CPP Program to print 1 to 100
// without loops and recursion
#include <iostream>
using namespace std;

template <int N> class PrintOneToN {
public:
    static void print()
    {
        PrintOneToN<N - 1>::print();

        // Note that this is not recursion
        cout << N << endl;
    }
};

template <> class PrintOneToN<1> {
public:
    static void print() { cout << 1 << endl; }
};

// Driver Code
int main()
{
    const int N = 100;
    PrintOneToN<N>::print();
    return 0;
}
```

**输出**

```
1
2
3
..
..
98
99
100
```

该程序打印从 1 到 n 的所有数字，而不使用循环和递归。

**解释:**

*   In the above program, n is passed as a non-data type value. Create a new instance of generic classes for each parameter, which are created at compile time.
*   Here, when the compiler sees the statement "printoneon <>:: print ()" with N = 100, it will create an instance of printoneon 【T1].
*   In the function printoneton <100>: print (), another function printoneton <99>: print () was called, so an instance printoneton < 99 > was created.
*   Similarly, all instances from printone on 【T0] to printone on 【T1] will be created. Print one ton <1> :print () is already there, print 1.
*   Function print one < 2 > print two, and so on. Therefore, we will print all numbers from 1 to n on the screen.

**2)** 接下来是**另一种方法**使用[类](https://www.geeksforgeeks.org/c-classes-and-objects/)和[静态变量](https://www.geeksforgeeks.org/static-variables-in-c/)、

T10】CPPT0T14】

**输出**

```
1
2
3
..
..
98
99
100
```

该程序的输出与上述程序相同。

**说明:**在上面的程序中，A 类有一个静态变量‘A’，随着 A 的每个实例递增，A 类的默认构造函数打印‘A’的值。当我们创建一个类型为 A 的对象数组时，所有对象的默认构造函数都被逐个调用。因此，我们将从 1 到 100 的所有值打印在屏幕上。

**3)使用** [**goto**](https://www.geeksforgeeks.org/goto-statement-in-c-cpp/) **关键字:**goto 语句是一个跳转语句，可以用来从一个函数内的任何地方跳转到任何地方。

**例:**

## c++

```
// CPP Program to print 1 to 100
// without loops and recursion
#include <iostream>

// Driver Code
int main()
{
    short sum = 0;

update:
    sum++;
    std::cout << sum << std::endl;

    if (sum == 100)
        return 0;
    goto update;
}
```

**输出**

```
1
2
3
..
..
98
99
100
```

该程序的输出与上述程序相同。

**说明:**在上面的程序中， **goto** 关键字是再次跳转到名为 update 的标签。“sum”的值会在每次调用时打印并递增。一旦变量和等于 100，程序就停止执行。这样，我们可以在控制台上打印从 1 到 100 的所有值。