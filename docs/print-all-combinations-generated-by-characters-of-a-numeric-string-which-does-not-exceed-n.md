# 打印由不超过 N 的数字字符串的字符生成的所有组合

> 原文:[https://www . geesforgeks . org/print-all-combinations-由不超过 n 的数字字符串字符生成/](https://www.geeksforgeeks.org/print-all-combinations-generated-by-characters-of-a-numeric-string-which-does-not-exceed-n/)

给定一个长度为 **M** 的数字[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** 和一个整数 **N** ，任务是找出最多为 **N** 的 **S** ( *允许重复次数*)的所有不同组合。

**示例:**

> **输入:** S = "124 "，N = 100
> **输出:** 1、11、12、14、2、21、22、24、4、41、42、44
> **说明:**组合“111”、“112”、“122”、“124”、“412”大于 100。因此，这些组合被排除在输出之外。
> 
> **输入:** S = "345 "，N = 400
> **输出:** 3、33、333、334、335、34、343、344、345、35、353、354、355、4、43、44、45、5、53、54、55

**方法:**想法是使用[回溯](https://www.geeksforgeeks.org/backtracking-introduction/)生成所有可能的数字，然后打印那些不超过 **N** 的数字。按照以下步骤解决问题:

*   初始化一组[字符串，比如**组合[]、**来存储所有不同的 **S** 组合，数值不超过 **N** 。](https://www.geeksforgeeks.org/set-in-cpp-stl/)
*   初始化一个字符串**和**来存储当前可能来自**的数字组合**。
*   声明一个函数 **generateCombinations()** 来生成所有必需的组合，这些组合的值小于给定值 **N** ，该函数定义为:
    *   使用变量 **i** 在范围**【0，M】**内遍历字符串 **S** ，并执行以下操作:
        *   将当前字符 **S[i]** 推至 **ans** 并将当前字符串 **ans** 转换为数字并存储在 **x** 中。
        *   如果 **x** 小于或等于 **N** ，则将字符串 **ans** 推入**组合【】**并递归调用函数 **generateCombinations()** 。
    *   通过从**和**中移除 **i <sup>th</sup>** 字符，返回到其先前的状态。
*   完成上述步骤后，打印存储在**组合【】**中的所有字符串的集合。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Store the current sequence of s
string combination;

// Store the all the required sequences
set<string> combinations;

// Function to print all sequences of S
// satisfying the required condition
void printSequences(
    set<string> combinations)
{
    // Print all strings in the set
    for (string s : combinations) {
        cout << s << ' ';
    }
}

// Function to generate all sequences
// of string S that are at most N
void generateCombinations(string& s, int n)
{

    // Iterate over string s
    for (int i = 0; i < s.size(); i++) {

        // Push ith character to combination
        combination.push_back(s[i]);

        // Convert the string to number
        long x = stol(combination);

        // Check if the condition is true
        if (x <= n) {

            // Push the current string to
            // the final set of sequences
            combinations.insert(combination);

            // Recursively call function
            generateCombinations(s, n);
        }

        // Backtrack to its previous state
        combination.pop_back();
    }
}

// Driver Code
int main()
{
    string S = "124";
    int N = 100;

    // Function Call
    generateCombinations(S, N);

    // Print required sequences
    printSequences(combinations);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Store the current sequence of s
static String combination = "";

// Store the all the required sequences
static HashSet<String> combinations = new LinkedHashSet<String>();

// Function to print all sequences of S
// satisfying the required condition
static void printSequences(
    HashSet<String> combinations)
{

    // Print all Strings in the set
    for(String s : combinations)
    {
        System.out.print(s + " ");
    }
}

// Function to generate all sequences
// of String S that are at most N
static void generateCombinations(String s, int n)
{

    // Iterate over String s
    for(int i = 0; i < s.length(); i++)
    {

        // Push ith character to combination
        combination += (s.charAt(i));

        // Convert the String to number
        long x = Integer.valueOf(combination);

        // Check if the condition is true
        if (x <= n)
        {

            // Push the current String to
            // the final set of sequences
            combinations.add(combination);

            // Recursively call function
            generateCombinations(s, n);
        }

        // Backtrack to its previous state
        combination = combination.substring(
            0, combination.length() - 1);
    }
}

// Driver Code
public static void main(String[] args)
{
    String S = "124";
    int N = 100;

    // Function Call
    generateCombinations(S, N);

    // Print required sequences
    printSequences(combinations);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Store the current sequence of s
combination = "";

# Store the all the required sequences
combinations = [];

# Function to print all sequences of S
# satisfying the required condition
def printSequences(combinations) :

    # Print all strings in the set
    for s in (combinations) :
        print(s, end = ' ');

# Function to generate all sequences
# of string S that are at most N
def generateCombinations(s, n) :   
    global combination;

    # Iterate over string s
    for i in range(len(s)) :

        # Push ith character to combination
        combination += s[i];

        # Convert the string to number
        x = int(combination);

        # Check if the condition is true
        if (x <= n) :

            # Push the current string to
            # the final set of sequences
            combinations.append(combination);

            # Recursively call function
            generateCombinations(s, n);

        # Backtrack to its previous state
        combination = combination[:-1];

# Driver Code
if __name__ == "__main__" :

    S = "124";
    N = 100;

    # Function Call
    generateCombinations(S, N);

    # Print required sequences
    printSequences(combinations);

    # This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

// Store the current sequence of s
static String combination = "";

// Store the all the required sequences
static SortedSet<String> combinations = new SortedSet<String>();

// Function to print all sequences of S
// satisfying the required condition
static void printSequences(
    SortedSet<String> combinations)
{

    // Print all Strings in the set
    foreach(String s in combinations)
    {
        Console.Write(s + " ");
    }
}

// Function to generate all sequences
// of String S that are at most N
static void generateCombinations(String s, int n)
{

    // Iterate over String s
    for(int i = 0; i < s.Length; i++)
    {

        // Push ith character to combination
        combination += (s[i]);

        // Convert the String to number
        long x = Int32.Parse(combination);

        // Check if the condition is true
        if (x <= n)
        {

            // Push the current String to
            // the readonly set of sequences
            combinations.Add(combination);

            // Recursively call function
            generateCombinations(s, n);
        }

        // Backtrack to its previous state
        combination = combination.Substring(
            0, combination.Length - 1);
    }
}

// Driver Code
public static void Main(String[] args)
{
    String S = "124";
    int N = 100;

    // Function Call
    generateCombinations(S, N);

    // Print required sequences
    printSequences(combinations);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
      // JavaScript program for the above approach
      // Store the current sequence of s
      var combination = "";

      // Store the all the required sequences
      var combinations = [];

      // Function to print all sequences of S
      // satisfying the required condition
      function printSequences(combinations) {
        // Print all Strings in the set
        for (var s of combinations) {
          document.write(s + " ");
        }
      }

      // Function to generate all sequences
      // of String S that are at most N
      function generateCombinations(s, n) {
        // Iterate over String s
        for (var i = 0; i < s.length; i++) {
          // Push ith character to combination
          combination += s[i];

          // Convert the String to number
          var x = parseInt(combination);

          // Check if the condition is true
          if (x <= n) {
            // Push the current String to
            // the readonly set of sequences
            combinations.push(combination);

            // Recursively call function
            generateCombinations(s, n);
          }

          // Backtrack to its previous state
          combination = combination.substring(0, combination.length - 1);
        }
      }

      // Driver Code
      var S = "124";
      var N = 100;

      // Function Call
      generateCombinations(S, N);

      // Print required sequences
      printSequences(combinations);
    </script>
```

**Output:** 

```
1 11 12 14 2 21 22 24 4 41 42 44
```

***时间复杂度:**O(N<sup>N</sup>)*
***辅助空间:** O(N <sup>N</sup> )*