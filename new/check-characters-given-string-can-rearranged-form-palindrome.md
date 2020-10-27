# 检查给定字符串的字符是否可以重新排列以形成回文

给定字符串，请检查给定字符串的字符是否可以重新排列以形成回文。
例如，可以重新排列“ geeksogeeks”的字符以形成回文“ geeksoskeegeg”，但是不能重新排列“ geeksforgeeks”的字符以形成回文。

如果最多一个字符出现奇数次而所有字符出现偶数次，则一组字符可以形成回文。

一个简单的解决方案是运行两个循环，外循环一个接一个地拾取所有字符，内循环计算被拾取字符的出现次数。 我们跟踪奇数。 该解决方案的时间复杂度为 O（n <sup>2</sup> ）。

我们可以使用 count 数组在 O（n）时间内完成此操作。 以下是详细步骤。
1）创建一个字母大小的计数数组，通常为 256。将计数数组的所有值初始化为 0。
2）遍历给定的字符串并递增每个字符的计数。
3）遍历计数数组，如果计数数组具有多个奇数，则返回 false。 否则返回 true。

下面是上述方法的实现。

## C++

```cpp

// C++ implementation to check if 
// characters of a given string can 
// be rearranged to form a palindrome 
#include<bits/stdc++.h> 
using namespace std; 
#define NO_OF_CHARS 256 

/* function to check whether characters of a string can form  
   a palindrome */
bool canFormPalindrome(string str) 
{ 
    // Create a count array and initialize all  
    // values as 0 
    int count[NO_OF_CHARS] = {0}; 

    // For each character in input strings, 
    // increment count in the corresponding 
    // count array 
    for (int i = 0; str[i];  i++) 
        count[str[i]]++; 

    // Count odd occurring characters 
    int odd = 0; 
    for (int i = 0; i < NO_OF_CHARS; i++) 
    { 
        if (count[i] & 1) 
            odd++; 

        if (odd > 1) 
            return false; 
    } 

    // Return true if odd count is 0 or 1,  
    return true; 
} 

/* Driver program*/
int main() 
{ 
  canFormPalindrome("geeksforgeeks")? cout << "Yes\n":  
                                     cout << "No\n"; 
  canFormPalindrome("geeksogeeks")? cout << "Yes\n":  
                                    cout << "No\n"; 
  return 0; 
} 

```

## Java

```java

// Java implementation to check if 
// characters of a given string can 
// be rearranged to form a palindrome 
import java.io.*; 
import java.util.*; 
import java.math.*; 

class GFG { 

static int NO_OF_CHARS = 256; 

    /* function to check whether characters  
    of a string can form a palindrome */
    static boolean canFormPalindrome(String str) { 

    // Create a count array and initialize all 
    // values as 0 
    int count[] = new int[NO_OF_CHARS]; 
    Arrays.fill(count, 0); 

    // For each character in input strings, 
    // increment count in the corresponding 
    // count array 
    for (int i = 0; i < str.length(); i++) 
    count[(int)(str.charAt(i))]++; 

    // Count odd occurring characters 
    int odd = 0; 
    for (int i = 0; i < NO_OF_CHARS; i++)  
    { 
    if ((count[i] & 1) == 1) 
        odd++; 

    if (odd > 1) 
        return false; 
    } 

    // Return true if odd count is 0 or 1, 
    return true; 
} 

// Driver program 
public static void main(String args[]) 
{ 
    if (canFormPalindrome("geeksforgeeks")) 
    System.out.println("Yes"); 
    else
    System.out.println("No"); 

    if (canFormPalindrome("geeksogeeks")) 
    System.out.println("Yes"); 
    else
    System.out.println("No"); 
} 
} 

// This code is contributed by Nikita Tiwari. 

```

## Python3

```py

# Python3 implementation to check if 
# characters of a given string can 
# be rearranged to form a palindrome 

NO_OF_CHARS = 256

# function to check whether characters 
# of a string can form a palindrome  
def canFormPalindrome(st) : 

    # Create a count array and initialize   
    # all values as 0 
    count = [0] * (NO_OF_CHARS) 

    # For each character in input strings, 
    # increment count in the corresponding 
    # count array 
    for i in range( 0, len(st)) : 
        count[ord(st[i])] = count[ord(st[i])] + 1

    # Count odd occurring characters 
    odd = 0

    for i in range(0, NO_OF_CHARS ) : 
        if (count[i] & 1) : 
            odd = odd + 1

        if (odd > 1) : 
            return False

    # Return true if odd count is 0 or 1,  
    return True

# Driver program 
if(canFormPalindrome("geeksforgeeks")) : 
    print("Yes") 
else : 
    print("No") 

if(canFormPalindrome("geeksogeeks")) : 
    print("Yes") 
else : 
    print("No") 

# This code is contributed by Nikita Tiwari. 

```

## C#

```cs

// C# implementation to check if 
// characters of a given string can 
// be rearranged to form a palindrome 

using System; 

class GFG { 

static int NO_OF_CHARS = 256; 

    /* function to check whether characters  
    of a string can form a palindrome */
    static bool canFormPalindrome(string str) { 

    // Create a count array and initialize all 
    // values as 0 
    int[] count = new int[NO_OF_CHARS]; 
    Array.Fill(count, 0); 

    // For each character in input strings, 
    // increment count in the corresponding 
    // count array 
    for (int i = 0; i < str.Length; i++) 
    count[(int)(str[i])]++; 

    // Count odd occurring characters 
    int odd = 0; 
    for (int i = 0; i < NO_OF_CHARS; i++)  
    { 
    if ((count[i] & 1) == 1) 
        odd++; 

    if (odd > 1) 
        return false; 
    } 

    // Return true if odd count is 0 or 1, 
    return true; 
} 

// Driver program 
public static void Main() 
{ 
    if (canFormPalindrome("geeksforgeeks")) 
    Console.WriteLine("Yes"); 
    else
    Console.WriteLine("No"); 

    if (canFormPalindrome("geeksogeeks")) 
    Console.WriteLine("Yes"); 
    else
    Console.WriteLine("No"); 
} 
} 

```

**Output:**

```
No
Yes
```

本文由 Abhishek 提供。 如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请发表评论。

**另一种方法**：

我们可以使用列表在 O（n）时间内完成此操作。 以下是详细步骤。
1）创建一个字符列表。
2）遍历给定的字符串。
3）对于字符串中的每个字符，如果列表中已经包含其他字符，请删除该字符，否则添加到列表中。
3）如果字符串长度为偶数，则列表应该为空。
4）或如果字符串长度为奇数，则列表大小应为 1。
5）在上述两个条件（3）或（4）中返回 true，否则返回 false。

## C++

```cpp

#include<bits/stdc++.h> 
using namespace std; 

/* 
* function to check whether characters of  
a string can form a palindrome 
*/
bool canFormPalindrome(string str) 
{ 

    // Create a list 
    vector<char> list; 

    // For each character in input strings, 
    // remove character if list contains 
    // else add character to list 
    for (int i = 0; i < str.length(); i++) 
    { 
        auto pos = find(list.begin(), list.end(), str[i]); 
        if (pos != list.end()) 
        { 
            auto posi = find(list.begin(), list.end(),str[i]); 
            list.erase(posi); 
        } 
        else
            list.push_back(str[i]); 
    } 

    // if character length is even list is expected to be empty 
    // or if character length is odd list size is expected to be 1 
    if (str.length() % 2 == 0 && list.empty() // if string length is even 
        || (str.length() % 2 == 1 && list.size() == 1)) // if string length is odd 
        return true; 
    else
        return false; 

} 

// Driver program 
int main()  
{ 
    if (canFormPalindrome("geeksforgeeks")) 
        cout << ("Yes") << endl; 
    else
        cout << ("No") << endl; 

    if (canFormPalindrome("geeksogeeks")) 
        cout << ("Yes") << endl; 
    else
        cout << ("No") << endl; 
} 

// This code is contributed by Rajput-Ji 

```

## Java

```java

import java.util.ArrayList; 
import java.util.List; 

class GFG{ 

    /* 
     * function to check whether characters of a string can form a palindrome 
     */
    static boolean canFormPalindrome(String str) { 

        // Create a list 
        List<Character> list = new ArrayList<Character>(); 

        // For each character in input strings, 
        // remove character if list contains 
        // else add character to list 
        for (int i = 0; i < str.length(); i++) { 
            if (list.contains(str.charAt(i))) 
                list.remove((Character) str.charAt(i)); 
            else
                list.add(str.charAt(i)); 
        } 

        // if character length is even list is expected to be empty 
        // or if character length is odd list size is expected to be 1 
        if (str.length() % 2 == 0 && list.isEmpty() // if string length is even 
                || (str.length() % 2 == 1 && list.size() == 1)) // if string length is odd 
            return true; 
        else
            return false; 

    } 

    // Driver program 
    public static void main(String args[]) { 
        if (canFormPalindrome("geeksforgeeks")) 
            System.out.println("Yes"); 
        else
            System.out.println("No"); 

        if (canFormPalindrome("geeksogeeks")) 
            System.out.println("Yes"); 
        else
            System.out.println("No"); 
    } 
} 

// This code is contributed by Sugunakumar P 

```

## Python3

```py

''' 
* function to check whether characters of  
a strring can form a palindrome 
'''
def canFormPalindrome(strr): 

    # Create a listt 
    listt = [] 

    # For each character in input strrings, 
    # remove character if listt contains 
    # else add character to listt 
    for i in range(len(strr)): 
        if (strr[i] in listt): 
            listt.remove(strr[i]) 
        else: 
            listt.append(strr[i]) 

    # if character length is even listt is expected to be empty 
    # or if character length is odd listt size is expected to be 1 
    if (len(strr)% 2 == 0 and len(listt) == 0 or \ 
        (len(strr) % 2 == 1 and len(listt) == 1)): 
        return True
    else: 
        return False

# Driver code 
if (canFormPalindrome("geeksforgeeks")): 
    print("Yes") 
else: 
    print("No") 

if (canFormPalindrome("geeksogeeks")): 
    print("Yes") 
else: 
    print("No") 

# This code is contributed by SHUBHAMSINGH10 

```

## C#

```cs

// C# Implementation of the above approach  
using System;  
using System.Collections.Generic; 
class GFG 
{ 

    /* 
    * function to check whether characters  
      of a string can form a palindrome 
    */
    static Boolean canFormPalindrome(String str)  
    { 

        // Create a list 
        List<char> list = new List<char>(); 

        // For each character in input strings, 
        // remove character if list contains 
        // else add character to list 
        for (int i = 0; i < str.Length; i++)  
        { 
            if (list.Contains(str[i])) 
                list.Remove((char) str[i]); 
            else
                list.Add(str[i]); 
        } 

        // if character length is even 
        // list is expected to be empty 
        // or if character length is odd  
        // list size is expected to be 1 
        if (str.Length % 2 == 0 && list.Count == 0 || // if string length is even 
           (str.Length % 2 == 1 && list.Count == 1)) // if string length is odd 
            return true; 
        else
            return false; 

    } 

    // Driver Code 
    public static void Main(String []args)  
    { 
        if (canFormPalindrome("geeksforgeeks")) 
            Console.WriteLine("Yes"); 
        else
            Console.WriteLine("No"); 

        if (canFormPalindrome("geeksogeeks")) 
            Console.WriteLine("Yes"); 
        else
            Console.WriteLine("No"); 
    } 
} 

// This code is contributed by Rajput-Ji 

```

**输出**：

```
No
Yes
```

