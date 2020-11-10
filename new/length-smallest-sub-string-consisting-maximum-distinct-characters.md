# 包含最大不同字符的最小子字符串的长度

> 原文：[https://www.geeksforgeeks.org/length-smallest-sub-string-consisting-maximum-distinct-characters/](https://www.geeksforgeeks.org/length-smallest-sub-string-consisting-maximum-distinct-characters/)

给定一个长度为`N`的字符串，找到由最大不同字符组成的最小子字符串的长度。 注意：我们的输出可以具有相同的字符。

![](img/56dd44ceb89660fa05f6a6b05fa3cda3.png)

**示例**：

```
Input : "AABBBCBB"
Output : 5

Input : "AABBBCBBAC"
Output : 3
Explanation : Sub-string -> "BAC"

Input : "GEEKSGEEKSFOR"
Output : 8
Explanation : Sub-string -> "GEEKSFOR"

```

**方法 1（暴力）**

我们可以一一考虑所有子字符串，然后一起检查每个子字符串的两个条件

1.子字符串的唯一字符等于最大不同字符

2.子字符串的长度应最小。

**时间复杂度**：`O(n ^ 3)`

## C++

```cpp

/* C++ program to find the length of the smallest  
substring consisting of maximum distinct characters */
#include <bits/stdc++.h> 
using namespace std; 

#define NO_OF_CHARS 256 

// Find maximum distinct characters in any string 
int max_distinct_char(string str, int n){ 

    // Initialize all character's count with 0 
    int count[NO_OF_CHARS] = {0}; 

    // Increase the count in array if a character 
    // is found 
    for (int i = 0; i < n;  i++) 
        count[str[i]]++; 

    int max_distinct = 0; 
    for (int i = 0; i < NO_OF_CHARS;  i++) 
        if (count[i] != 0)       
            max_distinct++;      

    return max_distinct; 
} 

int smallesteSubstr_maxDistictChar(string str){ 

    int n = str.size();     // size of given string 

    // Find maximum distinct characters in any string 
    int max_distinct = max_distinct_char(str, n); 
    int minl = n;   // result 

    // Brute force approach to find all substrings 
    for (int i=0 ;i<n ;i++){ 
        for (int j=0; j<n; j++){ 
            string subs =  str.substr(i,j); 
            int subs_lenght = subs.size(); 
            int sub_distinct_char = max_distinct_char(subs, subs_lenght);  

            // We have to check here both conditions together 
            // 1\. substring's distinct characters is equal 
            //    to maximum distinct characters 
            // 2\. substing's length should be minimum  
            if (subs_lenght < minl && max_distinct == sub_distinct_char){ 
                minl = subs_lenght; 
            } 
        } 
    } 
    return minl; 
} 

/* Driver program to test above function */
int main() 
{ 
    // Input String 
    string str = "AABBBCBB"; 

    int len =  smallesteSubstr_maxDistictChar(str); 
    cout << " The length of the smallest substring"
            " consisting of maximum distinct "
            "characters : " << len; 
    return 0; 
} 

```

## Java

```java

/* Java program to find the length of the smallest  
substring consisting of maximum distinct characters */
class GFG { 

    final static int NO_OF_CHARS = 256; 

// Find maximum distinct characters in any string 
    static int max_distinct_char(String str, int n) { 

        // Initialize all character's count with 0 
        int count[] = new int[NO_OF_CHARS]; 

        // Increase the count in array if a character 
        // is found 
        for (int i = 0; i < n; i++) { 
            count[str.charAt(i)]++; 
        } 

        int max_distinct = 0; 
        for (int i = 0; i < NO_OF_CHARS; i++) { 
            if (count[i] != 0) { 
                max_distinct++; 
            } 
        } 

        return max_distinct; 
    } 

    static int smallesteSubstr_maxDistictChar(String str) { 

        int n = str.length();     // size of given string 

        // Find maximum distinct characters in any string 
        int max_distinct = max_distinct_char(str, n); 
        int minl = n;   // result 

        // Brute force approach to find all substrings 
        for (int i = 0; i < n; i++) { 
            for (int j = 0; j < n; j++) { 

                String subs = null; 
                if(i<j) 
                    subs = str.substring(i, j); 
                else
                    subs = str.substring(j, i); 
                int subs_lenght = subs.length(); 
                int sub_distinct_char = max_distinct_char(subs, subs_lenght); 

                // We have to check here both conditions together 
                // 1\. substring's distinct characters is equal 
                //    to maximum distinct characters 
                // 2\. substing's length should be minimum  
                if (subs_lenght < minl && max_distinct == sub_distinct_char) { 
                    minl = subs_lenght; 
                } 
            } 
        } 
        return minl; 
    } 

    /* Driver program to test above function */
    static public void main(String[] args) { 
        // Input String 
        String str = "AABBBCBB"; 

        int len = smallesteSubstr_maxDistictChar(str); 
        System.out.println(" The length of the smallest substring"
                + " consisting of maximum distinct "
                + "characters : "+len); 
    } 
} 

// This code is contributed by 29AjayKumar 

```

## Python 3

```

# Python 3 program to find the length  
# of the smallest substring consisting 
# of maximum distinct characters  
NO_OF_CHARS = 256

# Find maximum distinct characters 
# in any string 
def max_distinct_char(str, n): 

    # Initialize all character's 
    # count with 0 
    count = [0] * NO_OF_CHARS 

    # Increase the count in array  
    # if a character is found 
    for i in range(n): 
        count[ord(str[i])] += 1

    max_distinct = 0
    for i in range(NO_OF_CHARS): 
        if (count[i] != 0): 
            max_distinct += 1    

    return max_distinct 

def smallesteSubstr_maxDistictChar(str): 

    n = len(str)     # size of given string 

    # Find maximum distinct characters 
    # in any string 
    max_distinct = max_distinct_char(str, n) 
    minl = n     # result 

    # Brute force approach to 
    # find all substrings 
    for i in range(n): 
        for j in range(n): 
            subs = str[i:j] 
            subs_lenght = len(subs) 
            sub_distinct_char = max_distinct_char(subs,  
                                                  subs_lenght) 

            # We have to check here both conditions together 
            # 1\. substring's distinct characters is equal 
            # to maximum distinct characters 
            # 2\. substing's length should be minimum  
            if (subs_lenght < minl and 
                max_distinct == sub_distinct_char): 
                minl = subs_lenght 

    return minl 

# Driver Code 
if __name__ == "__main__": 

    # Input String 
    str = "AABBBCBB"

    l = smallesteSubstr_maxDistictChar(str); 
    print( "The length of the smallest substring", 
           "consisting of maximum distinct", 
           "characters :", l) 

# This code is contributed by ChitraNayal 

```

## C#

```cs

/* C# program to find the length of the smallest  
substring consisting of maximum distinct characters */
using System; 

class GFG  
{ 

    static int NO_OF_CHARS = 256; 

    // Find maximum distinct characters in any string 
    static int max_distinct_char(String str, int n)  
    { 

        // Initialize all character's count with 0 
        int []count = new int[NO_OF_CHARS]; 

        // Increase the count in array if a character 
        // is found 
        for (int i = 0; i < n; i++)  
        { 
            count[str[i]]++; 
        } 

        int max_distinct = 0; 
        for (int i = 0; i < NO_OF_CHARS; i++) 
        { 
            if (count[i] != 0)  
            { 
                max_distinct++; 
            } 
        } 

        return max_distinct; 
    } 

    static int smallesteSubstr_maxDistictChar(String str) 
    { 

        int n = str.Length;     // size of given string 

        // Find maximum distinct characters in any string 
        int max_distinct = max_distinct_char(str, n); 
        int minl = n; // result 

        // Brute force approach to find all substrings 
        for (int i = 0; i < n; i++)  
        { 
            for (int j = 0; j < n; j++)  
            { 

                String subs = null; 
                if(i < j) 
                    subs = str.Substring(i, str.Length-j); 
                else
                    subs = str.Substring(j, str.Length-i); 
                int subs_lenght = subs.Length; 
                int sub_distinct_char = max_distinct_char(subs, subs_lenght); 

                // We have to check here both conditions together 
                // 1\. substring's distinct characters is equal 
                // to maximum distinct characters 
                // 2\. substing's length should be minimum  
                if (subs_lenght < minl && max_distinct == sub_distinct_char) 
                { 
                    minl = subs_lenght; 
                } 
            } 
        } 
        return minl; 
    } 

    /* Driver program to test above function */
    static public void Main(String[] args) 
    { 
        // Input String 
        String str = "AABBBCBB"; 

        int len = smallesteSubstr_maxDistictChar(str); 
        Console.WriteLine(" The length of the smallest substring"
                + " consisting of maximum distinct "
                + "characters : "+len); 
    } 
} 

// This code contributed by Rajput-Ji 

```

## PHP

```php

<?php 
/* PHP program to find the length of the smallest  
substring consisting of maximum distinct characters */

$NO_OF_CHARS=256; 

// Find maximum distinct characters in any string 
function max_distinct_char($str, $n) 
{ 
    global $NO_OF_CHARS; 

    // Initialize all character's count with 0 
    $count = array_fill(0, $NO_OF_CHARS, 0); 

    // Increase the count in array if a character 
    // is found 
    for ($i = 0; $i < $n; $i++) 
        $count[ord($str[$i])]++; 

    $max_distinct = 0; 
    for ($i = 0; $i < $NO_OF_CHARS; $i++) 
        if ($count[$i] != 0)      
            $max_distinct++;      

    return $max_distinct; 
} 

function smallesteSubstr_maxDistictChar($str) 
{ 

    $n = strlen($str); // size of given string 

    // Find maximum distinct characters in any string 
    $max_distinct = max_distinct_char($str, $n); 
    $minl = $n; // result 

    // Brute force approach to find all substrings 
    for ($i = 0 ; $i < $n ; $i++) 
    { 
        for ($j = 0; $j < $n; $j++) 
        { 
            $subs = substr($str, $i, $j); 
            $subs_lenght = strlen($subs); 
            $sub_distinct_char = max_distinct_char($subs, $subs_lenght);  

            // We have to check here both conditions together 
            // 1\. substring's distinct characters is equal 
            // to maximum distinct characters 
            // 2\. substing's length should be minimum  
            if ($subs_lenght < $minl &&  
                $max_distinct == $sub_distinct_char) 
            { 
                $minl = $subs_lenght; 
            } 
        } 
    } 
    return $minl; 
} 

/* Driver code */

    // Input String 
    $str = "AABBBCBB"; 

    $len = smallesteSubstr_maxDistictChar($str); 
    echo " The length of the smallest substring"
            ." consisting of maximum distinct characters : ".$len; 

// This coe is contributed by mits 
?> 

```

**输出**：

```
 The length of the smallest substring consisting
 of maximum distinct characters : 5

```

**方法 2（有效）**

1.  计算给定字符串中的所有不同字符。

2.  维护一个字符窗口。 只要窗口包含给定字符串的所有字符，我们就会从左侧缩小窗口以删除多余的字符，然后将其长度与到目前为止的最小窗口大小进行比较。

请参考[包含字符串本身的所有字符的最小窗口](https://www.geeksforgeeks.org/smallest-window-contains-characters-string/)，以获取实现和更多详细信息。

**提问者：DailyHunt**

本文由 **Harshit Agrawal** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

