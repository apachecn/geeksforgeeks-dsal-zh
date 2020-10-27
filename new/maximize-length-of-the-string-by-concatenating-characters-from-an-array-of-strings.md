# 通过连接字符串数组中的字符来最大化字符串的长度

给定字符串数组 **arr []** ，任务是找到可以通过串联给定数组的子序列而生成的不同字符字符串的最大可能长度。

**示例：**

> **输入：** arr [] = {“ ab”，“ cd”，“ ab”}
> **输出：** 4
> **说明：** ]所有可能的组合为{“”，“ ab”，“ cd”，“ abcd”，“ cdab”}。
> 因此，最大长度可能是 4。
> 
> **输入：** arr [] = {“ abcdefgh”}
> **输出：** 8
> **说明：**
> 所有可能的组合是：“” ，“ abcdefgh”。
> 因此，最大长度为 8。

**方法：**的想法是使用[递归](https://www.geeksforgeeks.org/recursion/)。
请按照以下步骤解决问题：

*   从左到右迭代，并将每个字符串视为可能的起始子字符串。
*   初始化 [HashSet](http://www.geeksforgeeks.org/hashset-in-java/) ，以存储到目前为止遇到的不同字符。
*   一旦选择了一个字符串作为起始子字符串，请检查是否还有其余的字符串（如果它仅包含以前没有出现过的字符）。 将此字符串作为子字符串追加到正在生成的当前字符串中。
*   执行上述步骤后，打印已生成的字符串的最大长度。

下面是上述方法的实现：

## C++

```cpp

// C++ Program to implement 
// the above approach 
#include <bits/stdc++.h> 
using namespace std; 

// Function to check if all the 
// string characters are unique 
bool check(string s) 
{ 

    set<char> a; 

    // Check for repetation in 
    // characters 
    for (auto i : s) { 
        if (a.count(i)) 
            return false; 
        a.insert(i); 
    } 

    return true; 
} 

// Funcyion to generate all possible strings 
// from the given array 
vector<string> helper(vector<string>& arr, 
                    int ind) 
{ 

    // Base case 
    if (ind == arr.size()) 
        return { "" }; 

    // Consider every string as 
    // a starting substring and 
    // store the generated string 
    vector<string> tmp 
        = helper(arr, ind + 1); 

    vector<string> ret(tmp.begin(), 
                    tmp.end()); 

    // Add current string to result of 
    // other strings and check if 
    // characters are unique or not 
    for (auto i : tmp) { 
        string test = i + arr[ind]; 
        if (check(test)) 
            ret.push_back(test); 
    } 

    return ret; 
} 

// Function to find the maximum 
// possible length of a string 
int maxLength(vector<string>& arr) 
{ 
    vector<string> tmp = helper(arr, 0); 

    int len = 0; 

    // Return max length possible 
    for (auto i : tmp) { 
        len = len > i.size() 
                ? len 
                : i.size(); 
    } 

    // Return the answer 
    return len; 
} 

// Driver Code 
int main() 
{ 
    vector<string> s; 
    s.push_back("abcdefgh"); 

    cout << maxLength(s); 

    return 0; 
} 

```

## Java

```java

// Java program to implement  
// the above approach 
import java.util.*;
import java.lang.*;

class GFG{

// Function to check if all the
// string characters are unique 
static boolean check(String s) 
{ 
    HashSet<Character> a = new HashSet<>(); 

    // Check for repetation in 
    // characters 
    for(int i = 0; i < s.length(); i++) 
    { 
        if (a.contains(s.charAt(i))) 
        { 
            return false; 
        } 
        a.add(s.charAt(i)); 
    } 
    return true; 
} 

// Function to generate all possible 
//  strings from the given array 
static ArrayList<String> helper(ArrayList<String> arr, 
                                int ind) 
{ 
    ArrayList<String> fin = new ArrayList<>();
    fin.add("");

    // Base case 
    if (ind == arr.size() )
        return fin; 

    // Consider every string as 
    // a starting substring and 
    // store the generated string 
    ArrayList<String> tmp = helper(arr, ind + 1); 

    ArrayList<String> ret = new ArrayList<>(tmp); 

    // Add current string to result of 
    // other strings and check if 
    // characters are unique or not 
    for(int i = 0; i < tmp.size(); i++) 
    { 
        String test = tmp.get(i) + 
                      arr.get(ind); 

        if (check(test)) 
            ret.add(test); 
    } 
    return ret; 
} 

// Function to find the maximum 
// possible length of a string 
static int maxLength(ArrayList<String> arr) 
{ 
    ArrayList<String> tmp = helper(arr, 0); 

    int len = 0; 

    // Return max length possible 
    for(int i = 0; i < tmp.size(); i++) 
    { 
        len = len > tmp.get(i).length() ? len :  
                    tmp.get(i).length(); 
    } 

    // Return the answer 
    return len; 
}

// Driver code
public static void main (String[] args)
{
    ArrayList<String> s = new ArrayList<>(); 
    s.add("abcdefgh"); 

    System.out.println(maxLength(s)); 
}
}

// This code is contributed by offbeat

```

## C#

```cs

// C# program to implement 
// the above approach 
using System; 
using System.Collections; 
using System.Collections.Generic; 
using System.Text; 

class GFG{ 

// Function to check if all the 
// string characters are unique 
static bool check(string s) 
{ 

    HashSet<char> a = new HashSet<char>(); 

    // Check for repetation in 
    // characters 
    for(int i = 0; i < s.Length; i++) 
    { 
        if (a.Contains(s[i])) 
        { 
            return false; 
        } 
        a.Add(s[i]); 
    } 
    return true; 
} 

// Funcyion to generate all possible 
// strings from the given array 
static ArrayList helper(ArrayList arr, 
                        int ind) 
{ 

    // Base case 
    if (ind == arr.Count) 
        return new ArrayList(){""}; 

    // Consider every string as 
    // a starting substring and 
    // store the generated string 
    ArrayList tmp = helper(arr, ind + 1); 

    ArrayList ret = new ArrayList(tmp); 

    // Add current string to result of 
    // other strings and check if 
    // characters are unique or not 
    for(int i = 0; i < tmp.Count; i++) 
    { 
        string test = (string)tmp[i] + 
                    (string)arr[ind]; 

        if (check(test)) 
            ret.Add(test); 
    } 
    return ret; 
} 

// Function to find the maximum 
// possible length of a string 
static int maxLength(ArrayList arr) 
{ 
    ArrayList tmp = helper(arr, 0); 

    int len = 0; 

    // Return max length possible 
    for(int i = 0; i < tmp.Count; i++) 
    { 
        len = len > ((string)tmp[i]).Length ? len : 
                    ((string)tmp[i]).Length; 
    } 

    // Return the answer 
    return len; 
} 

// Driver Code 
public static void Main(string[] args) 
{ 
    ArrayList s = new ArrayList(); 
    s.Add("abcdefgh"); 

    Console.Write(maxLength(s)); 
} 
} 

// This code is contributed by rutvik_56 

```

**Output:** 

```
8

```

***时间复杂度：** O（2 <sup>N</sup> ）*
***辅助空间：** O（N * 2 <sup>N</sup> ）*



* * *

* * *



