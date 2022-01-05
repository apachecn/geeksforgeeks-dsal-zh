# 不使用乘法、除法和按位运算符乘法两个整数，不循环

> 原文:[https://www . geeksforgeeks . org/乘法-二进制数-不使用乘法-除法-按位-运算符-不循环/](https://www.geeksforgeeks.org/multiply-two-numbers-without-using-multiply-division-bitwise-operators-and-no-loops/)

通过使用递归，我们可以用给定的约束条件乘以两个整数。
要将 x 和 y 相乘，递归加 x 和 y 次。

## C++

```
// C++ program to Multiply two integers without
// using multiplication, division and bitwise
//  operators, and no loops
#include<iostream>

using namespace std;
class GFG
{

/* function to multiply two numbers x and y*/
public : int multiply(int x, int y)
{
    /* 0 multiplied with anything gives 0 */
    if(y == 0)
    return 0;

    /* Add x one by one */
    if(y > 0 )
    return (x + multiply(x, y-1));

    /* the case where y is negative */
    if(y < 0 )
    return -multiply(x, -y);
}
};

// Driver code
int main()
{
    GFG g;
    cout << endl << g.multiply(5, -11);
    getchar();
    return 0;
}

// This code is contributed by SoM15242
```

## C

```
#include<stdio.h>
/* function to multiply two numbers x and y*/
int multiply(int x, int y)
{
   /* 0  multiplied with anything gives 0 */
   if(y == 0)
     return 0;

   /* Add x one by one */
   if(y > 0 )
     return (x + multiply(x, y-1));

  /* the case where y is negative */
   if(y < 0 )
     return -multiply(x, -y);
}

int main()
{
  printf("\n %d", multiply(5, -11));
  getchar();
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
class GFG {

    /* function to multiply two numbers x and y*/
    static int multiply(int x, int y) {

        /* 0 multiplied with anything gives 0 */
        if (y == 0)
            return 0;

        /* Add x one by one */
        if (y > 0)
            return (x + multiply(x, y - 1));

        /* the case where y is negative */
        if (y < 0)
            return -multiply(x, -y);

        return -1;
    }

    // Driver code
    public static void main(String[] args) {

        System.out.print("\n" + multiply(5, -11));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Function to multiply two numbers
# x and y
def multiply(x,y):

    # 0 multiplied with anything
    # gives 0
    if(y == 0):
        return 0

    # Add x one by one
    if(y > 0 ):
        return (x + multiply(x, y - 1))

    # The case where y is negative
    if(y < 0 ):
        return -multiply(x, -y)

# Driver code
print(multiply(5, -11))

# This code is contributed by Anant Agarwal.
```

## C#

```
// Multiply two integers without
// using multiplication, division
// and bitwise operators, and no
// loops
using System;

class GFG {

    // function to multiply two numbers
    // x and y
    static int multiply(int x, int y) {

        // 0 multiplied with anything gives 0
        if (y == 0)
            return 0;

        // Add x one by one
        if (y > 0)
            return (x + multiply(x, y - 1));

        // the case where y is negative
        if (y < 0)
            return -multiply(x, -y);

        return -1;
    }

    // Driver code
    public static void Main() {

        Console.WriteLine(multiply(5, -11));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// function to multiply
// two numbers x and y
function multiply($x, $y)
{
/* 0 multiplied with
anything gives 0 */
if($y == 0)
    return 0;

/* Add x one by one */
if($y > 0 )
    return ($x + multiply($x,
                          $y - 1));

/* the case where
y is negative */
if($y < 0 )
    return -multiply($x, -$y);
}

// Driver Code
echo multiply(5, -11);

// This code is contributed by mits.
?>
```

## java 描述语言

```
<script>

// javascript program to Multiply two integers without
// using multiplication, division and bitwise
//  operators, and no loops

/* function to multiply two numbers x and y*/
function multiply( x,  y)
{
    /* 0 multiplied with anything gives 0 */
    if(y == 0)
    return 0;

    /* Add x one by one */
    if(y > 0 )
    return (x + multiply(x, y-1));

    /* the case where y is negative */
    if(y < 0 )
    return -multiply(x, -y);
}

// Driver code

   document.write( multiply(5, -11));

// This code is contributed by todaysgaurav

</script>
```

**输出:**

```
-55
```

时间复杂度:O(y)，其中 y 是函数乘法()的第二个参数。

辅助空间:O(y)
[俄罗斯农民(使用按位运算符乘以两个数字)](https://www.geeksforgeeks.org/russian-peasant-multiply-two-numbers-using-bitwise-operators/)
如果您发现上面的代码/算法有任何不正确的地方，请写评论，或者找到更好的方法来解决同样的问题。