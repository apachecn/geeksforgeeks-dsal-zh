# 检查字符串是否包含具有超过 K 个有效字符的任何索引

> 原文：[https://www.geeksforgeeks.org/check-if-a-string-contains-any-index-with-more-than-k-active-characters/](https://www.geeksforgeeks.org/check-if-a-string-contains-any-index-with-more-than-k-active-characters/)

给定一个包含小写英文字母的字符串 **S** 和一个整数 **K** ，任务是查找包含超过 **K** 个以上有效字符串的任何索引 字符。 如果找到，则打印**是**。 否则，打印**否**。

> 任何索引的**活动字符**的计数是具有在当前索引之前或当前索引中先前出现以及在当前索引之后或之后最后出现的字符数。

**示例**：

> **输入**：S =“ aabbcd”，K = 1
> **输出**：否
> **说明**：
> 索引 1：有效字符：
> 索引 2：活动字符：a
> 索引 3：活动字符：b
> 索引 4：活动字符：b
> 索引 5：活动字符：c
> 索引 6：活动字符：d
> 字符串中任何索引处的活动字符不得超过一个。
> 
> **输入**：S =“ aabbcdca”，K = 2
> **输出**：是
> **说明**：
> 索引 1：有效字符：a
> 索引 2：活动字符：a
> 索引 3：活动字符：a，b
> 索引 4：活动字符：a，b
> 索引 5：活动字符：a，c
> 索引 6：活动字符： **a，c，d** 。
> 因此，存在一个索引，其中包含两个以上的活动字符。

**方法**：[

]请按照以下步骤解决问题：

*   这个想法是将出现在字符串中的每个字符的最后出现都存储在 [Map](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/) 中。

*   遍历字符串并继续将活动字母存储在[设置](https://www.geeksforgeeks.org/set-in-java/)中。

*   如果**设置**的大小超过 **K** ，则打印**为“是”** 。

*   否则，检查当前索引是否是当前字符的最后一次出现。 如果是这样，请从 **Set** 中删除字符。

*   最后，如果没有找到超过 **K** 个活动字符的索引，则打印**“否”** 。

下面是上述方法的实现：

## C++

```cpp

// C++ Program to implement 
// the above approach 
#include <bits/stdc++.h> 
using namespace std; 

// Function to check if any index 
// contains more than K active characters 
string checkString(string s, int K) 
{ 

    int n = s.length(); 

    // Store the last occurrence of 
    // each character in the map. 
    unordered_map<char, int> mp; 

    for (int i = 0; i < n; i++) { 
        mp[s[i]] = i; 
    } 

    int cnt = 0, f = 0; 

    // Stores the active 
    // characters 
    unordered_set<int> st; 

    for (int i = 0; i < n; i++) { 

        // Insert the character 
        st.insert(s[i]); 

        // If the size of set 
        // exceeds K 
        if (st.size() > K) { 
            f = 1; 
            break; 
        } 

        // Remove the character from 
        // set if i is the last index 
        // of the current character 
        if (mp[s[i]] == i) 
            st.erase(s[i]); 
    } 

    return (f == 1 ? "Yes" : "No"); 
} 

// Driver Code 
int main() 
{ 

    string s = "aabbcdca"; 
    int k = 2; 
    cout << checkString(s, k); 
    return 0; 
} 

```

## Java

```java

// Java program to implement the 
// above approach 
import java.util.*; 

class GFG{ 

// Function to check if any index 
// contains more than K active characters 
static String checkString(String s, int K) 
{ 
    int n = s.length(); 

    // Store the last occurrence of 
    // each character in the map. 
    Map<Character,  
        Integer> mp = new HashMap<>(); 

    for(int i = 0; i < n; i++) 
    { 
        mp.put(s.charAt(i), i); 
    } 

    int cnt = 0, f = 0; 

    // Stores the active 
    // characters 
    Set<Character> st = new HashSet<>(); 

    for(int i = 0; i < n; i++) 
    { 

        // Insert the character 
        st.add(s.charAt(i)); 

        // If the size of set 
        // exceeds K 
        if (st.size() > K) 
        { 
            f = 1; 
            break; 
        } 

        // Remove the character from 
        // set if i is the last index 
        // of the current character 
        if (mp.get(s.charAt(i)) == i) 
            st.remove(s.charAt(i)); 
    } 
    return (f == 1 ? "Yes" : "No"); 
} 

// Driver code 
public static void main(String[] args) 
{ 
    String s = "aabbcdca"; 
    int k = 2; 

    System.out.println(checkString(s, k)); 
} 
} 

// This code is contributed by offbeat 

```

## Python3

```py

# Python3 program to implement  
# the above approach  

# Function to check if any index  
# contains more than K active characters  
def checkString(s, K): 

    n = len(s) 

    # Store the last occurrence of  
    # each character   
    dict = {} 

    for i in range(n): 
        dict[s[i]] = i; 

    # Stores the active  
    # characters  
    st = set() 

    for i in range(n): 

        # Insert the character  
        st.add(s[i]) 

        # If the size of set  
        # exceeds K  
        if len(st) > K: 
            print("Yes") 
            return

        # Remove the character from  
        # set if i is the last index  
        # of the current character  
        if dict[s[i]] == i: 
            st.remove(s[i]) 

    print("No") 

# Driver code 
s = "aabbcdca"
K = 2

checkString(s, K) 

# This code is contributed by vashisthamadhur2 

```

## C#

```cs

// C# program to implement the 
// above approach 
using System; 
using System.Collections.Generic; 

class GFG{ 

// Function to check if any index 
// contains more than K active characters 
static String checkString(String s, int K) 
{ 
    int n = s.Length; 

    // Store the last occurrence of 
    // each character in the map. 
    Dictionary<char,  
               int> mp = new Dictionary<char, 
                                        int>(); 

    for(int i = 0; i < n; i++) 
    { 
        if(mp.ContainsKey(s[i])) 
            mp[s[i]] = i; 
        else
            mp.Add(s[i], i); 
    } 

    int f = 0; 

    // Stores the active 
    // characters 
    HashSet<char> st = new HashSet<char>(); 

    for(int i = 0; i < n; i++) 
    { 

        // Insert the character 
        st.Add(s[i]); 

        // If the size of set 
        // exceeds K 
        if (st.Count > K) 
        { 
            f = 1; 
            break; 
        } 

        // Remove the character from 
        // set if i is the last index 
        // of the current character 
        if (mp[s[i]] == i) 
            st.Remove(s[i]); 
    } 
    return (f == 1 ? "Yes" : "No"); 
} 

// Driver code 
public static void Main(String[] args) 
{ 
    String s = "aabbcdca"; 
    int k = 2; 

    Console.WriteLine(checkString(s, k)); 
} 
} 

// This code is contributed by shikhasingrajput

```

**Output:** 

```
Yes

```

***时间复杂度**：O（N）*

***辅助空间**：O（N）*



* * *

* * *



