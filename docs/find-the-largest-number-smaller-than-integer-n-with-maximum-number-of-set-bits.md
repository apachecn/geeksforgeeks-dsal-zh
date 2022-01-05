# 用最大设定位数找到小于整数 N 的最大数值

> 原文:[https://www . geeksforgeeks . org/find-最大数-小于整数 n-具有最大集合位数/](https://www.geeksforgeeks.org/find-the-largest-number-smaller-than-integer-n-with-maximum-number-of-set-bits/)

给定一个**整数 N** ，任务是找到比具有最大设置位数的 N 小的**最大值。
**例:**** 

> **输入:** N = 345
> **输出:** 255
> **解释:**
> 二进制表示的 345 为 101011001，有 5 个设置位，255 为 111111111，最大设置位数小于整数 N.
> **输入:** N = 2
> **输出:** 1
> **解释:【T11**

**天真方法:**
解决上述问题的天真方法是迭代到整数 N，求出每个数的集合位数，并存储每一步集合位数最大的数。
以下是上述办法的实施:

## C++

```
// C++ implementation to Find the
// largest number smaller than integer
// N with maximum number of set bits
#include <bits/stdc++.h>
using namespace std;

// Function to return the largest
// number less than N
int largestNum(int n)
{
    int num = 0;

    int max_setBits = 0;

    // Iterate through all the numbers
    for (int i = 0; i <= n; i++) {

        // Find the number of set bits
        // for the current number
        int setBits = __builtin_popcount(i);

        // Check if this number has the
        // highest set bits
        if (setBits >= max_setBits) {
            num = i;
            max_setBits = setBits;
        }
    }

    // Return the result
    return num;
}

// Driver code
int main()
{
    int N = 345;

    cout << largestNum(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to Find the
// largest number smaller than integer
// N with maximum number of set bits
class GFG
{

    /* Function to get no of set
    bits in binary representation
    of positive integer n */
    static int countSetBits(int n)
    {
        int count = 0;
        while (n > 0)
        {
            count += n & 1;
            n >>= 1;
        }
        return count;
    }

    // Function to return the largest
    // number less than N
    static int largestNum(int n)
    {
        int num = 0;

        int max_setBits = 0;

        // Iterate through all the numbers
        for (int i = 0; i <= n; i++)
        {

            // Find the number of set bits
            // for the current number
            int setBits = countSetBits(i);

            // Check if this number has the
            // highest set bits
            if (setBits >= max_setBits)
            {
                num = i;
                max_setBits = setBits;
            }
        }

        // Return the result
        return num;
    }

    // Driver code
    public static void main (String[] args)
    {
        int N = 345;

        System.out.println(largestNum(N));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation to find the
# largest number smaller than integer
# N with maximum number of set bits

# Function to return the largest
# number less than N
def largestNum(n):

    num = 0;
    max_setBits = 0;

    # Iterate through all the numbers
    for i in range(n + 1):

        # Find the number of set bits
        # for the current number
        setBits = bin(i).count('1');

        # Check if this number has the
        # highest set bits
        if (setBits >= max_setBits):
            num = i;
            max_setBits = setBits;

    # Return the result
    return num;

# Driver code
if __name__ == "__main__" :

    N = 345;

    print(largestNum(N));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation to Find the
// largest number smaller than integer
// N with a maximum number of set bits
using System;

class GFG{   

// Function to get no of set
// bits in binary representation
// of positive integer n
static int countSetBits(int n)
{
    int count = 0;
    while (n > 0)
    {
        count += n & 1;
        n >>= 1;
    }
    return count;
}

// Function to return the largest
// number less than N
static int largestNum(int n)
{
    int num = 0;
    int max_setBits = 0;

    // Iterate through all the numbers
    for(int i = 0; i <= n; i++)
    {

       // Find the number of set bits
       // for the current number
       int setBits = countSetBits(i);

       // Check if this number has
       // the  highest set bits
       if (setBits >= max_setBits)
       {
           num = i;
           max_setBits = setBits;
       }
    }

    // Return the result
    return num;
}

// Driver code
public static void Main(String[] args)
{
    int N = 345;

    Console.Write(largestNum(N));
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

    // Javascript implementation to Find the
    // largest number smaller than integer
    // N with a maximum number of set bits

    // Function to get no of set
    // bits in binary representation
    // of positive integer n
    function countSetBits(n)
    {
        let count = 0;
        while (n > 0)
        {
            count += n & 1;
            n >>= 1;
        }
        return count;
    }

    // Function to return the largest
    // number less than N
    function largestNum(n)
    {
        let num = 0;
        let max_setBits = 0;

        // Iterate through all the numbers
        for(let i = 0; i <= n; i++)
        {

           // Find the number of set bits
           // for the current number
           let setBits = countSetBits(i);

           // Check if this number has
           // the  highest set bits
           if (setBits >= max_setBits)
           {
               num = i;
               max_setBits = setBits;
           }
        }

        // Return the result
        return num;
    }

    let N = 345;

    document.write(largestNum(N));

</script>
```

**Output:** 

```
255
```

***时间复杂度:** O(n)*

***辅助空间:** O(1)*

**有效方法:**为了优化上述解决方案，我们必须观察到具有最高设置位的数字肯定是形式 2<sup>k</sup>–1。因此，我们只需要迭代 k 的可能值，并找到仅小于整数 N 的最高值。由于我们迭代指数变量，因此最多需要 log(N)步。
以下是上述方法的实施:

## C++

```
// C++ implementation to Find the
// largest number smaller than integer
// N with maximum number of set bits
#include <bits/stdc++.h>
using namespace std;

// Function to return the largest
// number less than N
int largestNum(int n)
{

    int num = 0;

    // Iterate through all possible values
    for (int i = 0; i <= 32; i++)
    {
        // Multiply the number by 2 i times
        int x = (1 << i);

        if ((x - 1) <= n)
            num = (1 << i) - 1;

        else
            break;
    }

    // Return the final result
    return num;
}

// Driver code
int main()
{
    int N = 345;

    cout << largestNum(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to Find the
// largest number smaller than integer
// N with maximum number of set bits
import java.util.*;
class GFG{

// Function to return the largest
// number less than N
static int largestNum(int n)
{
    int num = 0;

    // Iterate through all possible values
    for (int i = 0; i <= 32; i++)
    {
        // Multiply the number by 2 i times
        int x = (1 << i);

        if ((x - 1) <= n)
            num = (1 << i) - 1;

        else
            break;
    }

    // Return the final result
    return num;
}

// Driver code
public static void main(String args[])
{
    int N = 345;

    System.out.print(largestNum(N));
}
}

// This code is contributed by Akanksha_Rai
```

## 蟒蛇 3

```
# Python3 implementation to find the
# largest number smaller than integer
# N with the maximum number of set bits

# Function to return the largest
# number less than N
def largestNum(n):

    num = 0;

    # Iterate through all possible
    # values
    for i in range(32):

        # Multiply the number by
        # 2 i times
        x = (1 << i);

        if ((x - 1) <= n):
            num = (1 << i) - 1;
        else:
            break;

    # Return the final result
    return num;

# Driver code
if __name__ == "__main__":

    N = 345;

    print(largestNum(N));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation to Find the
// largest number smaller than integer
// N with maximum number of set bits
using System;
class GFG{

// Function to return the largest
// number less than N
static int largestNum(int n)
{
    int num = 0;

    // Iterate through all possible values
    for (int i = 0; i <= 32; i++)
    {
        // Multiply the number by 2 i times
        int x = (1 << i);

        if ((x - 1) <= n)
            num = (1 << i) - 1;

        else
            break;
    }

    // Return the final result
    return num;
}

// Driver code
public static void Main()
{
    int N = 345;

    Console.Write(largestNum(N));
}
}

// This code is contributed by Nidhi_Biet
```

## java 描述语言

```
<script>
    // Javascript implementation to Find the
    // largest number smaller than integer
    // N with maximum number of set bits

    // Function to return the largest
    // number less than N
    function largestNum(n)
    {

        let num = 0;

        // Iterate through all possible values
        for (let i = 0; i <= 32; i++)
        {
            // Multiply the number by 2 i times
            let x = (1 << i);

            if ((x - 1) <= n)
                num = (1 << i) - 1;

            else
                break;
        }

        // Return the final result
        return num;
    }

    let N = 345;

    document.write(largestNum(N));

    // This code is contributed by suresh07.
</script>
```

**Output:** 

```
255
```

**时间复杂度:** O(对数 N)

**辅助空间:** O(1)