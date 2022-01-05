# 检查一个数字是否有相同数量的置位和未置位位

> 原文:[https://www . geesforgeks . org/check-if-a-number-with-number-of-set-and-unset-bits/](https://www.geeksforgeeks.org/check-if-a-number-has-same-number-of-set-and-unset-bits/)

给定一个数字 N，任务是检查给定数字中的设置位和未设置位的计数是否相同。
**例:**

```
Input: 12
Output: Yes
1100 is the binary representation of 12
which has 2 set and 2 unset bits 

Input: 14
Output: No
```

**方法:**在给定数字的二进制表示中遍历，使用 **n & 1** 检查最左边的位是否被设置。如果 n & 1 返回 1，则最左边的位被置位。对，每次将数字移动 1 来检查下一位。一旦二进制表示被完全遍历，检查设置位和未设置位的数量是否相同。如果相同，则打印“是”，否则打印“否”。
以下是上述方法的实施:

## C++

```
// C++ program to check if a number
// has same number of set and unset bits
#include <bits/stdc++.h>
using namespace std;

// Function to check if a number
// has same setbits and unset bits
bool checkSame(int n)
{
    int set = 0, unset = 0;

    // iterate for all bits of a number
    while (n) {

        // if set
        if (n & 1)
            set++;
        // if unset
        else
            unset++;

        // right shift number by 1
        n = n >> 1;
    }

    // is number of set bits are
    // equal to unset bits
    if (set == unset)
        return true;
    else
        return false;
}

// Driver Code
int main()
{
    int n = 12;

    // function to check
    if (checkSame(n))
        cout << "YES";
    else
        cout << "NO";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if
// a number has same number
// of set and unset bits
import java.io.*;

class GFG
{

// Function to check if a
// number has same setbits
// and unset bits
static boolean checkSame(int n)
{
    int set = 0;
    int unset = 0;

    // iterate for all
    // bits of a number
    while (n > 0)
    {

        // if set
        if ((n & 1) ==  1)
            set++;

        // if unset
        else
            unset++;

        // right shift
        // number by 1
        n = n >> 1;
    }

    // is number of set bits
    // are equal to unset bits
    if (set == unset)
        return true;
    else
        return false;
}

// Driver Code
public static void main (String[] args)
{
int n = 12;

// function to check
if (checkSame(n))
    System.out.println ("YES");
else
    System.out.println("NO");

}
}

// This code is contributed
// by akt_mit
```

## 蟒蛇 3

```
# Python program to check if a number
# has same number of set and unset bits

# Function to check if a number
# has same setbits and unset bits
def checkSame(n):
    set, unset = 0, 0

    # iterate for all bits of a number
    while(n):

        # if set
        if (n and 1):
            set + 1

        # if unset
        else:
            unset += 1

        # right shift number by 1
        n = n >> 1

    # is number of set bits are
    # equal to unset bits
    if (set == unset):
        return True
    else:
        return False

# Driver Code
if __name__ == '__main__':
    n = 12

    # function to check
    if (checkSame(n)):
        print("YES")
    else:
        print("NO")

# This code is contributed
# by 29AjayKumar
```

## C#

```
// C# program to check if
// a number has same number
// of set and unset bits
using System;

public class GFG{

// Function to check if a
// number has same setbits
// and unset bits
static bool checkSame(int n)
{
    int set = 0;
    int unset = 0;

    // iterate for all
    // bits of a number
    while (n > 0)
    {

        // if set
        if ((n & 1) == 1)
            set++;

        // if unset
        else
            unset++;

        // right shift
        // number by 1
        n = n >> 1;
    }

    // is number of set bits
    // are equal to unset bits
    if (set == unset)
        return true;
    else
        return false;
}

// Driver Code

    static public void Main (){
        int n = 12;

    // function to check
    if (checkSame(n))
        Console.WriteLine("YES");
    else
        Console.WriteLine("NO");

    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if a number
// has same number of set and unset bits

// Function to check if a number
// has same setbits and unset bits
function checkSame($n)
{
    $set = 0;
    $unset = 0;

    // iterate for all bits
    // of a number
    while ($n)
    {

        // if set
        if ($n & 1)
            $set++;
        // if unset
        else
            $unset++;

        // right shift number by 1
        $n = $n >> 1;
    }

    // is number of set bits are
    // equal to unset bits
    if ($set == $unset)
        return true;
    else
        return false;
}

// Driver Code
$n = 12;

// function to check
if (checkSame($n))
    echo "YES";
else
    echo "NO";

// This code is contributed
// by Sach_Code
?>
```

## java 描述语言

```
<script>

// Javascript program to check if a number
// has same number of set and unset bits

// Function to check if a number
// has same setbits and unset bits
function checkSame( n)
{
    let set = 0, unset = 0;

    // iterate for all bits of a number
    while (n) {

        // if set
        if (n & 1)
            set++;
        // if unset
        else
            unset++;

        // right shift number by 1
        n = n >> 1;
    }

    // is number of set bits are
    // equal to unset bits
    if (set == unset)
        return true;
    else
        return false;
}

    // driver code 
    let n = 12;

    // function to check
    if (checkSame(n))
        document.write("YES");
    else
       document.write("NO");

  // This code is contributed by jana_sayantan. 
</script>
```

**Output:** 

```
YES
```