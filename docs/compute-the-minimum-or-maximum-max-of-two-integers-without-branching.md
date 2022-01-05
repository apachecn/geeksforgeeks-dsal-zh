# 计算两个无分支整数的最小值或最大值

> 原文:[https://www . geeksforgeeks . org/计算无分支的两个整数的最小值或最大值/](https://www.geeksforgeeks.org/compute-the-minimum-or-maximum-max-of-two-integers-without-branching/)

在一些稀有的机器上，分支是昂贵的，下面明显的寻找最小值的方法可能很慢，因为它使用分支。

## C

```
/* The obvious approach to find minimum (involves branching) */
int min(int x, int y)
{
  return (x < y) ? x : y
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* The obvious approach to find minimum (involves branching) */
static int min(int x, int y)
{
  return (x < y) ? x : y;
}

// This code is contributed by rishavmahato348.
```

## 蟒蛇 3

```
# The obvious approach to find minimum (involves branching)
def min(x, y):
    return x if x < y else y

  # This code is contributed by subham348.
```

## C#

```
/* The obvious approach to find minimum (involves branching) */
static int min(int x, int y)
{
  return (x < y) ? x : y;
}

// This code is contributed by rishavmahato348.
```

## java 描述语言

```
<script>

/* The obvious approach to find minimum (involves branching) */
function min(x, y)
{
  return (x < y) ? x : y;
}

// This code is contributed by subham348.
</script>
```

以下是不使用分支获得最小值(或最大值)的方法。通常，最明显的方法是最好的。

**方法 1(使用异或和比较运算符)**
x 和 y 的最小值将为

```
y ^ ((x ^ y) & -(x < y))
```

它之所以有效，是因为如果 x < y，那么-(x < y)将是-1，也就是全 1(11111…)，所以 r = y ^((x ^ y)&(111111…)= y ^ x ^ y = x。

如果 x>y，那么-(x

在某些机器上，评估(x < y) as 0 or 1 requires a branch instruction, so there may be no advantage.
要找到最大值，请使用

```
x ^ ((x ^ y) & -(x < y));
```

## C++

```
// C++ program to Compute the minimum
// or maximum of two integers without
// branching
#include<iostream>
using namespace std;

class gfg
{

    /*Function to find minimum of x and y*/
    public:
    int min(int x, int y)
    {
        return y ^ ((x ^ y) & -(x < y));
    }

    /*Function to find maximum of x and y*/
    int max(int x, int y)
    {
        return x ^ ((x ^ y) & -(x < y));
    }
    };

    /* Driver code */
    int main()
    {
        gfg g;
        int x = 15;
        int y = 6;
        cout << "Minimum of " << x <<
             " and " << y << " is ";
        cout << g. min(x, y);
        cout << "\nMaximum of " << x <<
                " and " << y << " is ";
        cout << g.max(x, y);
        getchar();
    }

// This code is contributed by SoM15242
```

## C

```
// C program to Compute the minimum
// or maximum of two integers without
// branching
#include<stdio.h>

/*Function to find minimum of x and y*/
int min(int x, int y)
{
return y ^ ((x ^ y) & -(x < y));
}

/*Function to find maximum of x and y*/
int max(int x, int y)
{
return x ^ ((x ^ y) & -(x < y));
}

/* Driver program to test above functions */
int main()
{
int x = 15;
int y = 6;
printf("Minimum of %d and %d is ", x, y);
printf("%d", min(x, y));
printf("\nMaximum of %d and %d is ", x, y);
printf("%d", max(x, y));
getchar();
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Compute the minimum
// or maximum of two integers without
// branching
public class AWS {

    /*Function to find minimum of x and y*/
    static int min(int x, int y)
    {
    return y ^ ((x ^ y) & -(x << y));
    }

    /*Function to find maximum of x and y*/
    static int max(int x, int y)
    {
    return x ^ ((x ^ y) & -(x << y));
    }

    /* Driver program to test above functions */
    public static void main(String[] args) {

        int x = 15;
        int y = 6;
        System.out.print("Minimum of "+x+" and "+y+" is ");
        System.out.println(min(x, y));
        System.out.print("Maximum of "+x+" and "+y+" is ");
        System.out.println( max(x, y));
    }

}
```

## 蟒蛇 3

```
# Python3 program to Compute the minimum
# or maximum of two integers without
# branching

# Function to find minimum of x and y

def min(x, y):

    return y ^ ((x ^ y) & -(x < y))

# Function to find maximum of x and y
def max(x, y):

    return x ^ ((x ^ y) & -(x < y))

# Driver program to test above functions
x = 15
y = 6
print("Minimum of", x, "and", y, "is", end=" ")
print(min(x, y))
print("Maximum of", x, "and", y, "is", end=" ")
print(max(x, y))

# This code is contributed
# by Smitha Dinesh Semwal
```

## C#

```
using System;

// C# program to Compute the minimum
// or maximum of two integers without 
// branching
public class AWS
{

    /*Function to find minimum of x and y*/
    public  static int min(int x, int y)
    {
    return y ^ ((x ^ y) & -(x << y));
    }

    /*Function to find maximum of x and y*/
    public  static int max(int x, int y)
    {
    return x ^ ((x ^ y) & -(x << y));
    }

    /* Driver program to test above functions */
    public static void Main(string[] args)
    {

        int x = 15;
        int y = 6;
        Console.Write("Minimum of " + x + " and " + y + " is ");
        Console.WriteLine(min(x, y));
        Console.Write("Maximum of " + x + " and " + y + " is ");
        Console.WriteLine(max(x, y));
    }

}

  // This code is contributed by Shrikant13
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to Compute the minimum
// or maximum of two integers without
// branching

// Function to find minimum
// of x and y
function m_in($x, $y)
{
    return $y ^ (($x ^ $y) &
            - ($x < $y));
}

// Function to find maximum
// of x and y
function m_ax($x, $y)
{
    return $x ^ (($x ^ $y) &
            - ($x < $y));
}

// Driver Code
$x = 15;
$y = 6;
echo"Minimum of"," ", $x," ","and",
    " ",$y," "," is "," ";

echo m_in($x, $y);

echo "\nMaximum of"," ",$x," ",
    "and"," ",$y," ", " is ";

echo m_ax($x, $y);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
// Javascript program to Compute the minimum
// or maximum of two integers without
// branching

    /*Function to find minimum of x and y*/
    function min(x,y)
    {
        return y ^ ((x ^ y) & -(x << y));
    }

    /*Function to find maximum of x and y*/
    function max(x,y)
    {
        return x ^ ((x ^ y) & -(x << y));
    }

    /* Driver program to test above functions */
    let x = 15
    let y = 6
    document.write("Minimum of  "+ x + " and " + y + " is ");
    document.write(min(x, y) + "<br>");
    document.write("Maximum of " + x + " and " + y + " is ");
    document.write(max(x, y) + "\n");

    // This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
Minimum of 15 and 6 is 6
Maximum of 15 and 6 is 15
```

**方法 2(使用减法和移位)**
如果我们知道

```
INT_MIN <= (x - y) <= INT_MAX
```

，那么我们可以使用下面的方法，因为(x–y)只需要计算一次，所以速度更快。
x 和 y 的最小值为

```
y + ((x - y) & ((x - y) >>(sizeof(int) * CHAR_BIT - 1)))
```

此方法将 x 和 y 的减法移位 31(如果整数的大小为 32)。如果(x-y)小于 0，则(x -y)>>31 将为 1。如果(x-y)大于或等于 0，则(x -y)>>31 将为 0。
所以如果 x > = y，我们得到最小值为 y + (x-y) & 0，这是 y。
如果 x < y，我们得到最小值为 y + (x-y) & 1，这是 x。
同样，找到最大用途

```
x - ((x - y) & ((x - y) >> (sizeof(int) * CHAR_BIT - 1)))
```

## C++

```
#include <bits/stdc++.h>
using namespace std;
#define CHARBIT 8

/*Function to find minimum of x and y*/
int min(int x, int y)
{
    return y + ((x - y) & ((x - y) >>
            (sizeof(int) * CHARBIT - 1)));
}

/*Function to find maximum of x and y*/
int max(int x, int y)
{
    return x - ((x - y) & ((x - y) >>
            (sizeof(int) * CHARBIT - 1)));
}

/* Driver code */
int main()
{
    int x = 15;
    int y = 6;
    cout<<"Minimum of "<<x<<" and "<<y<<" is ";
    cout<<min(x, y);
    cout<<"\nMaximum of"<<x<<" and "<<y<<" is ";
    cout<<max(x, y);
}

// This code is contributed by rathbhupendra
```

## C

```
#include<stdio.h>
#define CHAR_BIT 8

/*Function to find minimum of x and y*/
int min(int x, int y)
{
  return  y + ((x - y) & ((x - y) >>
            (sizeof(int) * CHAR_BIT - 1)));
}

/*Function to find maximum of x and y*/
int max(int x, int y)
{
  return x - ((x - y) & ((x - y) >>
            (sizeof(int) * CHAR_BIT - 1)));
}

/* Driver program to test above functions */
int main()
{
  int x = 15;
  int y = 6;
  printf("Minimum of %d and %d is ", x, y);
  printf("%d", min(x, y));
  printf("\nMaximum of %d and %d is ", x, y);
  printf("%d", max(x, y));
  getchar();
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA implementation of above approach
class GFG
{

static int CHAR_BIT = 4;
static int INT_BIT = 8;
/*Function to find minimum of x and y*/
static int min(int x, int y)
{
    return y + ((x - y) & ((x - y) >>
                (INT_BIT * CHAR_BIT - 1)));
}

/*Function to find maximum of x and y*/
static int max(int x, int y)
{
    return x - ((x - y) & ((x - y) >>
            (INT_BIT * CHAR_BIT - 1)));
}

/* Driver code */
public static void main(String[] args)
{
    int x = 15;
    int y = 6;
    System.out.println("Minimum of "+x+" and "+y+" is "+min(x, y));
    System.out.println("Maximum of "+x+" and "+y+" is "+max(x, y));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import sys;

CHAR_BIT = 8;
INT_BIT = sys.getsizeof(int());

#Function to find minimum of x and y
def Min(x, y):
    return y + ((x - y) & ((x - y) >>
                (INT_BIT * CHAR_BIT - 1)));

#Function to find maximum of x and y
def Max(x, y):
    return x - ((x - y) & ((x - y) >>
                (INT_BIT * CHAR_BIT - 1)));

# Driver code
x = 15;
y = 6;
print("Minimum of", x, "and",
                    y, "is", Min(x, y));
print("Maximum of", x, "and",
                    y, "is", Max(x, y));

# This code is contributed by PrinciRaj1992
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

static int CHAR_BIT = 8;

/*Function to find minimum of x and y*/
static int min(int x, int y)
{
    return y + ((x - y) & ((x - y) >>
                (sizeof(int) * CHAR_BIT - 1)));
}

/*Function to find maximum of x and y*/
static int max(int x, int y)
{
    return x - ((x - y) & ((x - y) >>
            (sizeof(int) * CHAR_BIT - 1)));
}

/* Driver code */
static void Main()
{
    int x = 15;
    int y = 6;
    Console.WriteLine("Minimum of "+x+" and "+y+" is "+min(x, y));
    Console.WriteLine("Maximum of "+x+" and "+y+" is "+max(x, y));
}
}

// This code is contributed by mits
```

## java 描述语言

```
<script>
// javascript implementation of above approach   
var CHAR_BIT = 4;
    var INT_BIT = 8;

    /* Function to find minimum of x and y */
    function min(x , y) {
        return y + ((x - y) & ((x - y) >> (INT_BIT * CHAR_BIT - 1)));
    }

    /* Function to find maximum of x and y */
    function max(x , y) {
        return x - ((x - y) & ((x - y) >> (INT_BIT * CHAR_BIT - 1)));
    }

    /* Driver code */
        var x = 15;
        var y = 6;
        document.write("Minimum of " + x + " and " + y + " is " + min(x, y)+"<br/>");
        document.write("Maximum of " + x + " and " + y + " is " + max(x, y));

// This code is contributed by shikhasingrajput
</script>
```

注意，1989 ANSI C 规范没有规定带符号右移的结果，所以上述方法不可移植。如果在溢出时抛出异常，那么 x 和 y 的值应该是无符号的，或者对于减法转换成无符号的，以避免不必要的抛出异常，然而右移需要一个有符号的操作数来产生负的所有 1 位，所以转换成有符号的。

**方法 3(使用绝对值)**

求绝对值最大/最小数的一般公式是:

```
(x + y + ABS(x-y) )/2
```

找到的最小数量是:

```
(x + y - ABS(x-y) )/2
```

因此，如果我们可以使用按位运算来找到绝对值，我们就可以在不使用 if 条件的情况下找到最大/最小数。用位运算求绝对路的方法可以在[这里](https://stackoverflow.com/questions/12041632/how-to-compute-the-integer-absolute-value)找到:

步骤 1)将掩码设置为整数右移 31(假设整数存储为二进制补码 32 位值，并且右移运算符进行符号扩展)。

```
mask = n>>31
```

步骤 2)将掩码与数字异或

```
mask ^ n
```

步骤 3)从步骤 2 的结果中减去掩码并返回结果。

```
(mask^n) - mask 
```

因此，我们可以得出如下解决方案:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

int absbit32(int x, int y)
{
    int sub = x - y;
    int mask = (sub >> 31);
    return (sub ^ mask) - mask;        
 }

int max(int x, int y)
{
    int abs = absbit32(x, y);        
    return (x + y + abs) / 2;        
 }

int min(int x, int y)
{
    int abs = absbit32(x, y);        
    return (x + y - abs) / 2;
}

// Driver Code
int main()
{
    cout << max(2, 3) << endl; //3
    cout <<  max(2, -3) << endl; //2
    cout << max(-2, -3) << endl; //-2
    cout <<  min(2, 3) << endl; //2
    cout << min(2, -3) << endl; //-3
    cout << min(-2, -3) << endl; //-3

    return 0;
}

// This code is contributed by avijitmondal1998
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;

class GFG {
     public static void main(String []args){
        System.out.println( max(2,3) ); //3
        System.out.println( max(2,-3) ); //2
        System.out.println( max(-2,-3) ); //-2
        System.out.println( min(2,3) ); //2
        System.out.println( min(2,-3) ); //-3
        System.out.println( min(-2,-3) ); //-3
     }

     public static int max(int x, int y){
         int abs = absbit32(x,y);        
         return (x + y + abs)/2;        
     }

     public static int min(int x, int y){
         int abs = absbit32(x,y);        
         return (x + y - abs)/2;
     }

     public static int absbit32(int x, int y){
         int sub = x - y;
         int mask = (sub >> 31);
         return (sub ^ mask) - mask;        
     }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach
def max(x, y):
  abs = absbit32(x,y)
  return (x + y + abs)//2     

def min(x, y):
  abs = absbit32(x,y)
  return (x + y - abs)//2

def absbit32( x, y):
  sub = x - y
  mask = (sub >> 31)
  return (sub ^ mask) - mask      

# Driver code
print( max(2,3) ) #3
print( max(2,-3) ) #2
print( max(-2,-3) ) #-2
print( min(2,3) ) #2
print( min(2,-3) ) #-3
print( min(-2,-3) ) #-3

# This code is contributed by rohitsingh07052.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

public static void Main(String []args)
{
    Console.WriteLine(max(2, 3)); //3
    Console.WriteLine(max(2, -3)); //2
    Console.WriteLine(max(-2, -3)); //-2
    Console.WriteLine(min(2, 3)); //2
    Console.WriteLine(min(2, -3)); //-3
    Console.WriteLine(min(-2, -3)); //-3
}

public static int max(int x, int y)
{
    int abs = absbit32(x, y);        
    return (x + y + abs) / 2;        
}

public static int min(int x, int y)
{
    int abs = absbit32(x, y);        
    return (x + y - abs) / 2;
}

public static int absbit32(int x, int y)
{
    int sub = x - y;
    int mask = (sub >> 31);
    return (sub ^ mask) - mask;        
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript program for the above approach

 function max(x , y){
     var abs = absbit32(x,y);        
     return (x + y + abs)/2;        
 }

 function min(x , y){
     var abs = absbit32(x,y);        
     return (x + y - abs)/2;
 }

 function absbit32(x , y){
     var sub = x - y;
     var mask = (sub >> 31);
     return (sub ^ mask) - mask;        
 }
 // Drive code
 document.write( max(2,3)+"<br>" ); //3
 document.write( max(2,-3)+"<br>" ); //2
 document.write( max(-2,-3)+"<br>" ); //-2
 document.write( min(2,3)+"<br>" ); //2
 document.write( min(2,-3)+"<br>" ); //-3
 document.write( min(-2,-3) ); //-3

// This code is contributed by 29AjayKumar

</script>
```

**来源:**