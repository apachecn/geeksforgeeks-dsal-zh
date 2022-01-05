# 计算绘制 N×3 网格的独特方法的数量

> 原文:[https://www . geesforgeks . org/count-number-of-unique-way-paint-a-n-x-3-grid/](https://www.geeksforgeeks.org/count-number-of-unique-ways-to-paint-a-n-x-3-grid/)

给定一个整数 **N** ，任务是使用颜色**红色**、**黄色**或**绿色**绘制一个大小为**N×3**的网格，同时使没有一对相邻单元格具有相同的颜色。打印可能的不同方式的数量

**示例:**

> **输入:** N = 1
> **输出:** 12
> **解释:**
> 存在以下 12 种可能的绘制网格的方式:
> 
> 1.  红色，黄色，红色
> 2.  黄色，红色，黄色
> 3.  绿色，红色，黄色
> 4.  红色、黄色、绿色
> 5.  黄色，红色，绿色
> 6.  绿色，红色，绿色
> 7.  红色，绿色，红色
> 8.  黄色、绿色、红色
> 9.  绿色，黄色，红色
> 10.  红色、绿色、黄色
> 11.  黄色，绿色，黄色
> 12.  绿色，黄色，绿色
> 
> **输入:**N = 2
> T3】输出: 102

**方法:**按照以下步骤解决问题:

*   给行着色的方法可以分为以下两类:
    *   最左边和最右边的单元格颜色相同。
    *   最左边和最右边的单元格颜色不同。
*   考虑到第一种情况:
    *   有六种可能的方法来绘制行，使最左边和最右边的颜色相同。
    *   对于占据最左边和最右边单元格的每种颜色，都有两种不同的颜色可以用来给中间的行着色。
*   考虑第二种情况:
    *   存在六种可能的方法来绘制最左边和最右边不同的颜色。
    *   左单元格三个选项，中间两个选项，用剩下的唯一颜色填充最右边的单元格。因此，可能性总数为 **3*2*1 = 6** 。
*   现在，对于后续的单元格，请看下面的示例:
    *   如果前一行被绘制为**红绿红**，那么当前行有以下五种有效的着色方式:
        *   **{青红绿}**
        *   **{青红黄}**
        *   **{绿黄绿}**
        *   **{黄色红色绿色}**
        *   **{黄红黄}**
    *   从上面的观察，很明显，三种可能性都有相同颜色的端点，两种可能性都有不同颜色的端点。
    *   如果前一行被着色为**红绿黄**，则当前行存在以下四种着色可能性:
        *   **{青红绿}**
        *   **{绿黄红}**
        *   **{绿黄绿}**
        *   **{黄色红色绿色}**
    *   从上面的观察，很明显，可能性有相同颜色的端点，两种可能性有不同颜色的端点。
*   因此，基于以上观察，可以为绘制 **N** 行的方式数定义以下递归关系:

> 对具有相同颜色 S<sub>N+1</sub>= 3 * S<sub>N</sub>+2D<sub>N</sub>末端的当前行进行着色的方式计数
> 
> 对具有不同颜色末端的当前行进行着色的方式计数 D<sub>N+1</sub>= 2 * S<sub>N</sub>+2D<sub>N</sub>
> 
> 绘制所有 N 行的方法总数等于 S <sub>N</sub> 和 D <sub>N</sub> 之和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the number
// of ways to paint  N * 3 grid
// based on given conditions
void waysToPaint(int n)
{

    // Count of ways to pain a
    // row with same colored ends
    int same = 6;

    // Count of ways to pain a row
    // with different colored ends
    int diff = 6;

    // Traverse up to (N - 1)th row
    for (int i = 0; i < n - 1; i++) {

        // Calculate the count of ways
        // to paint the current row

        // For same colored ends
        long sameTmp = 3 * same + 2 * diff;

        // For different colored ends
        long diffTmp = 2 * same + 2 * diff;

        same = sameTmp;
        diff = diffTmp;
    }

    // Print the total number of ways
    cout << (same + diff);
}

// Driver Code
int main()
{
    int N = 2;
    waysToPaint(N);
}

// This code is contributed by ukasp.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG {

    // Function to count the number
    // of ways to paint  N * 3 grid
    // based on given conditions
    static void waysToPaint(int n)
    {

        // Count of ways to pain a
        // row with same colored ends
        long same = 6;

        // Count of ways to pain a row
        // with different colored ends
        long diff = 6;

        // Traverse up to (N - 1)th row
        for (int i = 0; i < n - 1; i++) {

            // Calculate the count of ways
            // to paint the current row

            // For same colored ends
            long sameTmp = 3 * same + 2 * diff;

            // For different colored ends
            long diffTmp = 2 * same + 2 * diff;

            same = sameTmp;
            diff = diffTmp;
        }

        // Print the total number of ways
        System.out.println(same + diff);
    }

    // Driver code
    public static void main(String[] args)
    {

        int N = 2;

        // Function call
        waysToPaint(N);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the number
# of ways to paint  N * 3 grid
# based on given conditions

def waysToPaint(n):

    # Count of ways to pain a
    # row with same colored ends
    same = 6

    # Count of ways to pain a row
    # with different colored ends
    diff = 6

    # Traverse up to (N - 1)th row
    for _ in range(n - 1):

        # Calculate the count of ways
        # to paint the current row

        # For same colored ends
        sameTmp = 3 * same + 2 * diff

        # For different colored ends
        diffTmp = 2 * same + 2 * diff

        same = sameTmp
        diff = diffTmp

    # Print the total number of ways
    print(same + diff)

# Driver Code

N = 2
waysToPaint(N)
```

## C#

```
// C# program for the above approach
using System;

class GFG {

    // Function to count the number
    // of ways to paint N * 3 grid
    // based on given conditions
    static void waysToPaint(int n)
    {

        // Count of ways to pain a
        // row with same colored ends
        long same = 6;

        // Count of ways to pain a row
        // with different colored ends
        long diff = 6;

        // Traverse up to (N - 1)th row
        for (int i = 0; i < n - 1; i++) {

            // Calculate the count of ways
            // to paint the current row

            // For same colored ends
            long sameTmp = 3 * same + 2 * diff;

            // For different colored ends
            long diffTmp = 2 * same + 2 * diff;

            same = sameTmp;
            diff = diffTmp;
        }

        // Print the total number of ways
        Console.WriteLine(same + diff);
    }

    // Driver code
    static public void Main()
    {
        int N = 2;

        waysToPaint(N);
    }
}

// This code is contributed by offbeat
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count the number
// of ways to paint  N * 3 grid
// based on given conditions
function waysToPaint(n)
{

    // Count of ways to pain a
    // row with same colored ends
    var same = 6;

    // Count of ways to pain a row
    // with different colored ends
    var diff = 6;

    // Traverse up to (N - 1)th row
    for(var i = 0; i < n - 1; i++)
    {

        // Calculate the count of ways
        // to paint the current row

        // For same colored ends
        var sameTmp = 3 * same + 2 * diff;

        // For different colored ends
        var diffTmp = 2 * same + 2 * diff;

          same = sameTmp;
          diff = diffTmp;
    }

    // Print the total number of ways
    document.write(same + diff);
}

// Driver code
var N = 2;

// Function call
waysToPaint(N);

// This code is contributed by Khushboogoyal499

</script>
```

**Output:** 

```
12
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)