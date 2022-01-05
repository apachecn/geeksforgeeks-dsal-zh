# 找出给定的数是否是 4 的幂

> 原文:[https://www . geesforgeks . org/find-不管给定的数字是 4 的幂还是不是/](https://www.geeksforgeeks.org/find-whether-a-given-number-is-a-power-of-4-or-not/)

给定一个整数 n，求它是否是 4 的幂。

**示例:**

```
Input : 16
Output : 16 is a power of 4

Input : 20
Output : 20 is not a power of 4
```

## [我们强烈建议您点击此处进行练习，然后再进入解决方案。](https://practice.geeksforgeeks.org/probfunc-page.php?pid=700129)

**1。**一个简单的方法是取给定数的对数，以 4 为基数，如果我们得到一个整数，那么这个数就是 4 的幂。
T3】2。另一种解决方法是继续用 4 除数，即迭代做 n = n/4。在任何迭代中，如果 n%4 变成非零且 n 不是 1，则 n 不是 4 的幂，否则 n 是 4 的幂。

## C++

```
// C++ program to find whether a given
// number is a power of 4 or not
#include<iostream>

using namespace std;
#define bool int

class GFG
{

/* Function to check if x is power of 4*/
public : bool isPowerOfFour(int n)
{
    if(n == 0)
        return 0;
    while(n != 1)
    {
        if(n % 4 != 0)
            return 0;
        n = n / 4;
    }
    return 1;
}
};

/*Driver code*/
int main()
{
    GFG g;
    int test_no = 64;
    if(g.isPowerOfFour(test_no))
        cout << test_no << " is a power of 4";
    else
        cout << test_no << "is not a power of 4";
    getchar();
}

// This code is contributed by SoM15242
```

## C

```
#include<stdio.h>
#define bool int

/* Function to check if x is power of 4*/
bool isPowerOfFour(int n)
{
  if(n == 0)
    return 0;
  while(n != 1)
  {   
   if(n % 4 != 0)
      return 0;
    n = n / 4;     
  }
  return 1;
}

/*Driver program to test above function*/
int main()
{
  int test_no = 64;
  if(isPowerOfFour(test_no))
    printf("%d is a power of 4", test_no);
  else
    printf("%d is not a power of 4", test_no);
  getchar();
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to check if given
// number is power of 4 or not

class GFG {

    // Function to check if
    // x is power of 4
    static int isPowerOfFour(int n)
    {
        if(n == 0)
        return 0;
        while(n != 1)
        {
            if(n % 4 != 0)
            return 0;
            n = n / 4;    
        }
        return 1;
    }

    // Driver program
    public static void main(String[] args)
    {
        int test_no = 64;
        if(isPowerOfFour(test_no) == 1)
         System.out.println(test_no +
                           " is a power of 4");
        else
         System.out.println(test_no +
                           "is not a power of 4");
    }
}

// This code is contributed
// by  prerna saini
```

## 蟒蛇 3

```
# Python3 program to check if given
# number is power of 4 or not

# Function to check if x is power of 4
def isPowerOfFour(n):
    if (n == 0):
        return False
    while (n != 1):
            if (n % 4 != 0):
                return False
            n = n // 4

    return True

# Driver code
test_no = 64
if(isPowerOfFour(64)):
    print(test_no, 'is a power of 4')
else:
    print(test_no, 'is not a power of 4')

# This code is contributed by Danish Raza
```

## C#

```
// C# code to check if given
// number is power of 4 or not
using System;

class GFG {

    // Function to check if
    // x is power of 4
    static int isPowerOfFour(int n)
    {
        if (n == 0)
            return 0;
        while (n != 1) {
            if (n % 4 != 0)
                return 0;
            n = n / 4;
        }
        return 1;
    }

    // Driver code
    public static void Main()
    {
        int test_no = 64;
        if (isPowerOfFour(test_no) == 1)
            Console.Write(test_no +
                    " is a power of 4");
        else
            Console.Write(test_no +
                " is not a power of 4");
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to check if given
// number is power of 4 or not

// Function to check if
// x is power of 4
function isPowerOfFour($n)
{

    if($n == 0)
        return 0;
    while($n != 1)
    {
        if($n % 4 != 0)
            return 0;
            $n = $n / 4;    
    }
    return 1;
}

// Driver Code
$test_no = 64;

if(isPowerOfFour($test_no))
    echo $test_no," is a power of 4";
else
    echo $test_no," is not a power of 4";

// This code is contributed by Rajesh
?>
```

## java 描述语言

```
<script>

/* Function to check if x is power of 4*/
function isPowerOfFour( n)
{
  if(n == 0)
    return false;
  while(n != 1)
  {   
   if(n % 4 != 0)
      return false;
    n = n / 4;     
  }
  return true;
}

/*Driver program to test above function*/
let test_no = 64;
  if(isPowerOfFour(test_no))
    document.write(test_no+" is a power of 4");
  else
    document.write(test_no+" is not a power of 4");

// This code is contributed by gauravrajput1

</script>
```

**Output**

```
64 is a power of 4
```