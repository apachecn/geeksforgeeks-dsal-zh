# 使给定二进制字符串交替所需的最小子字符串反转次数

> 原文:[https://www . geesforgeks . org/minimum-substring-reverses-required-make-给定-binary-string-alternative/](https://www.geeksforgeeks.org/minimum-substring-reversals-required-to-make-given-binary-string-alternating/)

给定一个长度为 **N** 的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **S** ，任务是计算 **S** 的最小子串数，该数需要被反转以使字符串 **S** 交替。如果无法使字符串交替，则打印**-1”**。

**示例:**

> **输入:** S = "10001110"
> **输出:** 2
> **说明:**
> 第一次操作，反转子串 **{S[3]，..，S[6]}** 将字符串修改为“10110010”。
> 第二次操作，反转子串 **{S[4]，..S[5]}** 将字符串修改为“10101010”，这是交替的。
> 
> **输入:** S = "100001"
> **输出:** -1
> **说明:**不可能得到交替的二进制字符串。

**方法:**这个想法是基于这样的观察:当一个子串**S【L，R】**被反转时，那么不超过两对**S【L–1】**、**S【L】**和**S【R】**、**S【R+1】**被改变。而且，一对应该是连续的一对 **00** ，另一对 **11** 。因此，通过将 00 与 11 或与 **S** 的左/右边框配对，可以获得最小的运算次数。因此，所需的操作数是同一字符的连续对数的一半。按照以下步骤解决问题:

*   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** 统计 **1s** 和 **0s** 的个数，分别存储在 **sum1** 和 **sum0** 中。
*   如果 **sum1** 和 **sum0 > 1** 的绝对差，则打印**-1”**。
*   否则，[查找字符串 **S**](https://www.geeksforgeeks.org/maximum-consecutive-repeating-character-string/) 中相同的连续字符数。让那个计数为 **1 的 **K** 和 **0** 的 L** 。
*   完成以上步骤后，打印 **K** 的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the minimum number
// of substrings required to be reversed
// to make the string S alternating
int minimumReverse(string s, int n)
{
    // Store count of consecutive pairs
    int k = 0 , l = 0 ;

    // Stores the count of 1s and 0s
    int sum1 = 0, sum0 = 0;

    // Traverse through the string
    for (int i = 1; i < n; i++) {

        if (s[i] == '1')

            // Increment 1s count
            sum1++;
        else

            // Increment 0s count
            sum0++;

        // Increment K if consecutive
        // same elements are found
        if (s[i] == s[i - 1]&& s[i] == '0')
            k++;
      else if( s[i] == s[i - 1]&& s[i] == '1')
        l++;
    }

    // Increment 1s count
    if(s[0]=='1')    
       sum1++;
    else  // Increment 0s count
       sum0++;

    // Check if it is possible or not
    if (abs(sum1 - sum0) > 1)
        return -1;

    // Otherwise, print the number
    // of required operations
    return max(k , l );
}

// Driver Code
int main()
{
    string S = "10001";
    int N = S.size();

    // Function Call
    cout << minimumReverse(S, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import java.lang.*;

class GFG
{

  // Function to count the minimum number
  // of substrings required to be reversed
  // to make the string S alternating
  static int minimumReverse(String s, int n)
  {

    // Store count of consecutive pairs
    int k = 0 , l = 0 ;

    // Stores the count of 1s and 0s
    int sum1 = 0, sum0 = 0;

    // Traverse through the string
    for (int i = 1; i < n; i++)
    {

      if (s.charAt(i) == '1')

        // Increment 1s count
        sum1++;
      else

        // Increment 0s count
        sum0++;

      // Increment K if consecutive
      // same elements are found
      if (s.charAt(i) == s.charAt(i - 1) && s.charAt(i) == '0')
        k++;
      else if( s.charAt(i) == s.charAt(i - 1) && s.charAt(i) == '1')
        l++;
    }

    // Increment 1s count
    if(s.charAt(0)=='1')    
      sum1++;
    else  // Increment 0s count
      sum0++;

    // Check if it is possible or not
    if (Math.abs(sum1 - sum0) > 1)
      return -1;

    // Otherwise, print the number
    // of required operations
    return Math.max(k , l);
  }

  // Driver code
  public static void main (String[] args)
  {
    String S = "10001";
    int N = S.length();

    // Function Call
    System.out.print(minimumReverse(S, N));

  }
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to count the minimum number
# of substrings required to be reversed
# to make the string S alternating
def minimumReverse(s, n):

    # Store count of consecutive pairs
    k = 0;
    l = 0;

    # Stores the count of 1s and 0s
    sum1 = 0;
    sum0 = 0;

    # Traverse through the string
    for i in range(1, n):
        if (s[i] == '1'):

            # Increment 1s count
            sum1 += 1;
        else:

            # Increment 0s count
            sum0 += 1;

        # Increment K if consecutive
        # same elements are found
        if (s[i] == s[i - 1] and s[i] == '0'):
            k += 1;
        elif (s[i] == s[i - 1] and s[i] == '1'):
            l += 1;

    # Increment 1s count
    if (s[0] == '1'):
        sum1 += 1;
    else:  # Increment 0s count
        sum0 += 1;

    # Check if it is possible or not
    if (abs(sum1 - sum0) > 1):
        return -1;

    # Otherwise, print the number
    # of required operations
    return max(k, l);

# Driver code
if __name__ == '__main__':
    S = "10001";
    N = len(S);

    # Function Call
    print(minimumReverse(S, N));

# This code is contributed by shikhasingrajput
```

## C#

```
// C# program for the above approach
using System;

public class GFG
{

  // Function to count the minimum number
  // of substrings required to be reversed
  // to make the string S alternating
  static int minimumReverse(String s, int n)
  {

    // Store count of consecutive pairs
    int k = 0 , l = 0 ;

    // Stores the count of 1s and 0s
    int sum1 = 0, sum0 = 0;

    // Traverse through the string
    for (int i = 1; i < n; i++)
    {

      if (s[i] == '1')

        // Increment 1s count
        sum1++;
      else

        // Increment 0s count
        sum0++;

      // Increment K if consecutive
      // same elements are found
      if (s[i] == s[i-1] && s[i] == '0')
        k++;
      else if( s[i] == s[i-1] && s[i] == '1')
        l++;
    }

    // Increment 1s count
    if(s[0] == '1')    
      sum1++;
    else  // Increment 0s count
      sum0++;

    // Check if it is possible or not
    if (Math.Abs(sum1 - sum0) > 1)
      return -1;

    // Otherwise, print the number
    // of required operations
    return Math.Max(k , l);
  }

  // Driver code
  public static void Main(String[] args)
  {
    String S = "10001";
    int N = S.Length;

    // Function Call
    Console.Write(minimumReverse(S, N));
  }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

  // Function to count the minimum number
  // of substrings required to be reversed
  // to make the string S alternating
  function minimumReverse(s, n)
  {

    // Store count of consecutive pairs
    let k = 0 , l = 0 ;

    // Stores the count of 1s and 0s
    let sum1 = 0, sum0 = 0;

    // Traverse through the string
    for (let i = 1; i < n; i++)
    {

      if (s[i] == '1')

        // Increment 1s count
        sum1++;
      else

        // Increment 0s count
        sum0++;

      // Increment K if consecutive
      // same elements are found
      if (s[i] == s[i-1] && s[i] == '0')
        k++;
      else if( s[i] == s[i-1] && s[i] == '1')
        l++;
    }

    // Increment 1s count
    if(s[0] == '1')   
      sum1++;
    else  // Increment 0s count
      sum0++;

    // Check if it is possible or not
    if (Math.abs(sum1 - sum0) > 1)
      return -1;

    // Otherwise, print the number
    // of required operations
    return Math.max(k , l);
  }

// Driver code

    let S = "10001";
    let N = S.length;

    // Function Call
    document.write(minimumReverse(S, N));

</script>
```

**Output:** 

```
2
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)