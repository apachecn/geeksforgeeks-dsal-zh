# 如何找到给定字符串中任意货币符号的索引

> 原文:[https://www . geesforgeks . org/如何找到给定字符串中任何货币符号的索引/](https://www.geeksforgeeks.org/how-to-find-index-of-any-currency-symbols-in-a-given-string/)

给定一个字符串 **txt** ，任务是找到给定字符串中货币符号的索引。
**例:**

> **输入:** txt =“美国的货币符号为{ content } # x201D；
> **输出:** 26
> **解释:**
> 符号$出现在指数 33。
> **输入:** txt =“一美元($)等于 75.70 印度卢比。";
> **输出:** 14

**天真的做法:**
解决问题最简单的做法是做以下几点:

*   创建一组所有货币。
*   遍历字符串，如果在字符串中找到集合中的任何货币符号，则打印其索引。

上述方法需要[辅助空间](https://www.geeksforgeeks.org/g-fact-86/)来存储集合中的所有货币。

**有效方法:**

1.  思路就是用[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)来解决这个问题。
2.  如下所述，创建一个正则表达式来查找字符串中的货币符号:
    regex = "**\ \ p { Sc }**"；
    其中:
    {\\p{Sc}
    代表任何货币符号。
    对于 C++ / Python，我们可以使用 regex = " **\\$|\\ |\\€** "
    其中 regex 检查字符串中是否存在任何给定的货币符号($，，€)。
3.  使用 [Pattern.matcher()](https://www.geeksforgeeks.org/matcher-pattern-method-in-java-with-examples/) 将给定字符串与正则表达式匹配。
4.  打印与给定正则表达式匹配的字符串字符的索引。

下面是上述方法的实现:

## C++

```
// C++ program to find indices of
// currency symbols present in a
// string using regular expression
#include <iostream>
#include <regex>
using namespace std;

// Function to find currency symbol
// in a text using regular expression
void findCurrencySymbol(string text)
{

  // Regex to find any currency
  // symbol in a text
  const regex pattern("\\$|\\£|\\€");
  for (auto it = sregex_iterator(text.begin(), text.end(), pattern);
       it != sregex_iterator(); it++)
  {

      // flag type for determining the matching behavior
      // here it is for matches on 'string' objects
      smatch match;
      match = *it;
      cout << match.str(0) << " - " << match.position(0) << endl;
  }
  return ;
}

// Driver Code
int main()
{
  string txt
      = "$27 - $21.30equal to $5.70";
  findCurrencySymbol(txt);
  return 0;
}

// This code is contributed by yuvraj_chandra
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find indices of
// currency symbols present in a
// string using regular expression
import java.util.regex.*;
class GFG {

    // Function to find currency symbol
    // in a text using regular expression
    public static void findCurrencySymbol(
        String text)
    {

        // Regex to find any currency
        // symbol in a text
        String regex = "\\p{Sc}";

        // Compile the ReGex
        Pattern p = Pattern.compile(
            regex);

        // Find match between the
        // given string and the
        // Regex using Pattern.matcher()
        Matcher m = p.matcher(text);

        // Find the next subsequence
        // of the input subsequence
        // that matches the pattern
        while (m.find()) {

            System.out.println(
                text.charAt(m.start())
                + " - "
                + m.start());
        }
    }
    // Driver Code
    public static void main(String args[])
    {
        String txt = "$27 - $21.30"
                    + "equal to $5.70";
        findCurrencySymbol(txt);
    }
}
```

## 蟒蛇 3

```
# Python program to find indices of
# currency symbols present in a
# string using regular expression
import re

# Function to find currency symbol
# in a text using regular expression
def findCurrencySymbol(text):

    # Regex to find any currency
    # symbol in a text
    regex = "\\$|\\£|\\€"

    for m in re.finditer(regex, text):
        print(text[m.start(0)], "-" ,m.start(0))

# Driver code
txt = "$27 - $21.30equal to $5.70"
findCurrencySymbol(txt)

# This code is contributed by yuvraj_chandra
```

**输出:**

```
$ - 0
$ - 6
$ - 21
```

**时间复杂度:O(N)**

**辅助空间:O(1)**