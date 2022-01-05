# 生成偶数元素大于

的整数最小和序列

> 原文:[https://www . geeksforgeeks . org/generate-最小和-偶数元素整数序列-大于/](https://www.geeksforgeeks.org/generate-minimum-sum-sequence-of-integers-with-even-elements-greater/)

给定一个整数 **N** ，任务是生成一个正整数序列 **N** ，这样:

*   偶数位置的每个元素必须大于它后面的元素和它前面的元素，即**arr[I–1]<arr[I]>arr[I+1]**
*   元素的总和必须是偶数，并且是最小的可能值(在所有可能的序列中)。

**示例:**

> **输入:**N = 4
> T3】输出: 1 2 1 2
> 
> **输入:**N = 5
> T3】输出: 1 3 1 2 1

**方法:**为了得到可能具有最小和的序列，该序列必须是 **1，2，1，2，1，2，1 …** 的形式，并且对于序列的和不为偶数的情况，该序列中的任何 **2** 可以被改变为一个 **3** 以使该序列的和为偶数。

下面是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the required sequence
void make_sequence(int N)
{

    // arr[] will hold the sequence
    // sum variable will store the sum
    // of the sequence
    int arr[N + 1], sum = 0;

    for (int i = 1; i <= N; i++) {

        if (i % 2 == 1)
            arr[i] = 1;
        else
            arr[i] = 2;

        sum += arr[i];
    }

    // If sum of the sequence is odd
    if (sum % 2 == 1)
        arr[2] = 3;

    // Print the sequence
    for (int i = 1; i <= N; i++)
        cout << arr[i] << " ";
}

// Driver Code
int main()
{
    int N = 9;

    make_sequence(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach

class GFG
{

// Function to print the required sequence
static void make_sequence(int N)
{

    // arr[] will hold the sequence
    // sum variable will store the sum
    // of the sequence
    int[] arr = new int[N + 1];
    int sum = 0;

    for (int i = 1; i <= N; i++)
    {
        if (i % 2 == 1)
            arr[i] = 1;
        else
            arr[i] = 2;

        sum += arr[i];
    }

    // If sum of the sequence is odd
    if (sum % 2 == 1)
        arr[2] = 3;

    // Print the sequence
    for (int i = 1; i <= N; i++)
        System.out.print(arr[i] + " ");
}

// Driver Code
public static void main(String[] args)
{
    int N = 9;
    make_sequence(N);
}
}

// This code is contributed by iAyushRaj.
```

## 蟒蛇 3

```
# Python 3 implementation of above approach

# Function to print the required sequence
def make_sequence( N):

    # arr[] will hold the sequence
    # sum variable will store the sum
    # of the sequence
    arr = [0] * (N + 1)
    sum = 0

    for i in range(1, N + 1):

        if (i % 2 == 1):
            arr[i] = 1
        else:
            arr[i] = 2

        sum += arr[i]

    # If sum of the sequence is odd
    if (sum % 2 == 1):
        arr[2] = 3

    # Print the sequence
    for i in range(1, N + 1):
        print(arr[i], end = " ")

# Driver Code
if __name__ == "__main__":

    N = 9
    make_sequence(N)

# This code is contributed by ita_c
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

// Function to print the required sequence
public static void make_sequence(int N)
{

    // arr will hold the sequence
    // sum variable will store the sum
    // of the sequence
    int[] arr = new int[N + 1];
    int sum = 0;

    for (int i = 1; i <= N; i++)
    {
        if (i % 2 == 1)
            arr[i] = 1;
        else
            arr[i] = 2;

        sum += arr[i];
    }

    // If sum of the sequence is odd
    if (sum % 2 == 1)
        arr[2] = 3;

    // Print the sequence
    for (int i = 1; i <= N; i++)
        Console.Write(arr[i] + " ");
}

// Driver Code
public static void Main()
{
    int N = 9;

    make_sequence(N);
}
}

// This code is contributed by iAyushRaj.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function to print the required sequence
function make_sequence($N)
{

    // arr[] will hold the sequence
    // sum variable will store the sum
    // of the sequence
    $arr = array();
    $sum = 0;

    for ($i = 1; $i <= $N; $i++)
    {
        if ($i % 2 == 1)
            $arr[$i] = 1;
        else
            $arr[$i] = 2;

        $sum += $arr[$i];
    }

    // If sum of the sequence is odd
    if ($sum % 2 == 1)
        $arr[2] = 3;

    // Print the sequence
    for ($i = 1; $i <= $N; $i++)
        echo $arr[$i], " ";
}

// Driver Code
$N = 9;
make_sequence($N);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// Function to print the required sequence
function make_sequence(N)
{

    // arr[] will hold the sequence
    // sum variable will store the sum
    // of the sequence
    var arr = Array(N+1), sum = 0;

    for (var i = 1; i <= N; i++) {

        if (i % 2 == 1)
            arr[i] = 1;
        else
            arr[i] = 2;

        sum += arr[i];
    }

    // If sum of the sequence is odd
    if (sum % 2 == 1)
        arr[2] = 3;

    // Print the sequence
    for (var i = 1; i <= N; i++)
        document.write( arr[i] + " ");
}

// Driver Code
var N = 9;
make_sequence(N);

</script>
```

**Output:** 

```
1 3 1 2 1 2 1 2 1
```