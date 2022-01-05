# 打印数字 N 的按位“与”集

> 原文:[https://www . geesforgeks . org/print-bitwise-and-set-of-a-number-n/](https://www.geeksforgeeks.org/print-bitwise-and-set-of-a-number-n/)

给定一个数字 N，打印所有的数字，这些数字是 N 的二进制表示的按位“与”集合。按位“与”集合 N 是所有可能的小于或等于 N 的数字 x，使得对于某个数字 I，N & i 等于 x

**示例:**

```
Input : N = 5
Output : 0, 1, 4, 5 
Explanation: 0 & 5 = 0 
             1 & 5 = 1
             2 & 5 = 0
             3 & 5 = 1
             4 & 5 = 4
             5 & 5 = 5  
So we get 0, 1, 4 and 5 in the 
bitwise subsets of N.

Input : N = 9
Output : 0, 1, 8, 9 
```

**简单方法**:一个天真的方法是从 0 到 N 迭代所有的数字，检查是否(N & i == i)。打印满足指定条件的数字。

以下是上述想法的实现:

## C++

```
// CPP program to print all bitwise
// subsets of N (Naive approach)
#include <bits/stdc++.h>
using namespace std;

// function to find bitwise subsets
// Naive approach
void printSubsets(int n) {
  for (int i = 0; i <= n; i++)
    if ((n & i) == i)
      cout << i << " ";
}

// Driver Code
int main() {

  int n = 9;
  printSubsets(n);
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to print all bitwise
// subsets of N (Naive approach)
class GFG {

    // function to find bitwise subsets
    // Naive approach
    static void printSubsets(int n)
    {

        for (int i = 0; i <= n; i++)
            if ((n & i) == i)
                System.out.print(i + " ");
    }

    // Driver function
    public static void main(String[] args)
    {
        int n = 9;

        printSubsets(n);
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python program to print all bitwise
# subsets of N (Naive approach)
def printSubsets(n):

    for i in range(n + 1):

        if ((n & i) == i):
            print(i ," ", end = "")

# Driver code
n = 9
printSubsets(n)

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# program to print all bitwise
// subsets of N (Naive approach)
using System;

class GFG {

    // function to find bitwise subsets
    // Naive approach
    static void printSubsets(int n)
    {

        for (int i = 0; i <= n; i++)
            if ((n & i) == i)
                Console.Write(i + " ");
    }

    // Driver function
    public static void Main()
    {
        int n = 9;

        printSubsets(n);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print all bitwise
// subsets of N (Naive approach)

// function to find bitwise subsets
// Naive approach
function printSubsets($n)
{
for ($i = 0; $i <= $n; $i++)
    if (($n & $i) == $i)
    echo $i." ";
}

// Driver Code
$n = 9;
printSubsets($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript program to print all bitwise
// subsets of N (Efficient approach)

// function to find bitwise
    // subsets Efficient approach
    function printSubsets(n)
    {
    for (let i = n; i > 0; i = (i - 1) & n)

        document.write(i + " ");
        document.write(" 0 ");

    }
// Driver code

    let n = 9;
    printSubsets(n);

// This code is contributed by souravghosh0416.
</script>
```

**输出:**

```
0 1 8 9
```

**时间复杂度:** O(N)

**高效解决方案**:高效的解决方案是使用按位运算符来查找子集。我们可以只迭代按位子集，而不是迭代每个 I。向后迭代 **i=(i-1) & n** 给我们每个按位子集，其中我从 n 开始，以 1 结束。

以下是上述想法的实现:

## C++

```
// CPP program to print all bitwise
// subsets of N (Efficient approach)

#include <bits/stdc++.h>
using namespace std;

// function to find bitwise subsets
// Efficient approach
void printSubsets(int n) {

  for (int i = n; i > 0; i = (i - 1) & n)
    cout << i << " ";
  cout << 0;
}

// Driver Code
int main() { 
  int n = 9; 
  printSubsets(n); 
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all bitwise
// subsets of N (Efficient approach)

class GFG
{

    // function to find bitwise
    // subsets Efficient approach
    static void printSubsets(int n)
    {
    for (int i = n; i > 0; i = (i - 1) & n)

        System.out.print(i + " ");
        System.out.print(" 0 ");

    }

// Driver Code
public static void main(String[] args)
{
    int n = 9;
    printSubsets(n);
}
}

// This code is contributed by ajit.
```

## 蟒蛇 3

```
# Python 3 program to
# print all bitwise
# subsets of N
# (Efficient approach)

# function to find
# bitwise subsets
# Efficient approach
def printSubsets(n):
    i=n
    while(i != 0):
        print(i,end=" ")
        i=(i - 1) & n
    print("0")

# Driver Code
n = 9
printSubsets(n)

# This code is contributed by
# Smith Dinesh Semwal
```

## C#

```
// C# program to print all bitwise
// subsets of N (Efficient approach)
using System;

public class GFG {

    // function to find bitwise subsets
    // Efficient approach
    static void printSubsets(int n) {

    for (int i = n; i > 0; i = (i - 1) & n)
        Console.Write(i +" ");
        Console.WriteLine("0");
    }

    // Driver Code
    static public void Main () {

        int n = 9;

        printSubsets(n);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print all bitwise
// subsets of N (Efficient approach)

// function to find bitwise subsets
// Efficient approach
function printSubsets($n)
{

    for ($i = $n; $i > 0;
         $i = ($i - 1) & $n)

        echo $i." ";
    echo "0";
}

// Driver Code
$n = 9;
printSubsets($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to print all bitwise
// subsets of N (Efficient approach)

// Function to find bitwise subsets
// Efficient approach
function printSubsets(n)
{
    for(let i = n; i > 0; i = (i - 1) & n)
        document.write(i +" ");
        document.write("0" + "</br>");
}

// Driver code
let n = 9;

printSubsets(n);

// This code is contributed by divyesh072019

</script>
```

**输出:**

```
9 8 1 0
```

**时间复杂度** : O(K)，其中 K 是 n 的按位子集数