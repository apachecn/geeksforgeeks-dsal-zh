# 计算在给定字符串

的所有子字符串中出现的元音数量

给定一个长度为 N 的包含 0 个或多个元音的小写字符的字符串，任务是查找在给定字符串的所有子字符串中出现的元音计数。

**示例**：

> **输入**：str =“ abc”
> **输出**：3
> 
> 给定的字符串“ abc”仅包含一个元音='a'
> “ abc”的子字符串为= {“ a”，“ b”，“ c”，“ ab”，“ bc，“ abc”}}
> 因此，这些字符串中元音出现的总和= 3。（“ a”出现 3 次）
> 
> **输入**：str =“ daceh”
> **输出**：16

**天真的方法**：给定长度为 N 的字符串，可以形成的子字符串数= N（N + 1）/ 2。 一个简单的解决方案是针对每个子串，我们计算元音的出现并将其相加以获得结果。 此方法的时间复杂度为 O（N <sup>3</sup> ），不适合大 N 值。

**高效方法**：这个想法是使用基于前缀和数组的技术，在此技术中，我们将每个字符的出现存储在所有串联的子字符串中。

*   For the first character,

    > 没有。 出现次数=否。 以第一个字符= N 开头的子串数。

*   For each of the following characters, we store the

    > 没有。 以该字符 **+** 开头的子串数，其中包含该字符 **的先前字符形成的子串数–** 仅由先前字符形成的子串数。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the above approach 
#include <bits/stdc++.h> 
using namespace std; 

// Returns the total sum of 
// occurrences of all vowels 
int vowel_calc(string s) 
{ 
    int n = s.length(); 
    vector<int> arr; 

    for (int i = 0; i < n; i++) { 

        if (i == 0) 
            // No. of occurrences of 0th character 
            // in all the substrings 
            arr.push_back(n); 

        else
            // No. of occurrences of the ith character 
            // in all the substrings 
            arr.push_back((n - i) + arr[i - 1] - i); 
    } 

    int sum = 0; 
    for (int i = 0; i < n; i++) 

        // Check if ith character is a vowel 
        if (s[i] == 'a' || s[i] == 'e' || s[i] == 'i'
            || s[i] == 'o' || s[i] == 'u') 
            sum += arr[i]; 

    // Return the total sum 
    // of occurrences of vowels 
    return sum; 
} 

// Driver code 
int main() 
{ 
    string s = "daceh"; 
    cout << vowel_calc(s) << endl; 

    return 0; 
} 

```

## Java

```java

// Java implementation of the above approach 

import java.io.*; 
import java.util.*; 

public class Gfg { 

    // Returns the total sum of 
    // occurrences of all vowels 
    static int vowel_calc(String s) 
    { 
        int n = s.length(); 
        int arr[] = new int[n]; 

        for (int i = 0; i < n; i++) { 

            if (i == 0) 
                // No. of occurrences of 0th character 
                // in all the substrings 
                arr[i] = n; 

            else
                // No. of occurrences of ith character 
                // in all the substrings 
                arr[i] = (n - i) + arr[i - 1] - i; 
        } 

        int sum = 0; 
        for (int i = 0; i < n; i++) { 
            char ch = s.charAt(i); 
            // Check if ith character is a vowel 
            if (ch == 'a' || ch == 'e' || ch == 'i'
                || ch == 'o' || ch == 'u') 
                sum += arr[i]; 
        } 

        // Return the total sum 
        // of occurrences of vowels 
        return sum; 
    } 

    // Driver Code 
    public static void main(String args[]) 
    { 
        String s = "daceh"; 
        System.out.println(vowel_calc(s)); 
    } 
} 

```

## Python3

```py

# Python 3 implementation of  
# a more efficient approach. 
# return sum of all occurrences of all vowels 
def sumVowel(string): 
    n = len(string) 
    sum = 0
    string = string.lower() 

    # iterate through every character in the string 
    for i in range(0, n): 
        s = string[i] 

        # checks if the character is a vowel or not 
        if (s=="a" or s == "e" or s == "i" or s == "o" or s == "u"): 

            # uses below expression to calculate the count  
                        # of all occurrences of character in substrings  
                        # of the string 
            sum += ((n - i) * (i + 1))             

    # return the total sum of occurrence 
    return sum

#driver code 
if __name__ == '__main__': 
    #input string here 
    string = "abhay"
    #print returned sum 
    print(sumVowel(string)) 

# This code is contributed by  
# Abhay Subramanian K 

```

## C#

```cs

// C# implementation of the above approach 

using System; 

public class Gfg { 

    // Returns the total sum of 
    // occurrences of all vowels 
    static int vowel_calc(string s) 
    { 
        int n = s.Length; 
        int[] arr = new int[n]; 

        for (int i = 0; i < n; i++) { 

            if (i == 0) 
                // No. of occurrences of 0th character 
                // in all the substrings 
                arr[i] = n; 

            else
                // No. of occurrences of ith character 
                // in all the substrings 
                arr[i] = (n - i) + arr[i - 1] - i; 
        } 

        int sum = 0; 
        for (int i = 0; i < n; i++) { 
            char ch = s[i]; 
            // Check if ith character is a vowel 
            if (ch == 'a' || ch == 'e' || ch == 'i'
                || ch == 'o' || ch == 'u') 
                sum += arr[i]; 
        } 

        // Return the total sum 
        // of occurrences of vowels 
        return sum; 
    } 

    // Driver Code 
    public static void Main() 
    { 
        string s = "daceh"; 
        Console.Write(vowel_calc(s)); 
    } 
} 

```

## PHP

```php

<?php 
// PHP implementation of the above approach 

// Returns the total sum of 
// occurrences of all vowels 
function vowel_calc($s) 
{ 
    $n = strlen($s); 
    $arr = array(); 

    for ($i = 0; $i < $n; $i++) 
    { 
        if ($i == 0) 

            // No. of occurrences of 0th character 
            // in all the substrings 
            $arr[$i] = $n; 

        else

            // No. of occurrences of ith character 
            // in all the substrings  
            $arr[$i] = ($n - $i) + $arr[$i - 1] - $i; 
        } 

    $sum = 0; 
    for ($i = 0; $i < $n; $i++) 
    { 

        // Check if ith character is a vowel 
        if ($s[$i] == 'a' || $s[$i] == 'e' ||  
            $s[$i] == 'i' || $s[$i] == 'o' || 
            $s[$i] == 'u') 
            $sum += $arr[$i]; 
        } 

        // Return the total sum 
        // of occurrences of vowels 
        return $sum; 
    } 

// Driver Code 
$s = "daceh"; 
echo(vowel_calc($s)); 

// This code is contributed by Shivi_Aggarwal 
?> 

```

**Output:**

```
16

```

**时间复杂度**：O（N）

[![competitive-programming-img](img/5211864e7e7a28eeeb039fa5d6073a24.png)](https://practice.geeksforgeeks.org/courses/competitive-programming-live?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_cp)

* * *

* * *



