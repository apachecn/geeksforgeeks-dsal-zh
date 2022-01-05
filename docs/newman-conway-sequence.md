# 纽曼-康威序列

> 原文:[https://www.geeksforgeeks.org/newman-conway-sequence/](https://www.geeksforgeeks.org/newman-conway-sequence/)

纽曼-康威序列是生成以下整数序列的序列。
1 1 2 3 4 4 5 6 7……
在数学术语中，纽曼-康威数的序列 P(n)由递推关系定义

```
P(n) = P(P(n - 1)) + P(n - P(n - 1)) 
```

用种子值 P(1) = 1 和 P(2) = 1
给定一个数 n，在纽曼-康威序列中打印第 n 个数。

示例:

```
Input : n = 2
Output : 1

Input : n = 10
Output : 6
```

**方法 1(使用递归):**

一个简单的方法是直接递归实现上述递归关系。

## C++

```
// C++ program for n-th
// element of Newman-Conway Sequence
#include <bits/stdc++.h>
using namespace std;

// Recursive Function to find the n-th element
int sequence(int n)
{
    if (n == 1 || n == 2)
        return 1;
    else
        return sequence(sequence(n - 1))
                + sequence(n - sequence(n - 1));
}

// Driver Program
int main()
{
    int n = 10;
    cout << sequence(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find nth
// element of Newman-Conway Sequence
import java.io.*;

class GFG {

    // Recursion to find
    // n-th element
    static int sequence(int n)
    {
        if (n == 1 || n == 2)
            return 1;
        else
            return sequence(sequence(n - 1))
                  + sequence(n - sequence(n - 1));
    }

    // Driver Program
    public static void main(String args[])
    {
        int n = 10;
        System.out.println(sequence(n));
    }
}

/*This code is contributed by Nikita Tiwari.*/
```

## 计算机编程语言

```
# Recursive function to find the n-th
# element of sequence
def sequence(n):
    if n == 1 or n == 2:
        return 1
    else:
        return sequence(sequence(n-1)) + sequence(n-sequence(n-1));

# Driver code
def main():
    n = 10
    print sequence(n)

if __name__ == '__main__':
    main()
```

## C#

```
// C# program to find nth element
// of Newman-Conway Sequence
using System;

class GFG {

    // Recursion to find
    // n-th element
    static int sequence(int n)
    {
        if (n == 1 || n == 2)
            return 1;
        else
            return sequence(sequence(n - 1)) + sequence
                           (n - sequence(n - 1));
    }

    // Driver code
    public static void Main()
    {
        int n = 10;
        Console.Write(sequence(n));
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for n-th element
// of Newman-Conway Sequence

// Recursive Function to
// find the n-th element
function sequence($n)
{
    if ($n == 1 || $n == 2)
        return 1;
    else
        return sequence(sequence($n - 1))+
               sequence($n - sequence($n - 1));
}

// Driver Code
$n = 10;
echo(sequence($n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// JavaScript program to find nth
// element of Newman-Conway Sequence

// Recursion to find
// n-th element
function sequence(n)
{
    if (n == 1 || n == 2)
        return 1;
    else
        return sequence(sequence(n - 1)) +
           sequence(n - sequence(n - 1));
}

// Driver code
let n = 10;
document.write(sequence(n));

// This code is contributed by souravghosh0416  

</script>
```

**输出:**

```
6
```

**方法 2(使用动态编程):**
我们可以通过将序列中的值存储在数组中来避免重复方法 1 中所做的工作。

## C++

```
// C++ program to find the n-th element of
// Newman-Conway Sequence
#include <bits/stdc++.h>
using namespace std;

// Function to find the n-th element
int sequence(int n)
{
    // Declare array to store sequence
    int f[n + 1];
    int i;
    f[0] = 0;
    f[1] = 1;
    f[2] = 1;

    for (i = 3; i <= n; i++)
        f[i] = f[f[i - 1]] + f[i - f[i - 1]];   

    return f[n];
}

// Driver Program
int main()
{
    int n = 10;
    cout << sequence(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA Code for Newman-Conway Sequence
import java.util.*;

class GFG {

    // Function to find the n-th element
    static int sequence(int n)
    {
        // Declare array to store sequence
        int f[] = new int[n + 1];
        f[0] = 0;
        f[1] = 1;
        f[2] = 1;

        int i;

        for (i = 3; i <= n; i++)
            f[i] = f[f[i - 1]] +
                        f[i - f[i - 1]];   

        return f[n];
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
         int n = 10;
         System.out.println(sequence(n));

    }
}

// This code is contributed by Arnav Kr. Mandal.
```

## 计算机编程语言

```
''' Python program to find the n-th element of
    Newman-Conway Sequence'''

# To declare array import module array
import array
def sequence(n):
    f = array.array('i', [0, 1, 1])

    # To store values of sequence in array
    for i in range(3, n + 1):
        r = f[f[i-1]]+f[i-f[i-1]]
        f.append(r);

    return r

# Driver code
def main():
    n = 10
    print sequence(n)

if __name__ == '__main__':
    main()
```

## C#

```
// C# Code for Newman-Conway Sequence
using System;

class GFG {

    // Function to find the n-th element
    static int sequence(int n)
    {
        // Declare array to store sequence
        int []f = new int[n + 1];
        f[0] = 0;
        f[1] = 1;
        f[2] = 1;

        int i;

        for (i = 3; i <= n; i++)
            f[i] = f[f[i - 1]] +
                   f[i - f[i - 1]];

        return f[n];
    }

    // Driver Code
    public static void Main()
    {
        int n = 10;
        Console.Write(sequence(n));

    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the n-th element 
// of Newman-Conway Sequence

// Function to find
// the n-th element
function sequence($n)
{

    // Declare array to
    // store sequence
    $i;
    $f[0] = 0;
    $f[1] = 1;
    $f[2] = 1;

    for ($i = 3; $i <= $n; $i++)
        $f[$i] = $f[$f[$i - 1]] +
                 $f[$i - $f[$i - 1]];

    return $f[$n];
}

// Driver Code
$n = 10;
echo(sequence($n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>
// Javascript program to find the n-th element
// of Newman-Conway Sequence

// Function to find
// the n-th element
function sequence(n)
{

    // Declare array to
    // store sequence
    let i;
    let f = [];
    f[0] = 0;
    f[1] = 1;
    f[2] = 1;

    for (let i = 3; i <= n; i++)
        f[i] = f[f[i - 1]] +
                f[i - f[i - 1]];

    return f[n];
}

// Driver Code
let n = 10;
document.write(sequence(n));

// This code is contributed by gfgking.
</script>
```

**输出:**

```
6
```

时间复杂度:O(n)
**参考文献:**[https://archive.lib.msu.edu/crcmath/math/math/n/n078.htm](https://archive.lib.msu.edu/crcmath/math/math/n/n078.htm)T5】