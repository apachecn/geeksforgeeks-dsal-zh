# 按排序顺序重新排列一个字符串，后跟整数和

> 原文:[https://www . geeksforgeeks . org/rearray-a-string-in-sorted-order-后跟整数 sum/](https://www.geeksforgeeks.org/rearrange-a-string-in-sorted-order-followed-by-the-integer-sum/)

给定一个包含大写字母和整数数字(从 0 到 9)的字符串，任务是按照数字总和后面的顺序打印字母。

**示例:**

```
Input : AC2BEW3
Output : ABCEW5
Alphabets in the lexicographic order 
followed by the sum of integers(2 and 3).
```

```
Implementation:
1- Start traversing the given string.
   a) If an alphabet comes increment its
      occurrence count into a hash_table.
   b) If an integer comes then store it 
      separately by summing up everytime.
2- Using hash_table append all the 
   characters first into a string and 
   then at the end, append the integers 
   sum.
3- Return the resultant string.
```

## C++

```
// C++ program for above implementation
#include<bits/stdc++.h>
using namespace std;
const int MAX_CHAR = 26;

// Function to return string in lexicographic
// order followed by integers sum
string arrangeString(string str)
{
    int char_count[MAX_CHAR] = {0};
    int sum = 0;

    // Traverse the string
    for (int i = 0; i < str.length(); i++)
    {
        // Count occurrence of uppercase alphabets
        if (str[i]>='A' && str[i] <='Z')
            char_count[str[i]-'A']++;

        //Store sum of integers
        else
            sum = sum + (str[i]-'0');
    }

    string res = "";

    // Traverse for all characters A to Z
    for (int i = 0; i < MAX_CHAR; i++)
    {
        char ch = (char)('A'+i);

        // Append the current character
        // in the string no. of times it
        //  occurs in the given string
        while (char_count[i]--)
            res = res + ch;
    }

    // Append the sum of integers
    if (sum > 0)
        res = res + to_string(sum);

    // return resultant string
    return res;
}

// Driver program
int main()
{
    string str = "ACCBA10D2EW30";
    cout << arrangeString(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above implementation

class Test
{
    static final int MAX_CHAR = 26;

    // Method to return string in lexicographic
    // order followed by integers sum
    static String arrangeString(String str)
    {
        int char_count[] = new int[MAX_CHAR];
        int sum = 0;

        // Traverse the string
        for (int i = 0; i < str.length(); i++)
        {
            // Count occurrence of uppercase alphabets
            if (Character.isUpperCase(str.charAt(i)))
                char_count[str.charAt(i)-'A']++;

            //Store sum of integers
            else
                sum = sum + (str.charAt(i)-'0');

        }

        String res = "";

        // Traverse for all characters A to Z
        for (int i = 0; i < MAX_CHAR; i++)
        {
            char ch = (char)('A'+i);

            // Append the current character
            // in the string no. of times it
            //  occurs in the given string
            while (char_count[i]-- != 0)
                res = res + ch;
        }

        // Append the sum of integers
        if (sum > 0)
            res = res + sum;

        // return resultant string
        return res;
    }

    // Driver method
    public static void main(String args[])
    {
        String str = "ACCBA10D2EW30";
        System.out.println(arrangeString(str));
    }
}
```

## 蟒蛇 3

```
# Python3 program for above implementation
MAX_CHAR = 26

# Function to return string in lexicographic
# order followed by integers sum
def arrangeString(string):
    char_count = [0] * MAX_CHAR
    s = 0

    # Traverse the string
    for i in range(len(string)):

        # Count occurrence of uppercase alphabets
        if string[i] >= "A" and string[i] <= "Z":
            char_count[ord(string[i]) - ord("A")] += 1

        # Store sum of integers
        else:
            s += ord(string[i]) - ord("0")

    res = ""

    # Traverse for all characters A to Z
    for i in range(MAX_CHAR):
        ch = chr(ord("A") + i)

        # Append the current character
        # in the string no. of times it
        # occurs in the given string
        while char_count[i]:
            res += ch
            char_count[i] -= 1

    # Append the sum of integers
    if s > 0:
        res += str(s)

    # return resultant string
    return res

# Driver code
if __name__ == "__main__":
    string = "ACCBA10D2EW30"
    print(arrangeString(string))

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program for above implementation
using System;

class GFG {

    static int MAX_CHAR = 26;

    // Method to return string in lexicographic
    // order followed by integers sum
    static String arrangeString(string str)
    {
        int []char_count = new int[MAX_CHAR];
        int sum = 0;

        // Traverse the string
        for (int i = 0; i < str.Length; i++)
        {

            // Count occurrence of uppercase
            // alphabets
            if (char.IsUpper(str[i]))
                char_count[str[i]-'A']++;

            //Store sum of integers
            else
                sum = sum + (str[i]-'0');

        }

        string res = "";

        // Traverse for all characters A to Z
        for (int i = 0; i < MAX_CHAR; i++)
        {
            char ch = (char)('A' + i);

            // Append the current character
            // in the string no. of times it
            // occurs in the given string
            while (char_count[i]-- != 0)
                res = res + ch;
        }

        // Append the sum of integers
        if (sum > 0)
            res = res + sum;

        // return resultant string
        return res;
    }

    // Driver method
    public static void Main()
    {
        string str = "ACCBA10D2EW30";
        Console.Write(arrangeString(str));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for above implementation

$MAX_CHAR = 26;

// Function to return string in lexicographic
// order followed by integers sum
function arrangeString($str)
{
    global $MAX_CHAR;
    $char_count = array_fill(0, $MAX_CHAR, NULL);
    $sum = 0;

    // Traverse the string
    for ($i = 0; $i < strlen($str); $i++)
    {
        // Count occurrence of uppercase alphabets
        if ($str[$i] >= 'A' && $str[$i] <= 'Z')
            $char_count[ord($str[$i]) -    
                        ord('A')]++;

        // Store sum of integers
        else
            $sum = $sum + (ord($str[$i]) -
                           ord('0'));
    }

    $res = "";

    // Traverse for all characters A to Z
    for ($i = 0; $i < $MAX_CHAR; $i++)
    {
        $ch = chr(ord('A') + $i);

        // Append the current character
        // in the string no. of times it
        // occurs in the given string
        while ($char_count[$i]--)
            $res = $res . $ch;
    }

    // Append the sum of integers
    if ($sum > 0)
        $res = $res . strval($sum);

    // return resultant string
    return $res;
}

// Driver Code
$str = "ACCBA10D2EW30";
echo arrangeString($str);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>

// Javascript program for above implementation

    let MAX_CHAR = 26;

    // Method to return string in lexicographic
    // order followed by integers sum
    function arrangeString(str)
    {
        let char_count = new Array(MAX_CHAR);
        for(let i=0;i<MAX_CHAR;i++)
        {
            char_count[i]=0;
        }
        let sum = 0;

        // Traverse the string
        for (let i = 0; i < str.length; i++)
        {
            // Count occurrence of uppercase alphabets
            if (str[i] >= "A" && str[i] <= "Z")
                char_count[str[i].charCodeAt(0)-
                'A'.charCodeAt(0)]++;

            //Store sum of integers
            else
                sum = sum + (str[i].charCodeAt(0)-
                '0'.charCodeAt(0));

        }

        let res = "";

        // Traverse for all characters A to Z
        for (let i = 0; i < MAX_CHAR; i++)
        {
            let ch =
            String.fromCharCode('A'.charCodeAt(0)+i);

            // Append the current character
            // in the string no. of times it
            //  occurs in the given string
            while (char_count[i]-- != 0)
                res = res + ch;
        }

        // Append the sum of integers
        if (sum > 0)
            res = res + sum;

        // return resultant string
        return res;
    }

     // Driver method
    let str = "ACCBA10D2EW30";
    document.write(arrangeString(str));

    // This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
AABCCDEW6
```

**时间复杂度:** O(n)
**参考:**
[https://www.careercup.com/question?id=13382661](https://www.careercup.com/question?id=13382661)
本文由 [**萨哈布拉**](https://www.facebook.com/sahil.chhabra.965) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。