# 字符串

> 原文：[https://www.geeksforgeeks.org/count-number-of-distinct-substring-in-a-string/](https://www.geeksforgeeks.org/count-number-of-distinct-substring-in-a-string/)

中不同子字符串的计数

给定一个字符串，计算给定字符串的所有不同子字符串。

**示例**：

```
Input : abcd
Output : abcd abc ab a bcd bc b cd c d
All Elements are Distinct

Input : aaa
Output : aaa aa a aa a a
All elements are not Distinct
```

先决条件：[打印给定数组](https://www.geeksforgeeks.org/program-print-substrings-given-string/)的子数组

这个想法是使用哈希表（Java 中为 [HashSet](http://www.geeksforgeeks.org/hashset-in-java/) ）来存储所有生成的子字符串。 最后，我们返回 HashSet 的大小。

## C++

```cpp

// C++ program to count all distinct substrings in a string 
#include<bits/stdc++.h> 
using namespace std; 

int distinctSubstring(string str) 
{ 
    // Put all distinct substring in a HashSet 
    set<string> result ; 

    // List All Substrings 
    for (int i = 0; i <= str.length(); i++) 
    { 
        for (int j = 1; j <= str.length()-i; j++) 
        { 

            // Add each substring in Set 
            result.insert(str.substr(i, j)); 
        } 
    } 

    // Return size of the HashSet 
    return result.size(); 
} 

// Driver Code 
int main() 
{ 
    string str = "aaaa"; 
    cout << (distinctSubstring(str)); 
} 

// This code is contributed by Rajput-Ji 

```

## Java

```java

// Java program to count all distinct substrings in a string 
import java.util.HashSet; 
import java.util.Iterator; 
import java.util.Set; 

public class DistinctSubstring { 

    public static int distinctSubstring(String str) 
    { 
        // Put all distinct substring in a HashSet 
        Set<String> result = new HashSet<String>(); 

        // List All Substrings 
        for (int i = 0; i <= str.length(); i++) { 
            for (int j = i + 1; j <= str.length(); j++) { 

                // Add each substring in Set 
                result.add(str.substring(i, j)); 
            } 
        } 

        // Return size of the HashSet 
        return result.size(); 
    } 

    // Driver Code 
    public static void main(String[] args) 
    { 
        String str = "aaaa"; 
        System.out.println(distinctSubstring(str)); 
    } 
} 

```

## Python3

```py

# Python3 program to count all distinct substrings in a string 

> 原文：[https://www.geeksforgeeks.org/count-number-of-distinct-substring-in-a-string/](https://www.geeksforgeeks.org/count-number-of-distinct-substring-in-a-string/)

def distinctSubstring(str): 
    # Put all distinct substring in a HashSet 
    result = set() 

    # List All Substrings 
    for i in range(len(str)+1): 
        for j in range( i + 1, len(str)+1): 

            # Add each substring in Set 
            result.add(str[i:j]); 
        # Return size of the HashSet 
    return len(result); 

# Driver Code 

> 原文：[https://www.geeksforgeeks.org/count-number-of-distinct-substring-in-a-string/](https://www.geeksforgeeks.org/count-number-of-distinct-substring-in-a-string/)
if __name__ == '__main__': 
    str = "aaaa"; 
    print(distinctSubstring(str)); 

# This code has been contributed by 29AjayKumar 

> 原文：[https://www.geeksforgeeks.org/count-number-of-distinct-substring-in-a-string/](https://www.geeksforgeeks.org/count-number-of-distinct-substring-in-a-string/)

```

## C#

```cs

// C# program to count all distinct 
// substrings in a string 
using System; 
using System.Collections.Generic; 

class DistinctSubstring  
{ 
    public static int distinctSubstring(String str) 
    { 
        // Put all distinct substring in a HashSet 
        HashSet<String> result = new HashSet<String>(); 

        // List All Substrings 
        for (int i = 0; i <= str.Length; i++)  
        { 
            for (int j = i + 1; j <= str.Length; j++)  
            { 

                // Add each substring in Set 
                result.Add(str.Substring(i, j - i)); 
            } 
        } 

        // Return size of the HashSet 
        return result.Count; 
    } 

    // Driver Code 
    public static void Main(String[] args) 
    { 
        String str = "aaaa"; 
        Console.WriteLine(distinctSubstring(str)); 
    } 
} 

// This code is contributed by 29AjayKumar 

```

**Output:**

```
4

```

**如何打印不同的子字符串？**

## C++

```cpp

// C++ program to count all distinct 
// substrings in a string 
#include <bits/stdc++.h> 
using namespace std; 

set<string> distinctSubstring(string str) 
{ 

    // Put all distinct substrings 
    // in the Hashset 
    set<string> result; 

    // List all substrings 
    for(int i = 0; i <= str.length(); i++) 
    { 
        for(int j = i + 1; j <= str.length(); j++) 
        { 

            // Add each substring in Set 
            result.insert(str.substr(i, j)); 
        } 
    } 

    // Return the hashset 
    return result; 
} 

// Driver code 
int main() 
{ 
    string str = "aaaa"; 
    set<string> subs = distinctSubstring(str); 

    cout << "Distinct Substrings are: \n"; 
    for(auto i : subs) 
        cout << i << endl; 
} 

// This code is contributed by Ronak Mangal 

```

## Java

```java

// Java program to count all distinct substrings in a string 
import java.util.HashSet; 
import java.util.Iterator; 
import java.util.Set; 

public class DistinctSubstring { 

    public static Set<String> distinctSubstring(String str) 
    { 

        // Put all distinct substring in a HashSet 
        Set<String> result = new HashSet<String>(); 

        // List All Substrings 
        for (int i = 0; i <= str.length(); i++) { 
            for (int j = i + 1; j <= str.length(); j++) { 

                // Add each substring in Set 
                result.add(str.substring(i, j)); 
            } 
        } 

        // Return the HashSet 
        return result; 
    } 

    // Driver Code 
    public static void main(String[] args) 
    { 
        String str = "aaaa"; 
        Set<String> subs = distinctSubstring(str); 

        System.out.println("Distinct Substrings are: "); 
        for (String s : subs) { 
            System.out.println(s); 
        } 
    } 
} 

```

## Python3

```py

# Python3 program to count all distinct  

> 原文：[https://www.geeksforgeeks.org/count-number-of-distinct-substring-in-a-string/](https://www.geeksforgeeks.org/count-number-of-distinct-substring-in-a-string/)
# substrings in a string 

> 原文：[https://www.geeksforgeeks.org/count-number-of-distinct-substring-in-a-string/](https://www.geeksforgeeks.org/count-number-of-distinct-substring-in-a-string/)

def distinctSubstring(str): 

    # Put all distinct substring in a HashSet 
    result = set(); 

    # List All Substrings 
    for i in range(len(str)): 
        for j in range(i + 1, len(str) + 1): 

            # Add each substring in Set 
            result.add(str[i:j]); 

        # Return the HashSet 
    return result; 

# Driver Code 

> 原文：[https://www.geeksforgeeks.org/count-number-of-distinct-substring-in-a-string/](https://www.geeksforgeeks.org/count-number-of-distinct-substring-in-a-string/)
if __name__ == '__main__': 

    str = "aaaa"; 
    subs = distinctSubstring(str); 

    print("Distinct Substrings are: "); 
    for s in subs: 
        print(s); 

# This code is contributed by 29AjayKumar 

> 原文：[https://www.geeksforgeeks.org/count-number-of-distinct-substring-in-a-string/](https://www.geeksforgeeks.org/count-number-of-distinct-substring-in-a-string/)

```

## C#

```cs

// C# program to count all distinct  
// substrings in a string 
using System; 
using System.Collections.Generic; 

class GFG 
{ 
    public static HashSet<String> distinctSubstring(String str) 
    { 

        // Put all distinct substring in a HashSet 
        HashSet<String> result = new HashSet<String>(); 

        // List All Substrings 
        for (int i = 0; i <= str.Length; i++)  
        { 
            for (int j = i + 1; j <= str.Length; j++)  
            { 

                // Add each substring in Set 
                result.Add(str.Substring(i, j - i)); 
            } 
        } 

        // Return the HashSet 
        return result; 
    } 

    // Driver Code 
    public static void Main(String[] args) 
    { 
        String str = "aaaa"; 
        HashSet<String> subs = distinctSubstring(str); 

        Console.WriteLine("Distinct Substrings are: "); 
        foreach (String s in subs)  
        { 
            Console.WriteLine(s); 
        } 
    } 
} 

// This code is contributed by 29AjayKumar 

```

**Output:**

```
Distinct Substrings are: 
aa
aaa
a
aaaa

```

**优化**：

我们可以进一步优化上面的代码。 substr（）函数以线性时间工作。 我们可以使用将当前字符追加到前一个子字符串来获取当前子字符串。

## C++

```cpp

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

// Function to return the count of 
// valid sub-strings 
void printSubstrings(string s) 
{ 

    // To store distinct output substrings 
    unordered_set<string> us; 

    // Traverse through the given string and 
    // one by one generate substrings beginning 
    // from s[i]. 
    for (int i = 0; i < s.size(); ++i) { 

        // One by one generate substrings ending 
        // with s[j] 
        string ss = ""; 
        for (int j = i; j < s.size(); ++j) { 

            ss = ss + s[j]; 
            us.insert(ss); 
        } 
    } 

    // Print all substrings one by one 
    for (auto s : us) 
        cout << s << " "; 
} 

// Driver code 
int main() 
{ 
    string str = "aaabc"; 
    printSubstrings(str); 
    return 0; 
} 

```

## Java

```java

// Java implementation of the approach 
import java.util.*; 

class GFG 
{ 

// Function to return the count of 
// valid sub-Strings 
static void printSubStrings(String s) 
{ 

    // To store distinct output subStrings 
    HashSet<String> us = new HashSet<String>(); 

    // Traverse through the given String and 
    // one by one generate subStrings beginning 
    // from s[i]. 
    for (int i = 0; i < s.length(); ++i) 
    { 

        // One by one generate subStrings ending 
        // with s[j] 
        String ss = ""; 
        for (int j = i; j < s.length(); ++j)  
        { 
            ss = ss + s.charAt(j); 
            us.add(ss); 
        } 
    } 

    // Print all subStrings one by one 
    for (String str : us) 
        System.out.print(str + " "); 
} 

// Driver code 
public static void main(String[] args) 
{ 
    String str = "aaabc"; 
    printSubStrings(str); 
} 
} 

// This code is contributed by Rajput-Ji 

```

## Python3

```py

# Python3 implementation of the approach 

> 原文：[https://www.geeksforgeeks.org/count-number-of-distinct-substring-in-a-string/](https://www.geeksforgeeks.org/count-number-of-distinct-substring-in-a-string/)

# Function to return the count of 

> 原文：[https://www.geeksforgeeks.org/count-number-of-distinct-substring-in-a-string/](https://www.geeksforgeeks.org/count-number-of-distinct-substring-in-a-string/)
# valid sub-Strings 

> 原文：[https://www.geeksforgeeks.org/count-number-of-distinct-substring-in-a-string/](https://www.geeksforgeeks.org/count-number-of-distinct-substring-in-a-string/)
def printSubStrings(s): 

    # To store distinct output subStrings 
    us = set(); 

    # Traverse through the given String and 
    # one by one generate subStrings beginning 
    # from s[i]. 
    for i in range(len(s)): 

        # One by one generate subStrings ending 
        # with s[j] 
        ss = ""; 
        for j in range(i, len(s)): 
            ss = ss + s[j]; 
            us.add(ss); 

    # Prall subStrings one by one 
    for str in us: 
        print(str, end=" "); 

# Driver code 

> 原文：[https://www.geeksforgeeks.org/count-number-of-distinct-substring-in-a-string/](https://www.geeksforgeeks.org/count-number-of-distinct-substring-in-a-string/)
if __name__ == '__main__': 
    str = "aaabc"; 
    printSubStrings(str); 

# This code is contributed by 29AjayKumar 

> 原文：[https://www.geeksforgeeks.org/count-number-of-distinct-substring-in-a-string/](https://www.geeksforgeeks.org/count-number-of-distinct-substring-in-a-string/)

```

## C#

```cs

// C# implementation of the approach 
using System; 
using System.Collections.Generic; 

class GFG 
{ 

// Function to return the count of 
// valid sub-Strings 
static void printSubStrings(String s) 
{ 

    // To store distinct output subStrings 
    HashSet<String> us = new HashSet<String>(); 

    // Traverse through the given String and 
    // one by one generate subStrings  
    // beginning from s[i]. 
    for (int i = 0; i < s.Length; ++i) 
    { 

        // One by one generate subStrings 
        // ending with s[j] 
        String ss = ""; 
        for (int j = i; j < s.Length; ++j)  
        { 
            ss = ss + s[j]; 
            us.Add(ss); 
        } 
    } 

    // Print all subStrings one by one 
    foreach (String str in us) 
        Console.Write(str + " "); 
} 

// Driver code 
public static void Main(String[] args) 
{ 
    String str = "aaabc"; 
    printSubStrings(str); 
} 
} 

// This code is contributed by Rajput-Ji 

```

**Output:**

```
bc b abc ab aabc aa aaa c a aaab aab aaabc

```c



* * *

* * *



