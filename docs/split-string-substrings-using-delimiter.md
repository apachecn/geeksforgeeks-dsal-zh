# 使用分隔符

将字符串拆分为子字符串

> 原文:[https://www . geesforgeks . org/split-string-substrings-using-delimiter/](https://www.geeksforgeeks.org/split-string-substrings-using-delimiter/)

给定字符串和分隔符。根据分隔符拆分字符串，并打印结果子字符串列表。
**例:**

```
Input : str = "geeks;for;geeks"
        d_ch = ';'
Output : geeks
         for
         geeks

Input : str = "##ayush##jauhari####"
        d_ch = '#'
Output : ayush
         jauhari
```

**来源:** [微软 IDC 班加罗尔访谈|第 153 集。](https://www.geeksforgeeks.org/microsoft-idc-bangalore-interview-set-153-o365-team/)

**算法:**

```
splitStrings(str, substr_list, dl)
    Initialize word = ""
    Initialize num = 0
    str = str + dl
    l = str.size

    for i = 0 to l-1
        if str[i] != dl
           word = word + str[i]
        else
           if word.size != 0
               substr_list[num] = word
               num++
           word = ""

    return num
```

该算法将填充数组**substr _ list【】**中的拆分子串，并返回**数**等子串的个数。

## C++

```
// C++ implementation to split string into
// substrings on the basis of delimiter
#include <bits/stdc++.h>
using namespace std;

// function to split string into substrings on the
// basis of delimiter and return the substrings
// after split
vector<string> splitStrings(string str, char dl)
{
    string word = "";

    // to count the number of split strings
    int num = 0;

    // adding delimiter character at the end
    // of 'str'
    str = str + dl;

    // length of 'str'
    int l = str.size();

    // traversing 'str' from left to right
    vector<string> substr_list;
    for (int i = 0; i < l; i++) {

        // if str[i] is not equal to the delimiter
        // character then accumulate it to 'word'
        if (str[i] != dl)
            word = word + str[i];

        else {

            // if 'word' is not an empty string,
            // then add this 'word' to the array
            // 'substr_list[]'
            if ((int)word.size() != 0)
                substr_list.push_back(word);

            // reset 'word'
            word = "";
        }
    }

    // return the splitted strings
    return substr_list;
}

// Driver program to test above
int main()
{
    string str = "geeks;for;geeks";
    char dl = ';';

    vector<string> res = splitStrings(str, dl);
    for (auto x : res)
        cout << x << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to split String into
// substrings on the basis of delimiter
import java.util.*;

class GFG
{

    // function to split String into subStrings
    // on the basis of delimiter and return
    // the subStrings after split
    static Vector<String> splitStrings(String str, char dl)
    {
        String word = "";

        // to count the number of split Strings
        int num = 0;

        // adding delimiter character
        // at the end of 'str'
        str = str + dl;

        // length of 'str'
        int l = str.length();

        // traversing 'str' from left to right
        Vector<String> substr_list = new Vector<String>();
        for (int i = 0; i < l; i++)
        {

            // if str[i] is not equal to the delimiter
            // character then accumulate it to 'word'
            if (str.charAt(i) != dl)
            {
                word = word + str.charAt(i);
            }
            else
            {

                // if 'word' is not an empty String,
                // then add this 'word' to the array
                // 'substr_list[]'
                if ((int) word.length() != 0)
                {
                    substr_list.add(word);
                }

                // reset 'word'
                word = "";
            }
        }

        // return the splitted Strings
        return substr_list;
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "geeks;for;geeks";
        char dl = ';';
        Vector<String> res = splitStrings(str, dl);
        for (String x : res)
        {
            System.out.println(x);
        }
    }
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python 3 implementation to split string
# into substrings on the basis of delimiter

# function to split string into substrings
# on the basis of delimiter and return the
# substrings after split
def splitStrings(st, dl):
    word = ""

    # to count the number of split strings
    num = 0

    # adding delimiter character at
    # the end of 'str'
    st += dl

    # length of 'str'
    l = len(st)

    # traversing 'str' from left to right
    substr_list = []
    for i in range(l):

        # if str[i] is not equal to the
        # delimiter character then accumulate
        # it to 'word'
        if (st[i] != dl):
            word += st[i]

        else:

            # if 'word' is not an empty string,
            # then add this 'word' to the array
            # 'substr_list[]'
            if (len(word) != 0):
                substr_list.append(word)

            # reset 'word'
            word = ""

    # return the splitted strings
    return substr_list

# Driver Code
if __name__ == '__main__':
    str = "geeks;for;geeks"
    dl = ';'

    res = splitStrings(str, dl)
    for x in range(len(res)):
        print(res[x])

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation to split String into
// substrings on the basis of delimiter
using System;
using System.Collections.Generic;

class GFG
{

    // function to split String into subStrings
    // on the basis of delimiter and return
    // the subStrings after split
    static List<String> splitStrings(String str, char dl)
    {
        String word = "";

        // to count the number of split Strings
        int num = 0;

        // adding delimiter character
        // at the end of 'str'
        str = str + dl;

        // length of 'str'
        int l = str.Length;

        // traversing 'str' from left to right
        List<String> substr_list = new List<String>();
        for (int i = 0; i < l; i++)
        {

            // if str[i] is not equal to the delimiter
            // character then accumulate it to 'word'
            if (str[i] != dl)
            {
                word = word + str[i];
            }
            else
            {

                // if 'word' is not an empty String,
                // then add this 'word' to the array
                // 'substr_list[]'
                if ((int) word.Length != 0)
                {
                    substr_list.Add(word);
                }

                // reset 'word'
                word = "";
            }
        }

        // return the splitted Strings
        return substr_list;
    }

    // Driver code
    public static void Main()
    {
        String str = "geeks;for;geeks";
        char dl = ';';
        List<String> res = splitStrings(str, dl);
        foreach (String x in res)
        {
            Console.WriteLine(x);
        }
    }
}

//This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation to split string into
// substrings on the basis of delimiter

// function to split string into substrings on the
// basis of delimiter and return the substrings
// after split
function splitStrings(str, dl)
{
    var word = "";

    // to count the number of split strings
    var num = 0;

    // adding delimiter character at the end
    // of 'str'
    str = str + dl;

    // length of 'str'
    var l = str.length;

    // traversing 'str' from left to right
    var substr_list = [];
    for (var i = 0; i < l; i++) {

        // if str[i] is not equal to the delimiter
        // character then accumulate it to 'word'
        if (str[i] != dl)
            word = word + str[i];

        else {

            // if 'word' is not an empty string,
            // then add this 'word' to the array
            // 'substr_list[]'
            if (word.length != 0)
                substr_list.push(word);

            // reset 'word'
            word = "";
        }
    }

    // return the splitted strings
    return substr_list;
}

// Driver program to test above
var str = "geeks;for;geeks";
var dl = ';';
var res = splitStrings(str, dl);
res.forEach(x => {

    document.write( x + "<br>");
});

</script>
```

**输出:**

```
geeks
for
geeks
```

**时间复杂度:** O(n)，其中 **n** 是给定字符串的长度。