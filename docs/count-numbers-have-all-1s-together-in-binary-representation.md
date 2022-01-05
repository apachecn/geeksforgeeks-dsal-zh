# 计数数字在二进制表示中全部为 1

> 原文:[https://www . geesforgeks . org/count-numbers-have-all-1s-together-in-binary-presentation/](https://www.geeksforgeeks.org/count-numbers-have-all-1s-together-in-binary-representation/)

给定一个整数 **n** ，任务是计算小于或等于 n 的幸运数字的总数。如果一个数字从一开始就有二进制表示的 1 的所有传染数，则称它是幸运的。例如，1、3、7、15 是幸运数字，2、5 和 9 不是幸运数字。
**例:**

```
Input :n = 7 
Output :3
1, 3 and 7 are lucky numbers

Input :n = 17
Output :4
```

**方法:**一种方法是首先找出每个数的二进制表示，然后检查每个数的 1 的传染数，但是这种方法很耗时，并且可以给出 **tle** 如果约束是两个大的，通过观察这些数可以找出有效的方法，我们可以说每个带有幸运数的**可以通过公式 **2 <sup>i</sup> -1** 找到，通过迭代一个循环直到小于等于 n 的数我们可以找到
**以下是上述方法的实施**** 

## 卡片打印处理机（Card Print Processor 的缩写）

```
#include <bits/stdc++.h>
using namespace std;

int countLuckyNum(int n)
{
    int count = 0, i = 1;

    while (1) {
        if (n >= ((1 << i) - 1))
            count++;
        else
            break;
        i++;
    }

    return count;
}

// Driver code
int main()
{
    int n = 7;
    cout << countLuckyNum(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;
import java.lang.*;
import java.io.*;

public class GFG {

    // Function to return the count of lucky number
    static int countLuckyNum(int n)
    {

        int count = 0, i = 1;
        while (true) {
            if (n >= ((1 << i) - 1))
                count++;
            else
                break;
            i++;
        }
        return count;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 7;
        System.out.println(countLuckyNum(n));
    }
}
```

## 计算机编程语言

```
# python3 code of above problem

# function to count the lucky number

def countLuckyNum(n):

    count, i = 0, 1

    while True:
        if n>= 2**i-1:
            count+= 1
        else:
            break
        i+= 1;
    return count    

# driver code
n = 7

print(countLuckyNum(n))
```

## C#

```
// C# implementation of the approach
using System;

public class GFG {

    // Function to return the count of lucky number
    static int countLuckyNum(int n)
    {

        int count = 0, i = 1;
        while (true) {
            if (n >= ((1 << i) - 1))
                count++;
            else
                break;
            i++;
        }
        return count;
    }

    // Driver code
    public static void Main()
    {
        int n = 7;
        Console.WriteLine(countLuckyNum(n));
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to count the lucky number
function countLuckyNum($n)  
{  

  $count = 0;
  $i = 1;

  while(1)
  {
      if ($n >= ((1 << $i) - 1))
        $count += 1;
      else
        break;
      $i += 1;
  }
  return $count;                    
}  

// Driver code  
$n = 7;
echo countLuckyNum($n) ;  
?>
```

## java 描述语言

```
<script>

    // Function to return the count of lucky number
    function countLuckyNum(n) {

        var count = 0, i = 1;
        while (true) {
            if (n >= ((1 << i) - 1))
                count++;
            else
                break;
            i++;
        }
        return count;
    }

    // Driver code
    var n = 7;
    document.write(countLuckyNum(n));

// This code is contributed by aashish1995
</script>
```

```
output:3
```