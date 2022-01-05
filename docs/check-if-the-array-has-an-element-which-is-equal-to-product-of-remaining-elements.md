# 检查数组中是否有一个元素等于剩余元素的乘积

> 原文:[https://www . geesforgeks . org/check-如果数组有一个等于剩余元素乘积的元素/](https://www.geeksforgeeks.org/check-if-the-array-has-an-element-which-is-equal-to-product-of-remaining-elements/)

给定一个由 N 个元素组成的数组，任务是检查该数组中是否有一个元素等于所有剩余元素的乘积。

**示例:**

```
Input: arr[] = {1, 2, 12, 3, 2}
Output: YES
12 is the product of all the remaining elements 
i.e. 1 * 2 * 3 * 2 = 12

Input: arr[] = {1, 2, 3}
Output: NO
```

**方法-1:**

1.  首先，取数组中所有元素的乘积。
2.  现在再次遍历整个数组。
3.  对于任何元素 a[i]，检查它是否等于所有元素除以该元素的乘积。
4.  如果至少找到一个这样的元素，则打印“是”。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to Check if the array
// has an element which is equal to
// product of all the remaining elements
bool CheckArray(int arr[], int n)
{
    int prod = 1;

    // Calculate the product of all the elements
    for (int i = 0; i < n; ++i)
        prod *= arr[i];

    // Return true if any such element is found
    for (int i = 0; i < n; ++i)
        if (arr[i] == prod / arr[i])
            return true;

    // If no element is found
    return false;
}

int main()
{
    int arr[] = { 1, 2, 12, 3, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);

    if (CheckArray(arr, n))
        cout << "YES";

    else
        cout << "NO";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

import java.io.*;

class GFG {

// Function to Check if the array
// has an element which is equal to
// product of all the remaining elements
static boolean CheckArray(int arr[], int n)
{
    int prod = 1;

    // Calculate the product of all the elements
    for (int i = 0; i < n; ++i)
        prod *= arr[i];

    // Return true if any such element is found
    for (int i = 0; i < n; ++i)
        if (arr[i] == prod / arr[i])
            return true;

    // If no element is found
    return false;
}

    public static void main (String[] args) {
            int arr[] = { 1, 2, 12, 3, 2 };
    int n =arr.length;

    if (CheckArray(arr, n))
        System.out.println("YES");

    else
        System.out.println("NO");

    }
}
// This code is contributed by shs..
```

## 蟒蛇 3

```
# Python 3 implementation of the above approach

# Function to Check if the array
# has an element which is equal to
# product of all the remaining elements
def CheckArray(arr, n):
    prod = 1

    # Calculate the product of all
    # the elements
    for i in range(0, n, 1):
        prod *= arr[i]

    # Return true if any such element
    # is found
    for i in range(0, n, 1):
        if (arr[i] == prod / arr[i]):
            return True

    # If no element is found
    return False

# Driver code
if __name__ == '__main__':
    arr = [1, 2, 12, 3, 2]
    n = len(arr)

    if (CheckArray(arr, n)):
        print("YES")

    else:
        print("NO")

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the above approach
class GFG
{
// Function to Check if the array
// has an element which is equal to
// product of all the remaining elements
static bool CheckArray(int[] arr, int n)
{
    int prod = 1;

    // Calculate the product of
    // all the elements
    for (int i = 0; i < n; ++i)
        prod *= arr[i];

    // Return true if any such
    // element is found
    for (int i = 0; i < n; ++i)
        if (arr[i] == prod / arr[i])
            return true;

    // If no element is found
    return false;
}

// Driver Code
public static void Main ()
{
    int[] arr = new int[] { 1, 2, 12, 3, 2 };
    int n = arr.Length;

    if (CheckArray(arr, n))
        System.Console.WriteLine("YES");

    else
        System.Console.WriteLine("NO");
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to Check if the array
// has an element which is equal to
// product of all the remaining elements
function CheckArray($arr, $n)
{
    $prod = 1;

    // Calculate the product of
    // all the elements
    for ($i = 0; $i < $n; ++$i)
        $prod *= $arr[$i];

    // Return true if any such element
    // is found
    for ($i = 0; $i < $n; ++$i)
        if ($arr[$i] == $prod / $arr[$i])
            return true;

    // If no element is found
    return false;
}

// Driver Code
$arr = array(1, 2, 12, 3, 2);
$n = sizeof($arr);

if (CheckArray($arr, $n))
    echo "YES";
else
    echo "NO";

// This code is contributed
// by Akanksha Rai
```

## java 描述语言

```
<script>
// Java script implementation of the above approach

// Function to Check if the array
// has an element which is equal to
// product of all the remaining elements
function CheckArray(arr,n)
{
    let prod = 1;

    // Calculate the product of all the elements
    for (let i = 0; i < n; ++i)
        prod *= arr[i];

    // Return true if any such element is found
    for (let i = 0; i < n; ++i)
        if (arr[i] == prod / arr[i])
            return true;

    // If no element is found
    return false;
}

    let arr = [ 1, 2, 12, 3, 2 ];
    let n =arr.length;

    if (CheckArray(arr, n))
        document.write("YES");

    else
        document.write("NO");

// This code is contributed by sravan kumar Gottumukkala
</script>
```

**Output:** 

```
YES
```

**方法-2:** 方法是找到数组所有元素的乘积，检查它是否是一个完美的正方形。如果它是一个完美的正方形，那么检查这个乘积的平方根是否存在于数组中。如果存在，则打印是，否则打印否

> 根据问题陈述，a * b = N
> 其中 b 是除了 **a** 之外的数组所有剩余元素的乘积，即 arr【I】
> 并且还提到找到索引使得 **a = b** 。
> 所以，简单来说就是 **a*a = N 即 N** 是一个完美的正方形。而 **a** 就是它的平方根。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to Check if the array
// has an element which is equal to
// product of all the remaining elements
bool CheckArray(int arr[], int n)
{
    int prod = 1;

    // Storing frequency in map
    unordered_set<int> freq;

    // Calculate the product of all the elements
    for (int i = 0; i < n; ++i) {
        freq.insert(arr[i]);
        prod *= arr[i];
    }

    int root = sqrt(prod);

    // If the prod is a perfect square
    if (root * root == prod)

        // then check if its square root
        // exist in the array or not
        if (freq.find(root) != freq.end())
            return true;

    return false;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 12, 3, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);

    if (CheckArray(arr, n))
        cout << "YES";

    else
        cout << "NO";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.ArrayList;

// Java implementation of the above approach
class GFG {

// Function to Check if the array
// has an element which is equal to
// product of all the remaining elements
    static boolean CheckArray(int arr[], int n) {
        int prod = 1;

        // Storing frequency in map
        ArrayList<Integer> freq = new ArrayList<>();

        // Calculate the product of all the elements
        for (int i = 0; i < n; ++i) {
            freq.add(arr[i]);
            prod *= arr[i];
        }

        int root = (int) Math.sqrt(prod);

        // If the prod is a perfect square
        if (root * root == prod) // then check if its square root
        // exist in the array or not
        {
            if (freq.contains(root) & freq.lastIndexOf(root) != (freq.size())) {
                return true;
            }
        }

        return false;
    }
// Driver code

    public static void main(String[] args) {

        int arr[] = {1, 2, 12, 3, 2};
        int n = arr.length;

        if (CheckArray(arr, n)) {
            System.out.println("YES");
        } else {
            System.out.println("NO");
        }

    }
}
//This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

import math

# Function to Check if the array
# has an element which is equal to
# product of all the remaining elements
def CheckArray( arr, n):

    prod = 1

    # Storing frequency in map
    freq = []

    # Calculate the product of all the elements
    for i in range(n) :
        freq.append(arr[i])
        prod *= arr[i]

    root = math.sqrt(prod)

    # If the prod is a perfect square
    if (root * root == prod):

        # then check if its square root
        # exist in the array or not
        if root in freq:
            return True

    return False

# Driver code
if __name__ == "__main__":

    arr = [1, 2, 12, 3, 2 ]
    n = len(arr)

    if (CheckArray(arr, n)):
        print ("YES")

    else:
        print ("NO")
```

## C#

```
// C# implementation of above approach
using System;
using System.Collections;

class GFG
{

    // Function to Check if the array
    // has an element which is equal to
    // product of all the remaining elements
    static bool CheckArray(int []arr, int n)
    {
        int prod = 1;

        // Storing frequency in map
        ArrayList freq = new ArrayList();

        // Calculate the product of all the elements
        for (int i = 0; i < n; ++i)
        {
            freq.Add(arr[i]);
            prod *= arr[i];
        }

        int root = (int) Math.Sqrt(prod);

        // If the prod is a perfect square
        if (root * root == prod) // then check if its square root
        // exist in the array or not
        {
            if (freq.Contains(root) & freq.LastIndexOf(root) != (freq.Count))
            {
                return true;
            }
        }

        return false;
    }

    // Driver code
    public static void Main()
    {

        int []arr = {1, 2, 12, 3, 2};
        int n = arr.Length;

        if (CheckArray(arr, n))
        {
            Console.WriteLine("YES");
        }
        else
        {
            Console.WriteLine("NO");
        }
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to Check if the array
// has an element which is equal to
// product of all the remaining elements
function CheckArray($arr, $n)
{
    $prod = 1;

    // Storing frequency in map
    $freq = array();

    // Calculate the product of all the elements
    for ($i = 0; $i < $n; ++$i)
    {
        array_push($freq, $arr[$i]);
        $prod *= $arr[$i];
    }
    $freq = array_unique($freq);
    $root = (int)(sqrt($prod));

    // If the prod is a perfect square
    if ($root * $root == $prod)

        // then check if its square root
        // exist in the array or not
        if (in_array($root, $freq))
            return true;

    return false;
}

// Driver code
$arr = array( 1, 2, 12, 3, 2 );
$n = count($arr);

if (CheckArray($arr, $n))
    echo "YES";

else
    echo "NO";

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of
// the above approach

    // Function to Check if the array
// has an element which is equal to
// product of all the remaining elements
    function CheckArray(arr,n)
    {
        let prod = 1;

        // Storing frequency in map
        let freq = [];

        // Calculate the product of all the elements
        for (let i = 0; i < n; ++i) {
            freq.push(arr[i]);
            prod *= arr[i];
        }

        let root =  Math.floor(Math.sqrt(prod));

        // If the prod is a perfect square
        // then check if its square root
        if (root * root == prod)
        // exist in the array or not
        {
            if (freq.includes(root) &
            freq.lastIndexOf(root) != (freq.length))
            {
                return true;
            }
        }

        return false;
    }

    // Driver code
    let arr=[1, 2, 12, 3, 2];
    let n = arr.length;

    if (CheckArray(arr, n)) {
        document.write("YES");
    } else {
        document.write("NO");
    }

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
YES
```