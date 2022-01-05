# 找出能被 D 整除的 N 位数

> 原文:[https://www . geesforgeks . org/find-n-digits-number-可被 d 整除/](https://www.geeksforgeeks.org/find-n-digits-number-which-is-divisible-by-d/)

给定![N ](img/479cbec0e01453d6ddc99e257783bb88.png "Rendered by QuickLaTeX.com")和![D](img/4bf58c30470f92164b71a158e9fd8b22.png "Rendered by QuickLaTeX.com")。任务是找到一个能被 D 整除的 N 位数(2 < = D < = 10)。如果不可能，则打印不可能。

**示例**:

```
Input : N = 2 and D = 2
Output : 20

Input : N = 1 and D = 10
Output : Impossible
```

**进场:**有两个条件，D=10，D 不等于 10。如果 D = 10，N = 1，那么唯一的答案是不可能的，在所有其他条件下，答案都是可能的。

```
1\. If D is 10,
   Print 1 followed by n-1 times zero.
2\. If D is not 10
   Print D followed by n-1 times zero
```

下面是上述方法的实现:

## C++

```
// CPP program to Find N digits
// number which is divisible by D
#include <bits/stdc++.h>
using namespace std;

// Function to return N digits
// number which is divisible by D
string findNumber(int n, int d)
{
    // to store answer
    string ans = "";

    if (d != 10) {
        ans += to_string(d);
        for (int i = 1; i < n; i++)
            ans += '0';
    }
    else {
        if (n == 1)
            ans += "Impossible";
        else {
            ans += '1';
            for (int i = 1; i < n; i++)
                ans += '0';
        }
    }

    return ans;
}

// Driver code
int main()
{
    int n = 12, d = 3;

    cout << findNumber(n, d);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Find N digits
// number which is divisible by D

import java.io.*;

class GFG {

// Function to return N digits
// number which is divisible by D
static String findNumber(int n, int d)
{
    // to store answer
    String ans = "";

    if (d != 10) {
        ans += Integer.toString(d);
        for (int i = 1; i < n; i++)
            ans += '0';
    }
    else {
        if (n == 1)
            ans += "Impossible";
        else {
            ans += '1';
            for (int i = 1; i < n; i++)
                ans += '0';
        }
    }

    return ans;
}

// Driver code

    public static void main (String[] args) {
            int n = 12, d = 3;

    System.out.println(findNumber(n, d));
    }
}
// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python 3 program to Find N digits
# number which is divisible by D

# Function to return N digits
# number which is divisible by D
def findNumber(n, d):

    # to store answer
    ans = ""

    if (d != 10) :
        ans += str(d)
        for i in range(1,n):
            ans += '0'
    else :
        if (n == 1):
            ans += "Impossible"
        else :
            ans += '1'
            for i in range(1,n):
                ans += '0'

    return ans

# Driver code
if __name__ == "__main__":
    n = 12
    d = 3

    print(findNumber(n, d))

# This code is contributed by
# ChitraNayal
```

## C#

```
// C# program to Find N digits
// number which is divisible by D
using System;

class GFG {

// Function to return N digits
// number which is divisible by D
static string findNumber(int n, int d)
{

    // to store answer
    string ans = "";

    if (d != 10) {

        ans += d.ToString();

        for (int i = 1; i < n; i++)
            ans += '0';
    }

    else {

        if (n == 1)
            ans += "Impossible";

        else {

            ans += '1';
            for (int i = 1; i < n; i++)
                ans += '0';
        }
    }

    return ans;
}

// Driver code
public static void Main ()
{

    int n = 12, d = 3;
    Console.WriteLine(findNumber(n, d));
}
}

// This code is contributed by Subhadeep
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to Find N digits
// number which is divisible by D

// Function to return N digits
// number which is divisible by D
function findNumber($n, $d)
{
    // to store answer
    $ans = "";

    if ($d != 10)
    {
        $ans .= strval($d);
        for($i = 1; $i < $n; $i++)
            $ans .= '0';
    }
    else
    {
        if (n == 1)
            $ans .= "Impossible";
        else
            $ans .= '1';
            for($i = 1; $i < $n; $i++)
                $ans .= '0';
    }

    return $ans;
}

// Driver code
$n = 12;
$d = 3;

print(findNumber($n, $d));

// This code is contributed by mits
```

## java 描述语言

```
<script>
// Javascript program to Find N digits
// number which is divisible by D

// Function to return N digits
// number which is divisible by D
  function findNumber(n,d)
  {
        // to store answer
    let ans = "";

    if (d != 10) {
        ans += (d).toString();
        for (let i = 1; i < n; i++)
            ans += '0';
    }
    else {
        if (n == 1)
            ans += "Impossible";
        else {
            ans += '1';
            for (let i = 1; i < n; i++)
                ans += '0';
        }
      }

      return ans;
  }

  // Driver code
  let n = 12, d = 3;
  document.write(findNumber(n, d));

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
300000000000
```