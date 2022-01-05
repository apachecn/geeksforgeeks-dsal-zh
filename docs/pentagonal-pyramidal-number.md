# 五边形金字塔数字

> 原文:[https://www.geeksforgeeks.org/pentagonal-pyramidal-number/](https://www.geeksforgeeks.org/pentagonal-pyramidal-number/)

给定一个数 n，求第 n 个五边形金字塔数。
A [**五边形棱锥数**](https://en.wikipedia.org/wiki/Pentagonal_pyramidal_number) 属于具象数类。它是以五边形为底的金字塔中物体的数量。第 n 个五边形金字塔数等于前 n 个[五边形数](https://www.geeksforgeeks.org/nth-pentagonal-number/)之和。
**举例:**

```
Input : n = 3 
Output : 18

Input : n = 7
Output : 196
```

**方法一:(天真的方法):**
这个方法很简单。它说把所有的五边形数加起来到 n(通过运行循环)得到第 n 个五边形金字塔数。

以下是该方法的实现:

## C++

```
// CPP Program to get nth Pentagonal
// pyramidal number.
#include <bits/stdc++.h>
using namespace std;

// function to get nth Pentagonal
// pyramidal number.
int pentagon_pyramidal(int n)
{
    int sum = 0;

    // Running loop from 1 to n
    for (int i = 1; i <= n; i++) {

        // get nth pentagonal number
        int p = (3 * i * i - i) / 2;

        // add to sum
        sum = sum + p;
    }
    return sum;
}

// Driver Program
int main()
{
    int n = 4;
    cout << pentagon_pyramidal(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to get nth
// Pentagonal pyramidal number.
import java.io.*;

class GFG
{

// function to get nth
// Pentagonal pyramidal number.
static int pentagon_pyramidal(int n)
{
    int sum = 0;

    // Running loop from 1 to n
    for (int i = 1; i <= n; i++)
    {

        // get nth pentagonal number
        int p = (3 * i * i - i) / 2;

        // add to sum
        sum = sum + p;
    }
    return sum;
}

// Driver Code
public static void main (String[] args)
{
    int n = 4;
    System.out.println(pentagon_pyramidal(n));
}
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python3 Program to get nth Pentagonal
# pyramidal number.

# function to get nth Pentagonal
# pyramidal number.
def pentagon_pyramidal(n):
    sum = 0

    # Running loop from 1 to n
    for i in range(1, n + 1):

        # get nth pentagonal number
        p = ( 3 * i * i - i ) / 2

        # add to sum
        sum = sum + p      

    return sum

# Driver Program
n = 4
print(int(pentagon_pyramidal(n)))
```

## C#

```
// C# Program to get nth
// Pentagonal pyramidal number.
using System;

class GFG
{

// function to get nth
// Pentagonal pyramidal number.
static int pentagon_pyramidal(int n)
{
    int sum = 0;

    // Running loop from 1 to n
    for (int i = 1; i <= n; i++)
    {

        // get nth pentagonal number
        int p = (3 * i *
                 i - i) / 2;

        // add to sum
        sum = sum + p;
    }
    return sum;
}

// Driver Code
static public void Main ()
{
    int n = 4;
    Console.WriteLine(pentagon_pyramidal(n));
}
}

// This code is contributed by ajit.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to get nth
// Pentagonal pyramidal number.

// function to get nth
// Pentagonal pyramidal number.
function pentagon_pyramidal($n)
{
    $sum = 0;

    // Running loop from 1 to n
    for ($i = 1; $i <= $n; $i++)
    {

        // get nth pentagonal number
        $p = (3 * $i *
                  $i - $i) / 2;

        // add to sum
        $sum = $sum + $p;
    }
    return $sum;
}

// Driver Code
$n = 4;
echo pentagon_pyramidal($n);

// This code is contributed by m_kit
?>
```

## java 描述语言

```
<script>
// javascript Program to get nth
// Pentagonal pyramidal number.

// function to get nth
// Pentagonal pyramidal number.
function pentagon_pyramidal(n)
{
    var sum = 0;

    // Running loop from 1 to n
    for (i = 1; i <= n; i++)
    {

        // get nth pentagonal number
        var p = (3 * i * i - i) / 2;

        // add to sum
        sum = sum + p;
    }
    return sum;
}

// Driver Code
var n = 4;
document.write(pentagon_pyramidal(n));

// This code is contributed by Amit Katiyar
</script>
```

**输出:**

```
40
```

**时间复杂度:** O(n)

**方法二:(高效方法):**
在这种方法中，我们用公式得到 O(1)时间内的第 n 个五边形金字塔数。

第 n 个五边形金字塔数= **n <sup>2</sup> (n + 1) / 2**
下面是这种方法的实现:

## C++

```
// CPP Program to get nth Pentagonal
// pyramidal number.
#include <bits/stdc++.h>
using namespace std;

// function to get nth Pentagonal
// pyramidal number.
int pentagon_pyramidal(int n)
{
    return n * n * (n + 1) / 2;
}

// Driver Program
int main()
{
    int n = 4;
    cout << pentagon_pyramidal(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to get nth
// Pentagonal pyramidal number.
import java.io.*;

class GFG
{

// function to get nth
// Pentagonal pyramidal number.
static int pentagon_pyramidal(int n)
{
    return n * n *
          (n + 1) / 2;
}

// Driver Code
public static void main (String[] args)
{
    int n = 4;
    System.out.println(pentagon_pyramidal(n));
}
}

// This code is contributed by ajit
```

## 蟒蛇 3

```
# Python3 Program to get nth Pentagonal
# pyramidal number.

# function to get nth Pentagonal
# pyramidal number.
def pentagon_pyramidal(n):    
    return n * n * (n + 1) / 2

# Driver Program
n = 4
print(int(pentagon_pyramidal(n)))
```

## C#

```
// C# Program to get nth
// Pentagonal pyramidal number.
using System;

class GFG
{

// function to get nth
// Pentagonal pyramidal number.
static int pentagon_pyramidal(int n)
{
    return n * n *
          (n + 1) / 2;
}

// Driver Code
static public void Main ()
{
    int n = 4;
    Console.WriteLine(
            pentagon_pyramidal(n));
}
}

// This code is contributed
// by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to get
// nth Pentagonal
// pyramidal number.

// function to get
// nth Pentagonal
// pyramidal number.

function pentagon_pyramidal($n)
{
    return $n * $n *
          ($n + 1) / 2;
}

// Driver Code
$n = 4;
echo pentagon_pyramidal($n);

// This code is contributed
// by akt_mit
?>
```

## java 描述语言

```
<script>
// javascript Program to get nth
// Pentagonal pyramidal number.

// function to get nth
// Pentagonal pyramidal number.
function pentagon_pyramidal(n)
{
    return n * n *
          (n + 1) / 2;
}

// Driver Code
var n = 4;
document.write(pentagon_pyramidal(n));

// This code is contributed by Princi Singh
</script>
```

**输出:**

```
40
```

**时间复杂度:** O(1)