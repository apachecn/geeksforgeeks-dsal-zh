# 从给定字符串中删除奇数索引字符

> 原文:[https://www . geesforgeks . org/remove-奇数-索引-给定字符串中的字符/](https://www.geeksforgeeks.org/remove-odd-indexed-characters-from-a-given-string/)

给定大小为 **N** 的字符串**字符串**，任务是删除给定字符串奇数索引(基于 0 的索引)中的字符。

**示例:**

> **输入:** str = "abcdef"
> **输出:**王牌
> **说明:**
> 字符‘b’、‘d’和‘f’出现在奇数索引处，即分别为 1、3 和 5。因此，它们将从字符串中移除。
> 
> **输入:** str = "极客"
> T3】输出: ges

**方法:**按照以下步骤解决问题:

*   初始化一个空字符串，说 **new_string，**存储结果。
*   遍历给定的字符串，对于每个索引，检查它是否是**甚至**。
*   如果发现为真，则将这些索引处的字符追加到字符串 **new_string** 中。
*   最后，在完成整个字符串的遍历后，返回 **new_string** 。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to remove the odd
// indexed characters from a given string
string removeOddIndexCharacters(string s)
{

    // Stores the resultant string
    string new_string = "";

    for (int i = 0; i < s.length(); i++) {

        // If current index is odd
        if (i % 2 == 1) {

            // Skip the character
            continue;
        }

        // Otherwise, append the
        // character
        new_string += s[i];
    }

    // Return the result
    return new_string;
}

// Driver Code
int main()
{
    string str = "abcdef";

    // Function call
    cout << removeOddIndexCharacters(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG {

    // Function to remove odd indexed
    // characters from a given string
    static String removeOddIndexCharacters(
        String s)
    {

        // Stores the resultant string
        String new_string = "";

        for (int i = 0; i < s.length(); i++) {

            // If the current index is odd
            if (i % 2 == 1)

                // Skip the character
                continue;

            // Otherwise, append the
            // character
            new_string += s.charAt(i);
        }

        // Return the modified string
        return new_string;
    }

    // Driver Code
    public static void main(String[] args)
    {
        String str = "abcdef";

        // Remove the characters which
        // have odd index
        str = removeOddIndexCharacters(str);
        System.out.print(str);
    }
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to remove the odd
# indexed characters from a given string
def removeOddIndexCharacters(s): 

    # Stores the resultant string 
    new_s = "" 

    i = 0
    while i < len(s): 

        # If the current index is odd
        if (i % 2 == 1):

            # Skip the character
            i+= 1
            continue

        # Otherwise, append the 
        # character 
        new_s += s[i]
        i+= 1

    # Return the modified string 
    return new_s 

# Driver Code 
if __name__ == '__main__': 
    str = "abcdef"

    # Remove the characters which 
    # have odd index 
    str = removeOddIndexCharacters(str) 
    print(str)
```

## C#

```
// C# program to implement 
// the above approach 
using System;

class GFG{ 

// Function to remove odd indexed 
// characters from a given string 
static string removeOddIndexCharacters(string s) 
{ 

    // Stores the resultant string 
    string new_string = ""; 

    for(int i = 0; i < s.Length; i++)
    { 

        // If the current index is odd 
        if (i % 2 == 1) 

            // Skip the character 
            continue; 

        // Otherwise, append the 
        // character 
        new_string += s[i]; 
    } 

    // Return the modified string 
    return new_string; 
} 

// Driver Code 
public static void Main() 
{ 
    string str = "abcdef"; 

    // Remove the characters which 
    // have odd index 
    str = removeOddIndexCharacters(str); 

    Console.Write(str); 
} 
}

// This code is contributed by sanjoy_62
```

**Output:** 

```
ace

```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)