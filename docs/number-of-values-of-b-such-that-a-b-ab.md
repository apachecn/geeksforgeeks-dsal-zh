# 使得 a = b + (a^b)的 b 的值的数量

> 原文:[https://www . geeksforgeeks . org/of-b-so-a-b-ab/](https://www.geeksforgeeks.org/number-of-values-of-b-such-that-a-b-ab/)

给定一个整数![a    ](img/e601e610cd0f8488d8b71390172c9e86.png "Rendered by QuickLaTeX.com")。求![b    ](img/56c19e62ea115719245402c109e4c477.png "Rendered by QuickLaTeX.com")的解数，满足方程:

> **a = b + (a^b)**

**示例:**

```
Input: a = 4 
Output: 2
The only values of b are 0 and 4 itself.

Input: a = 3 
Output: 4 
```

一个**天真的解决方案**是从 0 迭代到![a    ](img/e601e610cd0f8488d8b71390172c9e86.png "Rendered by QuickLaTeX.com")，并计算满足给定方程的值的数量。我们只需要遍历到![a    ](img/e601e610cd0f8488d8b71390172c9e86.png "Rendered by QuickLaTeX.com")，因为任何大于![a    ](img/e601e610cd0f8488d8b71390172c9e86.png "Rendered by QuickLaTeX.com")的值都会给出异或值> ![a    ](img/e601e610cd0f8488d8b71390172c9e86.png "Rendered by QuickLaTeX.com")，因此不能满足等式。

下面是上述方法的实现:

## C++

```
// C++ program to find the number of values
// of b such that a = b + (a^b)
#include <bits/stdc++.h>
using namespace std;

// function to return the number of solutions
int countSolutions(int a)
{
    int count = 0;

    // check for every possible value
    for (int i = 0; i <= a; i++) {
        if (a == (i + (a ^ i)))
            count++;
    }

    return count;
}

// Driver Code
int main()
{
    int a = 3;
    cout << countSolutions(a);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the number of values
// of b such that a = b + (a^b)

import java.io.*;

class GFG {

// function to return the number of solutions
 static int countSolutions(int a)
{
    int count = 0;

    // check for every possible value
    for (int i = 0; i <= a; i++) {
        if (a == (i + (a ^ i)))
            count++;
    }

    return count;
}

// Driver Code

    public static void main (String[] args) {
        int a = 3;
    System.out.println( countSolutions(a));
    }
}
// This code is contributed by inder_verma
```

## 蟒蛇 3

```
# Python 3 program to find
# the number of values of b
# such that a = b + (a^b)

# function to return the
# number of solutions
def countSolutions(a):

    count = 0

    # check for every possible value
    for i in range(a + 1):
        if (a == (i + (a ^ i))):
            count += 1

    return count

# Driver Code
if __name__ == "__main__":
    a = 3
    print(countSolutions(a))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to find the number of
// values of b such that a = b + (a^b)
using System;

class GFG
{

// function to return the
// number of solutions
static int countSolutions(int a)
{
    int count = 0;

    // check for every possible value
    for (int i = 0; i <= a; i++)
    {
        if (a == (i + (a ^ i)))
            count++;
    }

    return count;
}

// Driver Code
public static void Main ()
{
    int a = 3;
    Console.WriteLine(countSolutions(a));
}
}

// This code is contributed by inder_verma
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the number of
// values of b such that a = b + (a^b)

// function to return the
// number of solutions
function countSolutions($a)
{
    $count = 0;

    // check for every possible value
    for ($i = 0; $i <= $a; $i++)
    {
        if ($a == ($i + ($a ^ $i)))
            $count++;
    }

    return $count;
}

// Driver Code
$a = 3;
echo countSolutions($a);

// This code is contributed
// by inder_verma
?>
```

## java 描述语言

```
<script>

// Javascript program to find the number of values
// of b such that a = b + (a^b)

// function to return the number of solutions
function countSolutions(a)
{
    let count = 0;

    // check for every possible value
    for (let i = 0; i <= a; i++) {
        if (a == (i + (a ^ i)))
            count++;
    }

    return count;
}

// Driver Code
let a = 3;
document.write(countSolutions(a));

</script>
```

**Output:** 

```
4
```

**时间复杂度** : O(a)

一个有效的方法是当我们为不同的 T2 值写可能的答案时，观察答案的模式。只有设置位用于确定可能答案的数量。这个问题的答案永远是 2^(number，它可以通过观察来确定。

下面是上述方法的实现:

## C++

```
// C++ program to find the number of values
// of b such that a = b + (a^b)
#include <bits/stdc++.h>
using namespace std;

// function to return the number of solutions
int countSolutions(int a)
{
    int count = __builtin_popcount(a);

    count = pow(2, count);
    return count;
}

// Driver Code
int main()
{
    int a = 3;
    cout << countSolutions(a);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the number of values
// of b such that a = b + (a^b)
import java.io.*;
class GFG
{

    // function to return the number of solutions
    static int countSolutions(int a)
    {
        int count = Integer.bitCount(a);

        count =(int) Math.pow(2, count);
        return count;
    }

    // Driver Code
        public static void main (String[] args)
    {
        int a = 3;
        System.out.println(countSolutions(a));
    }
}
// This code is contributed by Raj
```

## 蟒蛇 3

```
# Python3 program to find the number
# of values of b such that a = b + (a^b)

# function to return the number
# of solutions
def countSolutions(a):

    count = bin(a).count('1')
    return 2 ** count

# Driver Code
if __name__ == "__main__":

    a = 3
    print(countSolutions(a))

# This code is contributed by
# Rituraj Jain
```

## C#

```
// C# program to find the number of
// values of b such that a = b + (a^b)
class GFG
{

// function to return the number
// of solutions
static int countSolutions(int a)
{
    int count = bitCount(a);

    count =(int) System.Math.Pow(2, count);
    return count;
}

static int bitCount(int n)
{
    int count = 0;
    while (n != 0)
    {
        count++;
        n &= (n - 1);
    }
    return count;
}

// Driver Code
public static void Main()
{
    int a = 3;
    System.Console.WriteLine(countSolutions(a));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the number of
// values of b such that a = b + (a^b)

// function to return the number
// of solutions
function countSolutions($a)
{
    $count = bitCount($a);

    $count = (int)pow(2, $count);
    return $count;
}

function bitCount($n)
{
    $count = 0;
    while ($n != 0)
    {
        $count++;
        $n &= ($n - 1);
    }
    return $count;
}

// Driver Code
$a = 3;
echo (countSolutions($a));

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript program to find the number
// of values of b such that a = b + (a^b)
function bitCount(n)
{
    let count = 0;
    while (n != 0)
    {
        count++;
        n &= (n - 1);
    }
    return count;
}

// Function to return the number of solutions
function countSolutions(a)
{
    let count = bitCount(a);

    count = Math.pow(2, count);
    return count;
}

// Driver Code
let a = 3;

document.write(countSolutions(a));

// This code is contributed by subhammahato348

</script>
```

**Output:** 

```
4
```

**时间复杂度:** O(log N)