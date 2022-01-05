# 通过二进制字符串的循环旋转，检查任意一对连续的 1 是否最多能被 M 个 0 分开

> 原文:[https://www . geeksforgeeks . org/check-if-of-no-pair-of-on-continuous-1-1-最多可以通过循环旋转二进制字符串来分隔 m-0/](https://www.geeksforgeeks.org/check-if-any-pair-of-consecutive-1s-can-be-separated-by-at-most-m-0s-by-circular-rotation-of-a-binary-string/)

给定一个长度为 **N** 的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **S** 和一个正整数 **M** ，任务是检查是否有可能[将字符串循环](https://www.geeksforgeeks.org/left-rotation-right-rotation-string-2/)任意次，使得任意一对连续的 **1** s 最多相隔 **M** **0s** 。如果可能，则打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:** S = "101001 "，M = 1
> **输出:**是
> **说明:**将给定字符串的字符右移 1 位。因此，字符串 S 修改为“110100”，剩下所有连续的一对 **1s** 最多由 M(= 1) **0** s 隔开。
> 
> **输入:** S = 1001001，M = 1
> T3】输出:否

**方法:**给定的问题可以基于这样的观察来解决，即如果有超过 1 对相邻的 **1s** 在它们之间具有超过 **M** 数量的 **0s** ，则不可能满足给定的条件，因为只有这样的一对可以通过旋转弦线来处理，使得它们之间的所有 **0** s 都在末端。
按照以下步骤解决问题:

*   初始化一个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)，比如 **V** ，将所有 **1** s 的[指数存储在给定的字符串](https://www.geeksforgeeks.org/check-if-all-the-1s-in-a-binary-string-are-equidistant-or-not/) **S** 中。
*   初始化一个变量，比如说**计数**，以存储它们之间大于**M**T6【0s】T7 的 **1s** 对的数量。
*   [遍历给定的字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** 并将**【1】**的所有[索引存储在向量 **V** 中。](https://www.geeksforgeeks.org/find-last-index-character-string/)
*   [遍历向量](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **V** ，从索引 **1** 开始使用变量，说出 **i** ，并执行以下步骤:
    *   将字符串 **S** 中索引**V【I】**和**V【I–1】**之间的 **0s** 的数量存储在变量 **T** 中作为**(V【I】–V【I–1】–1)**。
    *   如果 **T** 的值大于 **M** ，则将**计数**的值增加 **1** 。
*   如果 **'1'** 的第一次和最后一次出现之间的 **0s** 的数量大于 **M** ，那么将**的值递增**1。
*   完成上述步骤后，如果**计数**的值最多为**1**，则打印**是**。否则，打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if any pair of
// consecutive 1s can be separated by at
// most M 0s by circular rotation of string S
void rotateString(int n, int m, string s)
{
    // Stores the indices of all 1s
    vector<int> v;

    // Store the number of pairs
    // separated by at least M 0s
    int cnt = 0;

    // Traverse the string
    for (int i = 0; i < n; i++) {

        if (s[i] == '1') {

            // Store the current index
            v.push_back(i);
        }
    }

    // Traverse the array containing indices
    for (int i = 1; i < (int)v.size(); i++) {

        // If the number of 0s > M,
        // then increment cnt by 1
        if ((v[i] - v[i - 1] - 1) > m) {

            // Increment cnt
            cnt++;
        }
    }

    // Check if at least M '0's lie between
    // the first and last occurrence of '1'
    if (v.size() >= 2
        && (n - (v.back() - v[0]) - 1) > m) {

        // Increment cnt
        cnt++;
    }

    // If the value of cnt <= 1, then
    // rotation of string is possible
    if (cnt <= 1) {
        cout << "Yes";
    }

    // Otherwise
    else {
        cout << "No";
    }
}

// Driver Code
int main()
{
    string S = "101001";
    int M = 1;
    int N = S.size();
    rotateString(N, M, S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to check if any pair of
// consecutive 1s can be separated by at
// most M 0s by circular rotation of string S
static void rotateString(int n, int m, String s)
{

    // Stores the indices of all 1s
    int v[] = new int[n];

    // Store the number of pairs
    // separated by at least M 0s
    int cnt = 0;
    int j = 0;

    // Traverse the string
    for(int i = 0; i < n; i++)
    {
        if (s.charAt(i) == '1')
        {

            // Store the current index
            v[j] = i;
            j += 1;
        }
    }

    // Traverse the array containing indices
    for(int i = 1; i < j; i++)
    {

        // If the number of 0s > M,
        // then increment cnt by 1
        if ((v[i] - v[i - 1] - 1) > m)
        {

            // Increment cnt
            cnt++;
        }
    }

    // Check if at least M '0's lie between
    // the first and last occurrence of '1'
    if (j >= 2 && (n - (v[j - 1] - v[0]) - 1) > m)
    {

        // Increment cnt
        cnt++;
    }

    // If the value of cnt <= 1, then
    // rotation of string is possible
    if (cnt <= 1)
    {
        System.out.print("Yes");
    }

    // Otherwise
    else
    {
        System.out.print("No");
    }
}

// Driver Code
public static void main (String[] args)
{
    String S = "101001";
    int M = 1;
    int N = S.length();

    rotateString(N, M, S);
}
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if any pair of
# consecutive 1s can be separated by at
# most M 0s by circular rotation of string S
def rotateString(n, m, s):

    # Stores the indices of all 1s
    v = []

    # Store the number of pairs
    # separated by at least M 0s
    cnt = 0

    # Traverse the string
    for i in range(n):
        if (s[i] == '1'):

            # Store the current index
            v.append(i)

    # Traverse the array containing indices
    for i in range(1, len(v)):

        # If the number of 0s > M,
        # then increment cnt by 1
        if ((v[i] - v[i - 1] - 1) > m):

            # Increment cnt
            cnt += 1

    # Check if at least M '0's lie between
    # the first and last occurrence of '1'
    if (len(v) >= 2 and
       (n - (v[-1] - v[0]) - 1) > m):

        # Increment cnt
        cnt += 1

    # If the value of cnt <= 1, then
    # rotation of string is possible
    if (cnt <= 1):
        print("Yes")

    # Otherwise
    else:
        print("No")

# Driver Code
if __name__ == '__main__':

    S = "101001"
    M = 1
    N = len(S)

    rotateString(N, M, S)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to check if any pair of
// consecutive 1s can be separated by at
// most M 0s by circular rotation of string S
static void rotateString(int n, int m, string s)
{

    // Stores the indices of all 1s
    List<int> v = new List<int>();

    // Store the number of pairs
    // separated by at least M 0s
    int cnt = 0;

    // Traverse the string
    for(int i = 0; i < n; i++)
    {
        if (s[i] == '1')
        {

            // Store the current index
            v.Add(i);
        }
    }

    // Traverse the array containing indices
    for(int i = 1; i < v.Count; i++)
    {

        // If the number of 0s > M,
        // then increment cnt by 1
        if ((v[i] - v[i - 1] - 1) > m)
        {

            // Increment cnt
            cnt++;
        }
    }

    // Check if at least M '0's lie between
    // the first and last occurrence of '1'
    if (v.Count >= 2 &&
       (n - (v[v.Count - 1] - v[0]) - 1) > m)
    {

        // Increment cnt
        cnt++;
    }

    // If the value of cnt <= 1, then
    // rotation of string is possible
    if (cnt <= 1)
    {
        Console.Write("Yes");
    }

    // Otherwise
    else
    {
        Console.Write("No");
    }
}

// Driver Code
public static void Main()
{
    string S = "101001";
    int M = 1;
    int N = S.Length;

    rotateString(N, M, S);
}
}

// This code is contributed by ipg2016107
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to check if any pair of
// consecutive 1s can be separated by at
// most M 0s by circular rotation of string S

function rotateString(n, m, s)
{
    // Stores the indices of all 1s
    var v = [];

    // Store the number of pairs
    // separated by at least M 0s
    var cnt = 0;
     var i;
    // Traverse the string
    for (i = 0; i < n; i++) {

        if (s[i] == '1') {

            // Store the current index
            v.push(i);
        }
    }

    // Traverse the array containing indices
    for (i = 1; i < v.length; i++) {

        // If the number of 0s > M,
        // then increment cnt by 1
        if ((v[i] - v[i - 1] - 1) > m) {

            // Increment cnt
            cnt++;
        }
    }

    // Check if at least M '0's lie between
    // the first and last occurrence of '1'
    if (v.length >= 2
        && (n - (v[v.length-1] - v[0]) - 1) > m) {

        // Increment cnt
        cnt++;
    }

    // If the value of cnt <= 1, then
    // rotation of string is possible
    if (cnt <= 1) {
       document.write("Yes");
    }

    // Otherwise
    else {
        document.write("No");
    }
}

// Driver Code
    var S = "101001";
    var M = 1;
    var N = S.length;
    rotateString(N, M, S);

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)