# 元素乘积为偶数的子集总数

> 原文:[https://www . geesforgeks . org/元素乘积为偶数的子集总数/](https://www.geeksforgeeks.org/total-number-of-subsets-in-which-the-product-of-the-elements-is-even/)

给定一个整数元素的数组 **arr[]** ，任务是找出元素乘积为偶数的 **arr[]** 的子集总数。

**示例:**

> **输入:** arr[] = {2，2，3}
> **输出:** 6
> 所有可能的子集为{2}、{2}、{2，2}、{2，3}、{2，3}和{2，2，3}
> 
> **输入:** arr[] = {3，3，3 }
> T3】输出: 6

**进场:**我们已经知道:

*   偶数*偶数=偶数
*   奇数*偶数=偶数
*   奇数*奇数=奇数

现在，我们需要计算至少存在一个偶数元素的子集总数，以便元素的乘积为偶数。
现在，**具有至少一个偶数元素的子集总数= n 个可能子集的总数–具有所有奇数元素的子集总数**
即**(2<sup>n</sup>–1)–(2<sup>总计奇数</sup>–1)**
以下是上述方法的实现:

## C++

```
// C++ implementation of above approach

#include <iostream>
#include<bits/stdc++.h>

using namespace std;

// Function to find total number of subsets
// in which product of the elements is even
void find(int a[], int n)
{
    int count_odd = 0;

    for(int i = 0; i < n ; i++)
    {
        // counting number of odds elements
        if (i % 2 != 0)
        count_odd += 1;
    }

    int result = pow(2, n) - 1 ;
    result -= (pow(2, count_odd) - 1) ;
    cout << result << endl;

}

// Driver code
int main()
{
   int a[] = {2, 2, 3} ;
   int n = sizeof(a)/sizeof(a[0]) ;

   // function calling
   find(a,n);

   return 0;
   // This code is contributed by ANKITRAI1;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach

class GFG {

// Function to find total number of subsets
// in which product of the elements is even
    static void find(int a[], int n) {
        int count_odd = 0;

        for (int i = 0; i < n; i++) {
            // counting number of odds elements
            if (i % 2 != 0) {
                count_odd += 1;
            }
        }

        int result = (int) (Math.pow(2, n) - 1);
        result -= (Math.pow(2, count_odd) - 1);
        System.out.println(result);

    }

// Driver code
    public static void main(String[] args) {
        int a[] = {2, 2, 3};
        int n = a.length;

// function calling
        find(a, n);

    }
}
//this code contributed by 29AJayKumar
```

## 蟒蛇 3

```
# Python3 implementation of above approach
import math as ma

# Function to find total number of subsets
# in which product of the elements is even
def find(a):
    count_odd = 0
    for i in a:

        # counting number of odds elements
        if(i % 2 != 0):
            count_odd+= 1

    result = pow(2, len(a)) - 1
    result = result - (pow(2, count_odd) - 1)
    print(result)

# Driver code
a =[2, 2, 3]
find(a)
```

## C#

```

// C# implementation of above approach
using System;
public class GFG {

// Function to find total number of subsets
// in which product of the elements is even
    static void find(int []a, int n) {
        int count_odd = 0;

        for (int i = 0; i < n; i++) {
            // counting number of odds elements
            if (i % 2 != 0) {
                count_odd += 1;
            }
        }

        int result = (int) (Math.Pow(2, n) - 1);
        result -= (int)(Math.Pow(2, count_odd) - 1);
        Console.Write(result);

    }

// Driver code
    public static void Main() {
        int []a = {2, 2, 3};
        int n = a.Length;

// function calling
        find(a, n);

    }
}
//this code contributed by 29AJayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function to find total number of subsets
// in which product of the elements is even
function find(&$a, $n)
{
    $count_odd = 0;

    for($i = 0; $i < $n ; $i++)
    {
        // counting number of odds elements
        if ($i % 2 != 0)
        $count_odd += 1;
    }

    $result = pow(2, $n) - 1 ;
    $result -= (pow(2, $count_odd) - 1) ;
    echo $result ."\n";

}

// Driver code

$a = array(2, 2, 3) ;
$n = sizeof($a)/sizeof($a[0]) ;

// function calling
find($a,$n);

return 0;

?>
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// Function to find total number of subsets
// in which product of the elements is even
function find(a, n)
{
    var count_odd = 0;

    for(var i = 0; i < n ; i++)
    {
        // counting number of odds elements
        if (i % 2 != 0)
            count_odd += 1;
    }

    var result = Math.pow(2, n) - 1 ;
    result -= (Math.pow(2, count_odd) - 1) ;
    document.write( result );

}

// Driver code
var a = [2, 2, 3];
var n = a.length;

// function calling
find(a,n);

</script>
```

**Output:** 

```
6
```