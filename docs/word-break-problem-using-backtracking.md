# 使用回溯的断字问题

> 原文:[https://www . geesforgeks . org/word-break-problem-use-backtracing/](https://www.geeksforgeeks.org/word-break-problem-using-backtracking/)

给定一个单词之间没有空格的有效句子和一个有效英语单词词典，找到所有可能的方法将句子分解成单个词典单词。

**例**

```
Consider the following dictionary 
{ i, like, sam, sung, samsung, mobile, ice, 
  and, cream, icecream, man, go, mango}

Input: "ilikesamsungmobile"
Output: i like sam sung mobile
        i like samsung mobile

Input: "ilikeicecreamandmango"
Output: i like ice cream and man go
        i like ice cream and mango
        i like icecream and man go
        i like icecream and mango
```

我们已经在下面的帖子中讨论了动态编程解决方案。
[动态编程|第 32 集(断字问题)](https://www.geeksforgeeks.org/dynamic-programming-set-32-word-break-problem/)

动态编程解决方案只发现是否可能中断一个单词。这里我们需要打印所有可能的断字。
我们从左边开始扫描句子。当我们找到一个有效词时，我们需要检查句子的其余部分是否能构成有效词。因为在某些情况下，从左侧第一个找到的单词可能会留下无法进一步分离的剩余部分。因此，在这种情况下，我们应该回来，留下当前找到的单词，并继续搜索下一个单词。这个过程是递归的，因为要找出正确的部分是否可分离，我们需要同样的逻辑。所以我们将使用递归和回溯来解决这个问题。为了跟踪找到的单词，我们将使用堆栈。每当字符串的右边部分没有构成有效的单词时，我们就从堆栈中弹出顶部字符串并继续查找。

下面是上述想法的实现:

## C++

```
// A recursive program to print all possible
// partitions of a given string into dictionary
// words
#include <iostream>
using namespace std;

/* A utility function to check whether a word
  is present in dictionary or not.  An array of
  strings is used for dictionary.  Using array
  of strings for dictionary is definitely not
  a good idea. We have used for simplicity of
  the program*/
int dictionaryContains(string &word)
{
    string dictionary[] = {"mobile","samsung","sam","sung",
                            "man","mango", "icecream","and",
                            "go","i","love","ice","cream"};
    int n = sizeof(dictionary)/sizeof(dictionary[0]);
    for (int i = 0; i < n; i++)
        if (dictionary[i].compare(word) == 0)
            return true;
    return false;
}

// Prototype of wordBreakUtil
void wordBreakUtil(string str, int size, string result);

// Prints all possible word breaks of given string
void wordBreak(string str)
{
    // Last argument is prefix
    wordBreakUtil(str, str.size(), "");
}

// Result store the current prefix with spaces
// between words
void wordBreakUtil(string str, int n, string result)
{
    //Process all prefixes one by one
    for (int i=1; i<=n; i++)
    {
        // Extract substring from 0 to i in prefix
        string prefix = str.substr(0, i);

        // If dictionary contains this prefix, then
        // we check for remaining string. Otherwise
        // we ignore this prefix (there is no else for
        // this if) and try next
        if (dictionaryContains(prefix))
        {
            // If no more elements are there, print it
            if (i == n)
            {
                // Add this element to previous prefix
                result += prefix;
                cout << result << endl;
                return;
            }
            wordBreakUtil(str.substr(i, n-i), n-i,
                                result + prefix + " ");
        }
    }     
}

//Driver Code
int main()
{

    // Function call
    cout << "First Test:\n";
    wordBreak("iloveicecreamandmango");

    cout << "\nSecond Test:\n";
    wordBreak("ilovesamsungmobile");
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A recursive program to print all possible
// partitions of a given string into dictionary
// words
import java.io.*;
import java.util.*;

class GFG {

  // Prints all possible word breaks of given string
  static void wordBreak(int n, List<String> dict, String s)
  {
    String ans="";
    wordBreakUtil(n, s, dict, ans);
  }

  static void wordBreakUtil(int n, String s, List<String> dict, String ans)
  {
    for(int i = 1; i <= n; i++)
    {

      // Extract substring from 0 to i in prefix
      String prefix=s.substring(0, i);

      // If dictionary contains this prefix, then
      // we check for remaining string. Otherwise
      // we ignore this prefix (there is no else for
      // this if) and try next
      if(dict.contains(prefix))
      {
        // If no more elements are there, print it
        if(i == n)
        {

          // Add this element to previous prefix
          ans += prefix;
          System.out.println(ans);
          return;
        }
        wordBreakUtil(n - i, s.substring(i,n), dict, ans+prefix+" ");
      }
    }
  }

  // main function
  public static void main(String args[])
  {
    String str1 = "iloveicecreamandmango"; // for first test case
    String str2 ="ilovesamsungmobile";     // for second test case
    int n1 = str1.length();                 // length of first string
    int n2 = str2.length();                 // length of second string

    // List of strings in dictionary
    List <String> dict= Arrays.asList("mobile","samsung","sam","sung",
                                      "man","mango", "icecream","and",
                                      "go","i","love","ice","cream");        
    System.out.println("First Test:");

    // call to the method
    wordBreak(n1,dict,str1);
    System.out.println("\nSecond Test:");

    // call to the method
    wordBreak(n2,dict,str2);
  }
}

// This code is contributed by mohitjha727.
```

## 蟒蛇 3

```
# A recursive program to print all possible
# partitions of a given string into dictionary
# words

# A utility function to check whether a word
# is present in dictionary or not.  An array of
# strings is used for dictionary.  Using array
# of strings for dictionary is definitely not
# a good idea. We have used for simplicity of
# the program
def dictionaryContains(word):
    dictionary = {"mobile", "samsung", "sam", "sung", "man",
                  "mango", "icecream", "and", "go", "i", "love", "ice", "cream"}
    return word in dictionary

# Prints all possible word breaks of given string
def wordBreak(string):

    # Last argument is prefix
    wordBreakUtil(string, len(string), "")

# Result store the current prefix with spaces
# between words
def wordBreakUtil(string, n, result):

    # Process all prefixes one by one
    for i in range(1, n + 1):

        # Extract substring from 0 to i in prefix
        prefix = string[:i]

        # If dictionary contains this prefix, then
        # we check for remaining string. Otherwise
        # we ignore this prefix (there is no else for
        # this if) and try next
        if dictionaryContains(prefix):

            # If no more elements are there, print it
            if i == n:

                # Add this element to previous prefix
                result += prefix
                print(result)
                return
            wordBreakUtil(string[i:], n - i, result+prefix+" ")

# Driver Code
if __name__ == "__main__":
    print("First Test:")
    wordBreak("iloveicecreamandmango")

    print("\nSecond Test:")
    wordBreak("ilovesamsungmobile")

# This code is contributed by harshitkap00r
```

## C#

```
// A recursive program to print all possible
// partitions of a given string into dictionary
// words
using System;
using System.Collections.Generic;
class GFG {

      // Prints all possible word breaks of given string
      static void wordBreak(int n, List<string> dict, string s)
      {
        string ans="";
        wordBreakUtil(n, s, dict, ans);
      }

      static void wordBreakUtil(int n, string s, List<string> dict, string ans)
      {
        for(int i = 1; i <= n; i++)
        {

          // Extract substring from 0 to i in prefix
          string prefix=s.Substring(0, i);

          // If dictionary contains this prefix, then
          // we check for remaining string. Otherwise
          // we ignore this prefix (there is no else for
          // this if) and try next
          if(dict.Contains(prefix))
          {
            // If no more elements are there, print it
            if(i == n)
            {

              // Add this element to previous prefix
              ans += prefix;
              Console.WriteLine(ans);
              return;
            }
            wordBreakUtil(n - i, s.Substring(i,n-i), dict, ans+prefix+" ");
          }
        }
      }

  static void Main() {
    string str1 = "iloveicecreamandmango"; // for first test case
    string str2 ="ilovesamsungmobile";     // for second test case
    int n1 = str1.Length;                 // length of first string
    int n2 = str2.Length;                 // length of second string

    // List of strings in dictionary
    List<string> dict= new List<string>(new string[]{"mobile","samsung","sam","sung",
                                      "man","mango", "icecream","and",
                                      "go","i","love","ice","cream"});
    Console.WriteLine("First Test:");

    // call to the method
    wordBreak(n1,dict,str1);
    Console.WriteLine();
    Console.WriteLine("Second Test:");

    // call to the method
    wordBreak(n2,dict,str2);
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>
// A recursive program to print all possible
// partitions of a given string into dictionary
// words

// Prints all possible word breaks of given string
function wordBreak(n,dict,s)
{
    let ans="";
    wordBreakUtil(n, s, dict, ans);
}

function wordBreakUtil(n,s,dict,ans)
{
    for(let i = 1; i <= n; i++)
    {

      // Extract substring from 0 to i in prefix
      let prefix=s.substring(0, i);

      // If dictionary contains this prefix, then
      // we check for remaining string. Otherwise
      // we ignore this prefix (there is no else for
      // this if) and try next
      if(dict.includes(prefix))
      {
        // If no more elements are there, print it
        if(i == n)
        {

          // Add this element to previous prefix
          ans += prefix;
          document.write(ans+"<br>");
          return;
        }
        wordBreakUtil(n - i, s.substring(i,n), dict, ans+prefix+" ");
      }
    }
}

 // main function
let  str1 = "iloveicecreamandmango"; // for first test case
let str2 ="ilovesamsungmobile";     // for second test case
let n1 = str1.length;                 // length of first string
let n2 = str2.length;                 // length of second string

// List of strings in dictionary
let dict= ["mobile","samsung","sam","sung",
                                  "man","mango", "icecream","and",
                                  "go","i","love","ice","cream"];       
document.write("First Test:<br>");

// call to the method
wordBreak(n1,dict,str1);
document.write("<br>Second Test:<br>");

// call to the method
wordBreak(n2,dict,str2);

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output**

```
First Test:
i love ice cream and man go
i love ice cream and mango
i love icecream and man go
i love icecream and mango

Second Test:
i love sam sung mobile
i love samsung mobile
```

**复杂性:**

*   **时间复杂度** : O(2 <sup>n</sup> )。因为最坏情况下有 2 个 <sup>n</sup> 组合。
*   **辅助空间** : O(n <sup>2</sup> )。因为在最坏的情况下 wordBreakUtil(…)函数的递归堆栈。

其中 n 是输入字符串的长度。

本文由 [**Raghav Jajodia**](http://jajodiaraghav.me) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。