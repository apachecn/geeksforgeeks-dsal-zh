# 从字符串中拆分数字、字母和特殊符号

> 原文:[https://www . geesforgeks . org/split-numeric-字母-和-special-symbols-from-a-string/](https://www.geeksforgeeks.org/split-numeric-alphabetic-and-special-symbols-from-a-string/)

给定字符串，将字符串分成三部分，一部分包含数字，一部分包含字母，一部分包含特殊字符。

**示例:**

```
Input : geeks01for02geeks03!!!
Output :geeksforgeeks
        010203
        !!!
Here str = "Geeks01for02Geeks03!!!", we scan every character and 
append in res1, res2 and res3 string accordingly.

Input : **Docoding123456789everyday##
Output :Docodingeveryday
        123456789
        **##
```

**步骤:**

1.  计算字符串的长度。
2.  逐个扫描字符串中的每个字符
    *   如果(ch 是一个数字)则将其附加到 res1 字符串中。
    *   否则，如果(ch 是字母)追加到字符串 res2 中。
    *   否则在字符串 res3 中追加。
3.  打印所有字符串，我们将有一个字符串包含一个数字部分，其他非数字部分，最后一个包含特殊字符。

## C++

```
// CPP program to split an alphanumeric
// string using STL
#include<bits/stdc++.h>
using namespace std;

void splitString(string str)
{
    string alpha, num, special;
    for (int i=0; i<str.length(); i++)
    {
        if (isdigit(str[i]))
            num.push_back(str[i]);
        else if((str[i] >= 'A' && str[i] <= 'Z') ||
                (str[i] >= 'a' && str[i] <= 'z'))
            alpha.push_back(str[i]);
        else
            special.push_back(str[i]);
    }

    cout << alpha << endl;
    cout << num << endl;
    cout << special << endl;
}

// Driver code
int main()
{
    string str = "geeks01$for02geeks03!@!!";
    splitString(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program to split an alphanumeric
// string using stringbuffer

class Test
{
    static void splitString(String str)
    {
        StringBuffer alpha = new StringBuffer(),
        num = new StringBuffer(), special = new StringBuffer();

        for (int i=0; i<str.length(); i++)
        {
            if (Character.isDigit(str.charAt(i)))
                num.append(str.charAt(i));
            else if(Character.isAlphabetic(str.charAt(i)))
                alpha.append(str.charAt(i));
            else
                special.append(str.charAt(i));
        }

        System.out.println(alpha);
        System.out.println(num);
        System.out.println(special);
    }

    // Driver method
    public static void main(String args[])
    {
        String str = "geeks01$for02geeks03!@!!";
        splitString(str);
    }
}
```

## 蟒蛇 3

```
# Python 3 program to split an alphanumeric
# string using STL
def splitString(str):

    alpha = ""
    num = ""
    special = ""
    for i in range(len(str)):
        if (str[i].isdigit()):
            num = num+ str[i]
        elif((str[i] >= 'A' and str[i] <= 'Z') or
             (str[i] >= 'a' and str[i] <= 'z')):
            alpha += str[i]
        else:
            special += str[i]

    print(alpha)
    print(num )
    print(special)

# Driver code
if __name__ == "__main__":

    str = "geeks01$for02geeks03!@!!"
    splitString(str)

# This code is contributed by ita_c
```

## C#

```
// C# program to split an alphanumeric
// string using stringbuffer
using System;
using System.Text;

class GFG  {

    // Function ot split string
    static void splitString(string str)
    {
        StringBuilder alpha =
                 new StringBuilder();
        StringBuilder num =
                 new StringBuilder();
        StringBuilder special =
                 new StringBuilder();

        for (int i = 0; i < str.Length; i++)
        {
            if (Char.IsDigit(str[i]))
                num.Append(str[i]);
            else if((str[i] >= 'A' &&
                     str[i] <= 'Z') ||
                     (str[i] >= 'a' &&
                      str[i] <= 'z'))
                alpha.Append(str[i]);
            else
                special.Append(str[i]);
        }

        Console.WriteLine(alpha);
        Console.WriteLine(num);
        Console.WriteLine(special);
    }

    // Driver code
    public static void Main()
    {
        string str = "geeks01$for02geeks03!@!!";
        splitString(str);
    }
}

// This code is contributed by Sam007
```

## java 描述语言

```
<script>
// Javascript program to split an alphanumeric
// string using stringbuffer   

    function splitString(str)
    {
        let alpha = "";
        let num = "";
        let special = "";
        for (let i=0; i<str.length; i++)
        {
            if (!isNaN(String(str[i]) * 1))
                num+=str[i];
            else if((str[i] >= 'A' && str[i] <= 'Z') ||
             (str[i] >= 'a' && str[i] <= 'z'))
                alpha+=str[i];
            else
                special+=str[i];
        }

        document.write(alpha+"<br>");
        document.write(num+"<br>");
        document.write(special+"<br>");
    }

    // Driver method
    let str = "geeks01$for02geeks03!@!!";
    splitString(str);

    // This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
geeksforgeeks
010203
$!@!!
```

上述解决方案的时间复杂度是 O(n)，其中 n 是字符串的长度。