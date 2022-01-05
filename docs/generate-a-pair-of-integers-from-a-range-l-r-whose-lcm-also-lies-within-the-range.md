# 从 LCM 也在范围

内的范围【L，R】生成一对整数

> 原文:[https://www . geeksforgeeks . org/generate-a-对整数-from-range-l-r-其-LCM-也位于范围内/](https://www.geeksforgeeks.org/generate-a-pair-of-integers-from-a-range-l-r-whose-lcm-also-lies-within-the-range/)

给定两个整数 **L** 和 **R** ，任务是从范围**【L，R】**中找出一对整数，它们的 [LCM](https://www.geeksforgeeks.org/program-to-find-lcm-of-two-numbers/) 也在范围【L，R】内。如果无法获得这样的配对，则打印 **-1** 。如果存在多对，请打印其中任何一对。

**示例:**

> **输入:** L = 13，R = 69
> **输出:** X =13，Y = 26
> **说明:** LCM(x，y) = 26 满足条件 L ≤ x < y ≤ R 和 L < = LCM(x，y) < = R
> 
> **输入:**L =**T3】1，R = 665
> T5】输出:** X = 1，Y = 2

**天真方法:**最简单的方法是生成 **L** 和 **R** 之间的每一对，并计算它们的 [LCM](https://www.geeksforgeeks.org/lcm-gq/) 。打印一对 LCM 在范围 **L** 和 **R** 之间的。如果在给定范围内没有发现任何一对具有 LCM，则打印**-1”**。

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

**高效途径:**基于 **LCM(x，y)** 至少等于 **2*x** (是 **(x，2*x)** 的 LCM)的观察，使用**[贪婪手法](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决问题。以下是实施该方法的步骤:**

1.  **选择 x 的值为 1，计算 y 的值为 2*x**
2.  **检查 y 是否小于 R。**
3.  **如果 y 小于 R，则打印该对(x，y)**
4.  **否则打印“-1”**

**下面是上述方法的实现:**

## **C++**

```
// C++ implementation of the above approach
#include <iostream>
using namespace std;

void lcmpair(int l, int r)
{
    int x, y;
    x = l;
    y = 2 * l;

    // Checking if any pair is possible
    // or not in range(l, r)
    if (y > r) {

        // If not possible print(-1)
        cout << "-1\n";
    }
    else {

        // Print LCM pair
        cout << "X = " << x << " Y = "
             << y << "\n";
    }
}

// Driver code
int main()
{
    int l = 13, r = 69;

    // Function call
    lcmpair(l, r);
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java implementation of the above approach
import java.util.*;

class GFG{

static void lcmpair(int l, int r)
{
    int x, y;
    x = l;
    y = 2 * l;

    // Checking if any pair is possible
    // or not in range(l, r)
    if (y > r)
    {

        // If not possible print(-1)
        System.out.print("-1\n");
    }
    else
    {

        // Print LCM pair
        System.out.print("X = " + x +
                        " Y = " + y + "\n");
    }
}

// Driver code
public static void main(String[] args)
{
    int l = 13, r = 69;

    // Function call
    lcmpair(l, r);
}
}

// This code is contributed by 29AjayKumar
```

## **蟒蛇 3**

```
# Python3 implementation of the above approach
def lcmpair(l, r):

    x = l
    y = 2 * l

    # Checking if any pair is possible
    # or not in range(l, r)
    if(y > r):

        # If not possible print(-1)
        print(-1)
    else:

        # Print LCM pair
        print("X = {} Y = {}".format(x, y))

# Driver Code
l = 13
r = 69

# Function call
lcmpair(l, r)

# This code is contributed by Shivam Singh
```

## **C#**

```
// C# implementation of the above approach
using System;
class GFG{

static void lcmpair(int l, int r)
{
    int x, y;
    x = l;
    y = 2 * l;

    // Checking if any pair is possible
    // or not in range(l, r)
    if (y > r)
    {       
        // If not possible print(-1)
        Console.Write("-1\n");
    }
    else
    {       
        // Print LCM pair
        Console.Write("X = " + x +
                      " Y = " + y + "\n");
    }
}

// Driver code
public static void Main(String[] args)
{
    int l = 13, r = 69;

    // Function call
    lcmpair(l, r);
}
}

// This code is contributed by shikhasingrajput
```

## **java 描述语言**

```
<script>
// javascript implementation of the above approach

    function lcmpair(l , r) {
        var x, y;
        x = l;
        y = 2 * l;

        // Checking if any pair is possible
        // or not in range(l, r)
        if (y > r) {

            // If not possible print(-1)
            document.write("-1\n");
        } else {

            // Print LCM pair
            document.write("X = " + x + " Y = " + y + "\n");
        }
    }

    // Driver code
        var l = 13, r = 69;

        // Function call
        lcmpair(l, r);

// This code is contributed by aashish1995
</script>
```

****Output:** 

```
X = 13 Y = 26
```** 

*****时间复杂度:**O(1)*
T5**辅助空间:** O(1)**