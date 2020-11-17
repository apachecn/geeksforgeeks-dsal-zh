# 计算范围内的数字数量，它与`q`的乘积不相等

> 原文：[https://www.geeksforgeeks.org/count-numbers-in-range-such-that-digits-in-it-and-its-product-with-q-are-unequal/](https://www.geeksforgeeks.org/count-numbers-in-range-such-that-digits-in-it-and-its-product-with-q-are-unequal/)

给定一系列数字`[l, r]`和一个整数`q`。 任务是对给定范围内的所有此类数字进行计数，以使该数字的任何数字与乘积中具有给定数字`q`的任何数字都不匹配。

**示例**：

```
Input : l = 10, r = 12, q = 2
Output : 1
10*2 = 20 which has 0 as same digit
12*2 = 24 which as 2 as same digit
11*2 = 22 no same digit

Input : l = 5, r = 15, q = 2
Output : 9

```

**来源**：[高盛面试集 46](https://www.geeksforgeeks.org/goldman-sachs-interview-experience-set-46-experienced/)

的想法是从`l`到`r`循环运行，以生成范围内的所有数字，并将每个此类数字`n`转换为`q`，即使用[`to_string()`](https://www.geeksforgeeks.org/stdto_string-in-cpp/)方法对字符串进行`n * q`，然后使用基本字符串哈希检查`string2`中是否存在`string2`中的任何字符。

下面是上述方法的实现：

## C++

```cpp

// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if all of the digits
// in a number and it's product with q
// are unequal or not
bool checkIfUnequal(int n, int q)
{

    // convert first number into string
    string s1 = to_string(n);
    int a[26] = { 0 };

    // Insert elements from 1st number
    // to hash
    for (int i = 0; i < s1.size(); i++)
        a[s1[i] - '0']++;

    // Calculate corresponding product
    int prod = n * q;

    // Convert the product to string
    string s2 = to_string(prod);

    // Using the hash check if any digit of
    // product matches with the digits of
    // input number
    for (int i = 0; i < s2.size(); i++) 
    {
        // If yes, return false
        if (a[s2[i] - '0'])
            return false;
    }

    // Return true
    return true;
}

// Function to count numbers in the range [l, r]
// such that all of the digits of the number and
// it's product with q are unequal
int countInRange(int l, int r, int q)
{
    int count = 0;

    for (int i = l; i <= r; i++) {
        // check for every number between l and r
        if (checkIfUnequal(i, q))
            count++;
    }

    return count;
}

// Driver Code
int main()
{

    int l = 10, r = 12, q = 2;

    // Function Call
    cout << countInRange(l, r, q);
    return 0;
}

```

## Java

```java

// Java program for above approach
class GfG {

    // Function to check if all of the digits
    // in a number and it's product with q
    // are unequal or not
    static boolean checkIfUnequal(int n, int q)
    {

        // convert first number into string
        String s1 = Integer.toString(n);
        int a[] = new int[26];

        // Insert elements from 1st number
        // to hash
        for (int i = 0; i < s1.length(); i++)
            a[s1.charAt(i) - '0']++;

        // Calculate corresponding product
        int prod = n * q;

        // Convert the product to string
        String s2 = Integer.toString(prod);

        // Using the hash check if any digit of
        // product matches with the digits of
        // input number
        for (int i = 0; i < s2.length(); i++) 
        {
            // If yes, return false
            if (a[s2.charAt(i) - '0'] > 0)
                return false;
        }
        // else, return true
        return true;
    }

    // Function to count numbers in the range [l, r]
    // such that all of the digits of the number and
    // it's product with q are unequal
    static int countInRange(int l, int r, int q)
    {
        int count = 0;

        for (int i = l; i <= r; i++) {

            // check for every number between l and r
            if (checkIfUnequal(i, q))
                count++;
        }

        return count;
    }

    // Driver Code
    public static void main(String[] args)
    {

        int l = 10, r = 12, q = 2;

        // Function Call
        System.out.println(countInRange(l, r, q));
    }
}

```

## Python3

```py

# Python 3 program for above approach

# Function to check if all of the digits
# in a number and it's product with q
# are unequal or not
def checkIfUnequal(n, q):

    # convert first number into string
    s1 = str(n)
    a = [0 for i in range(26)]

    # Insert elements from 1st number
    # to hash
    for i in range(0, len(s1), 1):
        a[ord(s1[i]) - ord('0')] += 1

    # Calculate corresponding product
    prod = n * q

    # Convert the product to string
    s2 = str(prod)

    # Using the hash check if any digit of
    # product matches with the digits of
    # input number
    for i in range(0, len(s2), 1):

        # If yes, return false
        if (a[ord(s2[i]) - ord('0')]):
            return False

    # Return true
    return True

# Function to count numbers in the range [l, r]
# such that all of the digits of the number and
# it's product with q are unequal
def countInRange(l, r, q):
    count = 0

    for i in range(l, r + 1, 1):

        # check for every number between l and r
        if (checkIfUnequal(i, q)):
            count += 1

    return count

# Driver Code
if __name__ == '__main__':
    l = 10
    r = 12
    q = 2

    # Function call
    print(countInRange(l, r, q))

# This code is contributed by
# Sahil_Shelangia

```

## C#

```cs

// C# program for above approach
using System;

class GfG {

    // Function to check if all of the digits
    // in a number and it's product with q
    // are unequal or not
    static bool checkIfUnequal(int n, int q)
    {

        // convert first number into string
        string s1 = n.ToString();
        int[] a = new int[26];

        // Insert elements from 1st number
        // to hash
        for (int i = 0; i < s1.Length; i++)
            a[s1[i] - '0']++;

        // Calculate corresponding product
        int prod = n * q;

        // Convert the product to string
        string s2 = prod.ToString();

        // Using the hash check if any digit of
        // product matches with the digits of
        // input number
        for (int i = 0; i < s2.Length; i++)
        {
            // If yes, return false
            if (a[s2[i] - '0'])
                return false;
        }

        // Else, return true
        return true;
    }

    // Function to count numbers in the range [l, r]
    // such that all of the digits of the number and
    // it's product with q are unequal
    static int countInRange(int l, int r, int q)
    {
        int count = 0;

        for (int i = l; i <= r; i++) 
        {
            // check for every number between l and r
            if (checkIfUnequal(i, q))
                count++;
        }

        return count;
    }

    // Driver Code
    public static void Main()
    {

        int l = 10, r = 12, q = 2;

        // Function call
        Console.WriteLine(countInRange(l, r, q));
    }
}

// This code is contributed bt Archana_kumari

```

## PHP

```php

// PHP program for above code

// Function to check if all of the digits
// in a number and it's product with q
// are unequal or not
function checkIfUnequal($n, $q)
{
    // convert first number into string
    $s1 = strval($n);
    $a = array_fill(0, 26, NULL);

    // Insert elements from 1st number
    // to hash
    for ($i = 0; $i < strlen($s1); $i++)
        $a[ord($s1[$i]) - ord('0')]++;

    // Calculate corresponding product
    $prod = $n * $q;

    // Convert the product to string
    $s2 = strval($prod);

    // Using the hash check if any digit of
    // product matches with the digits of
    // input number
    for ($i = 0; $i < strlen($s2); $i++)
    {

       // If yes, return false
       if ($a[ord($s2[$i]) - ord('0')]) 
            return false;
    }

    // Else, return true
    return true;
}

// Function to count numbers in the range 
// [l, r] such that all of the digits of the
// number and it's product with q are unequal
function countInRange($l, $r, $q)
{
    $count = 0;

    for ($i = $l; $i <= $r; $i++) 
    {
        // check for every number between l and r
        if (checkIfUnequal($i, $q))
            $count++;
    }

    return $count;
}

// Driver Code
$l = 10;
$r = 12;
$q = 2;

// Function call
echo countInRange($l, $r, $q);

// This code is contributed by ita_c
?>

```

**输出**：

```
1
```



* * *

* * *



