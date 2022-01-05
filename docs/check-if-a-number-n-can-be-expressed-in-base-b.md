# 检查一个数字 N 是否可以用基数 B 表示

> 原文:[https://www . geesforgeks . org/check-if-a-number-n-can-express-in-base-b/](https://www.geeksforgeeks.org/check-if-a-number-n-can-be-expressed-in-base-b/)

给定一个数字 **N** 和任意一个基数 **B** 。任务是检查 **N** 是否可以用**a<sub>1</sub>* b<sup>0</sup>+a<sub>2</sub>* b<sup>1</sup>+a<sub>3</sub>* b<sup>2</sup>+…。+a<sub>101</sub>* b<sup>100</sup>**其中各系数 **a <sub>1</sub> ，a <sub>2</sub> ，a<sub>3</sub>…a<sub>101</sub>T33】为 **0，1 或-1** 。**

**示例:**

> **输入:** B = 3，N = 7
> **输出:**是
> **说明:**
> 数字 7 可以表示为 1 * 3<sup>0</sup>+(-1)* 3<sup>1</sup>+1 * 3<sup>2</sup>= 1–3+9。
> 
> **输入:** B = 100，N = 50
> **输出:**否
> **说明:**
> 这个数字没有可能的表达方式。

**进场:**以下是步骤:

*   如果 **N** 的基本 **B** 表示仅由**0 和 1**组成，则答案存在。
*   如果不满足上述条件，则从**低位向高位**迭代，如果该位不等于 0 或 1，则尝试从中减去 **B** 的适当幂，并增加高位。
*   如果变成等于 **-1** ，那么我们可以减去这个幂位数，如果变成等于 0，那么就直接忽略，其他情况下，用要求的形式表示数字是不可能的。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if a number
// N can be expressed in base B
bool check(int n, int w)
{
    vector<int> a(105);
    int p = 0;

    // Check if n is greater than 0
    while (n > 0) {
        a[p++] = n % w;
        n /= w;
    }

    // Initialize a boolean variable
    bool flag = true;

    for (int i = 0; i <= 100; i++) {

        // Check if digit is 0 or 1
        if (a[i] == 0 || a[i] == 1)
            continue;

        // Subtract the appropriate
        // power of B from it and
        // increment higher digit
        else if (a[i] == w
                 || a[i] == w - 1)
            a[i + 1]++;

        else
            flag = false;
    }

    return flag;
}

// Driver Code
int main()
{
    // Given Number N and base B
    int B = 3, N = 7;

    // Function Call
    if (check(N, B))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to check if a number
// N can be expressed in base B
static boolean check(int n, int w)
{
    int[] a = new int[105];
    int p = 0;

    // Check if n is greater than 0
    while (n > 0)
    {
        a[p++] = n % w;
        n /= w;
    }

    // Initialize a boolean variable
    boolean flag = true;

    for(int i = 0; i <= 100; i++)
    {

        // Check if digit is 0 or 1
        if (a[i] == 0 || a[i] == 1)
            continue;

        // Subtract the appropriate
        // power of B from it and
        // increment higher digit
        else if (a[i] == w || a[i] == w - 1)
            a[i + 1]++;

        else
            flag = false;
    }
    return flag;
}

// Driver Code
public static void main(String[] args)
{

    // Given number N and base B
    int B = 3, N = 7;

    // Function call
    if (check(N, B))
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if a number
# N can be expressed in base B
def check(n, w):

    a = [0 for i in range(105)];
    p = 0

    # Check if n is greater than 0
    while (n > 0):
        a[p] = n % w
        p += 1
        n //= w

    # Initialize a boolean variable
    flag = True

    for i in range(101):

        # Check if digit is 0 or 1
        if (a[i] == 0 or a[i] == 1):
            continue

        # Subtract the appropriate
        # power of B from it and
        # increment higher digit
        elif (a[i] == w or a[i] == w - 1):
            a[i + 1] += 1
        else:
            flag = False

    return flag

# Driver code
if __name__=="__main__":

    # Given number N and base B
    B = 3
    N = 7

    # Function call
    if (check(N, B)):
        print("Yes")
    else:
        print("No")

# This code is contributed by rutvik_56
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if a number
// N can be expressed in base B
static bool check(int n, int w)
{
    int[] a = new int[105];
    int p = 0;

    // Check if n is greater than 0
    while (n > 0)
    {
        a[p++] = n % w;
        n /= w;
    }

    // Initialize a bool variable
    bool flag = true;

    for(int i = 0; i <= 100; i++)
    {

        // Check if digit is 0 or 1
        if (a[i] == 0 || a[i] == 1)
            continue;

        // Subtract the appropriate
        // power of B from it and
        // increment higher digit
        else if (a[i] == w || a[i] == w - 1)
            a[i + 1]++;

        else
            flag = false;
    }
    return flag;
}

// Driver Code
public static void Main(String[] args)
{

    // Given number N and base B
    int B = 3, N = 7;

    // Function call
    if (check(N, B))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>
// javascript program for the above approach   

    // Function to check if a number
    // N can be expressed in base B
    function check(n , w) {
        var a = Array(105).fill(0);
        var p = 0;

        // Check if n is greater than 0
        while (n > 0) {
            a[p++] = n % w;
            n /= w;
            n = parseInt(n);
        }

        // Initialize a boolean variable
        var flag = true;

        for (i = 0; i <= 100; i++) {

            // Check if digit is 0 or 1
            if (a[i] == 0 || a[i] == 1)
                continue;

            // Subtract the appropriate
            // power of B from it and
            // increment higher digit
            else if (a[i] == w || a[i] == w - 1)
                a[i + 1]++;

            else
                flag = false;
        }
        return flag;
    }

    // Driver Code

        // Given number N and base B
        var B = 3, N = 7;

        // Function call
        if (check(N, B))
            document.write("Yes");
        else
            document.write("No");

// This code is contributed by gauravrajput1
</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(log<sub>B</sub>N)*
***辅助空间:** O(1)*