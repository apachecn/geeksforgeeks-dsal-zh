# 用 2 的幂计算模数除法

> 原文:[https://www . geesforgeks . org/compute-module-除以 2 的幂次数/](https://www.geeksforgeeks.org/compute-modulus-division-by-a-power-of-2-number/)

不使用除法(/)和模(%)运算符计算 n 模 d，其中 d 是 2 的幂。
让 *i* 从右数第几位设置为 d，为了得到 n 个模 d，我们只需要将 0 返回到 *i* -1(从右数)位，其他位为 0。
例如，如果 n = 6 (00..110)和 d = 4(00..100).d 中的最后一个设置位在位置 3(从右侧)。因此，我们需要返回 n 的最后两位，其他位为 0，即 00..010.
现在做起来好容易，猜猜看。
是的，你猜对了。请看下面的程序。

## C++

```
#include<iostream>
using namespace std;
// This function will return n % d.
// d must be one of: 1, 2, 4, 8, 16, 32, …
unsigned int getModulo(unsigned int n,
                       unsigned int d)
{
  return ( n & (d - 1) );
}        

// Driver Code
int main()
{
  unsigned int n = 6;

  // d must be a power of 2
  unsigned int d = 4;
  cout<< n <<" moduo "<<d <<" is "<< getModulo(n, d);

  getchar();
  return 0;
}    

// this code is contributed by shivanisinghss2110
```

## C

```
#include<stdio.h>

// This function will return n % d.
// d must be one of: 1, 2, 4, 8, 16, 32, …
unsigned int getModulo(unsigned int n,
                       unsigned int d)
{
return ( n & (d - 1) );
}        

// Driver Code
int main()
{
unsigned int n = 6;

// d must be a power of 2
unsigned int d = 4;
printf("%u moduo %u is %u", n, d, getModulo(n, d));

getchar();
return 0;
}    
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for Compute modulus division by
// a power-of-2-number
class GFG {

    // This function will return n % d.
    // d must be one of: 1, 2, 4, 8, 16, 32,
    static int getModulo(int n, int d)
    {
        return ( n & (d-1) );
    }    

    // Driver Code
    public static void main(String[] args)
    {
        int n = 6;

        /*d must be a power of 2*/
        int d = 4;

        System.out.println(n+" moduo " + d +
                    " is " + getModulo(n, d));
    }
}

// This code is contributed
// by Smitha Dinesh Semwal.
```

## 蟒蛇 3

```
# Python code to demonstrate
# modulus division by power of 2

# This function will
# return n % d.
# d must be one of:
# 1, 2, 4, 8, 16, 32, …
def getModulo(n, d):

    return ( n & (d-1) )

# Driver program to
# test above function
n = 6

#d must be a power of 2
d = 4
print(n,"moduo",d,"is",
      getModulo(n, d))

# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// C# code for Compute modulus
// division by a power-of-2-number
using System;

class GFG {

// This function will return n % d.
// d must be one of: 1, 2, 4, 8, 16, 32, …
static uint getModulo( uint n, uint d)
{
return ( n & (d-1) );
}    

// Driver code
static public void Main ()
   {
    uint n = 6;
    uint d = 4; /*d must be a power of 2*/

    Console.WriteLine( n + " moduo " + d +
                " is " + getModulo(n, d));

    }
}
// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// This function will return n % d.
// d must be one of: 1, 2, 4, 8, 16, 32, …
function getModulo($n, $d)
{
return ( $n & ($d - 1) );
}    

// Driver Code
$n = 6;

// d must be a power of 2
$d = 4;
echo $n ," moduo"," ", $d, " is ",
         " ",getModulo($n, $d);

// This code is contributed by vt_m.
?>
```

## java 描述语言

```
<script>
// This function will return n % d.
// d must be one of: 1, 2, 4, 8, 16, 32, …
function getModulo(n,d)
{
    return ( n & (d - 1) );
}        

// Driver Code
 n = 6;
 d = 4;

document.write(n  +" moduo "+ d + " is "+ getModulo(n, d));

  // This code is contributed by simranarora5sos
</script>
```

**输出:**

```
6 moduo 4 is 2
```

时间复杂度:0(1)

辅助空间:0(1)

[https://www.youtube.com/watch?v=fSjW-wDghTs](https://www.youtube.com/watch?v=fSjW-wDghTs)T2】

**参考文献:**
[http://graphics . Stanford . edu/~ seander/bithacks . html # modulusivisioneasy](http://graphics.stanford.edu/~seander/bithacks.html#ModulusDivisionEasy)
如发现上述程序/算法有任何 bug 或其他方法解决同样问题，请写评论。