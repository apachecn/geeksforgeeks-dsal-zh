# 检查一个数是否可以表示为至少有一位等于 K 的数的和

> 原文:[https://www . geesforgeks . org/check-如果一个数字可以表示为至少有一位数字等于 k 的数字总和/](https://www.geeksforgeeks.org/check-if-a-number-can-be-represented-as-the-sum-of-numbers-with-at-least-one-digit-equal-to-k/)

给定整数 **N** 和 **K** ，任务是检查一个数是否可以表示为至少有一个数字等于 K 的数的和

**示例:**

> **输入:** N = 68，K = 7
> **输出:** YES
> **解释:** 68 = (27 + 17 + 17 + 7)。每个数字至少有一个等于 7 的数字。
> 
> **输入:** N = 23，K = 3
> **输出:** YES
> **说明:** 23 本身包含一个等于 3 的数字。

**方法:**给定的问题可以通过使用[数学](https://www.geeksforgeeks.org/what-is-the-importance-of-mathematics-in-computer-science/)的简单概念来解决。按照以下步骤解决问题:

*   将一个变量 **temp** 初始化为 **k** ，同时取一个计数器说**计数**，赋 0
*   迭代至**温度**和 **N** 的最后一位不相等，每次迭代
    *   将**温度**的值增加 **k**
    *   保持迭代次数**计数**，如果计数大于 10，则中断循环
*   检查**温度**和 **N** 的最后一位数字是否相等，如果**温度** **< =** **N** 的值:
    *   如果满足上述条件，返回真
    *   否则返回 false
*   同样如果 **k * 10 < = N** ，返回真
*   否则返回 false

下面是上述方法的实现:

## C++

```
// C++ implementation for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to Check if a number can
// be equal to sum of numbers having
// at least one digit equal to k
bool checkEqualtoSum(int N, int k)
{
    // Temporary variable to
    // store k
    int temp = k;

    // Variable for count
    int count = 0;

    // Iterating till count is less or
    // equal to 10 and N % 10 is not
    // equal to temp % 10
    while(count <= 10 &&
                  N % 10 != temp % 10) {

        temp += k;
        count++;
    }

    // If N % 10 is equal to temp % 10
    // and temp is less or equal to N,
    // return true
    if(N % 10 == temp % 10 && temp <= N)
        return true;

    // If k * 10 <= N, return true
    if(k * 10 <= N)
        return true;

    // Else return false
    return false;
}

// Driver Code
int main()
{
    int N = 68;
    int K = 7;

      // Call the function
    if(checkEqualtoSum(N, K))
          cout << "YES";
    else cout << "NO";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
class GFG {

    // Function to Check if a number can
    // be equal to sum of numbers having
    // at least one digit equal to k
    static boolean checkEqualtoSum(int N, int k)
    {
        // Temporary variable to
        // store k
        int temp = k;

        // Variable for count
        int count = 0;

        // Iterating till count is less or
        // equal to 10 and N % 10 is not
        // equal to temp % 10
        while (count <= 10 && N % 10 != temp % 10) {

            temp += k;
            count++;
        }

        // If N % 10 is equal to temp % 10
        // and temp is less or equal to N,
        // return true
        if (N % 10 == temp % 10 && temp <= N)
            return true;

        // If k * 10 <= N, return true
        if (k * 10 <= N)
            return true;

        // Else return false
        return false;
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given Input
        int N = 68;
        int K = 7;

        // Call the function
        if (checkEqualtoSum(N, K))
            System.out.println("YES");
        else
            System.out.println("NO");
    }
}

// This code is contributed by dwivediyash
```

## 蟒蛇 3

```
# python implementation for the above approach

# Function to Check if a number can
# be equal to sum of numbers having
# at least one digit equal to k

def checkEqualtoSum(N, k):

    # Temporary variable to
    # store k
    temp = k

    # Variable for count
    count = 0

    # Iterating till count is less or
    # equal to 10 and N % 10 is not
    # equal to temp % 10
    while(count <= 10 and N % 10 != temp % 10):

        temp += k
        count += 1

    # If N % 10 is equal to temp % 10
    # and temp is less or equal to N,
    # return true
    if(N % 10 == temp % 10 and temp <= N):
        return True

    # If k * 10 <= N, return true
    if(k * 10 <= N):
        return True

    # Else return false
    return False

# Driver Code
if __name__ == "__main__":

    N = 68
    K = 7

    # Call the function
    if(checkEqualtoSum(N, K)):
        print("YES")
    else:
        print("NO")

    # This code is contributed by rakeshsahni
```

## java 描述语言

```
<script>
    // JavaScript implementation for the above approach

    // Function to Check if a number can
    // be equal to sum of numbers having
    // at least one digit equal to k
    const checkEqualtoSum = (N, k) => {
        // Temporary variable to
        // store k
        let temp = k;

        // Variable for count
        let count = 0;

        // Iterating till count is less or
        // equal to 10 and N % 10 is not
        // equal to temp % 10
        while (count <= 10 &&
            N % 10 != temp % 10) {

            temp += k;
            count++;
        }

        // If N % 10 is equal to temp % 10
        // and temp is less or equal to N,
        // return true
        if (N % 10 == temp % 10 && temp <= N)
            return true;

        // If k * 10 <= N, return true
        if (k * 10 <= N)
            return true;

        // Else return false
        return false;
    }

    // Driver Code
    let N = 68;
    let K = 7;

    // Call the function
    if (checkEqualtoSum(N, K))
        document.write("YES");
    else document.write("NO");

    // This code is contributed by rakeshsahni

</script>
```

## C#

```
// C# implementation for the above approach
using System;
class gFG
{

    // Function to Check if a number can
    // be equal to sum of numbers having
    // at least one digit equal to k
    static bool checkEqualtoSum(int N, int k)
    {
        // Temporary variable to
        // store k
        int temp = k;

        // Variable for count
        int count = 0;

        // Iterating till count is less or
        // equal to 10 and N % 10 is not
        // equal to temp % 10
        while (count <= 10 && N % 10 != temp % 10) {

            temp += k;
            count++;
        }

        // If N % 10 is equal to temp % 10
        // and temp is less or equal to N,
        // return true
        if (N % 10 == temp % 10 && temp <= N)
            return true;

        // If k * 10 <= N, return true
        if (k * 10 <= N)
            return true;

        // Else return false
        return false;
    }

    // Driver Code
    public static void Main()
    {
        int N = 68;
        int K = 7;

        // Call the function
        if (checkEqualtoSum(N, K))
            Console.WriteLine("YES");
        else
            Console.WriteLine("NO");
    }
}

// This code is contributed by ukasp.
```

**Output**

```
YES
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)