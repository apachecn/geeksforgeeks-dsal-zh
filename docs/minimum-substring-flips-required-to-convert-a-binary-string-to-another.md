# 将一个二进制字符串转换为另一个二进制字符串所需的最小子字符串翻转次数

> 原文:[https://www . geesforgeks . org/minimum-substring-flips-required-convert-a-binary-string-to-other/](https://www.geeksforgeeks.org/minimum-substring-flips-required-to-convert-a-binary-string-to-another/)

给定两个大小分别为 **N** 和 **M** 的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/)**【S1】**和 **S2** ，任务是找到将字符串 **S1** 转换为 **S2** 所需的相等字符的[子字符串的最小反转次数。如果无法将字符串 **S1** 转换为 **S2** ，则打印**-1”**。](https://www.geeksforgeeks.org/program-print-substrings-given-string/)

**示例:**

> **输入:**S1 =“100001”，S2 =“110111”
> **输出:** 2
> **说明:**
> 初串 S1 =“100001”。
> **反转 1:** 反转子串 S1[1，1]，那么字符串 S1 就变成了“110001”。
> **反转 2:** 反转子串 S1[3，4]，那么字符串 S1 就变成了“110111”。
> 经过上述反转，弦 S1 和 S2 相等。
> 因此，反转的计数为 2。
> 
> **输入:** S1 = 101，S2 = 10
> T3】输出: -1

**方法:**按照以下步骤解决这个问题:

*   初始化一个变量，说**回答**，以存储所需反转的结果计数。
*   如果给定字符串**和 **S2** 的[长度不相同，则打印**-1”**。](https://www.geeksforgeeks.org/5-different-methods-find-length-string-c/)**
*   **[迭代范围**【0，N-1】**](https://www.geeksforgeeks.org/range-based-loop-c/)，并执行以下步骤:

    *   如果**S1【I】**和**S2【I】**不一样，那么迭代直到**S1【I】**和**S2【I】**一样。将答案增加 **1** ，因为当前子串需要翻转。
    *   否则，[继续](https://www.geeksforgeeks.org/continue-statement-cpp/)进行下一次迭代。** 
*   **完成上述步骤后，打印**答案**的值，作为所需子字符串的翻转结果。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the minimum number
// of reversals required to make the
// given binary strings s1 and s2 same
int canMakeSame(string s1, string s2)
{
    // Stores the minimum count of
    // reversal of substrings required
    int ans = 0;

    // If the length of the strings
    // are not the same then return -1
    if (s1.size() != s2.size()) {
        return -1;
    }

    int N = s1.length();

    // Iterate over each character
    for (int i = 0; i < N; i++) {

        // If s1[i] is not
        // equal to s2[i]
        if (s1[i] != s2[i]) {

            // Iterate until s1[i] != s2[i]
            while (i < s1.length()
                   && s1[i] != s2[i]) {
                i++;
            }

            // Increment answer by 1
            ans++;
        }
    }

    // Return the resultant count of
    // reversal of substring required
    return ans;
}

// Driver Code
int main()
{
    string S1 = "100001";
    string S2 = "110111";

    // Function Call
    cout << canMakeSame(S1, S2);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.io.*;
class GFG
{

  // Function to count the minimum number
  // of reversals required to make the
  // given binary strings s1 and s2 same
  static int canMakeSame(String s1, String s2)
  {

    // Stores the minimum count of
    // reversal of substrings required
    int ans = 0;

    // If the length of the strings
    // are not the same then return -1
    if (s1.length() != s2.length()) {
      return -1;
    }

    int N = s1.length();

    // Iterate over each character
    for (int i = 0; i < N; i++)
    {

      // If s1[i] is not
      // equal to s2[i]
      if (s1.charAt(i) != s2.charAt(i))
      {

        // Iterate until s1[i] != s2[i]
        while (i < s1.length()
               && s1.charAt(i) != s2.charAt(i))
        {
          i++;
        }

        // Increment answer by 1
        ans++;
      }
    }

    // Return the resultant count of
    // reversal of substring required
    return ans;
  }

  // Driver Code
  public static void main(String[] args)
  {
    String S1 = "100001";
    String S2 = "110111";

    // Function Call
    System.out.println(canMakeSame(S1, S2));
  }
}

// This code is contributed by Dharanendra L V
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Function to count the minimum number
# of reversals required to make the
# given binary strings s1 and s2 same
def canMakeSame(s1, s2) :

    # Stores the minimum count of
    # reversal of substrings required
    ans = -1

    # If the length of the strings
    # are not the same then return -1
    if (len(s1) != len(s2)) :
        return -1
    N = len(s1)

    # Iterate over each character
    for i in range(0, N):

        # If s1[i] is not
        # equal to s2[i]
        if (s1[i] != s2[i]) :

            # Iterate until s1[i] != s2[i]
            while (i < len(s1)
                and s1[i] != s2[i]) :
                i += 1

            # Increment answer by 1
            ans += 1

    # Return the resultant count of
    # reversal of subrequired
    return ans

# Driver Code

S1 = "100001"
S2 = "110111"

# Function Call
print(canMakeSame(S1, S2))

# This code is contributed by code_hunt.
```

## **C#**

```
// C# program for the above approach
using System;

class GFG{

  // Function to count the minimum number
  // of reversals required to make the
  // given binary strings s1 and s2 same
  static int canMakeSame(string s1, string s2)
  {

    // Stores the minimum count of
    // reversal of substrings required
    int ans = 0;

    // If the length of the strings
    // are not the same then return -1
    if (s1.Length != s2.Length) {
      return -1;
    }

    int N = s1.Length;

    // Iterate over each character
    for (int i = 0; i < N; i++)
    {

      // If s1[i] is not
      // equal to s2[i]
      if (s1[i] != s2[i])
      {

        // Iterate until s1[i] != s2[i]
        while (i < s1.Length
               && s1[i] != s2[i])
        {
          i++;
        }

        // Increment answer by 1
        ans++;
      }
    }

    // Return the resultant count of
    // reversal of substring required
    return ans;
  }

// Driver Code
public static void Main(string[] args)
{
    string S1 = "100001";
    string S2 = "110111";

    // Function Call
    Console.Write(canMakeSame(S1, S2));
}
}

// This code is contributed by susmitakundugoaldanga.
```

## **java 描述语言**

```
<script>

// JavaScript program for the above approach

// Function to count the minimum number
// of reversals required to make the
// given binary strings s1 and s2 same
function canMakeSame(s1, s2)
{
    // Stores the minimum count of
    // reversal of substrings required
    var ans = 0;

    // If the length of the strings
    // are not the same then return -1
    if (s1.length != s2.length) {
        return -1;
    }

    var N = s1.length;

    // Iterate over each character
    for (var i = 0; i < N; i++) {

        // If s1[i] is not
        // equal to s2[i]
        if (s1[i] != s2[i]) {

            // Iterate until s1[i] != s2[i]
            while (i < s1.length
                   && s1[i] != s2[i]) {
                i++;
            }

            // Increment answer by 1
            ans++;
        }
    }

    // Return the resultant count of
    // reversal of substring required
    return ans;
}

// Driver Code
var S1 = "100001";
var S2 = "110111";

// Function Call
document.write( canMakeSame(S1, S2));

</script>
```

****Output:** 

```
2
```** 

*****时间复杂度:**O(N)*
T5**辅助空间:** O(1)**