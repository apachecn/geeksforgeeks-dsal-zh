# 如果某天后有一个人离开

，则完成任务所需的总天数

> 原文:[https://www . geeksforgeeks . org/总天数-完成任务所需的天数-如果某天后一个人离开/](https://www.geeksforgeeks.org/total-number-of-days-taken-to-complete-the-task-if-after-certain-days-one-person-leaves/)

假设某人 **A** 花 **a** 天做某件工作，而人 **B** 花 **b** 天做同样的工作。如果 **A** 和 **B** 一起开始工作，并且在工作完成前 **n** 天， **A** 离开工作。查找完成工作所需的总天数。

**示例:**

> **输入:** a = 10，b = 20，n = 5
> T3】输出: 10
> 
> **输入:** a = 5，b = 15，n = 3
> T3】输出: 6

**进场:**设 **D** 为完成工作的总天数。 **A** 和 **B** 一起工作**D–n**天。所以，

> (D–n)*(1/a+1/b)+(n)*(1/b)= 1
> D *(1/a+1/b)–(n/a)–(n/b)+(n/b)= 1
> D *(1/a+1/b)=(n+a)/a
> **D = b *(n+a)/(a+b)**

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the
// number of days required
int numberOfDays(int a, int b, int n)
{
    int Days = b * (n + a) / (a + b);

    return Days;
}

// Driver code
int main()
{
    int a = 10, b = 20, n = 5;

    cout << numberOfDays(a, b, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

// Function to return the
// number of days required
static int numberOfDays(int a, int b, int n)
{
    int Days = b * (n + a) / (a + b);

    return Days;
}

// Driver code
public static void main (String[] args)
{

    int a = 10, b = 20, n = 5;
    System.out.println (numberOfDays(a, b, n));

}
}

// This code is contributed by jit_t
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the
# number of days required
def numberOfDays(a, b, n):

    Days = b * (n + a) // (a + b)

    return Days

# Driver code
if __name__ == "__main__" :

    a = 10
    b = 20
    n = 5

    print(numberOfDays(a, b, n))

# This code is contributed by rrrtnx
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the
    // number of days required
    static int numberOfDays(int a, int b, int n)
    {
        int Days = b * (n + a) / (a + b);

        return Days;
    }

    // Driver code
    public static void Main ()
    {

        int a = 10, b = 20, n = 5;
        Console.WriteLine(numberOfDays(a, b, n));

    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// javascript implementation of the approach

    // Function to return the
    // number of days required
    function numberOfDays(a , b , n)
    {
        var Days = b * (n + a) / (a + b);
        return Days;
    }

    // Driver code
    var a = 10, b = 20, n = 5;
    document.write(numberOfDays(a, b, n));

// This code is contributed by Rajput-Ji
</script>
```

**Output:** 

```
10
```

**时间复杂度:** O(1)

**辅助空间:** O(1)