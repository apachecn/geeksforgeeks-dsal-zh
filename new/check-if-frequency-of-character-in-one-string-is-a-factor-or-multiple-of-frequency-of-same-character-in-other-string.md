# 检查一个字符串中字符的频率是否是另一字符串中相同字符的频率的因数或倍数

> 原文：[https://www.geeksforgeeks.org/check-if-frequency-of-character-in-one-string-is-a-factor-or-multiple-of-frequency-of-same-character-in-other-string/](https://www.geeksforgeeks.org/check-if-frequency-of-character-in-one-string-is-a-factor-or-multiple-of-frequency-of-same-character-in-other-string/)

给定两个字符串，任务是检查一个字符串中一个字符（每个字符）的频率是另一个字符串中的倍数还是一个因数。 如果是，则输出“是”，否则输出“否”。

**示例**：

> **输入**：s1 =“ aabccd”，s2 =“ bbbaaaacc”
> **输出**：是
> s1 和 s2 中“ a”的频率分别为 2 和 4，并且 2 是 4 的因数。
> s1 和 s2 中的'b'频率分别为 1 和 3，而 1 是 3 的因数。
> s1 和 s2 中的'c'频率相同。
> s1 和 s2 中“ d”的频率分别为 1 和 0，但 0 是每个数字的倍数，因此可以满足。
> 因此，答案为是。
> 
> **输入**：s1 =“ hhdwjwqq”，s2 =“ qwjdddhhh”
> **输出**：否

**方法**：

1.  将字符频率存储在第一个映射 STL 中的 s1 中。

2.  将字符频率存储在第二个地图 STL 中的 s2 中。

3.  令第一个图中的字符频率为 F1。 让我们还假设第二个映射中此字符的频率为 F2。

4.  检查 F1％F2 和 F2％F1（模运算）。 如果其中任何一个为 0，则满足条件。

5.  检查所有字符。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of above approach 
#include <bits/stdc++.h> 
using namespace std; 

// Function that checks if the frequency of character 
// are a factor or multiple of each other 
bool multipleOrFactor(string s1, string s2) 
{ 
    // map store frequency of each character 
    map<char, int> m1, m2; 
    for (int i = 0; i < s1.length(); i++) 
        m1[s1[i]]++; 

    for (int i = 0; i < s2.length(); i++) 
        m2[s2[i]]++; 

    map<char, int>::iterator it; 

    for (it = m1.begin(); it != m1.end(); it++) { 

        // if any frequency is 0, then continue 
        // as condition is satisfied 
        if (m2.find((*it).first) == m2.end()) 
            continue; 

        // if factor or multiple, then condition satified 
        if (m2[(*it).first] % (*it).second == 0 
            || (*it).second % m2[(*it).first] == 0) 
            continue; 

        // if condition not satisfied 
        else
            return false; 
    } 
} 

// Driver code 
int main() 
{ 
    string s1 = "geeksforgeeks"; 
    string s2 = "geeks"; 

    multipleOrFactor(s1, s2) ? cout << "YES"
                             : cout << "NO"; 

    return 0; 
} 

```

## Java

```java

// Java implementation of above approach 
import java.util.HashMap; 

class GFG  
{ 

    // Function that checks if the frequency of character 
    // are a factor or multiple of each other 
    public static boolean multipleOrFactor(String s1, String s2) 
    { 

        // map store frequency of each character 
        HashMap<Character, Integer> m1 = new HashMap<>(); 
        HashMap<Character, Integer> m2 = new HashMap<>(); 

        for (int i = 0; i < s1.length(); i++)  
        { 
            if (m1.containsKey(s1.charAt(i))) 
            { 
                int x = m1.get(s1.charAt(i)); 
                m1.put(s1.charAt(i), ++x); 
            }  
            else
                m1.put(s1.charAt(i), 1); 
        } 

        for (int i = 0; i < s2.length(); i++) 
        { 
            if (m2.containsKey(s2.charAt(i)))  
            { 
                int x = m2.get(s2.charAt(i)); 
                m2.put(s2.charAt(i), ++x); 
            }  
            else
                m2.put(s2.charAt(i), 1); 
        } 

        for (HashMap.Entry<Character, Integer> entry : m1.entrySet())  
        { 

            // if any frequency is 0, then continue 
            // as condition is satisfied 
            if (!m2.containsKey(entry.getKey())) 
                continue; 

            // if factor or multiple, then condition satified 
            if (m2.get(entry.getKey()) != null &&  
                (m2.get(entry.getKey()) % entry.getValue() == 0
                || entry.getValue() % m2.get(entry.getKey()) == 0)) 
                continue; 

            // if condition not satisfied 
            else
                return false; 
        } 
        return true; 
    } 

    // Driver code 
    public static void main(String[] args)  
    { 
        String s1 = "geeksforgeeks", s2 = "geeks"; 
        if (multipleOrFactor(s1, s2)) 
            System.out.println("Yes"); 
        else
            System.out.println("No"); 

    } 
} 

// This code is contributed by 
// sanjeev2552 

```

## Python3

```py

# Python3 implementation of above approach  

> 原文：[https://www.geeksforgeeks.org/check-if-frequency-of-character-in-one-string-is-a-factor-or-multiple-of-frequency-of-same-character-in-other-string/](https://www.geeksforgeeks.org/check-if-frequency-of-character-in-one-string-is-a-factor-or-multiple-of-frequency-of-same-character-in-other-string/)
from collections import defaultdict 

# Function that checks if the frequency of  

> 原文：[https://www.geeksforgeeks.org/check-if-frequency-of-character-in-one-string-is-a-factor-or-multiple-of-frequency-of-same-character-in-other-string/](https://www.geeksforgeeks.org/check-if-frequency-of-character-in-one-string-is-a-factor-or-multiple-of-frequency-of-same-character-in-other-string/)
# character are a factor or multiple of each other  

> 原文：[https://www.geeksforgeeks.org/check-if-frequency-of-character-in-one-string-is-a-factor-or-multiple-of-frequency-of-same-character-in-other-string/](https://www.geeksforgeeks.org/check-if-frequency-of-character-in-one-string-is-a-factor-or-multiple-of-frequency-of-same-character-in-other-string/)
def multipleOrFactor(s1, s2):  

    # map store frequency of each character  
    m1 = defaultdict(lambda:0) 
    m2 = defaultdict(lambda:0) 
    for i in range(0, len(s1)):  
        m1[s1[i]] += 1

    for i in range(0, len(s2)):  
        m2[s2[i]] += 1

    for it in m1:   

        # if any frequency is 0, then continue  
        # as condition is satisfied  
        if it not in m2:  
            continue 

        # if factor or multiple, then condition satified  
        if (m2[it] % m1[it] == 0 or 
            m1[it] % m2[it] == 0):  
            continue 

        # if condition not satisfied  
        else: 
            return False

    return True

# Driver code  

> 原文：[https://www.geeksforgeeks.org/check-if-frequency-of-character-in-one-string-is-a-factor-or-multiple-of-frequency-of-same-character-in-other-string/](https://www.geeksforgeeks.org/check-if-frequency-of-character-in-one-string-is-a-factor-or-multiple-of-frequency-of-same-character-in-other-string/)
if __name__ == "__main__": 

    s1 = "geeksforgeeks" 
    s2 = "geeks" 

    if multipleOrFactor(s1, s2): print("YES") 
    else: print("NO")  

# This code is contributed by Rituraj Jain 

> 原文：[https://www.geeksforgeeks.org/check-if-frequency-of-character-in-one-string-is-a-factor-or-multiple-of-frequency-of-same-character-in-other-string/](https://www.geeksforgeeks.org/check-if-frequency-of-character-in-one-string-is-a-factor-or-multiple-of-frequency-of-same-character-in-other-string/)

```

## C#

```cs

// C# implementation of the approach 
using System; 
using System.Collections.Generic; 

class GFG  
{ 

    // Function that checks if the  
    // frequency of character are  
    // a factor or multiple of each other 
    public static Boolean multipleOrFactor(String s1,  
                                           String s2) 
    { 

        // map store frequency of each character 
        Dictionary<char, int> m1 = new Dictionary<char, int>(); 
        Dictionary<char, int> m2 = new Dictionary<char, int>(); 

        for (int i = 0; i < s1.Length; i++)  
        { 
            if (m1.ContainsKey(s1[i])) 
            { 
                var x = m1[s1[i]]; 
                m1[s1[i]]= ++x; 
            }  
            else
                m1.Add(s1[i], 1); 
        } 

        for (int i = 0; i < s2.Length; i++) 
        { 
            if (m2.ContainsKey(s2[i]))  
            { 
                var x = m2[s2[i]]; 
                m2[s2[i]]= ++x; 
            }  
            else
                m2.Add(s2[i], 1); 
        } 

        foreach(KeyValuePair<char, int> entry in m1) 
        { 

            // if any frequency is 0, then continue 
            // as condition is satisfied 
            if (!m2.ContainsKey(entry.Key)) 
                continue; 

            // if factor or multiple, then condition satified 
            if (m2[entry.Key] != 0 &&  
               (m2[entry.Key] % entry.Value == 0 ||  
                   entry.Value % m2[entry.Key] == 0)) 
                continue; 

            // if condition not satisfied 
            else
                return false; 
        } 
        return true; 
    } 

    // Driver code 
    public static void Main(String[] args)  
    { 
        String s1 = "geeksforgeeks", s2 = "geeks"; 
        if (multipleOrFactor(s1, s2)) 
            Console.WriteLine("Yes"); 
        else
            Console.WriteLine("No"); 
    } 
} 

// This code is contributed by PrinciRaj1992  

```

**Output:**

```
YES

```



* * *

* * *



