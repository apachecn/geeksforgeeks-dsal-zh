# 将字符串更改为新的字符集

> 原文:[https://www . geesforgeks . org/change-string-to-new-character-set/](https://www.geeksforgeeks.org/change-string-to-a-new-character-set/)

给定一个 26 个字母的字符集，它相当于英语字母表的字符集(即 ABCD……。xyz)并充当关系。我们还会得到几个句子，我们必须在给定的新字符集的帮助下翻译它们。

**示例:**

```
New character set : qwertyuiopasdfghjklzxcvbnm
Input : "utta"
Output : geek

Input : "egrt"
Output : code
```

新字符集转换背后的想法是使用哈希。执行新字符集的散列，其中集的元素是索引，其位置将是新的字母值。

**方法 1:**
给定新字符集

1.  第一个字符是 q，在散列过程中，我们将在*索引 q* 处放置‘a’(表示位置)，即(17 <sup>第</sup>)。
2.  散列之后，我们的新字符集是“kvmcnophqrszyijadlegwbuft”。
3.  对于输入“egrt”=
    hash[e-' a ']= c
    hash[g-' a ']= o
    hash[r-' a ']= d
    hash[t-' a ']= e
    对于“egrt”相当于“code”。

## C++

```
// CPP program to change the sentence
// with virtual dictionary 
#include<bits/stdc++.h>
using namespace std;

// Converts str to given character set
void conversion(char charSet[], string &str)
{ 
    int n = str.length();

    // hashing for new character set
    char hashChar[26];
    for (int i = 0; i < 27; i++)    
        hashChar[charSet[i]-'a'] = 'a' + i;    

    // conversion of new character set
    for (int i = 0; i < n; i++)
        str[i] = hashChar[str[i]-'a'];
}

// Driver code
int main()
{
    char charSet[27] = "qwertyuiopasdfghjklzxcvbnm";
    string str = "egrt"; 
    conversion(charSet, str);
    cout << str;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to change the sentence
// with virtual dictionary 
class GFG {

// Converts str to given character set
    static String conversion(char charSet[], String str) {
        int n = str.length();

        // hashing for new character set
        char hashChar[] = new char[26];
        for (int i = 0; i < 26; i++) {
            int ch = Math.abs(charSet[i] - 'a');
            hashChar[ch] = (char) ('a' + i);
        }

        // conversion of new character set
        String s="";
        for (int i = 0; i < n; i++) {
            s += hashChar[str.charAt(i) - 'a'];
        }
        return s;
    }

// Driver code
    public static void main(String[] args) {
        char charSet[] = "qwertyuiopasdfghjklzxcvbnm".toCharArray();
        String str = "egrt";
        str = conversion(charSet, str);
        System.out.println(str);
// This code is contributed by princiRaj1992
    }
}
```

## C#

```
// C# program to change the sentence
// with virtual dictionary 
using System;

class GFG 
{

    // Converts str to given character set
    static String conversion(char []charSet, 
                             String str) 
    {
        int n = str.Length;

        // hashing for new character set
        char []hashChar = new char[26];
        for (int i = 0; i < 26; i++) 
        {
            int ch = Math.Abs(charSet[i] - 'a');
            hashChar[ch] = (char) ('a' + i);
        }

        // conversion of new character set
        String s = "";
        for (int i = 0; i < n; i++) 
        {
            s += hashChar[str[i] - 'a'];
        }
        return s;
    }

    // Driver code
    public static void Main(String[] args) 
    {
        char []charSet = "qwertyuiopasdfghjklzxcvbnm".ToCharArray();
        String str = "egrt";
        str = conversion(charSet, str);
        Console.WriteLine(str);
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// Javascript program to change the sentence
// with virtual dictionary 

// Converts str to given character set
function conversion(charSet, str)
{ 
    var n = str.length;

    // hashing for new character set
    var hashChar = Array(26);
    for (var i = 0; i < 26; i++)    
     {
       var ch = Math.abs(charSet[i].charCodeAt(0)-
        'a'.charCodeAt(0));
        hashChar[ch] = 
        String.fromCharCode('a'.charCodeAt(0) + i);   
} 
    var s = "";

    // conversion of new character set
    for (var i = 0; i < n; i++)
        s += (hashChar[str[i].charCodeAt(0)-'a'.charCodeAt(0)]);
    return s;
}

// Driver code
var charSet = "qwertyuiopasdfghjklzxcvbnm".split('');
var str = "egrt"; 
str = conversion(charSet, str);
document.write( str);

// This code is contributed by importantly.
</script>
```

**输出:**

```
code
```

**近路 2:**
1。初始化两个字符串，一个是实际的字母表，另一个是修改过的。
2。从用户处获取要转换的字符串。
3。检索字符串的第一个元素，在修改后的字母表中找到它的索引(例如:0 代表“q”)。
4。在实际的字母表集合中找到相同索引的元素，并将其与结果字符串连接起来。
5。对输入字符串的所有剩余元素重复上述步骤。
6。返回结果字符串。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to change the sentence
// with virtual dictionary 

class GFG 
{
    static char[] alphabets = "abcdefghijklmnopqrstuvwxyz".toCharArray();

    // function for converting the string
    static String conversion(String charSet, char[] str1)
    {
        String s2 = "";
        for (char i : str1)

            // find the index of each element of the
            // string in the modified set of alphabets
            // replace the element with the one having the
            // same index in the actual set of alphabets
            s2 += alphabets[charSet.indexOf(i)];

        return s2;
    }

    // Driver Code
    public static void main(String[] args)
    {
        String charSet = "qwertyuiopasdfghjklzxcvbnm";
        String str1 = "egrt";
        System.out.print(conversion(charSet, str1.toCharArray()));
    }
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to change the sentence
#  with virtual dictionary 

#function for converting the string
def conversion(charSet,str1):
    s2=""
    for i in str1:
        # find the index of each element of the
        # string in the modified set of alphabets
        # replace the element with the one having the
        # same index in the actual set of alphabets
        s2 += alphabets[charSet.index(i)]

    return s2

# Driver Code
if __name__=='__main__':
    alphabets = "abcdefghijklmnopqrstuvwxyz"
    charSet= "qwertyuiopasdfghjklzxcvbnm"
    str1 = "egrt"
    print(conversion(charSet,str1))

#This code is contributed by PradeepEswar
```

## C#

```
// C# program to change the sentence
// with virtual dictionary 
using System;

class GFG 
{
    static char[] alphabets = "abcdefghijklmnopqrstuvwxyz".ToCharArray();

    // function for converting the string
    static String conversion(String charSet, char[] str1)
    {
        String s2 = "";
        foreach (char i in str1)

            // find the index of each element of the
            // string in the modified set of alphabets
            // replace the element with the one having the
            // same index in the actual set of alphabets
            s2 += alphabets[charSet.IndexOf(i)];

        return s2;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        String charSet = "qwertyuiopasdfghjklzxcvbnm";
        String str1 = "egrt";
        Console.Write(conversion(charSet, str1.ToCharArray()));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
      // JavaScript program to change the sentence
      // with virtual dictionary
      var alphabets = "abcdefghijklmnopqrstuvwxyz".split("");

      // function for converting the string
      function conversion(charSet, str1) {
        var s2 = "";
        str1.forEach((i) => {
          // find the index of each element of the
          // string in the modified set of alphabets
          // replace the element with the one having the
          // same index in the actual set of alphabets
          s2 = s2 + alphabets[charSet.indexOf(i)];
        });
        return s2;
      }

      // Driver Code
      var charSet = "qwertyuiopasdfghjklzxcvbnm";
      var str1 = "egrt";
      document.write(conversion(charSet, str1.split("")));

      // This code is contributed by rdtank.
    </script>
```

**输出:**

```
code
```