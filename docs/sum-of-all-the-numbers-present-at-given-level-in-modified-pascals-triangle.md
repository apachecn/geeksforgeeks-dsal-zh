# 修正帕斯卡三角形中给定级别的所有数字的总和

> 原文:[https://www . geeksforgeeks . org/所有数字的总和-在给定级别出现-修正-帕斯卡-三角形/](https://www.geeksforgeeks.org/sum-of-all-the-numbers-present-at-given-level-in-modified-pascals-triangle/)

给定一个 N 级，任务是在一个交替的帕斯卡三角形中找到这个给定级上所有整数的和。
一个 5 级的**修正帕斯卡三角形**如下图所示。

```
     1
   -1 1
   1 -2 1
 -1 3 -3 1
1 -4 6 -4 1
```

**示例:**

```
Input: N = 1
Output: 1

Input: N = 2
Output: 0
```

**方法:**正如我们可以观察到的，对于偶数级和是 0，对于奇数级除了 1 之外和也是 0。所以最多有两种情况:

*   如果 L = 1，那么答案是 1。
*   否则答案永远是 0。

下面是上述方法的实现:

## C++

```
// C++ program to calculate sum of
// all the numbers present at given
// level in an Modified Pascal’s triangle

#include <bits/stdc++.h>
using namespace std;

// Function to calculate sum
void ans(int n)
{
    if (n == 1)
        cout << "1";
    else
        cout << "0";
}

// Driver Code
int main()
{
    int n = 2;
    ans(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate sum of
// all the numbers present at given
// level in an Modified Pascal's triangle
class GFG
{

// Function to calculate sum
static void ans(int n)
{
    if (n == 1)
        System.out.println("1");
    else
        System.out.println("0");
}

// Driver Code
public static void main(String[] args)
{
    int n = 2;
    ans(n);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to calculate sum of
# all the numbers present at given
# level in an Modified Pascal’s triangle

# Function to calculate sum
def ans(n) :

    if (n == 1) :
        print("1",end="");
    else :
        print("0",end="");

# Driver Code
if __name__ == "__main__" :

    n = 2;
    ans(n);

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to calculate sum of
// all the numbers present at given
// level in an Modified Pascal's triangle
using System;

class GFG
{

// Function to calculate sum
static void ans(int n)
{
    if (n == 1)
        Console.WriteLine("1");
    else
        Console.WriteLine("0");
}

// Driver Code
public static void Main(String[] args)
{
    int n = 2;
    ans(n);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to calculate sum of
// all the numbers present at given
// level in an Modified Pascal’s triangle

// Function to calculate sum
function ans(n)
{
    if (n == 1)
        document.write("1");
    else
        document.write("0");
}

// Driver Code
var n = 2;

ans(n);

// This code is contributed by rutvik_56

</script>
```

**Output:** 

```
0
```

**时间复杂度:** O(1)