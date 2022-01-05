# 使用 Z 算法

从给定字符串中删除所有出现的单词

> 原文:[https://www . geesforgeks . org/从给定字符串中删除所有出现的单词-使用-z-算法/](https://www.geeksforgeeks.org/remove-all-occurrences-of-a-word-from-a-given-string-using-z-algorithm/)

给定两个长度为 **N** 的[**字符串**和长度为 **M** 的**单词**，任务是从字符串**字符串**中移除字符串**单词**的所有出现。](https://www.geeksforgeeks.org/string-data-structure/)

**示例:**

> **输入:**str = " asmgeesmasmforasmgeeks "，word = "asm"
> **输出:** GeeksForGeeks
> **解释:**
> 从字符串中移除“asm”，str 将 str 修改为 GeeksForGeeks
> 
> **输入:**str = " Z-kmalgorithm kmiskmkmhelpflekminkmsarching "，word = "km"
> **输出:**Z-algorithm ishelpfirsearch
> 
> **解释:**
> 去掉字符串中的“km”，str 将 str 修改为“Z-algorithm is helpfirsearch”。

**天真方法:**解决这个问题最简单的方法就是[迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **字符串**的字符。对于每个索引，检查是否可以找到起始索引等于当前索引的子串，并且子串等于字符串**字**。如果发现为真，则移除子字符串。最后，打印字符串。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

[**STL**](https://www.geeksforgeeks.org/the-c-standard-template-library-stl/) **【基于】的方法** : [使用](https://www.geeksforgeeks.org/remove-a-given-word-from-a-string/) [replace()](https://www.geeksforgeeks.org/stdstringreplace-stdstringreplace_if-c/) 方法从字符串 **str** 中删除所有出现的字符串**单词**。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以使用 [Z 算法](https://www.geeksforgeeks.org/z-algorithm-linear-time-pattern-searching-algorithm/)进行优化。按照以下步骤解决问题:

*   初始化一个字符串，说 **res** ，通过从给定字符串 **str** 中删除单词来存储该字符串。
*   初始化一个[数组](https://www.geeksforgeeks.org/array-data-structure/)，比如 **Z[]** ，来存储字符串的 **Z** 值。
*   使用 Z 算法查找给定字符串**字符串**中所有出现的字符串**单词**。
*   最后，[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **Z[]** ，检查 **z[i +长度(字)+ 1]** 是否等于**长度(字)**。如果发现为真，则更新 **i +=长度(字)–1**。
*   否则，将当前字符追加到字符串 **res** 中。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to fill the Z-array for str
void getZarr(string str, int Z[])
{
    int n = str.length();
    int k;

    // L Stores start index of window
    // which matches with prefix of str
    int L = 0;

    // R Stores end index of window
    // which matches with prefix of str
    int R = 0;

    // Iterate over the characters of str
    for (int i = 1; i < n; ++i) {

        // If i is greater thn R
        if (i > R) {

            // Update L and R
            L = R = i;

            // If substring match with prefix
            while (R < n && str[R - L] == str[R]) {

                // Update R
                R++;
            }

            // Update Z[i]
            Z[i] = R - L;

            // Update R
            R--;
        }
        else {

            // Update k
            k = i - L;

            // if Z[k] is less than
            // remaining interval
            if (Z[k] < R - i + 1) {

                // Update Z[i]
                Z[i] = Z[k];
            }

            else {

                // Start from R and check manually
                L = i;
                while (R < n && str[R - L] == str[R]) {

                    // Update R
                    R++;
                }

                // Update Z[i]
                Z[i] = R - L;

                // Update R
                R--;
            }
        }
    }
}

// Function to remove all the occurrences
// of word from str
string goodStr(string str, string word)
{
    // Create concatenated string "P$T"
    string concat = word + "{content}quot; + str;
    int l = concat.length();

    // Store Z array of concat
    int Z[l];

    getZarr(concat, Z);

    // Stores string, str by removing all
    // the occurrences of word from str
    string res;

    // Stores length of word
    int pSize = word.size();

    // Traverse the array, Z[]
    for (int i = 0; i < l; ++i) {

        // if Z[i + pSize + 1] equal to
        // length of word
        if (i + pSize < l - 1 && Z[i + pSize + 1] == pSize) {

            // Update i
            i += pSize - 1;
        }
        else if (i < str.length()) {
            res += str[i];
        }
    }
    return res;
}

// Driver Code
int main()
{
    string str
        = "Z-kmalgorithmkmiskmkmkmhelpfulkminkmsearching";
    string word = "km";

    cout << goodStr(str, word);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

  // Function to fill the Z-array for str
  static void getZarr(String str, int Z[])
  {
    int n = str.length();
    int k;

    // L Stores start index of window
    // which matches with prefix of str
    int L = 0;

    // R Stores end index of window
    // which matches with prefix of str
    int R = 0;

    // Iterate over the characters of str
    for (int i = 1; i < n; ++i)
    {

      // If i is greater thn R
      if (i > R)
      {

        // Update L and R
        L = R = i;

        // If subString match with prefix
        while (R < n && str.charAt(R - L) ==
               str.charAt(R))
        {

          // Update R
          R++;
        }

        // Update Z[i]
        Z[i] = R - L;

        // Update R
        R--;
      }
      else
      {

        // Update k
        k = i - L;

        // if Z[k] is less than
        // remaining interval
        if (Z[k] < R - i + 1)
        {

          // Update Z[i]
          Z[i] = Z[k];
        }

        else
        {

          // Start from R and check manually
          L = i;
          while (R < n && str.charAt(R - L) ==
                 str.charAt(R))
          {

            // Update R
            R++;
          }

          // Update Z[i]
          Z[i] = R - L;

          // Update R
          R--;
        }
      }
    }
  }

  // Function to remove all the occurrences
  // of word from str
  static String goodStr(String str, String word)
  {
    // Create concatenated String "P$T"
    String concat = word + "{content}quot; + str;
    int l = concat.length();

    // Store Z array of concat
    int []Z = new int[l];

    getZarr(concat, Z);

    // Stores String, str by removing all
    // the occurrences of word from str
    String res="";

    // Stores length of word
    int pSize = word.length();

    // Traverse the array, Z[]
    for (int i = 0; i < l; ++i) {

      // if Z[i + pSize + 1] equal to
      // length of word
      if (i + pSize < l - 1 && Z[i + pSize + 1] == pSize) {

        // Update i
        i += pSize - 1;
      }
      else if (i < str.length()) {
        res += str.charAt(i);
      }
    }
    return res;
  }

  // Driver Code
  public static void main(String[] args)
  {
    String str
      = "Z-kmalgorithmkmiskmkmkmhelpfulkminkmsearching";
    String word = "km";

    System.out.print(goodStr(str, word));
  }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to fill the Z-array for str
def getZarr(st, Z):
    n = len(st)
    k = 0

    # L Stores start index of window
    # which matches with prefix of str
    L = 0

    # R Stores end index of window
    # which matches with prefix of str
    R = 0

    # Iterate over the characters of str
    for i in range(1, n):

        # If i is greater thn R
        if (i > R):

            # Update L and R
            L = R = i

            # If substring match with prefix
            while (R < n and st[R - L] == st[R]):

                # Update R
                R += 1

            # Update Z[i]
            Z[i] = R - L

            # Update R
            R -= 1

        else:

            # Update k
            k = i - L

            # if Z[k] is less than
            # remaining interval
            if (Z[k] < R - i + 1):

                # Update Z[i]
                Z[i] = Z[k]

            else:

                # Start from R and check manually
                L = i
                while (R < n and st[R - L] == st[R]):

                    # Update R
                    R += 1

                # Update Z[i]
                Z[i] = R - L

                # Update R
                R -= 1

# Function to remove all the occurrences
# of word from str

def goodStr(st, word):

    # Create concatenated string "P$T"
    concat = word + "{content}quot; + st
    l = len(concat)

    # Store Z array of concat
    Z = [0]*l

    getZarr(concat, Z)

    # Stores string, str by removing all
    # the occurrences of word from str
    res = ""

    # Stores length of word
    pSize = len(word)

    # Traverse the array, Z[]
    for i in range(l):

        # if Z[i + pSize + 1] equal to
        # length of word
        if (i + pSize < l - 1 and Z[i + pSize + 1] == pSize):

            # Update i
            i += pSize - 1

        elif (i < len(st)):
            res += st[i]

    return res

# Driver Code
if __name__ == "__main__":

    st = "Z-kmalgorithmkmiskmkmkmhelpfulkminkmsearching"
    word = "km"

    print(goodStr(st, word))

    # This code is contributed by chitranayal.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG
{

  // Function to fill the Z-array for str
  static void getZarr(string str, int[] Z)
  {
    int n = str.Length;
    int k;

    // L Stores start index of window
    // which matches with prefix of str
    int L = 0;

    // R Stores end index of window
    // which matches with prefix of str
    int R = 0;

    // Iterate over the characters of str
    for (int i = 1; i < n; ++i)
    {

      // If i is greater thn R
      if (i > R)
      {

        // Update L and R
        L = R = i;

        // If subString match with prefix
        while (R < n && str[R - L] ==
               str[R])
        {

          // Update R
          R++;
        }

        // Update Z[i]
        Z[i] = R - L;

        // Update R
        R--;
      }
      else
      {

        // Update k
        k = i - L;

        // if Z[k] is less than
        // remaining interval
        if (Z[k] < R - i + 1)
        {

          // Update Z[i]
          Z[i] = Z[k];
        }

        else
        {

          // Start from R and check manually
          L = i;
          while (R < n && str[R - L] ==
                 str[R])
          {

            // Update R
            R++;
          }

          // Update Z[i]
          Z[i] = R - L;

          // Update R
          R--;
        }
      }
    }
  }

  // Function to remove all the occurrences
  // of word from str
  static string goodStr(string str, string word)
  {

    // Create concatenated String "P$T"
    string concat = word + "{content}quot; + str;
    int l = concat.Length;

    // Store Z array of concat
    int []Z = new int[l];
    getZarr(concat, Z);

    // Stores String, str by removing all
    // the occurrences of word from str
    string res="";

    // Stores length of word
    int pSize = word.Length;

    // Traverse the array, Z[]
    for (int i = 0; i < l; ++i) {

      // if Z[i + pSize + 1] equal to
      // length of word
      if (i + pSize < l - 1 && Z[i + pSize + 1] == pSize) {

        // Update i
        i += pSize - 1;
      }
      else if (i < str.Length) {
        res += str[i];
      }
    }
    return res;
  }

  // Driver Code
  static public void Main()
  {
    string str
      = "Z-kmalgorithmkmiskmkmkmhelpfulkminkmsearching";
    string word = "km";

    Console.WriteLine(goodStr(str, word));
  }
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>
//js program for the above approach

// Function to fill the Z-array for str
function getZarr(str,Z)
{
  let  n = str.length;
  let  k;

  // L Stores start index of window
  // which matches with prefix of str
  let  L = 0;

  // R Stores end index of window
  // which matches with prefix of str
  let  R = 0;

  // Iterate over the characters of str
  for (let  i = 1; i < n; ++i)
  {

    // If i is greater thn R
    if (i > R)
    {

      // Update L and R
      L = R = i;

      // If subString match with prefix
      while (R < n && str[R - L] ==
             str[R])
      {

        // Update R
        R++;
      }

      // Update Z[i]
      Z[i] = R - L;

      // Update R
      R--;
    }
    else
    {

      // Update k
      k = i - L;

      // if Z[k] is less than
      // remaining interval
      if (Z[k] < R - i + 1)
      {

        // Update Z[i]
        Z[i] = Z[k];
      }

      else
      {

        // Start from R and check manually
        L = i;
        while (R < n && str[R - L] ==
               str[R])
        {

          // Update R
          R++;
        }

        // Update Z[i]
        Z[i] = R - L;

        // Update R
        R--;
      }
    }
  }
}

// Function to remove all the occurrences
// of word from str
function goodStr(str,word)
{

  // Create concatenated String "P$T"
  let concat = word + "{content}quot; + str;
  let  l = concat.length;

  // Store Z array of concat
  let  Z = new Array(l);
  getZarr(concat, Z);

  // Stores String, str by removing all
  // the occurrences of word from str
  let res="";

  // Stores length of word
  let  pSize = word.length;

  // Traverse the array, Z[]
  for (let  i = 0; i < l; ++i) {

    // if Z[i + pSize + 1] equal to
    // length of word
    if (i + pSize < l - 1 && Z[i + pSize + 1] == pSize) {

      // Update i
      i += pSize - 1;
    }
    else if (i < str.length) {
      res += str[i];
    }
  }
  return res;
}

// Driver Code

let str = "Z-kmalgorithmkmiskmkmkmhelpfulkminkmsearching";
let word = "km";

document.write(goodStr(str, word));

</script>
```

**Output:** 

```
Z-algorithmishelpfulinsearching
```

***时间复杂度:** O(N + M)*
***辅助空间:** O(N)*