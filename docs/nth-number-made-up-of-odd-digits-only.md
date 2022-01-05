# 仅由奇数组成的第 n 个数字

> 原文:[https://www . geesforgeks . org/n-number-仅由奇数位组成/](https://www.geeksforgeeks.org/nth-number-made-up-of-odd-digits-only/)

给定一个整数 **N** ，任务是找到仅由奇数位(1，3，5，7，9)组成的**N**号。
由奇数组成的前几个数字是 1，3，5，7，9，11，13，15，17，19，31，…

**示例:**

> **输入:** N = 7
> **输出:** 13
> 1、3、5、7、9、11、13
> 13 是系列中的第 7 个数字
> 
> **输入:**N = 10
> T3】输出: 19

**接近 1(简单):**从 **1** 开始，继续检查号码是否仅由奇数(1、3、5、7、9)组成，当发现第 n 个这样的号码时停止。

下面是上述方法的实现:

## C++

```
// C++ program to find nth number made up of odd digits only
#include <bits/stdc++.h>
using namespace std;

// Function to return nth number made up of odd digits only
int findNthOddDigitNumber(int n)
{

    // Variable to keep track of how many
    // such elements have been found
    int count = 0;
    for (int i = 1;; i++) {
        int num = i;
        bool isMadeOfOdd = true;

        // Checking each digit of the number
        while (num != 0) {

            // If 0, 2, 4, 6 or 8 is found
            // then the number is not made up of odd digits
            if (num % 10 == 0
                || num % 10 == 2
                || num % 10 == 4
                || num % 10 == 6
                || num % 10 == 8) {
                isMadeOfOdd = false;
                break;
            }

            num = num / 10;
        }

        // If the number is made up of odd digits only
        if (isMadeOfOdd == true)
            count++;

        // If it is the nth number
        if (count == n)
            return i;
    }
}

// Driver Code
int main()
{
    int n = 10;
    cout << findNthOddDigitNumber(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find nth number
// made up of odd digits only

import java.io.*;

class GFG {
    // Function to return nth number made up of odd digits only
static int findNthOddDigitNumber(int n)
{

    // Variable to keep track of how many
    // such elements have been found
    int count = 0;
    for (int i = 1;; i++) {
        int num = i;
        boolean isMadeOfOdd = true;

        // Checking each digit of the number
        while (num != 0) {

            // If 0, 2, 4, 6 or 8 is found
            // then the number is not made up of odd digits
            if (num % 10 == 0
                || num % 10 == 2
                || num % 10 == 4
                || num % 10 == 6
                || num % 10 == 8) {
                isMadeOfOdd = false;
                break;
            }

            num = num / 10;
        }

        // If the number is made up of odd digits only
        if (isMadeOfOdd == true)
            count++;

        // If it is the nth number
        if (count == n)
            return i;
    }
}

// Driver Code

    public static void main (String[] args) {
    int n = 10;
    System.out.println (findNthOddDigitNumber(n));

    }
//This code is contributed by ajit   
}
```

## 蟒蛇 3

```
# Python3 program to find nth number
# made up of odd digits only

# Function to return nth number made
# up of odd digits only
def findNthOddDigitNumber(n) :

    # Variable to keep track of how many
    # such elements have been found
    count = 0

    i = 1
    while True :
        num = i
        isMadeOfOdd = True

        # Checking each digit of the number
        while num != 0 :

            # If 0, 2, 4, 6 or 8 is found
            # then the number is not made
            # up of odd digits
            if (num % 10 == 0 or num % 10 == 2 or
                num % 10 == 4 or num % 10 == 6 or
                num % 10 == 8) :

                    isMadeOfOdd = False
                    break

            num /= 10

        # If the number is made up of
        # odd digits only
        if isMadeOfOdd == True :
            count += 1

        # If it is the nth number
        if count == n :
            return i

        i += 1

# Driver code
if __name__ == "__main__" :

    n = 10

    # Function call
    print(findNthOddDigitNumber(n))

# This code is contributed by Ryuga
```

## C#

```
// C# program to find nth number
// made up of odd digits only
using System;

class GFG
{

// Function to return nth number
// made up of odd digits only
static int findNthOddDigitNumber(int n)
{

    // Variable to keep track of
    // how many such elements have
    // been found
    int count = 0;
    for (int i = 1;; i++)
    {
        int num = i;
        bool isMadeOfOdd = true;

        // Checking each digit
        // of the number
        while (num != 0)
        {

            // If 0, 2, 4, 6 or 8 is found
            // then the number is not made
            // up of odd digits
            if (num % 10 == 0 || num % 10 == 2 ||
                num % 10 == 4 || num % 10 == 6 ||
                num % 10 == 8)
            {
                isMadeOfOdd = false;
                break;
            }

            num = num / 10;
        }

        // If the number is made up of
        // odd digits only
        if (isMadeOfOdd == true)
            count++;

        // If it is the nth number
        if (count == n)
            return i;
    }
}

// Driver Code
static public void Main ()
{
    int n = 10;
    Console.WriteLine(findNthOddDigitNumber(n));
}
}

// This code is contributed
// by Ajit Deshpal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find nth number
// made up of odd digits only

// Function to return nth number
// made up of odd digits only
function findNthOddDigitNumber($n)
{
    // Variable to keep track of how many
    // such elements have been found
    $count = 0;

    $i = 1;
    while (true)
    {
        $num = $i;
        $isMadeOfOdd = true;

        // Checking each digit of
        // the number
        while ($num != 0)
        {

            // If 0, 2, 4, 6 or 8 is found
            // then the number is not made
            // up of odd digits
            if ($num % 10 == 0 or $num % 10 == 2 or
                $num % 10 == 4 or $num % 10 == 6 or
                $num % 10 == 8)
            {
                $isMadeOfOdd = false;
                break;
            }
            $num = (int)($num / 10);
        }

        // If the number is made up of
        // odd digits only
        if ($isMadeOfOdd == true)
            $count += 1;

        // If it is the nth number
        if ($count == $n)
            return $i;

        $i += 1;
    }
}

// Driver code
$n = 10;

// Function call
print(findNthOddDigitNumber($n));

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript program to find nth
// number made up of odd digits only

// Function to return nth number
// made up of odd digits only
function findNthOddDigitNumber(n)
{

    // Variable to keep track of how many
    // such elements have been found
    let count = 0;
    for(let i = 1;; i++)
    {
        let num = i;
        let isMadeOfOdd = true;

        // Checking each digit of the number
        while (num != 0)
        {

            // If 0, 2, 4, 6 or 8 is found
            // then the number is not made
            // up of odd digits
            if (num % 10 == 0 ||
                num % 10 == 2 ||
                num % 10 == 4 ||
                num % 10 == 6 ||
                num % 10 == 8)
            {
                isMadeOfOdd = false;
                break;
            }
            num = Math.floor(num / 10);
        }

        // If the number is made up of
        // odd digits only
        if (isMadeOfOdd == true)
            count++;

        // If it is the nth number
        if (count === n)
            return i;
    }
}

// Driver Code
let n = 10;

document.write(findNthOddDigitNumber(n));

// This code is contributed by Manoj.

</script>
```

**Output:** 

```
19
```

**方法 2(基于队列):**想法是生成所有只包含奇数的数字(小于 n)。如何用奇数生成所有小于 n 的数字？我们用队列来做这个。最初，我们将“1”、“3”、“5”、“7”和“9”推送到队列中。然后我们运行一个循环，同时处理的元素数小于 n。我们逐个弹出一个项目，对于每个弹出的项目 x，我们生成下一个数字 x*10 + 1、x*10 + 3、x*10 + 5、x*10 + 7 和 x*10 + 9。我们把这些新数字排成队列。该方法的时间复杂度为 O(n)
请参考以下帖子了解该方法的实施情况。
[小于 N 的二进制数字计数](https://www.geeksforgeeks.org/count-binary-digit-numbers-smaller-n/)