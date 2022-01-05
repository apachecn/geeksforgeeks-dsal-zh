# 山茶花序列中的字数

> 原文:[https://www . geesforgeks . org/camel case-sequence 中的字数/](https://www.geeksforgeeks.org/number-of-words-in-a-camelcase-sequence/)

CamelCase 是一个或多个单词的序列，具有以下属性:

1.  它是一个或多个由英文字母组成的单词的串联。
2.  第一个单词中的所有字母都是小写的。
3.  对于后面的每个单词，第一个字母是大写的，其余的字母是小写的。

给定一个表示为字符串的 CamelCase 序列。任务是找到 CamelCase 序列中的单词数。
**例:**

```
Input : str = "geeksForGeeks"
Output : 3

Input : str = "iGotAnInternInGeeksForGeeks"
Output : 8
```

**做法:**由于已经知道序列是 CamelCase，所以可以说序列中的字数会比大写字母多一个。

*   从序列的第二个字母迭代到序列的末尾。
*   在第一步迭代中，字数将等于大写字母+1。

以下是上述方法的实现:

## C++

```
// CPP code to find the count of words
// in a CamelCase sequence
#include <bits/stdc++.h>
using namespace std;

// Function to find the count of words
// in a CamelCase sequence
int countWords(string str)
{
    int count = 1;

    for (int i = 1; i < str.length() - 1; i++) {
        if (isupper(str[i]))
            count++;
    }

    return count;
}

// Driver code
int main()
{
    string str = "geeksForGeeks";

    cout << countWords(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find the count of words
// in a CamelCase sequence
class solution
{

// Function to find the count of words
// in a CamelCase sequence
static int countWords(String str)
{
    int count = 1;

    for (int i = 1; i < str.length() - 1; i++) {
        if (str.charAt(i)>=65&&str.charAt(i)<=90)
            count++;
    }

    return count;
}

// Driver code
public static void main(String args[])
{
    String str = "geeksForGeeks";

    System.out.print( countWords(str));

}
}
//contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python code to find the count of words
# in a CamelCase sequence

# Function to find the count of words
# in a CamelCase sequence
def countWords(str):
    count = 1
    for i in range(1, len(str) - 1):
        if (str[i].isupper()):
            count += 1

    return count

# Driver code
str = "geeksForGeeks";
print(countWords(str))

# This code is contributed
# by sahishelangia
```

## C#

```
// C# code to find the count of words
// in a CamelCase sequence
using System;

class GFG
{

// Function to find the count of words
// in a CamelCase sequence
static int countWords(String str)
{
    int count = 1;

    for (int i = 1; i < str.Length - 1; i++)
    {
        if (str[i] >= 65 && str[i] <= 90)
            count++;
    }

    return count;
}

// Driver code
public static void Main(String []args)
{
    String str = "geeksForGeeks";

    Console.Write(countWords(str));

}
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript code to find the count of words
// in a CamelCase sequence

// Function to find the count of words
// in a CamelCase sequence
function countWords(str)
{
    let count = 1;

    for (let i = 1; i < str.length - 1; i++) {
        if (str[i]>= 'A' && str[i]<= 'Z')
            count++;
    }

    return count;
}

// driver program

    let str = "geeksForGeeks";

    document.write( countWords(str));

</script>
```

**Output:** 

```
3
```