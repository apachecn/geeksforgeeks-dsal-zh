# 使一个字符串严格大于另一个字符串所需的两个字符串之间的最小交换量

> 原文:[https://www . geesforgeks . org/minimum-swap-required-two-string-to-make-one-string-严格大于其他/](https://www.geeksforgeeks.org/minimum-swaps-required-between-two-strings-to-make-one-string-strictly-greater-than-the-other/)

给定两个长度分别为 **M** 和 **N** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **A** 和 **B** ，任务是找到使字符串**A**T12】在字典上大于字符串 **B** 所需的两个字符的最小交换。

**示例:**

> **输入:** A = "1432 "，B = "789 "，M = 4，N = 3
> **输出:** 1
> **解释:**
> 一种可能的方法是在两个字符串的索引 0 处交换字符。因此，A 修改为“7432”，B 修改为“189”。
> 
> **输入:**A =“3733”，B =“3333”，M = 4，N = 4
> **输出:** 2
> **说明:**
> 第一步:将字符串 A 的索引 1 处的字符与字符串 B 的索引 0 处的字符交换，字符串 A 和 B 修改为“3333”和“7333”。
> 第二步:将字符串 A 的索引 0 处的字符换成字符串 B 的索引 0 处的字符，字符串 A 和 B 修改为“7333”和“3333”。

**方法:**可以观察到，如果 **M ≤ N** 且所有字符都相同，包括两个字符串，那么不可能使字符串 **A** 严格大于字符串 **B** 。否则，通过将两个不同的字符放在****0<sup>索引</sup>**处，最多**两次**移动，字符串 **A** 可以严格大于字符串 **B** 。**

**按照以下步骤解决问题:**

1.  **首先检查字符串 **A** 的第一个字符是否大于字符串 **B** 的第一个字符，然后打印 **0** 。**
2.  **否则，检查 **B[0] > A[0]** 是否需要 **1** 交换，所以用 **B[0]** 交换 **A[0]** ，打印 **1。****
3.  **否则，检查两个字符串中的所有字符是否相同， **M ≤ N** 则不可能，所以打印 **-1** 。**
4.  **否则，检查 **A** 中是否有小于**A【0】**的字符或大于**B【0】**的 **B** 中的字符，然后打印 **1** 。**
5.  **否则，检查 **A** 中是否有小于**A【0】**的字符，或者 **B** 中是否有大于**B【0】**的字符，然后打印 **2** 。**
6.  **否则，如果以上条件都不满足，则返回 **0** 。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum
// number of steps to make A > B
int minSteps(string A, string B, int M, int N)
{

    if (A[0] > B[0])
        return 0;

    if (B[0] > A[0]) {
        return 1;
    }

    // If all character are same and M <= N
    if (M <= N && A[0] == B[0]
        && count(A.begin(), A.end(), A[0]) == M
        && count(B.begin(), B.end(), B[0]) == N)
        return -1;

    // If there lies any character
    // in B which is greater than B[0]
    for (int i = 1; i < N; i++) {

        if (B[i] > B[0])
            return 1;
    }

    // If there lies any character
    // in A which is smaller than A[0]
    for (int i = 1; i < M; i++) {

        if (A[i] < A[0])
            return 1;
    }

    // If there lies a character which
    // is in A and greater than A[0]
    for (int i = 1; i < M; i++) {

        if (A[i] > A[0]) {

            swap(A[i], B[0]);
            swap(A[0], B[0]);
            return 2;
        }
    }

    // If there lies a character which
    // is in B and less than B[0]
    for (int i = 1; i < N; i++) {

        if (B[i] < B[0]) {

            swap(A[0], B[i]);
            swap(A[0], B[0]);
            return 2;
        }
    }

    // Otherwise
    return 0;
}

// Driver Code
int main()
{
    string A = "adsfd";
    string B = "dffff";

    int M = A.length();
    int N = B.length();

    cout << minSteps(A, B, M, N);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for above approach
import java.util.*;
import java.lang.*;
class GFG
{

  // Function to find the minimum
  // number of steps to make A > B
  static int minSteps(StringBuilder A,
                      StringBuilder B,
                      int M, int N)
  {

    if (A.charAt(0) > B.charAt(0))
      return 0;

    if (B.charAt(0) > A.charAt(0))
    {
      return 1;
    }

    // If all character are same and M <= N
    if (M <= N && A.charAt(0) == B.charAt(0)
        && count(A, A.charAt(0)) == M
        && count(B, B.charAt(0)) == N)
      return -1;

    // If there lies any character
    // in B which is greater than B[0]
    for (int i = 1; i < N; i++)
    {

      if (B.charAt(i) > B.charAt(0))
        return 1;
    }

    // If there lies any character
    // in A which is smaller than A[0]
    for (int i = 1; i < M; i++)
    {

      if (A.charAt(i) < A.charAt(0))
        return 1;
    }

    // If there lies a character which
    // is in A and greater than A[0]
    for (int i = 1; i < M; i++)
    {
      if (A.charAt(i) > A.charAt(0))
      {
        swap(A, i, B, 0);
        swap(A, 0, B, 0);
        return 2;
      }
    }

    // If there lies a character which
    // is in B and less than B[0]
    for (int i = 1; i < N; i++)
    {
      if (B.charAt(i) < B.charAt(0))
      {
        swap(A, 0, B, i);
        swap(A, 0, B, 0);
        return 2;
      }
    }

    // Otherwise
    return 0;
  }

  static int count(StringBuilder a,
                   char c)
  {
    int count = 0;
    for(int i = 0; i < a.length(); i++)
      if(a.charAt(i) == c)
        count++; 
    return count;  
  }

  static void swap(StringBuilder s1,
                   int index1,
                   StringBuilder s2,
                   int index2)
  {
    char c = s1.charAt(index1);
    s1.setCharAt(index1,s2.charAt(index2));
    s2.setCharAt(index2,c);

  }
  // Driver function
  public static void main (String[] args)
  {
    StringBuilder A = new StringBuilder("adsfd");
    StringBuilder B = new StringBuilder("dffff");
    int M = A.length();
    int N = B.length();
    System.out.println(minSteps(A, B, M, N));
  }
}

// This code is contributed by offbeat.
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Function to find the minimum
# number of steps to make A > B
def minSteps(A, B, M, N):

    if (A[0] > B[0]):
        return 0

    if (B[0] > A[0]):
        return 1

    # If all character are same and M <= N
    if (M <= N and A[0] == B[0] and
           A.count(A[0]) == M and
           B.count(B[0]) == N):
        return -1

    # If there lies any character
    # in B which is greater than B[0]
    for i in range(1, N):
        if (B[i] > B[0]):
            return 1

    # If there lies any character
    # in A which is smaller than A[0]
    for i in range(1, M):
        if (A[i] < A[0]):
            return 1

    # If there lies a character which
    # is in A and greater than A[0]
    for i in range(1, M):
        if (A[i] > A[0]):
            A[0], B[i] = B[i], A[0]
            A[0], B[0] = B[0], A[0]
            return 2

    # If there lies a character which
    # is in B and less than B[0]
    for i in range(1, N):
        if (B[i] < B[0]):
            A[0], B[i] = B[i], A[0]
            A[0], B[0] = B[0], A[0]
            return 2

    # Otherwise
    return 0

# Driver Code
if __name__ == '__main__':

    A = "adsfd"
    B = "dffff"

    M = len(A)
    N = len(B)

    print(minSteps(A, B, M, N))

# This code is contributed by mohit kumar 29
```

## **C#**

```
// C# program for above approach
using System;
using System.Text;

public class GFG
{

  // Function to find the minimum
  // number of steps to make A > B
  static int minSteps(StringBuilder A, StringBuilder B,  int M, int N)
  {
    if (A[0] > B[0])
      return 0;

    if (B[0] > A[0])
    {
      return 1;
    }

    // If all character are same and M <= N
    if (M <= N && A[0] == B[0]
        && count(A, A[0]) == M
        && count(B, B[0]) == N)
      return -1;

    // If there lies any character
    // in B which is greater than B[0]
    for (int i = 1; i < N; i++)
    {

      if (B[i] > B[0])
        return 1;
    }

    // If there lies any character
    // in A which is smaller than A[0]
    for (int i = 1; i < M; i++)
    {

      if (A[i] < A[0])
        return 1;
    }

    // If there lies a character which
    // is in A and greater than A[0]
    for (int i = 1; i < M; i++)
    {
      if (A[i] > A[0])
      {
        swap(A, i, B, 0);
        swap(A, 0, B, 0);
        return 2;
      }
    }

    // If there lies a character which
    // is in B and less than B[0]
    for (int i = 1; i < N; i++)
    {
      if (B[i] < B[0])
      {
        swap(A, 0, B, i);
        swap(A, 0, B, 0);
        return 2;
      }
    }

    // Otherwise
    return 0;

  }

  static int count(StringBuilder a,
                   char c)
  {
    int count = 0;
    for(int i = 0; i < a.Length; i++)
      if(a[i] == c)
        count++; 
    return count;  
  }

  static void swap(StringBuilder s1,
                   int index1,
                   StringBuilder s2,
                   int index2)
  {

    char c = s1[index1];
    s1[index1] = s2[index2];
    s2[index2] = c;
  }

  // Driver function
  static public void Main ()
  {
    StringBuilder A = new StringBuilder("adsfd");
    StringBuilder B = new StringBuilder("dffff");
    int M=A.Length;
    int N=B.Length;
    Console.WriteLine(minSteps(A, B, M, N));
  }
}

// This code is contributed by avanitrachhadiya2155
```

## **java 描述语言**

```
<script>
//Javascript  program to implement
// the above approach

// Function to find the minimum
// number of steps to make A > B
function minSteps( A, B,M, N)
{

    if (A[0] > B[0])
    return 0;

    if (B[0] > A[0])
    {
        return 1;
    }

    // If all character are same and M <= N
    if (M <= N && A[0] == B[0] && count(A, A[0]) == M
        && count(B, B[0]) == N)
        return -1;

    // If there lies any character
    // in B which is greater than B[0]
    for (var i = 1; i < N; i++)
    {

        if (B[i] > B[0])
            return 1;
    }

    // If there lies any character
    // in A which is smaller than A[0]
    for (var i = 1; i < M; i++)
    {

        if (A[i] < A[0])
            return 1;
    }

    // If there lies a character which
    // is in A and greater than A[0]
    for (var i = 1; i < M; i++)
    {
        if (A[i] > A[0])
          {
            swap(A, i, B, 0);
            swap(A, 0, B, 0);
            return 2;
          }
    }

    // If there lies a character which
    // is in B and less than B[0]
    for (var i = 1; i < N; i++)
    {
        if (B[i] < B[0])
          {
            swap(A, 0, B, i);
            swap(A, 0, B, 0);
            return 2;
          }
    }

    // Otherwise
    return 0;
}

function count(a, c)
{
    count = 0;
    for(var i = 0; i < a.length; i++)
          if(a[i] == c)
            count++; 
    return count;  
}

function swap(s1, index1, s2, index2)
{
      var c = s1[index1];
    s1[index1] = s2[index2];
    s2[index2] = c;
}

var A = "adsfd";
var B = "dffff";
var M = A.length;
var N = B.length;

document.write(minSteps(A, B, M, N));

// This code is contributed by SoumikMondal
</script>
```

****Output:** 

```
1
```** 

*****时间复杂度:*** O(N)
***辅助空间*** **:** O(1)**