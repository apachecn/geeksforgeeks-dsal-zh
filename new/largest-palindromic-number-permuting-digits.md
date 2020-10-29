# 按排列数字排列的最大回文数

> 原文：[https://www.geeksforgeeks.org/largest-palindromic-number-permuting-digits/](https://www.geeksforgeeks.org/largest-palindromic-number-permuting-digits/)

给定 N（非常大），任务是打印通过排列 N 的数字获得的最大回文数。如果不可能生成回文数，则打印适当的消息。

**示例**：

```
Input : 313551
Output : 531135
Explanations : 531135 is the largest number 
which is a palindrome, 135531, 315513 and other 
numbers can also be formed but we need the highest 
of all of the palindromes. 

Input : 331
Output : 313

Input : 3444
Output : Pallindrome cannot be formed 

```

**天真的方法**：**天真的**方法将尝试所有可能的[排列](https://www.geeksforgeeks.org/print-all-palindrome-permutations-of-a-string/)，并打印出此类组合中最大的一个回文。

**有效方法**：一种有效方法是使用**贪婪算法。** 由于数字较大，因此请将数字存储在字符串中。 将给定数字中每个数字的出现次数存储在地图中。 [检查是否可能形成回文。](https://www.geeksforgeeks.org/check-characters-given-string-can-rearranged-form-palindrome/) 如果可以将给定数字的数字重新排列以形成回文，则可以使用贪婪方法获得该数字。 检查是否存在每个数字（9 到 0），并将每个可用数字放在前面和后面。 **最初，前指针将在索引 0 处，因为最大的数字将被放在第一位，以使数字大。** 每执行一步，将前指针向前移动 1 个位置。 如果该数字出现奇数次，则将**一位放在偶数位数的中间和其余部分**的前面和后面。 保持重复**（map [digit] / 2）**一次的次数。 在前面和后面放置偶数次的特定数字后，将前指针向前移动一级。 放置完成直到 map [digit]为 0。char 数组将贪婪地完成数字放置后，将具有最大的回文数。

在最坏的情况下，如果数字在每个位置都包含相同的数字，则时间复杂度将为 **O（10 *（字符串的长度/ 2））**。

下面是上述想法的实现：

## C++

```cpp

// CPP program to print the largest palindromic 
// number by permuting digits of a number 
#include <bits/stdc++.h> 
using namespace std; 

// function to check if a number can be 
// permuted to form a palindrome number 
bool possibility(unordered_map<int, int> m, 
                 int length, string s) 
{ 
    // counts the occurrence of number which is odd 
    int countodd = 0; 
    for (int i = 0; i < length; i++) { 

        // if occurrence is odd 
        if (m[s[i] - '0'] & 1) 
            countodd++; 

        // if number exceeds 1 
        if (countodd > 1) 
            return false; 
    } 

    return true; 
} 

// function to print the largest palindromic number 
// by permuting digits of a number 
void largestPalindrome(string s) 
{ 

    // string length 
    int l = s.length(); 

    // map that marks the occurrence of a number 
    unordered_map<int, int> m; 
    for (int i = 0; i < l; i++) 
        m[s[i] - '0']++; 

    // check the possibility of a palindromic number 
    if (possibility(m, l, s) == false) { 
        cout << "Palindrome cannot be formed"; 
        return; 
    } 

    // string array that stores the largest 
    // permuted palindromic number 
    char largest[l]; 

    // pointer of front 
    int front = 0; 

    // greedily start from 9 to 0 and place the 
    // greater number in front and odd in the 
    // middle 
    for (int i = 9; i >= 0; i--) { 

        // if the occurrence of number is odd 
        if (m[i] & 1) { 

            // place one odd occurring number 
            // in the middle 
            largest[l / 2] = char(i + 48); 

            // decrease the count 
            m[i]--; 

            // place the rest of numbers greedily 
            while (m[i] > 0) { 
                largest[front] = char(i + 48); 
                largest[l - front - 1] = char(i + 48); 
                m[i] -= 2; 
                front++; 
            } 
        } 
        else { 

            // if all numbers occur even times, 
            // then place greedily 
            while (m[i] > 0) { 

                // place greedily at front 
                largest[front] = char(i + 48); 
                largest[l - front - 1] = char(i + 48); 

                // 2 numbers are placed, so decrease the count 
                m[i] -= 2; 

                // increase placing position 
                front++; 
            } 
        } 
    } 

    // print the largest string thus formed 
    for (int i = 0; i < l; i++) 
        cout << largest[i]; 
} 

// Driver Code 
int main() 
{ 
    string s = "313551"; 
    largestPalindrome(s); 
    return 0; 
} 

```

## Python3

```py

# Python3 program to print the largest palindromic  
# number by permuting digits of a number  
from collections import defaultdict 

# Function to check if a number can be  
# permuted to form a palindrome number  
def possibility(m, length, s):  

    # counts the occurrence of  
    # number which is odd  
    countodd = 0
    for i in range(0, length):  

        # if occurrence is odd  
        if m[int(s[i])] & 1:  
            countodd += 1

        # if number exceeds 1  
        if countodd > 1:  
            return False

    return True

# Function to print the largest palindromic  
# number by permuting digits of a number  
def largestPalindrome(s):  

    # string length  
    l = len(s)  

    # map that marks the occurrence of a number  
    m = defaultdict(lambda:0) 
    for i in range(0, l):  
        m[int(s[i])] += 1

    # check the possibility of a  
    # palindromic number  
    if possibility(m, l, s) == False: 
        print("Palindrome cannot be formed")  
        return

    # string array that stores the largest  
    # permuted palindromic number  
    largest = [None] * l  

    # pointer of front  
    front = 0

    # greedily start from 9 to 0 and place the  
    # greater number in front and odd in the middle  
    for i in range(9, -1, -1):  

        # if the occurrence of number is odd  
        if m[i] & 1: 

            # place one odd occurring number  
            # in the middle  
            largest[l // 2] = chr(i + 48)  

            # decrease the count  
            m[i] -= 1

            # place the rest of numbers greedily  
            while m[i] > 0:  
                largest[front] = chr(i + 48)  
                largest[l - front - 1] = chr(i + 48)  
                m[i] -= 2
                front += 1

        else: 

            # if all numbers occur even times,  
            # then place greedily  
            while m[i] > 0:  

                # place greedily at front  
                largest[front] = chr(i + 48)  
                largest[l - front - 1] = chr(i + 48)  

                # 2 numbers are placed,  
                # so decrease the count  
                m[i] -= 2

                # increase placing position  
                front += 1

    # print the largest string thus formed  
    for i in range(0, l):  
        print(largest[i], end = "")  

# Driver Code  
if __name__ == "__main__":  

    s = "313551"
    largestPalindrome(s)  

# This code is contributed by Rituraj Jain 

```

## C#

```cs

// C# program to print the largest  
// palindromic number by permuting 
// digits of a number  
using System; 
using System.Collections.Generic;  

class GFG{ 

// Function to check if a number can be 
// permuted to form a palindrome number 
static bool possibility(Dictionary<int, int> m, 
                        int length, string s) 
{ 

    // Counts the occurrence of number 
    // which is odd 
    int countodd = 0; 

    for(int i = 0; i < length; i++) 
    { 

        // If occurrence is odd 
        if ((m[s[i] - '0'] & 1) != 0) 
            countodd++; 

        // If number exceeds 1 
        if (countodd > 1) 
            return false; 
    } 
    return true; 
} 

// Function to print the largest palindromic 
// number by permuting digits of a number 
static void largestPalindrome(string s) 
{ 

    // string length 
    int l = s.Length; 

    // Map that marks the occurrence of a number 
    Dictionary<int,  
               int> m = new Dictionary<int, 
                                       int>(); 

    for(int i = 0; i < 10; i++) 
        m[i] = 0; 

    for(int i = 0; i < l; i++) 
        m[s[i] - '0']++; 

    // Check the possibility of a 
    // palindromic number 
    if (possibility(m, l, s) == false) 
    { 
        Console.Write("Palindrome cannot be formed"); 
        return; 
    } 

    // string array that stores the largest 
    // permuted palindromic number 
    char []largest = new char[l]; 

    // Pointer of front 
    int front = 0; 

    // Greedily start from 9 to 0 and place the 
    // greater number in front and odd in the 
    // middle 
    for(int i = 9; i >= 0; i--) 
    { 

        // If the occurrence of number is odd 
        if ((m[i] & 1) != 0)  
        { 

            // Place one odd occurring number 
            // in the middle 
            largest[l / 2] = (char)(i + '0'); 

            // Decrease the count 
            m[i]--; 

            // Place the rest of numbers greedily 
            while (m[i] > 0) 
            { 
                largest[front] = (char)(i + '0'); 
                largest[l - front - 1] = (char)(i + '0'); 
                m[i] -= 2; 
                front++; 
            } 
        } 
        else 
        { 

            // If all numbers occur even times, 
            // then place greedily 
            while (m[i] > 0) 
            { 

                // Place greedily at front 
                largest[front] = (char)(i + '0'); 
                largest[l - front - 1] = (char)(i + '0'); 

                // 2 numbers are placed, so  
                // decrease the count 
                m[i] -= 2; 

                // Increase placing position 
                front++; 
            } 
        } 
    } 

    // Print the largest string thus formed 
    for(int i = 0; i < l; i++) 
    { 
        Console.Write(largest[i]); 
    } 
} 

// Driver Code 
public static void Main(string[] args) 
{ 
    string s = "313551"; 

    largestPalindrome(s); 
} 
} 

// This code is contributed by rutvik_56 

```

**Output:**

```
531135

```

**时间复杂度**：`O(n)`，其中 n 是字符串的长度。



* * *

* * *



