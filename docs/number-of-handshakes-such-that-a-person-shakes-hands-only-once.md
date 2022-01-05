# 一个人只握手一次的握手次数

> 原文:[https://www . geesforgeks . org/握手次数-一个人只能握手一次/](https://www.geeksforgeeks.org/number-of-handshakes-such-that-a-person-shakes-hands-only-once/)

一个聚会有 N 个人。找出握手的总数，这样一个人只能握手一次。

**示例:**

```
Input : 5
Output : 10

Input : 9
Output : 36 
```

我们可以看到这个问题的递归性质。

```
// n-th person has (n-1) choices and after
// n-th person chooses a person, problem
// recurs for n-1.
handshake(n) = (n-1) + handshake(n-1)

// Base case
handshake(0) = 0 
```

![](img/4cd4a915fca20f1e3c9b71a807d0714b.png)

下面是上面递归公式的实现。

## C++

```
// Recursive C++ program to count total
// number of handshakes when a person
// can shake hand with only one.
#include <bits/stdc++.h>
using namespace std;

// Function to find all possible handshakes
int handshake(int n)
{

    // When n becomes 0 that means all the
    // persons have done handshake with other
    if (n == 0)
        return 0;
    else
        return (n - 1) + handshake(n - 1);
}

// Driver code
int main()
{
    int n = 9;
    cout << " " << handshake(n);
    return 0;
}

// This code is contributed by shivanisinghss2110
```

## C

```
// Recursive C program to count total
// number of  handshakes when a person
// can shake hand with only one.
#include <stdio.h>

// function to find all possible handshakes
int handshake(int n)
{
    // when n becomes 0 that means all the
    // persons have done handshake with other
    if (n == 0)
        return 0;
    else
        return (n - 1) + handshake(n - 1);
}

int main()
{
    int n = 9;
    printf("%d", handshake(n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Recursive Java program to
// count total number of
// handshakes when a person
// can shake hand with only one.
import java.io.*;

class GFG
{

// function to find all
// possible handshakes
static int handshake(int n)
{
    // when n becomes 0 that
    // means all the persons
    // have done handshake
    // with other
    if (n == 0)
        return 0;
    else
        return (n - 1) + handshake(n - 1);
}

// Driver Code
public static void main (String[] args)
{
    int n = 9;
    System.out.print(handshake(n));
}
}

// This code is contributed
// by chandan_jnu
```

## 蟒蛇 3

```
# Recursive Python program
# to count total number of
# handshakes when a person
# can shake hand with only one.

# function to find all
# possible handshakes
def handshake(n):

    # when n becomes 0 that means
    # all the persons have done
    # handshake with other
    if (n == 0):
        return 0
    else:
        return (n - 1) + handshake(n - 1)

# Driver Code
n = 9
print(handshake(n))

# This code is contributed
# by Shivi_Aggarwal
```

## C#

```
// Recursive C# program to
// count total number of
// handshakes when a person
// can shake hand with only one.
using System;

class GFG
{

// function to find all
// possible handshakes
static int handshake(int n)
{
    // when n becomes 0 that
    // means all the persons
    // have done handshake
    // with other
    if (n == 0)
        return 0;
    else
        return (n - 1) + handshake(n - 1);
}

// Driver Code
public static void Main (String []args)
{
    int n = 9;
    Console.WriteLine(handshake(n));
}
}

// This code is contributed
// by Arnab Kundu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Recursive PHP program to 
// count total number of
// handshakes when a person
// can shake hand with only one.

// function to find all
// possible handshakes
function handshake($n)
{
    // when n becomes 0 that means
    // all the persons have done
    // handshake with other
    if ($n == 0)
        return 0;
    else
        return ($n - 1) + handshake($n - 1);
}

// Driver Code
$n = 9;
echo(handshake($n));

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>
      // Recursive JavaScript program to
      // count total number of
      // handshakes when a person
      // can shake hand with only one.
      // function to find all
      // possible handshakes
      function handshake(n) {
        // when n becomes 0 that
        // means all the persons
        // have done handshake
        // with other
        if (n === 0)
          return 0;
        else
          return n - 1 + handshake(n - 1);
      }

      // Driver Code
      var n = 9;
      document.write(handshake(n));
</script>
```

**Output:** 

```
36
```

我们可以通过扩展递归得出一个**直接公式**。

```
handshake(n) = (n-1) + handshake(n-1)
             = (n-1) + (n-2) + handshake(n-2)
             = (n-1) + (n-2) + .... 1 + 0
             = n * (n - 1)/2  
```

## C++

```
// Recursive CPP program to count total
// number of  handshakes when a person
// can shake hand with only one.
#include <stdio.h>

// function to find all possible handshakes
int handshake(int n)
{
   return n * (n - 1)/2;
}

int main()
{
    int n = 9;
    printf("%d", handshake(n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Recursive Java program to
// count total number of
// handshakes when a person
// can shake hand with only one.
class GFG
{

// function to find all
// possible handshakes
static int handshake(int n)
{
    return n * (n - 1) / 2;
}

// Driver code
public static void main(String args[])
{
    int n = 9;
    System.out.println(handshake(n));
}
}

// This code is contributed
// by Arnab Kundu
```

## 蟒蛇 3

```
# Recursive Python program
# to count total number of
# handshakes when a person
# can shake hand with only one.

# function to find all
# possible handshakes
def handshake(n):

    return int(n * (n - 1) / 2)

# Driver Code
n = 9
print(handshake(n))

# This code is contributed
# by Shivi_Aggarwal
```

## C#

```
// Recursive C# program to
// count total number of
// handshakes when a person
// can shake hand with only one.
using System;

class GFG
{

// function to find all
// possible handshakes
static int handshake(int n)
{
    return n * (n - 1) / 2;
}

// Driver code
static public void Main ()
{
    int n = 9;
    Console.WriteLine(handshake(n));
}
}

// This code is contributed by Sachin
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Recursive PHP program to
// count total number of
// handshakes when a person
// can shake hand with only one.

// function to find all
// possible handshakes
function handshake($n)
{
    return $n * ($n - 1) / 2;
}

// Driver Code
$n = 9;
echo(handshake($n));

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// Recursive Javascript program to
// count total number of
// handshakes when a person
// can shake hand with only one.

// Function to find all
// possible handshakes
function handshake(n)
{
    return n * parseInt((n - 1) / 2, 10);
}

// Driver code
let n = 9;

document.write(handshake(n));

// This code is contributed by rameshtravel07

</script>
```

**Output:** 

```
36
```