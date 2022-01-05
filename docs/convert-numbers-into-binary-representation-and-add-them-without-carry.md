# 将数字转换成二进制表示，不进位相加

> 原文:[https://www . geeksforgeeks . org/convert-numbers-to-binary-presentation-and-add-它们-不带进位/](https://www.geeksforgeeks.org/convert-numbers-into-binary-representation-and-add-them-without-carry/)

给定两个数字 **N** 和 **M** 。将两个数字转换为二进制形式的任务是将两个二进制转换后的数字的相应位相加，但要满足一个给定的条件，即此加法中没有任何进位系统。

```
Input: N = 37, M = 12
Output: 41

Input: N = 456, M = 854
Output: 670
```

**进场:**

*   如果我们不考虑进位，那么两位的二进制相加将是:

```
    1 + 0 = 1
    0 + 1 = 1
    0 + 0 = 0
    1 + 1 = 0 (No carry)
```

*   如果你观察清楚，你会注意到这只是两个数字的按位异或。

以下是上述方法的实施

## C++

```
// C++ program to add two binary
// number without carry
#include<bits/stdc++.h>
using namespace std;

// Function returns sum of both
// the binary number without
// carry
int NoCarrySum(int N, int M)
{
    // XOR of N and M
    return N ^ M;
}

// Driver code
int main()
{
    int N = 37;
    int M = 12;

    cout << NoCarrySum(N, M);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to add two binary
// number without carry
import java.util.*;

class GFG{

// Function returns sum of both
// the binary number without
// carry
static int NoCarrySum(int N, int M)
{
    // XOR of N and M
    return N ^ M;
}

// Driver code
public static void main(String[] args)
{
    int N = 37;
    int M = 12;
    System.out.print(NoCarrySum(N, M));
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 program to add two binary
# number without carry

# Function returns sum of both
# the binary number without
# carry
def NoCarrySum(N, M):

    # XOR of N and M
    return N ^ M

# Driver code
N = 37
M = 12
print(NoCarrySum(N, M))

# This code is contributed by sayesha
```

## C#

```
// C# program to add two binary
// number without carry
using System;

class GFG{

// Function returns sum of both
// the binary number without
// carry
static int NoCarrySum(int N, int M)
{

    // XOR of N and M
    return N ^ M;
}

// Driver code
static public void Main(String[] args)
{
    int N = 37;
    int M = 12;
    Console.Write(NoCarrySum(N, M));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to add two binary
// number without carry

// Function returns sum of both
// the binary number without
// carry
function NoCarrySum(N, M)
{
    // XOR of N and M
    return N ^ M;
}

// Driver code
    let N = 37;
    let M = 12;

    document.write(NoCarrySum(N, M));

</script>
```

**Output:** 

```
41
```