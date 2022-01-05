# 圣埃克苏佩里号

> 原文:[https://www.geeksforgeeks.org/saint-exupery-numbers/](https://www.geeksforgeeks.org/saint-exupery-numbers/)

**圣埃克苏佩里数**一个数 **N** 这样 **N** 就是毕达哥拉斯三角形三边的乘积。
圣埃克苏佩里的一些号码是:

> 60, 480, 780, 1620, 2040, 3840, 4200, 6240, 7500, 12180….

### 检查 N 是否是圣埃克苏佩里数字

给定一个数字 **N** ，任务是检查 **N** 是否为**圣埃克苏佩里号**。如果 **N** 是圣埃克苏佩里号，则打印**“是”**否则打印**“否”**。
**示例:**

> **输入:** N = 60
> **输出:** Yes
> **解释:**
> 60 = 3 * 4 * 5 和 3^2 + 4^2 = 5^2.
> **输入:** N = 120
> **输出:**否

**天真方法:**一个简单的解决方案是运行三个嵌套循环来生成所有可能的三元组，对于每个三元组，检查它是否是毕达哥拉斯三元组并且已经给出了乘积。这个解的时间复杂度为 O(n <sup>3</sup> )。
**高效途径:**思路是运行两个循环，其中第一个循环从 i = 1 运行到 n/3，第二个循环从 j = i+1 运行到 n/2。在第二个循环中，我们检查(n / i / j)是否等于 I * I+j * j。
下面是上述方法的实现:

## C++

```
// C++ implementation to check if N
// is a Saint-Exupery number

#include <bits/stdc++.h>
using namespace std;

// Function to check if a number is
//  a Saint-Exupery number
bool isSaintExuperyNum(int n)
{
    // Considering triplets in
    // sorted order. The value
    // of first element in sorted
    // triplet can be at-most n/3.
    for (int i = 1; i <= n / 3; i++) {

        // The value of second
        // element must be less
        // than equal to n/2
        for (int j = i + 1; j <= n / 2; j++) {
            int k = n / i / j;
            if (i * i + j * j == k * k) {
                if (i * j * k == n)
                    return true;
                ;
            }
        }
    }

    return false;
}

// Driver Code
int main()
{
    // Given Number N
    int N = 60;

    // Function Call
    if (isSaintExuperyNum(N))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
class GFG{

// Function to check if a number is
// a Saint-Exupery number
static boolean isSaintExuperyNum(int n)
{
    // Considering triplets in
    // sorted order. The value
    // of first element in sorted
    // triplet can be at-most n/3.
    for (int i = 1; i <= n / 3; i++)
    {

        // The value of second
        // element must be less
        // than equal to n/2
        for (int j = i + 1; j <= n / 2; j++)
        {
            int k = n / i / j;
            if (i * i + j * j == k * k)
            {
                if (i * j * k == n)
                    return true;
            }
        }
    }

    return false;
}

// Driver Code
public static void main(String[] args)
{
    // Given Number N
    int N = 60;

    // Function Call
    if (isSaintExuperyNum(N))
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code is contributed by Shubham Prakash
```

## 蟒蛇 3

```
# Python3 implementation to check if N
# is a Saint-Exupery number

# Function to check if a number is
# a Saint-Exupery number
def isSaintExuperyNum(n):

    # Considering triplets in
    # sorted order. The value
    # of first element in sorted
    # triplet can be at-most n/3.
    for i in range(1, (n // 3) + 1):

        # The value of second
        # element must be less
        # than equal to n/2
        for j in range(i + 1, (n // 2) + 1):
            k = n / i / j
            if i * i + j * j == k * k:
                if i * j * k == n:
                    return True

    return False

# Driver Code

# Given Number N
N = 60

# Function Call
if isSaintExuperyNum(N):
    print("Yes")
else:
    print("No")

# This code is contributed by
# divyamohan123
```

## C#

```
// C# program for above approach
using System;
class GFG{

// Function to check if a number is
// a Saint-Exupery number
static bool isSaintExuperyNum(int n)
{
    // Considering triplets in
    // sorted order. The value
    // of first element in sorted
    // triplet can be at-most n/3.
    for (int i = 1; i <= n / 3; i++)
    {

        // The value of second
        // element must be less
        // than equal to n/2
        for (int j = i + 1; j <= n / 2; j++)
        {
            int k = n / i / j;
            if (i * i + j * j == k * k)
            {
                if (i * j * k == n)
                    return true;
            }
        }
    }

    return false;
}

// Driver Code
public static void Main()
{
    // Given Number N
    int N = 60;

    // Function Call
    if (isSaintExuperyNum(N))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// Javascript program for above approach

    // Function to check if a number is
    // a Saint-Exupery number
    function isSaintExuperyNum( n) {
        // Considering triplets in
        // sorted order. The value
        // of first element in sorted
        // triplet can be at-most n/3.
        for ( i = 1; i <= n / 3; i++) {

            // The value of second
            // element must be less
            // than equal to n/2
            for ( j = i + 1; j <= n / 2; j++) {
                let k = n / i / j;
                if (i * i + j * j == k * k) {
                    if (i * j * k == n)
                        return true;
                }
            }
        }

        return false;
    }

    // Driver Code

        // Given Number N
        let N = 60;

        // Function Call
        if (isSaintExuperyNum(N))
            document.write("Yes");
        else
            document.write("No");

// This code contributed by gauravrajput1

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:***o(n^2)*
t5】参考:[http://www.numbersaplenty.com/set/Saint-Exupery_number/](http://www.numbersaplenty.com/set/Saint-Exupery_number/)T9】