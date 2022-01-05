# 打印给定数字序列的所有可能的解码

> 原文:[https://www . geesforgeks . org/print-all-可能性-给定数字序列的解码/](https://www.geeksforgeeks.org/print-all-possible-decodings-of-a-given-digit-sequence/)

给定数字字符串 **str** ，其中 1 代表 **'a'** ，2 代表 **'b'** ，…，26 代表 **'z'** ，任务是打印所有可能从 **str** 获得的字母字符串。

**示例:**

> **输入:** str = "1123"
> **输出:**
> aabc
> KBC
> ALC
> aaw
> kw
> **解释:**
> 给定字符串可拆分为:
> 1)“1123”=“1”+“1”+“2”+“3”= aabc
> 2)“1123”=“11”+“2”+“3”= KBC【T16
> 
> **输入:** str = "56"
> **输出:**
> ef
> **解释:**
> 给定字符串可拆分为:
> 1)“56”=“5”+“6”= ef

**接近**:可以观察到，除了 **0** 之外，每个字符都代表一个字母表。这个问题是[递归](https://www.geeksforgeeks.org/recursion/)，可以分解为子问题。当传递的字符串为空时，将出现终止条件。以下是解决问题的步骤:

1.  创建一个辅助函数 **getChar()** ，返回给定数字字符的对应字母表。
2.  创建一个递归函数，将输入作为字符串，并返回提取的每个字符的所需答案的数组。
3.  基本情况是**输入字符串为空**时。在这种情况下，返回一个包含空字符串的长度为 1 的数组。
4.  使用 helper 函数提取每个字符，并首先将其附加到空字符串中，然后将其存储在数组中，比如 **output1** 。
5.  同时检查字符长度是否大于或等于 2，并检查提取的两个字符是否在字母范围内。现在，将相应的字符存储在一个数组中，比如**输出 2** 。
6.  然后创建一个最终输出数组，其长度为**输出 1** 和**输出 2** 的长度之和，并存储它们的答案并返回。
7.  对提取的每一个或每一对相邻字符重复上述步骤。现在，返回获得的最终数组。
8.  [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个字符串，生成相应的小写字母字符串并打印出来。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to check if all the
// characters are lowercase or not
bool nonLower(string s)
{

    // Traverse the string
    for(int i = 0; i < s.size(); i++)
    {

        // If any character is not
        // found to be in lowerCase
        if (!islower(s[i]))
        {
            return true;
        }
    }
    return false;
}

// Function to print the decodings
void printCodes(vector<string> output)
{
    for(int i = 0; i < output.size(); i++)
    {

        // If all characters are not
        // in lowercase
        if (nonLower(output[i]))
            continue;

        cout << (output[i]) << endl;
    }
}

// Function to return the character
// corresponding to given integer
char getChar(int n)
{
    return (char)(n + 96);
}

// Function to return the decodings
vector<string> getCode(string str)
{

    // Base case
    if (str.size() == 0)
    {
        vector<string> ans;
        ans.push_back("");
        return ans;
    }

    // Recursive call
    vector<string> output1 = getCode(str.substr(1));

    // Stores the characters of
    // two digit numbers
    vector<string> output2(0);

    // Extract first digit and
    // first two digits
    int firstDigit= (str[0] - '0');
    int firstTwoDigit = 0;

    if (str.size() >= 2)
    {
        firstTwoDigit = (str[0] - '0') * 10 +
                        (str[1] - '0');

        // Check if it lies in the
        // range of alphabets
        if (firstTwoDigit >= 10 &&
            firstTwoDigit <= 26)
        {

            // Next recursive call
            output2 = getCode(str.substr(2));
        }
    }

    // Combine both the output in a
    // single final output array
    vector<string> output(output1.size() +
                          output2.size());

    // Index of final output array
    int k = 0;

    // Store the elements of output1
    // in final output array
    for(int i = 0; i < output1.size(); i++)
    {
        char ch = getChar(firstDigit);

        output[i] = ch + output1[i];
        k++;
    }

    // Store the elements of output2
    // in final output array
    for(int i = 0; i < output2.size(); i++)
    {
        char ch = getChar(firstTwoDigit);

        output[k] = ch + output2[i];
        k++;
    }

    // Result the result
    return output;
}

// Driver Code
int main()
{
    string input = "101";

    // Function call
    vector<string> output = getCode(input);

    // Print function call
    printCodes(output);
}

// This code is contributed by grand_master
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;

class GFG {

    // Function to check if all the
    // characters are lowercase or not
    public static boolean
    nonLower(String s)
    {
        // Traverse the string
        for (int i = 0; i < s.length(); i++) {

            // If any character is not
            // found to be in lowerCase
            if (!Character
                     .isLowerCase(s.charAt(i))) {
                return true;
            }
        }

        return false;
    }

    // Function to print the decodings
    public static void
    printCodes(String output[])
    {
        for (int i = 0; i < output.length; i++) {

            // If all characters are not
            // in lowercase
            if (nonLower(output[i]))
                continue;
            System.out.println(output[i]);
        }
    }

    // Function to return the character
    // corresponding to given integer
    public static char getChar(int n)
    {
        return (char)(n + 96);
    }

    // Function to return the decodings
    public static String[] getCode(
        String str)
    {
        // Base case
        if (str.length() == 0) {

            String ans[] = { "" };
            return ans;
        }

        // Recursive call
        String output1[]
            = getCode(str.substring(1));

        // Stores the characters of
        // two digit numbers
        String output2[] = new String[0];

        // Extract first digit and
        // first two digits
        int firstDigit
            = (str.charAt(0) - '0');
        int firstTwoDigit = 0;

        if (str.length() >= 2) {

            firstTwoDigit
                = (str.charAt(0) - '0') * 10
                  + (str.charAt(1) - '0');

            // Check if it lies in the
            // range of alphabets
            if (firstTwoDigit >= 10
                && firstTwoDigit <= 26) {

                // Next recursive call
                output2
                    = getCode(str.substring(2));
            }
        }

        // Combine both the output in a
        // single final output array
        String output[]
            = new String[output1.length
                         + output2.length];

        // Index of final output array
        int k = 0;

        // Store the elements of output1
        // in final output array
        for (int i = 0; i < output1.length; i++) {

            char ch = getChar(firstDigit);

            output[i] = ch + output1[i];
            k++;
        }

        // Store the elements of output2
        // in final output array
        for (int i = 0; i < output2.length; i++) {

            char ch = getChar(firstTwoDigit);

            output[k] = ch + output2[i];
            k++;
        }

        // Result the result
        return output;
    }

    // Driver Code
    public static void main(String[] args)
    {
        String input = "101";

        // Function call
        String output[] = getCode(input);

        // Print function call
        printCodes(output);
    }
}
```

## 蟒蛇 3

```
# Python3 program for
# the above approach

# Function to check if all the
# characters are lowercase or not
def nonLower(s):

    # Traverse the string
    for i in range(len(s)):

        # If any character is not
        # found to be in lowerCase
        if not s[i].islower():
            return True

    return False

# Function to print the decodings
def printCodes(output):

    for i in range(len(output)):

        # If all characters are not
        # in lowercase
        if (nonLower(output[i])):
            continue

        print(output[i])

# Function to return the character
# corresponding to given integer
def getChar(n):

  return chr(n + 96)

# Function to return the decodings
def getCode(str):

    # Base case
    if (len(str) == 0):
        ans = [""]
        return ans

    # Recursive call
    output1 = getCode(str[1:])

    # Stores the characters of
    # two digit numbers
    output2 = []

    # Extract first digit and
    # first two digits
    firstDigit = (ord(str[0]) - ord('0'))
    firstTwoDigit = 0

    if (len(str) >= 2):
      firstTwoDigit = ((ord(str[0]) - ord('0')) * 10 +
                       (ord(str[1]) - ord('0')))

      # Check if it lies in the
      # range of alphabets
      if (firstTwoDigit >= 10 and firstTwoDigit <= 26):

        # Next recursive call
        output2 = getCode(str[2:])

    # Combine both the output in a
    # single readonly output array
    output = ['' for i in range(len(output1) +
                                len(output2))]

    # Index of readonly output array
    k = 0

    # Store the elements of output1
    # in readonly output array
    for i in range(len(output1)):
        ch = getChar(firstDigit)
        output[i] = ch + output1[i]
        k += 1

    # Store the elements of output2
    # in readonly output array
    for i in range(len(output2)):
        ch = getChar(firstTwoDigit)
        output[k] = ch + output2[i]
        k += 1

    # Result the result
    return output

# Driver Code
if __name__=='__main__':

    input = "101"

    # Function call
    output = getCode(input)

    # Print function call
    printCodes(output)

# This code is contributed by rutvik_56
```

## C#

```
// C# program for
// the above approach
using System;
class GFG{

// Function to check if all the
// characters are lowercase or not
public static bool nonLower(String s)
{
  // Traverse the string
  for (int i = 0; i < s.Length; i++)
  {
    // If any character is not
    // found to be in lowerCase
    if (!char.IsLower(s[i]))
    {
      return true;
    }
  }
  return false;
}

// Function to print the decodings
public static void printCodes(String []output)
{
  for (int i = 0; i < output.Length; i++)
  {
    // If all characters are not
    // in lowercase
    if (nonLower(output[i]))
      continue;
    Console.WriteLine(output[i]);
  }
}

// Function to return the character
// corresponding to given integer
public static char getChar(int n)
{
  return (char)(n + 96);
}

// Function to return the decodings
public static String[] getCode(String str)
{
  // Base case
  if (str.Length == 0)
  {
    String []ans = { "" };
    return ans;
  }

  // Recursive call
  String []output1 = getCode(str.Substring(1));

  // Stores the characters of
  // two digit numbers
  String []output2 = new String[0];

  // Extract first digit and
  // first two digits
  int firstDigit = (str[0] - '0');
  int firstTwoDigit = 0;

  if (str.Length >= 2)
  {
    firstTwoDigit = (str[0] - '0') * 10 +
                    (str[1] - '0');

    // Check if it lies in the
    // range of alphabets
    if (firstTwoDigit >= 10 &&
        firstTwoDigit <= 26)
    {
      // Next recursive call
      output2 = getCode(str.Substring(2));
    }
  }

  // Combine both the output in a
  // single readonly output array
  String []output = new String[output1.Length +
                               output2.Length];

  // Index of readonly output array
  int k = 0;

  // Store the elements of output1
  // in readonly output array
  for (int i = 0; i < output1.Length; i++)
  {
    char ch = getChar(firstDigit);
    output[i] = ch + output1[i];
    k++;
  }

  // Store the elements of output2
  // in readonly output array
  for (int i = 0; i < output2.Length; i++)
  {
    char ch = getChar(firstTwoDigit);   
    output[k] = ch + output2[i];
    k++;
  }

  // Result the result
  return output;
}

// Driver Code
public static void Main(String[] args)
{
  String input = "101";

  // Function call
  String []output = getCode(input);

  // Print function call
  printCodes(output);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Function to check if all the
    // characters are lowercase or not
    function nonLower(s)
    {

      // Traverse the string
      for(let i = 0; i < s.length; i++)
      {

        // If any character is not
        // found to be in lowerCase
        if (!(s[i].charCodeAt() >= 97 && s[i].charCodeAt() <= 122))
        {
          return true;
        }
      }
      return false;
    }

    // Function to print the decodings
    function printCodes(output)
    {
      for (let i = 0; i < output.length; i++)
      {

        // If all characters are not
        // in lowercase
        if (nonLower(output[i]))
          continue;
        document.write(output[i] + "</br>");
      }
    }

    // Function to return the character
    // corresponding to given integer
    function getChar(n)
    {
      return String.fromCharCode(n + 96);
    }

    // Function to return the decodings
    function getCode(str)
    {
      // Base case
      if (str.length == 0)
      {
        let ans = [ "" ];
        return ans;
      }

      // Recursive call
      let output1 = getCode(str.substring(1));

      // Stores the characters of
      // two digit numbers
      let output2 = new Array(0);

      // Extract first digit and
      // first two digits
      let firstDigit = (str[0] - '0');
      let firstTwoDigit = 0;

      if (str.length >= 2)
      {
        firstTwoDigit = (str[0].charCodeAt() - '0'.charCodeAt()) * 10 +
                        (str[1].charCodeAt() - '0'.charCodeAt());

        // Check if it lies in the
        // range of alphabets
        if (firstTwoDigit >= 10 &&
            firstTwoDigit <= 26)
        {
          // Next recursive call
          output2 = getCode(str.substring(2));
        }
      }

      // Combine both the output in a
      // single readonly output array
      let output = new Array(output1.length + output2.length);

      // Index of readonly output array
      let k = 0;

      // Store the elements of output1
      // in readonly output array
      for (let i = 0; i < output1.length; i++)
      {
        let ch = getChar(firstDigit);
        output[i] = ch + output1[i];
        k++;
      }

      // Store the elements of output2
      // in readonly output array
      for (let i = 0; i < output2.length; i++)
      {
        let ch = getChar(firstTwoDigit);  
        output[k] = ch + output2[i];
        k++;
      }

      // Result the result
      return output;
    }

    let input = "101";

    // Function call
    let output = getCode(input);

    // Print function call
    printCodes(output);

  // This code is contributed by mukesh07.
</script>
```

**Output:** 

```
ja
```

***时间复杂度:**O(2<sup>N</sup>)*
***空间复杂度:** O(N)*