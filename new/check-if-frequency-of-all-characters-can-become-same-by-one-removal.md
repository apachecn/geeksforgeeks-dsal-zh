# 检查一次删除后所有字符的频率是否可以相同

> 原文：[https://www.geeksforgeeks.org/check-if-frequency-of-all-characters-can-become-same-by-one-removal/](https://www.geeksforgeeks.org/check-if-frequency-of-all-characters-can-become-same-by-one-removal/)

给定一个包含较低字母字符的字符串，我们需要从该字符串中删除最多一个字符，以使该字符串中每个不同字符的频率相同。

**示例**：

> **输入**：str =“ xyyz”
> **输出**：是
> 我们可以从
> 字符串上方删除字符 y，以使每个
> 的频率 性格相同。
> 
> **输入**：str =“ xyyzz”
> **输出**：是
> 我们可以从
> 字符串上方删除字符“ x”以使每个
> 的频率 性格相同。
> 
> **输入**：str =“ xxxxyyzz”
> **输出**：否
> 仅通过最移开
> 不可能使
> 的每个字符的频率相同 字符串上方一个字符。

**方法**：可以使用[散列](http://www.geeksforgeeks.org/hashing-data-structure/)的概念解决问题。 在此问题中要观察的主要问题是，此处的字符位置无关紧要，因此我们将计算字符的出现频率，如果所有字符都相同，那么我们就完成了操作，无需删除任何字符来产生频率 相同的字符，否则我们可以一遍遍地遍历所有字符，并将它们的频率降低一遍，如果所有频率都相同，那么我们将标记为最多可以去除一个字符并且如果频率不匹配，可以使字符频率相同 那么我们将再次增加该频率并循环其他字符。

以下是上述方法的模拟：

![](img/28bff1b907df67d599cd102a0acec929.png)

下面是上述方法的实现：

## C++

```cpp

// C++ program to get same frequency character 
// string by removal of at most one char 
#include <bits/stdc++.h> 
using namespace std; 
#define M 26 

// Utility method to get index of character ch 
// in lower alphabet characters 
int getIdx(char ch) 
{ 
    return (ch - 'a'); 
} 

// Returns true if all non-zero elements 
// values are same 
bool allSame(int freq[], int N) 
{ 
    int same; 

    // get first non-zero element 
    int i; 
    for (i = 0; i < N; i++) { 
        if (freq[i] > 0) { 
            same = freq[i]; 
            break; 
        } 
    } 

    // check equality of each element with variable same 
    for (int j = i + 1; j < N; j++) 
        if (freq[j] > 0 && freq[j] != same) 
            return false; 

    return true; 
} 

// Returns true if we can make all character 
// frequencies same 
bool possibleSameCharFreqByOneRemoval(string str) 
{ 
    int l = str.length(); 

    // fill frequency array 
    int freq[M] = { 0 }; 
    for (int i = 0; i < l; i++) 
        freq[getIdx(str[i])]++; 

    // if all frequencies are same, then return true 
    if (allSame(freq, M)) 
        return true; 

    /*  Try decreasing frequency of all character 
        by one and then    check all equality of all 
        non-zero frequencies */
    for (char c = 'a'; c <= 'z'; c++) { 
        int i = getIdx(c); 

        // Check character only if it occurs in str 
        if (freq[i] > 0) { 
            freq[i]--; 

            if (allSame(freq, M)) 
                return true; 
            freq[i]++; 
        } 
    } 

    return false; 
} 

// Driver code to test above methods 
int main() 
{ 
    string str = "xyyzz"; 
    if (possibleSameCharFreqByOneRemoval(str)) 
        cout << "Yes"; 
    else
        cout << "No"; 
} 

```

## Java

```java

// Java program to get same frequency character 
// string by removal of at most one char 
public class GFG { 

    static final int M = 26; 

    // Utility method to get index of character ch 
    // in lower alphabet characters 
    static int getIdx(char ch) 
    { 
        return (ch - 'a'); 
    } 

    // Returns true if all non-zero elements 
    // values are same 
    static boolean allSame(int freq[], int N) 
    { 
        int same = 0; 

        // get first non-zero element 
        int i; 
        for (i = 0; i < N; i++) { 
            if (freq[i] > 0) { 
                same = freq[i]; 
                break; 
            } 
        } 

        // check equality of each element with 
        // variable same 
        for (int j = i + 1; j < N; j++) 
            if (freq[j] > 0 && freq[j] != same) 
                return false; 

        return true; 
    } 

    // Returns true if we can make all character 
    // frequencies same 
    static boolean possibleSameCharFreqByOneRemoval(String str) 
    { 
        int l = str.length(); 

        // fill frequency array 
        int[] freq = new int[M]; 

        for (int i = 0; i < l; i++) 
            freq[getIdx(str.charAt(i))]++; 

        // if all frequencies are same, then return true 
        if (allSame(freq, M)) 
            return true; 

        /*  Try decreasing frequency of all character 
            by one and then check all equality of all 
            non-zero frequencies */
        for (char c = 'a'; c <= 'z'; c++) { 
            int i = getIdx(c); 

            // Check character only if it occurs in str 
            if (freq[i] > 0) { 
                freq[i]--; 

                if (allSame(freq, M)) 
                    return true; 
                freq[i]++; 
            } 
        } 

        return false; 
    } 

    // Driver code to test above methods 
    public static void main(String args[]) 
    { 
        String str = "xyyzz"; 
        if (possibleSameCharFreqByOneRemoval(str)) 
            System.out.println("Yes"); 
        else
            System.out.println("No"); 
    } 
} 
// This code is contributed by Sumit Ghosh 

```

## Python 3

```

# Python3 program to get same frequency character  
# string by removal of at most one char 
M = 26

# Utility method to get index of character ch  
# in lower alphabet characters  
def getIdx(ch): 
    return (ord(ch) - ord('a')) 

# Returns true if all non-zero elements  
# values are same  
def allSame(freq, N): 

    # get first non-zero element  
    for i in range(0, N): 
        if(freq[i] > 0): 
            same = freq[i] 
            break

    # check equality of each element  
    # with variable same      
    for j in range(i + 1, N): 
        if(freq[j] > 0 and freq[j] != same): 
            return False

    return True

# Returns true if we can make all  
# character frequencies same  
def possibleSameCharFreqByOneRemoval(str1): 
    l = len(str1) 

    # fill frequency array 
    freq = [0] * M 
    for i in range(0, l): 
        freq[getIdx(str1[i])] += 1

    # if all frequencies are same,  
    # then return true  
    if(allSame(freq, M)): 
        return True

    # Try decreasing frequency of all character  
    # by one and then check all equality of all  
    # non-zero frequencies  
    for i in range(0, 26): 

        # Check character only if it  
        # occurs in str  
        if(freq[i] > 0): 
            freq[i] -= 1

            if(allSame(freq, M)): 
                return True
            freq[i] += 1

    return False

# Driver code 
if __name__ == "__main__": 
    str1 = "xyyzz"
    if(possibleSameCharFreqByOneRemoval(str1)): 
        print("Yes") 
    else: 
        print("No") 

# This code is contributed by Sairahul099 

```

## C#

```cs

// C# program to get same frequency 
// character string by removal of 
// at most one char 
using System; 

class GFG { 
    static int M = 26; 

    // Utility method to get 
    // index of character ch 
    // in lower alphabet characters 
    static int getIdx(char ch) 
    { 
        return (ch - 'a'); 
    } 

    // Returns true if all 
    // non-zero elements 
    // values are same 
    static bool allSame(int[] freq, 
                        int N) 
    { 
        int same = 0; 

        // get first non-zero element 
        int i; 
        for (i = 0; i < N; i++) { 
            if (freq[i] > 0) { 
                same = freq[i]; 
                break; 
            } 
        } 

        // check equality of 
        // each element with 
        // variable same 
        for (int j = i + 1; j < N; j++) 
            if (freq[j] > 0 && freq[j] != same) 
                return false; 

        return true; 
    } 

    // Returns true if we 
    // can make all character 
    // frequencies same 
    static bool possibleSameCharFreqByOneRemoval(string str) 
    { 
        int l = str.Length; 

        // fill frequency array 
        int[] freq = new int[M]; 

        for (int i = 0; i < l; i++) 
            freq[getIdx(str[i])]++; 

        // if all frequencies are same, 
        // then return true 
        if (allSame(freq, M)) 
            return true; 

        /* Try decreasing frequency of all  
            character by one and then check  
            all equality of all non-zero  
            frequencies */
        for (char c = 'a'; c <= 'z'; c++) { 
            int i = getIdx(c); 

            // Check character only if 
            // it occurs in str 
            if (freq[i] > 0) { 
                freq[i]--; 

                if (allSame(freq, M)) 
                    return true; 
                freq[i]++; 
            } 
        } 

        return false; 
    } 

    // Driver code 
    public static void Main() 
    { 
        string str = "xyyzz"; 
        if (possibleSameCharFreqByOneRemoval(str)) 
            Console.Write("Yes"); 
        else
            Console.Write("No"); 
    } 
} 

// This code is contributed 
// by ChitraNayal 

```

## PHP

```php

<?php  
// PHP program to get same frequency  
// character string by removal of at  
// most one char 
$M = 26; 

// Utility method to get index  
// of character ch in lower  
// alphabet characters 
function getIdx($ch) 
{ 
    return ($ch - 'a'); 
} 

// Returns true if all  
// non-zero elements 
// values are same 
function allSame(&$freq, $N) 
{ 
    // get first non-zero element 
    for ($i = 0; $i < $N; $i++) 
    { 
        if ($freq[$i] > 0) 
        { 
            $same = $freq[$i]; 
            break; 
        } 
    } 

    // check equality of each 
    // element with variable same 
    for ($j = $i + 1; $j < $N; $j++) 
        if ($freq[$j] > 0 &&  
            $freq[$j] != $same) 
            return false; 

    return true; 
} 

// Returns true if we 
// can make all character 
// frequencies same 
function possibleSameCharFreqByOneRemoval($str) 
{ 
    global $M; 
    $l = strlen($str); 

    // fill frequency array 
    $freq = array_fill(0, $M, NULL); 
    for ($i = 0; $i < $l; $i++) 
        $freq[getIdx($str[$i])]++; 

    // if all frequencies are same,  
    // then return true 
    if (allSame($freq, $M)) 
        return true; 

    /* Try decreasing frequency of all  
        character by one and then check  
        all equality of all non-zero  
        frequencies */
    for ($c = 'a'; $c <= 'z'; $c++) 
    { 
        $i = getIdx($c); 

        // Check character only  
        // if it occurs in str 
        if ($freq[$i] > 0) 
        { 
            $freq[$i]--; 

            if (allSame($freq, $M)) 
                return true; 
            $freq[$i]++; 
        } 
    } 

    return false; 
} 

// Driver code 
$str = "xyyzz"; 
if (possibleSameCharFreqByOneRemoval($str)) 
echo "Yes"; 
else
echo "No"; 

// This code is contributed  
// by ChitraNayal 
?> 

```

**Output:**

```
Yes

```

**时间复杂度**：O（n）假设字母大小恒定。

本文由 **[Utkarsh Trivedi](https://in.linkedin.com/in/utkarsh-trivedi-253069a7)** 贡献。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

