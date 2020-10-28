# 具有卢卡斯序列

> 原文：[https://www.geeksforgeeks.org/string-with-frequency-of-characters-in-lucas-sequence/](https://www.geeksforgeeks.org/string-with-frequency-of-characters-in-lucas-sequence/)

中字符频率的字符串

给定包含小写英文字母的字符串“ str”，任务是查找字符串字符的频率是否按 Lucas 顺序排列。 您可以随意安排频率编号，以形成卢卡斯序列。 如果可能，请打印*是*，否则打印 *NO* 。

[卢卡斯序列](https://www.geeksforgeeks.org/lucas-numbers/)。

**注意**：必须使用所有频率检查它们是否在 Lucas 序列中。

**示例**：

> **输入**：str =“ gggeek”
> **输出**：是
> 的频率'g'= 3
> 的频率'e'= 2
> 的频率 'k'= 1
> 这些频率可以安排为形成卢卡斯序列的前 3 个项{2，1，3}。
> 
> **输入**：str =“ geeksforgeeks”
> **输出**：否

**方法**：

*   使用[映射 STL](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/) 将每个字符的频率存储在矢量中。 然后将向量排序。

*   由于卢卡斯序列的前两个数字为“ 2”和“ 1”，因此将第一个向量的第一个和第二个元素分别更改为“ 2”和“ 1”。 但是，只有在向量中存在“ 1”和“ 2”的情况下，才可以进行更改。 如果不存在，则频率永远不会处于卢卡斯序列中并输出 NO。

*   然后，制作另一个向量。 令第一个向量的大小为 n。

*   在第二个向量中插入第一个“ n”卢卡斯数字。

*   然后，比较两个向量中的每个元素。 如果两个向量都相同，则输出“是”，否则输出“否”。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of 
// the approach 
#include <bits/stdc++.h> 
using namespace std; 

// function that checks 
// if the frequencies 
// are in Lucas sequence. 
string lucas_sequence(string s, int n) 
{ 
    // map is used to store 
    // character frequencies 
    map<char, int> m; 
    for (int i = 0; i < n; i++) { 
        if (m.find(s[i]) == m.end()) 
            m[s[i]] = 1; 
        else
            m[s[i]]++; 
    } 

    vector<int> v1, v2; 

    map<char, int>::iterator it; 

    // frequencies are extracted from 
    // map and stored in vector v1 
    for (it = m.begin(); it != m.end(); it++) 
        v1.push_back((*it).second); 

    // vector v1 elements are sorted, 
    // but first and second element are 
    // changed to '2' and '1' respectively, 
    // only if '1' and '2' are present in the vector. 
    sort(v1.begin(), v1.end()); 
    if (v1[0] == 1 && v1[1] == 2) { 
        v1[0] = 2; 
        v1[1] = 1; 
    } 
    else
        return "NO"; 

    // a and b are first and 
    // second terms of 
    // Lucas sequence 
    int a = 2, b = 1; 
    int c; 
    v2.push_back(a); 
    v2.push_back(b); 

    // v2 contains Lucas sequence 
    for (int i = 0; i < v1.size() - 2; i++) { 
        v2.push_back(a + b); 
        c = a + b; 
        a = b; 
        b = c; 
    } 
    int flag = 1; 

    // both vectors are compared 
    for (int i = 0; i < v1.size(); i++) { 
        if (v1[i] != v2[i]) { 
            flag = 0; 
            break; 
        } 
    } 

    if (flag == 1) 
        return "YES"; 
    else
        return "NO"; 
} 

// Driver code 
int main() 
{ 
    string s = "oooeeeeqkk"; 
    int n = s.length(); 
    cout << lucas_sequence(s, n); 
    return 0; 
} 

```

## Java

```java

// Java implementation of the approach  
import java.util.Collections; 
import java.util.HashMap; 
import java.util.Vector; 

class GFG  
{ 

    // function that checks 
    // if the frequencies 
    // are in Lucas sequence. 
    static String lucas_sequence(String s,  
                                 int n)  
    { 

        // map is used to store 
        // character frequencies 
        HashMap<Character,  
                Integer> m = new HashMap<>(); 
        for (int i = 0; i < n; i++) 
            m.put(s.charAt(i),  
            m.get(s.charAt(i)) == null ? 1 :  
            m.get(s.charAt(i)) + 1); 

        Vector<Integer> v1 = new Vector<>(); 
        Vector<Integer> v2 = new Vector<>(); 

        // frequencies are extracted from 
        // map and stored in vector v1 
        for (HashMap.Entry<Character,  
                           Integer> entry : m.entrySet()) 
            v1.add(entry.getValue()); 

        // vector v1 elements are sorted, 
        // but first and second element are 
        // changed to '2' and '1' respectively, 
        // only if '1' and '2' are present in the vector. 
        Collections.sort(v1); 
        if (v1.elementAt(0) == 1 && 
            v1.elementAt(1) == 2)  
        { 
            v1.set(0, 2); 
            v1.set(1, 1); 
        }  
        else
            return "NO"; 

        // a and b are first and 
        // second terms of 
        // Lucas sequence 
        int a = 2, b = 1; 
        int c; 
        v2.add(a); 
        v2.add(b); 

        // v2 contains Lucas sequence 
        for (int i = 0; i < v1.size() - 2; i++) 
        { 
            v2.add(a + b); 
            c = a + b; 
            a = b; 
            b = c; 
        } 
        int flag = 1; 

        // both vectors are compared 
        for (int i = 0; i < v1.size(); i++)  
        { 
            if (v1.elementAt(i) != v2.elementAt(i)) 
            { 
                flag = 0; 
                break; 
            } 
        } 

        if (flag == 1) 
            return "YES"; 
        else
            return "NO"; 
    } 

    // Driver Code 
    public static void main(String[] args)  
    { 
        String s = "oooeeeeqkk"; 
        int n = s.length(); 
        System.out.println(lucas_sequence(s, n)); 
    } 
} 

// This code is contributed by 
// sanjeev2552 

```

## Python3

```py

# Python3 implementation of the approach  
from collections import defaultdict 

# Function that checks if the  
# frequencies are in Lucas sequence.  
def lucas_sequence(s, n):  

    # map is used to store  
    # character frequencies  
    m = defaultdict(lambda:0) 

    for i in range(0, n):  
        m[s[i]] += 1    

    v1, v2 = [], []  

    # frequencies are extracted from  
    # map and stored in vector v1  
    for it in m:  
        v1.append(m[it])  

    # vector v1 elements are sorted, but 
    # first and second element are changed  
    # to '2' and '1' respectively, only if  
    # '1' and '2' are present in the vector.  
    v1.sort()  
    if v1[0] == 1 and v1[1] == 2:  
        v1[0], v1[1] = 2, 1

    else: 
        return "NO"

    # a and b are first and second terms  
    # of Lucas sequence  
    a, b = 2, 1
    v2.append(a)  
    v2.append(b)  

    # v2 contains Lucas sequence  
    for i in range(0, len(v1) - 2):  
        v2.append(a + b)  
        a, b = b, a + b  

    flag = 1

    # both vectors are compared  
    for i in range(0, len(v1)):  
        if v1[i] != v2[i]:  
            flag = 0
            break

    if flag == 1:  
        return "YES"
    else: 
        return "NO"

# Driver code  
if __name__ == "__main__": 

    s = "oooeeeeqkk"
    n = len(s)  
    print(lucas_sequence(s, n))  

# This code is contributed by Rituraj Jain 

```

## C#

```cs

// C# implementation of the approach 
using System; 
using System.Collections.Generic;  

class GFG  
{ 

    // function that checks 
    // if the frequencies 
    // are in Lucas sequence. 
    static String lucas_sequence(String s,  
                                 int n)  
    { 

        // map is used to store 
        // character frequencies 
        Dictionary<char, 
                   int> m = new Dictionary<char,  
                                           int>(); 
        for (int i = 0; i < n; i++) 
        { 
            if(m.ContainsKey(s[i])) 
            { 
                m[s[i]] = m[s[i]] + 1; 
            } 
            else
            { 
                m.Add(s[i], 1); 
            } 
        } 
        List<int> v1 = new List<int>(); 
        List<int> v2 = new List<int>(); 

        // frequencies are extracted from 
        // map and stored in vector v1 
        foreach(KeyValuePair<char, 
                             int> entry in m) 
            v1.Add(entry.Value); 

        // vector v1 elements are sorted, 
        // but first and second element are 
        // changed to '2' and '1' respectively, 
        // only if '1' and '2' are present in the vector. 
        v1.Sort(); 
        if (v1[0] == 1 && 
            v1[1] == 2)  
        { 
            v1[0] = 2; 
            v1[1] = 1; 
        }  
        else
            return "NO"; 

        // a and b are first and 
        // second terms of 
        // Lucas sequence 
        int a = 2, b = 1; 
        int c; 
        v2.Add(a); 
        v2.Add(b); 

        // v2 contains Lucas sequence 
        for (int i = 0; i < v1.Count - 2; i++) 
        { 
            v2.Add(a + b); 
            c = a + b; 
            a = b; 
            b = c; 
        } 
        int flag = 1; 

        // both vectors are compared 
        for (int i = 0; i < v1.Count; i++)  
        { 
            if (v1[i] != v2[i]) 
            { 
                flag = 0; 
                break; 
            } 
        } 

        if (flag == 1) 
            return "YES"; 
        else
            return "NO"; 
    } 

    // Driver Code 
    public static void Main(String[] args)  
    { 
        String s = "oooeeeeqkk"; 
        int n = s.Length; 
        Console.WriteLine(lucas_sequence(s, n)); 
    } 
} 

// This code is contributed by Rajput-Ji 

```

**Output:**

```
YES

```



* * *

* * *



