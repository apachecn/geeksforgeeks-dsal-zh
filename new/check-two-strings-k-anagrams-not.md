# 检查两个字符串是否为 k-anagrams

给定两个字符串的小写字母和一个值 k，任务是查找两个字符串是否彼此为 K-anagram。

如果满足以下两个条件，则两个字符串称为 **k-anagrams** 。

1.  两者具有相同的字符数。

2.  通过改变一个字符串中最多 k 个字符，两个字符串可以变成字谜。

**示例**：

```
Input:  str1 = "anagram" , str2 = "grammar" , k = 3
Output:  Yes
Explanation: We can update maximum 3 values and 
it can be done in changing only 'r' to 'n' 
and 'm' to 'a' in str2.

Input:  str1 = "geeks", str2 = "eggkf", k = 1
Output:  No
Explanation: We can update or modify only 1 
value but there is a need of modifying 2 characters. 
i.e. g and f in str 2.

```

**方法 1**：

下面是一种检查两个字符串是否彼此为 k-anagram 的解决方案。

1.  将两个字符串的所有字符的出现都存储在单独的计数数组中。

2.  计算两个字符串中不同字符的数量（在这种情况下，如果一个字符串有 4 个 a，而第二个字符串有 3 个“ a”，则也将被计数。

3.  如果不同字符的数量小于或等于 k，则返回 true，否则返回 false。

## C++

```cpp

// C++ program to check if two strings are k anagram 
// or not. 
#include<bits/stdc++.h> 
using namespace std; 
const int MAX_CHAR = 26; 

// Function to check that string is k-anagram or not 
bool arekAnagrams(string str1, string str2, int k) 
{ 
    // If both strings are not of equal 
    // length then return false 
    int n = str1.length(); 
    if (str2.length() != n) 
        return false; 

    int count1[MAX_CHAR] = {0}; 
    int count2[MAX_CHAR] = {0}; 

    // Store the occurrence of all characters 
    // in a hash_array 
    for (int i = 0; i < n; i++) 
        count1[str1[i]-'a']++; 
    for (int i = 0; i < n; i++) 
        count2[str2[i]-'a']++; 

    int count = 0; 

    // Count number of characters that are 
    // different in both strings 
    for (int i = 0; i < MAX_CHAR; i++) 
        if (count1[i] > count2[i]) 
            count = count + abs(count1[i]-count2[i]); 

    // Return true if count is less than or 
    // equal to k 
    return (count <= k); 
} 

// Driver code 
int main() 
{ 
    string str1 = "anagram"; 
    string str2 = "grammar"; 
    int k = 2; 
    if (arekAnagrams(str1, str2, k)) 
        cout << "Yes"; 
    else
        cout<< "No"; 
    return 0; 
} 

```

## Java

```java

// Java program to check if two strings are k anagram 
// or not. 
public class GFG { 

    static final int MAX_CHAR = 26; 

    // Function to check that string is k-anagram or not 
    static boolean arekAnagrams(String str1, String str2,  
                                                 int k) 
    { 
        // If both strings are not of equal 
        // length then return false 
        int n = str1.length(); 
        if (str2.length() != n) 
            return false; 

        int[] count1 = new int[MAX_CHAR]; 
        int[] count2 = new int[MAX_CHAR]; 
        int count = 0; 

        // Store the occurrence of all characters 
        // in a hash_array 
        for (int i = 0; i < n; i++) 
            count1[str1.charAt(i) - 'a']++; 
        for (int i = 0; i < n; i++) 
            count2[str2.charAt(i) - 'a']++; 

        // Count number of characters that are 
        // different in both strings 
        for (int i = 0; i < MAX_CHAR; i++) 
            if (count1[i] > count2[i]) 
                count = count + Math.abs(count1[i] -  
                                          count2[i]); 

        // Return true if count is less than or 
        // equal to k 
        return (count <= k); 
    } 

    // Driver code 
    public static void main(String args[]) 
    { 
        String str1 = "anagram"; 
        String str2 = "grammar"; 
        int k = 2; 
        if (arekAnagrams(str1, str2, k)) 
            System.out.println("Yes"); 
        else
            System.out.println("No"); 
    } 
} 
// This code is contributed by Sumit Ghosh 

```

## Python3

```py

# Python3 program to check if two  
# strings are k anagram or not. 
MAX_CHAR = 26

# Function to check that is  
# k-anagram or not  
def arekAnagrams(str1, str2, k) : 

    # If both strings are not of equal  
    # length then return false  
    n = len(str1) 
    if (len(str2)!= n) : 
        return False

    count1 = [0] * MAX_CHAR  
    count2 = [0] * MAX_CHAR 

    # Store the occurrence of all  
    # characters in a hash_array  
    for i in range(n):  
        count1[ord(str1[i]) - 
               ord('a')] += 1
    for i in range(n):  
        count2[ord(str2[i]) - 
               ord('a')] += 1

    count = 0

    # Count number of characters that 
    # are different in both strings  
    for i in range(MAX_CHAR): 
        if (count1[i] > count2[i]) : 
            count = count + abs(count1[i] - 
                                count2[i])  

    # Return true if count is less 
    # than or equal to k  
    return (count <= k)  

# Driver Code  
if __name__ == '__main__': 
    str1 = "anagram"
    str2 = "grammar"
    k = 2
    if (arekAnagrams(str1, str2, k)):  
        print("Yes")  
    else: 
        print("No") 

# This code is contributed 
# by SHUBHAMSINGH10 

```

## C#

```cs

// C# program to check if two  
// strings are k anagram or not. 
using System; 
class GFG { 

    static int MAX_CHAR = 26; 

    // Function to check that  
    // string is k-anagram or not 
    static bool arekAnagrams(string str1,  
                             string str2,  
                                      int k) 
    { 

        // If both strings are not of equal 
        // length then return false 
        int n = str1.Length; 
        if (str2.Length != n) 
            return false; 

        int[] count1 = new int[MAX_CHAR]; 
        int[] count2 = new int[MAX_CHAR]; 
        int count = 0; 

        // Store the occurrence 
        // of all characters 
        // in a hash_array 
        for (int i = 0; i < n; i++) 
            count1[str1[i] - 'a']++; 
        for (int i = 0; i < n; i++) 
            count2[str2[i] - 'a']++; 

        // Count number of characters that are 
        // different in both strings 
        for (int i = 0; i < MAX_CHAR; i++) 
            if (count1[i] > count2[i]) 
                count = count + Math.Abs(count1[i] -  
                                         count2[i]); 

        // Return true if count is 
        // less than or equal to k 
        return (count <= k); 
    } 

    // Driver code 
    public static void Main() 
    { 
        string str1 = "anagram"; 
        string str2 = "grammar"; 
        int k = 2; 
        if (arekAnagrams(str1, str2, k)) 
            Console.Write("Yes"); 
        else
            Console.Write("No"); 
    } 
} 
// This code is contributed by nitin mittal. 

```

## PHP

```php

<?php 
// PHP program to check  
// if two strings are  
// k anagram or not. 
$MAX_CHAR = 26; 

// Function to check that 
// string is k-anagram or not 
function arekAnagrams($str1, $str2, $k) 
{ 
    global $MAX_CHAR; 
    // If both strings are not of  
    // equal length then return false 
    $n = strlen($str1); 
    if (strlen($str2) != $n) 
        return false; 

    $count1 = (0); 
    $count2 = (0); 

    // Store the occurrence of all 
    // characters in a hash_array 
    $count = 0; 

    // Count number of characters that  
    // are different in both strings 
    for ($i = 0; $i < $MAX_CHAR; $i++) 
        if ($count1[$i] > $count2[$i]) 
            $count = $count + abs($count1[$i] -  
                                  $count2[$i]); 

    // Return true if count is  
    // less than or equal to k 
    return ($count <= $k); 
} 

// Driver Code 
$str1 = "anagram"; 
$str2 = "grammar"; 
$k = 2; 
if (arekAnagrams($str1, $str2, $k)) 
    echo "Yes"; 
else
    echo "No"; 

// This code is contributed by m_kit 
?> 

```

**Output :**

```
Yes

```

**方法 2**：

我们可以优化上述解决方案。 在这里，我们仅使用一个 count 数组来存储 str1 中的字符计数。 我们遍历 str2 并减少出现在 str2 中的 count 数组中每个字符的出现。 如果在 str1 中找到一个不存在的字符，则增加不同字符的计数。 如果不同字符的数量大于 k，则返回 false。

## C++

```cpp

// Optimized C++ program to check if two strings 
// are k anagram or not. 
#include<bits/stdc++.h> 
using namespace std; 

const int MAX_CHAR = 26; 

// Function to check if str1 and str2 are k-anagram 
// or not 
bool areKAnagrams(string str1, string str2, int k) 
{ 
    // If both strings are not of equal 
    // length then return false 
    int n = str1.length(); 
    if (str2.length() != n) 
        return false; 

    int hash_str1[MAX_CHAR] = {0}; 

    // Store the occurrence of all characters 
    // in a hash_array 
    for (int i = 0; i < n ; i++) 
        hash_str1[str1[i]-'a']++; 

    // Store the occurrence of all characters 
    // in a hash_array 
    int count = 0; 
    for (int i = 0; i < n ; i++) 
    { 
        if (hash_str1[str2[i]-'a'] > 0) 
            hash_str1[str2[i]-'a']--; 
        else
            count++; 

        if (count > k) 
            return false; 
    } 

    // Return true if count is less than or 
    // equal to k 
    return true; 
} 

// Driver code 
int main() 
{ 
    string str1 = "fodr"; 
    string str2 = "gork"; 
    int k = 2; 
    if (areKAnagrams(str1, str2, k) == true) 
        cout << "Yes"; 
    else
        cout << "No"; 
    return 0; 
} 

```

## Java

```java

// Optimized Java program to check if two strings 
// are k anagram or not. 
public class GFG { 

    static final int MAX_CHAR = 26; 

    // Function to check if str1 and str2 are k-anagram 
    // or not 
    static boolean areKAnagrams(String str1, String str2,  
                                                  int k) 
    { 
        // If both strings are not of equal 
        // length then return false 
        int n = str1.length(); 
        if (str2.length() != n) 
            return false; 

        int[] hash_str1 = new int[MAX_CHAR]; 

        // Store the occurrence of all characters 
        // in a hash_array 
        for (int i = 0; i < n ; i++) 
            hash_str1[str1.charAt(i)-'a']++; 

        // Store the occurrence of all characters 
        // in a hash_array 
        int count = 0; 
        for (int i = 0; i < n ; i++) 
        { 
            if (hash_str1[str2.charAt(i)-'a'] > 0) 
                hash_str1[str2.charAt(i)-'a']--; 
            else
                count++; 

            if (count > k) 
                return false; 
        } 

        // Return true if count is less than or 
        // equal to k 
        return true; 
    } 

    // Driver code 
    public static void main(String args[]) 
    { 
        String str1 = "fodr"; 
        String str2 = "gork"; 
        int k = 2; 
        if (areKAnagrams(str1, str2, k) == true) 
            System.out.println("Yes"); 
        else
            System.out.println("No"); 
    } 
} 
// This code is contributed by Sumit Ghosh 

```

## Python3

```py

# Optimized Python3 program  
# to check if two strings 
# are k anagram or not. 
MAX_CHAR = 26; 

# Function to check if str1  
# and str2 are k-anagram or not 
def areKAnagrams(str1, str2, k): 
    # If both strings are  
    # not of equal length  
    # then return false 

    n = len(str1); 
    if (len(str2) != n): 
        return False; 

    hash_str1 = [0]*(MAX_CHAR); 

    # Store the occurrence of  
    # all characters in a hash_array 
    for i in range(n): 
        hash_str1[ord(str1[i]) - ord('a')]+=1; 

    # Store the occurrence of all  
    # characters in a hash_array 
    count = 0; 
    for i in range(n): 
        if (hash_str1[ord(str2[i]) - ord('a')] > 0): 
            hash_str1[ord(str2[i]) - ord('a')]-=1; 
        else: 
            count+=1; 

        if (count > k): 
            return False; 

    # Return true if count is  
    # less than or equal to k 
    return True; 

# Driver code 
str1 = "fodr"; 
str2 = "gork"; 
k = 2; 
if (areKAnagrams(str1, str2, k) == True): 
    print("Yes"); 
else: 
    print("No"); 

# This code is contributed by mits 

```

## C#

```cs

// Optimized C# program to check if two strings 
// are k anagram or not. 
using System; 

 class GFG { 

    static  int MAX_CHAR = 26; 

    // Function to check if str1 and str2 are k-anagram 
    // or not 
    static bool areKAnagrams(String str1, String str2,  
                                                int k) 
    { 
        // If both strings are not of equal 
        // [i] then return false 
        int n = str1.Length; 
        if (str2.Length != n) 
            return false; 

        int[] hash_str1 = new int[MAX_CHAR]; 

        // Store the occurrence of all characters 
        // in a hash_array 
        for (int i = 0; i < n ; i++) 
            hash_str1[str1[i]-'a']++; 

        // Store the occurrence of all characters 
        // in a hash_array 
        int count = 0; 
        for (int i = 0; i < n ; i++) 
        { 
            if (hash_str1[str2[i]-'a'] > 0) 
                hash_str1[str2[i]-'a']--; 
            else
                count++; 

            if (count > k) 
                return false; 
        } 

        // Return true if count is less than or 
        // equal to k 
        return true; 
    } 

    // Driver code 
     static void Main() 
    { 
        String str1 = "fodr"; 
        String str2 = "gork"; 
        int k = 2; 

        if (areKAnagrams(str1, str2, k) == true) 
            Console.Write("Yes"); 
        else
            Console.Write("No"); 
    } 
} 
// This code is contributed by Anuj_67 

```

## PHP

```php

<?php 
// Optimized PHP program  
// to check if two strings 
// are k anagram or not. 
$MAX_CHAR = 26; 

// Function to check if str1  
// and str2 are k-anagram or not 
function areKAnagrams($str1,  
                      $str2, $k) 
{ 
    global $MAX_CHAR; 
    // If both strings are  
    // not of equal length  
    // then return false 

    $n = strlen($str1); 
    if (strlen($str2) != $n) 
        return false; 

    $hash_str1 = array(0); 

    // Store the occurrence of  
    // all characters in a hash_array 
    for ($i = 0; $i < $n ; $i++) 
        $hash_str1[$str1[$i] - 'a']++; 

    // Store the occurrence of all  
    // characters in a hash_array 
    $count = 0; 
    for ($i = 0; $i < $n ; $i++) 
    { 
        if ($hash_str1[$str2[$i] - 'a'] > 0) 
            $hash_str1[$str2[$i] - 'a']--; 
        else
            $count++; 

        if ($count > $k) 
            return false; 
    } 

    // Return true if count is  
    // less than or equal to k 
    return true; 
} 

// Driver code 
$str1 = "fodr"; 
$str2 = "gork"; 
$k = 2; 
if (areKAnagrams($str1, $str2, $k) == true) 
    echo "Yes"; 
else
    echo "No"; 

// This code is contributed by ajit 
?> 

```

**Output:**

```
Yes

```

**方法 3**：

*   在这种方法中，其思想是初始化一个数组或一个列表，而基本情况将是检查字符串，如果它们的长度不同，则它们不能构成一个字谜。

*   否则，将字符串转换为字符数组并对其进行排序。

*   然后迭代直到字符串的长度，如果字符不相等，则将其添加到列表中，并检查列表大小是否小于等于 K，则有可能形成 K 字形符号，否则就不能形成。

下面是上述方法的实现：

## Java

```java

// Java program for the above approach 
import java.util.*; 
class GFG{ 

// Function to check k  
// anagram of two strings 
public static boolean kAnagrams(String str1, 
                                String str2, int k) 
{ 
    int flag = 0; 

    List<Character> list = new ArrayList<>(); 

    // First Condition: If both the  
    // strings have different length ,  
    // then they cannot form anagram 
    if (str1.length() != str2.length()) 
        System.exit(0); 

    // Coverting str1 to Character Array arr1 
    char arr1[] = str1.toCharArray(); 

    // Coverting str2 to Character Array arr2 
    char arr2[] = str2.toCharArray(); 

    // Sort arr1 in increasing order 
    Arrays.sort(arr1); 

    // Sort arr2 in increasing order 
    Arrays.sort(arr2); 

    // Iterate till str1.length() 
    for (int i = 0; i < str1.length(); i++) 
    { 

        // Condition if arr1[i] is  
        // not equal to arr2[i] 
        // then add it to list 
        if (arr1[i] != arr2[i])  
        { 
            list.add(arr2[i]); 
        } 
    } 

    // Condition to check if  
    // strings for K-anagram or not  
    if (list.size() <= k) 
        flag = 1; 

    if (flag == 1) 
        return true; 
    else
        return false; 
} 

// Driver Code 
public static void main(String[] args) 
{ 

    String str1 = "fodr"; 
    String str2 = "gork"; 
    int k = 2; 

    // Function Call 
    kAnagrams(str1, str2, k); 
    if (kAnagrams(str1, str2, k) == true) 
        System.out.println("Yes"); 
    else
        System.out.println("No"); 
} 
} 

```

**输出**：

```
Yes

```

本文由 **[Sahil Chhabra（akku）](https://practice.geeksforgeeks.org/user-profile.php?user=sahil_coder)** 贡献。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

