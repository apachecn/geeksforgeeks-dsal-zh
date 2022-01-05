# 在不使用任何比较运算符的情况下比较两个整数

> 原文:[https://www . geesforgeks . org/compare-two-integer-not-use-comparison-operator/](https://www.geeksforgeeks.org/compare-two-integers-without-using-comparison-operator/)

给定两个整数 A 和 B。任务是在不使用比较运算符的情况下检查 A 和 B 是否相同。
**例:**

```
Input : A = 5 , B = 6
Output : 0

Input : A = 5 , B = 5 
Output : 1

Note : 1 = "YES" and 0 = "NO"
```

想法很简单，我们对两个元素(A，B)进行异或运算。如果 Xor 为零，则两个数相等，否则不相等。
以下是上述思路的实现:

## C++

```
// C++ program to compare two integers without
// any comparison operator.
#include<bits/stdc++.h>
using namespace std;

// function return true if A ^ B > 0  else false
bool EqualNumber(int A, int B)
{
   return ( A ^ B ) ;
}

// Driver program
int main()
{
  int A = 5 , B = 6;
  cout << !EqualNumber(A, B) << endl;
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to compare two integers without
// any comparison operator.
import java.util.*;

class solution
{

// function return true if A ^ B > 0 else false
static boolean EqualNumber(int A, int B)
{

  if ((A^B) != 0)
   return true;
  else
   return false;
}

// Driver program
public static void main(String args[])
{
int A = 5 , B = 6;
if(EqualNumber(A, B) == false)
 System.out.println(1);
else
 System.out.println(0);

}
}
// This code is contributed by
// Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 program to compare two integers
# without any comparison operator.

# Function return true if
# A ^ B > 0 else false
def EqualNumber(A, B):

    return ( A ^ B )

# Driver Code
A = 5; B = 6
print(int(not(EqualNumber(A, B))))

# This code is contributed by Smitha Dinesh Semwal.
```

## C#

```
// C# program to compare two integers
// without any comparison operator.
using System;

class GFG
{
// function return true if
// A ^ B > 0 else false
static bool EqualNumber(int A, int B)
{
    if(( A ^ B ) > 0)
        return true;
    else
        return false;
}

// Driver Code
public static void Main()
{
    int A = 5 , B = 6;
    if(!EqualNumber(A, B) == false)
        Console.WriteLine("0");
    else
        Console.WriteLine("1");
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to compare two integers
// without any comparison operator.

// function return true if
// A ^ B > 0 else false
function EqualNumber($A, $B)
{
return ( $A ^ $B ) ;
}

// Driver Code
$A = 5 ;
$B = 6;
echo ((int)!(EqualNumber($A, $B))) . "\n";

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// JavaScript program to compare two integers without
// any comparison operator.

// function return true if A ^ B > 0 else false
function EqualNumber(A, B)
{
return ( A ^ B ) ;
}

// Driver program

let A = 5 , B = 6; 
if(!EqualNumber(A, B) == false)
    document.write("0"); 
else
    document.write("1"); 

// This code is contributed by Surbhi Tyagi.

</script>
```

**输出:**

```
0
```

参考:[http://stackoverflow . com/questions/476800/comparison-two-integer-not-comparison](http://stackoverflow.com/questions/476800/comparing-two-integers-without-any-comparison)
本文由 [**尼尚·辛格**](https://practice.geeksforgeeks.org/user-profile.php?user=_code) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。