# 计数数字与其数字和之差大于特定值的数字

> 原文:[https://www . geesforgeks . org/count-numbers-difference-number-digital-sum-greater-specific-value/](https://www.geeksforgeeks.org/count-numbers-difference-number-digit-sum-greater-specific-value/)

给定一个正值 N，我们需要找到小于 N 的数的计数，使得数与其位数之和的差大于或等于给定的特定值 diff。
示例:

```
Input : N = 13, diff = 2
Output : 4
Then 10, 11, 12 and 13 satisfy the given
condition shown below,
10 – sumofdigit(10) = 9 >= 2
11 – sumofdigit(11) = 9 >= 2
12 – sumofdigit(12) = 9 >= 2
13 – sumofdigit(13) = 9 >= 2  
Whereas no number from 1 to 9 satisfies 
above equation so final result will be 4
```

我们可以通过观察一个事实来解决这个问题，对于一个小于 N 的数 k，

```

if k – sumofdigit(k) >= diff then
above equation will be true for (k+1)
also because we know that sumofdigit(k+1)
is not greater than sumofdigit(k) + 1
so, k + 1 - sumofdigit(k + 1) >= 
k - sumofdigit(k)
but we know that right side of above 
inequality is greater than diff, 
so left side will also be greater than 
diff.
```

所以，最后我们可以说，如果一个数 k 满足差分条件，那么(k + 1)也将满足相同的方程，所以我们的工作是找到满足差分条件的最小数，那么所有大于这个数的数，直到 N，都将满足这个条件，所以我们的答案将是 N，我们找到的最小数。
我们可以利用二分搜索法找到满足这个条件的最小数，所以解的总时间复杂度为 O(log N)

## C++

```
/* C++ program to count total numbers which
have difference with sum of digits greater
than specific value */
#include <bits/stdc++.h>
using namespace std;

// Utility method to get sum of digits of K
int sumOfDigit(int K)
{
    // loop until K is not zero
    int sod = 0;
    while (K)
    {
        sod += K % 10;
        K /= 10;
    }
    return sod;
}

// method returns count of numbers smaller than N,
// satisfying difference condition
int totalNumbersWithSpecificDifference(int N, int diff)
{
    int low = 1, high = N;

    // binary search while loop   
    while (low <= high)
    {
        int mid = (low + high) / 2;

        /* if difference between number and its sum
        of digit is smaller than given difference
        then smallest number will be on left side */
        if (mid - sumOfDigit(mid) < diff)       
            low = mid + 1;

        /* if difference between number and its sum
        of digit is greater than or equal to given
        difference then smallest number will be on
        right side */
        else       
            high = mid - 1;       
    }

    // return the difference between 'smallest number
    // found' and 'N' as result
    return (N - high);
}

// Driver code to test above methods
int main()
{
    int N = 13;
    int diff = 2;

    cout << totalNumbersWithSpecificDifference(N, diff);   
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*  Java program to count total numbers which
   have difference with sum of digits greater
   than specific value */

class Test
{
    //  Utility method to get sum of digits of K
    static int sumOfDigit(int K)
    {
        //  loop until K is not zero
        int sod = 0;
        while (K != 0)
        {
            sod += K % 10;
            K /= 10;
        }
        return sod;
    }

    // method returns count of numbers smaller than N,
    // satisfying difference condition
    static int totalNumbersWithSpecificDifference(int N, int diff)
    {
        int low = 1, high = N;

        //  binary search while loop   
        while (low <= high)
        {
            int mid = (low + high) / 2;

            /* if difference between number and its sum
               of digit is smaller than given difference
               then  smallest number will be on left side */
            if (mid - sumOfDigit(mid) < diff)       
                low = mid + 1;

            /* if difference between number and its sum
               of digit is greater than or equal to given
               difference then  smallest number will be on
               right side */
            else      
                high = mid - 1;       
        }

        // return the difference between 'smallest number
        // found' and 'N' as result
        return (N - high);
    }

    // Driver method
    public static void main(String args[])
    {
        int N = 13;
        int diff = 2;

        System.out.println(totalNumbersWithSpecificDifference(N, diff));
    }
}
```

## 蟒蛇 3

```
# Python program to count total numbers which
# have difference with sum of digits greater
# than specific value

# Utility method to get sum of digits of K
def sumOfDigit(K):

    # loop until K is not zero
    sod = 0
    while (K):

        sod =sod + K % 10
        K =K // 10

    return sod

# method returns count of
# numbers smaller than N,
# satisfying difference condition
def totalNumbersWithSpecificDifference(N,diff):

    low = 1
    high = N

    # binary search while loop   
    while (low <= high):

        mid = (low + high) // 2

        ''' if difference between number and its sum
        of digit is smaller than given difference
        then smallest number will be on left side'''
        if (mid - sumOfDigit(mid) < diff):       
            low = mid + 1

        # if difference between number and its sum
        # of digit greater than equal to given
        # difference then smallest number will be on
        # right side   
        else:

            high = mid - 1       

    # return the difference between 'smallest number
    # found' and 'N' as result
    return (N - high)

# Driver code to test above methods
N = 13
diff = 2

print(totalNumbersWithSpecificDifference(N, diff))   

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# program to count total numbers
// which have difference with sum of 
// digits greater than specific value
using System;

class Test {

    // Utility method to get sum
    // of digits of K
    static int sumOfDigit(int K)
    {

        // loop until K is not zero
        int sod = 0;
        while (K != 0)
        {
            sod += K % 10;
            K /= 10;
        }
        return sod;
    }

    // method returns count of numbers
    // smaller than N, satisfying
    // difference condition
    static int totalNumbersWithSpecificDifference(int N,
                                                  int diff)
    {
        int low = 1, high = N;

        // binary search while loop
        while (low <= high)
        {
            int mid = (low + high) / 2;

            // if difference between number and
            // its sum of digit is smaller than
            // given difference then smallest
            // number will be on left side
            if (mid - sumOfDigit(mid) < diff)    
                low = mid + 1;

            // if difference between number and 
            // its sum of digit is greater than 
            // or equal to given difference then 
            // smallest number will be on right side
            else   
                high = mid - 1;    
        }

        // return the difference between
        // 'smallest number found'
        // and 'N' as result
        return (N - high);
    }

    // Driver code
    public static void Main()
    {
        int N = 13;
        int diff = 2;

        Console.Write(totalNumbersWithSpecificDifference(N, diff));
    }
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count total numbers which
// have difference with sum of digits greater
// than specific value

// method to get sum of digits of K
function sumOfDigit($K)
{

    // loop until K is not zero
    $sod = 0;
    while ($K)
    {
        $sod += $K % 10;
        $K /= 10;
    }
    return $sod;
}

// method returns count of
// numbers smaller than N,
// satisfying difference condition
function totalNumbersWithSpecificDifference($N, $diff)
{
    $low = 1; $high = $N;

    // binary search while loop
    while ($low <= $high)
    {
        $mid = floor(($low + $high) / 2);

        /* if difference between number and its sum
           of digit is smaller than given difference
           then smallest number will be on left side */
        if ($mid - sumOfDigit($mid) < $diff)    
            $low = $mid + 1;

        /* if difference between number and its sum
           of digit is greater than or equal to given
           difference then smallest number will be on
           right side */
        else   
            $high = $mid - 1;    
    }

    // return the difference
    // between 'smallest number
    // found' and 'N' as result
    return ($N - $high);
}

// Driver Code
$N = 13;
$diff = 2;
echo totalNumbersWithSpecificDifference($N, $diff);

// This code is contributed by nitin mittal
?>
```

## java 描述语言

```
<script>

// javascript program to
// count total numbers which
// have difference with sum
// of digits greater
// than specific value

// method to get sum of digits of K
function sumOfDigit(K)
{

    // loop until K is not zero
    let sod = 0;
    while (K)
    {
        sod += K % 10;
        K /= 10;
    }
    return sod;
}

// method returns count of
// numbers smaller than N,
// satisfying difference condition
function
totalNumbersWithSpecificDifference(N, diff)
{
    let low = 1;
    let high = N;

    // binary search while loop
    while (low <= high)
    {
        let mid = Math.floor((low + high) / 2);

        /* if difference between number and its sum
        of digit is smaller than given difference
        then smallest number will be on left side */
        if (mid - sumOfDigit(mid) < diff)   
            low = mid + 1;

        /* if difference between number and its sum
        of digit is greater than or equal to given
        difference then smallest number will be on
        right side */
        else   
            high = mid - 1;   
    }

    // return the difference
    // between 'smallest number
    // found' and 'N' as result
    return (N - high);
}

// Driver Code
let N = 13;
let diff = 2;
document.write(
totalNumbersWithSpecificDifference(N, diff)
);

// This code is contributed by Bobby

</script>
```

**输出:**

```
4
```

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。