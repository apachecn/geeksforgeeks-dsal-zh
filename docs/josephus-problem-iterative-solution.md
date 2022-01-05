# 约瑟夫斯问题|(迭代求解)

> 原文:[https://www . geesforgeks . org/josephus-问题-迭代-求解/](https://www.geeksforgeeks.org/josephus-problem-iterative-solution/)

有 N 个孩子坐在排列成一圈的 N 把椅子上。椅子从 1 到 n 编号。游戏开始循环进行，从第一把椅子开始数孩子们。一旦计数达到 K，那个孩子就离开游戏，移开他/她的椅子。游戏再次开始，从圆圈中的下一把椅子开始。最后一个留在圈里的孩子是赢家。找到赢得比赛的孩子。

示例:

```
Input : N = 5, K = 2
Output : 3
Firstly, the child at position 2 is out, 
then position 4 goes out, then position 1
Finally, the child at position 5 is out. 
So the position 3 survives.

Input : 7 4
Output : 2

```

我们已经讨论了约瑟夫斯问题的递归解。给定的解优于约瑟夫斯解的递归解，后者不适合大输入，因为它给出堆栈溢出。时间复杂度为 O(N)。

**逼近**–在算法中，我们使用 sum 变量找出要移除的椅子。当前椅子位置是通过将椅子计数 K 加到先前位置(即总和和总和的模)来计算的。最后我们返回 sum+1，因为编号从 1 开始到 n

## C++

```
// Iterative solution for Josephus Problem 
#include <bits/stdc++.h>
using namespace std;

// Function for finding the winning child.
long long int find(long long int n, long long int k)
{
    long long int sum = 0, i;

    // For finding out the removed 
    // chairs in each iteration
    for (i = 2; i <= n; i++)
        sum = (sum + k) % i;

    return sum + 1;
}

// Driver function to find the winning child
int main()
{
    int n = 14, k = 2;
    cout << find(n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Iterative solution for Josephus Problem
class Test 
{

    // Method for finding the winning child.
    private int josephus(int n, int k) 
    {
        int sum = 0;

        // For finding out the removed 
        // chairs in each iteration 
        for(int i = 2; i <= n; i++) 
        {
            sum = (sum + k) % i;
        }

        return sum+1;
    }

    // Driver Program to test above method 
    public static void main(String[] args)
    { 
        int n = 14; 
        int k = 2; 
        Test obj = new Test();
        System.out.println(obj.josephus(n, k)); 
    }
}

// This code is contributed by Kumar Saras
```

**Output:**

```
13

```