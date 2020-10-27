# 根据另一个字符串

定义的字母顺序对字符串数组进行排序

给定字符串 **str** 和字符串 **strArr []** 的数组，任务是根据 **str** 定义的字母顺序对数组进行排序。
**注意：** **str** 和 **strArr []** 中的每个字符串仅由小写字母组成。

**示例：**

> **输入：** str =“ fguecbdavwyxzhijklmnopqrst”，
> strArr [] = {“ geeksforgeeks”，“ is”，“ the”，“ best”，“ place”，“ for”，“ learning”}
> **输出：**最适合用于 geeksforgeeks 的学习地点是
> 
> **输入：** str =“ avdfghiwyxzjkecbmnopqrstul”，
> strArr [] = {“彩虹”，“包含”，“的”，“颜色”}
> **输出：**由 彩虹的颜色

**方法：**遍历 **str** 的每个字符，并将值存储在以**字符**作为**键**及其**索引[ 数组中的**作为**值**。
现在，此地图将充当字符的新字母顺序。 开始比较 **strArr []** 中的字符串，而不是补偿字符的 ASCII 值，而是比较映射到映射中那些特定字符的值，即，如果字符 **c1** 出现在字符之前 **str** 中的 **c2** ，然后是 **c1 < c2** 。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

// Map to store the characters with their order 
// in the new alphabetical order 
unordered_map<char, int> h; 

// Function that returns true if x < y 
// according to the new alphabetical order 
bool compare(string x, string y) 
{ 
    for (int i = 0; i < min(x.size(), y.size()); i++) { 
        if (h[x[i]] == h[y[i]]) 
            continue; 
        return h[x[i]] < h[y[i]]; 
    } 
    return x.size() < y.size(); 
} 

// Driver code 
int main() 
{ 
    string str = "fguecbdavwyxzhijklmnopqrst"; 
    vector<string> v{ "geeksforgeeks", "is", "the", 
                      "best", "place", "for", "learning" }; 

    // Store the order for each character 
    // in the new alphabetical sequence 
    h.clear(); 
    for (int i = 0; i < str.size(); i++)  
        h[str[i]] = i;     

    sort(v.begin(), v.end(), compare); 

    // Print the strings after sorting 
    for (auto x : v)  
        cout << x << " "; 

    return 0; 
} 

```

## Java

```java

// Java implementation of the approach 
import java.util.Arrays; 
import java.util.Comparator; 

public class GFG  
{ 
private static void sort(String[] strArr, String str) 
{ 
    Comparator<String> myComp = new Comparator<String>() 
    { 
        @Override
        public int compare(String a, String b)  
        { 
            for(int i = 0;  
                    i < Math.min(a.length(), 
                                 b.length()); i++) 
            { 
                if (str.indexOf(a.charAt(i)) == 
                    str.indexOf(b.charAt(i)))  
                { 
                    continue; 
                }  
                else if(str.indexOf(a.charAt(i)) > 
                        str.indexOf(b.charAt(i))) 
                { 
                    return 1; 
                }  
                else
                { 
                    return -1; 
                } 
            } 
            return 0; 
        } 
    }; 
    Arrays.sort(strArr, myComp); 
} 

// Driver Code 
public static void main(String[] args) 
{ 
    String str = "fguecbdavwyxzhijklmnopqrst"; 
    String[] strArr = {"geeksforgeeks", "is", "the", "best",  
                       "place", "for", "learning"}; 

    sort(strArr, str); 

    for(int i = 0; i < strArr.length; i++) 
    { 
        System.out.print(strArr[i] + " "); 
    } 
} 
} 

```

## Python3

```py

# Python3 implementation of the approach 

# Function to sort and print the array  
# according to the new alphabetical order 
def sortStringArray(s, a, n): 

    # Sort the array according to the new alphabetical order 
    a = sorted(a, key = lambda word: [s.index(c) for c in word]) 
    for i in a: 
        print(i, end =' ') 

# Driver code 
s = "fguecbdavwyxzhijklmnopqrst"
a = ["geeksforgeeks", "is", "the", "best", "place", "for", "learning"] 
n = len(a) 
sortStringArray(s, a, n) 

```

**Output:**

```
for geeksforgeeks best is learning place the

```

[![competitive-programming-img](img/5211864e7e7a28eeeb039fa5d6073a24.png)](https://practice.geeksforgeeks.org/courses/competitive-programming-live?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_cp)

* * *

* * *



