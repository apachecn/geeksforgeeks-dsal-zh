# 位数总和为十的第 n 个数字

> 原文:[https://www . geesforgeks . org/n-th-number-其位数总和为-10/](https://www.geeksforgeeks.org/n-th-number-whose-sum-of-digits-is-ten/)

给定一个整数值 n，求和为 10 的第 n 个正整数。
**例:**

```
Input: n = 2
Output: 28
The first number with sum of digits as
10 is 19\. Second number is 28.

Input: 15
Output: 154
```

**方法 1(简单):**
我们遍历所有的数字。对于每个数字，我们找到数字的总和。当我们找到第 n 个数字的总和为 10 时，我们停止。

## C++

```
// Simple CPP program to find n-th number
// with sum of digits as 10.
#include <bits/stdc++.h>
using namespace std;

int findNth(int n)
{
    int count = 0;

    for (int curr = 1;; curr++) {

        // Find sum of digits in current no.
        int sum = 0;
        for (int x = curr; x > 0; x = x / 10)
            sum = sum + x % 10;

        // If sum is 10, we increment count
        if (sum == 10)
            count++;

        // If count becomes n, we return current
        // number.
        if (count == n)
            return curr;
    }
    return -1;
}

int main()
{
    printf("%d\n", findNth(5));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find n-th number
// with sum of digits as 10.

import java.util.*;
import java.lang.*;

public class GFG {
    public static int findNth(int n)
    {
        int count = 0;
        for (int curr = 1;; curr++) {

            // Find sum of digits in current no.
            int sum = 0;
            for (int x = curr; x > 0; x = x / 10)
                sum = sum + x % 10;

            // If sum is 10, we increment count
            if (sum == 10)
                count++;

            // If count becomes n, we return current
            // number.
            if (count == n)
                return curr;
        }
    }

    public static void main(String[] args)
    {
        System.out.print(findNth(5));
    }
}

// Contributed by _omg
```

## 蟒蛇 3

```
# Python3 program to find n-th number
# with sum of digits as 10.
import itertools

# function to find required number
def findNth(n):

    count = 0

    for curr in itertools.count():
        # Find sum of digits in current no.
        sum = 0
        x = curr
        while(x):
            sum = sum + x % 10
            x = x // 10

        # If sum is 10, we increment count
        if (sum == 10):
            count = count + 1

        # If count becomes n, we return current
        # number.
        if (count == n):
            return curr

    return -1

# Driver program
if __name__=='__main__':
    print(findNth(5))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# program to find n-th number
// with sum of digits as 10.
using System;

class GFG {
    public static int findNth(int n)
    {
        int count = 0;
        for (int curr = 1;; curr++) {

            // Find sum of digits in current no.
            int sum = 0;
            for (int x = curr; x > 0; x = x / 10)
                sum = sum + x % 10;

            // If sum is 10, we increment count
            if (sum == 10)
                count++;

            // If count becomes n, we
            // return current number.
            if (count == n)
                return curr;
        }
    }

    // Driver Code
    static public void Main()
    {
        Console.WriteLine(findNth(5));
    }
}

// This code is contributed
// by Sach_Code
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Simple PHP program to find n-th 
// number with sum of digits as 10. 
function findNth($n) 
{ 
    $count = 0; 

    for ($curr = 1; ; $curr++)
    { 

        // Find sum of digits in 
        // current no. 
        $sum = 0; 
        for ($x = $curr;
             $x > 0; $x = $x / 10) 
            $sum = $sum + $x % 10; 

        // If sum is 10, we increment 
        // count 
        if ($sum == 10) 
            $count++; 

        // If count becomes n, we return 
        // current number. 
        if ($count == $n) 
            return $curr; 
    } 
    return -1; 
} 

// Driver Code
echo findNth(5); 

// This code is contributed by Sach .
?>
```

## java 描述语言

```
<script>

// Simple JavaScript program to find n-th number
// with sum of digits as 10.

function findNth(n)
{
    let count = 0;

    for (let curr = 1;; curr++) {

        // Find sum of digits in current no.
        let sum = 0;
        for (let x = curr; x > 0; x = Math.floor(x / 10))
            sum = sum + x % 10;

        // If sum is 10, we increment count
        if (sum == 10)
            count++;

        // If count becomes n, we return current
        // number.
        if (count == n)
            return curr;
    }
    return -1;
}

    document.write(findNth(5));

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output**

```
55
```

**方法 2(有效率):**
如果我们仔细观察，可以注意到所有 9 的倍数都出现在等差数列 19、28、37、46、55、64、73、82、91、100、109、……
但是，上述数列中有一些数字的位数之和不是 10，例如 100。所以我们不是一个接一个地检查，而是从 19 开始，递增 9。

## C++

```
// Simple CPP program to find n-th number
// with sum of digits as 10.
#include <bits/stdc++.h>
using namespace std;

int findNth(int n)
{
    int count = 0;

    for (int curr = 19;; curr += 9) {

        // Find sum of digits in current no.
        int sum = 0;
        for (int x = curr; x > 0; x = x / 10)
            sum = sum + x % 10;

        // If sum is 10, we increment count
        if (sum == 10)
            count++;

        // If count becomes n, we return current
        // number.
        if (count == n)
            return curr;
    }
    return -1;
}

int main()
{
    printf("%d\n", findNth(5));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find n-th number
// with sum of digits as 10.

import java.util.*;
import java.lang.*;

public class GFG {
    public static int findNth(int n)
    {
        int count = 0;

        for (int curr = 19;; curr += 9) {

            // Find sum of digits in current no.
            int sum = 0;
            for (int x = curr; x > 0; x = x / 10)
                sum = sum + x % 10;

            // If sum is 10, we increment count
            if (sum == 10)
                count++;

            // If count becomes n, we return current
            // number.
            if (count == n)
                return curr;
        }
    }

    public static void main(String[] args)
    {
        System.out.print(findNth(5));
    }
}

// Contributed by _omg
```

## 蟒蛇 3

```
# Python3 program to find n-th 
# number with sum of digits as 10. 
def findNth(n): 
    count = 0;

    curr = 19;

    while (True): 

        # Find sum of digits in
        # current no. 
        sum = 0;
        x = curr;
        while (x > 0):
            sum = sum + x % 10;
            x = int(x / 10);

        # If sum is 10, we increment
        # count 
        if (sum == 10): 
            count+= 1; 

        # If count becomes n, we return 
        # current number. 
        if (count == n): 
            return curr;

        curr += 9;

    return -1; 

# Driver Code
print(findNth(5)); 

# This code is contributed 
# by mits
```

## C#

```
// C# program to find n-th number
// with sum of digits as 10.
using System;

class GFG {
    public static int findNth(int n)
    {
        int count = 0;

        for (int curr = 19;; curr += 9) {

            // Find sum of digits in
            // current no.
            int sum = 0;
            for (int x = curr;
                 x > 0; x = x / 10)
                sum = sum + x % 10;

            // If sum is 10, we increment
            // count
            if (sum == 10)
                count++;

            // If count becomes n, we return
            // current number.
            if (count == n)
                return curr;
        }
    }

    // Driver Code
    static public void Main()
    {
        Console.WriteLine(findNth(5));
    }
}

// This code is contributed
// by Sach_Code
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Simple PHP program to find n-th  
// number with sum of digits as 10. 
function findNth($n) 
{ 
    $count = 0; 

    for ($curr = 19; ;$curr += 9) 
    { 

        // Find sum of digits in
        // current no. 
        $sum = 0; 
        for ($x = $curr; $x > 0;
             $x = (int)$x / 10) 
            $sum = $sum + $x % 10; 

        // If sum is 10, we increment
        // count 
        if ($sum == 10) 
            $count++; 

        // If count becomes n, we return 
        // current number. 
        if ($count == $n) 
            return $curr; 
    } 
    return -1; 
} 

// Driver Code
echo findNth(5); 

// This code is contributed 
// by Sach_Code
?>
```

## java 描述语言

```
<script>

// Simple Javascript program to find n-th 
// number with sum of digits as 10.
function findNth(n)
{
    let count = 0;

    for (let curr = 19; ;curr += 9)
    {

        // Find sum of digits in
        // current no.
        let sum = 0;
        for (let x = curr; x > 0;
             x = parseInt(x / 10))
            sum = sum + x % 10;

        // If sum is 10, we increment
        // count
        if (sum == 10)
            count++;

        // If count becomes n, we return
        // current number.
        if (count == n)
            return curr;
    }
    return -1;
}

// Driver Code
document.write(findNth(5));

// This code is contributed
// by gfgking
</script>
```

**Output**

```
55
```