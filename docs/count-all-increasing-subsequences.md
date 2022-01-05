# 计数所有递增的子序列

> 原文:[https://www . geesforgeks . org/count-all-递增-subseries/](https://www.geeksforgeeks.org/count-all-increasing-subsequences/)

给我们一组数字(值在 0 到 9 的范围内)。任务是计算数组中所有可能的子序列，使得在每个子序列中，每个数字都大于它在子序列中的前几个数字。

示例:

```
Input : arr[] = {1, 2, 3, 4}
Output: 15
There are total increasing subsequences
{1}, {2}, {3}, {4}, {1,2}, {1,3}, {1,4}, 
{2,3}, {2,4}, {3,4}, {1,2,3}, {1,2,4}, 
{1,3,4}, {2,3,4}, {1,2,3,4}

Input : arr[] = {4, 3, 6, 5}
Output: 8
Sub-sequences are {4}, {3}, {6}, {5}, 
{4,6}, {4,5}, {3,6}, {3,5}

Input : arr[] = {3, 2, 4, 5, 4}
Output : 14
Sub-sequences are {3}, {2}, {4}, {3,4},
{2,4}, {5}, {3,5}, {2,5}, {4,5}, {3,2,5}
{3,4,5}, {4}, {3,4}, {2,4}
```

**方法 1(类似于 LIS)**

一个简单的解决方法是使用最长增加子序列(LIS) 问题的[动态规划解。像](https://www.geeksforgeeks.org/dynamic-programming-set-3-longest-increasing-subsequence/) [LIS](https://www.geeksforgeeks.org/dynamic-programming-set-3-longest-increasing-subsequence/) 问题一样，我们首先计算在每个索引处结束的递增子序列的计数。最后，我们返回所有值的和(在 LCS 问题中，我们返回所有值的最大值)。

```
// We count all increasing subsequences ending at every 
// index i
subCount(i) = Count of increasing subsequences ending 
              at arr[i]. 

// Like LCS, this value can be recursively computed
subCount(i) = 1 + ∑ subCount(j) 
              where j is index of all elements
              such that arr[j] < arr[i] and j < i.
1 is added as every element itself is a subsequence
of size 1.

// Finally we add all counts to get the result.
Result = ∑ subCount(i)
         where i varies from 0 to n-1.
```

插图:

```
For example, arr[] = {3, 2, 4, 5, 4}

// There are no smaller elements on left of arr[0] 
// and arr[1]
subCount(0) = 1
subCount(1) = 1  

// Note that arr[0] and arr[1] are smaller than arr[2]
subCount(2) = 1 + subCount(0) + subCount(1)  = 3

subCount(3) = 1 + subCount(0) + subCount(1) + subCount(2) 
            = 1 + 1 + 1 + 3
            = 6

subCount(3) = 1 + subCount(0) + subCount(1)
            = 1 + 1 + 1
            = 3

Result = subCount(0) + subCount(1) + subCount(2) + subCount(3)
       = 1 + 1 + 3 + 6 + 3
       = 14.
```

时间复杂度:O(n)<sup>2</sup>)
辅助空间:O(n)
参照[本](https://ide.geeksforgeeks.org/cLGaNg)执行。

**方法 2(高效)**

上面的解决方案没有利用我们在给定数组中只有 10 个可能值的事实。我们可以通过使用数组 count[]来使用这个事实，这样 count[d]存储的当前计数位数小于 d。

```
For example, arr[] = {3, 2, 4, 5, 4}

// We create a count array and initialize it as 0.
count[10] = {0, 0, 0, 0, 0, 0, 0, 0, 0, 0}

// Note that here value is used as index to store counts
count[3] += 1 = 1  // i = 0, arr[0] = 3
count[2] += 1 = 1  // i = 1, arr[0] = 2

// Let us compute count for arr[2] which is 4
count[4] += 1 + count[3] + count[2] += 1 + 1 + 1  = 3

// Let us compute count for arr[3] which is 5
count[5] += 1 + count[3] + count[2] + count[4] 
         += 1 + 1 + 1 + 3
         = 6

// Let us compute count for arr[4] which is 4
count[4] += 1 + count[0] + count[1]
         += 1 + 1 + 1
         += 3
         = 3 + 3
         = 6

Note that count[] = {0, 0, 1, 1, 6, 6, 0, 0, 0, 0}                  
Result = count[0] + count[1] + ... + count[9]
       = 1 + 1 + 6 + 6 {count[2] = 1, count[3] = 1
                        count[4] = 6, count[5] = 6} 
       = 14.
```

以下是上述想法的实现。

## C++

```
// C++ program to count increasing subsequences
// in an array of digits.
#include<bits/stdc++.h>
using namespace std;

// Function To Count all the sub-sequences
// possible in which digit is greater than
// all previous digits arr[] is array of n
// digits
int countSub(int arr[], int n)
{
    // count[] array is used to store all sub-
    // sequences possible using that digit
    // count[] array covers all the digit
    // from 0 to 9
    int count[10] = {0};

    // scan each digit in arr[]
    for (int i=0; i<n; i++)
    {
        // count all possible sub-sequences by
        // the digits less than arr[i] digit
        for (int j=arr[i]-1; j>=0; j--)
            count[arr[i]] += count[j];

        // store sum of all sub-sequences plus
        // 1 in count[] array
        count[arr[i]]++;
    }

    // now sum up the all sequences possible in
    // count[] array
    int result = 0;
    for (int i=0; i<10; i++)
        result += count[i];

    return result;
}

// Driver program to run the test case
int main()
{
    int arr[] = {3, 2, 4, 5, 4};
    int n = sizeof(arr)/sizeof(arr[0]);

    cout << countSub(arr,n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count increasing
// subsequences in an array of digits.
import java.io.*;

class GFG {

    // Function To Count all the sub-sequences
    // possible in which digit is greater than
    // all previous digits arr[] is array of n
    // digits
    static int countSub(int arr[], int n)
    {
        // count[] array is used to store all
        // sub-sequences possible using that
        // digit count[] array covers all
        // the digit from 0 to 9
        int count[] = new int[10]; 

        // scan each digit in arr[]
        for (int i = 0; i < n; i++)
        {
            // count all possible sub-
            // sequences by the digits
            // less than arr[i] digit
            for (int j = arr[i] - 1; j >= 0; j--)
                count[arr[i]] += count[j]; 

            // store sum of all sub-sequences
            // plus 1 in count[] array
            count[arr[i]]++;
        }  

        // now sum up the all sequences
        // possible in count[] array
        int result = 0;
        for (int i = 0; i < 10; i++)
            result += count[i];

        return result;
    }

    // Driver program to run the test case
    public static void main(String[] args)
    {
        int arr[] = {3, 2, 4, 5, 4};
        int n = arr.length;

        System.out.println(countSub(arr,n));
    }
}
// This code is contributed by Prerna Saini
```

## 蟒蛇 3

```
# Python3 program to count increasing
# subsequences in an array of digits.

# Function To Count all the sub-
# sequences possible in which digit
# is greater than all previous digits
# arr[] is array of n digits
def countSub(arr, n):

    # count[] array is used to store all
    # sub-sequences possible using that
    # digit count[] array covers all the
    # digit from 0 to 9
    count = [0 for i in range(10)]

    # scan each digit in arr[]
    for i in range(n):

        # count all possible sub-sequences by
        # the digits less than arr[i] digit
        for j in range(arr[i] - 1, -1, -1):
            count[arr[i]] += count[j]

        # store sum of all sub-sequences
        # plus 1 in count[] array
        count[arr[i]] += 1

    # Now sum up the all sequences
    # possible in count[] array
    result = 0
    for i in range(10):
        result += count[i]

    return result

# Driver Code
arr = [3, 2, 4, 5, 4]
n = len(arr)
print(countSub(arr, n))

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# program to count increasing
// subsequences in an array of digits.
using System;
class GFG {

    // Function To Count all the sub-sequences
    // possible in which digit is greater than
    // all previous digits arr[] is array of n
    // digits
    static int countSub(int []arr, int n)
    {
        // count[] array is used to store all
        // sub-sequences possible using that
        // digit count[] array covers all
        // the digit from 0 to 9
        int []count = new int[10]; 

        // scan each digit in arr[]
        for (int i = 0; i < n; i++)
        {
            // count all possible sub-
            // sequences by the digits
            // less than arr[i] digit
            for (int j = arr[i] - 1; j >= 0; j--)
                count[arr[i]] += count[j]; 

            // store sum of all sub-sequences
            // plus 1 in count[] array
            count[arr[i]]++;
        }  

        // now sum up the all sequences
        // possible in count[] array
        int result = 0;
        for (int i = 0; i < 10; i++)
            result += count[i];

        return result;
    }

    // Driver program
    public static void Main()
    {
        int []arr = {3, 2, 4, 5, 4};
        int n = arr.Length;

        Console.WriteLine(countSub(arr,n));
    }
}
// This code is contributed by Anant Agarwal.
```

## java 描述语言

```
<script>

// Javascript program to count increasing
// subsequences in an array of digits.

// Function To Count all the sub-sequences
// possible in which digit is greater than
// all previous digits arr[] is array of n
// digits
function countSub(arr, n)
{

    // count[] array is used to store all sub-
    // sequences possible using that digit
    // count[] array covers all the digit
    // from 0 to 9
    let count = new Array(10).fill(0);

    // Scan each digit in arr[]
    for(let i = 0; i < n; i++)
    {

        // Count all possible sub-sequences by
        // the digits less than arr[i] digit
        for(let j = arr[i] - 1; j >= 0; j--)
            count[arr[i]] += count[j];

        // Store sum of all sub-sequences plus
        // 1 in count[] array
        count[arr[i]]++;
    }

    // Now sum up the all sequences possible in
    // count[] array
    let result = 0;
    for(let i = 0; i < 10; i++)
        result += count[i];

    return result;
}

// Driver code
let arr = [ 3, 2, 4, 5, 4 ];
let n = arr.length;

document.write(countSub(arr, n));

// This code is contributed by _saurabh_jaiswal

</script>
```

输出:

```
14
```

时间复杂度:O(n)注意，内部循环最多运行 10 次。
辅助空间:O(1)注意计数最多有-10 个元素。

本文由 [**沙莎克·米什拉(古卢)**](https://practice.geeksforgeeks.org/user-profile.php?user=Shashank%20Mishra) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。