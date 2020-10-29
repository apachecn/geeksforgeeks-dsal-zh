# 返回输入字符串

> 原文：[https://www.geeksforgeeks.org/return-maximum-occurring-character-in-the-input-string/](https://www.geeksforgeeks.org/return-maximum-occurring-character-in-the-input-string/)

中出现的最大字符

编写高效的函数以返回输入字符串中出现的最大字符，例如，如果输入字符串为“ test”，则函数应返回“ t”。

 **算法**：

解决此问题的一种显而易见的方法是对输入字符串进行排序，然后遍历排序后的字符串以查找出现次数最多的字符。 让我们看看是否可以对此进行改进。 因此，我们将使用一种称为“哈希”的技术。 这样，当我们遍历字符串时，我们会将每个字符散列为 ASCII 字符数组。

```
Input string = “test”
1: Construct character count array from the input string.
  count['e'] = 1
  count['s'] = 1
  count['t'] = 2

2: Return the index of maximum value in count array (returns ‘t’).

```

通常，ASCII 字符为 256，因此我们将 Hash 数组的大小设为 256。但是，如果我们知道输入字符串的字符值只能从 0 到 127，则可以将 Hash 数组的大小限制为 128。类似地， 有关输入字符串的信息，哈希数组的大小可以限制为 26。

**实施**：

## C++

```cpp

// C++ program to output the maximum occurring character 
// in a string 
#include<bits/stdc++.h> 
#define ASCII_SIZE 256 
using namespace std; 

char getMaxOccuringChar(char* str) 
{ 
    // Create array to keep the count of individual 
    // characters and initialize the array as 0 
    int count[ASCII_SIZE] = {0}; 

    // Construct character count array from the input 
    // string. 
    int len = strlen(str); 
    int max = 0;  // Initialize max count 
    char result;   // Initialize result 

    // Traversing through the string and maintaining 
    // the count of each character 
    for (int i = 0; i < len; i++) { 
        count[str[i]]++; 
        if (max < count[str[i]]) { 
            max = count[str[i]]; 
            result = str[i]; 
        } 
    } 

    return result; 
} 

// Driver program to test the above function 
int main() 
{ 
    char str[] = "sample string"; 
    cout << "Max occurring character is "
         << getMaxOccuringChar(str); 
} 

```

## Java

```java

// Java program to output the maximum occurring character 
// in a string 

public class GFG  
{ 
    static final int ASCII_SIZE = 256; 
    static char getMaxOccuringChar(String str) 
    { 
        // Create array to keep the count of individual 
        // characters and initialize the array as 0 
        int count[] = new int[ASCII_SIZE]; 

        // Construct character count array from the input 
        // string. 
        int len = str.length(); 
        for (int i=0; i<len; i++) 
            count[str.charAt(i)]++; 

        int max = -1;  // Initialize max count 
        char result = ' ';   // Initialize result 

        // Traversing through the string and maintaining 
        // the count of each character 
        for (int i = 0; i < len; i++) { 
            if (max < count[str.charAt(i)]) { 
                max = count[str.charAt(i)]; 
                result = str.charAt(i); 
            } 
        } 

        return result; 
    } 

    // Driver Method 
    public static void main(String[] args) 
    { 
        String str = "sample string"; 
        System.out.println("Max occurring character is " + 
                            getMaxOccuringChar(str)); 
    } 
} 

```

## 蟒蛇

```

# Python program to return the maximum occurring character in the input string 
ASCII_SIZE = 256

def getMaxOccuringChar(str): 
    # Create array to keep the count of individual characters 
    # Initialize the count array to zero 
    count = [0] * ASCII_SIZE 

    # Utility variables 
    max = -1
    c = '' 

    # Traversing through the string and maintaining the count of 
    # each character 
    for i in str: 
        count[ord(i)]+=1; 

    for i in str: 
        if max < count[ord(i)]: 
            max = count[ord(i)] 
            c = i 

    return c 

# Driver program to test the above function 
str = "sample string"
print "Max occurring character is " + getMaxOccuringChar(str) 

# Although this program can be written in atmost 3 lines in Python 
# the above program has been written for a better understanding of 
# the reader 

# Shorter version of the program 
# import collections 
# str = "sample string" 
# print "Max occurring character is " + 
#        collections.Counter(str).most_common(1)[0][0] 

# This code has been contributed by Bhavya Jain 

```

## C#

```cs

// C# program to output the maximum  
// occurring character in a string 
using System; 

class GFG 
{ 
    static int ASCII_SIZE = 256; 

    static char getMaxOccuringChar(String str) 
    { 
        // Create array to keep the count of 
        // individual characters and  
        // initialize the array as 0 
        int []count = new int[ASCII_SIZE]; 

        // Construct character count array 
        // from the input string. 
        int len = str.Length; 
        for (int i = 0; i < len; i++) 
            count[str[i]]++; 

        int max = -1; // Initialize max count 
        char result = ' '; // Initialize result 

        // Traversing through the string and  
        // maintaining the count of each character 
        for (int i = 0; i < len; i++) { 
            if (max < count[str[i]]) { 
                max = count[str[i]]; 
                result = str[i]; 
            } 
        } 

        return result; 
    } 

    // Driver Method 
    public static void Main() 
    { 
        String str = "sample string"; 
        Console.Write("Max occurring character is " + 
                            getMaxOccuringChar(str)); 
    } 
} 

// This code is contributed by Sam007 

```

## PHP

```php

<?php  
// PHP program to output the maximum  
// occurring character in a string  
$ASCII_SIZE = 256;  

function getMaxOccuringChar($str)  
{  
    global $ASCII_SIZE;  

    // Create array to keep the count  
    // of individual characters and  
    // initialize the array as 0  
    $count = array_fill(0, $ASCII_SIZE, NULL);  

    // Construct character count array  
    // from the input string.  
    $len = strlen($str);  
    $max = 0; // Initialize max count  

    // Traversing through the string  
    // and maintaining the count of  
    // each character  
    for ($i = 0; $i < ($len); $i++)  
    {  
        $count[ord($str[$i])]++;  
        if ($max < $count[ord($str[$i])])  
        {  
            $max = $count[ord($str[$i])];  
            $result = $str[$i];  
        }  
    }  

    return $result;  
}  

// Driver Code  
$str = "sample string";  
echo "Max occurring character is " .  
           getMaxOccuringChar($str);  

// This code is contributed by ita_c  
?>  

```

**输出**：

```
Max occurring character is s
```

**时间复杂度**：`O(n)`

**空间复杂度**：`O(1)`—因为我们使用固定空间（哈希数组），而不考虑输入字符串的大小。

**注意**：

如果多个字符具有相同的计数，并且该计数为最大，则该函数将在输入字符串中返回具有最大计数的第一个字符。 例如，如果输入字符串为“ test sample”，则三个字符具有相同且最大计数为两个，即“ t”，“ e”和“ s”，但我们的程序将得到“ t”，因为“ t”在输入字符串中排在首位 。 同样，“ cbbbbccc”的输出为“ c”。

作为上述程序的一种变体，如果要输出“ e”作为输入“测试样本”，请考虑代码的变化，即最大计数的字符且该字符应为最小 ASCII 值。 对于“ cbbbbccc”，输出应为“ b”。 试试看 ！

另外，如果我们可以避免上面的两个循环，您能想到改进吗？ 基本上，您需要弄清楚我们是否可以通过一个循环而不是两个循环来解决相同的问题。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请发表评论。

