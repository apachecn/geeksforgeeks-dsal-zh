# 通过反转子串

对字符串进行字典排序

> 原文:[https://www . geeksforgeeks . org/sort-a-string-按字典顺序通过反转子串/](https://www.geeksforgeeks.org/sort-a-string-lexicographically-by-reversing-a-substring/)

给定一个由 **N** 个小写字符组成的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是找到给定字符串 **S** 的子字符串的起始索引和结束索引( *0 基索引*)，该子字符串需要被反转以对字符串 **S** 进行排序。如果无法通过[反转任意子串](https://www.geeksforgeeks.org/reverse-the-substrings-of-the-given-string-according-to-the-given-array-of-indices/)对给定字符串 **S** 进行排序，则打印**-1”**。

**示例:**

> **输入:** S = "abcyxuz"
> **输出:** 3 5
> **解释:**从索引[3，5]中反转子串将字符串修改为“abcyxyz”，并进行排序。
> 因此，打印 3 和 5。
> 
> **输入:**S =【GFG】
> T3】输出: 0 1

**天真方法:**解决给定问题的最简单方法是[生成给定字符串 **S** 的所有可能的子字符串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)，如果存在任何这样的子字符串，将其反转[使字符串排序](https://www.geeksforgeeks.org/sort-string-characters/)，然后打印该子字符串的索引。否则，打印**-1”**。

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法也可以基于以下观察进行优化:要通过仅反转一个子串来对字符串进行[排序，原始字符串必须采用以下格式之一:](https://www.geeksforgeeks.org/program-sort-string-descending-order/)

*   递减字符串
*   增加子串+减少子串
*   减少子串+增加子串
*   增加子串+减少子串+增加子串

按照以下步骤解决问题:

*   初始化两个变量，比如**开始**和**结束**为 **-1** ，分别存储待反转子串的开始和结束索引。
*   初始化一个变量，比如说**将**标记为 **1** ，存储是否可以[对字符串](https://www.geeksforgeeks.org/sort-a-string-in-java-2-different-ways/)进行排序。
*   [迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，N】**并执行以下操作:
    *   如果字符 **S[i]** 小于字符**S[I–1]**，则从索引**(I–1)**开始查找递减子串右边界的索引，并存储在 **end** 中。
    *   检查反转子串**S[I–1，end]** 是否使字符串排序。如果发现是**假**那就打印 **"-1"** 并返回。否则，将**标志**标记为**假**。
    *   完成上述步骤后，用子串的右边界更新 **i** 的值。
    *   如果字符 **S[i]** 小于字符**S[I–1]**，且**标志**为**假**，则打印**-1”**并返回。
*   如果**开始**等于 **-1，**则更新**开始**和**结束**的值为 **1** 。
*   完成上述步骤后，打印**开始**和**结束**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the substring
// in S required to be reversed
bool adjust(string& S, int& i,
            int& start, int& end)
{
    // Stores the size of the string
    int N = S.length();

    // Stores the starting point
    // of the substring
    start = i - 1;

    // Iterate over the string S
    // while i < N
    while (i < N && S[i] < S[i - 1]) {

        // Increment the value of i
        i++;
    }

    // Stores the ending index of
    // the substring
    end = i - 1;

    // If start <= 0 or i >= N
    if (start <= 0 && i >= N)
        return true;

    // If start >= 1 and i <= N
    if (start >= 1 && i <= N) {

        // Return the boolean value
        return (S[end] >= S[start - 1]
                && S[start] <= S[i]);
    }

    // If start >= 1
    if (start >= 1) {

        // Return the boolean value
        return S[end] >= S[start - 1];
    }

    // If i < N
    if (i < N) {

        // Return true if S[start]
        // is less than or equal to
        // S[i]
        return S[start] <= S[i];
    }

    // Otherwise
    return false;
}

// Function to check if it is possible
// to sort the string or not
void isPossible(string& S, int N)
{
    // Stores the starting and the
    // ending index of substring
    int start = -1, end = -1;

    // Stores whether it is possible
    // to sort the substring
    bool flag = true;

    // Traverse the range [1, N]
    for (int i = 1; i < N; i++) {

        // If S[i] is less than S[i-1]
        if (S[i] < S[i - 1]) {

            // If flag stores true
            if (flag) {

                // If adjust(S, i, start,
                // end) return false
                if (adjust(S, i, start, end)
                    == false) {

                    // Print -1
                    cout << -1 << endl;
                    return;
                }

                // Unset the flag
                flag = false;
            }

            // Otherwise
            else {

                // Print -1
                cout << -1 << endl;
                return;
            }
        }
    }

    // If start is equal to -1
    if (start == -1) {
        // Update start and end
        start = end = 1;
    }

    // Print the value of start
    // and end
    cout << start << " "
         << end << "\n";
}

// Driver Code
int main()
{
    string S = "abcyxuz";
    int N = S.length();
    isPossible(S, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import java.lang.*;

class GFG{

static int i, start, end;

// Function to find the substring
// in S required to be reversed
static boolean adjust(String S)
{

    // Stores the size of the string
    int N = S.length();

    // Stores the starting point
    // of the substring
    start = i - 1;

    // Iterate over the string S
    // while i < N
    while (i < N && S.charAt(i) < 
                    S.charAt(i - 1))
    {

        // Increment the value of i
        i++;
    }

    // Stores the ending index of
    // the substring
    end = i - 1;

    // If start <= 0 or i >= N
    if (start <= 0 && i >= N)
        return true;

    // If start >= 1 and i <= N
    if (start >= 1 && i <= N)
    {

        // Return the boolean value
        return (S.charAt(end) >= S.charAt(start - 1) &&
                S.charAt(start) <= S.charAt(i));
    }

    // If start >= 1
    if (start >= 1)
    {

        // Return the boolean value
        return S.charAt(end) >= S.charAt(start - 1);
    }

    // If i < N
    if (i < N)
    {

        // Return true if S[start]
        // is less than or equal to
        // S[i]
        return S.charAt(start) <= S.charAt(i);
    }

    // Otherwise
    return false;
}

// Function to check if it is possible
// to sort the string or not
static void isPossible(String S, int N)
{

    // Stores the starting and the
    // ending index of substring
    start = -1; end = -1;

    // Stores whether it is possible
    // to sort the substring
    boolean flag = true;

    // Traverse the range [1, N]
    for(i = 1; i < N; i++)
    {

        // If S[i] is less than S[i-1]
        if (S.charAt(i) < S.charAt(i - 1))
        {

            // If flag stores true
            if (flag)
            {

                // If adjust(S, i, start,
                // end) return false
                if (adjust(S) == false)
                {

                    // Print -1
                    System.out.println(-1);
                    return;
                }

                // Unset the flag
                flag = false;
            }

            // Otherwise
            else
            {

                // Print -1
                System.out.println(-1);
                return;
            }
        }
    }

    // If start is equal to -1
    if (start == -1)
    {

        // Update start and end
        start = end = 1;
    }

    // Print the value of start
   System.out.println(start + " " + end);
}

// Driver code
public static void main(String[] args)
{
    String S = "abcyxuz";
    int N = S.length();
    isPossible(S, N);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the substring
# in S required to be reversed
def adjust(S, i, start, end):

    # Stores the size of the string
    N = len(S)

    # Stores the starting point
    # of the substring
    start = i - 1

    # Iterate over the string S
    # while i < N
    while (i < N and S[i] < S[i - 1]):

        # Increment the value of i
        i += 1

    # Stores the ending index of
    # the substring
    end = i - 1

    # If start <= 0 or i >= N
    if (start <= 0 and i >= N):
        return True,start,i,end

    # If start >= 1 and i <= N
    if (start >= 1 and i <= N):

        # Return the boolean value
        return (S[end] >= S[start - 1] and S[start] <= S[i]),start,i,end

    # If start >= 1
    if (start >= 1):

        # Return the boolean value
        return (S[end] >= S[start - 1]),start,i,end

    # If i < N
    if (i < N):

        # Return true if S[start]
        # is less than or equal to
        # S[i]
        return (S[start] <= S[i]),start,i,end

    # Otherwise
    return False,start,i,end

# Function to check if it is possible
# to sort the string or not
def isPossible(S, N):

    # global start,end,i
    # Stores the starting and the
    # ending index of substring
    start, end = -1, -1

    # Stores whether it is possible
    # to sort the substring
    flag = True

    # Traverse the range [1, N]
    i = 1
    while i < N:

        # If S[i] is less than S[i-1]
        if (S[i] < S[i - 1]):

            # If flag stores true
            if (flag):

                # If adjust(S, i, start,
                # end) return false
                f, start, i, end = adjust(S, i, start, end)
                if (f== False):
                    # Pr-1
                    print(-1)
                    return

                # Unset the flag
                flag = False
            # Otherwise
            else:

                # Pr-1
                print(-1)
                return
        i += 1       

    # If start is equal to -1
    if (start == -1):
        # Update start and end
        start, end = 1, 1

    # Print the value of start
    # and end
    print(start, end)

# Driver Code
if __name__ == '__main__':
    S = "abcyxuz"
    N = len(S)
    isPossible(S, N)

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

static int i, start, end;

// Function to find the substring
// in S required to be reversed
static bool adjust(string S)
{

    // Stores the size of the string
    int N = S.Length;

    // Stores the starting point
    // of the substring
    start = i - 1;

    // Iterate over the string S
    // while i < N
    while (i < N && S[i] <  S[i - 1])
    {

        // Increment the value of i
        i++;
    }

    // Stores the ending index of
    // the substring
    end = i - 1;

    // If start <= 0 or i >= N
    if (start <= 0 && i >= N)
        return true;

    // If start >= 1 and i <= N
    if (start >= 1 && i <= N)
    {

        // Return the boolean value
        return (S[end] >= S[start - 1] &&
                S[start] <= S[i]);
    }

    // If start >= 1
    if (start >= 1)
    {

        // Return the boolean value
        return S[end] >= S[start - 1];
    }

    // If i < N
    if (i < N)
    {

        // Return true if S[start]
        // is less than or equal to
        // S[i]
        return S[start] <= S[i];
    }

    // Otherwise
    return false;
}

// Function to check if it is possible
// to sort the string or not
static void isPossible(string S, int N)
{

    // Stores the starting and the
    // ending index of substring
    start = -1; end = -1;

    // Stores whether it is possible
    // to sort the substring
    bool flag = true;

    // Traverse the range [1, N]
    for(i = 1; i < N; i++)
    {

        // If S[i] is less than S[i-1]
        if (S[i] < S[i - 1])
        {

            // If flag stores true
            if (flag)
            {

                // If adjust(S, i, start,
                // end) return false
                if (adjust(S) == false)
                {

                    // Print -1
                    Console.WriteLine(-1);
                    return;
                }

                // Unset the flag
                flag = false;
            }

            // Otherwise
            else
            {

                // Print -1
                 Console.WriteLine(-1);
                return;
            }
        }
    }

    // If start is equal to -1
    if (start == -1)
    {

        // Update start and end
        start = end = 1;
    }

    // Print the value of start
    Console.WriteLine(start + " " + end);
}

// Driver code
static void Main()
{
    string S = "abcyxuz";
    int N = S.Length;

    isPossible(S, N);
}
}

// This code is contributed by SoumikMondal
```

## java 描述语言

```
<script>

      // JavaScript program for the above approach
      var i, start, end;

      // Function to find the substring
      // in S required to be reversed
      function adjust(S) {
        // Stores the size of the string
        var N = S.length;

        // Stores the starting point
        // of the substring
        start = i - 1;

        // Iterate over the string S
        // while i < N
        while (i < N && S[i] < S[i - 1]) {
          // Increment the value of i
          i++;
        }

        // Stores the ending index of
        // the substring
        end = i - 1;

        // If start <= 0 or i >= N
        if (start <= 0 && i >= N) return true;

        // If start >= 1 and i <= N
        if (start >= 1 && i <= N) {
          // Return the boolean value
          return S[end] >= S[start - 1] && S[start] <= S[i];
        }

        // If start >= 1
        if (start >= 1) {
          // Return the boolean value
          return S[end] >= S[start - 1];
        }

        // If i < N
        if (i < N) {
          // Return true if S[start]
          // is less than or equal to
          // S[i]
          return S[start] <= S[i];
        }

        // Otherwise
        return false;
      }

      // Function to check if it is possible
      // to sort the string or not
      function isPossible(S, N) {
        // Stores the starting and the
        // ending index of substring
        start = -1;
        end = -1;

        // Stores whether it is possible
        // to sort the substring
        var flag = true;

        // Traverse the range [1, N]
        for (i = 1; i < N; i++) {
          // If S[i] is less than S[i-1]
          if (S[i] < S[i - 1]) {
            // If flag stores true
            if (flag) {
              // If adjust(S, i, start,
              // end) return false
              if (adjust(S) === false) {
                // Print -1
                document.write(-1);
                return;
              }

              // Unset the flag
              flag = false;
            }

            // Otherwise
            else {
              // Print -1
              document.write(-1);
              return;
            }
          }
        }

        // If start is equal to -1
        if (start === -1) {
          // Update start and end
          start = end = 1;
        }

        // Print the value of start
        document.write(start + " " + end + "<br>");
      }

      // Driver code
      var S = "abcyxuz";
      var N = S.length;

      isPossible(S, N);

</script>
```

**Output:** 

```
3 5
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)