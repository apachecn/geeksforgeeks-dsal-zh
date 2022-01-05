# 检查给定操作是否可以同时使 x 和 y 为零

> 原文:[https://www . geeksforgeeks . org/check-if-it-make-x-y-zero-at-time-with-给定操作/](https://www.geeksforgeeks.org/check-if-it-is-possible-to-make-x-and-y-zero-at-same-time-with-given-operation/)

给定两个数字 **X** 和 **Y** 。任务是通过执行以下操作任意次数，检查 **X** 和 **Y** 是否可以同时归零:

*   每次操作时，选择任意自然数(**表示 z** )并减少 **X 和 Y** 为下列之一:
    1.  X = X–z，Y = Y–2 * z
    2.  X = X–2 * z，Y = Y–z

**示例:**

> **输入:** X = 6，Y = 9
> **输出:** YES
> **解释:**
> 我们可以通过以下方式进行运算:
> 如果 z = 1，那么
> X = X–2 * z = 6–2 *(1)
> Y = Y–z = 9–1
> =>X = 4&Y = 8
> 现在再次如果 z = 4， 然后
> X = X–z = 4–4
> Y = Y–2 * z = 8–2 *(4)
> =>X = 0&Y = 0
> 因此，X & Y 分别假设 z 为 1 和 4，分两步变为零。
> 
> **输入:** X = 1，Y = 1
> **输出:**否
> **解释:**
> 我们没有 z 的任何可能值，所以 X & Y 可以同时变成零。

**方法:**
以下是对给定问题陈述的观察:

1.  由于 **X** 和 **Y** 更新为(**X–z**和**Y–2 * z**)或(**X–2 * z**和**Y–z**，因此在 **n** 之后，操作次数( **X + Y** )更新为(**X+Y–3 * n * z**)。因此，如果 **(X+Y)%3 等于 0** ，X 和 Y 可以同时减少到零。
2.  在每一步中 **X** 或 **Y** 中的一个被 **2*z** 减少。要使 **X 和 Y** 同时归零，必须满足以下条件:**最大值(X，Y)≤2 *最小值(X，Y)** 。
    例如:

> 设 X = 6 和 Y = 15
> 由于(X+Y)%3 = (21%3) = 0
> 作为我们的第一个条件得到满足，
> 但是通过取 z = 6
> X = X–z = 6–6 = 0
> Y = Y–2 * z = 15–12 = 3
> 由于 Y 不小于或等于 2*X，因此 X 和 Y 不能同时降为零。

如果以上两个条件满足 **X 和 Y** 的值，那么 **X** 和 **Y** 可以同时降为 **0** 。

下面是上述方法的实现:

## C++

```
// C++ program of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if it is possible to
// make x and y can become 0 at same time
void canBeReduced(int x, int y)
{
    int maxi = max(x, y);
    int mini = min(x, y);

    // Check the given conditions
    if (((x + y) % 3) == 0 && maxi <= 2*mini)
        cout << "YES" << endl;
    else
        cout << "NO" << endl;
}

// Driver Code
int main()
{
    int x = 6, y = 9;

    // Function Call
    canBeReduced(x, y);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the above approach
import java.util.*;

class GFG{

// Function to check if it is possible to
// make x and y can become 0 at same time
static void canBeReduced(int x, int y)
{
    int maxi = Math.max(x, y);
    int mini = Math.min(x, y);

    // Check the given conditions
    if (((x + y) % 3) == 0 && maxi <= 2*mini)
        System.out.print("YES" +"\n");
    else
        System.out.print("NO" +"\n");
}

// Driver Code
public static void main(String[] args)
{
    int x = 6, y = 9;

    // Function Call
    canBeReduced(x, y);
}
}

// This code is contributed by Rajput-Ji
```

## C#

```
// C# program of the above approach
using System;

class GFG 
{
    // Function to check if it is possible to
    // make x and y can become 0 at same time
    static void canBeReduced(int x, int y)
    {
        int maxi = Math.Max(x, y);
        int mini = Math.Min(x, y);

        // Check the given conditions
        if (((x + y) % 3) == 0 && maxi <= 2*mini)
            Console.WriteLine("YES");
        else
            Console.WriteLine("NO");
    }

    // Driver Code
    static void Main()
    {
        int x = 6, y = 9;

        // Function Call
        canBeReduced(x, y);
    }
}

// This code is contributed by shubhamsingh10
```

## 蟒蛇 3

```
# Python 3 program of the above approach

# Function to check if it is possible to
# make x and y can become 0 at same time
def canBeReduced(x,y):
    maxi = max(x, y)
    mini = min(x, y)

    # Check the given conditions
    if (((x + y) % 3) == 0 and maxi <= 2*mini):
        print("YES")
    else:
        print("NO")

# Driver Code
if __name__ == '__main__':
    x = 6
    y = 9

    # Function Call
    canBeReduced(x, y)

# This code is contributed by Surendra_Gangwar
```

## java 描述语言

```
<script>

// javascript program of the above approach

// Function to check if it is possible to
// make x and y can become 0 at same time
function canBeReduced(x , y)
{
    var maxi = Math.max(x, y);
    var mini = Math.min(x, y);

    // Check the given conditions
    if (((x + y) % 3) == 0 && maxi <= 2*mini)
        document.write("YES" +"\n");
    else
        document.write("NO" +"\n");
}

// Driver Code

var x = 6, y = 9;

// Function Call
canBeReduced(x, y);

// This code contributed by shikhasingrajput

</script>
```

**Output:** 

```
YES
```

**时间复杂度:** O(1)