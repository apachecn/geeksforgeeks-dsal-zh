# 最小子阵列，其和是阵列大小的倍数

> 原文:[https://www . geesforgeks . org/minist-subarray-what-sum-multiple-size/](https://www.geeksforgeeks.org/smallest-subarray-whose-sum-multiple-size/)

给定一个大小为 N 的阵列，我们需要找到最小大小的子阵列，其和可被阵列大小 N 整除。
**示例:**

```
Input  : arr[] = [1, 1, 2, 2, 4, 2]    
Output : [2 4]
Size of array, N = 6    
Following subarrays have sum as multiple of N
[1, 1, 2, 2], [2, 4], [1, 1, 2, 2, 4, 2]
The smallest among all is [2 4]
```

我们可以考虑以下事实来解决这个问题，

```
Let S[i] denotes sum of first i elements i.e.  
   S[i] = a[1] + a[2] .. + a[i]
Now subarray arr(i, i + x) has sum multiple of N then,
  (arr(i] + arr[i+1] + .... + arr[i + x])) % N = 0
  (S[i+x] – S[i] ) % N  = 0
  S[i] % N = S[i + x] % N 
```

我们需要找到满足上述条件的 x 的最小值。这可以使用另一个大小为 N 的数组 modIdx 在时间复杂度为 O(N)的单次迭代中实现。数组 **modIdx** 用所有元素初始化为-1。 **modIdx[k]** 在每次迭代中都要用 I 更新，其中 k = sum % N.
现在在每次迭代中，我们需要根据 sum % N 的值更新**modIdx[k]**
我们需要检查两件事，
如果在任何时刻 k = 0 并且是我们第一次更新 **modIdx[0]** (即 **modIdx[0]** 被 因为(i + 1)将是子阵列的长度，子阵列的和是 N 的倍数
在其他情况下，每当我们得到一个 mod 值时，如果这个索引不是-1，这意味着它被其他一些和值更新，这些和值的索引存储在那个索引处，我们用这个差值更新 x，即通过 I–**modIdx[k]**。
在上述每个操作之后，我们为子阵列更新长度的最小值和相应的起始索引和结束索引。最后，这给出了我们问题的解决方案。

## C++

```
// C++ program to find subarray whose sum
// is multiple of size
#include <bits/stdc++.h>
using namespace std;

// Method prints smallest subarray whose sum is
// multiple of size
void printSubarrayMultipleOfN(int arr[], int N)
{
    // A direct index table to see if sum % N
    // has appeared before or not.  
    int modIdx[N];

    //  initialize all mod index with -1
    for (int i = 0; i < N; i++)
        modIdx[i] = -1;

    // initializing minLen and curLen with larger
    // values
    int minLen = N + 1;
    int curLen = N + 1;

    // To store sum of array elements
    int sum = 0;

    //  looping for each value of array
    int l, r;
    for (int i = 0; i < N; i++)
    {
        sum += arr[i];
        sum %= N;

        // If this is the first time we have
        // got mod value as 0, then S(0, i) % N
        // == 0
        if (modIdx[sum] == -1 && sum == 0)
            curLen = i + 1;

        // If we have reached this mod before then
        // length of subarray will be i - previous_position
        if (modIdx[sum] != -1)
            curLen = i - modIdx[sum];

        //  choose minimum length os subarray till now
        if (curLen < minLen)
        {
            minLen = curLen;

            //  update left and right indices of subarray
            l = modIdx[sum] + 1;
            r = i;
        }
        modIdx[sum] = i;
    }

    //  print subarray
    for (int i = l; i <= r; i++)
        cout << arr[i] << " ";
    cout << endl;
}

//  Driver code to test above method
int main()
{
    int arr[] = {1, 1, 2, 2, 4, 2};
    int N = sizeof(arr) / sizeof(int);

    printSubarrayMultipleOfN(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find subarray whose sum
// is multiple of size
class GFG {

    // Method prints smallest subarray whose sum is
    // multiple of size
    static void printSubarrayMultipleOfN(int arr[],
                                              int N)
    {

        // A direct index table to see if sum % N
        // has appeared before or not.
        int modIdx[] = new int[N];

        // initialize all mod index with -1
        for (int i = 0; i < N; i++)
            modIdx[i] = -1;

        // initializing minLen and curLen with
        // larger values
        int minLen = N + 1;
        int curLen = N + 1;

        // To store sum of array elements
        int sum = 0;

        // looping for each value of array
        int l = 0, r = 0;

        for (int i = 0; i < N; i++) {
            sum += arr[i];
            sum %= N;

            // If this is the first time we
            // have got mod value as 0, then
            // S(0, i) % N == 0
            if (modIdx[sum] == -1 && sum == 0)
                curLen = i + 1;

            // If we have reached this mod before
            // then length of subarray will be i
            // - previous_position
            if (modIdx[sum] != -1)
                curLen = i - modIdx[sum];

            // choose minimum length os subarray
            // till now
            if (curLen < minLen) {
                minLen = curLen;

                // update left and right indices
                // of subarray
                l = modIdx[sum] + 1;
                r = i;
            }

            modIdx[sum] = i;
        }

        // print subarray
        for (int i = l; i <= r; i++)
            System.out.print(arr[i] + " ");

        System.out.println();
    }

    // Driver program
    public static void main(String arg[])
    {
        int arr[] = { 1, 1, 2, 2, 4, 2 };
        int N = arr.length;

        printSubarrayMultipleOfN(arr, N);
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to find subarray
# whose sum is multiple of size

# Method prints smallest subarray
# whose sum is multiple of size
def printSubarrayMultipleOfN(arr, N):

    # A direct index table to see if sum % N
    # has appeared before or not.
    modIdx = [0 for i in range(N)]

    # initialize all mod index with -1
    for i in range(N):
        modIdx[i] = -1

    # initializing minLen and curLen
    # with larger values
    minLen = N + 1
    curLen = N + 1

    # To store sum of array elements
    sum = 0

    # looping for each value of array
    l = 0; r = 0
    for i in range(N):

        sum += arr[i]
        sum %= N

        # If this is the first time we have
        # got mod value as 0, then S(0, i) % N
        # == 0
        if (modIdx[sum] == -1 and sum == 0):
            curLen = i + 1

        # If we have reached this mod before then
        # length of subarray will be i - previous_position
        if (modIdx[sum] != -1):
            curLen = i - modIdx[sum]

        # choose minimum length os subarray till now
        if (curLen < minLen):

            minLen = curLen

            # update left and right indices of subarray
            l = modIdx[sum] + 1
            r = i

        modIdx[sum] = i

    # print subarray
    for i in range(l, r + 1):
        print(arr[i] , " ", end = "")
    print()

# Driver program
arr = [1, 1, 2, 2, 4, 2]
N = len(arr)
printSubarrayMultipleOfN(arr, N)

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# program to find subarray whose sum
// is multiple of size
using System;
class GFG {

    // Method prints smallest subarray whose sum is
    // multiple of size
    static void printSubarrayMultipleOfN(int []arr,
                                            int N)
    {

        // A direct index table to see if sum % N
        // has appeared before or not.
        int []modIdx = new int[N];

        // initialize all mod index with -1
        for (int i = 0; i < N; i++)
            modIdx[i] = -1;

        // initializing minLen and curLen with
        // larger values
        int minLen = N + 1;
        int curLen = N + 1;

        // To store sum of array elements
        int sum = 0;

        // looping for each value of array
        int l = 0, r = 0;

        for (int i = 0; i < N; i++) {
            sum += arr[i];
            sum %= N;

            // If this is the first time we
            // have got mod value as 0, then
            // S(0, i) % N == 0
            if (modIdx[sum] == -1 && sum == 0)
                curLen = i + 1;

            // If we have reached this mod before
            // then length of subarray will be i
            // - previous_position
            if (modIdx[sum] != -1)
                curLen = i - modIdx[sum];

            // choose minimum length os subarray
            // till now
            if (curLen < minLen) {
                minLen = curLen;

                // update left and right indices
                // of subarray
                l = modIdx[sum] + 1;
                r = i;
            }

            modIdx[sum] = i;
        }

        // print subarray
        for (int i = l; i <= r; i++)
            Console.Write(arr[i] + " ");

        Console.WriteLine();
    }

    // Driver Code
    public static void Main()
    {
        int []arr = {1, 1, 2, 2, 4, 2};
        int N = arr.Length;

        printSubarrayMultipleOfN(arr, N);
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find subarray
// whose sum is multiple of size

// Method prints smallest subarray
// whose sum is multiple of size
function printSubarrayMultipleOfN($arr,
                                  $N)
{
    // A direct index table to see
    // if sum % N has appeared
    // before or not.
    $modIdx = array();

    // initialize all mod
    // index with -1
    for ($i = 0; $i < $N; $i++)
        $modIdx[$i] = -1;

    // initializing minLen and
    // curLen with larger values
    $minLen = $N + 1;
    $curLen = $N + 1;

    // To store sum of
    // array elements
    $sum = 0;

    // looping for each
    // value of array
    $l; $r;
    for ($i = 0; $i < $N; $i++)
    {
        $sum += $arr[$i];
        $sum %= $N;

        // If this is the first time
        // we have got mod value as 0,
        // then S(0, i) % N == 0
        if ($modIdx[$sum] == -1 &&
            $sum == 0)
            $curLen = $i + 1;

        // If we have reached this mod
        // before then length of subarray
        // will be i - previous_position
        if ($modIdx[$sum] != -1)
            $curLen = $i - $modIdx[$sum];

        // choose minimum length
        // as subarray till now
        if ($curLen < $minLen)
        {
            $minLen = $curLen;

            // update left and right
            // indices of subarray
            $l = $modIdx[$sum] + 1;
            $r = $i;
        }
        $modIdx[$sum] = $i;
    }

    // print subarray
    for ($i = $l; $i <= $r; $i++)
        echo $arr[$i] , " ";
    echo "\n" ;
}

// Driver Code
$arr = array(1, 1, 2, 2, 4, 2);
$N = count($arr);

printSubarrayMultipleOfN($arr, $N);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

    // Javascript program to find subarray whose sum
    // is multiple of size

    // Method prints smallest subarray whose sum is
    // multiple of size
    function printSubarrayMultipleOfN(arr, N)
    {

        // A direct index table to see if sum % N
        // has appeared before or not.
        let modIdx = new Array(N);

        // initialize all mod index with -1
        for (let i = 0; i < N; i++)
            modIdx[i] = -1;

        // initializing minLen and curLen with
        // larger values
        let minLen = N + 1;
        let curLen = N + 1;

        // To store sum of array elements
        let sum = 0;

        // looping for each value of array
        let l = 0, r = 0;

        for (let i = 0; i < N; i++) {
            sum += arr[i];
            sum %= N;

            // If this is the first time we
            // have got mod value as 0, then
            // S(0, i) % N == 0
            if (modIdx[sum] == -1 && sum == 0)
                curLen = i + 1;

            // If we have reached this mod before
            // then length of subarray will be i
            // - previous_position
            if (modIdx[sum] != -1)
                curLen = i - modIdx[sum];

            // choose minimum length os subarray
            // till now
            if (curLen < minLen) {
                minLen = curLen;

                // update left and right indices
                // of subarray
                l = modIdx[sum] + 1;
                r = i;
            }

            modIdx[sum] = i;
        }

        // print subarray
        for (let i = l; i <= r; i++)
            document.write(arr[i] + " ");

        document.write("</br>");
    }

    let arr = [1, 1, 2, 2, 4, 2];
    let N = arr.length;

    printSubarrayMultipleOfN(arr, N);

</script>
```

**输出:**

```
2 4
```

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。