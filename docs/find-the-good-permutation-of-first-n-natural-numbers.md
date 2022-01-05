# 找到前 N 个自然数的好排列

> 原文:[https://www . geesforgeks . org/find-the-good-排列第一个 n 个自然数/](https://www.geeksforgeeks.org/find-the-good-permutation-of-first-n-natural-numbers/)

给定一个整数 **N** ，任务是打印第一个 **N** 自然数的良好排列。让我们把排列的第 **i <sup>第</sup>T7】元素表示为 **p <sub>i</sub>** 。
一个好的排列是这样的排列:对于所有的 **1 ≤ i ≤ N** 下列等式成立，** 

*   **p <sub>pi</sub> = i**
*   **p <sub>i</sub> ！= i**

基本上以上表达式的意思是，没有一个值等于它的位置。
如果不存在这样好的排列，那么打印 **-1** 。
**示例:**

> **输入:** N = 1
> **输出:** -1
> 不存在好的排列。
> **输入:** N = 2
> **输出:**2 1
> 2 的位置为 1，1 的位置为 2。

**方法:**考虑排列 **p** 使得 **p <sub>i</sub> = i** 。其实 **p** 是从 **1** 到 **N** 和 **p <sub>pi</sub> = i** 的一个数列。
现在唯一的诀窍就是改变排列来满足第二个等式，即 **p <sub>i</sub> ！= i** 。让我们每两个连续的元素交换一次。更正式地说，对于每一个 **k** : **2k ≤ n** 让我们互换**p<sub>2k–1</sub>T30】和**p<sub>2k</sub>T34】。很容易看出，得到的排列对于每一个 **n** 都满足两个方程，唯一的例外是:n 为奇数时，没有答案，我们应该打印 **-1** 。
以下是上述方法的实施:**** 

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the good permutation
// of first N natural numbers
int printPermutation(int n)
{
    // If n is odd
    if (n % 2 != 0)
        cout << -1;

    // Otherwise
    else
        for (int i = 1; i <= n / 2; i++)
            cout << 2 * i << " " << 2 * i - 1 << " ";
}

// Driver code
int main()
{
    int n = 4;
    printPermutation(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG
{

// Function to print the good permutation
// of first N natural numbers
static int printPermutation(int n)
{
    // If n is odd
    if (n % 2 != 0)
    {
        System.out.println("-1");
    }

    // Otherwise
    else
        for (int i = 1; i <= n / 2; i++)
        {
            System.out.print(2 * i + " " + ((2 * i) - 1) + " ");
        }

    return n;

}

// Driver code
public static void main(String []args)
{
    int n = 4;
    printPermutation(n);
}
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to print the good permutation
# of first N natural numbers
def printPermutation(n):

    # If n is odd
    if (n % 2 != 0):
        print(-1);

    # Otherwise
    else:
        for i in range(1, (n // 2) + 1):
            print((2 * i), (2 * i - 1), end = " ");

# Driver code
n = 4;
printPermutation(n);

# This code is contributed by mits
```

## C#

```
// C# implementation of the approach
using System;

class GFG {

// Function to print the good permutation
// of first N natural numbers
static int printPermutation(int n)
{
    // If n is odd
    if (n % 2 != 0)
    {
        Console.WriteLine("-1");
    }

    // Otherwise
    else
        for (int i = 1; i <= n / 2; i++)
        {
            Console.WriteLine(2 * i + " " + ((2 * i) - 1) + " ");
        }

    return n;

}

// Driver code
public static void Main(String []args)
{
    int n = 4;
    printPermutation(n);
}
}

// This code is contributed by Kirti_Mangal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?phP
// PHP implementation of the approach

// Function to print the good permutation
// of first N natural numbers
function printPermutation($n)
{
    // If n is odd
    if ($n % 2 != 0)
    {
        echo("-1");
    }

    // Otherwise
    else
        for ($i = 1; $i <= $n / 2; $i++)
        {
            echo(2 * $i . " " .
               ((2 * $i) - 1) . " ");
        }

    return $n;
}

// Driver code
$n = 4;
printPermutation($n);

// This code contributed
// by Code_Mech.
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to print the good permutation
// of first N natural numbers
function printPermutation(n)
{
    // If n is odd
    if (n % 2 != 0)
        document.write(-1);

    // Otherwise
    else
        for (let i = 1; i <= Math.floor(n / 2); i++)
            document.write((2 * i) + " " + ((2 * i) - 1) + " ");
}

// Driver code
    let n = 4;
    printPermutation(n);

//This code is contributed by Manoj
</script>
```

**Output:** 

```
2 1 4 3
```