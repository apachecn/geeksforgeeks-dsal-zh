# 生成相邻数字间绝对差为 K 的所有 N 位数字

> 原文:[https://www . geeksforgeeks . org/generate-all-n-digits-numbers-相邻数字间有绝对差 as-k/](https://www.geeksforgeeks.org/generate-all-n-digit-numbers-having-absolute-difference-as-k-between-adjacent-digits/)

给定两个整数 **N** 和 **K** ，任务是生成所有长度为 **N** 的正整数，相邻数字的绝对差值等于 **K** 。

**示例:**

> **输入:** N = 4，K = 8
> **输出:** 1919，8080，9191
> **说明:**
> 每个数字每连续一位数的绝对差为 8。
> 例如:8080 (abs(8-0) = 8，abs(0-8) = 8)
> 
> **输入:** N = 2，K = 2
> **输出:** 13、24、20、35、31、46、42、57、53、68、64、79、75、86、97
> **说明:**
> 每个数字的每一个连续数字的绝对差为 1。

**方法:**思路是使用[回溯](https://www.geeksforgeeks.org/backtracking-algorithms/)。使用[递归](https://www.geeksforgeeks.org/recursion/)对数字**【1，9】**进行迭代，并对绝对数字为 **K** 的 N 位数中的每个数字进行迭代。以下是步骤:

1.创建一个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **和**来存储所有结果数字，并从 **1 到 9** 递归迭代，从每个数字开始生成数字。以下是案例:

*   **基本情况:**对于单个长度的所有整数，即 **N = 1** ，将其加到**ans【】**上。
*   **递归调用:**如果给一个数字加数字 **K** 不超过 **9** ，则通过减少 **N** 递归调用，并将 **num** 更新为 **(10*num + num%10 + K)** 如下所示:

> if(num % 10 + K ≤ 9) {
> 递归 _ 函数(10 * num + (num % 10 + K)，K，N–1，和)；
> }

*   如果在所有递归调用后 **K** 的值为非零，并且如果 **num % 10 > = K** ，则通过减少 **N** 再次递归调用，并将 **num** 更新为**(10 * num+num % 10–K)**如下:

> recursive _ function(10 * num+num % 10–K，K，N–1，ans)；

2.完成上述所有步骤后，打印存储在**和**中的数字。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that recursively finds the
// possible numbers and append into ans
void checkUntil(int num, int K,
                int N, vector<int>& ans)
{

    // Base Case
    if (N == 1)
    {
        ans.push_back(num);
        return;
    }

    // Check the sum of last digit and k
    // less than or equal to 9 or not
    if ((num % 10 + K) <= 9)
        checkUntil(10 * num
                       + (num % 10 + K),
                   K, N - 1, ans);

    // If k==0, then subtraction and
    // addition does not make any
    // difference
    // Hence, subtraction is skipped
    if (K) {
        if ((num % 10 - K) >= 0)
            checkUntil(10 * num
                           + num % 10 - K,
                       K, N - 1,
                       ans);
    }
}

// Function to call checkUntil function
// for every integer from 1 to 9
void check(int K, int N, vector<int>& ans)
{
    // check_util function recursively
    // store all numbers starting from i
    for (int i = 1; i <= 9; i++) {
        checkUntil(i, K, N, ans);
    }
}

// Function to print the all numbers
// which  satisfy the conditions
void print(vector<int>& ans)
{
    for (int i = 0; i < ans.size(); i++) {
        cout << ans[i] << ", ";
    }
}

// Driver Code
int main()
{
    // Given N and K
    int N = 4, K = 8;

    // To store the result
    vector<int> ans;

    // Function Call
    check(K, N, ans);

    // Print Resultant Numbers
    print(ans);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// the above approach
import java.util.*;
class GFG{

    // Function that recursively finds the
    // possible numbers and append into ans
    static void checkUntil(int num, int K, int N,
                           Vector<Integer> ans)
    {

        // Base Case
        if (N == 1)
        {
            ans.add(num);
            return;
        }

        // Check the sum of last digit and k
        // less than or equal to 9 or not
        if ((num % 10 + K) <= 9)
            checkUntil(10 * num + (num % 10 + K),
                       K, N - 1, ans);

        // If k==0, then subtraction and
        // addition does not make any
        // difference
        // Hence, subtraction is skipped
        if (K > 0)
        {
            if ((num % 10 - K) >= 0)
                checkUntil(10 * num + num % 10 - K,
                           K, N - 1, ans);
        }
    }

    // Function to call checkUntil function
    // for every integer from 1 to 9
    static void check(int K, int N, Vector<Integer> ans)
    {

        // check_util function recursively
        // store all numbers starting from i
        for (int i = 1; i <= 9; i++)
        {
            checkUntil(i, K, N, ans);
        }
    }

    // Function to print the all numbers
    // which  satisfy the conditions
    static void print(Vector<Integer> ans)
    {
        for (int i = 0; i < ans.size(); i++)
        {
            System.out.print(ans.get(i) + ", ");
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given N and K
        int N = 4, K = 8;

        // To store the result
        Vector<Integer> ans = new Vector<Integer>();;

        // Function Call
        check(K, N, ans);

        // Print Resultant Numbers
        print(ans);
    }
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function that recursively finds the
# possible numbers and append into ans
def checkUntil(num, K, N, ans):

    # Base Case
    if (N == 1):
        ans.append(num)
        return

    # Check the sum of last digit and k
    # less than or equal to 9 or not
    if ((num % 10 + K) <= 9):
        checkUntil(10 * num +
                 (num % 10 + K),
                 K, N - 1, ans)

    # If k==0, then subtraction and
    # addition does not make any
    # difference
    # Hence, subtraction is skipped
    if (K):
        if ((num % 10 - K) >= 0):
            checkUntil(10 * num +
                      num % 10 - K,
                     K, N - 1, ans)

# Function to call checkUntil function
# for every integer from 1 to 9
def check(K, N, ans):

    # check_util function recursively
    # store all numbers starting from i
    for i in range(1, 10):
        checkUntil(i, K, N, ans)

# Function to print the all numbers
# which satisfy the conditions
def print_list(ans):

    for i in range(len(ans)):
        print(ans[i], end = ", ")

# Driver Code
if __name__ == "__main__":

    # Given N and K
    N = 4
    K = 8;

    # To store the result
    ans = []

    # Function call
    check(K, N, ans)

    # Print resultant numbers
    print_list(ans)

# This code is contributed by chitranayal
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function that recursively finds the
// possible numbers and append into ans
static void checkUntil(int num, int K, int N,
                       List<int> ans)
{

    // Base Case
    if (N == 1)
    {
        ans.Add(num);
        return;
    }

    // Check the sum of last digit and k
    // less than or equal to 9 or not
    if ((num % 10 + K) <= 9)
        checkUntil(10 * num + (num % 10 + K),
                 K, N - 1, ans);

    // If k==0, then subtraction and
    // addition does not make any
    // difference
    // Hence, subtraction is skipped
    if (K > 0)
    {
        if ((num % 10 - K) >= 0)
            checkUntil(10 * num + num % 10 - K,
                     K, N - 1, ans);
    }
}

// Function to call checkUntil function
// for every integer from 1 to 9
static void check(int K, int N, List<int> ans)
{

    // check_util function recursively
    // store all numbers starting from i
    for(int i = 1; i <= 9; i++)
    {
        checkUntil(i, K, N, ans);
    }
}

// Function to print the all numbers
// which satisfy the conditions
static void print(List<int> ans)
{
    for(int i = 0; i < ans.Count; i++)
    {
        Console.Write(ans[i] + ", ");
    }
}

// Driver Code
public static void Main(String[] args)
{

    // Given N and K
    int N = 4, K = 8;

    // To store the result
    List<int> ans = new List<int>();;

    // Function call
    check(K, N, ans);

    // Print Resultant Numbers
    print(ans);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

    // Function that recursively finds the
    // possible numbers and append into ans
    function checkUntil(num, K, N,
                           ans)
    {

        // Base Case
        if (N == 1)
        {
            ans.push(num);
            return;
        }

        // Check the sum of last digit and k
        // less than or equal to 9 or not
        if ((num % 10 + K) <= 9)
            checkUntil(10 * num + (num % 10 + K),
                       K, N - 1, ans);

        // If k==0, then subtraction and
        // addition does not make any
        // difference
        // Hence, subtraction is skipped
        if (K > 0)
        {
            if ((num % 10 - K) >= 0)
                checkUntil(10 * num + num % 10 - K,
                           K, N - 1, ans);
        }
    }

    // Function to call checkUntil function
    // for every integer from 1 to 9
    function check(K, N, ans)
    {

        // check_util function recursively
        // store all numbers starting from i
        for (let i = 1; i <= 9; i++)
        {
            checkUntil(i, K, N, ans);
        }
    }

    // Function to print the all numbers
    // which  satisfy the conditions
    function print( ans)
    {
        for (let i = 0; i < ans.length; i++)
        {
            document.write(ans[i] + ", ");
        }
    }

// Driver Code

    // Given N and K
        let N = 4, K = 8;

        // To store the result
        let ans = []

        // Function Call
        check(K, N, ans);

        // Print Resultant Numbers
        print(ans);

</script>
```

**Output:** 

```
1919, 8080, 9191,
```

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(N)*