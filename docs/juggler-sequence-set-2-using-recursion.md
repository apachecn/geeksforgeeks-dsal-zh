# 杂耍者序列|集合 2(使用递归)

> 原文:[https://www . geesforgeks . org/杂耍者-序列-集合-2-使用-递归/](https://www.geeksforgeeks.org/juggler-sequence-set-2-using-recursion/)

杂耍序列是一系列整数，其中第一项以正整数 *a* 开始，其余项由前一项使用以下递归关系生成:

> ![a_{k+1}=\begin{Bmatrix} \lfloor a_{k}^{1/2} \rfloor & for \quad even \quad a_k\\ \lfloor a_{k}^{3/2} \rfloor & for \quad odd \quad a_k \end{Bmatrix}             ](img/3270169387630ac42a3e042133bb720a.png "Rendered by QuickLaTeX.com")
> 从数字 3 开始的杂耍者序列:
> 5、11、36、6、2、1
> 从数字 9 开始的杂耍者序列:
> 9、27、140、11、36、6、2、1

给定一个数字 **N** ，我们必须打印这个数字的杂耍序列作为序列的第一项。

**示例**:

> **输入:** N = 9
> **输出:** 9，27，140，11，36，6，2，1
> 我们从 9 开始，用上面的公式得到下一个项。
> 
> **输入:**N = 6
> T3】输出: 6，2，1

**迭代方法:**我们已经在这个问题的 [**集 1**](https://www.geeksforgeeks.org/juggler-sequence/) 中看到了迭代方法。

**递归方法:**在这种方法中，我们将从 n 开始递归遍历

*   输出 **N** 的值
*   如果 N 已经达到 1，结束递归
*   否则，遵循基于奇数或偶数的公式，并对新导出的数字调用递归函数。

以下是该方法的实施情况:

## C++

```
// C++ code for the above approach
#include <bits/stdc++.h>
using namespace std;

// Recursive function to print
// the juggler sequence
void jum_sequence(int N)
{

    cout << N << " ";

    if (N <= 1)
        return;
    else if (N % 2 == 0)
    {
        N = floor(sqrt(N));
        jum_sequence(N);
    }
    else
    {
        N = floor(N * sqrt(N));
        jum_sequence(N);
    }
}

// Driver code
int main()
{

    // Juggler sequence starting with 10
    jum_sequence(10);
    return 0;
}

// This code is contributed by Potta Lokesh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
class GFG
{

    // Recursive function to print
    // the juggler sequence
    public static void jum_sequence(int N) {

        System.out.print(N + " ");

        if (N <= 1)
            return;
        else if (N % 2 == 0) {
            N = (int) (Math.floor(Math.sqrt(N)));
            jum_sequence(N);
        } else {
            N = (int) Math.floor(N * Math.sqrt(N));
            jum_sequence(N);
        }
    }

    // Driver code
    public static void main(String args[]) {

        // Juggler sequence starting with 10
        jum_sequence(10);
    }
}

// This code is contributed by Saurabh Jaiswal
```

## 蟒蛇 3

```
# Python code to implement the above approach

# Recursive function to print
# the juggler sequence
def jum_sequence(N):

    print(N, end =" ")

    if (N == 1):
        return
    elif N & 1 == 0:
        N = int(pow(N, 0.5))
        jum_sequence(N)
    else:
        N = int(pow(N, 1.5))
        jum_sequence(N)

# Juggler sequence starting with 10
jum_sequence(10)
```

## C#

```
// C# code for the above approach
using System;

class GFG{

// Recursive function to print
// the juggler sequence
public static void jum_sequence(int N)
{
    Console.Write(N + " ");

    if (N <= 1)
        return;
    else if (N % 2 == 0)
    {
        N = (int)(Math.Floor(Math.Sqrt(N)));
        jum_sequence(N);
    }
    else
    {
        N = (int)Math.Floor(N * Math.Sqrt(N));
        jum_sequence(N);
    }
}

// Driver code
public static void Main()
{

    // Juggler sequence starting with 10
    jum_sequence(10);
}
}

// This code is contributed by Saurabh Jaiswal
```

## java 描述语言

```
<script>
// Javascript code for the above approach

// Recursive function to print
// the juggler sequence
function jum_sequence(N){

    document.write(N +" ");

    if (N <= 1)
        return;
    else if (N % 2 == 0)
    {
        N = Math.floor(Math.sqrt(N));
        jum_sequence(N);
    }
    else
    {
        N = Math.floor(N * Math.sqrt(N));
        jum_sequence(N);
    }
}

// Driver code
// Juggler sequence starting with 10

jum_sequence(10);

// This code is contributed by gfgking
</script>
```

**Output:** 

```
10 3 5 11 36 6 2 1
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)