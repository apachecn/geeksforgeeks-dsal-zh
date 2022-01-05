# 丑陋的数字

> 原文:[https://www.geeksforgeeks.org/ugly-numbers/](https://www.geeksforgeeks.org/ugly-numbers/)

丑陋的数字是唯一质因数是 2、3 或 5 的数字。序列 1，2，3，4，5，6，8，9，10，12，15，…显示了前 11 个丑陋的数字。按照惯例，包括 1。
给定一个数字 n，任务是找到第 n 个丑陋的数字。

**示例:**

```
Input  : n = 7
Output : 8

Input  : n = 10
Output : 12

Input  : n = 15
Output : 24

Input  : n = 150
Output : 5832
```

**方法 1(简单)**
循环所有正整数，直到丑数计数小于 n，如果一个整数比增量丑数计数更丑。
要检查一个数字是否丑陋，用 2、3 和 5 的最大可除数除以这个数字，如果这个数字变成 1，那么它就是一个丑陋的数字，否则不是。

比如，让我们看看如何检查 300 是丑还是不丑。2 的最大可分幂是 4，300 除以 4 后我们得到 75。3 的最大可分幂是 3，75 除以 3 后我们得到 25。5 的最大可分幂是 25，25 除以 25 后得到 1。既然我们最终得到了 1，300 就是一个丑陋的数字。

下面是上述方法的实现:

## C++

```
// C++ program to find nth ugly number
#include <iostream>
using namespace std;

// This function divides a by greatest
// divisible power of b
int maxDivide(int a, int b)
{
    while (a % b == 0)
        a = a / b;

    return a;
}

// Function to check if a number is ugly or not
int isUgly(int no)
{
    no = maxDivide(no, 2);
    no = maxDivide(no, 3);
    no = maxDivide(no, 5);

    return (no == 1) ? 1 : 0;
}

// Function to get the nth ugly number
int getNthUglyNo(int n)
{
    int i = 1;

    // Ugly number count
    int count = 1;

    // Check for all integers until ugly
    // count becomes n
    while (n > count)
    {
        i++;
        if (isUgly(i))
            count++;
    }
    return i;
}

// Driver Code
int main()
{

    // Function call
    unsigned no = getNthUglyNo(150);
    cout << "150th ugly no. is " << no;
    return 0;
}

// This code is contributed by shivanisinghss2110
```

## C

```
// C program to find nth ugly number
#include <stdio.h>
#include <stdlib.h>

// This function divides a by greatest divisible
//  power of b
int maxDivide(int a, int b)
{
    while (a % b == 0)
        a = a / b;
    return a;
}

// Function to check if a number is ugly or not
int isUgly(int no)
{
    no = maxDivide(no, 2);
    no = maxDivide(no, 3);
    no = maxDivide(no, 5);

    return (no == 1) ? 1 : 0;
}

// Function to get the nth ugly number
int getNthUglyNo(int n)
{

    int i = 1;

    // ugly number count
    int count = 1;

    // Check for all integers until ugly count
    //  becomes n
    while (n > count) {
        i++;
        if (isUgly(i))
            count++;
    }
    return i;
}

// Driver Code
int main()
{
    // Function call
    unsigned no = getNthUglyNo(150);
    printf("150th ugly no. is %d ", no);
    getchar();
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find nth ugly number
class GFG {

    /*This function divides a by greatest
    divisible power of b*/
    static int maxDivide(int a, int b)
    {
        while (a % b == 0)
            a = a / b;
        return a;
    }

    /* Function to check if a number
    is ugly or not */
    static int isUgly(int no)
    {
        no = maxDivide(no, 2);
        no = maxDivide(no, 3);
        no = maxDivide(no, 5);

        return (no == 1) ? 1 : 0;
    }

    /* Function to get the nth ugly
    number*/
    static int getNthUglyNo(int n)
    {
        int i = 1;

        // ugly number count
        int count = 1;

        // check for all integers
        // until count becomes n
        while (n > count) {
            i++;
            if (isUgly(i) == 1)
                count++;
        }
        return i;
    }

    /* Driver Code*/
    public static void main(String args[])
    {
        int no = getNthUglyNo(150);

        // Function call
        System.out.println("150th ugly "
                           + "no. is " + no);
    }
}

// This code has been contributed by
// Amit Khandelwal (Amit Khandelwal 1)
```

## 蟒蛇 3

```
# Python3 code to find nth ugly number

# This function divides a by greatest
# divisible power of b

def maxDivide(a, b):
    while a % b == 0:
        a = a / b
    return a

# Function to check if a number
# is ugly or not
def isUgly(no):
    no = maxDivide(no, 2)
    no = maxDivide(no, 3)
    no = maxDivide(no, 5)
    return 1 if no == 1 else 0

# Function to get the nth ugly number
def getNthUglyNo(n):
    i = 1

    # ugly number count
    count = 1 

    # Check for all integers until
    # ugly count becomes n
    while n > count:
        i += 1
        if isUgly(i):
            count += 1
    return i

# Driver code
no = getNthUglyNo(150)
print("150th ugly no. is ", no)

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// C# program to find nth ugly number
using System;

class GFG {

    /*This function divides a by
    greatest divisible power of b*/
    static int maxDivide(int a, int b)
    {
        while (a % b == 0)
            a = a / b;
        return a;
    }

    /* Function to check if a number
    is ugly or not */
    static int isUgly(int no)
    {
        no = maxDivide(no, 2);
        no = maxDivide(no, 3);
        no = maxDivide(no, 5);

        return (no == 1) ? 1 : 0;
    }

    /* Function to get the nth ugly
    number*/
    static int getNthUglyNo(int n)
    {
        int i = 1;

        // ugly number count
        int count = 1;

        // Check for all integers
        // until count becomes n
        while (n > count) {
            i++;
            if (isUgly(i) == 1)
                count++;
        }
        return i;
    }

    // Driver code
    public static void Main()
    {
        int no = getNthUglyNo(150);

        // Function call
        Console.WriteLine("150th ugly"
                          + " no. is " + no);
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find nth ugly number

// This function divides a by
// greatest divisible power of b
function maxDivide($a, $b)
{
    while ($a % $b == 0)
    $a = $a / $b;
    return $a;
}

// Function to check if a
// number is ugly or not
function isUgly($no)
{
    $no = maxDivide($no, 2);
    $no = maxDivide($no, 3);
    $no = maxDivide($no, 5);

    return ($no == 1)? 1 : 0;
}

// Function to get the nth
// ugly number
function getNthUglyNo($n)
{
    $i = 1;

    // ugly number count
    $count = 1;

// Check for all integers
// until ugly count becomes n
while ($n > $count)
{
    $i++;    
    if (isUgly($i))
    $count++;
}
return $i;
}

    // Driver Code
    $no = getNthUglyNo(150);
    echo "150th ugly no. is ". $no;

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>
// javascript program to find nth ugly number   
/*
     * This function divides a by greatest divisible power of b
     */
    function maxDivide(a , b) {
        while (a % b == 0)
            a = a / b;
        return a;
    }

    /*
     * Function to check if a number is ugly or not
     */
    function isUgly(no) {
        no = maxDivide(no, 2);
        no = maxDivide(no, 3);
        no = maxDivide(no, 5);

        return (no == 1) ? 1 : 0;
    }

    /*
     * Function to get the nth ugly number
     */
    function getNthUglyNo(n)
    {
        var i = 1;

        // ugly number count
        var count = 1;

        // check for all integers
        // until count becomes n
        while (n > count)
        {
            i++;
            if (isUgly(i) == 1)
                count++;
        }
        return i;
    }

    /* Driver Code */   
    var no = getNthUglyNo(150);

    // Function call
    document.write("150th ugly " + "no. is " + no);

// This code is contributed by shikhasingrajput
</script>
```

**Output**

```
150th ugly no. is 5832 
```

这个方法不是时间有效的，因为它检查所有整数，直到难看的数字计数变成 n，但是这个方法的空间复杂度是 O(1)

**方法 2(使用动态编程)**
这里有一个时间有效的解决方案，有 O(n)个额外的空间。丑数序列是 1、2、3、4、5、6、8、9、10、12、15、…
因为每个数只能除以 2、3、5，所以看序列的一种方法是把序列分成如下三组:
(1) 1×2、2×2、3×2、4×2、5×2、…
(2) 1×3、2×3、3×3、4×3、5×3、…
(2)然后我们使用类似合并排序的合并方法，从三个子序列中得到每个难看的数字。每走一步，我们都选择最小的那一步，然后再往前走一步。

```
1 Declare an array for ugly numbers:  ugly[n]
2 Initialize first ugly no:  ugly[0] = 1
3 Initialize three array index variables i2, i3, i5 to point to 
   1st element of the ugly array: 
        i2 = i3 = i5 =0; 
4 Initialize 3 choices for the next ugly no:
         next_mulitple_of_2 = ugly[i2]*2;
         next_mulitple_of_3 = ugly[i3]*3
         next_mulitple_of_5 = ugly[i5]*5;
5 Now go in a loop to fill all ugly numbers till 150:
For (i = 1; i < 150; i++ ) 
{
    /* These small steps are not optimized for good 
      readability. Will optimize them in C program */
    next_ugly_no  = Min(next_mulitple_of_2,
                        next_mulitple_of_3,
                        next_mulitple_of_5); 

    ugly[i] =  next_ugly_no       

    if (next_ugly_no  == next_mulitple_of_2) 
    {             
        i2 = i2 + 1;        
        next_mulitple_of_2 = ugly[i2]*2;
    } 
    if (next_ugly_no  == next_mulitple_of_3) 
    {             
        i3 = i3 + 1;        
        next_mulitple_of_3 = ugly[i3]*3;
     }            
     if (next_ugly_no  == next_mulitple_of_5)
     {    
        i5 = i5 + 1;        
        next_mulitple_of_5 = ugly[i5]*5;
     } 

}/* end of for loop */ 
6.return next_ugly_no
```

**示例:**
让我们看看它是如何工作的

```
initialize
   ugly[] =  | 1 |
   i2 =  i3 = i5 = 0;

First iteration
   ugly[1] = Min(ugly[i2]*2, ugly[i3]*3, ugly[i5]*5)
            = Min(2, 3, 5)
            = 2
   ugly[] =  | 1 | 2 |
   i2 = 1,  i3 = i5 = 0  (i2 got incremented ) 

Second iteration
    ugly[2] = Min(ugly[i2]*2, ugly[i3]*3, ugly[i5]*5)
             = Min(4, 3, 5)
             = 3
    ugly[] =  | 1 | 2 | 3 |
    i2 = 1,  i3 =  1, i5 = 0  (i3 got incremented ) 

Third iteration
    ugly[3] = Min(ugly[i2]*2, ugly[i3]*3, ugly[i5]*5)
             = Min(4, 6, 5)
             = 4
    ugly[] =  | 1 | 2 | 3 |  4 |
    i2 = 2,  i3 =  1, i5 = 0  (i2 got incremented )

Fourth iteration
    ugly[4] = Min(ugly[i2]*2, ugly[i3]*3, ugly[i5]*5)
              = Min(6, 6, 5)
              = 5
    ugly[] =  | 1 | 2 | 3 |  4 | 5 |
    i2 = 2,  i3 =  1, i5 = 1  (i5 got incremented )

Fifth iteration
    ugly[4] = Min(ugly[i2]*2, ugly[i3]*3, ugly[i5]*5)
              = Min(6, 6, 10)
              = 6
    ugly[] =  | 1 | 2 | 3 |  4 | 5 | 6 |
    i2 = 3,  i3 =  2, i5 = 1  (i2 and i3 got incremented )

Will continue same way till I < 150
```

## C++

```
// C++ program to find n'th Ugly number
#include <bits/stdc++.h>
using namespace std;

// Function to get the nth ugly number
unsigned getNthUglyNo(unsigned n)
{
    // To store ugly numbers
    unsigned ugly[n];
    unsigned i2 = 0, i3 = 0, i5 = 0;
    unsigned next_multiple_of_2 = 2;
    unsigned next_multiple_of_3 = 3;
    unsigned next_multiple_of_5 = 5;
    unsigned next_ugly_no = 1;

    ugly[0] = 1;
    for (int i = 1; i < n; i++) {
        next_ugly_no = min(
            next_multiple_of_2,
            min(next_multiple_of_3, next_multiple_of_5));
        ugly[i] = next_ugly_no;
        if (next_ugly_no == next_multiple_of_2) {
            i2 = i2 + 1;
            next_multiple_of_2 = ugly[i2] * 2;
        }
        if (next_ugly_no == next_multiple_of_3) {
            i3 = i3 + 1;
            next_multiple_of_3 = ugly[i3] * 3;
        }
        if (next_ugly_no == next_multiple_of_5) {
            i5 = i5 + 1;
            next_multiple_of_5 = ugly[i5] * 5;
        }
    } 

    // End of for loop (i=1; i<n; i++)
    return next_ugly_no;
}

// Driver Code
int main()
{
    int n = 150;
    cout << getNthUglyNo(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find nth ugly number
import java.lang.Math;

class UglyNumber
{
    // Function to get the nth ugly number
    int getNthUglyNo(int n)
    {
         // To store ugly numbers
        int ugly[] = new int[n];
        int i2 = 0, i3 = 0, i5 = 0;
        int next_multiple_of_2 = 2;
        int next_multiple_of_3 = 3;
        int next_multiple_of_5 = 5;
        int next_ugly_no = 1;

        ugly[0] = 1;

        for (int i = 1; i < n; i++)
        {
            next_ugly_no
                = Math.min(next_multiple_of_2,
                           Math.min(next_multiple_of_3,
                                    next_multiple_of_5));

            ugly[i] = next_ugly_no;
            if (next_ugly_no == next_multiple_of_2)
            {
                i2 = i2 + 1;
                next_multiple_of_2 = ugly[i2] * 2;
            }
            if (next_ugly_no == next_multiple_of_3)
            {
                i3 = i3 + 1;
                next_multiple_of_3 = ugly[i3] * 3;
            }
            if (next_ugly_no == next_multiple_of_5)
            {
                i5 = i5 + 1;
                next_multiple_of_5 = ugly[i5] * 5;
            }
        }

        // End of for loop (i=1; i<n; i++)
        return next_ugly_no;
    }

    // Driver code
    public static void main(String args[])
    {

        int n = 150;

        // Function call
        UglyNumber obj = new UglyNumber();
        System.out.println(obj.getNthUglyNo(n));
    }
}

// This code has been contributed by Amit Khandelwal (Amit
// Khandelwal 1)
```

## 计算机编程语言

```
# Python program to find n'th Ugly number

# Function to get the nth ugly number

def getNthUglyNo(n):

    ugly = [0] * n  # To store ugly numbers

    # 1 is the first ugly number
    ugly[0] = 1

    # i2, i3, i5 will indicate indices for
    # 2,3,5 respectively
    i2 = i3 = i5 = 0

    # Set initial multiple value
    next_multiple_of_2 = 2
    next_multiple_of_3 = 3
    next_multiple_of_5 = 5

    # Start loop to find value from
    # ugly[1] to ugly[n]
    for l in range(1, n):

        # Shoose the min value of all
        # available multiples
        ugly[l] = min(next_multiple_of_2,
                      next_multiple_of_3,
                      next_multiple_of_5)

        # Increment the value of index accordingly
        if ugly[l] == next_multiple_of_2:
            i2 += 1
            next_multiple_of_2 = ugly[i2] * 2

        if ugly[l] == next_multiple_of_3:
            i3 += 1
            next_multiple_of_3 = ugly[i3] * 3

        if ugly[l] == next_multiple_of_5:
            i5 += 1
            next_multiple_of_5 = ugly[i5] * 5

    # Return ugly[n] value
    return ugly[-1]

# Driver Code
def main():

    n = 150

    print getNthUglyNo(n)

if __name__ == '__main__':
    main()

# This code is contributed by Neelam Yadav
```

## C#

```
// C# program to count inversions in an array
using System;
using System.Collections.Generic;

class GFG {

    // Function to get the nth ugly number
    static int getNthUglyNo(int n)
    {

        // To store ugly numbers
        int[] ugly = new int[n];
        int i2 = 0, i3 = 0, i5 = 0;
        int next_multiple_of_2 = 2;
        int next_multiple_of_3 = 3;
        int next_multiple_of_5 = 5;
        int next_ugly_no = 1;

        ugly[0] = 1;

        for (int i = 1; i < n; i++)
        {
            next_ugly_no
                = Math.Min(next_multiple_of_2,
                           Math.Min(next_multiple_of_3,
                                    next_multiple_of_5));

            ugly[i] = next_ugly_no;

            if (next_ugly_no == next_multiple_of_2)
            {
                i2 = i2 + 1;
                next_multiple_of_2 = ugly[i2] * 2;
            }

            if (next_ugly_no == next_multiple_of_3)
            {
                i3 = i3 + 1;
                next_multiple_of_3 = ugly[i3] * 3;
            }
            if (next_ugly_no == next_multiple_of_5)
            {
                i5 = i5 + 1;
                next_multiple_of_5 = ugly[i5] * 5;
            }
        }

        return next_ugly_no;
    }

    // Driver code
    public static void Main()
    {
        int n = 150;

        // Function call
        Console.WriteLine(getNthUglyNo(n));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// n'th Ugly number

//  Function to get the
// nth ugly number
function getNthUglyNo($n)
{
    // To store ugly numbers
    $ugly = array_fill(0, $n, 0);
    $i2 = 0;
    $i3 = 0;
    $i5 = 0;
    $next_multiple_of_2 = 2;
    $next_multiple_of_3 = 3;
    $next_multiple_of_5 = 5;
    $next_ugly_no = 1;

    $ugly[0] = 1;
    for ($i = 1; $i < $n; $i++)
    {
    $next_ugly_no = min($next_multiple_of_2,
                    min($next_multiple_of_3,
                        $next_multiple_of_5));
    $ugly[$i] = $next_ugly_no;
    if ($next_ugly_no ==
        $next_multiple_of_2)
    {
        $i2 = $i2 + 1;
        $next_multiple_of_2 = $ugly[$i2] * 2;
    }
    if ($next_ugly_no ==
        $next_multiple_of_3)
    {
        $i3 = $i3 + 1;
        $next_multiple_of_3 = $ugly[$i3] * 3;
    }
    if ($next_ugly_no ==
        $next_multiple_of_5)
    {
        $i5 = $i5 + 1;
        $next_multiple_of_5 = $ugly[$i5] * 5;
    }
    } /*End of for loop (i=1; i<n; i++) */
    return $next_ugly_no;
}

// Driver code
$n = 150;
echo getNthUglyNo($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// javascript program to find nth ugly numberclass UglyNumber

// Function to get the nth ugly number
function getNthUglyNo(n)
{

     // To store ugly numbers
    var ugly = Array.from({length: n}, (_, i) => 0);
    var i2 = 0, i3 = 0, i5 = 0;
    var next_multiple_of_2 = 2;
    var next_multiple_of_3 = 3;
    var next_multiple_of_5 = 5;
    var next_ugly_no = 1;

    ugly[0] = 1;

    for (i = 1; i < n; i++)
    {
        next_ugly_no
            = Math.min(next_multiple_of_2,
                       Math.min(next_multiple_of_3,
                                next_multiple_of_5));

        ugly[i] = next_ugly_no;
        if (next_ugly_no == next_multiple_of_2)
        {
            i2 = i2 + 1;
            next_multiple_of_2 = ugly[i2] * 2;
        }
        if (next_ugly_no == next_multiple_of_3)
        {
            i3 = i3 + 1;
            next_multiple_of_3 = ugly[i3] * 3;
        }
        if (next_ugly_no == next_multiple_of_5)
        {
            i5 = i5 + 1;
            next_multiple_of_5 = ugly[i5] * 5;
        }
    }

    // End of for loop (i=1; i<n; i++)
    return next_ugly_no;
}

// Driver code
var n = 150;

// Function call
document.write(getNthUglyNo(n));

// This code is contributed by Amit Katiyar
</script>
```

**Output**

```
5832
```

**时间复杂度:** O(n)
**辅助空间:** O(n)
[超丑数(素数因子在](https://www.geeksforgeeks.org/super-ugly-number-number-whose-prime-factors-given-set/)[给定集合中的数)](https://www.geeksforgeeks.org/super-ugly-number-number-whose-prime-factors-given-set/)

**方法 3(使用 C++中的 SET 数据结构和 JAVA 中的 TreeSet)**

在这种方法中，设置数据结构来存储 3 个生成的丑数中的最小值，这 3 个丑数将第 i <sup>个</sup>丑数存储在集合的第一个位置。集合数据结构作为一个集合，以升序存储所有元素

下面是上述方法的实现:

## C++

```
// C++ Implemenatation of the above approach
#include <bits/stdc++.h>
using namespace std;

int nthUglyNumber(int n)
{
    // Base cases...
    if (n == 1 or n == 2 or n == 3 or n == 4 or n == 5)
        return n;

    set<long long int> s;
    s.insert(1);
    n--;

    while (n) {
        auto it = s.begin();

        // Get the beginning element of the set
        long long int x = *it;

        // Deleting the ith element
        s.erase(it);

        // Inserting all the other options
        s.insert(x * 2);
        s.insert(x * 3);
        s.insert(x * 5);
        n--;
    }

    // The top of the set represents the nth ugly number
    return *s.begin();
}

// Driver Code
int main()
{
    int n = 150;

    // Function call
    cout << nthUglyNumber(n);
}

// Contributed by:- Soumak Poddar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */

import java.io.*;
import java.util.*;

class GFG {

    static long nthUglyNumber(int n)
    {

        TreeSet<Long> t = new TreeSet<>();
        // Ugly number sequence starts with 1
        t.add(1L);
        int i = 1;
        // when i==n we have the nth ugly number
        while (i < n) {
            // remove the ith ugly number and add back its
            // multiples of 2,3 and 5 back to the set
            long temp = t.pollFirst();
            t.add(temp * 2);
            t.add(temp * 3);
            t.add(temp * 5);
            i++;
            // the first element of set is always the ith
            // ugly number
        }

        return t.pollFirst();
    }

    public static void main(String[] args)
    {
        int n = 150;
        System.out.println(nthUglyNumber(n));
    }
}
// Contributed by:- Saswata Halder
```

## 蟒蛇 3

```
# Python Implemenatation of the above approach
def nthUglyNumber(n):

    # Base cases...
    if (n == 1 or n == 2 or n == 3 or n == 4 or n == 5):
        return n
    s = [1]
    n-=1

    while (n):
        it = s[0]

        # Get the beginning element of the set
        x = it

        # Deleting the ith element
        s = s[1:]
        s = set(s)

        # Inserting all the other options
        s.add(x * 2)
        s.add(x * 3)
        s.add(x * 5)
        s = list(s)
        s.sort()
        n -= 1
    # The top of the set represents the nth ugly number
    return s[0]

# Driver Code
n = 150

# Function call
print( nthUglyNumber(n))

# This code is contributed by Shubham Singh
```

**Output**

```
5832
```

**时间复杂度:-**O(N log N)
T3】辅助空间:- O(N)

**方法 4(使用二分搜索法)**

1.  如果你有 n 的最大值，这个方法是合适的。否的形式是 x =幂(2，p)*幂(3，q)*幂(5，r)。
2.  从低=1 到高=21474836647 搜索。我们预计这个范围内会有第 n 个丑陋的数字。
3.  所以我们做了一个二分搜索法。现在假设我们在 mid，我们会发现丑陋数字的总数小于 mid，并相应地设置我们的条件。

以下是粗略的 CPP 代码:

## C++

```
// CPP program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Print nth Ugly number
int nthUglyNumber(int n)
{

  int pow[40] = { 1 };

  // stored powers of 2 from
  // pow(2,0) to pow(2,30)
  for (int i = 1; i <= 30; ++i)
    pow[i] = pow[i - 1] * 2;

  // Initialized low and high
  int l = 1, r = 2147483647;

  int ans = -1;

  // Applying Binary Search
  while (l <= r) {

    // Found mid
    int mid = l + ((r - l) / 2);

    // cnt stores total numbers of ugly
    // number less than mid
    int cnt = 0;

    // Iterate from 1 to mid
    for (long long i = 1; i <= mid; i *= 5)

    {
      // Possible powers of i less than mid is i
      for (long long j = 1; j * i <= mid; j *= 3)

      {
        // possible powers of 3 and 5 such that
        // their product is less than mid

        // using the power array of 2 (pow) we are
        // trying to find the max power of 2 such
        // that i*J*power of 2 is less than mid

        cnt += upper_bound(pow, pow + 31,
                           mid / (i * j)) - pow;
      }
    }

    // If total numbers of ugly number
    // less than equal
    // to mid is less than n we update l
    if (cnt < n)
      l = mid + 1;

    // If total numbers of ugly number
    // less than qual to
    // mid is greater than n we update
    // r and ans simultaneously.
    else
      r = mid - 1, ans = mid;
  }

  return ans;
}

// Driver Code
int main()
{

    int n = 150;

    // Function Call
    cout << nthUglyNumber(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program for the above approach
import java.util.*;

class GFG
{
  static int upperBound(int[] a, int low,
                        int high, int element)
  {
    while(low < high)
    {
      int middle = low + (high - low)/2;
      if(a[middle] > element)
        high = middle;
      else
        low = middle + 1;
    }
    return low;
  }

  // Print nth Ugly number
  static int nthUglyNumber(int n)
  {

    int pow[] = new int[40];
    Arrays.fill(pow, 1);

    // stored powers of 2 from
    // Math.pow(2,0) to Math.pow(2,30)
    for (int i = 1; i <= 30; ++i)
      pow[i] = pow[i - 1] * 2;

    // Initialized low and high
    int l = 1, r = 2147483647;

    int ans = -1;

    // Applying Binary Search
    while (l <= r) {

      // Found mid
      int mid = l + ((r - l) / 2);

      // cnt stores total numbers of ugly
      // number less than mid
      int cnt = 0;

      // Iterate from 1 to mid
      for (long i = 1; i <= mid; i *= 5)

      {
        // Possible powers of i less than mid is i
        for (long j = 1; j * i <= mid; j *= 3)

        {
          // possible powers of 3 and 5 such that
          // their product is less than mid

          // using the power array of 2 (pow) we are
          // trying to find the max power of 2 such
          // that i*J*power of 2 is less than mid

          cnt += upperBound(pow,0, 31,
                            (int)(mid / (i * j)));
        }
      }

      // If total numbers of ugly number
      // less than equal
      // to mid is less than n we update l
      if (cnt < n)
        l = mid + 1;

      // If total numbers of ugly number
      // less than qual to
      // mid is greater than n we update
      // r and ans simultaneously.
      else {
        r = mid - 1; ans = mid;
      }
    }

    return ans;
  }

  // Driver Code
  public static void main(String[] args)
  {

    int n = 150;

    // Function Call
    System.out.print(nthUglyNumber(n));
  }
}

// This code is contributed by Rajput-Ji
```

## C#

```
// C# program for the above approach
using System;

public class GFG {
  static int upperBound(int[] a, int low,
                        int high, int element)
  {
    while (low < high) {
      int middle = low + (high - low) / 2;
      if (a[middle] > element)
        high = middle;
      else
        low = middle + 1;
    }
    return low;
  }

  // Print nth Ugly number
  static int nthUglyNumber(int n) {

    int []pow = new int[40];
    for (int i = 0; i <40; ++i)
      pow[i] = 1;

    // stored powers of 2 from
    // Math.Pow(2,0) to Math.Pow(2,30)
    for (int i = 1; i <= 30; ++i)
      pow[i] = pow[i - 1] * 2;

    // Initialized low and high
    int l = 1, r = 2147483647;

    int ans = -1;

    // Applying Binary Search
    while (l <= r) {

      // Found mid
      int mid = l + ((r - l) / 2);

      // cnt stores total numbers of ugly
      // number less than mid
      int cnt = 0;

      // Iterate from 1 to mid
      for (long i = 1; i <= mid; i *= 5)

      {
        // Possible powers of i less than mid is i
        for (long j = 1; j * i <= mid; j *= 3)

        {
          // possible powers of 3 and 5 such that
          // their product is less than mid

          // using the power array of 2 (pow) we are
          // trying to find the max power of 2 such
          // that i*J*power of 2 is less than mid

          cnt += upperBound(pow, 0, 31,
                            (int) (mid / (i * j)));
        }
      }

      // If total numbers of ugly number
      // less than equal
      // to mid is less than n we update l
      if (cnt < n)
        l = mid + 1;

      // If total numbers of ugly number
      // less than qual to
      // mid is greater than n we update
      // r and ans simultaneously.
      else {
        r = mid - 1;
        ans = mid;
      }
    }

    return ans;
  }

  // Driver Code
  public static void Main(String[] args) {

    int n = 150;

    // Function Call
    Console.Write(nthUglyNumber(n));
  }
}

// This code is contributed by gauravrajput1
```

**Output**

```
5832
```

**时间复杂度:** O(对数 N)

**辅助空间:** O(1)

如果您发现上述程序中有任何 bug 或其他解决相同问题的方法，请写评论。