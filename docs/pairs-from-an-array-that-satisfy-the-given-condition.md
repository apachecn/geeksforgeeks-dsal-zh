# 满足给定条件的数组中的对

> 原文:[https://www . geeksforgeeks . org/满足给定条件的数组对/](https://www.geeksforgeeks.org/pairs-from-an-array-that-satisfy-the-given-condition/)

给定一个数组 **arr[]** ，任务是计算数组中所有有效的对。如果**func(arr[I])+func(arr[j])= func(XOR(arr[I]，arr[j]) )** 其中 **func(x)** 返回 **x** 中**设置位**的个数，则一对 **(arr[i]，arr[j])** 被认为是有效的。

**示例:**

> **输入:** arr[] = {2，3，4，5，6}
> **输出:** 3
> (2，4)、(2，5)和(3，4)是唯一有效的对。
> 
> **输入:** arr[] = {12，13，34，25，6 }
> T3】输出: 4

**方法:**迭代每一个可能的对，检查该对是否满足给定的条件。如果条件满足，则更新**计数=计数+ 1** 。最后打印**计数**。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the number
// of set bits in n
int setBits(int n)
{
    int count = 0;

    while (n) {
        n = n & (n - 1);
        count++;
    }
    return count;
}

// Function to return the count of required pairs
int countPairs(int a[], int n)
{
    int count = 0;

    for (int i = 0; i < n - 1; i++) {

        // Set bits for first element of the pair
        int setbits_x = setBits(a[i]);

        for (int j = i + 1; j < n; j++) {

            // Set bits for second element of the pair
            int setbits_y = setBits(a[j]);

            // Set bits of the resultant number which is
            // the XOR of both the elements of the pair
            int setbits_xor_xy = setBits(a[i] ^ a[j]);

            // If the condition is satisfied
            if (setbits_x + setbits_y == setbits_xor_xy)

                // Increment the count
                count++;
        }
    }

    // Return the total count
    return count;
}

// Driver code
int main()
{
    int a[] = { 2, 3, 4, 5, 6 };

    int n = sizeof(a) / sizeof(a[0]);

    cout << countPairs(a, n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

// Function to return the number
// of set bits in n
static int setBits(int n)
{
    int count = 0;

    while (n > 0)
    {
        n = n & (n - 1);
        count++;
    }
    return count;
}

// Function to return the count of
// required pairs
static int countPairs(int a[], int n)
{
    int count = 0;

    for (int i = 0; i < n - 1; i++)
    {

        // Set bits for first element
        // of the pair
        int setbits_x = setBits(a[i]);

        for (int j = i + 1; j < n; j++)
        {

            // Set bits for second element
            // of the pair
            int setbits_y = setBits(a[j]);

            // Set bits of the resultant number which is
            // the XOR of both the elements of the pair
            int setbits_xor_xy = setBits(a[i] ^ a[j]);

            // If the condition is satisfied
            if (setbits_x + setbits_y == setbits_xor_xy)

                // Increment the count
                count++;
        }
    }

    // Return the total count
    return count;
}

    // Driver code
    public static void main (String[] args)
    {

        int []a = { 2, 3, 4, 5, 6 };
        int n = a.length;
        System.out.println(countPairs(a, n));
    }
}

// This code is contributed by ajit.
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return the number
# of set bits in n
def setBits(n):
    count = 0

    while (n):
        n = n & (n - 1)
        count += 1

    return count

# Function to return the count
# of required pairs
def countPairs(a, n):
    count = 0

    for i in range(0, n - 1, 1):

        # Set bits for first element
        # of the pair
        setbits_x = setBits(a[i])

        for j in range(i + 1, n, 1):

            # Set bits for second element
            # of the pair
            setbits_y = setBits(a[j])

            # Set bits of the resultant number
            # which is the XOR of both the
            # elements of the pair
            setbits_xor_xy = setBits(a[i] ^ a[j]);

            # If the condition is satisfied
            if (setbits_x +
                setbits_y == setbits_xor_xy):

                # Increment the count
                count += 1

    # Return the total count
    return count

# Driver code
if __name__ == '__main__':
    a = [2, 3, 4, 5, 6]

    n = len(a)
    print(countPairs(a, n))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# implementation of the approach
using System;
class GFG
{

// Function to return the number
// of set bits in n
static int setBits(int n)
{
    int count = 0;

    while (n > 0)
    {
        n = n & (n - 1);
        count++;
    }
    return count;
}

// Function to return the count of
// required pairs
static int countPairs(int []a, int n)
{
    int count = 0;

    for (int i = 0; i < n - 1; i++)
    {

        // Set bits for first element
        // of the pair
        int setbits_x = setBits(a[i]);

        for (int j = i + 1; j < n; j++)
        {

            // Set bits for second element
            // of the pair
            int setbits_y = setBits(a[j]);

            // Set bits of the resultant number which is
            // the XOR of both the elements of the pair
            int setbits_xor_xy = setBits(a[i] ^ a[j]);

            // If the condition is satisfied
            if (setbits_x + setbits_y == setbits_xor_xy)

                // Increment the count
                count++;
        }
    }

    // Return the total count
    return count;
}

// Driver code
public static void Main()
{
    int []a = { 2, 3, 4, 5, 6 };

    int n = a.Length;

    Console.Write(countPairs(a, n));
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the number
// of set bits in n
function setBits($n)
{
    $count = 0;

    while ($n)
    {
        $n = $n & ($n - 1);
        $count++;
    }
    return $count;
}

// Function to return the count of
// required pairs
function countPairs(&$a, $n)
{
    $count = 0;

    for ($i = 0; $i < $n - 1; $i++)
    {

        // Set bits for first element
        // of the pair
        $setbits_x = setBits($a[$i]);

        for ($j = $i + 1; $j < $n; $j++)
        {

            // Set bits for second element of the pair
            $setbits_y = setBits($a[$j]);

            // Set bits of the resultant number which is
            // the XOR of both the elements of the pair
            $setbits_xor_xy = setBits($a[$i] ^ $a[$j]);

            // If the condition is satisfied
            if ($setbits_x +
                $setbits_y == $setbits_xor_xy)

                // Increment the count
                $count++;
        }
    }

    // Return the total count
    return $count;
}

// Driver code
$a = array(2, 3, 4, 5, 6 );
$n = sizeof($a) / sizeof($a[0]);
echo countPairs($a, $n);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the number
// of set bits in n
function setBits(n)
{
    let count = 0;

    while (n > 0)
    {
        n = n & (n - 1);
        count++;
    }
    return count;
}

// Function to return the count of
// required pairs
function countPairs(a, n)
{
    let count = 0;

    for(let i = 0; i < n - 1; i++)
    {

        // Set bits for first element
        // of the pair
        let setbits_x = setBits(a[i]);

        for(let j = i + 1; j < n; j++)
        {

            // Set bits for second element
            // of the pair
            let setbits_y = setBits(a[j]);

            // Set bits of the resultant number which is
            // the XOR of both the elements of the pair
            let setbits_xor_xy = setBits(a[i] ^ a[j]);

            // If the condition is satisfied
            if (setbits_x + setbits_y == setbits_xor_xy)

                // Increment the count
                count++;
        }
    }

    // Return the total count
    return count;
}

// Driver code
let a = [ 2, 3, 4, 5, 6 ];
let n = a.length;

document.write(countPairs(a, n));

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
3
```