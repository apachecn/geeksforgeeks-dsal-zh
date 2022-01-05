# 在 main()

中调用 main()的 C/C++程序

> 原文:[https://www . geesforgeks . org/c-c-program-for-calling-main-in-main/](https://www.geeksforgeeks.org/c-c-program-for-calling-main-in-main/)

给定一个数字 **N** ，任务是编写 [C/C++程序，通过使用](https://www.geeksforgeeks.org/c-program-to-print-numbers-from-1-to-n-without-using-semicolon/)[递归](https://www.geeksforgeeks.org/recursion/)调用 [main()](https://www.geeksforgeeks.org/executing-main-in-c-behind-the-scene/) 函数打印从 N 到 1 的数字。
**举例:**

> **输入:** N = 10
> **输出:**10 9 8 7 5 4 3 2 1
> T6】输入:N = 5
> T9】输出: 5 4 3 2 1

**进场:**

1.  使用[静态变量](https://www.geeksforgeeks.org/static-variables-in-c/)初始化给定的数字 **N** 。
2.  打印数字 **N** 并递减。
3.  完成上述步骤后，再次调用 main()函数。

以下是上述方法的实现:

## C

```
// C program to illustrate calling
// main() function in main() itself
#include "stdio.h"

// Driver Code
int main()
{

    // Declare a static variable
    static int N = 10;

    // Condition for calling main()
    // recursively
    if (N > 0) {
        printf("%d ", N);
        N--;
        main();
    }
}
```

## C++

```
// C++ program to illustrate calling
// main() function in main() itself
#include "iostream"
using namespace std;

// Driver Code
int main()
{
    // Declare a static variable
    static int N = 10;

    // Condition for calling main()
    // recursively until N is 0
    if (N > 0) {
        cout << N << ' ';
        N--;
        main();
    }
}
```

**Output:** 

```
10 9 8 7 6 5 4 3 2 1
```

**时间复杂度:** *O(N)* ，其中 N 为给定数。