# 检查每个字符的频率是否等于其在英语字母中的位置

> 原文：[https://www.geeksforgeeks.org/check-if-frequency-of-each-character-is-equal-to-its-position-in-english-alphabet/](https://www.geeksforgeeks.org/check-if-frequency-of-each-character-is-equal-to-its-position-in-english-alphabet/)

给定小写字母的字符串`str`，任务是检查字符串中每个不同字符的频率是否等于其在英语字母表中的位置。 如果有效，则打印`Yes`，否则打印`No`。

**示例**：

> **输入**：`str = "abbcccdddd"`
>
> **输出**：`Yes`
>
> **解释**：
> 
> ```
> F(a) = 1
> F(b) = 2
> F(c) = 3 
> F(d) = 4
> ```
> 
> 因此输出为`Yes`。
> 
> **输入**：`str = "geeksforgeeks"`
> 
> **输出**：`No`

**方法**：

1.  将每个字符的[频率](https://www.geeksforgeeks.org/python-frequency-of-each-character-in-string/)存储在 26 个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)中，以用于[散列](http://www.geeksforgeeks.org/hashing-data-structure/)。

2.  现在遍历哈希数组，并检查索引`i`处每个字符的频率是否等于`i + 1`。

3.  如果是，则打印`Yes`，否则打印为`No`。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach

#include "bits/stdc++.h"
using namespace std;

bool checkValidString(string str)
{

    // Initialise frequency array
    int freq[26] = { 0 };

    // Traverse the string
    for (int i = 0; str[i]; i++) {

        // Update the frequency
        freq[str[i] - 'a']++;
    }

    // Check for valid string
    for (int i = 0; i < 26; i++) {

        // If frequency is non-zero
        if (freq[i] != 0) {

            // If freq is not equals
            // to (i+1), then return
            // false
            if (freq[i] != i + 1) {
                return false;
            }
        }
    }

    // Return true;
    return true;
}

// Driver Code
int main()
{

    // Given string str
    string str = "abbcccdddd";

    if (checkValidString(str))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}

```

## Java

```java

// Java program for the above approach
class GFG{

static boolean checkValidString(String str)
{

    // Initialise frequency array
    int freq[] = new int[26];

    // Traverse the String
    for(int i = 0; i < str.length(); i++) 
    {

       // Update the frequency
       freq[str.charAt(i) - 'a']++;
    }

    // Check for valid String
    for(int i = 0; i < 26; i++)
    {

       // If frequency is non-zero
       if (freq[i] != 0)
       {

           // If freq is not equals
           // to (i+1), then return
           // false
           if (freq[i] != i + 1)
           {
               return false;
           }
       }
    }

    // Return true;
    return true;
}

// Driver Code
public static void main(String[] args)
{

    // Given String str
    String str = "abbcccdddd";

    if (checkValidString(str))
    {
        System.out.print("Yes");
    }
    else
    {
        System.out.print("No");
    }
}
}

// This code is contributed by sapnasingh4991

```

## Python3

```py

# Python3 program for the 
# above approach
def checkValidString(str):

    # Initialise frequency array
    freq = [0 for i in range(26)]

    # Traverse the string
    for i in range(len(str)):

        # Update the frequency
        freq[ord(str[i]) - ord('a')] += 1

    # Check for valid string 
    for i in range(26):

        # If frequency is non-zero
        if(freq[i] != 0):

            # If freq is not equals 
            # to (i+1), then return 
            # false 
            if(freq[i] != i + 1):
                return False
    # Return true
    return True

# Driver Code

# Given string str 
str = "abbcccdddd"

if(checkValidString(str)):
    print("Yes")
else:
    print("No")

# This code is contributed by avanitrachhadiya2155

```

## C#

```cs

// C# program for the above approach
using System;
class GFG{

static bool checkValidString(String str)
{

    // Initialise frequency array
    int []freq = new int[26];

    // Traverse the String
    for(int i = 0; i < str.Length; i++) 
    {

        // Update the frequency
        freq[str[i] - 'a']++;
    }

    // Check for valid String
    for(int i = 0; i < 26; i++)
    {

        // If frequency is non-zero
        if (freq[i] != 0)
        {

            // If freq is not equals
            // to (i+1), then return
            // false
            if (freq[i] != i + 1)
            {
                return false;
            }
        }
    }

    // Return true;
    return true;
}

// Driver Code
public static void Main(String[] args)
{

    // Given String str
    String str = "abbcccdddd";

    if (checkValidString(str))
    {
        Console.Write("Yes");
    }
    else
    {
        Console.Write("No");
    }
}
}

// This code is contributed by sapnasingh4991

```

**输出**： 

```
Yes

```

**时间复杂度**：`O(n)`，其中`N`是字符串的长度。

**辅助空间**：`O(26)`。



* * *

* * *



