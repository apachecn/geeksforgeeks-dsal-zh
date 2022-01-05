# 通过从给定字符串中的十六进制表示中删除字符来修改数组

> 原文:[https://www . geesforgeks . org/通过从给定字符串的十六进制表示中移除字符来修改数组/](https://www.geeksforgeeks.org/modify-array-by-removing-characters-from-their-hexadecimal-representations-which-are-present-in-a-given-string/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和一个[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是通过从 **S** 中存在的十六进制表示中移除所有字符，然后将等效的十进制元素替换回数组来修改给定数组。

**示例:**

> **输入:** arr[] = {74，91，31，122}，S = "1AB"
> **输出:** {4，5，15，7}
> **解释:**T8】74->(4A)<sup>16</sup>->(4)16->4
> 91->(5B)16->(5)116
> 
> **输入:** arr[] = {1450，1716，284，843}，S = "ABFE3"
> **输出:** {5，100，284，4}

**方法:**按照以下步骤解决问题:

*   [穿越阵](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)T2【arr】:
    *   [将每个数组元素转换为其等价的十六进制值](https://www.geeksforgeeks.org/program-decimal-hexadecimal-conversion/)。
    *   从字符串 s 中存在的十六进制数中删除字符
    *   [将修改后的十六进制数转换回十进制表示](https://www.geeksforgeeks.org/program-for-hexadecimal-to-decimal/)。
    *   用它替换数组元素。
*   打印修改后的数组。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to convert a decimal number
// to its equivalent hexadecimal number
string decHex(int n)
{
  char alpha[] = { 'A', 'B', 'C', 'D', 'E', 'F' };
  string ans;
  while (n > 0) {
    if (n % 16 < 10) {
      ans += to_string(n % 16);
    }
    else {
      ans += alpha[n % 16 - 10];
    }
    n /= 16;
  }
  reverse(ans.begin(), ans.end());
  return ans;
}

// Function to convert hexadecimal number
// to its equavalent decimal number
int hexDec(string convertedHex)
{

  // Stores characters with their
  // respective hexadecimal values
  char mp[] = { 10, 11, 12, 13, 14, 15 };

  // Stores answer
  int ans = 0;
  int pos = 0;

  // Traverse the string
  reverse(convertedHex.begin(), convertedHex.end());
  for (char ch : convertedHex) {

    // If digit
    if (isdigit(ch)) {
      ans += ((int)pow(16, pos)) * (ch - '0');
    }

    // If character
    else {
      ans += ((int)pow(16, pos)) * mp[ch - 'A'];
    }
    pos += 1;
  }
  // Return the answer
  return ans;
}

// Function to move all the
// alphabets to front
string removeChars(string hexaVal, string S)
{
  set<char> setk;
  for (char ch : S) {
    setk.insert(ch);
  }
  string ans = "";
  for (char ch : hexaVal) {
    if (setk.find(ch) != setk.end()) {
      continue;
    }
    ans += ch;
  }
  return ans;
}

// Function to modify each array
// element by removing characters
// from their hexadecimal representation
// which are present in a given string
void convertArr(int arr[], int N, string S)
{

  // Traverse the array
  for (int i = 0; i < N; i++) {

    // Stores hexadecimal value
    string hexaVal = decHex(arr[i]);

    // Remove the characters from hexadecimal
    // representation present in string S
    string convertedHex = removeChars(hexaVal, S);

    // Stores decimal value
    int decVal = hexDec(convertedHex);

    // Replace array element
    arr[i] = decVal;
  }

  // Print the modified array
  for (int i = 0; i < N; i++) {
    cout << arr[i] << " ";
  }
}

// Driven Program
int main()
{
  // Given array
  int arr[] = { 74, 91, 31, 122 };
  int N = sizeof(arr) / sizeof(arr[0]);

  // Given string
  string S = "1AB";

  // Function call to modify
  // array by given operations
  convertArr(arr, N, S);

  return 0;
}

// This code is contributed by Kingash.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG {

  // Function to convert a decimal number
  // to its equivalent hexadecimal number
  static String decHex(int n)
  {
    char alpha[] = { 'A', 'B', 'C', 'D', 'E', 'F' };
    StringBuilder ans = new StringBuilder("");
    while (n > 0) {
      if (n % 16 < 10) {
        ans.append(Integer.toString(n % 16));
      }
      else {
        ans.append(alpha[n % 16 - 10]);
      }
      n /= 16;
    }
    ans = ans.reverse();
    return ans.toString();
  }

  // Function to convert hexadecimal number
  // to its equavalent decimal number
  static int hexDec(String convertedHex)
  {

    // Stores characters with their
    // respective hexadecimal values
    char mp[] = { 10, 11, 12, 13, 14, 15 };

    // Stores answer
    int ans = 0;
    int pos = 0;

    // Traverse the string
    StringBuilder s = new StringBuilder(convertedHex);
    convertedHex = s.reverse().toString();
    for (char ch : convertedHex.toCharArray()) {

      // If digit
      if (Character.isDigit(ch)) {
        ans += ((int)Math.pow(16, pos))
          * (ch - '0');
      }

      // If character
      else {
        ans += ((int)Math.pow(16, pos))
          * mp[ch - 'A'];
      }
      pos += 1;
    }
    // Return the answer
    return ans;
  }

  // Function to move all the
  // alphabets to front
  static String removeChars(String hexaVal, String S)
  {
    HashSet<Character> setk = new HashSet<>();
    for (char ch : S.toCharArray()) {
      setk.add(ch);
    }
    String ans = "";
    for (char ch : hexaVal.toCharArray()) {
      if (setk.contains(ch)) {
        continue;
      }
      ans += ch;
    }
    return ans;
  }

  // Function to modify each array
  // element by removing characters
  // from their hexadecimal representation
  // which are present in a given string
  static void convertArr(int arr[], String S)
  {

    // Traverse the array
    for (int i = 0; i < arr.length; i++) {

      // Stores hexadecimal value
      String hexaVal = decHex(arr[i]);

      // Remove the characters from hexadecimal
      // representation present in string S
      String convertedHex = removeChars(hexaVal, S);

      // Stores decimal value
      int decVal = hexDec(convertedHex);

      // Replace array element
      arr[i] = decVal;
    }

    // Print the modified array
    for (int val : arr) {
      System.out.print(val + " ");
    }
  }

  // Driver Code
  public static void main(String[] args)
  {

    // Given array
    int arr[] = { 74, 91, 31, 122 };

    // Given string
    String S = "1AB";

    // Function call to modify
    // array by given operations
    convertArr(arr, S);
  }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to convert a decimal number
# to its equivalent hexadecimal number
def decHex(n):
    alpha = ['A', 'B', 'C', 'D', 'E', 'F']
    ans = ''
    while n:
        if n % 16 < 10:
            ans += str(n % 16)
        else:
            ans += alpha[n % 16 - 10]
        n //= 16

    ans = ans[::-1]
    return ans

# Function to convert hexadecimal number
# to its equavalent decimal number
def hexDec(convertedHex):

    # Stores characters with their
    # respective hexadecimal values
    mp = {"A": 10, "B": 11, "C": 12,
           "D": 13, "E": 14, "F": 15}

    # Stores answer
    ans = 0
    pos = 0

    # Traverse the string
    for i in convertedHex[::-1]:

        # If digit
        if i.isdigit():
            ans += (16**pos)*int(i)

        # If character
        else:
            ans += (16**pos)*mp[i]
        pos += 1

    # Return the answer
    return ans

# Function to move all the
# alphabets to front
def removeChars(hexaVal, S):
    setk = set()
    for i in S:
        setk.add(i)
    ans = ''
    for i in hexaVal:
        if i in setk:
            continue
        ans += i

    return ans

# Function to modify each array
# element by removing characters
# from their hexadecimal representation
# which are present in a given string
def convertArr(arr, S):

    # Traverse the array
    for i in range(len(arr)):

        # Stores hexadecimal value
        hexaVal = decHex(arr[i])

        # Remove the characters from hexadecimal
        # representation present in string S
        convertedHex = removeChars(hexaVal, S)

        # Stores decimal value
        decVal = hexDec(convertedHex)

        # Replace array element
        arr[i] = decVal

    # Print the modified array
    print(arr)

# Driver Code
# Given array
arr = [74, 91, 31, 122]

# Given string
S = "1AB"

# Function call to modify
# array by given operations
convertArr(arr, S)
```

**Output:** 

```
[4, 5, 15, 7]
```

***时间复杂度:**O(N * | S |)*
T5**辅助空间:** O(|S|)