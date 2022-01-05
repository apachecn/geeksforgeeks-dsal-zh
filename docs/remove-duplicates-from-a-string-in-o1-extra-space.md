# 从 O(1)个额外空间的字符串中删除重复项

> 原文:[https://www . geesforgeks . org/remove-replications-from-in-string-O1-extra-space/](https://www.geeksforgeeks.org/remove-duplicates-from-a-string-in-o1-extra-space/)

给定一个由小写字符组成的字符串 *str* ，任务是删除重复项并返回结果字符串，而不修改原始字符串中的字符顺序。

**示例:**

```
Input: str = "geeksforgeeks"
Output: geksfor

Input: str = "characters"
Output: chartes
```

**方法:**想法是使用*计数器*变量的位来标记字符串中字符的存在。标记“a”的存在，将第 0 位设置为 1，对于“b”，将第 1 位设置为 1，依此类推。如果原始字符串中出现的字符的对应位设置为 0，这意味着它是该字符的第一次出现，因此将其对应位设置为 1，并继续将当前字符包含在结果字符串中。

> **考虑字符串 str = "geeksforgeeks"**
> 
> *   字符:“g”
>     x = 6(g–97 的 ascii)
>     计数器中的第 6 位未置位，导致第一次出现字符“g”。
>     str[0] = 'g'
>     计数器= 00000000000000000000000010000000//将第 6 位标记为已访问
>     长度= 1
> *   字符:“e”
>     x = 4(e–97 的 ascii)
>     计数器中的第 4 位未置位，导致字符“e”首次出现。
>     str[1] = 'e'
>     计数器= 00000000000000000000000001010000//将第 4 位标记为已访问
>     长度= 2
> *   字符:“e”
>     x = 4(e–97 的 ascii)
>     计数器中的第 4 位被设置，导致重复字符。
>     忽略这个人物。移动到下一个字符。
>     计数器= 0000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
> *   字符:“k”
>     x = 10(k–97 的 ascii)
>     计数器中的第 10 位未置位，导致字符“k”首次出现。
>     str[2] = 'k'
>     计数器= 000000000000000000010001010000//将第 10 位标记为已访问
>     长度= 3
> 
> 同样，对所有角色也要这样做。
> **合成字符串:** geksfor(从索引 0 开始的长度为 7 的字符串)

**算法:**

1.  初始化一个计数器变量(跟踪字符串中访问的字符)，它是一个 32 位整数，最初表示为(0000000000000000000000000000000000000000000000000000000000000000000000000000000000000
2.  将“a”视为计数器的第 0 位，“b”视为计数器的第 1 位，“c”视为计数器的第 2 位，依此类推。
3.  遍历输入字符串的每个字符。
4.  获取字符值，其中字符值(x) =字符的 Ascii–97。这将确保“a”的值为 0，“b”的值为 1，依此类推。
5.  检查计数器的第 x 位。
6.  如果计数器的 Xth 位为 0，表示当前字符第一次出现，将当前字符保留在字符串的索引“length”处。
7.  通过设置计数器的 xth 位来标记当前访问的字符。
8.  增加长度。
9.  从索引 0 返回大小为“长度”的子字符串。

下面是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
#include <string>
using namespace std;

// Function to remove duplicates
string removeDuplicatesFromString(string str)
{

    // keeps track of visited characters
    int counter = 0;

    int i = 0;
    int size = str.size();

    // gets character value
    int x;

    // keeps track of length of resultant string
    int length = 0;

    while (i < size) {
        x = str[i] - 97;

        // check if Xth bit of counter is unset
        if ((counter & (1 << x)) == 0) {

            str[length] = 'a' + x;

            // mark current character as visited
            counter = counter | (1 << x);

            length++;
        }
        i++;
    }

    return str.substr(0, length);
}

// Driver code
int main()
{
    string str = "geeksforgeeks";
    cout << removeDuplicatesFromString(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.Arrays;

class GFG {

    // Function to remove duplicates
    static char[] removeDuplicatesFromString(String string)
    {

        // keeps track of visited characters
        int counter = 0;
        char[] str = string.toCharArray();
        int i = 0;
        int size = str.length;

        // gets character value
        int x;

        // keeps track of length of resultant String
        int length = 0;

        while (i < size) {
            x = str[i] - 97;

            // check if Xth bit of counter is unset
            if ((counter & (1 << x)) == 0) {

                str[length] = (char)('a' + x);

                // mark current character as visited
                counter = counter | (1 << x);

                length++;
            }
            i++;
        }

        return Arrays.copyOfRange(str, 0, length);
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "geeksforgeeks";
        System.out.println(removeDuplicatesFromString(str));
    }
}

// This code is contributed by Mithun Kumar
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# Function to remove duplicates
def removeDuplicatesFromString(str2):

    # keeps track of visited characters
    counter = 0;

    i = 0;
    size = len(str2);
    str1 = list(str2);

    # gets character value
    x = 0;

    # keeps track of length of resultant string
    length = 0;

    while (i < size):
        x = ord(str1[i]) - 97;

        # check if Xth bit of counter is unset
        if ((counter & (1 << x)) == 0):
            str1[length] = chr(97 + x);

            # mark current character as visited
            counter = counter | (1 << x);

            length += 1;
        i += 1;

    str2=''.join(str1);
    return str2[0:length];

# Driver code
str1 = "geeksforgeeks";
print(removeDuplicatesFromString(str1));

# This code is contributed by mits
```

## C#

```
// C# implementation of above approach
using System;

class GFG {

    // Function to remove duplicates
    static string removeDuplicatesFromString(string string1)
    {

        // keeps track of visited characters
        int counter = 0;
        char[] str = string1.ToCharArray();
        int i = 0;
        int size = str.Length;

        // gets character value
        int x;

        // keeps track of length of resultant String
        int length = 0;

        while (i < size) {
            x = str[i] - 97;

            // check if Xth bit of counter is unset
            if ((counter & (1 << x)) == 0) {

                str[length] = (char)('a' + x);

                // mark current character as visited
                counter = counter | (1 << x);

                length++;
            }
            i++;
        }

        return (new string(str)).Substring(0, length);
    }

    // Driver code
    static void Main()
    {
        string str = "geeksforgeeks";
        Console.WriteLine(removeDuplicatesFromString(str));
    }
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function to remove duplicates
function removeDuplicatesFromString($str)
{

    // keeps track of visited characters
    $counter = 0;

    $i = 0;
    $size = strlen($str);

    // gets character value
    $x = 0;

    // keeps track of length of resultant string
    $length = 0;

    while ($i < $size)
    {
        $x = ord($str[$i]) - 97;

        // check if Xth bit of counter is unset
        if (($counter & (1 << $x)) == 0)
        {
            $str[$length] = chr(97 + $x);

            // mark current character as visited
            $counter = $counter | (1 << $x);

            $length++;
        }
        $i++;
    }

    return substr($str, 0, $length);
}

// Driver code
$str = "geeksforgeeks";
echo removeDuplicatesFromString($str);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// Javascript implementation of above approach

// Function to remove duplicates
function removeDuplicatesFromString(string)
{
    // keeps track of visited characters
        let counter = 0;
        let str = string.split("");
        let i = 0;
        let size = str.length;

        // gets character value
        let x;

        // keeps track of length of resultant String
        let length = 0;

        while (i < size) {
            x = str[i].charCodeAt(0) - 97;

            // check if Xth bit of counter is unset
            if ((counter & (1 << x)) == 0) {

                str[length] = String.fromCharCode('a'.charCodeAt(0) + x);

                // mark current character as visited
                counter = counter | (1 << x);

                length++;
            }
            i++;
        }

        return str.join("").slice(0,length);
}

// Driver code
let  str = "geeksforgeeks";
document.write(removeDuplicatesFromString(str));

// This code is contributed by patel2127
</script>
```

**Output:** 

```
geksfor
```

**时间复杂度:**O(n)
T3】空间复杂度: O(n) - >因为它使用字符串的 char[]数组来存储字符串的字符(即取决于输入字符串的长度)

**另一种方法:**这种方法通过大小为 256 (所有可能的字符)的**整数数组来跟踪给定输入字符串中的访问字符。
想法如下:**

1.  创建一个大小为 256 的整数数组，以便跟踪所有可能的字符。
2.  迭代输入字符串，对于每个字符:
3.  以字符的 **ASCII** 值为索引查找数组:
    *   如果索引处的值为 0，则将字符复制到原始输入数组中，并增加 endIndex，同时将索引处的值更新为-1。
    *   否则跳过角色。

下面是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Method to remove duplicates
string removeDuplicatesFromString(string str)
{

    // Table to keep track of visited characters
    vector<int> table(256, 0);
    vector<char> chars;

    for(auto i : str)
        chars.push_back(i);

    // To keep track of end index of
    // resultant string
    int endIndex = 0;

    for(int i = 0; i < chars.size(); i++)
    {
        if (table[chars[i]] == 0)
        {
            table[chars[i]] = -1;
            chars[endIndex++] = chars[i];
        }
    }

    string ans = "";

    for(int i = 0; i < endIndex; i++)
        ans += chars[i];

    return ans;
}

// Driver code
int main()
{
    string str = "geeksforgeeks";

    cout << (removeDuplicatesFromString(str))
         << endl;
}

// This code is contributed by Mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java implementation of above approach
import java.util.Arrays;

class GFG {

    // Method to remove duplicates
    static char[] removeDuplicatesFromString(String string)
    {
        //table to keep track of visited characters
        int[] table = new int[256];
        char[] chars = string.toCharArray();

        //to keep track of end index of resultant string
        int endIndex = 0;

        for(int i = 0; i < chars.length; i++)
        {
            if(table[chars[i]] == 0)
            {
                table[chars[i]] = -1;
                chars[endIndex++] = chars[i];
            }
        }

        return Arrays.copyOfRange(chars, 0, endIndex);
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "geeksforgeeks";
        System.out.println(removeDuplicatesFromString(str));
    }
}

// This code is contributed by Sonu Singh
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# Method to remove duplicates
def removeDuplicatesFromString(string):

    # Table to keep track of visited
    # characters
    table = [0 for i in range(256)]

    # To keep track of end index
    # of resultant string
    endIndex = 0
    string = list(string)

    for i in range(len(string)):
        if (table[ord(string[i])] == 0):
            table[ord(string[i])] = -1
            string[endIndex] = string[i]
            endIndex += 1

    ans = ""
    for i in range(endIndex):
      ans += string[i]

    return ans

# Driver code
if __name__ == '__main__':

    temp = "geeksforgeeks"

    print(removeDuplicatesFromString(temp))

# This code is contributed by Kuldeep Singh
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

    // Method to remove duplicates
    static char[] removeDuplicatesFromString(String str)
    {
        // table to keep track of visited characters
        int[] table = new int[256];
        char[] chars = str.ToCharArray();

        // to keep track of end index
        // of resultant string
        int endIndex = 0;

        for(int i = 0; i < chars.Length; i++)
        {
            if(table[chars[i]] == 0)
            {
                table[chars[i]] = -1;
                chars[endIndex++] = chars[i];
            }
        }
        char []newStr = new char[endIndex];
        Array.Copy(chars, newStr, endIndex);
        return newStr;
    }

    // Driver code
    public static void Main(String[] args)
    {
        String str = "geeksforgeeks";
        Console.WriteLine(removeDuplicatesFromString(str));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript implementation of above approach

    // Method to remove duplicates
    function removeDuplicatesFromString(string)
    {
        // table to keep track of visited characters
        let table = new Array(256);
        for(let i=0;i<table.length;i++)
            table[i]=0;
        let chars = string.split("");

        // to keep track of end index of resultant string
        let endIndex = 0;

        for(let i = 0; i < chars.length; i++)
        {
            if(table[chars[i].charCodeAt(0)] == 0)
            {

                table[chars[i].charCodeAt(0)] = -1;
                chars[endIndex++] = chars[i];

            }
        }

         let ans="";
         for(let i=0;i<endIndex;i++)
            ans += chars[i]
        return ans;
    }

    // Driver code
    let str = "geeksforgeeks";
    document.write(removeDuplicatesFromString(str));

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
geksfor
```

**时间复杂度:** O(n)
**空间复杂度:** O(n) - >因为它使用 char[]字符串数组来存储字符串的字符(即取决于输入字符串的长度)
这种方法是由 [**Sonu Singh** 贡献的。](https://auth.geeksforgeeks.org/user/SonuSinghRajput1/articles)