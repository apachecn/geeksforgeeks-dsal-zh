# 两个给定数字之间的完美立方体的数量

> 原文:[https://www . geesforgeks . org/两个给定数字之间的完美立方体数量/](https://www.geeksforgeeks.org/number-of-perfect-cubes-between-two-given-numbers/)

给定两个给定的数字 **a** 和 **b** ，其中 1 < =a < =b，求 a 和 b(包括 a 和 b)之间的完美立方体的数量。
**例** :

```
Input :  a = 3, b = 16
Output : 1
The only perfect cube in given range is 8.

Input : a = 7, b = 30
Output : 2
The two cubes in given range are 8, 
and 27
```

**方法 1** :一个比较天真的做法是检查 a 和 b(包括 a 和 b)之间的所有数字，每当我们遇到一个完美的立方体时，就把计数增加一。

以下是上述思路的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// A Simple Method to count cubes between a and b
#include <bits/stdc++.h>
using namespace std;

// Function to count cubes between two numbers
int countCubes(int a, int b)
{
    int cnt = 0; // Initialize result

    // Traverse through all numbers
    for (int i = a; i <= b; i++)

        // Check if current number 'i' is perfect
        // cube
        for (int j = 1; j * j * j <= i; j++)
            if (j * j * j == i)
                cnt++;

    return cnt;
}

// Driver code
int main()
{
    int a = 7, b = 30;
    cout << "Count of Cubes is "
         << countCubes(a, b);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Simple Method to count cubes between a and b

class GFG{

// Function to count cubes between two numbers
static int countCubes(int a, int b)
{
    int cnt = 0; // Initialize result

    // Traverse through all numbers
    for (int i = a; i <= b; i++)

        // Check if current number 'i' is perfect
        // cube
        for (int j = 1; j * j * j <= i; j++)
            if (j * j * j == i)
                cnt++;

    return cnt;
}

// Driver code
public static void main(String[] args)
{
    int a = 7, b = 30;
    System.out.print("Count of Cubes is "
         + countCubes(a, b));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# A Simple Method to count cubes between a and b

# Function to count cubes between two numbers
def countCubes(a, b):
    cnt = 0 # Initialize result

    # Traverse through all numbers
    for i in range(a,b+1):

        # Check if current number 'i' is perfect
        # cube
        for j in range(i+1):
            if j*j*j>i:
                break
            if j * j * j == i:
                cnt+=1

    return cnt

# Driver code
if __name__ == '__main__':
    a = 7
    b = 30
    print("Count of Cubes is ",countCubes(a, b))

# This code is contributed by mohit kumar 29
```

## C#

```
// A Simple Method to count cubes between a and b
using System;

class GFG{

// Function to count cubes between two numbers
static int countCubes(int a, int b)
{
    int cnt = 0; // Initialize result

    // Traverse through all numbers
    for (int i = a; i <= b; i++)

        // Check if current number 'i' is perfect
        // cube
        for (int j = 1; j * j * j <= i; j++)
            if (j * j * j == i)
                cnt++;

    return cnt;
}

// Driver code
public static void Main()
{
    int a = 7, b = 30;
    Console.Write("Count of Cubes is "
         + countCubes(a, b));
}
}

// This code is contributed by chitranayal
```

## java 描述语言

```
<script>
// JavaScript program to count cubes between a and b

    // Function to count cubes between two numbers
    function countCubes(a, b)
    {
        let cnt = 0; // Initialize result

        // Traverse through all numbers
        for (let i = a; i <= b; i++)

            // Check if current number 'i' is perfect
            // cube
            for (let j = 1; j * j * j <= i; j++)
                if (j * j * j == i)
                    cnt++;

        return cnt;
    }

    // Driver code 
    let a = 7, b = 30;
    document.write("Count of Cubes is " + countCubes(a, b));

// This code is contributed by Surbhi Tyagi

</script>
```

**Output:** 

```
Count of Cubes is 2
```

时间复杂度:O((b–a)<sup>4/3</sup>)

辅助空间:0(1)

**方法 2(高效)**:我们可以简单的取‘a’的立方根和‘b’的立方根，向上取‘a’的圆立方根和向下取‘b’的立方根，利用:
统计它们之间的完美立方体

```
(floor(cbrt(b)) - ceil(cbrt(a)) + 1)

We take floor of cbrt(b) because we need to consider 
numbers before b.

We take ceil of cbrt(a) because we need to consider 
numbers after a.

For example, let b = 28, a = 7\.  floor(cbrt(b)) = 3, 
ceil(cbrt(a)) = 2\.  And number of cubes is 3 - 2 + 1
= 2\. The two numbers are 8 and 27.
```

以下是上述思路的实现:

## C++

```
// An Efficient Method to count cubes between a and b
#include <bits/stdc++.h>
using namespace std;

// Function to count cubes between two numbers
int countCubes(int a, int b)
{
    return (floor(cbrt(b)) - ceil(cbrt(a)) + 1);
}

// Driver code
int main()
{
    int a = 7, b = 28;
    cout << "Count of cubes is "
         << countCubes(a, b);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// An Efficient Method to count cubes between a and b
class GFG
{

// Function to count cubes between two numbers
static int countCubes(int a, int b)
{
    return (int) (Math.floor(Math.cbrt(b)) -
                Math.ceil(Math.cbrt(a)) + 1);
}

// Driver code
public static void main(String[] args)
{
    int a = 7, b = 28;
    System.out.print("Count of cubes is "
        + countCubes(a, b));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# An Efficient Method to count cubes between a and b
from math import *

# Function to count cubes between two numbers
def countCubes(a, b):

    return (floor(b **(1./3.)) - ceil(a **(1./3.)) + 1)

# Driver code
a = 7
b = 28
print("Count of cubes is",countCubes(a, b))

# This code is contributed by shubhamsingh10
```

## C#

```
// An Efficient Method to count cubes between a and b
// C# implementation of the above approach
using System;

class GFG
{

// Function to count cubes between two numbers
static int countCubes(int a, int b)
{
    return (int) (Math.Floor(Math.Cbrt(b)) -
                Math.Ceiling(Math.Cbrt(a)) + 1);
}

// Driver code
public static void Main(string[] args)
{
    int a = 7, b = 28;
    Console.WriteLine("Count of cubes is " + countCubes(a, b));
}
}

// This code is contributed by Yash_R
```

## java 描述语言

```
<script>

// An Efficient Method to count cubes between a and b

// Function to count cubes between two numbers
function countCubes(a, b){

    return (Math.floor(b **(1./3.)) - Math.ceil(a **(1./3.)) + 1)
}

// Driver code
let a = 7;
let b = 28;
document.write("Count of cubes is "+countCubes(a, b))

// This code is contributed
// by pulamolu mohan pavan cse
</script>
```

**Output:** 

```
Count of cubes is 2
```

**时间复杂度** : O(Log b)。

**辅助空间:** O(1)