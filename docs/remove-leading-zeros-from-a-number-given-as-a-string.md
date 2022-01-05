# 从作为字符串给出的数字中删除前导零

> 原文:[https://www . geesforgeks . org/从数字中移除前导零-作为字符串给出/](https://www.geeksforgeeks.org/remove-leading-zeros-from-a-number-given-as-a-string/)

给定数字字符串**字符串**，任务是从给定字符串中移除所有的**前导零**。如果包含**的字符串只有零**，那么打印单个**“0”**。

**示例:**

> **输入:** str = "0001234"
> **输出:** 1234
> **解释:**
> 删除前导子串**“000”**将字符串修改为“1234”。
> 因此，最终答案是“1234”。
> 
> **输入:** str = "00000000"
> **输出:** 0
> **说明:**
> 除 0 外没有数字

**天真方法:**
解决这个问题最简单的方法是遍历字符串直到字符串中出现的第一个非零字符，并存储从该索引开始的剩余字符串作为答案。如果遍历整个字符串，则表示字符串中的所有字符都是**‘0’**。对于这种情况，存储**“0”**作为答案。打印最终答案。

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)

**节省空间的方法:**
按照以下步骤使用[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)在恒定空间中解决问题:

*   如下所示创建一个正则表达式来删除前导零

> **regex = "^0+(？！$)"**
> 其中:
> **^0+** 从字符串的**开始匹配**一个**或**多个**零。
> **(？！$)** 是一个**否定前瞻**的表达，其中**“{ content } # x20d；**指绳子的**端**。**

*   使用字符串类的内置 [replaceAll()](https://www.geeksforgeeks.org/java-lang-string-replace-method-java/) 方法，该方法接受两个参数，一个**正则表达式**，一个**替换字符串**。
*   要删除前导零，传递一个**正则表达式**作为**第一参数**和**空字符串**作为**第二参数**。
*   此方法用给定的字符串替换匹配的值。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <iostream>
#include <regex>
using namespace std;

// Function to remove all leading
// zeros from a a given string
void removeLeadingZeros(string str)
{
    // Regex to remove leading
    // zeros from a string
    const regex pattern("^0+(?!$)");

    // Replaces the matched
    // value with given string
    str = regex_replace(str, pattern, "");
    cout << str;
}

// Driver Code
int main()
{
    string str = "0001234";
    removeLeadingZeros(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.util.regex.*;
class GFG
{

    // Function to remove all leading
    // zeros from a a given string
    public static void removeLeadingZeros(String str)
    {

        // Regex to remove leading
        // zeros from a string
        String regex = "^0+(?!$)";

        // Replaces the matched
        // value with given string
        str = str.replaceAll(regex, "");

        System.out.println(str);
    }

    // Driver Code
    public static void main(String args[])
    {
        String str = "0001234";

        removeLeadingZeros(str);
    }
}
```

## 蟒蛇 3

```
# Python3 Program to implement
# the above approach
import re

# Function to remove all leading
# zeros from a a given string
def removeLeadingZeros(str):

    # Regex to remove leading
    # zeros from a string
    regex = "^0+(?!$)"

    # Replaces the matched
    # value with given string
    str = re.sub(regex, "", str)

    print(str)

# Driver Code
str = "0001234"
removeLeadingZeros(str)

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Text.RegularExpressions;

class GFG{

// Function to remove all leading
// zeros from a a given string
public static void removeLeadingZeros(string str)
{

    // Regex to remove leading
    // zeros from a string
    string regex = "^0+(?!$)";

    // Replaces the matched
    // value with given string
    str = Regex.Replace(str, regex, "");

    Console.WriteLine(str);
}

// Driver Code
public static void Main(string[] args)
{
    string str = "0001234";

    removeLeadingZeros(str);
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>
// Javascript Program to implement
// the above approach

// Function to remove all leading
    // zeros from a a given string
function removeLeadingZeros(str)
{
    // Regex to remove leading
        // zeros from a string
        const regex = new RegExp("^0+(?!$)",'g');

        // Replaces the matched
        // value with given string
        str = str.replaceAll(regex, "");

        document.write(str);
}

// Driver Code
let str = "0001234";

removeLeadingZeros(str);

// This code is contributed by unknown2108
</script>
```

**Output**

```
1234
```

***时间复杂度:** O(N)，其中 N 是字符串的长度。*
***辅助空间:** O(1)*

**特定于 Java 的方法:**关于使用 [StringBuffer](https://www.geeksforgeeks.org/stringbuffer-class-in-java/) 的特定于 Java 的方法，请参考[这篇文章](https://www.geeksforgeeks.org/remove-trailing-zeros-string-java/)。