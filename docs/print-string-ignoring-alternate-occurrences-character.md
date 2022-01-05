# 通过忽略任何字符的交替出现来打印字符串

> 原文:[https://www . geesforgeks . org/print-string-忽略-交替出现-character/](https://www.geeksforgeeks.org/print-string-ignoring-alternate-occurrences-character/)

给定一个由大写字母和小写字母组成的字符串，任务是打印字符串，并替换掉任何字符(包括空格，并认为大写和小写相同)。
**例:**

```
Input : It is a long day Dear.
Output : It sa longdy ear.
Print first I and then ignore next i.
Similarly print first space then 
ignore next space.

Input : Geeks for geeks
Output : Geks fore
```

问于:[微软](https://www.geeksforgeeks.org/microsoft-interview-experience-set-55-for-software-engineer-2/)T2】

由于我们必须以另一种方式打印字符，因此开始遍历字符串并执行以下两个步骤:-

*   增加哈希表中当前字符的出现次数。
*   检查计数是否为奇数，然后打印当前字符，否则不打印。

## C++

```
// C++ program to print the string in given pattern
#include <bits/stdc++.h>
using namespace std;

// Function to print the string
void printStringAlternate(string str)
{
    unordered_map<char, int> occ;

    // Start traversing the string
    for (int i = 0; i < str.length(); i++) {

        // Convert uppercase to lowercase
        char temp = tolower(str[i]);

        // Increment occurrence count
        occ[temp]++;

        // If count is odd then print the character
        if (occ[temp] & 1)
            cout << str[i];
    }

    cout << endl;
}

// Drivers code
int main()
{
    string str = "Geeks for geeks";
    string str2 = "It is a long day Dear";

    printStringAlternate(str);
    printStringAlternate(str2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the string in given pattern
import java.io.*;

class GFG
{
    // Function to print the string
    static void printStringAlternate(String str)
    {
        int[] occ = new int[122];

        // Convert uppercase to lowercase
        String s = str.toLowerCase();

        // Start traversing the string
        for (int i = 0; i < str.length(); i++)
        {

            char temp = s.charAt(i);

            // Increment occurrence count
            occ[temp]++;

            // If count is odd then print the character
            if (occ[temp]%2 != 0)
                System.out.print(str.charAt(i));
        }
        System.out.println();
    }

    // driver program
    public static void main (String[] args)
    {
        String str1 = "Geeks for geeks";
        String str2 = "It is a long day Dear";
        printStringAlternate(str1);
        printStringAlternate(str2);
    }
}

// Contributed by Pramod Kumar
```

## 蟒蛇 3

```
# Python3 program to print the string
# in given pattern

# Function to print the string
def printStringAlternate(string):

    occ = {}

    # Start traversing the string
    for i in range(0, len(string)):

        # Convert uppercase to lowercase
        temp = string[i].lower()

        # Increment occurrence count
        occ[temp] = occ.get(temp, 0) + 1

        # If count is odd then print the character
        if occ[temp] & 1:
            print(string[i], end = "")

    print()

# Driver code
if __name__ == "__main__":

    string = "Geeks for geeks"
    string2 = "It is a long day Dear"

    printStringAlternate(string)
    printStringAlternate(string2)

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to print the
// string in given pattern
using System;

public class GFG {

    // Function to print the string
    static void printStringAlternate(String str)
    {
        int[] occ = new int[122];

        // Convert uppercase to lowercase
        string s = str.ToLower();

        // Start traversing the string
        for (int i = 0; i < str.Length; i++)
        {

            char temp = s[i];

            // Increment occurrence count
            occ[temp]++;

            // If count is odd then print
            // the character
            if (occ[temp] % 2 != 0)
                Console.Write(str[i]);
        }
        Console.WriteLine();
    }

    // Driver Code
    public static void Main ()
    {
        string str1 = "Geeks for geeks";
        string str2 = "It is a long day Dear";
        printStringAlternate(str1);
        printStringAlternate(str2);
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print the string
// in given pattern

// Function to print the string
function printStringAlternate($str)
{
    $occ = array();

    // Convert uppercase to lowercase
    $s = strtolower($str);

    // Start traversing the string
    for ($i = 0; $i < strlen($str); $i++)
    {

        $temp = $s[$i];

        // Increment occurrence count
        $occ[($temp)]++;

        // If count is odd
        // then print the character
        if ($occ[$temp] % 2 != 0)
            echo($str[$i]);
    }
    echo "\n";
}

// Driver Code
$str1 = "Geeks for geeks";
$str2 = "It is a long day Dear";
printStringAlternate($str1);
printStringAlternate($str2);

// This code is contributed by Code_Mech.
?>
```

## java 描述语言

```
<script>

    // JavaScript program to print the
    // string in given pattern

    // Function to print the string
    function printStringAlternate(str)
    {
        let occ = new Array(122);
        occ.fill(0);

        // Convert uppercase to lowercase
        let s = str.toLowerCase();

        // Start traversing the string
        for (let i = 0; i < str.length; i++)
        {

            let temp = s[i];

            // Increment occurrence count
            occ[temp.charCodeAt()]++;

            // If count is odd then print
            // the character
            if (occ[temp.charCodeAt()] % 2 != 0)
                document.write(str[i]);
        }
        document.write("</br>");
    }

    let str1 = "Geeks for geeks";
    let str2 = "It is a long day Dear";
    printStringAlternate(str1);
    printStringAlternate(str2);

</script>
```

**输出:**

```
Geks fore
It sa longdy ear
```

本文由 [**萨哈布拉**](https://www.facebook.com/sahil.chhabra.965) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。