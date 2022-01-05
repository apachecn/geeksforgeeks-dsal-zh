# 按顺序打印字符串的所有不同字符(3 种方法)

> 原文:[https://www . geesforgeks . org/print-all-distinct-characters-of-a-string-in-order-3-methods/](https://www.geeksforgeeks.org/print-all-distinct-characters-of-a-string-in-order-3-methods/)

给定一个字符串，找出其中所有不同的(或不重复的)字符。例如，如果输入字符串是“极客为极客”，那么输出应该是“为”，如果输入字符串是“极客测验”，那么输出应该是“GksQuiz”。
不同字符的打印顺序应与它们在输入字符串中出现的顺序相同。
**例:**

```
Input  : Geeks for Geeks
Output : for

Input  : Hello Geeks
Output : HoGks
```

**方法 1(简单:O(n<sup>2</sup>)**
一个简单的解决方法是运行两个循环。从左侧开始穿越。对于每个字符，检查它是否重复。如果字符不重复，增加非重复字符的计数。当计数变为 1 时，返回每个字符。

## C++

```
#include <bits/stdc++.h>
using namespace std;

int main()
{
    string str = "GeeksforGeeks";

    for (int i = 0; i < str.size(); i++)
    {
        int flag = 0;
        for (int j = 0; j < str.size(); j++)
        {
            // checking if two characters are equal
            if (str[i] == str[j] and i != j)
            {
                flag = 1;
                break;
            }
        }
        if (flag == 0)
            cout << str[i];
    }

    return 0;
}

// This code is contributed by umadevi9616
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;

class GFG{

public static void main(String[] args)
{
    String str = "GeeksforGeeks";

    for (int i = 0; i < str.length(); i++)
    {
        int flag = 0;
        for (int j = 0; j < str.length(); j++)
        {
            // checking if two characters are equal
            if (str.charAt(i) == str.charAt(j) && i != j)
            {
                flag = 1;
                break;
            }
        }
        if (flag == 0)
            System.out.print(str.charAt(i));
    }
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
string="GeeksforGeeks"

for i in range(0,len(string)):
    flag=0
    for j in range(0,len(string)):
        #checking if two characters are equal
        if(string[i]==string[j] and i!=j):
            flag=1
            break
    if(flag==0):
        print(string[i],end="")
```

## C#

```
using System;

public class GFG{

public static void Main(String[] args)
{
    String str = "GeeksforGeeks";

    for (int i = 0; i < str.Length; i++)
    {
        int flag = 0;
        for (int j = 0; j < str.Length; j++)
        {
            // checking if two characters are equal
            if (str[i] == str[j] && i != j)
            {
                flag = 1;
                break;
            }
        }
        if (flag == 0)
            Console.Write(str[i]);
    }
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
        var str = "GeeksforGeeks";

        for (var i = 0; i < str.length; i++) {
            var flag = 0;
            for (j = 0; j < str.length; j++) {
                // checking if two characters are equal
                if (str.charAt(i) == str.charAt(j) && i != j) {
                    flag = 1;
                    break;
                }
            }
            if (flag == 0)
                document.write(str.charAt(i));
        }

// This code is contributed by gauravrajput1
</script>
```

**Output**

```
for
```