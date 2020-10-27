# 允许以排列排列形成回文的最小插入量

给定一串小写字母。 查找要插入字符串中的最小字符，使其可以成为回文。 我们可以更改字符串中字符的位置。

**示例：**

```
Input : geeksforgeeks
Output : 2
geeksforgeeks can be changed as:
geeksroforskeeg
geeksorfroskeeg
and many more

Input : aabbc
Output : 0
aabbc can be changed as:
abcba
bacab

```

回文字符串只能在字符串的长度为奇数时才具有一个奇数字符，否则所有字符均出现偶数次。 因此，我们必须找到字符串中出现奇数次的字符。

这个想法是计算字符串中每个字符的出现。 由于回文串可以有一个出现奇数次的字符，因此插入数将比出现奇数次的字符数少一个。 如果字符串已经是回文，我们不需要添加任何字符，因此结果将为 0。

## C ++

```

// CPP program to find minimum number 
// of insertions to make a string 
// palindrome 
#include <bits/stdc++.h> 
using namespace std; 

// Function will return number of 
// characters to be added 
int minInsertion(string str) 
{ 
    // To store string length 
    int n = str.length(); 

    // To store number of characters 
    // occurring odd number of times 
    int res = 0; 

    // To store count of each 
    // character 
    int count[26] = { 0 }; 

    // To store occurrence of each 
    // character 
    for (int i = 0; i < n; i++) 
        count[str[i] - 'a']++; 

    // To count characters with odd 
    // occurrence 
    for (int i = 0; i < 26; i++) 
        if (count[i] % 2 == 1) 
            res++; 

    // As one character can be odd return 
    // res - 1 but if string is already 
    // palindrome return 0 
    return (res == 0) ? 0 : res - 1; 
} 

// Driver program 
int main() 
{ 
    string str = "geeksforgeeks"; 
    cout << minInsertion(str); 

    return 0; 
} 

```

## 爪哇

```

// Java program to find minimum number 
// of insertions to make a string 
// palindrome 
public class Palindrome { 

    // Function will return number of 
    // characters to be added 
    static int minInsertion(String str) 
    { 
        // To store string length 
        int n = str.length(); 

        // To store number of characters 
        // occurring odd number of times 
        int res = 0; 

        // To store count of each 
        // character 
        int[] count = new int[26]; 

        // To store occurrence of each 
        // character 
        for (int i = 0; i < n; i++) 
            count[str.charAt(i) - 'a']++; 

        // To count characters with odd 
        // occurrence 
        for (int i = 0; i < 26; i++) { 
            if (count[i] % 2 == 1) 
                res++; 
        } 

        // As one character can be odd return 
        // res - 1 but if string is already 
        // palindrome return 0 
        return (res == 0) ? 0 : res - 1; 
    } 

    // Driver program 
    public static void main(String[] args) 
    { 
        String str = "geeksforgeeks"; 
        System.out.println(minInsertion(str)); 
    } 
} 

```

## Python3

```

# Python3 program to find minimum number 
# of insertions to make a string 
# palindrome 
import math as mt 

# Function will return number of 
# characters to be added 
def minInsertion(tr1): 

    # To store str1ing length 
    n = len(str1) 

    # To store number of characters 
    # occurring odd number of times 
    res = 0

    # To store count of each 
    # character 
    count = [0 for i in range(26)] 

    # To store occurrence of each 
    # character 
    for i in range(n): 
        count[ord(str1[i]) - ord('a')] += 1

    # To count characters with odd 
    # occurrence 
    for i in range(26): 
        if (count[i] % 2 == 1): 
            res += 1

    # As one character can be odd return 
    # res - 1 but if str1ing is already 
    # palindrome return 0 
    if (res == 0): 
        return 0
    else: 
        return res - 1

# Driver Code 
str1 = "geeksforgeeks"
print(minInsertion(str1)) 

# This code is contributed by  
# Mohit kumar 29 

```

## C＃

```

// C# program to find minimum number 
// of insertions to make a string 
// palindrome 
using System; 

public class GFG { 

    // Function will return number of 
    // characters to be added 
    static int minInsertion(String str) 
    { 

        // To store string length 
        int n = str.Length; 

        // To store number of characters 
        // occurring odd number of times 
        int res = 0; 

        // To store count of each 
        // character 
        int[] count = new int[26]; 

        // To store occurrence of each 
        // character 
        for (int i = 0; i < n; i++) 
            count[str[i] - 'a']++; 

        // To count characters with odd 
        // occurrence 
        for (int i = 0; i < 26; i++) { 
            if (count[i] % 2 == 1) 
                res++; 
        } 

        // As one character can be odd 
        // return res - 1 but if string 
        // is already palindrome 
        // return 0 
        return (res == 0) ? 0 : res - 1; 
    } 

    // Driver program 
    public static void Main() 
    { 
        string str = "geeksforgeeks"; 

        Console.WriteLine(minInsertion(str)); 
    } 
} 

// This code is contributed by vt_m. 

```

## 的 PHP

```

<?php 
// PHP program to find minimum number 
// of insertions to make a string 
// palindrome 

// Function will return number of 
// characters to be added 
function minInsertion($str) 
{ 
    // To store string length 
    $n = strlen($str); 

    // To store number of characters 
    // occurring odd number of times 
    $res = 0; 

    // To store count of each 
    // character 
    $count = array(26); 

    // To store occurrence of each 
    // character 
    for ($i = 0; $i < $n; $i++) 
        $count[ord($str[$i]) - ord('a')]++; 

    // To count characters with odd 
    // occurrence 
    for ($i = 0; $i < 26; $i++) 
    { 
        if ($count[$i] % 2 == 1) 
            $res++; 
    } 

    // As one character can be odd return 
    // res - 1 but if string is already 
    // palindrome return 0 
    return ($res == 0) ? 0 : $res - 1; 
} 

// Driver program 
$str = "geeksforgeeks"; 
echo(minInsertion($str)); 

// This code is contributed  
// by Mukul Singh 
?> 

```

**输出：**

```
2

```

本文由 **[核](https://www.facebook.com/nuclode)** 贡献。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

注意读者！ 现在不要停止学习。 通过 [**DSA 自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的 DSA 概念，并为行业做好准备。