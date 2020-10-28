# 删除出现 k 次以上的字符

给定一串小写字母，通过删除出现在字符串中 k 次以上的字符来减少它。

**示例**：

```
Input : str = "geeksforgeeks"
        k = 2
Output : for

Input : str = "geeksforgeeks"
        k = 3
Output : gksforgks

```

**方法**：

*   创建一个包含 26 个索引的哈希表，其中第 0 个索引代表“ a”，第 1 个索引代表“ b”，依此类推。 将哈希表初始化为零。

*   遍历字符串并计数增加哈希表中 str [i]字符的频率。

*   现在再次遍历该字符串，并将那些在哈希表中的频率小于 k 的字符追加到新字符串中，并跳过那些看起来大于 k 的字符。

**时间复杂度** – O（N）

下面是上述方法的实现：

## C++

```cpp

// C++ program to reduce the string by 
// removing the characters which 
// appears more than k times 
#include <bits/stdc++.h> 
using namespace std; 

const int MAX_CHAR = 26; 

void removeChars(char arr[], int k) 
{ 
    // Hash table initialised to 0 
    int hash[MAX_CHAR] = { 0 }; 

    // Increment the frequency of the character 
    int n = strlen(arr); 
    for (int i = 0; i < n; ++i)  
        hash[arr[i] - 'a']++;     

    // Next index in reduced string 
    int index = 0; 
    for (int i = 0; i < n; ++i) { 

        // Append the characters which 
        // appears less than k times 
        if (hash[arr[i] - 'a'] < k) { 
           arr[index++] = arr[i]; 
        } 
    } 

    arr[index] = '\0'; 
} 

int main() 
{ 
    char str[] = "geeksforgeeks"; 
    int k = 2; 
    removeChars(str, k); 
    cout << str; 
    return 0; 
} 

```

## Java

```java

// Java program to reduce the string by 
// removing the characters which 
// appears more than k times 
import java.util.*; 
class Solution 
{ 

static final int MAX_CHAR = 26; 

static void removeChars(char arr[], int k) 
{ 
    // Hash table initialised to 0 
    int hash[]=new int[MAX_CHAR]; 

    for (int i = 0; i <MAX_CHAR; ++i) 
    hash[i]=0; 

    // Increment the frequency of the character 
    int n = (arr).length; 
    for (int i = 0; i < n; ++i)  
        hash[arr[i] - 'a']++;     

    // Next index in reduced string 
    int index = 0; 
    for (int i = 0; i < n; ++i) { 

        // Append the characters which 
        // appears less than k times 
        if (hash[arr[i] - 'a'] < k) { 
           arr[index++] = arr[i]; 
        } 
    } 
    for (int i = index; i < n; ++i) 
    arr[i] = ' '; 
} 

public static void main(String args[]) 
{ 
    char str[] = "geeksforgeeks".toCharArray();; 
    int k = 2; 
    removeChars(str, k); 
    System.out.println(String.valueOf( str)); 
} 

} 
//contributed by Arnab Kundu 

```

## Python3

```py

# Python 3 program to reduce the string by 
# removing the characters which 
# appears more than k times 
MAX_CHAR = 26

def removeChars(arr, k): 

    # Hash table initialised to 0 
    hash = [0 for i in range(MAX_CHAR)] 

    # Increment the frequency of the character 
    n = len(arr) 
    for i in range(n): 
        hash[ord(arr[i]) - ord('a')] += 1

    # Next index in reduced string 
    index = 0
    for i in range(n): 

        # Append the characters which 
        # appears less than k times 
        if (hash[ord(arr[i]) - ord('a')] < k): 
            arr[index] = arr[i] 
            index += 1

    arr[index] = ' '

    for i in range(index): 
        print(arr[i], end = '') 

# Driver code 
if __name__ == '__main__': 
    str = "geeksforgeeks"
    str = list(str) 
    k = 2
    removeChars(str, k) 

# This code is contributed by 
# Shashank_Sharma 

```

## C#

```cs

// C# program to reduce the string by  
// removing the characters which  
// appears more than k times  
using System; 
public class Solution{  

    static readonly int MAX_CHAR = 26;  

    static void removeChars(char []arr, int k)  
    {  
        // Hash table initialised to 0  
        int []hash=new int[MAX_CHAR];  

        for (int i = 0; i <MAX_CHAR; ++i)  
        hash[i]=0;  

        // Increment the frequency of the character  
        int n = (arr).Length;  
        for (int i = 0; i < n; ++i)  
            hash[arr[i] - 'a']++;      

        // Next index in reduced string  
        int index = 0;  
        for (int i = 0; i < n; ++i) {  

            // Append the characters which  
            // appears less than k times  
            if (hash[arr[i] - 'a'] < k) {  
            arr[index++] = arr[i];  
            }  
        }  
        for (int i = index; i < n; ++i)  
        arr[i] = ' ';  
    }  

    public static void Main()  
    {  
        char []str = "geeksforgeeks".ToCharArray();;  
        int k = 2;  
        removeChars(str, k);  
        Console.Write(String.Join("",str));  
    }  

}  
// This code is contributed by PrinciRaj1992 

```

## PHP

```php

<?php  
// PHP program to reduce the string by 
// removing the characters which 
// appears more than k times 
$MAX_CHAR = 26; 

function removeChars($arr, $k) 
{ 
    global $MAX_CHAR; 

    // Hash table initialised to 0 
    $hash = array_fill(0, $MAX_CHAR, NULL); 

    // Increment the frequency of  
    // the character 
    $n = strlen($arr); 
    for ($i = 0; $i < $n; ++$i)  
        $hash[ord($arr[$i]) - ord('a')]++;  

    // Next index in reduced string 
    $index = 0; 
    for ($i = 0; $i < $n; ++$i) 
    { 

        // Append the characters which 
        // appears less than k times 
        if ($hash[ord($arr[$i]) - ord('a')] < $k) 
        { 
            $arr[$index++] = $arr[$i]; 
        } 
    } 

    $arr[$index] = ''; 
    for($i = 0; $i < $index; $i++) 
        echo $arr[$i]; 
} 

// Driver Code 
$str = "geeksforgeeks"; 
$k = 2; 
removeChars($str, $k); 

// This code is contributed by ita_c 
?> 

```

**Output:**

```
for

```



* * *

* * *



