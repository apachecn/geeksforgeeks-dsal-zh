# 将字符串分成三个回文子串，并尽可能早地剪切

> 原文:[https://www . geeksforgeeks . org/split-string-in-three-回文-substrings-with-尽早-cuts/](https://www.geeksforgeeks.org/split-string-into-three-palindromic-substrings-with-earliest-possible-cuts/)

给定[字符串](https://www.geeksforgeeks.org/string-data-structure/) **字符串**，任务是检查给定字符串 **S** 是否可以拆分成三个[回文子字符串](https://www.geeksforgeeks.org/find-number-distinct-palindromic-sub-strings-given-string/)。如果可能有多个答案，那么打印切割指数最小的那一个。如果不存在这样的可能分区，则打印**-1”**。

**示例:**

> **输入:** str = "aabbcdc"
> **输出:** aa bb cdc
> **解释:**
> 只存在一个可能的分区{“aa”、“bb”、“CDC”}。
> 
> **输入:** str = "ababbcb"
> **输出:** a bab bcb
> **解释:**可能的拆分有{“ABA”、“b”、“BCB”}和{“a”、“bab”、“BCB”}。
> 由于{“a”、“bab”、“BCB”}在较早的指数上有分裂，这是必需的答案。

**方法:**按照以下步骤解决问题:

1.  [生成字符串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)的所有可能的子串，并检查给定的子串是否是[回文](https://www.geeksforgeeks.org/c-program-check-given-string-palindrome/)。
2.  如果存在任何子串，则将子串的最后一个索引存储在向量 **startPal** 中，其中 **startPal** 将存储从 0 个索引开始到存储值结束的第一个回文。
3.  与第一步类似，从给定字符串的最后一个索引 **str** 生成所有的子字符串，并检查给定的子字符串是否是回文。如果任何子串作为子串出现，那么将子串的最后一个索引存储在向量 **lastPal** 中，其中 **lastPal** 将存储第三个回文，从存储的值开始，到给定串**串**的**(N–1)<sup>第</sup>** 个索引结束。
4.  [反转矢量](https://www.geeksforgeeks.org/how-to-reverse-a-vector-using-stl-in-c/) **lastPal** 获得最早的切割。
5.  现在，迭代两个嵌套循环，外部循环从 **startPal** 中挑选第一个回文结束索引，内部循环从 **lastPal** 中挑选第三个回文开始索引。如果 **startPal** 的值小于 **lastPal** 的值，则以成对的形式将其存储在 **middlePal** 向量中。
6.  现在[遍历向量](https://www.geeksforgeeks.org/how-to-iterate-through-a-vector-without-using-iterators-in-c/) **middlePal** 检查第一个回文的结束索引和第三个回文的开始索引之间的子串是否是回文。如果发现是真的，那么第一个回文= **s.substr(0，middlePal[i]。第一个)**，第三个回文= **s.substr(middlePal[i]。第二，N–米德尔帕尔[i]。第二)**而休息弦将是第三弦。
7.  如果所有三个回文字符串都存在，则打印该字符串，否则打印**-1”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if a string
// is palindrome or not
bool isPalindrome(string x)
{
    // Copy the string x to y
    string y = x;

    // Reverse the string y
    reverse(y.begin(), y.end());

    if (x == y) {

        // If string x equals y
        return true;
    }

    return false;
}

// Function to find three palindromes
// from the given string with earliest
// possible cuts
void Palindromes(string S, int N)
{
    // Stores index of palindrome
    // starting from left & right
    vector<int> startPal, lastPal;

    string start;

    // Store the indices for possible
    // palindromes from left
    for (int i = 0;
         i < S.length() - 2; i++) {

        // Push the current character
        start.push_back(S[i]);

        // Check for palindrome
        if (isPalindrome(start)) {

            // Insert the current index
            startPal.push_back(i);
        }
    }

    string last;

    // Stores the indexes for possible
    // palindromes from right
    for (int j = S.length() - 1;
         j >= 2; j--) {

        // Push the current character
        last.push_back(S[j]);

        // Check palindromic
        if (isPalindrome(last)) {

            // Insert the current index
            lastPal.push_back(j);
        }
    }

    // Sort the indexes for palindromes
    // from right in ascending order
    reverse(lastPal.begin(),
            lastPal.end());

    vector<pair<int, int> > middlePal;

    for (int i = 0;
         i < startPal.size(); i++) {

        for (int j = 0;
             j < lastPal.size(); j++) {

            // If the value of startPal
            // < lastPal value then
            // store it in middlePal
            if (startPal[i] < lastPal[j]) {

                // Insert the current pair
                middlePal.push_back(
                    { startPal[i],
                      lastPal[j] });
            }
        }
    }

    string res1, res2, res3;
    int flag = 0;

    // Traverse over the middlePal
    for (int i = 0;
         i < middlePal.size(); i++) {

        int x = middlePal[i].first;
        int y = middlePal[i].second;

        string middle;

        for (int k = x + 1; k < y; k++) {
            middle.push_back(S[k]);
        }

        // Check if the middle part
        // is palindrome
        if (isPalindrome(middle)) {
            flag = 1;
            res1 = S.substr(0, x + 1);
            res2 = middle;
            res3 = S.substr(y, N - y);
            break;
        }
    }

    // Print the three palindromic
    if (flag == 1) {
        cout << res1 << " "
             << res2 << " "
             << res3;
    }

    // Otherwise
    else
        cout << "-1";
}

// Driver Code
int main()
{
    // Given string str
    string str = "ababbcb";

    int N = str.length();

    // Function Call
    Palindromes(str, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;
class GFG{

static class pair
{
  int first, second;
  public pair(int first,
              int second)
  {
    this.first = first;
    this.second = second;
  }
}

static String reverse(String input)
{
  char[] a = input.toCharArray();
  int l, r = a.length - 1;

  for (l = 0; l < r; l++, r--)
  {
    char temp = a[l];
    a[l] = a[r];
    a[r] = temp;
  }
  return String.valueOf(a);
}

// Function to check if a String
// is palindrome or not
static boolean isPalindrome(String x)
{
  // Copy the String x to y
  String y = x;

  // Reverse the String y
  y = reverse(y);

  if (x.equals(y))
  {
    // If String x equals y
    return true;
  }

  return false;
}

// Function to find three palindromes
// from the given String with earliest
// possible cuts
static void Palindromes(String S,
                        int N)
{
  // Stores index of palindrome
  // starting from left & right
  Vector<Integer> startPal =
         new Vector<>();
  Vector<Integer> lastPal =
         new Vector<>();

  String start = "";

  // Store the indices for possible
  // palindromes from left
  for (int i = 0;
           i < S.length() - 2; i++)
  {
    // Push the current character
    start += S.charAt(i);

    // Check for palindrome
    if (isPalindrome(start))
    {
      // Insert the current index
      startPal.add(i);
    }
  }

  String last = "";

  // Stores the indexes for possible
  // palindromes from right
  for (int j = S.length() - 1;
           j >= 2; j--)
  {
    // Push the current character
    last += S.charAt(j);

    // Check palindromic
    if (isPalindrome(last))
    {
      // Insert the current index
      lastPal.add(j);
    }
  }

  // Sort the indexes for palindromes
  // from right in ascending order
  Collections.reverse(lastPal);

  Vector<pair> middlePal =
               new Vector<>();

  for (int i = 0;
           i < startPal.size(); i++)
  {
    for (int j = 0;
             j < lastPal.size(); j++)
    {
      // If the value of startPal
      // < lastPal value then
      // store it in middlePal
      if (startPal.get(i) <
          lastPal.get(j))
      {
        // Insert the current pair
        middlePal.add(new pair(startPal.get(i),
                               lastPal.get(j)));
      }
    }
  }

  String res1 = "",
         res2 = "", res3 = "";
  int flag = 0;

  // Traverse over the middlePal
  for (int i = 0;
           i < middlePal.size(); i++)
  {
    int x = middlePal.get(i).first;
    int y = middlePal.get(i).second;
    String middle = "";

    for (int k = x + 1; k < y; k++)
    {
      middle += S.charAt(k);
    }

    // Check if the middle part
    // is palindrome
    if (isPalindrome(middle))
    {
      flag = 1;
      res1 = S.substring(0, x + 1);
      res2 = middle;
      res3 = S.substring(y, N);
      break;
    }
  }

  // Print the three palindromic
  if (flag == 1)
  {
    System.out.print(res1 + " " +
                     res2 + " " + res3);
  }

  // Otherwise
  else
    System.out.print("-1");
}

// Driver Code
public static void main(String[] args)
{
  // Given String str
  String str = "ababbcb";

  int N = str.length();

  // Function Call
  Palindromes(str, N);
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if a string
# is palindrome or not
def isPalindrome(x):

    # Copy the x to y
    y = x

    # Reverse the y
    y = y[::-1]

    if (x == y):

        # If x equals y
        return True

    return False

# Function to find three palindromes
# from the given with earliest
# possible cuts
def Palindromes(S, N):

    # Stores index of palindrome
    # starting from left & right
    startPal, lastPal = [], []

    start = []

    # Store the indices for possible
    # palindromes from left
    for i in range(len(S) - 2):

        # Push the current character
        start.append(S[i])

        # Check for palindrome
        if (isPalindrome(start)):

            # Insert the current index
            startPal.append(i)

    last = []

    # Stores the indexes for possible
    # palindromes from right
    for j in range(len(S) - 1, 1, -1):

        # Push the current character
        last.append(S[j])

        # Check palindromic
        if (isPalindrome(last)):

            # Insert the current index
            lastPal.append(j)

    # Sort the indexes for palindromes
    # from right in ascending order
    lastPal = lastPal[::-1]

    middlePal = []

    for i in range(len(startPal)):
        for j in range(len(lastPal)):

            # If the value of startPal
            # < lastPal value then
            # store it in middlePal
            if (startPal[i] < lastPal[j]):

                # Insert the current pair
                middlePal.append([startPal[i],
                                   lastPal[j]])

    res1, res2, res3 = "", "", ""
    flag = 0

    # Traverse over the middlePal
    for i in range(len(middlePal)):
        x = middlePal[i][0]
        y = middlePal[i][1]
        #print(x,y)

        middle = ""

        for k in range(x + 1, y):
            middle += (S[k])

        # Check if the middle part
        # is palindrome
        if (isPalindrome(middle)):
            flag = 1
            res1 = S[0 : x + 1]
            res2 = middle
            res3 = S[y : N]
            #print(S,x,y,N)
            break

    # Print the three palindromic
    if (flag == 1):
        print(res1, res2, res3)

    # Otherwise
    else:
        print("-1")

# Driver Code
if __name__ == '__main__':

    # Given strr
    strr = "ababbcb"

    N = len(strr)

    # Function call
    Palindromes(strr, N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the
// above approach
using System;
using System.Collections.Generic;

class GFG{

public class pair
{
  public int first, second;
  public pair(int first,
              int second)
  {
    this.first = first;
    this.second = second;
  }
}

static String reverse(String input)
{
  char[] a = input.ToCharArray();
  int l, r = a.Length - 1;

  for(l = 0; l < r; l++, r--)
  {
    char temp = a[l];
    a[l] = a[r];
    a[r] = temp;
  }
  return String.Join("",a);
}

// Function to check if a String
// is palindrome or not
static bool isPalindrome(String x)
{

  // Copy the String x to y
  String y = x;

  // Reverse the String y
  y = reverse(y);

  if (x.Equals(y))
  {

    // If String x equals y
    return true;
  }
  return false;
}

// Function to find three palindromes
// from the given String with earliest
// possible cuts
static void Palindromes(String S,
                        int N)
{

  // Stores index of palindrome
  // starting from left & right
  List<int> startPal = new List<int>();
  List<int> lastPal = new List<int>();

  String start = "";

  // Store the indices for possible
  // palindromes from left
  for(int i = 0;
          i < S.Length - 2; i++)
  {

    // Push the current character
    start += S[i];

    // Check for palindrome
    if (isPalindrome(start))
    {

      // Insert the current index
      startPal.Add(i);
    }
  }

  String last = "";

  // Stores the indexes for possible
  // palindromes from right
  for(int j = S.Length - 1;
          j >= 2; j--)
  {

    // Push the current character
    last += S[j];

    // Check palindromic
    if (isPalindrome(last))
    {

      // Insert the current index
      lastPal.Add(j);
    }
  }

  // Sort the indexes for palindromes
  // from right in ascending order
  lastPal.Reverse();

  List<pair> middlePal = new List<pair>();

  for(int i = 0;
          i < startPal.Count; i++)
  {
    for(int j = 0;
            j < lastPal.Count; j++)
    {

      // If the value of startPal
      // < lastPal value then
      // store it in middlePal
      if (startPal[i] < lastPal[j])
      {

        // Insert the current pair
        middlePal.Add(new pair(startPal[i],
                                lastPal[j]));
      }
    }
  }

  String res1 = "", res2 = "",
         res3 = "";
  int flag = 0;

  // Traverse over the middlePal
  for(int i = 0;
          i < middlePal.Count; i++)
  {
    int x = middlePal[i].first;
    int y = middlePal[i].second;
    String middle = "";

    for(int k = x + 1; k < y; k++)
    {
      middle += S[k];
    }

    // Check if the middle part
    // is palindrome
    if (isPalindrome(middle))
    {
      flag = 1;
      res1 = S.Substring(0, x + 1);
      res2 = middle;
      res3 = S.Substring(y);
      break;
    }
  }

  // Print the three palindromic
  if (flag == 1)
  {
    Console.Write(res1 + " " +
                  res2 + " " + res3);
  }

  // Otherwise
  else
    Console.Write("-1");
}

// Driver Code
public static void Main(String[] args)
{

  // Given String str
  String str = "ababbcb";

  int N = str.Length;

  // Function Call
  Palindromes(str, N);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
      // Function to check if a String
      // is palindrome or not
      function isPalindrome(x) {
        // Copy the String x to y
        var y = x;

        // Reverse the String y
        y = y.split("").reverse().join("");

        if (x === y) {
          // If String x equals y
          return true;
        }
        return false;
      }

      // Function to find three palindromes
      // from the given String with earliest
      // possible cuts
      function Palindromes(S, N) {
        // Stores index of palindrome
        // starting from left & right
        var startPal = [];
        var lastPal = [];

        var start = "";

        // Store the indices for possible
        // palindromes from left
        for (var i = 0; i < S.length - 2; i++) {
          // Push the current character
          start += S[i];

          // Check for palindrome
          if (isPalindrome(start)) {
            // Insert the current index
            startPal.push(i);
          }
        }

        var last = "";

        // Stores the indexes for possible
        // palindromes from right
        for (var j = S.length - 1; j >= 2; j--) {
          // Push the current character
          last += S[j];

          // Check palindromic
          if (isPalindrome(last)) {
            // Insert the current index
            lastPal.push(j);
          }
        }

        // Sort the indexes for palindromes
        // from right in ascending order
        lastPal.sort();

        var middlePal = [];

        for (var i = 0; i < startPal.length; i++) {
          for (var j = 0; j < lastPal.length; j++) {
            // If the value of startPal
            // < lastPal value then
            // store it in middlePal
            if (startPal[i] < lastPal[j]) {
              // Insert the current pair
              middlePal.push([startPal[i], lastPal[j]]);
            }
          }
        }

        var res1 = "",
          res2 = "",
          res3 = "";
        var flag = 0;

        // Traverse over the middlePal
        for (var i = 0; i < middlePal.length; i++) {
          var x = middlePal[i][0];
          var y = middlePal[i][1];
          var middle = "";

          for (var k = x + 1; k < y; k++) {
            middle += S[k];
          }

          // Check if the middle part
          // is palindrome
          if (isPalindrome(middle)) {
            flag = 1;
            res1 = S.substring(0, x + 1);
            res2 = middle;
            res3 = S.substring(y, N);
            break;
          }
        }

        // Print the three palindromic
        if (flag === 1) {
          document.write(res1 + " " + res2 + " " + res3);
        }

        // Otherwise
        else document.write("-1");
      }

      // Driver Code
      // Given String str
      var str = "ababbcb";

      var N = str.length;

      // Function Call
      Palindromes(str, N);
</script>
```

**Output:** 

```
a bab bcb
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*