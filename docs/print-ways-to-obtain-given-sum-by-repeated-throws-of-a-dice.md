# 打印通过重复掷骰子获得给定总和的方法

> 原文:[https://www . geeksforgeeks . org/print-通过重复掷骰子获得给定总和的方法/](https://www.geeksforgeeks.org/print-ways-to-obtain-given-sum-by-repeated-throws-of-a-dice/)

给定一个整数 **N** ，任务是打印通过反复掷骰子得到总和 **N** 的方法。

> **输入:** N = 3
> **输出:**
> 1 1
> 1 2
> 2 1
> 3
> **说明:**标准骰子有 6 个面，即{1，2，3，4，5，6}。因此反复掷骰子后得到和 3 的方式如下:
> 1+1+1 = 3
> 1+2 = 3
> 2+1 = 3
> 3 = 3
> 
> **输入:** N = 2
> **输出:**
> 1 1
> 2

**方法:**这个问题可以用[递归](http://www.geeksforgeeks.org/recursion/)和[回溯](http://www.geeksforgeeks.org/backtracking-algorithms/)来解决。其思想是迭代范围**【1，6】**和[内骰子 **i** 的每一个可能值，递归调用](https://www.geeksforgeeks.org/recursive-functions/)求剩余的和，即(**N–I**)，并在类似[字符串](https://www.geeksforgeeks.org/string-data-structure/)的数据结构中不断追加当前骰子值的值。如果所需的总和为零，则打印存储字符串中的元素。

下面是上述方法的实现

## C++

```
// C++ program of the above appraoch
#include <iostream>
using namespace std;

// Recursive function to print the
// number of ways to get the sum
// N with repeated throw of a dice
void printWays(int n, string ans)
{
    // Base Case
    if (n == 0) {

        // Print characters in
        // the string
        for (auto x : ans) {
            cout << x << " ";
        }
        cout << endl;
        return;
    }

    // If n is less than zero,
    // no sum is possible
    else if (n < 0) {
        return;
    }

    // Loop to iterate over all
    // the possible current moves
    for (int i = 1; i <= 6; i++) {

        // Recursive call for the
        // remaining sum considering
        // i as the current integer
        printWays(n - i, ans + to_string(i));
    }
}

// Driver Code
int main()
{
    int N = 3;
    printWays(N, "");
    return 0;
}
```

**Output**

```
1 1 1 
1 2 
2 1 
3 
```

***时间复杂度:**O(6<sup>N</sup>)*
***辅助空间:** O(1)*