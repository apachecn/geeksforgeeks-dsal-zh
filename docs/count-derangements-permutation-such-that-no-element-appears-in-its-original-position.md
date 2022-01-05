# 计数错乱(排列使得没有元素出现在其原始位置)

> 原文:[https://www . geeksforgeeks . org/count-range ments-arrangement-so-no-element-in-original-position/](https://www.geeksforgeeks.org/count-derangements-permutation-such-that-no-element-appears-in-its-original-position/)

无序是 n 个元素的排列，因此没有元素出现在其原始位置。例如，{0，1，2，3}的混乱是{2，3，1，0}。
给定一个数 n，求一组 n 个元素的错乱总数。

**示例:**

```
Input: n = 2
Output: 1
For two elements say {0, 1}, there is only one 
possible derangement {1, 0}

Input: n = 3
Output: 2
For three elements say {0, 1, 2}, there are two 
possible derangements {2, 0, 1} and {1, 2, 0}

Input: n = 4
Output: 9
For four elements say {0, 1, 2, 3}, there are 9
possible derangements {1, 0, 3, 2} {1, 2, 3, 0}
{1, 3, 0, 2}, {2, 3, 0, 1}, {2, 0, 3, 1}, {2, 3,
1, 0}, {3, 0, 1, 2}, {3, 2, 0, 1} and {3, 2, 1, 0}
```

设 counter der(n)是 n 个元素的错乱数。下面是它的递归关系。

```
countDer(n) = (n - 1) * [countDer(n - 1) + countDer(n - 2)]
```

**上述递归关系是如何工作的？**

元素 0 有 n–1 种方式(这解释了与 n–1 的乘法)。
将*T2【0】置于指数 IT4。现在有两种可能性，取决于元素 I 是否放在 0 处作为回报。*

1.  ***i 置于 0:*** 这种情况相当于解决了 n-2 个元素的问题，因为两个元素刚刚交换了位置。
2.  ***i 不在 0:*** 这种情况相当于解决了 n-1 个元素的问题，因为现在有 n-1 个元素，n-1 个位置，每个元素都有 n-2 个选择

以下是基于上述递归公式的简单解决方案:

## C++

```
// A Naive Recursive C++ program
// to count derangements
#include <bits/stdc++.h>
using namespace std;

int countDer(int n)
{
  // Base cases
  if (n == 1) return 0;
  if (n == 2) return 1;

  // countDer(n) = (n-1)[countDer(n-1) + der(n-2)]
  return (n - 1) * (countDer(n - 1) + countDer(n - 2));
}

// Driver Code
int main()
{
    int n = 4;
    cout << "Count of Derangements is "
         << countDer(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Naive Recursive java
// program to count derangements
import java.io.*;

class GFG
{

    // Function to count
    // derangements
    static int countDer(int n)
    {
        // Base cases
        if (n == 1) return 0;
        if (n == 2) return 1;

        // countDer(n) = (n-1)[countDer(n-1) + der(n-2)]
        return (n - 1) * (countDer(n - 1) +
                          countDer(n - 2));
    }

    // Driver Code
    public static void main (String[] args)
    {
        int n = 4;
        System.out.println( "Count of Derangements is "
                             +countDer(n));

    }
}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# A Naive Recursive Python3
# program to count derangements

def countDer(n):

    # Base cases
    if (n == 1): return 0
    if (n == 2): return 1

    # countDer(n) = (n-1)[countDer(n-1) + der(n-2)]
    return (n - 1) * (countDer(n - 1) +
                      countDer(n - 2))

# Driver Code
n = 4
print("Count of Derangements is ", countDer(n))

# This code is contributed by Azkia Anam.
```

## C#

```
// A Naive Recursive C#
// program to count derangements
using System;

class GFG
{

    // Function to count
    // derangements
    static int countDer(int n)
    {
        // Base cases
        if (n == 1) return 0;
        if (n == 2) return 1;

        // countDer(n) = (n-1)[countDer(n-1) + der(n-2)]
        return (n - 1) * (countDer(n - 1) +
                          countDer(n - 2));
    }

    // Driver Code
    public static void Main ()
    {
        int n = 4;
        Console.Write( "Count of Derangements is " +
                        countDer(n));

    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A Naive Recursive PHP program
// to count derangements

function countDer($n)
{

    // Base cases
    if ($n == 1)
        return 0;
    if ($n == 2)
        return 1;

    // countDer(n) = (n-1)[countDer(n-1) +
    // der(n-2)]
    return ($n - 1) * (countDer($n - 1) +
                       countDer($n - 2));
}

    // Driver Code
    $n = 4;
    echo "Count of Derangements is ", countDer($n);

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

    // A Naive Recursive Javascript
    // program to count derangements

    // Function to count
    // derangements
    function countDer(n)
    {
        // Base cases
        if (n == 1) return 0;
        if (n == 2) return 1;

        // countDer(n) = (n-1)[countDer(n-1) + der(n-2)]
        return (n - 1) * (countDer(n - 1) + countDer(n - 2));
    }

    let n = 4;
    document.write("Count of Derangements is " + countDer(n));

</script>
```

**Output**

```
Count of Derangements is 9
```

**时间复杂度:T(n) = T(n-1) + T(n-2)，为指数。**

我们可以观察到这个实现确实重复工作。例如，参见 counter der(5)的递归树，counter der(3)被求值两次。

```
cdr() ==> countDer()

                    cdr(5)   
                 /         \     
             cdr(4)          cdr(3)   
           /      \         /     \
       cdr(3)     cdr(2)  cdr(2)   cdr(1)
```

一种**高效的解决方案**是使用动态规划将子问题的结果存储在数组中，并以自下而上的方式构建数组。

## C++

```
// A Dynamic programming based C++
// program to count derangements
#include <bits/stdc++.h>
using namespace std;

int countDer(int n)
{
    // Create an array to store
    // counts for subproblems
    int der[n + 1] = {0};

    // Base cases
    der[1] = 0;
    der[2] = 1;

    // Fill der[0..n] in bottom up manner
    // using above recursive formula
    for (int i = 3; i <= n; ++i)
        der[i] = (i - 1) * (der[i - 1] +
                            der[i - 2]);

    // Return result for n
    return der[n];
}

// Driver code
int main()
{
    int n = 4;
    cout << "Count of Derangements is "
         << countDer(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Dynamic programming based
// java program to count derangements
import java.io.*;

class GFG
{

    // Function to count
    // derangements
    static int countDer(int n)
    {
        // Create an array to store
        // counts for subproblems
        int der[] = new int[n + 1];

        // Base cases
        der[1] = 0;
        der[2] = 1;

        // Fill der[0..n] in bottom up
        // manner using above recursive
        // formula
        for (int i = 3; i <= n; ++i)
            der[i] = (i - 1) * (der[i - 1] +
                                der[i - 2]);

        // Return result for n
        return der[n];
    }

    // Driver program
    public static void main (String[] args)
    {
        int n = 4;
        System.out.println("Count of Derangements is " +
                            countDer(n));

    }
}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# A Dynamic programming based Python3
# program to count derangements

def countDer(n):

    # Create an array to store
    # counts for subproblems
    der = [0 for i in range(n + 1)]

    # Base cases
    der[1] = 0
    der[2] = 1

    # Fill der[0..n] in bottom up manner
    # using above recursive formula
    for i in range(3, n + 1):
        der[i] = (i - 1) * (der[i - 1] +
                            der[i - 2])

    # Return result for n
    return der[n]

# Driver Code
n = 4
print("Count of Derangements is ", countDer(n))

# This code is contributed by Azkia Anam.
```

## C#

```
// A Dynamic programming based
// C# program to count derangements
using System;

class GFG
{

    // Function to count
    // derangements
    static int countDer(int n)
    {
        // Create an array to store
        // counts for subproblems
        int []der = new int[n + 1];

        // Base cases
        der[1] = 0;
        der[2] = 1;

        // Fill der[0..n] in bottom up
        // manner using above recursive
        // formula
        for (int i = 3; i <= n; ++i)
            der[i] = (i - 1) * (der[i - 1] +
                                der[i - 2]);

        // Return result for n
        return der[n];
    }

    // Driver code
    public static void Main ()
    {
        int n = 4;
        Console.Write("Count of Derangements is " +
                       countDer(n));

    }
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A Dynamic programming based PHP
// program to count derangements

function countDer($n)
{
    // Create an array to store
    // counts for subproblems

    // Base cases
    $der[1] = 0;
    $der[2] = 1;

    // Fill der[0..n] in bottom up manner
    // using above recursive formula
    for ($i = 3; $i <= $n; ++$i)
        $der[$i] = ($i - 1) * ($der[$i - 1] +
                               $der[$i - 2]);

    // Return result for n
    return $der[$n];
}

// Driver code
$n = 4;
echo "Count of Derangements is ",
                    countDer($n);

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>

    // A Dynamic programming based
    // javascript program to count
    // derangements

    // Function to count
    // derangements
    function countDer(n)
    {
        // Create an array to store
        // counts for subproblems
        let der = new Array(n + 1);

        // Base cases
        der[1] = 0;
        der[2] = 1;

        // Fill der[0..n] in bottom up
        // manner using above recursive
        // formula
        for (let i = 3; i <= n; ++i)
            der[i] = (i - 1) * (der[i - 1] +
                                der[i - 2]);

        // Return result for n
        return der[n];
    }

    let n = 4;
    document.write(
    "Count of Derangements is " + countDer(n)
    );

</script>
```

**Output**

```
Count of Derangements is 9
```

***时间复杂度:** O(n)*
***辅助空间:** O(n)*
感谢乌卡什·特里维迪提出上述解决方案。

无需使用**额外空间**的高效解决方案。

因为我们只需要记住两个先前的值，所以，两个变量可以用来只存储所需的先前值，而不是将值存储在数组中。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above
// approach

#include <iostream>
using namespace std;

int countDer(int n)
{

    // base case
    if (n == 1 or n == 2) {
        return n - 1;
    }

    // Variable for just storing
    // previous values
    int a = 0;
    int b = 1;

    // using above recursive formula
    for (int i = 3; i <= n; ++i) {
        int cur = (i - 1) * (a + b);
        a = b;
        b = cur;
    }

    // Return result for n
    return b;
}

// Driver Code
int main()
{

    cout << "Count of Dearrangements is " << countDer(4);
    return 0;
}

 // Code contributed by skagnihotri
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the
// above approach

import java.io.*;

class GFG {

    // Function to count derangements 
    static int countDer(int n) {
        // Base case
          if(n == 1 || n == 2) {
            return n-1;
        }

        // Variable for storing prev values
        int a = 0;
          int b = 1;

        // manner using above recursive formula
        for (int i = 3; i <= n; ++i) {
            int cur = (i-1)*(a+b);
            a = b;
              b = cur;
        }

        // Return result for n
        return b;
    }

    // Driver Code
    public static void main (String[] args) 
    {
        int n = 4;
        System.out.println("Count of Dearrangements is " + 
                            countDer(n));

    }

  // Code contributed by skagnihotri
}
```

## 计算机编程语言

```
# Python program to count derangements

def countDer(n):

    # Base Case
    if n == 1 or n == 2:
      return n-1;

    # Variables for storing previous values
    a = 0
    b = 1

    # using above recursive formula
    for i in range(3, n + 1):
        cur = (i-1)*(a+b)
        a = b
        b = cur

    # Return result for n
    return b

# Driver Code
n = 4
print("Count of Dearrangements is ", countDer(n))
# Code contributed by skagnihotri
```

## C#

```
// C# implementation of the above
// approach
using System;

class GFG{

// Function to count
// derangements
static int countDer(int n)
{

    // Base case
    if (n == 1 || n == 2)
    {
        return n - 1;
    }

    // Variable for just storing
    // previous values
    int a = 0;
    int b = 1;

    // Using above recursive formula
    for(int i = 3; i <= n; ++i)
    {
        int cur = (i - 1) * (a + b);
        a = b;
        b = cur;
    }

    // Return result for n
    return b;
}

// Driver code
public static void Main()
{
    Console.Write("Count of Dearrangements is " +
                   countDer(4));
}
}

// This code is contributed by koulick_sadhu
```

## java 描述语言

```
<script>

    // Javascript implementation
    // of the above approach

    // Function to count
    // derangements
    function countDer(n)
    {

        // Base case
        if (n == 1 || n == 2)
        {
            return n - 1;
        }

        // Variable for just storing
        // previous values
        let a = 0;
        let b = 1;

        // Using above recursive formula
        for(let i = 3; i <= n; ++i)
        {
            let cur = (i - 1) * (a + b);
            a = b;
            b = cur;
        }

        // Return result for n
        return b;
    }

    document.write("Count of Derangements is "
    + countDer(4));

</script>
```

**Output**

```
Count of Derangements is 9
```

***时间复杂度:**O(n)**T5
*T8】辅助空间: O(1)****

**感谢 Shubham Kumar 提出上述解决方案。**

****参考资料:**
[https://en . Wikipedia . org/wiki/consideration](https://en.wikipedia.org/wiki/Derangement)**

**如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。**