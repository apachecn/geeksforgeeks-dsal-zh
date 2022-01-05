# 设定位数与 N 相同

> 原文:[https://www.geeksforgeeks.org/number-set-bits-n/](https://www.geeksforgeeks.org/number-set-bits-n/)

给定一个正整数 N，找出有多少严格小于 N 的正整数具有与 N 相同的设置位数。

**示例:**

```
Input : 8
Output :3
Explanation: Binary representation of
8 : 1000, so number of set bits in 8 is 1.
So the integers less than 8 with same number 
of set bits are : 4, 2, 1

Input :1
Output :0

Input :4
Output :2 
```

**进场:**

```
1\. Using __builtin_popcount() inbuilt function, count set bits in N and store into a 
temp variable 
2\. Iterate from n-1 to 1 and also count set bits in i using __builtin_popcount() 
function
3\. Now, compare temp with __builtin_popcount(i)
4\. If both are equal then increment counter variable
5\. Return counter
```

下面是上述方法的实现。

## C++

```
// CPP program to find numbers less than N
// that have same Number Of Set Bits As N
#include <iostream>
using namespace std;

int smallerNumsWithSameSetBits(int n)
{       
    // __builtin_popcount function that count
    // set bits in n
    int temp = __builtin_popcount(n);

    // Iterate from n-1 to 1
    int count = 0;
    for (int i = n - 1; i > 0; i--) {

        // check if the number of set bits
        // equals to temp increment count       
        if (temp == __builtin_popcount(i))
            count++;
    }
    return count;
}

// Driver Code
int main()
{
    int n = 4;
    cout << smallerNumsWithSameSetBits(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find numbers less than N
// that have same Number Of Set Bits As N
class GFG {

    // returns number of set bits in a number
    static int __builtin_popcount(int n)
    {
        int d, t = 0;

        while(n > 0)
        {
            d = n % 2;
            n = n / 2;
            if(d == 1)
                t++;
        }
        return t;
    }

    static int smallerNumsWithSameSetBits(int n)
    {    
        // __builtin_popcount function that count
        // set bits in n
        int temp = __builtin_popcount(n);

        // Iterate from n-1 to 1
        int count = 0;
        for (int i = n - 1; i > 0; i--) {

            // check if the number of set bits
            // equals to temp increment count    
            if (temp == __builtin_popcount(i))
                count++;
        }
        return count;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 4;
        System.out.println(
            smallerNumsWithSameSetBits(n));
    }
}

// This code is contributed by Arnab Kundu.
```

## 蟒蛇 3

```
# Python3 program to find numbers
# less than N that have same
# Number Of Set Bits As N
def __builtin_popcount(n) :
    t = 0   
    while(n > 0) :
        d = n % 2
        n = int(n / 2)
        if(d == 1) :
            t = t + 1
    return t

def smallerNumsWithSameSetBits(n) :   

    # __builtin_popcount function
    # that count set bits in n
    temp = __builtin_popcount(n)

    # Iterate from n-1 to 1
    count = 0
    for i in range(n-1,0,-1) :    

        # check if the number of
        # set bits equals to temp
        # increment count    
        if (temp == __builtin_popcount(i)) :
            count = count + 1
    return count

# Driver Code
n = 4
print (smallerNumsWithSameSetBits(n))

# This code is contributed by
# Manish Shaw(manishshaw1)
```

## C#

```
// C# program to find numbers less than N
// that have same Number Of Set Bits As N
using System;

class GFG {

    // returns number of set bits in a number
    static int __builtin_popcount(int n)
    {
        int d, t = 0;

        while(n > 0)
        {
            d = n % 2;
            n = n / 2;
            if(d == 1)
                t++;
        }
        return t;
    }

    static int smallerNumsWithSameSetBits(int n)
    {    
        // __builtin_popcount function that count
        // set bits in n
        int temp = __builtin_popcount(n);

        // Iterate from n-1 to 1
        int count = 0;
        for (int i = n - 1; i > 0; i--) {

            // check if the number of set bits
            // equals to temp increment count    
            if (temp == __builtin_popcount(i))
                count++;
        }
        return count;
    }

    // Driver Code
    static public void Main(String []args)
    {
        int n = 4;
        Console.WriteLine(
            smallerNumsWithSameSetBits(n));
    }
}

// This code is contributed by Arnab Kundu.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find numbers
// less than N that have same
// Number Of Set Bits As N
function __builtin_popcount($n)
{
    $t = 0;    
    while($n > 0)
    {
        $d = $n % 2;
        $n = intval($n / 2);
        if($d == 1)
            $t++;
    }
    return $t;
}
function smallerNumsWithSameSetBits($n)
{    
    // __builtin_popcount function
    // that count set bits in n
    $temp = __builtin_popcount($n);

    // Iterate from n-1 to 1
    $count = 0;
    for ($i = $n - 1; $i > 0; $i--)
    {

        // check if the number of
        // set bits equals to temp
        // increment count    
        if ($temp == __builtin_popcount($i))
            $count++;
    }
    return $count;
}

// Driver Code
$n = 4;
echo (smallerNumsWithSameSetBits($n));

// This code is contributed by
// Manish Shaw(manishshaw1)
?>
```

## java 描述语言

```
<script>

// Javascript program to find numbers less than N
// that have same Number Of Set Bits As N

// returns number of set bits in a number
function __builtin_popcount(n)
{
    var d, t = 0;

    while(n > 0)
    {
        d = n % 2;
        n = parseInt(n / 2);
        if(d == 1)
            t++;
    }
    return t;
}

function smallerNumsWithSameSetBits(n)
{       
    // __builtin_popcount function that count
    // set bits in n
    var temp = __builtin_popcount(n);

    // Iterate from n-1 to 1
    var count = 0;
    for (var i = n - 1; i > 0; i--) {

        // check if the number of set bits
        // equals to temp increment count       
        if (temp == __builtin_popcount(i))
            count++;
    }
    return count;
}

// Driver Code
var n = 4;
document.write( smallerNumsWithSameSetBits(n));

</script>
```

**Output:** 

```
2
```