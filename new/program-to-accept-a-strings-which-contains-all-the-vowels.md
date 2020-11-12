# 程序接受包含所有元音的字符串

> 原文：[https://www.geeksforgeeks.org/program-to-accept-a-strings-which-contains-all-the-vowels/](https://www.geeksforgeeks.org/program-to-accept-a-strings-which-contains-all-the-vowels/)

给定字符串`S`，任务是检查并接受给定的字符串是否包含所有元音，即`'a', 'e', 'i'。'o', 'u'或 'A', 'E', 'I', 'O', 'U'`。

**示例**：

> **输入**：`S = "GeeksforGeeks"`
>
> **输出**：`Not Accepted`
>
> 由于`S`不包含元音`a`，`i`和`u`。
> 
> **输入**：`S = "ABeeIghiObhkUul"`
>
> **输出**：`Accepted`
>
> 由于`S`包含所有元音`a`，`e`，`i`，`o`和`u`。

**方法**：

*   [哈希](http://www.geeksforgeeks.org/hashing-data-structure/)可轻松解决此问题。 为此，需要创建大小为`S`的[哈希数据结构](https://www.geeksforgeeks.org/data-structure-gq/hash-gq/)，以使索引 0、1、2、3 和 4 表示元音`a, e, i, o, u`。

*   创建一个布尔数组，作为哈希数据结构，以检查字符串中是否存在所有元音。

*   逐字符遍历字符串，如果字符是元音，则标记布尔数组中存在该元音

*   在字符串迭代之后，检查布尔数组中是否存在不存在的元音。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation to check that 
// a string contains all vowels 

#include <iostream> 
using namespace std; 

// Function to to check that 
// a string contains all vowels 
int checkIfAllVowels(string str) 
{ 

    // Hash Array of size 5 
    // such that the index 0, 1, 2, 3 and 4 
    // represent the vowels a, e, i, o and u 
    int hash[5] = { 0 }; 

    // Loop the string to mark the vowels 
    // which are present 
    for (int i = 0; i < str.length(); i++) { 

        if (str[i] == 'A' || str[i] == 'a') 
            hash[0] = 1; 

        else if (str[i] == 'E' || str[i] == 'e') 
            hash[1] = 1; 

        else if (str[i] == 'I' || str[i] == 'i') 
            hash[2] = 1; 

        else if (str[i] == 'O' || str[i] == 'o') 
            hash[3] = 1; 

        else if (str[i] == 'U' || str[i] == 'u') 
            hash[4] = 1; 
    } 

    // Loop to check if there is any vowel 
    // which is not present in the string 
    for (int i = 0; i < 5; i++) { 
        if (hash[i] == 0) { 
            return 1; 
        } 
    } 
    return 0; 
} 

// Function to to check that 
// a string contains all vowels 
int checkIfAllVowelsArePresent(string str) 
{ 

    if (checkIfAllVowels(str)) 
        cout << "Not Accepted\n"; 
    else
        cout << "Accepted\n"; 
} 

// Driver Code 
int main() 
{ 
    string str = "aeioubc"; 
    checkIfAllVowelsArePresent(str); 

    return 0; 
} 

```

## Java

```java

// Java implementation to check that 
// a String contains all vowels 

class GFG 
{ 

// Function to to check that 
// a String contains all vowels 
static int checkIfAllVowels(String str) 
{ 

    // Hash Array of size 5 
    // such that the index 0, 1, 2, 3 and 4 
    // represent the vowels a, e, i, o and u 
    int []hash = new int[5]; 

    // Loop the String to mark the vowels 
    // which are present 
    for (int i = 0; i < str.length(); i++) 
    { 

        if (str.charAt(i) == 'A' || str.charAt(i) == 'a') 
            hash[0] = 1; 

        else if (str.charAt(i) == 'E' || str.charAt(i) == 'e') 
            hash[1] = 1; 

        else if (str.charAt(i) == 'I' || str.charAt(i) == 'i') 
            hash[2] = 1; 

        else if (str.charAt(i) == 'O' || str.charAt(i) == 'o') 
            hash[3] = 1; 

        else if (str.charAt(i) == 'U' || str.charAt(i) == 'u') 
            hash[4] = 1; 
    } 

    // Loop to check if there is any vowel 
    // which is not present in the String 
    for (int i = 0; i < 5; i++) 
    { 
        if (hash[i] == 0) 
        { 
            return 1; 
        } 
    } 
return 0; 
} 

// Function to to check that 
// a String contains all vowels 
static void checkIfAllVowelsArePresent(String str) 
{ 

    if (checkIfAllVowels(str) == 1) 
        System.out.print("Not Accepted\n"); 
    else
        System.out.print("Accepted\n"); 
} 

// Driver Code 
public static void main(String[] args) 
{ 
    String str = "aeioubc"; 
    checkIfAllVowelsArePresent(str); 
} 
} 

// This code is contributed by 29AjayKumar 

```

## Python3

```py

# Python3 implementation to check that  
# a string contains all vowels  

# Function to to check that  
# a string contains all vowels  
def checkIfAllVowels(string) :  

    # Hash Array of size 5  
    # such that the index 0, 1, 2, 3 and 4  
    # represent the vowels a, e, i, o and u  
    hash = [0]*5 ; 

    # Loop the string to mark the vowels 
    # which are present 
    for i in range(len(string)) : 
        if (string[i] == 'A' or string[i] == 'a') : 
            hash[0] = 1; 

        elif (string[i] == 'E' or string[i] == 'e') : 
            hash[1] = 1; 

        elif (string[i] == 'I' or string[i] == 'i') : 
            hash[2] = 1; 

        elif (string[i] == 'O' or string[i] == 'o') : 
            hash[3] = 1; 

        elif (string[i] == 'U' or string[i] == 'u') : 
            hash[4] = 1; 

    # Loop to check if there is any vowel 
    # which is not present in the string 
    for i in range(5) : 
        if (hash[i] == 0) : 
            return 1; 

    return 0;  

# Function to to check that  
# a string contains all vowels  
def checkIfAllVowelsArePresent(string) :  

    if (checkIfAllVowels(string)) : 
        print("Not Accepted");  
    else : 
        print("Accepted");  

# Driver Code  
if __name__ == "__main__" :  

    string = "aeioubc";  
    checkIfAllVowelsArePresent(string);  

# This code is contributed by AnkitRai01 

```

## C#

```cs

// C# implementation to check that 
// a String contains all vowels 
using System; 

class GFG 
{ 

// Function to to check that 
// a String contains all vowels 
static int checkIfAllVowels(String str) 
{ 

    // Hash Array of size 5 
    // such that the index 0, 1, 2, 3 and 4 
    // represent the vowels a, e, i, o and u 
    int []hash = new int[5]; 

    // Loop the String to mark the vowels 
    // which are present 
    for (int i = 0; i < str.Length; i++) 
    { 

        if (str[i] == 'A' || str[i] == 'a') 
            hash[0] = 1; 

        else if (str[i] == 'E' || str[i] == 'e') 
            hash[1] = 1; 

        else if (str[i] == 'I' || str[i] == 'i') 
            hash[2] = 1; 

        else if (str[i] == 'O' || str[i] == 'o') 
            hash[3] = 1; 

        else if (str[i] == 'U' || str[i] == 'u') 
            hash[4] = 1; 
    } 

    // Loop to check if there is any vowel 
    // which is not present in the String 
    for (int i = 0; i < 5; i++) 
    { 
        if (hash[i] == 0) 
        { 
            return 1; 
        } 
    } 
return 0; 
} 

// Function to to check that 
// a String contains all vowels 
static void checkIfAllVowelsArePresent(String str) 
{ 

    if (checkIfAllVowels(str) == 1) 
        Console.Write("Not Accepted\n"); 
    else
        Console.Write("Accepted\n"); 
} 

// Driver Code 
public static void Main(String[] args) 
{ 
    String str = "aeioubc"; 
    checkIfAllVowelsArePresent(str); 
} 
} 

// This code is contributed by 29AjayKumar 

```

**输出**：

```
Accepted

```



* * *

* * *



