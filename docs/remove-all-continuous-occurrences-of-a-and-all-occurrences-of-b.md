# 删除所有连续出现的“a”和所有出现的“b”

> 原文:[https://www . geesforgeks . org/remove-all-continuous-of-a-和-all-of-b/](https://www.geeksforgeeks.org/remove-all-continuous-occurrences-of-a-and-all-occurrences-of-b/)

给定一个字符串 **str** ，任务是移除所有连续出现的 **a** 和所有出现的 **b** 并打印结果字符串。
**举例:**

> **输入:**str = " abcddabcdddabbbaaaaa "
> T3】输出:acddadddda
> “abcddabcdddabbbaaaaa”不会产生“acddaddddaa”，因为删除所需的事件后，字符串将变成“acddaddddaa”，这将产生“acddadcdda”
> **输入:**str = " aacbccdbssaba "
> **输出:**

**方法:**我们初始化一个空的结果字符串。如果当前字符是 **b** 或者当前字符是 **a** 并且结果字符串的最后一个字符也是 **a** ，我们遍历输入字符串，然后忽略该字符，否则将该字符推入结果字符串。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to get the resultant string after
// removing the required occurrences
string removeOccurrences(string str)
{

    // String to store the resultant string
    string res = "";
    for (int i = 0; i < str.size(); i++) {

        // If 'a' appeared more than once continuously
        if (str[i] == 'a' && res.back() == 'a')

            // Ignore the character
            continue;

        // Ignore all 'b' characters
        else if (str[i] == 'b')
            continue;

        // Characters that will be included
        // in the resultant string
        res = res + str[i];
    }
    return res;
}

// Driver code
int main()
{
    string str = "abcddabcddddabbbaaaaaa";
    cout << removeOccurrences(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java implementation of the approach
class solution
{
// Function to get the resultant String after
// removing the required occurrences
static String removeOccurrences(String str)
{

    // String to store the resultant String
    String res = "";
    for (int i = 0; i < str.length(); i++) {

        // If 'a' appeared more than once continuously
        if (str.charAt(i) == 'a' && (res.length()==0?' ':res.charAt(res.length()-1)) == 'a')

            // Ignore the character
            continue;

        // Ignore all 'b' characters
        else if (str.charAt(i) == 'b')
            continue;

        // Characters that will be included
        // in the resultant String
        res = res + str.charAt(i);
    }
    return res;
}

// Driver code
public static void main(String args[])
{
    String str = "abcddabcddddabbbaaaaaa";
    System.out.println(removeOccurrences(str));
}
}
//contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to get the resultant string
# after removing the required occurrences
def removeOccurrences(str) :

    # String to store the resultant string
    res = ""
    for i in range(len(str)) :

        # If 'a' appeared more than
        # once continuously
        if (res) :

            if (str[i] == 'a' and res[-1] == 'a') :

                # Ignore the character
                continue

            # Ignore all 'b' characters
            elif (str[i] == 'b') :
                continue

            else :
                # Characters that will be included
                # in the resultant string
                res += str[i]

        else :

            if (str[i] == 'a' ) :
                res += str[i]

            # Ignore all 'b' characters
            elif (str[i] == 'b') :
                continue

            else :
                # Characters that will be included
                # in the resultant string
                res += str[i]

    return res

# Driver code
if __name__ == "__main__" :

    str = "abcddabcddddabbbaaaaaa"
    print(removeOccurrences(str))

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to get the resultant String after
// removing the required occurrences
static String removeOccurrences(String str)
{

    // String to store the resultant String
    String res = "";
    for (int i = 0; i < str.Length; i++)
    {

        // If 'a' appeared more than once continuously
        if (str[i] == 'a' && (res.Length==0?' ':
                        res[res.Length-1]) == 'a')

            // Ignore the character
            continue;

        // Ignore all 'b' characters
        else if (str[i] == 'b')
            continue;

        // Characters that will be included
        // in the resultant String
        res = res + str[i];
    }
    return res;
}

// Driver code
public static void Main(String []args)
{
    String str = "abcddabcddddabbbaaaaaa";
    Console.WriteLine(removeOccurrences(str));
}
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to get the resultant String after
// removing the required occurrences
function removeOccurrences(str)
{

    // String to store the resultant String
    var res = "";
    for (var i = 0; i < str.length; i++) {

        // If 'a' appeared more than once continuously
        if (str.charAt(i) == 'a' &&
        (res.length==0?' ':res.charAt(res.length-1)) == 'a')

            // Ignore the character
            continue;

        // Ignore all 'b' characters
        else if (str.charAt(i) == 'b')
            continue;

        // Characters that will be included
        // in the resultant String
        res = res + str.charAt(i);
    }
    return res;
}

// Driver code
var str = "abcddabcddddabbbaaaaaa";
document.write(removeOccurrences(str));

// This code contributed by Princi Singh

</script>
```

**Output:** 

```
acddacdddda
```