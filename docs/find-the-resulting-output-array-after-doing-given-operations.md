# 进行给定运算后找到结果输出数组

> 原文:[https://www . geeksforgeeks . org/find-执行给定操作后得到的输出数组/](https://www.geeksforgeeks.org/find-the-resulting-output-array-after-doing-given-operations/)

给定大小为 **N** 的整数数组**整数[]** 。执行一些操作后，找到结果输出数组:

*   如果 **(i-1) <sup>第</sup>** 元素为正，而**第<sup>第</sup>** 元素为负，则:
    *   如果**(I)**的绝对值大于 **(i-t)的**，则从左侧移除所有绝对值小于**的**相邻正元素**。**
    *   **如果**(I)**的绝对值小于 **(i-t)th** ，则移除该元素。**
    *   **如果**(I)**的绝对值等于**(I-1)**的绝对值，则移除两个元素。**

****示例:****

> ****输入:**整数[] = {3，-2，4}
> **输出:** 3 4
> **说明:**第一个数字会抵消第二个数字。
> 因此，输出数组将是{3，4}。**
> 
> ****输入:**整数[] = {-2，-1，1，2}
> **输出:** -2 -1 1 2
> **说明:**正数后不加负数。
> 所以每个数字都会出现在输出数组中**

****方法:**忽略相同符号的数字，不管它们的大小。所以我们唯一要考虑的情况就是前一个元素的量级为正，下一个元素的量级为负，我们可以用[叠加](https://www.geeksforgeeks.org/stack-data-structure/)来模拟这个问题。按照以下步骤解决问题:**

*   **[初始化](https://www.geeksforgeeks.org/stack-in-cpp-stl/)堆栈**。****
*   **[使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N)** ，并执行以下任务:

    *   如果**整数【I】**大于 **0** 或 **s[]** 为空，则将**整数【I】**推入堆栈 **s[]** 。
    *   否则，[循环遍历](https://www.geeksforgeeks.org/c-c-while-loop-with-examples/)直到 **s** 不为空， **s.top()** 大于 **0** ， **s.top()** 小于 **abs(整数[i])** 并执行以下任务:
        *   从堆栈中弹出元素 **s[]。**
    *   如果 **s** 不为空且 **s.top()** 等于 **abs(整数[i])** ，则从堆栈中弹出 **s[]。**
    *   否则，如果 **s[]** 为空或 **s.top()** 小于 **0** ，则将**整数【I】**推入堆栈 **s[]。**** 
*   **[初始化向量](https://www.geeksforgeeks.org/initialize-a-vector-in-cpp-different-ways/) **res[s.size()]** 来存储结果。**
*   **[使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【s . size()-1，0】**，并执行以下任务:

    *   将**RES【I】**设置为【T2 s . top()并从堆栈中弹出【T4 s】。** 
*   **执行上述步骤后，打印**RES【】**的值作为答案。**

**下面是上述方法的实现。**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the remaining numbers
vector<int> remainingNumbers(vector<int>& 
                             integers)
{

    // Size of the array
    int n = integers.size();

    // Initialize the stack
    stack<int> s;

    // Traverse the array
    for (int i = 0; i < n; i++) {
        if (integers[i] > 0 || s.empty()) {
            s.push(integers[i]);
        }
        else {
            while (!s.empty() and s.top() > 0
                   and s.top() < 
                   abs(integers[i])) {
                s.pop();
            }
            if (!s.empty()
                and s.top() == 
                abs(integers[i])) {
                s.pop();
            }
            else if (s.empty() || 
                     s.top() < 0) {
                s.push(integers[i]);
            }
        }
    }

    // Finally we are returning the elements
    // which remains in the stack.
    // we have to return them in reverse order.
    vector<int> res(s.size());
    for (int i = (int)s.size() - 1; i >= 0; 
         i--) {
        res[i] = s.top();
        s.pop();
    }
    return res;
}

// Driver Code
int main()
{

    vector<int> integers = { 3, -2, 4 };
    vector<int> ans = 
        remainingNumbers(integers);

    for (int x : ans) {
        cout << x << " ";
    }

    return 0;
}
```

****Output**

```
3 4 
```** 

*****时间复杂度:**O(N)*
T5**辅助空间:** O(N)**