# 通过交换数组中的字符串偶对的前缀可以实现不同字符串的计数

> 原文：[https://www.geeksforgeeks.org/count-of-distinct-strings-possible-by-swapping-prefixes-of-pairs-of-strings-from-the-array/](https://www.geeksforgeeks.org/count-of-distinct-strings-possible-by-swapping-prefixes-of-pairs-of-strings-from-the-array/)

给定一个数组`string[]`，该数组由`N`个数字字符串，长度为`M`组成，任务是找到可以通过选择两个字符串的任意一个生成的不同字符串的数量，例如数组中的`i`和`j`，并在它们之间交换所有可能的前缀。

**注意**：由于答案可能非常大，请计算 1000000007 的模。

**示例**：

> **输入**：`N = 2, M = 3, string[] = {"112", "211"}`
>
> **输出**：4
>
> **说明**：
>
> 在字符串之间交换`"1"`和`"2"`会生成`"212"`和`"111"`。
>
> 在字符串之间交换`"11`和`"21"`会生成`"212"`和`"111"`。
>
> 在字符串之间交换`"112"`和"211"会生成`"211"`和`"112"`。
>
> 因此，生成了 4 个不同的字符串。
> 
> **输入**：`N = 4, M = 5, string[] = {"12121", "23545", "11111", "71261"}`
>
> **输出**：216

**方法**：考虑形式为`s1s2s3s4…sm`形式的字符串，其中`s1`是数组中任何字符串的第一个字母，`s2`是以下数组任何一个字符串的第二个字母，依此类推，问题的答案是`count(i)`的乘积，其中`count(i)`是给定字符串中相同索引处的不同字母的计数。

下面是上述方法的实现：

## C++

```cpp

// C++ program to implement 
// the above approach 
#include <bits/stdc++.h>    
using namespace std;  

int mod = 1000000007; 

// Function to count the distinct strings 
// possible after swapping the prefixes 
// between two possible strings of the array 
long countS(string str[],int n, int m) 
{ 

    // Stores the count of unique 
    // characters for each index 
    unordered_map<int,  
    unordered_set<char>> counts; 

    for(int i = 0; i < n; i++)  
    { 

        // Store current string 
        string s = str[i]; 

        for(int j = 0; j < m; j++) 
        { 
            counts[j].insert(s[j]); 
        } 
    } 

    // Stores the total number of 
    // distinct strings possible 
    long result = 1; 

    for(auto index : counts) 
    { 
        result = (result *  
                  counts[index.first].size()) % mod; 
    } 

    // Return the answer 
    return result; 
} 

// Driver Code 
int main() 
{ 
    string str[] = { "112", "211" }; 

    int N = 2, M = 3; 

    cout << countS(str, N, M); 

    return 0; 
}  

// This code is contributed by rutvik_56 

```

## Java

```java

// Java Program to implement 
// the above approach 
import java.util.*; 
import java.io.*; 

public class Main { 

    static int mod = 1000000007; 

    // Function to count the distinct strings 
    // possible after swapping the prefixes 
    // between two possible strings of the array 
    public static long countS(String str[], int n, int m) 
    { 

        // Stores the count of unique 
        // characters for each index 
        Map<Integer, Set<Character> > counts 
            = new HashMap<>(); 

        for (int i = 0; i < m; i++) { 
            counts.put(i, new HashSet<>()); 
        } 

        for (int i = 0; i < n; i++) { 

            // Store current string 
            String s = str[i]; 

            for (int j = 0; j < m; j++) { 
                counts.get(j).add(s.charAt(j)); 
            } 
        } 

        // Stores the total number of 
        // distinct strings possible 
        long result = 1; 

        for (int index : counts.keySet()) 
            result = (result 
                    * counts.get(index).size()) 
                    % mod; 

        // Return the answer 
        return result; 
    } 

    // Driver Code 
    public static void main(String[] args) 
    { 

        String str[] = { "112", "211" }; 

        int N = 2, M = 3; 
        System.out.println(countS(str, N, M)); 
    } 
} 

```

## C#

```cs

// C# Program to implement 
// the above approach 
using System; 
using System.Collections.Generic; 
class GFG{ 

static int mod = 1000000007; 

// Function to count the distinct strings 
// possible after swapping the prefixes 
// between two possible strings of the array 
public static long countS(String []str, 
                            int n, int m) 
{ 

    // Stores the count of unique 
    // characters for each index 
    Dictionary<int,  
    HashSet<char> > counts = new Dictionary<int,  
                                    HashSet<char>>(); 

    for (int i = 0; i < m; i++) 
    { 
    counts.Add(i, new HashSet<char>()); 
    } 

    for (int i = 0; i < n; i++)  
    { 

    // Store current string 
    String s = str[i]; 

    for (int j = 0; j < m; j++) 
    { 
        counts[j].Add(s[j]); 
    } 
    } 

    // Stores the total number of 
    // distinct strings possible 
    long result = 1; 

    foreach (int index in counts.Keys) 
    result = (result * counts[index].Count) % mod; 

    // Return the answer 
    return result; 
} 

// Driver Code 
public static void Main(String[] args) 
{ 
    String []str = { "112", "211" }; 

    int N = 2, M = 3; 
    Console.WriteLine(countS(str, N, M)); 
} 
} 

// This code is contributed by Rajput-Ji 

```

**输出**： 

```
4

```

**时间复杂度**：`O(N * M)`。

**辅助空间**：`O(n)`。



* * *

* * *



