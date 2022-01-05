# A 从 B 或 B 从 A 到使它们(1，1)连续减少的次数

> 原文:[https://www . geeksforgeeks . org/a-from-b-or-b-from-a-make-1-1/](https://www.geeksforgeeks.org/number-of-continuous-reductions-of-a-from-b-or-b-from-a-to-make-them-1-1/)连续减少的数量

给定两个整数 **A** 和 **B** ，任务是找到将这一对变为(1，1)所需的最小操作数。在每个操作中(A，B)可以改为(A–B，B)，其中 A > B.
**注:**如果没有可能的解达到(1，1)，打印-1。

**示例:**

> **输入:** A = 7，B = 8
> **输出:** 7
> **解释:**
> 操作 1: (A，B) = > (7，8) = > (7，1)
> 操作 2: (A，B) = > (7，1) = > (6，1)
> 操作 3: (A，B) = > (6，1) = > (5，1)
> 1) = > (3，1)
> 操作 6: (A，B) = > (3，1) = > (2，1)
> 操作 7: (A，B) = > (2，1) = > (1，1)
> 
> **输入:** A = 75，B = 17
> T3】输出: 10

**天真的做法:**思路是用[递归](https://www.geeksforgeeks.org/recursion/)将对更新为(A，A–B)，其中 A > B，将所需操作数增加 1。如果在任何步骤中，该对中的任何元素小于 1，则不可能达到(1，1)。

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// minimum number of operations
// required to reach (1, 1)
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum
// number of steps required
int minimumSteps(int a, int b, int c)
{

    // Condition to check if it
    // is not possible to reach
    if(a < 1 || b < 1)
        return -1;

    // Condition to check if the
    // pair is reached to 1, 1
    if(a == 1 && b == 1)
        return c;

    // Condition to change the
    // A as the maximum element
    if(a < b)
    {
        a = a + b;
        b = a - b;
        a = a - b;
    }

    return minimumSteps(a - b, b, c + 1);
}

// Driver Code
int main()
{
    int a = 75;
    int b = 17;

    cout << minimumSteps(a, b, 0) << endl;
}

// This code is contributed by AbhiThakur
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// minimum number of operations
// required to reach (1, 1)
class GFG{

// Function to find the minimum
// number of steps required
static int minimumSteps(int a, int b, int c)
{

    // Condition to check if it
    // is not possible to reach
    if(a < 1 || b < 1)
        return -1;

    // Condition to check if the
    // pair is reached to 1, 1
    if(a == 1 && b == 1)
        return c;

    // Condition to change the
    // A as the maximum element
    if(a < b)
    {
        a = a + b;
        b = a - b;
        a = a - b;
    }

    return minimumSteps(a - b, b, c + 1);
}

// Driver Code
public static void main(String []args)
{
    int a = 75;
    int b = 17;

    System.out.println(minimumSteps(a, b, 0));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation to find the
# minimum number of operations
# required to reach (1, 1)

# Function to find the minimum
# number of steps required
def minimumSteps(a, b, c):

    # Condition to check if it
    # is not possible to reach
    if a < 1 or b < 1:
        return -1

    # Condition to check if the
    # pair is reached to 1, 1
    if a == 1 and b == 1:
        return c

    # Condition to change the
    # A as the maximum element
    if a < b:
        a, b = b, a

    return minimumSteps(a-b, b, c + 1)

# Driver Code
if __name__ == "__main__":
    a = 75; b = 17

    print(minimumSteps(a, b, 0))
```

## C#

```
// C# implementation to find the
// minimum number of operations
// required to reach (1, 1)
using System;

class GFG{

// Function to find the minimum
// number of steps required
static int minimumSteps(int a, int b, int c)
{

    // Condition to check if it
    // is not possible to reach
    if(a < 1 || b < 1)
       return -1;

    // Condition to check if the
    // pair is reached to 1, 1
    if(a == 1 && b == 1)
       return c;

    // Condition to change the
    // A as the maximum element
    if(a < b)
    {
        a = a + b;
        b = a - b;
        a = a - b;
    }
    return minimumSteps(a - b, b, c + 1);
}

// Driver Code
public static void Main()
{
    int a = 75;
    int b = 17;

    Console.WriteLine(minimumSteps(a, b, 0));
}
}

// This code is contributed by AbhiThakur
```

## java 描述语言

```
<script>

// JavaScript implementation to find the
// minimum number of operations
// required to reach (1, 1)

// Function to find the minimum
// number of steps required
function minimumSteps(a, b, c)
{

    // Condition to check if it
    // is not possible to reach
    if(a < 1 || b < 1)
        return -1;

    // Condition to check if the
    // pair is reached to 1, 1
    if(a == 1 && b == 1)
        return c;

    // Condition to change the
    // A as the maximum element
    if(a < b)
    {
        a = a + b;
        b = a - b;
        a = a - b;
    }

    return minimumSteps(a - b, b, c + 1);
}

// Driver Code
    let a = 75;
    let b = 17;

    document.write(minimumSteps(a, b, 0) + "<br>");

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
10
```

高效**方法:**想法是使用[欧几里德算法](https://www.geeksforgeeks.org/euclidean-algorithms-basic-and-extended/)来解决这个问题。通过这种方法，我们可以在 **A/B** 步骤中从(A，B)到(A % B，B)**。但是如果 A 和 B 的最小值是 1，那么我们可以在**A–1**步中达到(1，1)。**

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// minimum number of operations
// required to reach (1, 1)
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum
int minimumSteps(int a, int b, int c)
{

    // Condition to check if it
    // is not possible to reach
    if(a < 1 || b < 1)
    {
        return -1;
    }

    // Condition to check if the
    // pair is reached to 1, 1
    if(min(a, b) == 1)
    {
        return c + max(a, b) - 1;
    }

    // Condition to change the
    // A as the maximum element
    if(a < b)
    {
        swap(a, b);
    }

    return minimumSteps(a % b, b, c + (a / b));
}

// Driver Code
int main()
{
    int a = 75, b = 17;
    cout << minimumSteps(a, b, 0) << endl;

    return 0;
}

// This code is contributed by rutvik_56
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// minimum number of operations
// required to reach (1, 1)
import java.util.*;
class GFG{

// Function to find the minimum
static int minimumSteps(int a, int b, int c)
{

    // Condition to check if it
    // is not possible to reach
    if(a < 1 || b < 1)
    {
        return -1;
    }

    // Condition to check if the
    // pair is reached to 1, 1
    if(Math.min(a, b) == 1)
    {
        return c + Math.max(a, b) - 1;
    }

    // Condition to change the
    // A as the maximum element
    if(a < b)
    {
        a = a + b;
        b = a - b;
        a = a - b;
    }

    return minimumSteps(a % b, b, c + (a / b));
}

// Driver Code
public static void main(String[] args)
{
    int a = 75, b = 17;
    System.out.print(
           minimumSteps(a, b, 0) + "\n");
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 implementation to find the
# minimum number of operations
# required to reach (1, 1)

# Function to find the minimum
# number of steps required
def minimumSteps(a, b, c):

    # Condition to check if it
    # is not possible to reach
    if a < 1 or b < 1:
        return -1

    # Condition to check if the
    # pair is reached to 1, 1
    if min(a, b) == 1:
        return c + max(a, b) - 1

    # Condition to change the
    # A as the maximum element
    if a < b:
        a, b = b, a

    return minimumSteps(a % b, b, c + a//b)

# Driver Code
if __name__ == "__main__":
    a = 75; b = 17

    print(minimumSteps(a, b, 0))
```

## C#

```
// C# implementation to find the
// minimum number of operations
// required to reach (1, 1)
using System;
class GFG{

// Function to find the minimum
static int minimumSteps(int a, int b, int c)
{

    // Condition to check if it
    // is not possible to reach
    if(a < 1 || b < 1)
    {
        return -1;
    }

    // Condition to check if the
    // pair is reached to 1, 1
    if(Math.Min(a, b) == 1)
    {
        return c + Math.Max(a, b) - 1;
    }

    // Condition to change the
    // A as the maximum element
    if(a < b)
    {
        a = a + b;
        b = a - b;
        a = a - b;
    }

    return minimumSteps(a % b, b, c + (a / b));
}

// Driver Code
public static void Main()
{
    int a = 75, b = 17;
    Console.Write(minimumSteps(a, b, 0) + "\n");
}
}

// This code is contributed by Nidhi_biet
```

## java 描述语言

```
<script>

// JavaScript implementation to find the
// minimum number of operations
// required to reach (1, 1)

// Function to find the minimum
function minimumSteps(a, b, c)
{

    // Condition to check if it
    // is not possible to reach
    if(a < 1 || b < 1)
    {
        return -1;
    }

    // Condition to check if the
    // pair is reached to 1, 1
    if(Math.min(a, b) == 1)
    {
        return c + Math.max(a, b) - 1;
    }

    // Condition to change the
    // A as the maximum element
    if(a < b)
    {
        a = a + b;
        b = a - b;
        a = a - b;
    }

    return minimumSteps(a % b, b, c + parseInt(a / b));
}

// Driver Code
var a = 75, b = 17;
document.write(minimumSteps(a, b, 0) + "<br>");

</script>
```

**Output:** 

```
10
```