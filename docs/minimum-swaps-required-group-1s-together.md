# 将所有 1 组合在一起所需的最小互换量

> 原文:[https://www . geesforgeks . org/minimum-swaps-required-group-1s-together/](https://www.geeksforgeeks.org/minimum-swaps-required-group-1s-together/)

给定一个 0 和 1 的数组，我们需要编写一个程序来找到将数组中的所有 1 组合在一起所需的最小交换次数。

**示例:**

```
Input : arr[] = {1, 0, 1, 0, 1}
Output : 1
Explanation: Only 1 swap is required to 
group all 1's together. Swapping index 1
and 4 will give arr[] = {1, 1, 1, 0, 0}

Input : arr[] = {1, 0, 1, 0, 1, 1}
Output : 1
```

一个**简单的解决方法**是首先计算数组中 1 的总数。假设这个计数是 x，现在我们需要找到这个数组的长度为 x 的子数组，最大数量为 1。所需的最小交换将是长度为 x 的子数组中 0 的数量，最大数量为 1。
时间复杂度:O(n <sup>2</sup>

一个**有效的解决方案**是使用[滑动窗口](https://www.geeksforgeeks.org/window-sliding-technique/)技术的概念优化上述方法中寻找子阵列的蛮力技术。我们可以维持一个*预计数*阵列，以寻找在 0(1)时间复杂度的子阵列中存在的 1 的数量。

以下是上述想法的实现:

## C++

```
// C++ program to find minimum swaps
// required to group all 1's together
#include <iostream>
#include <limits.h>

using namespace std;

// Function to find minimum swaps
// to group all 1's together
int minSwaps(int arr[], int n) {

  int noOfOnes = 0;

  // find total number of all in the array
  for (int i = 0; i < n; i++) {
    if (arr[i] == 1)
      noOfOnes++;
  }

  // length of subarray to check for
  int x = noOfOnes;

  int maxOnes = INT_MIN;

  // array to store number of 1's upto
  // ith index
  int preCompute[n] = {0};

  // calculate number of 1's upto ith
  // index and store in the array preCompute[]
  if (arr[0] == 1)
    preCompute[0] = 1;
  for (int i = 1; i < n; i++) {
    if (arr[i] == 1) {
      preCompute[i] = preCompute[i - 1] + 1;
    } else
      preCompute[i] = preCompute[i - 1];
  }

  // using sliding window technique to find
  // max number of ones in subarray of length x
  for (int i = x - 1; i < n; i++) {
    if (i == (x - 1))
      noOfOnes = preCompute[i];
    else
      noOfOnes = preCompute[i] - preCompute[i - x];

    if (maxOnes < noOfOnes)
      maxOnes = noOfOnes;
  }

  // calculate number of zeros in subarray
  // of length x with maximum number of 1's
  int noOfZeroes = x - maxOnes;

  return noOfZeroes;
}

// Driver Code
int main() {
  int a[] = {1, 0, 1, 0, 1};
  int n = sizeof(a) / sizeof(a[0]);
  cout << minSwaps(a, n);
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java  program to find minimum swaps
// required to group all 1's together

import java.io.*;

class GFG {

// Function to find minimum swaps
// to group all 1's together
 static int minSwaps(int arr[], int n) {

int noOfOnes = 0;

// find total number of all in the array
for (int i = 0; i < n; i++) {
    if (arr[i] == 1)
    noOfOnes++;
}

// length of subarray to check for
int x = noOfOnes;

int maxOnes = Integer.MIN_VALUE;

// array to store number of 1's upto
// ith index
int preCompute[] = new int[n];

// calculate number of 1's upto ith
// index and store in the array preCompute[]
if (arr[0] == 1)
    preCompute[0] = 1;
for (int i = 1; i < n; i++) {
    if (arr[i] == 1) {
    preCompute[i] = preCompute[i - 1] + 1;
    } else
    preCompute[i] = preCompute[i - 1];
}

// using sliding window technique to find
// max number of ones in subarray of length x
for (int i = x - 1; i < n; i++) {
    if (i == (x - 1))
    noOfOnes = preCompute[i];
    else
    noOfOnes = preCompute[i] - preCompute[i - x];

    if (maxOnes < noOfOnes)
    maxOnes = noOfOnes;
}

// calculate number of zeros in subarray
// of length x with maximum number of 1's
int noOfZeroes = x - maxOnes;

return noOfZeroes;
}

// Driver Code
public static void main (String[] args) {
int a[] = {1, 0, 1, 0, 1};
int n = a.length;
System.out.println( minSwaps(a, n));

    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python program to
# find minimum swaps
# required to group
# all 1's together

# Function to find minimum swaps
# to group all 1's together
def minSwaps(arr,n):

    noOfOnes = 0

    # find total number of
    # all in the array
    for i in range(n):
        if (arr[i] == 1):
            noOfOnes=noOfOnes+1

    # length of subarray to check for
    x = noOfOnes

    maxOnes = -2147483648

    # array to store number of 1's upto
    # ith index
    preCompute={}

    # calculate number of 1's upto ith
    # index and store in the
    # array preCompute[]
    if (arr[0] == 1):
        preCompute[0] = 1
    for i in range(1,n):
        if (arr[i] == 1):
            preCompute[i] = preCompute[i - 1] + 1
        else:
            preCompute[i] = preCompute[i - 1]

    # using sliding window
    # technique to find
    # max number of ones in
    # subarray of length x
    for i in range(x-1,n):
        if (i == (x - 1)):
            noOfOnes = preCompute[i]
        else:
            noOfOnes = preCompute[i] - preCompute[i - x]

        if (maxOnes < noOfOnes):
            maxOnes = noOfOnes

    # calculate number of zeros in subarray
    # of length x with maximum number of 1's
    noOfZeroes = x - maxOnes

    return noOfZeroes

# Driver code

a = [1, 0, 1, 0, 1]
n = len(a)

print(minSwaps(a, n))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to find minimum swaps
// required to group all 1's together

using System;

class GFG {

    // Function to find minimum swaps
    // to group all 1's together
    static int minSwaps(int []arr, int n) {

        int noOfOnes = 0;

        // find total number of all in the array
        for (int i = 0; i < n; i++) {
            if (arr[i] == 1)
            noOfOnes++;
        }

        // length of subarray to check for
        int x = noOfOnes;

        int maxOnes = int.MinValue;

        // array to store number of 1's upto
        // ith index
        int []preCompute = new int[n];

        // calculate number of 1's upto ith
        // index and store in the array preCompute[]
        if (arr[0] == 1)
            preCompute[0] = 1;
        for (int i = 1; i < n; i++) {
            if (arr[i] == 1) {
            preCompute[i] = preCompute[i - 1] + 1;
            } else
            preCompute[i] = preCompute[i - 1];
        }

        // using sliding window technique to find
        // max number of ones in subarray of length x
        for (int i = x - 1; i < n; i++) {
            if (i == (x - 1))
            noOfOnes = preCompute[i];
            else
            noOfOnes = preCompute[i] - preCompute[i - x];

            if (maxOnes < noOfOnes)
            maxOnes = noOfOnes;
        }

        // calculate number of zeros in subarray
        // of length x with maximum number of 1's
        int noOfZeroes = x - maxOnes;

        return noOfZeroes;
    }

    // Driver Code
    public static void Main ()
    {
        int []a = {1, 0, 1, 0, 1};
        int n = a.Length;
        Console.WriteLine( minSwaps(a, n));

    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum swaps
// required to group all 1's together

// Function to find minimum swaps
// to group all 1's together
function minSwaps($arr, $n)
{

        $noOfOnes = 0;

        // find total number of
        // all in the array
        for($i = 0; $i < $n; $i++)
        {
            if ($arr[$i] == 1)
            $noOfOnes++;
        }

        // length of subarray
        // to check for
        $x = $noOfOnes;

        $maxOnes = PHP_INT_MIN;

        // array to store number of
        // 1's upto ith index
        $preCompute = array();

        // calculate number of 1's
        // upto ith index and store
        // in the array preCompute[]
        if ($arr[0] == 1)
            $preCompute[0] = 1;
        for($i = 1; $i < $n; $i++)
        {
            if ($arr[$i] == 1)
            {
                $preCompute[$i] = $preCompute[$i - 1] + 1;
            }
            else
                $preCompute[$i] = $preCompute[$i - 1];
        }

        // using sliding window
        // technique to find
        // max number of ones in
        // subarray of length x
        for ( $i = $x - 1; $i < $n; $i++)
        {
            if ($i == ($x - 1))
                $noOfOnes = $preCompute[$i];
            else
                $noOfOnes = $preCompute[$i] -
                            $preCompute[$i - $x];

            if ($maxOnes < $noOfOnes)
                $maxOnes = $noOfOnes;
        }

        // calculate number of zeros in subarray
        // of length x with maximum number of 1's
        $noOfZeroes = $x - $maxOnes;

        return $noOfZeroes;
}

// Driver Code
$a = array(1, 0, 1, 0, 10);
$n = count($a);
echo minSwaps($a, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
    // Javascript program to find minimum swaps
    // required to group all 1's together

    // Function to find minimum swaps
    // to group all 1's together
    function minSwaps(arr, n) {

        let noOfOnes = 0;

        // find total number of all in the array
        for (let i = 0; i < n; i++) {
            if (arr[i] == 1)
                noOfOnes++;
        }

        // length of subarray to check for
        let x = noOfOnes;

        let maxOnes = Number.MIN_VALUE;

        // array to store number of 1's upto
        // ith index
        let preCompute = new Array(n);
        preCompute.fill(0);

        // calculate number of 1's upto ith
        // index and store in the array preCompute[]
        if (arr[0] == 1)
            preCompute[0] = 1;
        for (let i = 1; i < n; i++) {
            if (arr[i] == 1) {
                preCompute[i] = preCompute[i - 1] + 1;
            } else
                preCompute[i] = preCompute[i - 1];
        }

        // using sliding window technique to find
        // max number of ones in subarray of length x
        for (let i = x - 1; i < n; i++) {
            if (i == (x - 1))
                noOfOnes = preCompute[i];
            else
                noOfOnes = preCompute[i] - preCompute[i - x];

            if (maxOnes < noOfOnes)
                maxOnes = noOfOnes;
        }

        // calculate number of zeros in subarray
        // of length x with maximum number of 1's
        let noOfZeroes = x - maxOnes;

        return noOfZeroes;
    }

    let a = [1, 0, 1, 0, 1];
    let n = a.length;
    document.write( minSwaps(a, n));

</script>
```

**Output**

```
1
```

**时间复杂度**:O(n)
T3】辅助空间 : O(n)

**另一种有效的方法:**
首先统计数组中 1 的总数。假设这个计数是 x，现在使用[窗口滑动](https://www.geeksforgeeks.org/window-sliding-technique/)技术的概念找到这个最大数量为 1 的数组的长度为 x 的子数组。维护一个变量，以便在 0(1)个额外空间中找到子数组中存在的 1 的数量，并且为每个子数组维护最大 1 变量，最后返回 0 的数量(0 的数量= x–最大 1)。

## C++

```
// C++ code for minimum swaps
// required to group all 1's together
#include <iostream>
#include <limits.h>

using namespace std;

// Function to find minimum swaps
// to group all 1's together
int minSwaps(int arr[], int n)
{

int numberOfOnes = 0;

// find total number of all 1's in the array
for (int i = 0; i < n; i++) {
    if (arr[i] == 1)
    numberOfOnes++;
}

// length of subarray to check for
int x = numberOfOnes;

int count_ones = 0, maxOnes;

// Find 1's for first subarray of length x
for(int i = 0; i < x; i++){
    if(arr[i] == 1)
    count_ones++;
}

maxOnes = count_ones;

// using sliding window technique to find
// max number of ones in subarray of length x
for (int i = 1; i <= n-x; i++) {

    // first remove leading element and check
    // if it is equal to 1 then decrement the
    // value of count_ones by 1
    if (arr[i-1] == 1)
    count_ones--;

    // Now add trailing element and check
    // if it is equal to 1 Then increment
    // the value of count_ones by 1
    if(arr[i+x-1] == 1)
    count_ones++;

    if (maxOnes < count_ones)
    maxOnes = count_ones;
}

// calculate number of zeros in subarray
// of length x with maximum number of 1's
int numberOfZeroes = x - maxOnes;

return numberOfZeroes;
}

// Driver Code
int main() {

int a[] = {0, 0, 1, 0, 1, 1, 0, 0, 1};
int n = sizeof(a) / sizeof(a[0]);

cout << minSwaps(a, n);

return 0;

}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program to find largest number
// smaller than equal to n with m set
// bits then m-1 0 bits.
public class GFG {

    // Function to find minimum swaps
    // to group all 1's together
    static int minSwaps(int arr[], int n)
    {

        int numberOfOnes = 0;

        // find total number of all 1's
        // in the array
        for (int i = 0; i < n; i++) {
            if (arr[i] == 1)
                numberOfOnes++;
        }

        // length of subarray to check for
        int x = numberOfOnes;

        int count_ones = 0, maxOnes;

        // Find 1's for first subarray
        // of length x
        for(int i = 0; i < x; i++){
            if(arr[i] == 1)
                count_ones++;
        }

        maxOnes = count_ones;

        // using sliding window technique
        // to find max number of ones in
        // subarray of length x
        for (int i = 1; i <= n-x; i++) {

            // first remove leading element
            // and check if it is equal to
            // 1 then decrement the
            // value of count_ones by 1
            if (arr[i - 1] == 1)
                count_ones--;

            // Now add trailing element
            // and check if it is equal
            // to 1 Then increment the
            // value of count_ones by 1
            if(arr[i + x - 1] == 1)
                count_ones++;

            if (maxOnes < count_ones)
            maxOnes = count_ones;
        }

        // calculate number of zeros in
        // subarray of length x with
        // maximum number of 1's
        int numberOfZeroes = x - maxOnes;

        return numberOfZeroes;
    }

    // Driver code
    public static void main(String args[])
    {
        int a[] = new int[]{0, 0, 1, 0,
                            1, 1, 0, 0, 1};
        int n = a.length;

        System.out.println(minSwaps(a, n));
    }
}

// This code is contributed by Sam007
```

## 蟒蛇 3

```
# Python code for minimum
# swaps required to group
# all 1's together

# Function to find minimum
# swaps to group all 1's
# together
def minSwaps(arr, n) :

    numberOfOnes = 0

    # find total number of
    # all 1's in the array
    for i in range(0, n) :

        if (arr[i] == 1) :
            numberOfOnes = numberOfOnes + 1

    # length of subarray
    # to check for
    x = numberOfOnes

    count_ones = 0
    maxOnes = 0

    # Find 1's for first
    # subarray of length x
    for i in range(0, x) :

        if(arr[i] == 1) :
            count_ones = count_ones + 1

    maxOnes = count_ones

    # using sliding window
    # technique to find
    # max number of ones in
    # subarray of length x
    for i in range(1, (n - x + 1)) :

        # first remove leading
        # element and check
        # if it is equal to 1
        # then decrement the
        # value of count_ones by 1
        if (arr[i - 1] == 1) :
            count_ones = count_ones - 1

        # Now add trailing
        # element and check
        # if it is equal to 1
        # Then increment
        # the value of count_ones by 1
        if(arr[i + x - 1] == 1) :
            count_ones = count_ones + 1

        if (maxOnes < count_ones) :
                maxOnes = count_ones

    # calculate number of
    # zeros in subarray
    # of length x with
    # maximum number of 1's
    numberOfZeroes = x - maxOnes

    return numberOfZeroes

# Driver Code
a = [0, 0, 1, 0, 1, 1, 0, 0, 1]
n = 9
print (minSwaps(a, n))

# This code is contributed
# by Manish Shaw(manishshaw1)
```

## C#

```
// C# code for minimum swaps
// required to group all 1's together
using System;

class GFG{

    // Function to find minimum swaps
    // to group all 1's together
    static int minSwaps(int []arr, int n)
    {

        int numberOfOnes = 0;

        // find total number of all 1's in the array
        for (int i = 0; i < n; i++) {
            if (arr[i] == 1)
            numberOfOnes++;
        }

        // length of subarray to check for
        int x = numberOfOnes;

        int count_ones = 0, maxOnes;

        // Find 1's for first subarray of length x
        for(int i = 0; i < x; i++){
            if(arr[i] == 1)
            count_ones++;
        }

        maxOnes = count_ones;

        // using sliding window technique to find
        // max number of ones in subarray of length x
        for (int i = 1; i <= n-x; i++) {

            // first remove leading element and check
            // if it is equal to 1 then decrement the
            // value of count_ones by 1
            if (arr[i - 1] == 1)
            count_ones--;

            // Now add trailing element and check
            // if it is equal to 1 Then increment
            // the value of count_ones by 1
            if(arr[i + x - 1] == 1)
            count_ones++;

            if (maxOnes < count_ones)
            maxOnes = count_ones;
        }

        // calculate number of zeros in subarray
        // of length x with maximum number of 1's
        int numberOfZeroes = x - maxOnes;

        return numberOfZeroes;
    }

    // Driver Code
    static public void Main ()
    {
        int []a = {0, 0, 1, 0, 1, 1, 0, 0, 1};
        int n = a.Length;

        Console.WriteLine(minSwaps(a, n));

    }
}
// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code for minimum swaps
// required to group all 1's together

// Function to find minimum swaps
// to group all 1's together
function minSwaps($arr, $n)
{

    $numberOfOnes = 0;

    // find total number of
    // all 1's in the array
    for ($i = 0; $i < $n; $i++)
    {
        if ($arr[$i] == 1)
            $numberOfOnes++;
    }

    // length of subarray to check for
    $x = $numberOfOnes;

    $count_ones = 0;
    $maxOnes;

    // Find 1's for first
    // subarray of length x
    for($i = 0; $i < $x; $i++)
    {
        if($arr[$i] == 1)
            $count_ones++;
    }

    $maxOnes = $count_ones;

    // using sliding window
    // technique to find
    // max number of ones in
    // subarray of length x
    for ($i = 1; $i <= $n - $x; $i++)
    {

        // first remove leading
        // element and check
        // if it is equal to 1
        // then decrement the
        // value of count_ones by 1
        if ($arr[$i - 1] === 1)
            $count_ones--;

        // Now add trailing
        // element and check
        // if it is equal to 1
        // Then increment
        // the value of count_ones by 1
        if($arr[$i + $x - 1] === 1)
                $count_ones++;

        if ($maxOnes < $count_ones)
                $maxOnes = $count_ones;
    }

    // calculate number of zeros in subarray
    // of length x with maximum number of 1's
    $numberOfZeroes = $x - $maxOnes;

    return $numberOfZeroes;
}

// Driver Code
$a = array(0, 0, 1, 0, 1, 1, 0, 0, 1);
$n = 9;
echo minSwaps($a, $n);

// This code is contributed by Anuj_67
?>
```

## java 描述语言

```
<script>   
    // Javascript code for minimum swaps
    // required to group all 1's together

    // Function to find minimum swaps
    // to group all 1's together
    function minSwaps(arr, n)
    {

        let numberOfOnes = 0;

        // find total number of all 1's in the array
        for (let i = 0; i < n; i++) {
            if (arr[i] == 1)
            numberOfOnes++;
        }

        // length of subarray to check for
        let x = numberOfOnes;

        let count_ones = 0, maxOnes;

        // Find 1's for first subarray of length x
        for(let i = 0; i < x; i++){
            if(arr[i] == 1)
            count_ones++;
        }

        maxOnes = count_ones;

        // using sliding window technique to find
        // max number of ones in subarray of length x
        for (let i = 1; i <= n-x; i++) {

            // first remove leading element and check
            // if it is equal to 1 then decrement the
            // value of count_ones by 1
            if (arr[i - 1] == 1)
                count_ones--;

            // Now add trailing element and check
            // if it is equal to 1 Then increment
            // the value of count_ones by 1
            if(arr[i + x - 1] == 1)
                count_ones++;

            if (maxOnes < count_ones)
                maxOnes = count_ones;
        }

        // calculate number of zeros in subarray
        // of length x with maximum number of 1's
        let numberOfZeroes = x - maxOnes;

        return numberOfZeroes;
    }

    let a = [0, 0, 1, 0, 1, 1, 0, 0, 1];
    let n = a.length;

    document.write(minSwaps(a, n));

</script>
```

**Output**

```
1
```

**时间复杂度:** O(n)
**辅助空间:** O(1)
感谢 [**杰拉先生**](https://auth.geeksforgeeks.org/user/Mr.Gera/practice/) 提出这个方法。

**滑动窗口易懂版**

**算法:**

1.将总数存储在一个变量中，比如计数。这将是窗口大小。

2.初始化一个变量来存储大小计数的所有子数组中的最大数量的 1，并初始化一个变量来存储当前窗口中的 1 计数。

3.现在迭代数组，一旦你达到窗口大小，将该窗口中的“1”的数量与目前所有窗口中的“1”的最大数量进行比较，如果当前窗口中的“1”数量更多，则更新“1”的最大数量。如果窗口的第一个元素是 1，则减少当前计数。

4.答案将是 1 的总数–所有窗口中 1 的最大数量。

## C++

```
#include <bits/stdc++.h>

using namespace std;

int minSwaps(int arr[], int n)
{
  int totalCount = 0; // To store total number of ones
  // count total no of ones
  for (int i = 0; i < n; i++)
    totalCount += arr[i];

  int currCount = 0; // To store count of ones in current window
  int maxCount = 0;  // To store maximum count ones out of all windows
  int i = 0;         // start of window
  int j = 0;         // end of window

  while (j < n)
  {
    currCount += arr[j];

    // update maxCount when reach window size i.e. total count of ones in array
    if ((j - i + 1) == totalCount)
    {
      maxCount = max(maxCount, currCount);
      if (arr[i] == 1)
        currCount--; // decrease current count if first element of window is 1
      i++;           // slide window
    }
    j++;
  }

  return totalCount - maxCount; // return total no of ones in array - maximum count of ones out of all windows
}

// Driver Code
int main()
{

  int a[] = {1, 0, 1, 0, 1, 1};
  int n = sizeof(a) / sizeof(a[0]);

  cout << minSwaps(a, n);

  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.io.*;
import java.util.*;

class GFG{

static int minSwaps(int[] arr, int n)
{

    // To store total number of ones
    int totalCount = 0;

    // Count total no of ones
    int i;
    for(i = 0; i < n; i++)
        totalCount += arr[i];

    int currCount = 0; // To store count of ones in current window
    int maxCount = 0;  // To store maximum count ones out
                       // of all windows

    // start of window
    i = 0;

    // end of window
    int j = 0;

    while (j < n)
    {
        currCount += arr[j];

        // update maxCount when reach window size i.e.
        // total count of ones in array
        if ((j - i + 1) == totalCount)
        {
            maxCount = Math.max(maxCount, currCount);
            if (arr[i] == 1)
                currCount--; // decrease current count
                             // if first element of
                             // window is 1

            // slide window
            i++;
        }
        j++;
    }

    return totalCount - maxCount; // return total no of ones in array
                                  // - maximum count of ones out of
                                  // all windows
}

// Driver Code
public static void main(String args[])
    {
    int[] a = { 1, 0, 1, 0, 1, 1 };
    int n = a.length;

    System.out.println(minSwaps(a, n));
}
}

// This code is contributed by shivanisinghss2110
```

## 计算机编程语言

```
def minSwaps(arr, n):

    # To store total number of ones
    totalCount = 0

    # count total no of ones
    for i in range(0,n):
        totalCount += arr[i]

    currCount = 0 # To store count of ones in current window
    maxCount = 0  # To store maximum count ones out of all windows
    i = 0         # start of window
    j = 0         # end of window

    while (j < n):
        currCount += arr[j]

        # update maxCount when reach window size i.e. total count of ones in array
        if ((j - i + 1) == totalCount):
            maxCount = max(maxCount, currCount)
            if (arr[i] == 1):
                currCount -= 1

                # decrease current count if first element of window is 1
            i += 1           # slide window
        j += 1

    return totalCount - maxCount # return total no of ones in array - maximum count of ones out of all windows

# Driver Code
a = [1, 0, 1, 0, 1, 1]
n = len(a)
print(minSwaps(a, n))

# this code is contributed by shivanisighss2110
```

## C#

```
using System;

class GFG{

static int minSwaps(int[] arr, int n)
{

    // To store total number of ones
    int totalCount = 0;

    // Count total no of ones
    int i;
    for(i = 0; i < n; i++)
        totalCount += arr[i];

    int currCount = 0; // To store count of ones in current window
    int maxCount = 0;  // To store maximum count ones out
                       // of all windows

    // start of window
    i = 0;

    // end of window
    int j = 0;

    while (j < n)
    {
        currCount += arr[j];

        // update maxCount when reach window size i.e.
        // total count of ones in array
        if ((j - i + 1) == totalCount)
        {
            maxCount = Math.Max(maxCount, currCount);
            if (arr[i] == 1)
                currCount--; // decrease current count
                             // if first element of
                             // window is 1

            // slide window
            i++;
        }
        j++;
    }

    return totalCount - maxCount; // return total no of ones in array
                                  // - maximum count of ones out of
                                  // all windows
}

// Driver Code
public static void Main()
{
    int[] a = { 1, 0, 1, 0, 1, 1 };
    int n = a.Length;

    Console.WriteLine(minSwaps(a, n));
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>

function minSwaps(arr, n)
{

    // To store total number of ones
    let totalCount = 0;

    // Count total no of ones
    let i;
    for(i = 0; i < n; i++)
        totalCount += arr[i];

    let currCount = 0; // To store count of ones in current window
    let maxCount = 0;  // To store maximum count ones out
                       // of all windows

    // start of window
    i = 0;

    // end of window
    let j = 0;

    while (j < n)
    {
        currCount += arr[j];

        // update maxCount when reach window size i.e.
        // total count of ones in array
        if ((j - i + 1) == totalCount)
        {
            maxCount = Math.max(maxCount, currCount);
            if (arr[i] == 1)
                currCount--; // decrease current count
                             // if first element of
                             // window is 1

            // slide window
            i++;
        }
        j++;
    }

    return totalCount - maxCount; // return total no of ones in array
                                  // - maximum count of ones out of
                                  // all windows
}

// Driver Code

    let a = [ 1, 0, 1, 0, 1, 1 ];
    let n = a.length;

    document.write(minSwaps(a, n));

// This code is contributed by shivanisinghss2110

</script>
```

**Output**

```
1
```

复杂性:

时间:O(n)

空间:0(1)