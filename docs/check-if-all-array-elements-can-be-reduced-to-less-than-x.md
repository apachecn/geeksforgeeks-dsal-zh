# 检查是否所有数组元素都可以减少到 X 以下

> 原文:[https://www . geesforgeks . org/check-if-all-array-elements-can-reduce-小于-x/](https://www.geeksforgeeks.org/check-if-all-array-elements-can-be-reduced-to-less-than-x/)

给定一个由 **N** 个正整数和一个整数 **X** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **A[]** ，任务是通过执行以下操作来确定是否有可能将所有数组元素转换为小于 **X** :

*   选择 2 个不同的指数 **j** 和 **k** 。
*   选择一个索引 **i** ，其中**A【I】>X**。
*   当且仅当 [gcd](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) (A[j]，A[k])1 时，替换 **A[i] = gcd(A[j]，A[k])。**

**示例:**

> ***输入:** A[] = {2，1，5，3，6}，X = 4*
> ***输出:**是*
> ***解释:***
> 
> *   *选择 i = 3，j = 4，k = 5，设置 A[i] = gcd(A[j]，A[k]) = 3。因此，A[]修改为{2，1，3，3，6}。*
> *   *选择 i = 5，j = 4，k = 5，设置 A[i] = gcd(A[j]，A[k]) = 3。因此，A[]修改为{2，1，3，3，3}。*
> 
> ***输入:** A[] = {2，3，2，5，4}，X = 3*
> ***输出:**是*

***进场:**按照以下步骤解决问题:*

1.  *找到两个分别有 **gcd ≠ 1** 和 **gcd ≤ X** 的数字，然后，通过使用*这两个*数字，所需的数字 **A[i]** 可以替换为 **gcd(A[j]，A[k])** 。*
2.  利用 **gcd(x，y) ≤ min(x，y)** 的事实，可以将数组元素简化为 **≤ X** 。
3.  这样，使用步骤 **2** 可以将数组的其余部分转换为 **≤ X** 。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if all array
// elements are≤ X
bool check(int A[], int X, int N)
{
    for(int i = 0; i < N; i++)
    {
        if (A[i] > X)
        {
            return false;
        }
    }
    return true;
}

// Function to check if all array elements
// can be reduced to less than X or not
bool findAns(int A[], int N, int X)
{

    // Checks if all array elements
    // are already ≤ X or not
    if (check(A, X, N))
    {
        return true;
    }

    // Traverse every possible pair
    for(int i = 0; i < N; i++)
    {
        for(int j = i + 1; j < N; j++)
        {

            // Calculate GCD of two
            // array elements
            int g = __gcd(A[i], A[j]);

            // If gcd is ≠ 1
            if (g != 1)
            {

                // If gcd is ≤ X, then a pair
                // is present to reduce all
                // array elements to ≤ X
                if (g <= X)
                {
                    return true;
                }
            }
        }
    }

    // If no pair is present
    // with gcd is ≤ X
    return false;
}

// Driver Code
int main()
{
    int X = 4;
    int A[] = { 2, 1, 5, 3, 6 };
    int N = 5;

    if (findAns(A, N, X))
    {
        cout << "true";
    }
    else
    {
        cout << "false";
    }
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach

import java.io.*;
import java.util.Arrays;

class GFG {

    // Function to check if all array elements
    // can be reduced to less than X or not
    public static boolean findAns(
        int[] A, int N, int X)
    {
        // Checks if all array elements
        // are already ≤ X or not
        if (check(A, X)) {
            return true;
        }

        // Traverse every possible pair
        for (int i = 0; i < N; i++) {
            for (int j = i + 1; j < N; j++) {

                // Calculate GCD of two
                // array elements
                int gcd = gcd(A[i], A[j]);

                // If gcd is ≠ 1
                if (gcd != 1) {

                    // If gcd is ≤ X, then a pair
                    // is present to reduce all
                    // array elements to ≤ X
                    if (gcd <= X) {

                        return true;
                    }
                }
            }
        }

        // If no pair is present
        // with gcd is ≤ X
        return false;
    }

    // Function to check if all array elements are≤ X
    public static boolean check(int[] A, int X)
    {
        for (int i = 0; i < A.length; i++) {
            if (A[i] > X) {
                return false;
            }
        }
        return true;
    }

    // Function to calculate gcd of two numbers
    public static int gcd(int a, int b)
    {
        if (b == 0)
            return a;
        return gcd(b, a % b);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int X = 4;
        int[] A = { 2, 1, 5, 3, 6 };
        int N = 5;

        System.out.println(findAns(A, N, X));
    }
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to check if all array elements
# can be reduced to less than X or not
def findAns(A, N, X):

  # Checks if all array elements
  # are already ≤ X or not
  if (check(A, X)):
    return True

  # Traverse every possible pair
  for i in range(N):
    for j in range(i + 1, N):

      # Calculate GCD of two
      # array elements
      gcd = GCD(A[i], A[j])

      # If gcd is ≠ 1
      if (gcd != 1):

        # If gcd is ≤ X, then a pair
        # is present to reduce all
        # array elements to ≤ X
        if (gcd <= X):
          return True

  # If no pair is present
  # with gcd is ≤ X
  return False

# Function to check if all array elements are≤ X
def check(A, X):
  for i in range(len(A)):
    if (A[i] > X):
      return False
  return True

# Function to calculate gcd of two numbers
def GCD(a, b):
  if (b == 0):
    return a
  return GCD(b, a % b)

# Driver Code
X = 4
A = [ 2, 1, 5, 3, 6 ]
N = 5

print(findAns(A, N, X))

# This code is contributed by rohitsingh07052
```

## C#

```
// C# Program to implement
// the above approach
using System;
class GFG {

    // Function to check if all array elements
    // can be reduced to less than X or not
    public static bool findAns(
        int[] A, int N, int X)
    {
        // Checks if all array elements
        // are already ≤ X or not
        if (check(A, X))
        {
            return true;
        }

        // Traverse every possible pair
        for (int i = 0; i < N; i++)
        {
            for (int j = i + 1; j < N; j++)
            {

                // Calculate GCD of two
                // array elements
                int gcd = gcdFoo(A[i], A[j]);

                // If gcd is ≠ 1
                if (gcd != 1)
                {

                    // If gcd is ≤ X, then a pair
                    // is present to reduce all
                    // array elements to ≤ X
                    if (gcd <= X)
                    {
                        return true;
                    }
                }
            }
        }

        // If no pair is present
        // with gcd is ≤ X
        return false;
    }

    // Function to check if all array elements are≤ X
    public static bool check(int[] A, int X)
    {
        for (int i = 0; i < A.Length; i++)
        {
            if (A[i] > X)
            {
                return false;
            }
        }
        return true;
    }

    // Function to calculate gcd of two numbers
    static int gcdFoo(int a, int b)
    {
        if (b == 0)
            return a;
        return gcdFoo(b, a % b);
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int X = 4;
        int[] A = { 2, 1, 5, 3, 6 };
        int N = 5;

        Console.WriteLine(findAns(A, N, X));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// javascript program of the above approach

    // Function to check if all array elements
    // can be reduced to less than X or not
    function findAns(
         A, N, X)
    {
        // Checks if all array elements
        // are already ≤ X or not
        if (check(A, X)) {
            return true;
        }

        // Traverse every possible pair
        for (let i = 0; i < N; i++) {
            for (let j = i + 1; j < N; j++) {

                // Calculate GCD of two
                // array elements
                let gcdd = gcd(A[i], A[j]);

                // If gcd is ≠ 1
                if (gcdd != 1) {

                    // If gcd is ≤ X, then a pair
                    // is present to reduce all
                    // array elements to ≤ X
                    if (gcdd <= X) {

                        return true;
                    }
                }
            }
        }

        // If no pair is present
        // with gcd is ≤ X
        return false;
    }

    // Function to check if all array elements are≤ X
    function check(A, X)
    {
        for (let i = 0; i < A.length; i++) {
            if (A[i] > X) {
                return false;
            }
        }
        return true;
    }

    // Function to calculate gcd of two numbers
    function gcd(a, b)
    {
        if (b == 0)
            return a;
        return gcd(b, a % b);
    }

    // Driver Code

        let X = 4;
        let A = [ 2, 1, 5, 3, 6 ];
        let N = 5;

        document.write(findAns(A, N, X));

// This code is contributed by target_2.
</script>
```

**Output**

```
true
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*