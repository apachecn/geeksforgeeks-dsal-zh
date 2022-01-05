# 从 1 到 N 选择包含偶数和奇数的配对的方式数

> 原文:[https://www . geesforgeks . org/从 1 到 n 选择一对包含一个偶数和一个奇数的路数/](https://www.geeksforgeeks.org/number-of-ways-to-choose-a-pair-containing-an-even-and-an-odd-number-from-1-to-n/)

给定一个数字 N，任务是从 1 到 N(含 1 和 N)之间的数字中找出包含偶数和奇数的对的数量。
**注:**对中数字的顺序无关紧要。即(1，2)和(2，1)是相同的。

**示例**:

```
Input: N = 3
Output: 2
The pairs are (1, 2) and (2, 3).

Input: N = 6
Output: 9
The pairs are (1, 2), (1, 4), (1, 6), (2, 3),
(2, 5), (3, 4), (3, 6), (4, 5), (5, 6). 
```

**方式:**成对的方式数为**(偶数总数*奇数总数)**。
如此

1.  如果 N 是偶数=奇数= N/2
2.  如果 N 是奇数，偶数= N/2，奇数= N/2+1

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <iostream>
using namespace std;

// Driver code
int main()
{
  int N = 6;

  int Even = N / 2 ;

  int Odd = N - Even ;

  cout << Even * Odd ;

  return 0;
  // This code is contributed
  // by ANKITRAI1
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;
import java.lang.*;
import java.io.*;
class GFG{

// Driver code
public static void main(String args[])
{
  int N = 6;

  int Even = N / 2 ;

  int Odd = N - Even ;

  System.out.println( Even * Odd );

}
}
```

## 蟒蛇 3

```
# Python implementation of the above approach
N = 6

 # number of even numbers
Even = N//2

# number of odd numbers
Odd = N-Even
print(Even * Odd)
```

## C#

```
// C# implementation of the
// above approach
using System;

class GFG
{

// Driver code
public static void Main()
{
    int N = 6;

    int Even = N / 2 ;

    int Odd = N - Even ;

    Console.WriteLine(Even * Odd);
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the
// above approach

// Driver code
$N = 6;

$Even = $N / 2 ;

$Odd = $N - $Even ;

echo $Even * $Odd ;

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach   

    // Driver code
    let N = 6;

      let Even = Math.floor(N / 2) ;

      let Odd = N - Even ;

     document.write( Even * Odd );

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
9
```