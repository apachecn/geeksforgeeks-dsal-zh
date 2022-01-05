# 打印一个严格小于给定数字的数字，使其所有数字都是不同的。

> 原文:[https://www . geesforgeks . org/print-a-number-严格来说-小于给定的数字-这样-它的所有数字都是不同的/](https://www.geeksforgeeks.org/print-a-number-strictly-less-than-a-given-number-such-that-all-its-digits-are-distinct/)

给定一个正数 n，打印一个小于 n 的数字，这样它的所有数字都是不同的。
**例:**

```
Input : 1134
Output : 1098
1098  is the largest number smaller than
1134 such that all digits are distinct.

Input : 4559
Output : 4539
```

这个问题很容易通过计数来解决。首先，循环遍历小于 n 的数字，对于每个数字，使用计数数组计算数字出现的频率。如果所有数字只出现一次，我们就打印这个数字。答案总是存在的，所以不存在无限循环的问题。

## C++

```
// CPP program to find a number less than
// n such that all its digits are distinct
#include <bits/stdc++.h>
using namespace std;

// Function to find a number less than
// n such that all its digits are distinct
int findNumber(int n)
{
    // looping through numbers less than n
    for (int i = n - 1; >=0 ; i--) {

        // initializing a hash array
        int count[10] = { 0 };

        int x = i; // creating a copy of i

        // initializing variables to compare lengths of digits
        int count1 = 0, count2 = 0;

        // counting frequency of the digits
        while (x) {
            count[x % 10]++;
            x /= 10;
            count1++;
        }

        // checking if each digit is present once
        for (int j = 0; j < 10; j++) {
            if (count[j] == 1)
                count2++;
        }        
        if (count1 == count2)
            return i;
    }
}

// Driver code
int main()
{
    int n = 8490;
    cout << findNumber(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find a number less than
// n such that all its digits are distinct

class GFG{
// Function to find a number less than
// n such that all its digits are distinct
static int findNumber(int n)
{
    // looping through numbers less than n
    for (int i = n - 1;i >=0 ; i--) {

        // initializing a hash array
        int[] count=new int[10];

        int x = i; // creating a copy of i

        // initializing variables to compare lengths of digits
        int count1 = 0, count2 = 0;

        // counting frequency of the digits
        while (x>0) {
            count[x % 10]++;
            x /= 10;
            count1++;
        }

        // checking if each digit is present once
        for (int j = 0; j < 10; j++) {
            if (count[j] == 1)
                count2++;
        }        
        if (count1 == count2)
            return i;
    }
    return -1;
}

// Driver code
public static void main(String[] args)
{
    int n = 8490;
    System.out.println(findNumber(n));
}
}
// This code is contributed by mits
```

## 蟒蛇 3

```
# python 3 program to find a number less than
# n such that all its digits are distinct

# Function to find a number less than
# n such that all its digits are distinct
def findNumber(n):
    # looping through numbers less than n
    i = n-1
    while(i>=0):
        # initializing a hash array
        count = [0 for i in range(10)]

        x = i
        # creating a copy of i

        # initializing variables to compare lengths of digits
        count1 = 0
        count2 = 0

        # counting frequency of the digits
        while (x):

            count[x%10] += 1
            x = int(x / 10)
            count1 += 1

        # checking if each digit is present once
        for j in range(0,10,1):
            if (count[j] == 1):
                count2 += 1

        if (count1 == count2):
            return i
        i -= 1

# Driver code
if __name__ == '__main__':

    n = 8490
    print(findNumber(n))

# This code is implemented by
# Surendra_Gangwar
```

## C#

```
// C# program to find a number less than
// n such that all its digits are distinct
using System;

class GFG
{

// Function to find a number less than
// n such that all its digits are distinct
static int findNumber(int n)
{
    // looping through numbers less than n
    for (int i = n - 1; i >= 0; i--)
    {

        // initializing a hash array
        int[] count = new int[10];

        int x = i; // creating a copy of i

        // initializing variables to compare
        // lengths of digits
        int count1 = 0, count2 = 0;

        // counting frequency of the digits
        while (x > 0)
        {
            count[x % 10]++;
            x /= 10;
            count1++;
        }

        // checking if each digit is
        // present once
        for (int j = 0; j < 10; j++)
        {
            if (count[j] == 1)
                count2++;
        }    
        if (count1 == count2)
            return i;
    }
    return -1;
}

// Driver code
static public void Main ()
{
    int n = 8490;
    Console.WriteLine(findNumber(n));
}
}

// This code is contributed by akt_mit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find a number less than
// n such that all its digits are distinct

// Function to find a number less than
// n such that all its digits are distinct
function findNumber($n)
{
    // looping through numbers less than n
    for ($i = $n - 1;$i >= 0 ; $i--)
    {

        // initializing a hash array
        $count = array_fill(0, 10, 0);

        $x = $i; // creating a copy of i

        // initializing variables to
        // compare lengths of digits
        $count1 = 0; $count2 = 0;

        // counting frequency of the digits
        while ($x)
        {
            $count[$x % 10]++;
            $x = (int)($x / 10);
            $count1++;
        }

        // checking if each digit
        // is present once
        for ($j = 0; $j < 10; $j++)
        {
            if ($count[$j] == 1)
                $count2++;
        }    
        if ($count1 == $count2)
            return $i;
    }
}

// Driver code
$n = 8490;
echo findNumber($n);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// Javascript program to find a number less than
// n such that all its digits are distinct

// Function to find a number less than
// n such that all its digits are distinct
function findNumber(n)
{
    // looping through numbers less than n
    for (i = n - 1;i >=0 ; i--) {

        // initializing a hash array
        var count=Array.from({length: 10}, (_, i) => 0);

        var x = i; // creating a copy of i

        // initializing variables to compare lengths of digits
        var count1 = 0, count2 = 0;

        // counting frequency of the digits
        while (x>0) {
            count[x % 10]++;
            x = parseInt(x/10);
            count1++;
        }

        // checking if each digit is present once
        for (j = 0; j < 10; j++) {
            if (count[j] == 1)
                count2++;
        }        
        if (count1 == count2)
            return i;
    }
    return -1;
}

// Driver code
var n = 8490;
document.write(findNumber(n));

// This code is contributed by 29AjayKumar

</script>
```

**Output:** 

```
8479
```