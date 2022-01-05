# 寻找第 n 个幻数

> 原文:[https://www.geeksforgeeks.org/find-nth-magic-number/](https://www.geeksforgeeks.org/find-nth-magic-number/)

幻数被定义为可以表示为 5 的幂或 5 的唯一幂之和的数。前几个神奇的数字是 5，25，30(5 + 25)，125，130(125 + 5)，…。
写函数求第 n 个幻数。
示例:

```
Input: n = 2
Output: 25

Input: n = 5
Output: 130 
```

如果我们仔细注意，幻数可以表示为 001、010、011、100、101、110 等，其中 001 是 0 *幂(5，3)+0 *幂(5，2)+1 *幂(5，1)。所以基本上我们需要给定整数 n 中的每一个位集加 5 的幂。
下面是基于这个思想的实现。

## C++

```
// C++ program to find nth magic number
#include <bits/stdc++.h>
using namespace std;

// Function to find nth magic number
int nthMagicNo(int n)
{
    int pow = 1, answer = 0;

    // Go through every bit of n
    while (n)
    {
       pow = pow*5;

       // If last bit of n is set
       if (n & 1)
         answer += pow;

       // proceed to next bit
       n >>= 1;  // or n = n/2
    }
    return answer;
}

// Driver program to test above function
int main()
{
    int n = 5;
    cout << "nth magic number is " << nthMagicNo(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find nth
// magic number
import java.io.*;

class GFG
{
  // Function to find nth magic number
  static int nthMagicNo(int n)
  {
     int pow = 1, answer = 0;

     // Go through every bit of n
     while (n != 0)
     {
       pow = pow*5;

       // If last bit of n is set
       if ((int)(n & 1) == 1)
         answer += pow;

       // proceed to next bit
       // or n = n/2
       n >>= 1; 
     }
     return answer;
  }

  // Driver program to test
  // above function
  public static void main(String[] args)
  {
    int n = 5;
    System.out.println("nth magic" +
    " number is " + nthMagicNo(n));
  }
}

// This code is contributed by
// prerna saini
```

## 蟒蛇 3

```
# Python program to find nth magic number

# Function to find nth magic number
def nthMagicNo(n):

    pow = 1
    answer = 0

    # Go through every bit of n
    while (n):

        pow = pow*5

        # If last bit of n is set
        if (n & 1):
            answer += pow

        # proceed to next bit
        n >>= 1 # or n = n/2

    return answer

# Driver program to test above function
n = 5
print("nth magic number is", nthMagicNo(n))

# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// C# program to find nth
// magic number
using System;

public class GFG
{

// Function to find nth magic number
static int nthMagicNo(int n)
{
    int pow = 1, answer = 0;

    // Go through every bit of n
    while (n != 0)
    {
        pow = pow * 5;

        // If last bit of n is set
        if ((int)(n & 1) == 1)
            answer += pow;

        // proceed to next bit
        // or n = n/2
        n >>= 1;
    }
    return answer;
}

// Driver Code
public static void Main()
{
    int n = 5;
    Console.WriteLine("nth magic" +    " number is "
                       + nthMagicNo(n));

}
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find nth
// magic number

// Function to find nth
// magic number
function nthMagicNo($n)
{
    $pow = 1;
    $answer = 0;

    // Go through every bit of n
    while ($n)
    {
    $pow = $pow * 5;

    // If last bit of n is set
    if ($n & 1)
        $answer += $pow;

    // proceed to next bit
    $n >>= 1; // or $n = $n/2
    }
    return $answer;
}

// Driver Code
$n = 5;
echo "nth magic number is ",
       nthMagicNo($n), "\n";

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

    // Javascript program to find nth
    // magic number

    // Function to find nth magic number
    function nthMagicNo(n)
    {
        let pow = 1, answer = 0;

        // Go through every bit of n
        while (n != 0)
        {
            pow = pow * 5;

            // If last bit of n is set
            if ((n & 1) == 1)
                answer += pow;

            // proceed to next bit
            // or n = n/2
            n >>= 1;
        }
        return answer;
    }

    let n = 5;
    document.write("nth magic" + " number is " + nthMagicNo(n));

</script>
```

**输出:**

```
 nth magic number is 130 
```

感谢曼拉辛格提出上述解决方案。

本文由 **Abhay** 供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。