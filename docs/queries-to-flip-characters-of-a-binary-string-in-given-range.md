# 查询给定范围内二进制字符串的翻转字符

> 原文:[https://www . geesforgeks . org/query-to-flip-给定范围内的二进制字符串字符/](https://www.geeksforgeeks.org/queries-to-flip-characters-of-a-binary-string-in-given-range/)

给定一个[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/)、**字符串**和一个 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/) **Q[][]** 表示形式为 **{L，R}** 的查询。在每个查询中，切换索引**【L，R】**中存在的二进制字符串的所有字符。任务是通过执行所有查询来打印[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/)。

**示例:**

> **输入:**str =“101010”，Q[][] = { {0，1}，{2，5}，{2，3}，{1，4}，{0，5} }
> **输出:** 111000
> **解释:**
> 查询 1:切换索引[0，1]中 str 的所有字符。因此，str 变成了“011010”。
> 查询 2:切换索引[2，5]中字符串的所有字符。因此，str 变成了“010101”。
> 查询 3:切换索引[2，3]中字符串的所有字符。因此，str 变成了“011001”。
> 查询 4:切换索引[1，4]中字符串的所有字符。因此，str 变成“000111”。
> 查询 5:切换索引[0，5]中字符串的所有字符。因此，字符串变为“111000”。
> 因此，需要的二进制字符串为“111000”。
> 
> **输入:** str = "00101 "，Q[][]={ {0，2}，{2，3}，{1，4} }
> **输出:** 10000

**天真方法:**解决问题最简单的方法是[遍历所有查询数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并切换索引**【L，R】**中的所有字符。最后，打印二进制字符串。

***时间复杂度:** O(M * N)，其中 N 表示二进制字符串*的长度。
***辅助空间:** O(1)*

**高效方法:**优化上述方法的思路是使用[前缀和数组技术](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)。按照以下步骤解决问题:

*   初始化一个数组，比如说 **prefixCnt[]** 来存储二进制字符串的第 i <sup>个</sup>元素切换的次数的值。
*   [遍历查询 Q[][]数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个查询，更新**前缀【Q[I][0]】+ = 1**和**前缀【Q[I][1]+1】-= 1**的值。
*   [遍历前缀[]数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，取前缀[]数组的[前缀和。](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)
*   最后，[遍历二进制字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)并检查**prefixcent[I]% 2 = = 1**的值是否存在。如果发现为真，则切换二进制字符串的第 i <sup>个</sup>元素。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the binary string by
// performing all the given queries
string toggleQuery(string str, int Q[][2],
                   int M)
{

    // Stores length of the string
    int N = str.length();

    // prefixCnt[i]: Stores number
    // of times str[i] toggled by
    // performing all the queries
    int prefixCnt[N + 1] = { 0 };

    for (int i = 0; i < M; i++) {

        // Update prefixCnt[Q[i][0]]
        prefixCnt[Q[i][0]] += 1;

        // Update prefixCnt[Q[i][1] + 1]
        prefixCnt[Q[i][1] + 1] -= 1;
    }

    // Calculate prefix sum of prefixCnt[i]
    for (int i = 1; i <= N; i++) {
        prefixCnt[i] += prefixCnt[i - 1];
    }

    // Traverse prefixCnt[] array
    for (int i = 0; i < N; i++) {

        // If ith element toggled
        // odd number of times
        if (prefixCnt[i] % 2) {

            // Toggled i-th element
            // of binary string
            str[i] = '1' - str[i] + '0';
        }
    }
    return str;
}

// Driver Code
int main()
{
    string str = "101010";
    int Q[][2] = { { 0, 1 }, { 2, 5 },
                   { 2, 3 }, { 1, 4 },
                   { 0, 5 } };
    int M = sizeof(Q) / sizeof(Q[0]);
    cout << toggleQuery(str, Q, M);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG{

// Function to find the binary
// String by performing all the
// given queries
static String toggleQuery(char[] str,
                          int Q[][], int M)
{
  // Stores length of the String
  int N = str.length;

  // prefixCnt[i]: Stores number
  // of times str[i] toggled by
  // performing all the queries
  int prefixCnt[] = new int[N + 1];

  for (int i = 0; i < M; i++)
  {
    // Update prefixCnt[Q[i][0]]
    prefixCnt[Q[i][0]] += 1;

    // Update prefixCnt[Q[i][1] + 1]
    prefixCnt[Q[i][1] + 1] -= 1;
  }

  // Calculate prefix sum of
  // prefixCnt[i]
  for (int i = 1; i <= N; i++)
  {
    prefixCnt[i] += prefixCnt[i - 1];
  }

  // Traverse prefixCnt[] array
  for (int i = 0; i < N; i++)
  {
    // If ith element toggled
    // odd number of times
    if (prefixCnt[i] % 2 == 1)
    {
      // Toggled i-th element
      // of binary String
      str[i] = (char)('1' -
                str[i] + '0');

    }
  }
  return String.valueOf(str);
}

// Driver Code
public static void main(String[] args)
{
  String str = "101010";
  int Q[][] = {{0, 1}, {2, 5},
               {2, 3}, {1, 4},
               {0, 5}};
  int M = Q.length;
  System.out.print(
  toggleQuery(str.toCharArray(),
              Q, M));
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the binary by
# performing all the given queries
def toggleQuery(strr, Q, M):

    strr = [i for i in strr]

    # Stores length of the string
    N = len(strr)

    # prefixCnt[i]: Stores number
    # of times strr[i] toggled by
    # performing all the queries
    prefixCnt = [0] * (N + 1)

    for i in range(M):

        # Update prefixCnt[Q[i][0]]
        prefixCnt[Q[i][0]] += 1

        # Update prefixCnt[Q[i][1] + 1]
        prefixCnt[Q[i][1] + 1] -= 1

    # Calculate prefix sum of prefixCnt[i]
    for i in range(1, N + 1):
        prefixCnt[i] += prefixCnt[i - 1]

    # Traverse prefixCnt[] array
    for i in range(N):

        # If ith element toggled
        # odd number of times
        if (prefixCnt[i] % 2):

            # Toggled i-th element
            # of binary string
            strr[i] = (chr(ord('1') -
                           ord(strr[i]) +
                           ord('0')))

    return "".join(strr)

# Driver Code
if __name__ == '__main__':

    strr = "101010";
    Q = [ [ 0, 1 ],[ 2, 5 ],
          [ 2, 3 ],[ 1, 4 ],
          [ 0, 5 ] ]
    M = len(Q)

    print(toggleQuery(strr, Q, M))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

// Function to find the binary
// String by performing all the
// given queries
static String toggleQuery(char[] str,
                          int [,]Q ,
                          int M)
{
  // Stores length of the String
  int N = str.Length;

  // prefixCnt[i]: Stores number
  // of times str[i] toggled by
  // performing all the queries
  int []prefixCnt = new int[N + 1];

  for (int i = 0; i < M; i++)
  {
    // Update prefixCnt[Q[i,0]]
    prefixCnt[Q[i, 0]] += 1;

    // Update prefixCnt[Q[i,1] + 1]
    prefixCnt[Q[i, 1] + 1] -= 1;
  }

  // Calculate prefix sum of
  // prefixCnt[i]
  for (int i = 1; i <= N; i++)
  {
    prefixCnt[i] += prefixCnt[i - 1];
  }

  // Traverse prefixCnt[] array
  for (int i = 0; i < N; i++)
  {
    // If ith element toggled
    // odd number of times
    if (prefixCnt[i] % 2 == 1)
    {
      // Toggled i-th element
      // of binary String
      str[i] = (char)('1' -
                str[i] + '0');

    }
  }
  return String.Join("", str);
}

// Driver Code
public static void Main(String[] args)
{
  String str = "101010";
  int [,]Q = {{0, 1}, {2, 5},
              {2, 3}, {1, 4},
              {0, 5}};
  int M = Q.GetLength(0);
  Console.Write(toggleQuery(str.ToCharArray(),
                            Q, M));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach

// Function to find the binary
// String by performing all the
// given queries
function toggleQuery(str, Q, M)
{

    // Stores length of the String
  let N = str.length;

  // prefixCnt[i]: Stores number
  // of times str[i] toggled by
  // performing all the queries
  let prefixCnt = new Array(N + 1);
  for(let i = 0; i < N + 1; i++)
  {
      prefixCnt[i] = 0;
  }

  for (let i = 0; i < M; i++)
  {
    // Update prefixCnt[Q[i][0]]
    prefixCnt[Q[i][0]] += 1;

    // Update prefixCnt[Q[i][1] + 1]
    prefixCnt[Q[i][1] + 1] -= 1;
  }

  // Calculate prefix sum of
  // prefixCnt[i]
  for (let i = 1; i <= N; i++)
  {
    prefixCnt[i] += prefixCnt[i - 1];
  }

  // Traverse prefixCnt[] array
  for (let i = 0; i < N; i++)
  {
    // If ith element toggled
    // odd number of times
    if (prefixCnt[i] % 2 == 1)
    {
      // Toggled i-th element
      // of binary String
      str[i] = String.fromCharCode('1'.charCodeAt(0) -
                str[i].charCodeAt(0) + '0'.charCodeAt(0));

    }
  }
  return (str).join("");
}

// Driver Code
let str = "101010";
let Q = [[0, 1], [2, 5],
[2, 3], [1, 4],
[0, 5]];
let M = Q.length;
document.write(
toggleQuery(str.split(""),
            Q, M));

// This code is contributed by patel2127
</script>
```

**Output:** 

```
111000
```

***时间复杂度:** O(N + |Q|)，其中 N 是二进制字符串的长度。*
***辅助空间:** O(N)*