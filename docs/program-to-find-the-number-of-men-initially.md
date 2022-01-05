# 程序初步查找男性人数

> 原文:[https://www . geesforgeks . org/program-to-find-the-number-of-men-initial/](https://www.geeksforgeeks.org/program-to-find-the-number-of-men-initially/)

一定数量的人可以在 **D** 天内完成一定的工作。如果有更多的 T2 人从事这项工作，那么这项工作可以在更短的时间内完成。任务是找出最初有多少人。
**举例:**

> **输入:** D = 5，m = 4，d = 4
> **输出:** 1
> **输入:** D = 180，m = 30，d = 20
> **输出:** 240

**方法:**假设初始人数为 **M** ，天数为 **D**
在 **D** 天内完成的工作数量为 **M** 人，则**M * D**T13】即**已完成的工作= M * D**……(1)
如果有 **M + m** 人，则**内完成的工作数量相同
即**完成的功=(M+M)*(D–D)**……(2)
等式 1 和等式 2，** 

> M * D =(M+M)*(D–D)
> M * D = M *(D–D)+M *(D–D)
> M * D–M *(D–D)= M *(D–D)
> M *(D–(D–D))= M *(D–D)
> **M = M *(D–D)/D**

以下是上述方法的实现:

## C++

```
// C++ implementation of above approach.
#include <bits/stdc++.h>
using namespace std;

// Function to return the
// number of men initially
int numberOfMen(int D, int m, int d)
{

    int Men = (m * (D - d)) / d;

    return Men;
}

// Driver code
int main()
{
    int D = 5, m = 4, d = 4;

    cout << numberOfMen(D, m, d);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the
// number of men initially
static int numberOfMen(int D, int m, int d)
{

    int Men = (m * (D - d)) / d;

    return Men;
}

// Driver code
public static void main(String args[])
{
    int D = 5, m = 4, d = 4;

    System.out.println(numberOfMen(D, m, d));

}
}
// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python implementation of above approach.

# Function to return the
# number of men initially
def numberOfMen(D, m, d):
    Men = (m * (D - d)) / d;

    return int(Men);

# Driver code
D = 5; m = 4; d = 4;

print(numberOfMen(D, m, d));

# This code contributed by Rajput-Ji
```

## C#

```
//  C# implementation of the approach
using System;

class GFG
{

// Function to return the
// number of men initially
static int numberOfMen(int D, int m, int d)
{

    int Men = (m * (D - d)) / d;

    return Men;
}

// Driver code
public static void Main()
{
    int D = 5, m = 4, d = 4;

    Console.WriteLine(numberOfMen(D, m, d));

}
}

// This code is contributed by anuj_67..
```

## java 描述语言

```
<script>

// Javascript implementation of above approach.

// Function to return the
// number of men initially
function numberOfMen(D, m, d)
{

    var Men = (m * (D - d)) / d;

    return Men;
}

// Driver code
var D = 5, m = 4, d = 4;
document.write(numberOfMen(D, m, d));

</script>
```

**Output:** 

```
1
```