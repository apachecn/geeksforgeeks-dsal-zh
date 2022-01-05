# 数组中平方根存在的元素之和

> 原文:[https://www . geeksforgeeks . org/数组中存在平方根的元素之和/](https://www.geeksforgeeks.org/sum-of-elements-whose-square-root-is-present-in-the-array/)

给定一个数组 **arr[]** ，任务是从给定的数组中找到所有那些元素的和，这些元素的平方根在同一个数组中。

**示例:**

> **输入:** arr[] = {1，2，3，4，6，9，10}
> **输出:** 13
> 4 和 9 是数组中仅有的平方根 2 和 3 的数字
> 
> **输入:** arr[] = {4，2，36，6，10，100 }
> T3】输出: 140

**天真方法:**要找到给定数组中平方根元素的和，通过从 **arr[0]** 迭代到 **arr[n]** 来检查每个元素的平方根，这将完成工作，但复杂度为 **O(n*n)** 。

下面是上述方法的实现:

## C++

```
// CPP program to find the sum of all the elements
// from the array whose square root is present
// in the same array

#include<bits/stdc++.h>
using namespace std;

    // Function to return the required sum
int getSum(int arr[], int n)
    {

        int sum = 0;

        for (int i = 0; i < n; i++) {
            double sqrtCurrent = sqrt(arr[i]);

            for (int j = 0; j < n; j++) {
                double x = arr[j];

                // If sqrtCurrent is present in array
                if (x == sqrtCurrent) {
                    sum += (sqrtCurrent * sqrtCurrent);
                    break;
                }
            }
        }

        return sum;
    }

    // Driver code
    int main()
    {
        int arr[] = { 2, 4, 5, 6, 7, 8, 9, 3 };
        int n = sizeof(arr)/sizeof(arr[0]);
        cout<<(getSum(arr, n));
    }
// This code is contributed by
// Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the sum of all the elements
// from the array whose square root is present
// in the same array
public class GFG {
    // Function to return the required sum
    public static int getSum(int arr[], int n)
    {

        int sum = 0;

        for (int i = 0; i < n; i++) {
            double sqrtCurrent = Math.sqrt(arr[i]);

            for (int j = 0; j < n; j++) {
                double x = arr[j];

                // If sqrtCurrent is present in array
                if (x == sqrtCurrent) {
                    sum += (sqrtCurrent * sqrtCurrent);
                    break;
                }
            }
        }

        return sum;
    }

    // Driver code
    public static void main(String args[])
    {
        int arr[] = { 2, 4, 5, 6, 7, 8, 9, 3 };
        int n = arr.length;
        System.out.println(getSum(arr, n));
    }
}
```

## 蟒蛇 3

```
# Python3 program to find the sum of
# all the elements from the array
# whose square root is present in
# the same array
import math

# Function to return the required sum
def getSum(arr, n):
    sum = 0
    for i in range(0, n):
        sqrtCurrent = math.sqrt(arr[i])
        for j in range(0, n):
            x = arr[j]

            # If sqrtCurrent is present in array
            if (x == sqrtCurrent):
                sum += (sqrtCurrent *
                        sqrtCurrent)
                break
    return int(sum)

# Driver code
if __name__ == '__main__':

    arr = [ 2, 4, 5, 6, 7, 8, 9, 3]
    n = len(arr)
    print(getSum(arr, n))

# This code is contributed
# by 29AjayKumar
```

## C#

```
// C# program to find the sum of all the elements
// from the array whose square root is present
// in the same array
using System ;

public class GFG {

    // Function to return the required sum
    public static float getSum(int []arr, int n)
    {

        float sum = 0;

        for (int i = 0; i < n; i++) {
            float sqrtCurrent = (float)Math.Sqrt(arr[i]);

            for (int j = 0; j < n; j++) {
                float x = (float)arr[j];

                // If sqrtCurrent is present in array
                if (x == sqrtCurrent) {
                    sum += (sqrtCurrent * sqrtCurrent);
                    break;
                }
            }
        }

        return sum;
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 2, 4, 5, 6, 7, 8, 9, 3 };
        int n = arr.Length;
        Console.WriteLine(getSum(arr, n));
    }
    // This code is contributed by Ryuga
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the sum of all
// the elements from the array whose
// square root is present in the same array

// Function to return the required sum
function getSum(&$arr, $n)
{
    $sum = 0;

    for ($i = 0; $i < $n; $i++)
    {
        $sqrtCurrent = sqrt($arr[$i]);

        for ($j = 0; $j < $n; $j++)
        {
            $x = $arr[$j];

            // If sqrtCurrent is present in array
            if ($x == $sqrtCurrent)
            {
                $sum += ($sqrtCurrent * $sqrtCurrent);
                break;
            }
        }
    }

    return $sum;
}

// Driver code
$arr = array(2, 4, 5, 6, 7, 8, 9, 3);
$n = sizeof($arr);
echo (getSum($arr, $n));

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>
    // Javascript program to find the sum of all the elements
    // from the array whose square root is present
    // in the same array

    // Function to return the required sum
    function getSum(arr, n)
    {

        let sum = 0;

        for (let i = 0; i < n; i++) {
            let sqrtCurrent = Math.sqrt(arr[i]);

            for (let j = 0; j < n; j++) {
                let x = arr[j];

                // If sqrtCurrent is present in array
                if (x == sqrtCurrent) {
                    sum += (sqrtCurrent * sqrtCurrent);
                    break;
                }
            }
        }

        return sum;
    }

    let arr = [ 2, 4, 5, 6, 7, 8, 9, 3 ];
    let n = arr.length;
    document.write(getSum(arr, n));

    // This code is contributed by suresh07.
</script>
```

**Output:** 

```
13
```

**有效方法:**我们可以创建一个包含数组中所有元素的[哈希集](https://www.geeksforgeeks.org/hashset-in-java/)，然后在 O(n)时间内检查数组中每个元素的平方根。

下面是上述方法的实现:

## C++

```
// C++ program to find the sum of all the elements
// from the array whose square root is present
// in the same array
#include<bits/stdc++.h>
using namespace std;

// Function to return the required sum
int getSum(int arr[], int n)
{

    int i, sum = 0;

    // Initialization of hash map
    set<int> hashSet;

    // Store each element in the hash map
    for (i = 0; i < n; i++)
        hashSet.insert(arr[i]);

    for (i = 0; i < n; i++)
    {
        double sqrtCurrent = sqrt(arr[i]);

        // If sqrtCurrent is a decimal number
        if (floor(sqrtCurrent) != ceil(sqrtCurrent))
            continue;

        // If hash set contains sqrtCurrent
        if (hashSet.find((int)sqrtCurrent) !=
            hashSet.end())
        {
            sum += (sqrtCurrent * sqrtCurrent);
        }
    }

    return sum;
}

// Driver code
int main()
{
    int arr[] = { 2, 4, 5, 6, 7, 8, 9, 3 };
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << (getSum(arr, n));
    return 0;
}

// This code is contributed by Rajput-Ji
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the sum of all the elements
// from the array whose square root is present
// in the same array

import java.util.*;
public class GFG {

    // Function to return the required sum
    public static int getSum(int arr[], int n)
    {

        int i, sum = 0;

        // Initialization of hash map
        Set<Integer> hashSet = new HashSet<>();

        // Store each element in the hash map
        for (i = 0; i < n; i++)
            hashSet.add(arr[i]);

        for (i = 0; i < n; i++) {
            double sqrtCurrent = Math.sqrt(arr[i]);

            // If sqrtCurrent is a decimal number
            if (Math.floor(sqrtCurrent) != Math.ceil(sqrtCurrent))
                continue;

            // If hash set contains sqrtCurrent
            if (hashSet.contains((int)sqrtCurrent)) {
                sum += (sqrtCurrent * sqrtCurrent);
            }
        }

        return sum;
    }

    // Driver code
    public static void main(String args[])
    {
        int arr[] = { 2, 4, 5, 6, 7, 8, 9, 3 };
        int n = arr.length;
        System.out.println(getSum(arr, n));
    }
}
```

## C#

```
// C# program to find the sum of all the elements
// from the array whose square root is present
// in the same array
using System;
using System.Collections.Generic;

class GFG
{

    // Function to return the required sum
    public static int getSum(int []arr, int n)
    {

        int i, sum = 0;

        // Initialization of hash map
        HashSet<int> hashSet = new HashSet<int>();

        // Store each element in the hash map
        for (i = 0; i < n; i++)
            hashSet.Add(arr[i]);

        for (i = 0; i < n; i++)
        {
            double sqrtCurrent = Math.Sqrt(arr[i]);

            // If sqrtCurrent is a decimal number
            if (Math.Floor(sqrtCurrent) !=
                Math.Ceiling(sqrtCurrent))
                continue;

            // If hash set contains sqrtCurrent
            if (hashSet.Contains((int)sqrtCurrent))
            {
                sum += (int)(sqrtCurrent * sqrtCurrent);
            }
        }

        return sum;
    }

    // Driver code
    public static void Main(String []args)
    {
        int []arr = { 2, 4, 5, 6, 7, 8, 9, 3 };
        int n = arr.Length;
        Console.WriteLine(getSum(arr, n));
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find the sum of all the
# elements from the array whose square
# root is present in the same array
import math

# Function to return the required sum
def getSum(arr, n):
    sum = 0;

    # Initialization of hash map
    hashSet = set();

    # Store each element in the hash map
    for i in range(n):
        hashSet.add(arr[i]);

    for i in range(n):

        sqrtCurrent = math.sqrt(arr[i]);

        # If sqrtCurrent is a decimal number
        if (math.floor(sqrtCurrent) != math.ceil(sqrtCurrent)):
            continue;

        # If hash set contains sqrtCurrent
        if (int(sqrtCurrent) in hashSet):
            sum += int(sqrtCurrent * sqrtCurrent);

    return sum;

# Driver code
arr = [ 2, 4, 5, 6, 7, 8, 9, 3 ];
n = len(arr);
print(getSum(arr, n));

# This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the sum of all the
// elements from the array whose square
// root is present in the same array

// Function to return the required sum
function getSum($arr, $n)
{
    $sum = 0;

    // Initialization of hash map
    $hashSet = array();

    // Store each element in the hash map
    for ($i = 0; $i < $n; $i++)
        array_push($hashSet, $arr[$i]);

    $hashSet = array_unique($hashSet);

    for ($i = 0; $i < $n; $i++)
    {
        $sqrtCurrent = sqrt($arr[$i]);

        // If sqrtCurrent is a decimal number
        if (floor($sqrtCurrent) != ceil($sqrtCurrent))
            continue;

        // If hash set contains sqrtCurrent
        if (in_array((int)$sqrtCurrent, $hashSet))
        {
            $sum += ($sqrtCurrent * $sqrtCurrent);
        }
    }

    return $sum;
}

// Driver code
$arr = array( 2, 4, 5, 6, 7, 8, 9, 3 );
$n = count($arr);
print(getSum($arr, $n));

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to find the sum of
// all the elements from the array whose
// square root is present in the same array

// Function to return the required sum
function getSum(arr, n)
{
    let i, sum = 0;

    // Initialization of hash map
    let hashSet = new Set();

    // Store each element in the hash map
    for(i = 0; i < n; i++)
        hashSet.add(arr[i]);

    for(i = 0; i < n; i++)
    {
        let sqrtCurrent = Math.sqrt(arr[i]);

        // If sqrtCurrent is a decimal number
        if (Math.floor(sqrtCurrent) !=
            Math.ceil(sqrtCurrent))
            continue;

        // If hash set contains sqrtCurrent
        if (hashSet.has(sqrtCurrent))
        {
            sum += (sqrtCurrent * sqrtCurrent);
        }
    }
    return sum;
}

// Driver code
let arr = [ 2, 4, 5, 6, 7, 8, 9, 3 ];
let n = arr.length;

document.write(getSum(arr, n));

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
13
```