# 如何用递归解决与数字相关的问题？

> 原文:[https://www . geeksforgeeks . org/如何使用递归解决与数字相关的问题/](https://www.geeksforgeeks.org/how-to-solve-problems-related-to-number-digits-using-recursion/)

函数直接或间接调用自身的过程称为[递归](https://www.geeksforgeeks.org/recursion/)，对应的函数称为递归函数。使用递归算法，某些问题可以很容易地解决。本文讨论了用递归方法解决数字问题的一种方法。
任何递归函数都存在两个主要组成部分:

1.  **基本情况:**基本情况是停止递归函数调用的条件。递归函数在没有基本情况下无法形成，因为当没有定义基本情况时会发生堆栈溢出错误，因为函数会不断重复调用自己。对于递归解决方案，可以有多个基本情况。
2.  **递归情况:**对于除基本情况之外的所有其他情况，函数用一组新的值调用自己，使得在一些有限的递归调用之后，函数最终调用基本情况并停止自身。

让我们通过从给定的数字中提取单个数字来可视化递归。这是执行许多其他数学运算的基本步骤。
下面是提取一个数字的每个数字的实现:

## C++

```
// Recursive function to extract
// individual digit for a given
// number
#include<bits/stdc++.h>
using namespace std;

void extract(int n){

    // If n is a zero
    // then, stop the recursion
    if(n == 0)
    {
        return;
    }

    // Call the function recursively
    // for n // 10 which basically
    // calls for the remaining number
    // after removing the last digit
    extract(n / 10);

      // print the current last digit of the number
      // with n%10;
    cout << n % 10 << endl;

}

// Driver code
int main()
{
    extract(1234);
    return 0;
}

// This code is contributed by 29AjayKumar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Recursive function to extract
// individual digit for a given
// number
class GFG{

static void extract(int n)
{

    // If n is a zero
    // then, stop the recursion
    if(n == 0)
    {
        return;
    }

    // Call the function recursively
    // for n/10 which basically
    // calls for the remaining number
    // after removing the last digit
    extract(n / 10);

      // print the current last digit of the number
      // with n%10;
      System.out.println(n%10);
}

// Driver code
public static void main(String[] args)
{
    extract(1234);
}
}

// This code is contributed by Rohit_ranjan
```

## 蟒蛇 3

```
# Recursive function to extract
# individual digit for a given
# number
def extract(n):

    # If n is a zero
    # the stop the recursion
    if(n == 0):
        return

    # Call the function recursively
    # for n // 10 which basically
    # calls for the remaining number
    # after removing the last digit
    extract(n//10)

    # print the last digit with n%10
    print(n % 10)

# Driver code
if __name__ == "__main__":
    extract(1234)
```

## C#

```
// Recursive function to extract
// individual digit for a given
// number
using System;

class GFG{

static void extract(int n)
{

   // If n is a zero
   // then, stop the recursion
    if(n  == 0)
    {
        return;
    }

    // Call the function recursively
    // for n // 10 which basically
    // calls for the remaining number
    // after removing the last digit
    extract(n / 10);

      // print the current last digit of the number
      // with n%10;
    Console.Write(n % 10 + "\n");

}

// Driver code
public static void Main(String[] args)
{
    extract(1234);
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

    // Recursive function to extract
    // individual digit for a given number

    function extract(n)
    {

        // If n is a zero
        // then stop the recursion
        if(parseInt(n) == 0)
        {
            return;
        }

        // Call the function recursively
        // for n // 10 which basically
        // calls for the remaining number
        // after removing the last digit
        extract(parseInt(n / 10, 10));

        // print the current last digit of the number
          // with n%10;
        document.write(n % 10 + "</br>");

    }

    extract(1001);

</script>
```

**Output**

```
1
2
3
4
```

与此类似，可以使用递归执行各种其他操作。每个迭代函数都可以用递归来计算。