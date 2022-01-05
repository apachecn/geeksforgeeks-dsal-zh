# 替换二进制字符串中所有出现的 X 后，字符串中最频繁出现的字符

> 原文:[https://www . geeksforgeeks . org/替换二进制字符串中所有出现的 x 后最频繁出现的字符串字符/](https://www.geeksforgeeks.org/most-frequent-character-in-a-string-after-replacing-all-occurrences-of-x-in-a-binary-string/)

给定一个由 **1** 、 **0** 和 **X** 组成的长度为 **N** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/)，任务是在每次出现 **X** 后，以最大频率打印[字符(*“1”或“0”*):](https://www.geeksforgeeks.org/return-maximum-occurring-character-in-the-input-string/)

*   如果 **X** 左边相邻的字符是 **1** ，将 **X** 替换为 **1** 。
*   如果出现在 **X** 右边的字符是 **0** ，将 **X** 替换为 **0** 。
*   如果上述两个条件都满足，则 **X** 保持不变。

***注:**如果更换后 **1** 和 **0** 的频率相同，则打印 **X** 。*

**示例:**

> **输入:**S =【xx1001100 x1031 xx】
> T3】输出: 1
> **解释:**
> 操作 1:S =【x11001100 x1xx】
> 操作 2:S =【111001100 x1xx】
> 无法再进行替换。
> 因此，“1”和“0”的频率分别为 6 和 4。
> 
> **输入:**S =“0xxx 1”
> T3】输出: X
> **说明:**
> 操作 1:S =“00X11”
> 无法再进行替换。
> 因此，“1”和“0”的频率都是 2。

**方法:**给定的问题可以基于以下观察来解决:

*   位于**【1】**和**【0】**(*如**1XX 0***)之间的所有**【X】**都没有意义，因为**【1】**和**【0】**都不能转换。
*   位于**【0】**和**【1】**(*如 **0XXX1*** )之间的所有**【X】**也没有意义，因为它对 **1** 和 **0** 的贡献相等。考虑**“0X…X1”**形式的任意子串，然后从字符串的**开始**到**结束**改变[第一次出现 **X**](https://www.geeksforgeeks.org/find-first-and-last-positions-of-an-element-in-a-sorted-array/) 后，子串中 **0** 和 **1** 的实际出现频率保持不变。

从以上观察可以得出结论，结果取决于以下条件:

*   原弦中**‘1’****‘0’**的计数。
*   在两个连续的 **0** s 或两个连续的 **1** s 之间出现的 **X** 的频率，即分别为**“0xx0”**和**“1xx31”**。
*   出现在字符串开始处的连续的**‘X’**的数量，其右端为**‘1’**，即**“XXXX1…”**。
*   出现在字符串末尾并具有左端**“0”**即**的连续**“X”**的数量…..0xx**。

因此，根据上述条件计算 **1** s 和 **0** s 的数量，并打印结果计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the most frequent
// character after replacing X with
// either '0' or '1' according as per
// the given conditions
void maxOccuringCharacter(string s)
{

    // Store the count of 0s and
    // 1s in the string S
    int count0 = 0, count1 = 0;

    // Count the frequency of
    // 0 and 1
    for (int i = 0; i < s.length(); i++) {

        // If the character is 1
        if (s[i] == '1') {
            count1++;
        }

        // If the character is 0
        else if (s[i] == '0') {
            count0++;
        }
    }

    // Stores first occurence of 1
    int prev = -1;
    for (int i = 0; i < s.length(); i++) {

        if (s[i] == '1') {
            prev = i;
            break;
        }
    }

    // Traverse the string to count
    // the number of X between two
    // consecutive 1s
    for (int i = prev + 1; i < s.length(); i++) {

        // If the current character
        // is not X
        if (s[i] != 'X') {

            // If the current character
            // is 1, add the number of
            // Xs to count1 and set
            // prev to i
            if (s[i] == '1') {
                count1 += i - prev - 1;
                prev = i;
            }

            // Otherwise
            else {

                // Find next occurence
                // of 1 in the string
                bool flag = true;

                for (int j = i + 1; j < s.length(); j++) {
                    if (s[j] == '1') {
                        flag = false;
                        prev = j;
                        break;
                    }
                }

                // If it is found,
                // set i to prev
                if (!flag) {
                    i = prev;
                }

                // Otherwise, break
                // out of the loop
                else {
                    i = s.length();
                }
            }
        }
    }

    // Store the first occurence of 0
    prev = -1;
    for (int i = 0; i < s.length(); i++) {

        if (s[i] == '0') {
            prev = i;
            break;
        }
    }

    // Repeat the same procedure to
    // count the number of X between
    // two consecutive 0s
    for (int i = prev + 1; i < s.length(); i++) {

        // If the current character is not X
        if (s[i] != 'X') {

            // If the current character is 0
            if (s[i] == '0') {

                // Add the count of Xs to count0
                count0 += i - prev - 1;

                // Set prev to i
                prev = i;
            }

            // Otherwise
            else {

                // Find the next occurence
                // of 0 in the string
                bool flag = true;

                for (int j = i + 1; j < s.length(); j++) {

                    if (s[j] == '0') {
                        prev = j;
                        flag = false;
                        break;
                    }
                }

                // If it is found,
                // set i to prev
                if (!flag) {
                    i = prev;
                }

                // Otherwise, break out
                // of the loop
                else {
                    i = s.length();
                }
            }
        }
    }

    // Count number of X present in
    // the starting of the string
    // as XXXX1...
    if (s[0] == 'X') {

        // Store the count of X
        int count = 0;
        int i = 0;
        while (s[i] == 'X') {
            count++;
            i++;
        }

        // Increment count1 by
        // count if the condition
        // is satisfied
        if (s[i] == '1') {
            count1 += count;
        }
    }

    // Count the number of X
    // present in the ending of
    // the string as ...XXXX0
    if (s[(s.length() - 1)] == 'X') {

        // Store the count of X
        int count = 0;
        int i = s.length() - 1;
        while (s[i] == 'X') {
            count++;
            i--;
        }

        // Increment count0 by
        // count if the condition
        // is satisfied
        if (s[i] == '0') {
            count0 += count;
        }
    }

    // If count of 1 is equal to
    // count of 0, print X
    if (count0 == count1) {
        cout << "X" << endl;
    }

    // Otherwise, if count of 1
    // is greater than count of 0
    else if (count0 > count1) {
        cout << 0 << endl;
    }

    // Otherwise, print 0
    else
        cout << 1 << endl;
}

// Driver Code
int main()
{
    string S = "XX10XX10XXX1XX";
    maxOccuringCharacter(S);
}

// This code is contributed by SURENDAR_GANGWAR.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG {

    // Function to find the most frequent
    // character after replacing X with
    // either '0' or '1' according as per
    // the given conditions
    public static void
    maxOccuringCharacter(String s)
    {
        // Store the count of 0s and
        // 1s in the string S
        int count0 = 0, count1 = 0;

        // Count the frequency of
        // 0 and 1
        for (int i = 0;
             i < s.length(); i++) {

            // If the character is 1
            if (s.charAt(i) == '1') {
                count1++;
            }

            // If the character is 0
            else if (s.charAt(i) == '0') {
                count0++;
            }
        }

        // Stores first occurence of 1
        int prev = -1;

        for (int i = 0;
             i < s.length(); i++) {

            if (s.charAt(i) == '1') {
                prev = i;
                break;
            }
        }

        // Traverse the string to count
        // the number of X between two
        // consecutive 1s
        for (int i = prev + 1;
             i < s.length(); i++) {

            // If the current character
            // is not X
            if (s.charAt(i) != 'X') {

                // If the current character
                // is 1, add the number of
                // Xs to count1 and set
                // prev to i
                if (s.charAt(i) == '1') {
                    count1 += i - prev - 1;
                    prev = i;
                }

                // Otherwise
                else {

                    // Find next occurence
                    // of 1 in the string
                    boolean flag = true;

                    for (int j = i + 1;
                         j < s.length();
                         j++) {
                        if (s.charAt(j) == '1') {
                            flag = false;
                            prev = j;
                            break;
                        }
                    }

                    // If it is found,
                    // set i to prev
                    if (!flag) {
                        i = prev;
                    }

                    // Otherwise, break
                    // out of the loop
                    else {
                        i = s.length();
                    }
                }
            }
        }

        // Store the first occurence of 0
        prev = -1;
        for (int i = 0; i < s.length(); i++) {

            if (s.charAt(i) == '0') {
                prev = i;
                break;
            }
        }

        // Repeat the same procedure to
        // count the number of X between
        // two consecutive 0s
        for (int i = prev + 1;
             i < s.length(); i++) {

            // If the current character is not X
            if (s.charAt(i) != 'X') {

                // If the current character is 0
                if (s.charAt(i) == '0') {

                    // Add the count of Xs to count0
                    count0 += i - prev - 1;

                    // Set prev to i
                    prev = i;
                }

                // Otherwise
                else {

                    // Find the next occurence
                    // of 0 in the string
                    boolean flag = true;

                    for (int j = i + 1;
                         j < s.length(); j++) {

                        if (s.charAt(j) == '0') {
                            prev = j;
                            flag = false;
                            break;
                        }
                    }

                    // If it is found,
                    // set i to prev
                    if (!flag) {
                        i = prev;
                    }

                    // Otherwise, break out
                    // of the loop
                    else {
                        i = s.length();
                    }
                }
            }
        }

        // Count number of X present in
        // the starting of the string
        // as XXXX1...
        if (s.charAt(0) == 'X') {

            // Store the count of X
            int count = 0;
            int i = 0;
            while (s.charAt(i) == 'X') {
                count++;
                i++;
            }

            // Increment count1 by
            // count if the condition
            // is satisfied
            if (s.charAt(i) == '1') {
                count1 += count;
            }
        }

        // Count the number of X
        // present in the ending of
        // the string as ...XXXX0
        if (s.charAt(s.length() - 1)
            == 'X') {

            // Store the count of X
            int count = 0;
            int i = s.length() - 1;
            while (s.charAt(i) == 'X') {
                count++;
                i--;
            }

            // Increment count0 by
            // count if the condition
            // is satisfied
            if (s.charAt(i) == '0') {
                count0 += count;
            }
        }

        // If count of 1 is equal to
        // count of 0, print X
        if (count0 == count1) {
            System.out.println("X");
        }

        // Otherwise, if count of 1
        // is greater than count of 0
        else if (count0 > count1) {
            System.out.println(0);
        }

        // Otherwise, print 0
        else
            System.out.println(1);
    }

    // Driver Code
    public static void main(String[] args)
    {
        String S = "XX10XX10XXX1XX";
        maxOccuringCharacter(S);
    }
}
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the most frequent
# character after replacing X with
# either '0' or '1' according as per
# the given conditions
def maxOccuringCharacter(s):

  # Store the count of 0s and
  # 1s in the S
  count0 = 0
  count1 = 0

  # Count the frequency of
  # 0 and 1
  for i in range(len(s)):

    # If the character is 1
    if (s[i] == '1') :
      count1 += 1

    # If the character is 0
    elif (s[i] == '0') :
      count0 += 1

  # Stores first occurence of 1
  prev = -1
  for i in range(len(s)):
    if (s[i] == '1') :
      prev = i
      break

  # Traverse the to count
  # the number of X between two
  # consecutive 1s
  for i in range(prev + 1, len(s)):

    # If the current character
    # is not X
    if (s[i] != 'X') :

      # If the current character
      # is 1, add the number of
      # Xs to count1 and set
      # prev to i
      if (s[i] == '1') :
        count1 += i - prev - 1
        prev = i

      # Otherwise
      else :

        # Find next occurence
        # of 1 in the string
        flag = True
        for j in range(i+1, len(s)):
          if (s[j] == '1') :
            flag = False
            prev = j
            break

        # If it is found,
        # set i to prev
        if (flag == False) :
          i = prev

        # Otherwise, break
        # out of the loop
        else :
          i = len(s)

  # Store the first occurence of 0
  prev = -1
  for i in range(0, len(s)):

    if (s[i] == '0') :
      prev = i
      break

  # Repeat the same procedure to
  # count the number of X between
  # two consecutive 0s
  for i in range(prev + 1, len(s)):

    # If the current character is not X
    if (s[i] != 'X') :

      # If the current character is 0
      if (s[i] == '0') :

        # Add the count of Xs to count0
        count0 += i - prev - 1

        # Set prev to i
        prev = i

      # Otherwise
      else :

        # Find the next occurence
        # of 0 in the string
        flag = True

        for j in range(i + 1, len(s)):
          if (s[j] == '0') :
            prev = j
            flag = False
            break

        # If it is found,
        # set i to prev
        if (flag == False) :
          i = prev

        # Otherwise, break out
        # of the loop
        else :
          i = len(s)

  # Count number of X present in
  # the starting of the string
  # as XXXX1...
  if (s[0] == 'X') :

    # Store the count of X
    count = 0
    i = 0
    while (s[i] == 'X') :
      count += 1
      i += 1

    # Increment count1 by
    # count if the condition
    # is satisfied
    if (s[i] == '1') :
      count1 += count

  # Count the number of X
  # present in the ending of
  # the as ...XXXX0
  if (s[(len(s) - 1)]
      == 'X') :

    # Store the count of X
    count = 0
    i = len(s) - 1
    while (s[i] == 'X') :
      count += 1
      i -= 1

    # Increment count0 by
    # count if the condition
    # is satisfied
    if (s[i] == '0') :
      count0 += count

  # If count of 1 is equal to
  # count of 0, prX
  if (count0 == count1) :
    print("X")

  # Otherwise, if count of 1
  # is greater than count of 0
  elif (count0 > count1) :
    print( 0 )

  # Otherwise, pr0
  else:
    print(1)

# Driver Code

S = "XX10XX10XXX1XX"
maxOccuringCharacter(S)

# This code is contributed by sanjoy_62.
```

## C#

```
// C# program for the above approach
using System;
public class GFG
{

  // Function to find the most frequent
  // character after replacing X with
  // either '0' or '1' according as per
  // the given conditions
  public static void maxOccuringCharacter(string s)
  {

    // Store the count of 0s and
    // 1s in the string S
    int count0 = 0, count1 = 0;

    // Count the frequency of
    // 0 and 1
    for (int i = 0;
         i < s.Length; i++) {

      // If the character is 1
      if (s[i] == '1') {
        count1++;
      }

      // If the character is 0
      else if (s[i] == '0') {
        count0++;
      }
    }

    // Stores first occurence of 1
    int prev = -1;

    for (int i = 0;
         i < s.Length; i++) {

      if (s[i] == '1') {
        prev = i;
        break;
      }
    }

    // Traverse the string to count
    // the number of X between two
    // consecutive 1s
    for (int i = prev + 1;
         i < s.Length; i++) {

      // If the current character
      // is not X
      if (s[i] != 'X') {

        // If the current character
        // is 1, add the number of
        // Xs to count1 and set
        // prev to i
        if (s[i] == '1') {
          count1 += i - prev - 1;
          prev = i;
        }

        // Otherwise
        else {

          // Find next occurence
          // of 1 in the string
          bool flag = true;

          for (int j = i + 1;
               j < s.Length;
               j++) {
            if (s[j] == '1') {
              flag = false;
              prev = j;
              break;
            }
          }

          // If it is found,
          // set i to prev
          if (!flag) {
            i = prev;
          }

          // Otherwise, break
          // out of the loop
          else {
            i = s.Length;
          }
        }
      }
    }

    // Store the first occurence of 0
    prev = -1;
    for (int i = 0; i < s.Length; i++) {

      if (s[i] == '0') {
        prev = i;
        break;
      }
    }

    // Repeat the same procedure to
    // count the number of X between
    // two consecutive 0s
    for (int i = prev + 1;
         i < s.Length; i++) {

      // If the current character is not X
      if (s[i] != 'X') {

        // If the current character is 0
        if (s[i] == '0') {

          // Add the count of Xs to count0
          count0 += i - prev - 1;

          // Set prev to i
          prev = i;
        }

        // Otherwise
        else {

          // Find the next occurence
          // of 0 in the string
          bool flag = true;

          for (int j = i + 1;
               j < s.Length; j++) {

            if (s[j] == '0') {
              prev = j;
              flag = false;
              break;
            }
          }

          // If it is found,
          // set i to prev
          if (!flag) {
            i = prev;
          }

          // Otherwise, break out
          // of the loop
          else {
            i = s.Length;
          }
        }
      }
    }

    // Count number of X present in
    // the starting of the string
    // as XXXX1...
    if (s[0] == 'X') {

      // Store the count of X
      int count = 0;
      int i = 0;
      while (s[i] == 'X') {
        count++;
        i++;
      }

      // Increment count1 by
      // count if the condition
      // is satisfied
      if (s[i] == '1') {
        count1 += count;
      }
    }

    // Count the number of X
    // present in the ending of
    // the string as ...XXXX0
    if (s[s.Length - 1]
        == 'X') {

      // Store the count of X
      int count = 0;
      int i = s.Length - 1;
      while (s[i] == 'X') {
        count++;
        i--;
      }

      // Increment count0 by
      // count if the condition
      // is satisfied
      if (s[i] == '0') {
        count0 += count;
      }
    }

    // If count of 1 is equal to
    // count of 0, print X
    if (count0 == count1) {
      Console.WriteLine("X");
    }

    // Otherwise, if count of 1
    // is greater than count of 0
    else if (count0 > count1) {
      Console.WriteLine(0);
    }

    // Otherwise, print 0
    else
      Console.WriteLine(1);
  }

  // Driver Code
  public static void Main(string[] args)
  {
    string S = "XX10XX10XXX1XX";
    maxOccuringCharacter(S);
  }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>

// javascript program for the above approach

   // Function to find the most frequent
    // character after replacing X with
    // either '0' or '1' according as per
    // the given conditions

function maxOccuringCharacter(s)
{
    // Store the count of 0s and
    // 1s in the string S
    var count0 = 0, count1 = 0;

    // Count the frequency of
    // 0 and 1
    for (var i = 0;
         i < s.length; i++) {

        // If the character is 1
        if (s.charAt(i) == '1') {
            count1++;
        }

        // If the character is 0
        else if (s.charAt(i) == '0') {
            count0++;
        }
    }

    // Stores first occurence of 1
    var prev = -1;

    for (var i = 0;
         i < s.length; i++) {

        if (s.charAt(i) == '1') {
            prev = i;
            break;
        }
    }

    // Traverse the string to count
    // the number of X between two
    // consecutive 1s
    for (var i = prev + 1;
         i < s.length; i++) {

        // If the current character
        // is not X
        if (s.charAt(i) != 'X') {

            // If the current character
            // is 1, add the number of
            // Xs to count1 and set
            // prev to i
            if (s.charAt(i) == '1') {
                count1 += i - prev - 1;
                prev = i;
            }

            // Otherwise
            else {

                // Find next occurence
                // of 1 in the string
                flag = true;

                for (var j = i + 1;
                     j < s.length;
                     j++) {
                    if (s.charAt(j) == '1') {
                        flag = false;
                        prev = j;
                        break;
                    }
                }

                // If it is found,
                // set i to prev
                if (!flag) {
                    i = prev;
                }

                // Otherwise, break
                // out of the loop
                else {
                    i = s.length;
                }
            }
        }
    }

    // Store the first occurence of 0
    prev = -1;
    for (var i = 0; i < s.length; i++) {

        if (s.charAt(i) == '0') {
            prev = i;
            break;
        }
    }

    // Repeat the same procedure to
    // count the number of X between
    // two consecutive 0s
    for (var i = prev + 1;
         i < s.length; i++) {

        // If the current character is not X
        if (s.charAt(i) != 'X') {

            // If the current character is 0
            if (s.charAt(i) == '0') {

                // Add the count of Xs to count0
                count0 += i - prev - 1;

                // Set prev to i
                prev = i;
            }

            // Otherwise
            else {

                // Find the next occurence
                // of 0 in the string
                flag = true;

                for (var j = i + 1;
                     j < s.length; j++) {

                    if (s.charAt(j) == '0') {
                        prev = j;
                        flag = false;
                        break;
                    }
                }

                // If it is found,
                // set i to prev
                if (!flag) {
                    i = prev;
                }

                // Otherwise, break out
                // of the loop
                else {
                    i = s.length;
                }
            }
        }
    }

    // Count number of X present in
    // the starting of the string
    // as XXXX1...
    if (s.charAt(0) == 'X') {

        // Store the count of X
        var count = 0;
        var i = 0;
        while (s.charAt(i) == 'X') {
            count++;
            i++;
        }

        // Increment count1 by
        // count if the condition
        // is satisfied
        if (s.charAt(i) == '1') {
            count1 += count;
        }
    }

    // Count the number of X
    // present in the ending of
    // the string as ...XXXX0
    if (s.charAt(s.length - 1)
        == 'X') {

        // Store the count of X
        var count = 0;
        var i = s.length - 1;
        while (s.charAt(i) == 'X') {
            count++;
            i--;
        }

        // Increment count0 by
        // count if the condition
        // is satisfied
        if (s.charAt(i) == '0') {
            count0 += count;
        }
    }

    // If count of 1 is equal to
    // count of 0, print X
    if (count0 == count1) {
        document.write("X");
    }

    // Otherwise, if count of 1
    // is greater than count of 0
    else if (count0 > count1) {
        document.write(0);
    }

    // Otherwise, print 0
    else
        document.write(1);
}

// Driver Code
var S = "XX10XX10XXX1XX";
maxOccuringCharacter(S);
// This code is contributed by 29AjayKumar
</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)