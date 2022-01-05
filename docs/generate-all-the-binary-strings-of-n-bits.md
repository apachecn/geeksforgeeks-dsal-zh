# 生成 N 位的所有二进制字符串

> 原文:[https://www . geeksforgeeks . org/generate-all-the-the-the-binary-strings-of-n-bits/](https://www.geeksforgeeks.org/generate-all-the-binary-strings-of-n-bits/)

给定一个正整数 **N** 。任务是生成所有 N 位的二进制字符串。这些二进制字符串应该按升序排列。
**例:**

```
Input: 2
Output:
0 0
0 1
1 0
1 1

Input: 3
Output:
0 0 0
0 0 1
0 1 0
0 1 1
1 0 0
1 0 1
1 1 0
1 1 1
```

**方法:**想法是尝试每一个[排列](https://www.geeksforgeeks.org/permutations-of-a-given-string-using-stl/)。每个位置都有 2 个选项，要么是“0”，要么是“1”。[回溯](https://www.geeksforgeeks.org/backtracking-algorithms/)在这种方法中用于尝试每一种可能性/排列。
以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach:

#include <bits/stdc++.h>
using namespace std;

// Function to print the output
void printTheArray(int arr[], int n)
{
    for (int i = 0; i < n; i++) {
        cout << arr[i] << " ";
    }
    cout << endl;
}

// Function to generate all binary strings
void generateAllBinaryStrings(int n, int arr[], int i)
{
    if (i == n) {
        printTheArray(arr, n);
        return;
    }

    // First assign "0" at ith position
    // and try for all other permutations
    // for remaining positions
    arr[i] = 0;
    generateAllBinaryStrings(n, arr, i + 1);

    // And then assign "1" at ith position
    // and try for all other permutations
    // for remaining positions
    arr[i] = 1;
    generateAllBinaryStrings(n, arr, i + 1);
}

// Driver Code
int main()
{
    int n = 4;

    int arr[n];

    // Print all binary strings
    generateAllBinaryStrings(n, arr, 0);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach:
import java.util.*;

class GFG
{

// Function to print the output
static void printTheArray(int arr[], int n)
{
    for (int i = 0; i < n; i++)
    {
        System.out.print(arr[i]+" ");
    }
    System.out.println();
}

// Function to generate all binary strings
static void generateAllBinaryStrings(int n,
                            int arr[], int i)
{
    if (i == n)
    {
        printTheArray(arr, n);
        return;
    }

    // First assign "0" at ith position
    // and try for all other permutations
    // for remaining positions
    arr[i] = 0;
    generateAllBinaryStrings(n, arr, i + 1);

    // And then assign "1" at ith position
    // and try for all other permutations
    // for remaining positions
    arr[i] = 1;
    generateAllBinaryStrings(n, arr, i + 1);
}

// Driver Code
public static void main(String args[])
{
    int n = 4;

    int[] arr = new int[n];

    // Print all binary strings
    generateAllBinaryStrings(n, arr, 0);
}
}

// This code is contributed by
// Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

# Function to print the output
def printTheArray(arr, n):

    for i in range(0, n):
        print(arr[i], end = " ")

    print()

# Function to generate all binary strings
def generateAllBinaryStrings(n, arr, i):

    if i == n:
        printTheArray(arr, n)
        return

    # First assign "0" at ith position
    # and try for all other permutations
    # for remaining positions
    arr[i] = 0
    generateAllBinaryStrings(n, arr, i + 1)

    # And then assign "1" at ith position
    # and try for all other permutations
    # for remaining positions
    arr[i] = 1
    generateAllBinaryStrings(n, arr, i + 1)

# Driver Code
if __name__ == "__main__":

    n = 4
    arr = [None] * n

    # Print all binary strings
    generateAllBinaryStrings(n, arr, 0)

# This code is contributed
# by Rituraj Jain
```

## C#

```
// C# implementation of the above approach:
using System;

class GFG
{

// Function to print the output
static void printTheArray(int []arr, int n)
{
    for (int i = 0; i < n; i++)
    {
        Console.Write(arr[i]+" ");
    }
    Console.WriteLine();
}

// Function to generate all binary strings
static void generateAllBinaryStrings(int n,
                            int []arr, int i)
{
    if (i == n)
    {
        printTheArray(arr, n);
        return;
    }

    // First assign "0" at ith position
    // and try for all other permutations
    // for remaining positions
    arr[i] = 0;
    generateAllBinaryStrings(n, arr, i + 1);

    // And then assign "1" at ith position
    // and try for all other permutations
    // for remaining positions
    arr[i] = 1;
    generateAllBinaryStrings(n, arr, i + 1);
}

// Driver Code
public static void Main(String []args)
{
    int n = 4;

    int[] arr = new int[n];

    // Print all binary strings
    generateAllBinaryStrings(n, arr, 0);
}
}

// This code has been contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to print the output
function printTheArray($arr, $n)
{
    for ($i = 0; $i < $n; $i++)
    {
        echo $arr[$i], " ";
    }
    echo "\n";
}

// Function to generate all binary strings
function generateAllBinaryStrings($n, $arr, $i)
{
    if ($i == $n)
    {
        printTheArray($arr, $n);
        return;
    }

    // First assign "0" at ith position
    // and try for all other permutations
    // for remaining positions
    $arr[$i] = 0;
    generateAllBinaryStrings($n, $arr, $i + 1);

    // And then assign "1" at ith position
    // and try for all other permutations
    // for remaining positions
    $arr[$i] = 1;
    generateAllBinaryStrings($n, $arr, $i + 1);
}

// Driver Code
$n = 4;

$arr = array_fill(0, $n, 0);

// Print all binary strings
generateAllBinaryStrings($n, $arr, 0);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of the above approach:

    // Function to print the output
    function printTheArray(arr, n)
    {
        for (let i = 0; i < n; i++)
        {
            document.write(arr[i]+" ");
        }
        document.write("</br>");
    }

    // Function to generate all binary strings
    function generateAllBinaryStrings(n, arr, i)
    {
        if (i == n)
        {
            printTheArray(arr, n);
            return;
        }

        // First assign "0" at ith position
        // and try for all other permutations
        // for remaining positions
        arr[i] = 0;
        generateAllBinaryStrings(n, arr, i + 1);

        // And then assign "1" at ith position
        // and try for all other permutations
        // for remaining positions
        arr[i] = 1;
        generateAllBinaryStrings(n, arr, i + 1);
    }

    let n = 4;

    let arr = new Array(n);
    arr.fill(0);

    // Print all binary strings
    generateAllBinaryStrings(n, arr, 0);

// This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
0 0 0 0 
0 0 0 1 
0 0 1 0 
0 0 1 1 
0 1 0 0 
0 1 0 1 
0 1 1 0 
0 1 1 1 
1 0 0 0 
1 0 0 1 
1 0 1 0 
1 0 1 1 
1 1 0 0 
1 1 0 1 
1 1 1 0 
1 1 1 1
```