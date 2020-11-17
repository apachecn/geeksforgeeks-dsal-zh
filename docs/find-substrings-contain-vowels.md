# 查找包含所有元音的子字符串

> 原文：[https://www.geeksforgeeks.org/find-substrings-contain-vowels/](https://www.geeksforgeeks.org/find-substrings-contain-vowels/)

我们给了我们一个小写字母的字符串。 我们需要至少打印一次包含所有元音的子字符串，并且子字符串中不存在辅音（非元音字符）。

**示例**：

```
Input : str = aeoibddaeoiud
Output : aeoiu

Input : str = aeoibsddaeiouudb
Output : aeiou, aeiouu

```

参考：-三星面试问题。

我们使用基于[散列](https://www.geeksforgeeks.org/hashing-data-structure/)的技术，并从头开始遍历字符串。 对于每个字符，我们考虑从该字符开始的所有子字符串。 如果遇到辅音，则移至下一个起始字符。 否则，我们在哈希中插入当前字符。 如果包括所有元音，我们将打印当前子串。

## C++

```cpp

// CPP program to find all substring that  
// contain all vowels 
#include <bits/stdc++.h> 

using namespace std; 

// Returns true if x is vowel. 
bool isVowel(char x) 
{ 
    // Function to check whether a character is 
    // vowel or not 
    return (x == 'a' || x == 'e' || x == 'i' || 
                        x == 'o' || x == 'u'); 
} 

void FindSubstring(string str) 
{ 
    set<char> hash; // To store vowels 

    // Outer loop picks starting character and  
    // inner loop picks ending character. 
    int n = str.length(); 
    for (int i = 0; i < n; i++) { 
       for (int j = i; j < n; j++) { 

            // If current character is not vowel, 
            // then no more result substrings  
            // possible starting from str[i]. 
            if (isVowel(str[j]) == false) 
              break; 

            // If vowel, then we insert it in hash               
            hash.insert(str[j]); 

            // If all vowels are present in current 
            // substring 
            if (hash.size() == 5) 
                cout << str.substr(i, j-i+1) << " "; 
        } 

        hash.clear(); 
    } 
} 

// Driver code 
int main() 
{ 
    string str = "aeoibsddaeiouudb"; 
    FindSubstring(str); 
    return 0; 
} 

```

## Java

```java

// Java program to find all substring that   
// contain all vowels  
import java.util.HashSet; 

public class GFG { 

    // Returns true if x is vowel. 
    static boolean isVowel(char x) { 
        // Function to check whether a character is 
        // vowel or not 
        return (x == 'a' || x == 'e' || x == 'i' 
                || x == 'o' || x == 'u'); 
    } 

    static void findSubstring(String str) { 
        HashSet<Character> hash = new HashSet<Character>();  
            // To store vowels 

        // Outer loop picks starting character and 
        // inner loop picks ending character. 
        int n = str.length(); 
        for (int i = 0; i < n; i++) { 
            for (int j = i; j < n; j++) { 

                // If current character is not vowel, 
                // then no more result substrings 
                // possible starting from str[i]. 
                if (isVowel(str.charAt(j)) == false) 
                    break; 

                // If vowel, then we insert it in hash 
                hash.add(str.charAt(j)); 

                // If all vowels are present in current 
                // substring 
                if (hash.size() == 5) 
                    System.out.print(str.substring(i, j + 1) + " "); 
            } 
            hash.clear(); 
        } 
    } 

    // Driver code 
    public static void main(String[] args) { 
        String str = "aeoibsddaeiouudb"; 
        findSubstring(str); 
    } 
} 

```

## Python3

```py

# Python3 program to find all subthat 
# contain all vowels 

# Returns true if x is vowel. 
def isVowel(x): 

    # Function to check whether a character is 
    # vowel or not 
    if (x == 'a' or x == 'e' or x == 'i' or 
        x == 'o' or x == 'u'): 
        return True
    return False

def FindSubstr1ing(str1): 

    # To store vowels 

    # Outer loop picks starting character and 
    # inner loop picks ending character. 
    n = len(str1) 
    for i in range(n): 
        hash = dict() 
        for j in range(i, n): 

            # If current character is not vowel, 
            # then no more result substr1ings 
            # possible starting from str1[i]. 
            if (isVowel(str1[j]) == False): 
                break

            # If vowel, then we insert it in hash 
            hash[str1[j]] = 1

            # If all vowels are present in current 
            # substr1ing 
            if (len(hash) == 5): 
                print(str1[i:j + 1], end = " ") 

# Driver code 
str1 = "aeoibsddaeiouudb"
FindSubstr1ing(str1) 

# This code is contributed by Mohit Kumar 

```

## C#

```cs

// C# program to find all substring that  
// contain all vowels  
using System; 
using System.Collections.Generic; 

public class GFG 
{ 

// Returns true if x is vowel.  
public static bool isVowel(char x) 
{ 
    // Function to check whether a  
    // character is vowel or not  
    return (x == 'a' || x == 'e' || 
            x == 'i' || x == 'o' || x == 'u'); 
} 

public static void findSubstring(string str) 
{ 
    HashSet<char> hash = new HashSet<char>(); 

    // To store vowels      
    // Outer loop picks starting character and  
    // inner loop picks ending character.  
    int n = str.Length; 
    for (int i = 0; i < n; i++) 
    { 
        for (int j = i; j < n; j++) 
        { 

            // If current character is not vowel,  
            // then no more result substrings  
            // possible starting from str[i].  
            if (isVowel(str[j]) == false) 
            { 
                break; 
            } 

            // If vowel, then we insert it in hash  
            hash.Add(str[j]); 

            // If all vowels are present in current  
            // substring  
            if (hash.Count == 5) 
            { 
                Console.Write(str.Substring(i,       
                             (j + 1) - i) + " "); 
            } 
        } 
        hash.Clear(); 
    } 
} 

// Driver code  
public static void Main(string[] args) 
{ 
    string str = "aeoibsddaeiouudb"; 
    findSubstring(str); 
} 
} 

// This code is contributed by Shrikant13 

```

**输出**：

```
aeiou aeiouu

```

**时间复杂度**：`O(N ^ 2)`。

**优化的解决方案**：

对于每个字符，如果当前字符是元音，则插入到哈希中。 否则将标志`Start`设置为从第`i + 1`个索引开始的下一个子字符串。 如果包括所有元音，我们将打印当前子串。

## C++

```cpp

// C++ program to find all substring that 
// contain all vowels 
#include<bits/stdc++.h> 

using namespace std; 

// Returns true if x is vowel. 
bool isVowel(char x) 
{ 
    // Function to check whether a character is 
    // vowel or not 
    return (x == 'a' || x == 'e' || x == 'i' || 
                        x == 'o' || x == 'u'); 
} 

// Function to FindSubstrings of string 
void FindSubstring(string str) 
{ 
    set<char> hash;  // To store vowels 

    int start = 0; 
    for (int i=0; i<str.length(); i++) 
    { 
        // If current character is vowel then 
        // insert into hash , 
        if (isVowel(str[i]) == true) 
        { 
            hash.insert(str[i]); 

            // If all vowels are present in current 
            // substring 
            if (hash.size()==5) 
                cout << str.substr(start, i-start+1) 
                     << " "; 
        } 
        else
        { 
            start = i+1; 
            hash.clear(); 
        } 
    } 
} 

// Driver Code 
int main() 
{ 
    string str = "aeoibsddaeiouudb"; 
    FindSubstring(str); 
    return 0; 
} 

```

## Java

```java

// Java program to find all substring that   
// contain all vowels  
import java.util.HashSet; 

public class GFG { 

    // Returns true if x is vowel. 
    static boolean isVowel(char x) { 
        // Function to check whether a character is 
        // vowel or not 
        return (x == 'a' || x == 'e' || x == 'i' 
                || x == 'o' || x == 'u'); 
    } 

    // Function to FindSubstrings of string 
    static void findSubstring(String str) { 
        HashSet<Character> hash = new HashSet<Character>(); 
        // To store vowels 

        int start = 0; 
        for (int i = 0; i < str.length(); i++) { 
            // If current character is vowel then 
            // insert into hash , 
            if (isVowel(str.charAt(i)) == true) { 
                hash.add(str.charAt(i)); 

                // If all vowels are present in current 
                // substring 
                if (hash.size() == 5) 
                    System.out.print(str.substring(start, i + 1) + " "); 
            } else { 
                start = i + 1; 
                hash.clear(); 
            } 
        } 
    } 

    // Driver Code 
    public static void main(String[] args) { 
        String str = "aeoibsddaeiouudb"; 
        findSubstring(str); 
    } 

} 

```

## Python3

```py

# Python3 program to find all substring  
# that contain all vowels 

# Returns true if x is vowel. 
def isVowel(x): 

    # Function to check whether  
    # a character is vowel or not 
    return (x == 'a' or x == 'e' or 
            x == 'i' or x == 'o' or 
            x == 'u'); 

# Function to FindSubstrings of string 
def FindSubstring(str): 

    hash = set(); # To store vowels 

    start = 0; 
    for i in range(len(str)): 

        # If current character is vowel  
        # then insert into hash 
        if (isVowel(str[i]) == True): 
            hash.add(str[i]); 

            # If all vowels are present  
            # in current substring 
            if (len(hash) == 5): 
                print(str[start : i + 1],  
                              end = " "); 
        else: 
            start = i + 1; 
            hash.clear(); 

# Driver Code 
str = "aeoibsddaeiouudb"; 
FindSubstring(str); 

# This code is contributed by 29AjayKumar 

```

## C#

```cs

using System; 
using System.Collections.Generic; 

// c# program to find all substring that    
// contain all vowels   

public class GFG 
{ 

    // Returns true if x is vowel.  
    public static bool isVowel(char x) 
    { 
        // Function to check whether a character is  
        // vowel or not  
        return (x == 'a' || x == 'e' || x == 'i' || x == 'o' || x == 'u'); 
    } 

    // Function to FindSubstrings of string  
    public static void findSubstring(string str) 
    { 
        HashSet<char> hash = new HashSet<char>(); 
        // To store vowels  

        int start = 0; 
        for (int i = 0; i < str.Length; i++) 
        { 
            // If current character is vowel then  
            // insert into hash ,  
            if (isVowel(str[i]) == true) 
            { 
                hash.Add(str[i]); 

                // If all vowels are present in current  
                // substring  
                if (hash.Count == 5) 
                { 
                    Console.Write(str.Substring(start, (i + 1) - start) + " "); 
                } 
            } 
            else
            { 
                start = i + 1; 
                hash.Clear(); 
            } 
        } 
    } 

    // Driver Code  
    public static void Main(string[] args) 
    { 
        string str = "aeoibsddaeiouudb"; 
        findSubstring(str); 
    } 

} 

// This code is contributed by Shrikant13 

```

**输出**：

```
aeiou aeiouu

```

感谢 **Kriti Shukla** 提出了这种优化的解决方案。

本文由 **Ashish Madaan** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

