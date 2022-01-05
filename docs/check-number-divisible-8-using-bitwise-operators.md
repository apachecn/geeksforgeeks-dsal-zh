# 使用按位运算符

检查一个数是否能被 8 整除

> 原文:[https://www . geesforgeks . org/check-number-divide-8-use-bitwise-operator/](https://www.geeksforgeeks.org/check-number-divisible-8-using-bitwise-operators/)

给定一个数字 n，使用按位运算符检查它是否能被 8 整除。
示例:

```
Input : 16
Output :YES

Input :15
Output :NO
```

**方法:**结果=((n>>3)<<3)= = n。首先，我们向右移动 3 位，然后向左移动 3 位，然后将该数与给定的数进行比较，如果该数等于该数，则该数可被 8 整除。
**解释:**
举例:n = 16 给定二进制数 16 的二进制数是 10000 现在我们向右移动 3 位，现在我们有 00010 所以我们再次向左移动 3 位，然后我们有 10000 现在与给定的数进行比较第一个二进制数 16==16 所以它为真所以这个数可以被 8 整除。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to check whether
// the number is divisible by
// 8 or not using bitwise operator
#include <bits/stdc++.h>
using namespace std;

// function to check number is
// div by 8 or not using bitwise
// operator
int Div_by_8(int n)
{
    return (((n >> 3) << 3) == n);
}

// Driver program
int main()
{
    int n = 16;
    if (Div_by_8(n))
        cout << "YES" << endl;
    else
        cout << "NO" << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check whether
// the number is divisible by
// 8 or not using bitwise operator
import java.io.*;
import java.util.*;

class GFG
{
    // function to check number is
    // div by 8 or not using bitwise
    // operator
    static boolean Div_by_8(int n)
    {
        return (((n >> 3) << 3) == n);
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 16;
        if (Div_by_8(n))
            System.out.println("YES");
        else
            System.out.println("NO");

    }
}

// This code is contributed by  Gitanjali
```

## 蟒蛇 3

```
# Python  program to check whether
# the number is divisible by
# 8 or not using bitwise operator

import math

# function to check number is
# div by 8 or not using bitwise
# operator

def Div_by_8(n):

    return (((n >> 3) << 3) == n)

#  driver code
n = 16
if (Div_by_8(n)):
    print("YES")
else:
    print("NO")

# This code is contributed by Gitanjali.
```

## C#

```
// C# program to check whether         
// the number is divisible by         
// 8 or not using bitwise operator         
using System;         
class GFG {         

 // function to check number is         
 // div by 8 or not using bitwise         
 // operator         
 static bool Div_by_8(int n)         
 {         
 return (((n >> 3) << 3) == n);         
 }         

 // Driver code         
 public static void Main ()          
 {         
 int n = 16;         

 if (Div_by_8(n))         
 Console.WriteLine("YES");         
 else         
 Console.WriteLine("NO");         

 }         
}    

// This code is contributed by vt_m.         
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check whether
// the number is divisible by
// 8 or not using bitwise operator

// function to check number is
// div by 8 or not using bitwise
// operator
function Div_by_8($n)
{
    return ((($n >> 3) << 3) == $n);
}

// Driver program
$n = 16;

if (Div_by_8($n))
    echo "YES";
else
    echo "NO";

//This code is contributed by mits.
?>
```

## java 描述语言

```
<script>
// javascript program to check whether
// the number is divisible by
// 8 or not using bitwise operator

// function to check number is
// div by 8 or not using bitwise
// operator
function Div_by_8(n)
{
    return (((n >> 3) << 3) == n);
}

// Driver code

var n = 16;
if (Div_by_8(n))
    document.write("YES");
else
    document.write("NO");

// This code is contributed by Princi Singh.
</script>
```

```
YES
```