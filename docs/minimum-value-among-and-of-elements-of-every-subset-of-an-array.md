# 数组的每个子集的元素的“与”之间的最小值

> 原文:[https://www . geeksforgeeks . org/数组每个子集的元素间最小值/](https://www.geeksforgeeks.org/minimum-value-among-and-of-elements-of-every-subset-of-an-array/)

给定一个整数数组，任务是找到数组每个子集的所有元素的“与”，并打印所有这些元素中的最小“与”值。
**例:**

```
Input: arr[] = {1, 2, 3}
Output: 0
AND of all possible subsets 
(1 & 2) = 0,
(1 & 3) = 1,
(2 & 3) = 2 and 
(1 & 2 & 3) = 0\. 
Minimum among these is 0\. 

Input: arr[] = {7, 2}
Output: 2    
```

**方法:**数组任何子集的最小 AND 值将是数组所有元素的 AND。所以，最简单的方法就是求子数组所有元素的“与”。
以下是上述办法的实施:
**实施:**

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

void minAND(int arr[], int n)
{

    int s = arr[0];

    // Find AND of whole array
    for (int i = 1; i < n; i++)
    {
        s = s & arr[i];
    }

    // Print the answer
    cout << (s) << endl;
}

// Driver code
int main()
{
    int arr[] = {1, 2, 3};
    int n = sizeof(arr)/sizeof(int);
    minAND(arr, n);
}

// This code has been contributed by Arnab Kundu
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG
{

    static void minAND(int[] arr, int n)
    {

        int s = arr[0];

        // Find AND of whole array
        for (int i = 1; i < n; i++)
        {
            s = s & arr[i];
        }

        // Print the answer
        System.out.println(s);
    }

    // Driver code
    public static void main(String[] args)
    {
        int[] arr = {1, 2, 3};
        int n = arr.length;
        minAND(arr, n);
    }
}

// This code has been contributed by 29AjayKumar
```

## 计算机编程语言

```
# Python program for the above approach
def minAND(arr, n):

    s = arr[0]

    # Find AND of whole array
    for i in range(1, n):
        s = s & arr[i]

    # Print the answer
    print(s)

# Driver code
arr = [1, 2, 3]
n = len(arr)
minAND(arr, n)
```

## C#

```
// C# program for the above approach
class GFG
{

    static void minAND(int[] arr, int n)
    {

        int s = arr[0];

        // Find AND of whole array
        for (int i = 1; i < n; i++)
        {
            s = s & arr[i];
        }

        // Print the answer
        System.Console.WriteLine(s);
    }

    // Driver code
    static void Main()
    {
        int[] arr = {1, 2, 3};
        int n = arr.Length;
        minAND(arr, n);
    }
}

// This code has been contributed by chandan_jnu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for the above approach

function minAND($arr, $n)
{

    $s = $arr[0];

    // Find AND of whole array
    for ($i = 1; $i < $n; $i++)
    {
        $s = $s & $arr[$i];
    }

    // Print the answer
    print($s . "\n");
}

// Driver code
$arr = array(1, 2, 3);
$n = count($arr);
minAND($arr, $n);

// This code is contributed
// by chandan_jnu
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the approach
function minAND(arr, n) {

    let s = arr[0];

    // Find AND of whole array
    for (let i = 1; i < n; i++) {
        s = s & arr[i];
    }

    // Prlet the answer
    document.write((s) + "<br>");
}

// Driver code

let arr = [1, 2, 3];
let n = arr.length;
minAND(arr, n);

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
0
```