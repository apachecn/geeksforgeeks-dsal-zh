# 给定 GCD 的递增顺序

> 原文:[https://www . geeksforgeeks . org/递增序列带给定-gcd/](https://www.geeksforgeeks.org/increasing-sequence-with-given-gcd/)

给定两个整数 **n** 和 **g** ，任务是生成 **n** 整数的**递增序列**，使得:

1.  序列中所有元素的 [gcd](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 为 **g** 。
2.  并且，所有元素的总和是所有可能序列中的最小值。

**示例:**

> **输入:** n = 6，g = 5
> T3】输出: 5 10 15 20 25 30
> 
> **输入:** n = 5，g = 3
> T3】输出: 3 6 9 12 15

**方法:**当序列由以下元素组成时，序列的总和将最小:
T3】g，2 * g，3 * g，4 * g，…..，n * g 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the required sequence
void generateSequence(int n, int g)
{
    for (int i = 1; i <= n; i++)
        cout << i * g << " ";
}

// Driver Code
int main()
{
    int n = 6, g = 5;
    generateSequence(n, g);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to print the required sequence
    static void generateSequence(int n, int g)
    {
        for (int i = 1; i <= n; i++)
            System.out.print(i * g + " ");;
    }

    // Driver Code
    public static void main(String []args)
    {
        int n = 6, g = 5;
        generateSequence(n, g);

    }
}

// This code is contributed by Rituraj Jain
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to print the required sequence
def generateSequence(n, g):

    for i in range(1, n + 1):
        print(i * g, end = " ")

# Driver Code
if __name__ == "__main__":

    n, g = 6, 5
    generateSequence(n, g)

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System ;

class GFG
{

    // Function to print the required sequence
    static void generateSequence(int n, int g)
    {
        for (int i = 1; i <= n; i++)
            Console.Write(i * g + " ");
    }

    // Driver Code
    public static void Main()
    {
        int n = 6, g = 5;
        generateSequence(n, g);
    }
}

// This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to print the required sequence
function generateSequence($n, $g)
{
    for ($i = 1; $i <= $n; $i++)
        echo $i * $g . " ";
}

// Driver Code
$n = 6;
$g = 5;
generateSequence($n, $g);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to print the required sequence
function generateSequence(n, g)
{
    for (var i = 1; i <= n; i++)
    {
        document.write(i*g+" ");
    }
}

// Driver Code
var n = 6, g = 5;
generateSequence(n, g);

</script>
```

**Output:** 

```
5 10 15 20 25 30
```