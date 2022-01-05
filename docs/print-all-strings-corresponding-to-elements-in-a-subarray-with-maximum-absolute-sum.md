# 以最大绝对和打印子阵列中元素对应的所有字符串

> 原文:[https://www . geesforgeks . org/print-all-strings-对应于最大绝对和子数组中的元素/](https://www.geeksforgeeks.org/print-all-strings-corresponding-to-elements-in-a-subarray-with-maximum-absolute-sum/)

给定一个由 **N 个**对组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，每个对由一个字符串和对应于[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/)的整数值组成。任务是找到**最大绝对和** [子阵](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)并打印子阵元素对应的字符串。

**示例:**

> ***输入:** arr[] = {(“极客”，4)、(“为”、-3)、(“极客”，2)、(“教程”，3)、(“程序”，-4)}*
> ***输出:**极客为极客教程*
> ***说明:**子阵的最大绝对和为{arr[0]，..arr[3]}，求和为 6。因此，这些值之间对应的字符串是“极客”、“for”、“极客”和“教程”。*
> 
> **输入:** arr[]= {(“练习”、-7)、(“makes”，2)、(“men perfect”，5)}
> **输出:**练习
> **说明:**子阵的最大绝对和为{arr[0]}，有和 7。因此，对应的字符串是“练习”。

**天真法:**最简单的方法是[生成所有可能的子阵](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)找到最大和子阵。然后，打印对应于该子阵列的字符串。
***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**最优思路是使用[卡丹算法](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)进行一些修改，使其能够处理负值，并在绝对最小值和绝对最大值之间选择最大值。

按照以下步骤解决问题:

1.  初始化变量， **res = 0** ，存储最终答案， **start = 0** ， **end = 0** 存储所需子阵列的起始和结束索引。
2.  再初始化两个变量，比如 **posPrefix** 和 **negPrefix** ，存储之前的正前缀值和负前缀值。
3.  [遍历阵列](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** 并执行以下操作
    *   如果当前元素为负，并且如果 **arr[i] + negPrefix > res** 的值，则更新 **res 的值，开始**和**结束**索引。
    *   如果当前元素为正，并且如果 **arr[i] + posPrefix > res** 的值，则更新 **res 的值，开始**和**结束**索引。
    *   检查将当前元素添加到 **negPrefix** 是否使其大于或等于 **0** ，然后更新**start****=****I+1**并设置 **negPrefix = 0** 否则，将当前值添加到 **negPrefix** 。
    *   检查将当前元素添加到 **posPrefix** 是否使其小于或等于 **0** ，然后更新 **start = i + 1** 并设置 **posPrefix = 0** 否则，将当前值添加到 **posPrefix** 。
4.  最后，遍历**【开始，结束】**范围内的数组，打印相应的字符串。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to print strings corresponding
// to the elements present in the subarray
// with maximum absolute sum
void maximumAbsSum(pair<string, int>* arr,
                   int N)
{
    int start = 0, end = 0, res = 0,
        negIndex = 0, posIndex = 0,
        negPrefix = 0, posPrefix = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        if (arr[i].second < 0) {

            // If adding current element
            // to negative
            // prefix makes it > res
            // then update the values

            if (res < abs(arr[i].second
                          + negPrefix)) {

                res = abs(arr[i].second
                          + negPrefix);
                start = negIndex;
                end = i;
            }
        }

        else {

            // If adding current element to
            // positive prefix exceeds res
            if (res < abs(arr[i].second
                          + posPrefix)) {

                res = abs(arr[i].second
                          + posPrefix);
                start = posIndex;
                end = i;
            }
        }

        // Since negPrefix > 0, there is
        // no benefit in adding it to a
        // negative value
        if (negPrefix + arr[i].second > 0) {

            negPrefix = 0;
            negIndex = i + 1;
        }

        // Since negative + negative
        // generates a larger negative value
        else {

            negPrefix += arr[i].second;
        }

        // Since positive + positive
        // generates a larger positive number
        if (posPrefix + arr[i].second >= 0) {

            posPrefix += arr[i].second;
        }

        // Since pos_prefix < 0, there is
        // no benefit in adding it to
        // a positive value
        else {

            posPrefix = 0;
            posIndex = i + 1;
        }
    }

    // Print the corresponding strings
    for (int i = start; i <= end; i++) {
        cout << arr[i].first << " ";
    }
}

// Driver Code
int main()
{
    // Given array
    pair<string, int> arr[] = { { "geeks", 4 },
                                { "for", -3 },
                                { "geeks", 2 },
                                { "tutorial", 3 },
                                { "program", -4 } };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call to print
    // string corresponding to
    // maximum absolute subarray sum
    maximumAbsSum(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG
{
    static class pair<E,R>
    {
        E first;
        R second;
        public pair(E first, R second) 
        {
            this.first = first;
            this.second = second;
        }   
    }

// Function to print Strings corresponding
// to the elements present in the subarray
// with maximum absolute sum
static void maximumAbsSum(pair<String,Integer> []arr,
                   int N)
{
    int start = 0, end = 0, res = 0,
        negIndex = 0, posIndex = 0,
        negPrefix = 0, posPrefix = 0;

    // Traverse the array
    for (int i = 0; i < N; i++)
    {
        if (arr[i].second < 0)
        {

            // If adding current element
            // to negative
            // prefix makes it > res
            // then update the values
            if (res < Math.abs(arr[i].second
                          + negPrefix)) {

                res = Math.abs(arr[i].second
                          + negPrefix);
                start = negIndex;
                end = i;
            }
        }
        else
        {

            // If adding current element to
            // positive prefix exceeds res
            if (res < Math.abs(arr[i].second
                          + posPrefix)) {

                res = Math.abs(arr[i].second
                          + posPrefix);
                start = posIndex;
                end = i;
            }
        }

        // Since negPrefix > 0, there is
        // no benefit in adding it to a
        // negative value
        if (negPrefix + arr[i].second > 0) {

            negPrefix = 0;
            negIndex = i + 1;
        }

        // Since negative + negative
        // generates a larger negative value
        else {

            negPrefix += arr[i].second;
        }

        // Since positive + positive
        // generates a larger positive number
        if (posPrefix + arr[i].second >= 0) {

            posPrefix += arr[i].second;
        }

        // Since pos_prefix < 0, there is
        // no benefit in adding it to
        // a positive value
        else {

            posPrefix = 0;
            posIndex = i + 1;
        }
    }

    // Print the corresponding Strings
    for (int i = start; i <= end; i++) {
        System.out.print(arr[i].first+ " ");
    }
}

// Driver Code
@SuppressWarnings("unchecked")
public static void main(String[] args)
{
    // Given array
    @SuppressWarnings("rawtypes")
    pair arr[] = { new pair( "geeks", 4 ),
            new pair( "for", -3 ),
            new pair( "geeks", 2 ),
            new pair( "tutorial", 3 ),
            new pair( "program", -4 ) };

    // Size of the array
    int N = arr.length;

    // Function call to print
    // String corresponding to
    // maximum absolute subarray sum
    maximumAbsSum(arr, N);
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to print strings corresponding
# to the elements present in the subarray
# with maximum absolute sum
def maximumAbsSum(arr, N):
    start, end, res = 0, 0, 0
    negIndex, posIndex = 0, 0
    negPrefix, posPrefix = 0, 0

    # Traverse the array
    for i in range(N):
        if (arr[i][1] < 0):

            # If adding current element
            # to negative
            # prefix makes it > res
            # then update the values
            if (res < abs(arr[i][1] + negPrefix)):
                res = abs(arr[i][1] + negPrefix)
                start = negIndex
                end = i
        else:

            # If adding current element to
            # positive prefix exceeds res
            if (res < abs(arr[i][1] + posPrefix)):
                res = abs(arr[i][1] + posPrefix)
                start = posIndex
                end = i

        # Since negPrefix > 0, there is
        # no benefit in adding it to a
        # negative value
        if (negPrefix + arr[i][1] > 0):
            negPrefix = 0
            negIndex = i + 1

        # Since negative + negative
        # generates a larger negative value
        else:
            negPrefix += arr[i][1]

        # Since positive + positive
        # generates a larger positive number
        if (posPrefix + arr[i][1] >= 0):
            posPrefix += arr[i][1]

        # Since pos_prefix < 0, there is
        # no benefit in adding it to
        # a positive value
        else:
            posPrefix = 0
            posIndex = i + 1

    # Print the corresponding strings
    for i in range(start, end + 1):
        print(arr[i][0], end = " ")

# Driver Code
if __name__ == '__main__':

    # Given array
    arr = [ [ "geeks", 4 ],
            [ "for", -3 ],
            [ "geeks", 2 ],
            [ "tutorial", 3 ],
            [ "program", -4 ] ]

    # Size of the array
    N = len(arr)

    # Function call to print
    # string corresponding to
    # maximum absolute subarray sum
    maximumAbsSum(arr, N)

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
public class GFG
{
  public class pair
  {
    public string first;
    public int second;
    public pair(string first, int second) 
    {
      this.first = first;
      this.second = second;
    }   
  }

  // Function to print Strings corresponding
  // to the elements present in the subarray
  // with maximum absolute sum
  static void maximumAbsSum(pair []arr,
                            int N)
  {
    int start = 0, end = 0, res = 0,
    negIndex = 0, posIndex = 0,
    negPrefix = 0, posPrefix = 0;

    // Traverse the array
    for (int i = 0; i < N; i++)
    {
      if (arr[i].second < 0)
      {

        // If adding current element
        // to negative
        // prefix makes it > res
        // then update the values
        if (res < Math.Abs(arr[i].second
                           + negPrefix)) {

          res = Math.Abs(arr[i].second
                         + negPrefix);
          start = negIndex;
          end = i;
        }
      }
      else
      {

        // If adding current element to
        // positive prefix exceeds res
        if (res < Math.Abs(arr[i].second
                           + posPrefix)) {

          res = Math.Abs(arr[i].second
                         + posPrefix);
          start = posIndex;
          end = i;
        }
      }

      // Since negPrefix > 0, there is
      // no benefit in adding it to a
      // negative value
      if (negPrefix + arr[i].second > 0) {

        negPrefix = 0;
        negIndex = i + 1;
      }

      // Since negative + negative
      // generates a larger negative value
      else {

        negPrefix += arr[i].second;
      }

      // Since positive + positive
      // generates a larger positive number
      if (posPrefix + arr[i].second >= 0) {

        posPrefix += arr[i].second;
      }

      // Since pos_prefix < 0, there is
      // no benefit in adding it to
      // a positive value
      else {

        posPrefix = 0;
        posIndex = i + 1;
      }
    }

    // Print the corresponding Strings
    for (int i = start; i <= end; i++) {
      Console.Write(arr[i].first+ " ");
    }
  }

  // Driver Code
  public static void Main(String[] args)
  {

    // Given array
    pair []arr = { new pair( "geeks", 4 ),
                  new pair( "for", -3 ),
                  new pair( "geeks", 2 ),
                  new pair( "tutorial", 3 ),
                  new pair( "program", -4 ) };

    // Size of the array
    int N = arr.Length;

    // Function call to print
    // String corresponding to
    // maximum absolute subarray sum
    maximumAbsSum(arr, N);
  }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript program for the above approach

class pair
{
    constructor(first,second)
    {
        this.first=first;
        this.second=second;
    }
}

// Function to print Strings corresponding
// to the elements present in the subarray
// with maximum absolute sum
function maximumAbsSum(arr,N)
{
    let start = 0, end = 0, res = 0,
        negIndex = 0, posIndex = 0,
        negPrefix = 0, posPrefix = 0;

    // Traverse the array
    for (let i = 0; i < N; i++)
    {
        if (arr[i].second < 0)
        {

            // If adding current element
            // to negative
            // prefix makes it > res
            // then update the values
            if (res < Math.abs(arr[i].second
                          + negPrefix)) {

                res = Math.abs(arr[i].second
                          + negPrefix);
                start = negIndex;
                end = i;
            }
        }
        else
        {

            // If adding current element to
            // positive prefix exceeds res
            if (res < Math.abs(arr[i].second
                          + posPrefix)) {

                res = Math.abs(arr[i].second
                          + posPrefix);
                start = posIndex;
                end = i;
            }
        }

        // Since negPrefix > 0, there is
        // no benefit in adding it to a
        // negative value
        if (negPrefix + arr[i].second > 0) {

            negPrefix = 0;
            negIndex = i + 1;
        }

        // Since negative + negative
        // generates a larger negative value
        else {

            negPrefix += arr[i].second;
        }

        // Since positive + positive
        // generates a larger positive number
        if (posPrefix + arr[i].second >= 0) {

            posPrefix += arr[i].second;
        }

        // Since pos_prefix < 0, there is
        // no benefit in adding it to
        // a positive value
        else {

            posPrefix = 0;
            posIndex = i + 1;
        }
    }

    // Print the corresponding Strings
    for (let i = start; i <= end; i++) {
        document.write(arr[i].first+ " ");
    }
}

// Driver Code
// Given array
let arr=[new pair( "geeks", 4 ),
            new pair( "for", -3 ),
            new pair( "geeks", 2 ),
            new pair( "tutorial", 3 ),
            new pair( "program", -4 )];

// Size of the array
let N = arr.length;

// Function call to print
    // String corresponding to
    // maximum absolute subarray sum
    maximumAbsSum(arr, N);

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
geeks for geeks tutorial
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)