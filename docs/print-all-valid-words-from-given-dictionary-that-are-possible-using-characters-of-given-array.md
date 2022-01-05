# 使用给定数组的字符打印给定词典中所有可能的有效单词

> 原文:[https://www . geeksforgeeks . org/print-所有来自给定字典的有效单词-可能使用给定数组的字符/](https://www.geeksforgeeks.org/print-all-valid-words-from-given-dictionary-that-are-possible-using-characters-of-given-array/)

给定一个字符串字典 **dict[]** 和一个字符数组 **arr[]** 。使用给定字符数组中的字符打印字典中所有可能的有效单词。
**例:**

> **输入:**dict–【“go”、“bat”、“me”、“eat”、“goal”、boy、“run”】
> arr【】=【‘e’、‘o’、‘b’、‘a’、‘m’、‘g’、‘l’】
> **输出:**“go”、“me”、“goal”。
> **说明:**字典中只有这三个字符串的所有字符。
> 
> **输入:**Dict =[“goa”、“诱饵”、“狼狈”、“吃了”、“目标”、“女孩”、“雨”]
> arr[]= ['s '，' o '，' t '，' a '，' e '，' g '，' l '，' I '，' r']
> **输出:**“goa”、“吃了”、“目标”、“女孩”

**做法:**通过查字典每个字符串的字符就可以解决问题。如果一个字符串的所有字符都存在，那么这个字符串就可以形成。按照下面提到的步骤来解决问题。

*   连接所有字符，形成一个字符串。
*   遍历字符串中的每个单词，并查找每个单词的所有字符是否都出现在串联的字符串中。

为了更好地理解，请遵循下图所示。

> **图解:**考虑下面的例子。
> 
> **dict[] = [“走”、“蝙蝠”、“吃”、“肉”、“进球”、“男孩”、“跑”]** 、
> **arr[]=[‘e’、‘o’、‘b’、‘a’、‘m’、‘g’、‘l’]**
> 
> *   串联字符串= e o b a m g l
> *   如果我们穿越“去”
> *   “eobamgl”中的“g”的索引为 5
> *   “eobamgl”中的索引为 1
> *   这意味着所有的索引都存在。因此，我们将打印“开始”
> *   如果有任何索引不存在，那就不包括在内。
> *   同样“我”和“目标”也满足条件。
> 
> 所以输出是“去”、“目标”和“我”。

下面是上述方法的实现。

## C++

```
// C++ code to implement the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the words
void printWord(string str, string s) {
    for (int i = 0; i < str.size(); i++) {
        if (s.find(str[i]) == string::npos) {
            return;
        }
    }
    cout << str << endl;
}

// Function to find the words
void findWord(vector<string> str1, vector<char> str2) {
    string s = "";
    for (int i = 0; i < str2.size(); i++) {
        s += str2[i];
    }
    for (int i = 0; i < str1.size(); i++) {
        printWord(str1[i], s);
    }
}

int main() {
    vector<string> str1 = {"go", "bat", "me", "eat",
                "goal", "boy", "run"};
    vector<char> str2 = {'e', 'o', 'b', 'a', 'm', 'g', 'l'};
    findWord(str1, str2);
    return 0;
}

// This code is contributed by Samim Hossain Mondal.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to implement the above approach
class GFG{

  // Function to print the words
  public static void printWord(String str, String s) {
    for (int i = 0; i < str.length(); i++) {
      if (s.indexOf(str.charAt(i)) < 0) {
        return;
      }
    }
    System.out.println(str);
  }

  // Function to find the words
  public static void findWord(String[] str1, char[] str2) {
    String s = "";
    for (int i = 0; i < str2.length; i++) {
      s += str2[i];
    }
    for (int i = 0; i < str1.length; i++) {
      printWord(str1[i], s);
    }
  }

  public static void main(String args[]) {
    String[] str1 = {"go", "bat", "me", "eat", "goal", "boy", "run"};
    char[] str2 = {'e', 'o', 'b', 'a', 'm', 'g', 'l'};
    findWord(str1, str2);
  }
}

// This code is contributed by Saurabh Jaiswal
```

## 蟒蛇 3

```
# python code to implement the above approach

# Function to print the words
def printWord(str, s):
    for i in range(0, len(str)):
        if (not (str[i] in s)):
            return

    print(str)

# Function to find the words
def findWord(str1, str2):
    s = ""
    for i in str2:
        s += i

    for i in range(0, len(str1)):
        printWord(str1[i], s)

# Driver Code
if __name__ == "__main__":
    str1 = ["go", "bat", "me", "eat", "goal", "boy", "run"]

    str2 = ["e", "o", "b", "a", "m", "g", "l"]

    findWord(str1, str2)

    # This code is contributed by rakeshsahni
```

## java 描述语言

```
<script>
    // JavaScript code to implement the above approach

    // Function to print the words
    function printWord(str, s) {
        for (var i = 0; i < str.length; i++) {
            if (s.indexOf(str[i]) < 0) {
                return;
            }
        }
        document.write(str);
        document.write("<br>");
    }

    // Function to find the words
    function findWord(str1, str2) {
        var s = "";
        for (var i in str2) {
            s += str2[i];
        }
        for (var i = 0; i < str1.length; i++) {
            printWord(str1[i], s);
        }
    }

    var str1 = ["go", "bat", "me", "eat",
                "goal", "boy", "run"];
    var str2 = ["e", "o", "b", "a", "m", "g", "l"];
    findWord(str1, str2);
</script>
```

**输出:**

```
go
me
goal
```

**时间复杂度:** O(N * K)，其中 N 是字典[]的长度，K 是 arr[]的长度。
**辅助空间:** O(1)