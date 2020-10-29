# 有效地查找字符串中的第一个重复字符，而无需在一次遍历中使用任何其他数据结构

> 原文：[https://www.geeksforgeeks.org/efficiently-find-first-repeated-character-string-without-using-additional-data-structure-one-traversal/](https://www.geeksforgeeks.org/efficiently-find-first-repeated-character-string-without-using-additional-data-structure-one-traversal/)

实现节省空间的算法，以检查字符串中的第一个重复字符，而无需在一次遍历中使用任何其他数据结构。 不允许使用其他数据结构，例如 count 数组，hash 等。

**示例**：

```
Input :  abcfdeacf
Output : char = a, index= 6

```

想法是使用整数变量，并使用其二进制表示形式的位来存储是否存在字符。 通常，整数至少有 32 位，我们只需要存储 26 个字符的存在/不存在。

## C++

```cpp

// Efficiently check First repeated character 
// in C++ program  
#include<bits/stdc++.h> 
using namespace std; 

// Returns -1 if all characters of str are 
// unique. 
// Assumptions : (1) str contains only characters 
//                 from 'a' to 'z' 
//             (2) integers are stored using 32 
//                 bits 
int FirstRepeated(string str) 
{ 
    // An integer to store presence/absence 
    // of 26 characters using its 32 bits. 
    int checker = 0; 

    for (int i = 0; i < str.length(); ++i) 
    { 
        int val = (str[i]-'a'); 

        // If bit corresponding to current 
        // character is already set 
        if ((checker & (1 << val)) > 0) 
            return i; 

        // set bit in checker 
        checker |= (1 << val); 
    } 

    return -1; 
} 

// Driver code 
int main() 
{ 
    string s = "abcfdeacf"; 
    int i=FirstRepeated(s); 
    if (i!=-1) 
        cout <<"Char = "<< s[i] << "   and Index = "<<i; 
    else
        cout << "No repeated Char"; 
    return 0; 
} 

```

## Java

```java

// Efficiently check First repeated character 
// in Java program  
public class First_Repeated_char { 

    static int FirstRepeated(String str) 
    { 
        // An integer to store presence/absence 
        // of 26 characters using its 32 bits. 
        int checker = 0; 

        for (int i = 0; i < str.length(); ++i) 
        { 
            int val = (str.charAt(i)-'a'); 

            // If bit corresponding to current 
            // character is already set 
            if ((checker & (1 << val)) > 0) 
                return i; 

            // set bit in checker 
            checker |= (1 << val); 
        } 

        return -1; 
    } 

    // Driver code 
    public static void main(String args[]) 
    { 
        String s = "abcfdeacf"; 
        int i=FirstRepeated(s); 
        if (i!=-1) 
           System.out.println("Char = "+ s.charAt(i) + "   and Index = "+i); 
        else
            System.out.println( "No repeated Char"); 
    } 
} 
// This code is contributed by Sumit Ghosh 

```

## 蟒蛇

```

# Efficiently check First repeated character 
# in Python  

# Returns -1 if all characters of str are 
# unique. 
# Assumptions : (1) str contains only characters 
#                 from 'a' to 'z' 
##             (2) integers are stored using 32 
##                 bits 
def FirstRepeated(string): 

    # An integer to store presence/absence 
    # of 26 characters using its 32 bits. 
    checker = 0

    pos = 0
    for i in string: 
        val = ord(i) - ord('a'); 

        # If bit corresponding to current 
        # character is already set 
        if ((checker & (1 << val)) > 0): 
            return pos 

        # set bit in checker 
        checker |= (1 << val) 
        pos += 1

    return -1

# Driver code 
string = "abcfdeacf"
i = FirstRepeated(string) 
if i != -1: 
    print "Char = ", string[i], " and Index = ", i; 
else: 
    print "No repeated Char"

# This code is contributed by Sachin Bisht 

```

## C#

```cs

// C# program to Efficiently  
// check First repeated character 
using System; 

public class First_Repeated_char { 

    static int FirstRepeated(string str) 
    { 
        // An integer to store presence/absence 
        // of 26 characters using its 32 bits. 
        int checker = 0; 

        for (int i = 0; i < str.Length; ++i) 
        { 
            int val = (str[i]-'a'); 

            // If bit corresponding to current 
            // character is already set 
            if ((checker & (1 << val)) > 0) 
                return i; 

            // set bit in checker 
            checker |= (1 << val); 
        } 

        return -1; 
    } 

    // Driver code 
    public static void Main() 
    { 
        string s = "abcfdeacf"; 
        int i=FirstRepeated(s); 
        if (i!=-1) 
           Console.WriteLine("Char = " + s[i] + 
                          " and Index = " + i); 
        else
            Console.WriteLine( "No repeated Char"); 
    } 
} 

// This code is contributed by vt_m. 

```

## PHP

```php

<?php  
// Efficiently check First repeated character 
// in PHP program  

// Returns -1 if all characters of str are 
// unique. 
// Assumptions : (1) str contains only characters 
//                     from 'a' to 'z' 
//                 (2) integers are stored using 32 
//                     bits 
function FirstRepeated($str) 
{ 
    // An integer to store presence/absence 
    // of 26 characters using its 32 bits. 
    $checker = 0; 

    for ($i = 0; $i < strlen($str); ++$i) 
    { 
        $val = (ord($str[$i]) - ord('a')); 

        // If bit corresponding to current 
        // character is already set 
        if (($checker & (1 << $val)) > 0) 
            return $i; 

        // set bit in checker 
        $checker |= (1 << $val); 
    } 

    return -1; 
} 

// Driver code 
$s = "abcfdeacf"; 
$i=FirstRepeated($s); 
if ($i!=-1) 
    echo "Char = " . $s[$i] . 
         " and Index = " . $i; 
else
    echo "No repeated Char"; 

// This code is contributed by ita_c 
?> 

```

**Output:**

```
Char = a   and Index = 6

```

**时间复杂度**：`O(n)`

**辅助空间**：O（1）

本文由 **Somesh Awasthi 先生**提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

