# 找出表格中包含 X 的单元格数

> 原文:[https://www . geeksforgeeks . org/find-表中单元格的数量-contains-x/](https://www.geeksforgeeks.org/find-the-number-of-cells-in-the-table-contains-x/)

给定两个整数 **N** 和 **X** 。 **N** 代表表格的行数和列数。表中第**行第**列第**列第**列的元素为 **i*j** 。任务是在包含 **X** 的表格中找到单元格的数量。

**示例:**

> **输入:** N = 6，X = 12
> **输出:** 4
> 单元格{2，6}、{3，4}、{4，3}、{6，2}包含数字 12
> 
> **输入:** N = 5，X = 11
> T3】输出: 0

**进场:**
很容易看出数字 **x** 连续只能出现一次。如果 **x** 包含在**和**行中，那么列号将是 **x/i** 。 **x** 包含在带有的**行中，如果 **x** 可被 **i** 整除。让我们检查一下 **x** 除 **i** 和 **x/i** **< = n** 。如果满足这些条件，请更新答案。**

下面是上述方法的实现:

## C++

```
// CPP program to find number of
// cells in the table contains X
#include <bits/stdc++.h>
using namespace std;

// Function to find number of
// cells in the table contains X
int Cells(int n, int x)
{
    int ans = 0;
    for (int i = 1; i <= n; i++)
        if (x % i == 0 && x / i <= n)
            ans++;

    return ans;
}

// Driver code
int main()
{
    int n = 6, x = 12;

    // Function call
    cout << Cells(n, x);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number of
// cells in the table contains X
class GFG
{

    // Function to find number of
    // cells in the table contains X
    public static int Cells(int n, int x)
    {
        int ans = 0;
        for (int i = 1; i <= n; i++)
            if (x % i == 0 && x / i <= n)
                ans++;

        return ans;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 6, x = 12;

        // Function call
        System.out.println(Cells(n, x));
    }
}

// This code is contributed by sanjeev2552
```

## 蟒蛇 3

```
# Python3 program to find number of
# cells in the table contains X

# Function to find number of
# cells in the table contains X
def Cells(n, x):

    ans = 0;
    for i in range(1, n + 1):
        if (x % i == 0 and x / i <= n):
            ans += 1;

    return ans;

# Driver code
if __name__ == '__main__':

    n = 6; x = 12;

    # Function call
    print(Cells(n, x));

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program to find number of
// cells in the table contains X
using System;

class GFG
{
    // Function to find number of
    // cells in the table contains X
    static int Cells(int n, int x)
    {
        int ans = 0;
        for (int i = 1; i <= n; i++)
            if (x % i == 0 && x / i <= n)
                ans++;

        return ans;
    }

    // Driver code
    public static void Main()
    {
        int n = 6, x = 12;

        // Function call
        Console.WriteLine(Cells(n,x));
    }
}

// This code is contributed by nidhiva
```

## java 描述语言

```
<script>

// JavaScript program to find number of
// cells in the table contains X

// Function to find number of
// cells in the table contains X
function Cells(n, x)
{
    let ans = 0;
    for (let i = 1; i <= n; i++)
        if (x % i == 0 && parseInt(x / i) <= n)
            ans++;

    return ans;
}

// Driver code
    let n = 6, x = 12;

    // Function call
    document.write(Cells(n, x));

</script>
```

**Output**

```
4
```

**接近**:

忽略负方格的情况。如果 n 是 0，那么正方形中不会有任何数字，如果 x 是 0，那么它不会出现在正方形中，所以在这两种情况下都返回 0。如果 x 大于 n^2，它就不在正方形中，所以在这种情况下也返回 0。
接下来，循环遍历所有数字 **i** 从 1 到 **x** 的平方根，如果 **i** 是 **x** 和**x/I**T27】=**n**的因子，那么由于关联属性: **i*(x/i)** 和**在 n 平方图上至少还有两个额外的位置 **x**
最后，找出 **x** 的平方根是否为整数。如果是，它会在 n-square 表的对角线上再出现一次，n-square 表是所有方块的列表。
| 1 | 2 | 3 | 4 | 5 | 6 |**

| 2 |   4 |   6 |   8 | 10 | 12 |

| 3 |   6 |   9 | 12 | 15 | 18 |

| 4 |   8 | 12 | 16 | 20 | 24 |

| 5 | 10 | 15 | 20 | 25 | 30 |

| 6 | 12 | 18 | 24 | 30 | 36 |

下面是上述方法的实现:

## C++

```
// C++ program to find number of
// cells in the table contains X
#include <bits/stdc++.h>
using namespace std;

// Function to find number of
// cells in the table contains X
int Cells(int n, int x)
{
    if (n <= 0 || x <= 0 || x > n * n)
        return 0;

    int i = 0, count = 0;
    while (++i * i < x)
        if (x % i == 0 && x <= n * i)
            count += 2;

    return i * i == x ? count + 1 : count;
}

// Driver code
int main()
{
    int n = 6, x = 12;

    // Function call
    cout << (Cells(n, x));
    return 0;
}

// This code is contributed by subhammahato348
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number of
// cells in the table contains X
class GFG {

    // Function to find number of
    // cells in the table contains X
    public static int Cells(int n, int x)
    {
        if (n <= 0 || x <= 0 || x > n * n)
            return 0;
        int i = 0, count = 0;
        while (++i * i < x)
            if (x % i == 0 && x <= n * i)
                count += 2;
        return i * i == x ? count + 1 : count;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 6, x = 12;

        // Function call
        System.out.println(Cells(n, x));
    }
}

// This code is contributed by stephenbrasel
```

## 蟒蛇 3

```
# Python program to find number of
# cells in the table contains X

# Function to find number of
# cells in the table contains X
def Cells(n, x):
    if (n <= 0 or x <= 0 or x > n * n):
        return 0;
    i = 1
    count = 0

    while (i * i < x):
        if (x % i == 0 and x <= n * i):
            count += 2;
        i+=1

    if(i * i == x):
        return count + 1
    else:
        return count

# Driver Code
n = 6

x = 12

print(Cells(n, x))

# This code is contributed by rag2127.
```

## C#

```
// C# program to find number of
// cells in the table contains X
using System;

class GFG{

// Function to find number of
// cells in the table contains X
public static int Cells(int n, int x)
{
    if (n <= 0 || x <= 0 || x > n * n)
        return 0;

    int i = 0, count = 0;
    while (++i * i < x)
        if (x % i == 0 && x <= n * i)
            count += 2;

    return i * i == x ? count + 1 : count;
}

// Driver code
static public void Main ()
{
    int n = 6, x = 12;

    // Function call
    Console.WriteLine(Cells(n, x));
}
}

// This code is contributed by kirti
```

## java 描述语言

```
<script>

// JavaScript program to find number of
// cells in the table contains X

// Function to find number of
// cells in the table contains X
function Cells(n, x)
{
    if (n <= 0 || x <= 0 || x > n * n)
        return 0;

    var i = 0, count = 0;

    while (++i * i < x)
        if (x % i == 0 && x <= n * i)
            count += 2;

    return i * i == x ? count + 1 : count;
}

// Driver Code
var n = 6, x = 12;

// Function call
document.write(Cells(n, x));

// This code is contributed by Khushboogoyal499

</script>
```

**Output**

```
4
```