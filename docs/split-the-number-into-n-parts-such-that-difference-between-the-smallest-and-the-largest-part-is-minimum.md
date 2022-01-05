# 将数字分成 N 个部分，使得最小部分和最大部分之间的差值最小

> 原文:[https://www . geesforgeks . org/将数字拆分成 n 个部分，这样最小部分和最大部分之间的差异最小/](https://www.geeksforgeeks.org/split-the-number-into-n-parts-such-that-difference-between-the-smallest-and-the-largest-part-is-minimum/)

给定两个整数“X”和“N”，任务是将整数“X”精确地分成“N”个部分，使得:
X1 + X2 + X3 + … + Xn = X，并且序列中最大值和最小值之间的差值最小。
最后打印序列，如果数字不能精确地分成“N”个部分，则打印“-1”。

**示例:**

> **输入:** X = 5，N = 3
> **输出:** 1 2 2
> 将 5 分成 3 份，使得
> 中最大和最小的整数之差尽可能小。所以我们把 5 除以 1 + 2 + 2。
> 
> **输入:** X = 25，N = 5
> T3】输出:5 5 5 5 5 5

**方法:**如果 X > = N，总有一种拆分数字的方法

*   如果数字被精确地分成“N”个部分，那么每个部分都将具有 X/N 值，而剩余的 X%N 部分可以分布在任何 X%N 个数字中。
*   因此，如果 X % N == 0，那么最小差值将总是“0”，并且序列将包含所有相等的数字，即 x/n
*   否则，差将是“1”，序列将是 X/N，X/N，…，(X/N)+1，(X/N)+1..

下面是上述方法的实现:

## C++

```
// CPP implementation of the approach
#include<bits/stdc++.h>
using namespace std;;

// Function that prints
// the required sequence
void split(int x, int n)
{

// If we cannot split the
// number into exactly 'N' parts
if(x < n)
cout<<"-1"<<" ";

    // If x % n == 0 then the minimum
    // difference is 0 and all
    // numbers are x / n
    else if (x % n == 0)
    {
        for(int i=0;i<n;i++)
        cout<<(x/n)<<" ";
    }
    else
    {

        // upto n-(x % n) the values
        // will be x / n
        // after that the values
        // will be x / n + 1
        int zp = n - (x % n);
        int pp = x/n;
        for(int i=0;i<n;i++)
        {

            if(i>= zp)
            cout<<(pp + 1)<<" ";
            else
            cout<<pp<<" ";
        }
    }
}

// Driver code
int main()
{

int x = 5;
int n = 3;
split(x, n);

}
//THis code is contributed
// Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG{
// Function that prints
// the required sequence
static void split(int x, int n)
{

// If we cannot split the
// number into exactly 'N' parts
if(x < n)
System.out.print("-1 ");

    // If x % n == 0 then the minimum
    // difference is 0 and all
    // numbers are x / n
    else if (x % n == 0)
    {
        for(int i=0;i<n;i++)
        System.out.print((x/n)+" ");
    }
    else
    {

        // upto n-(x % n) the values
        // will be x / n
        // after that the values
        // will be x / n + 1
        int zp = n - (x % n);
        int pp = x/n;
        for(int i=0;i<n;i++)
        {

            if(i>= zp)
            System.out.print((pp + 1)+" ");
            else
            System.out.print(pp+" ");
        }
    }
}

// Driver code
public static void main(String[] args)
{

int x = 5;
int n = 3;
split(x, n);

}
}
//This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that prints
# the required sequence
def split(x, n):

    # If we cannot split the
    # number into exactly 'N' parts
    if(x < n):
        print(-1)

    # If x % n == 0 then the minimum
    # difference is 0 and all
    # numbers are x / n
    elif (x % n == 0):
        for i in range(n):
            print(x//n, end =" ")
    else:
        # upto n-(x % n) the values
        # will be x / n
        # after that the values
        # will be x / n + 1
        zp = n - (x % n)
        pp = x//n
        for i in range(n):
            if(i>= zp):
                print(pp + 1, end =" ")
            else:
                print(pp, end =" ")

# Driver code         
x = 5
n = 3
split(x, n)
```

## C#

```
// C# implementation of the approach
using System;

public class GFG{
    // Function that prints
// the required sequence
static void split(int x, int n)
{

// If we cannot split the
// number into exactly 'N' parts
if(x < n)
Console.WriteLine("-1 ");

    // If x % n == 0 then the minimum
    // difference is 0 and all
    // numbers are x / n
    else if (x % n == 0)
    {
        for(int i=0;i<n;i++)
    Console.Write((x/n)+" ");
    }
    else
    {

        // upto n-(x % n) the values
        // will be x / n
        // after that the values
        // will be x / n + 1
        int zp = n - (x % n);
        int pp = x/n;
        for(int i=0;i<n;i++)
        {

            if(i>= zp)
            Console.Write((pp + 1)+" ");
            else
            Console.Write(pp+" ");
        }
    }
}

// Driver code
static public void Main (){

int x = 5;
int n = 3;
split(x, n);

}
}
//This code is contributed by Sachin.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function that prints
// the required sequence
function split($x, $n)
{
    // If we cannot split the
    // number into exactly 'N' parts
    if($x < $n)
        echo (-1);

    // If x % n == 0 then the minimum
    // difference is 0 and all
    // numbers are x / n
    else if ($x % $n == 0)
    {
        for($i = 0; $i < $n; $i++)
        {
            echo ($x / $n);
            echo (" ");
        }
    }

    else
    {
        // upto n-(x % n) the values
        // will be x / n
        // after that the values
        // will be x / n + 1
        $zp = $n - ($x % $n);
        $pp = $x / $n;
        for ($i = 0; $i < $n; $i++)
        {
            if($i >= $zp)
            {
                echo (int)$pp + 1;
                echo (" ");
            }
            else
            {
                echo (int)$pp;
                echo (" ");
            }
        }
    }
}

// Driver code    
$x = 5;
$n = 3;
split( $x, $n);

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach

// Function that prlets
// the required sequence
function split(x, n)
{

// If we cannot split the
// number into exactly 'N' parts
if(x < n)
document.write("-1 ");

    // If x % n == 0 then the minimum
    // difference is 0 and all
    // numbers are x / n
    else if (x % n == 0)
    {
        for(let i=0;i<n;i++)
        document.write((x/n)+" ");
    }
    else
    {

        // upto n-(x % n) the values
        // will be x / n
        // after that the values
        // will be x / n + 1
        let zp = n - (x % n);
        let pp = Math.floor(x/n);
        for(let i=0;i<n;i++)
        {

            if(i>= zp)
            document.write((pp + 1)+" ");
            else
            document.write(pp+" ");
        }
    }
}

// driver code

        let x = 5;
        let n = 3;
        split(x, n);

</script>
```

**Output:** 

```
1 2 2
```