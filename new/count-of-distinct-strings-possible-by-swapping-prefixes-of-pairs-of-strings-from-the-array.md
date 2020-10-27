# 通过交换数组

中的成对字符串的前缀可以实现不同字符串的计数

给定一个数组 **string []** ，该数组由 **N** 个数字字符串，长度为 **M** 组成，任务是找到可以通过选择任意一个生成的不同字符串的数量 两个字符串，例如数组中的 **i** 和 **j** ，并在它们之间交换所有可能的前缀。
***注意：**由于答案可能非常大，请以模 1000000007 为模。*

**示例：**

> **输入：** N = 2 M = 3 字符串[] = {“ 112”，“ 211”}
> **输出：** 4
> **说明：**
> 在字符串之间交换“ 1”和“ 2”会生成“ **212** ”和“ **111** ”。
> 在字符串之间交换“ 11”和“ 21”会生成“ 212”和“ 111”。
> 在字符串之间交换“ 112”和“ 211”会生成“ **211** ”和“ **112** ”。
> 因此，生成了 4 个不同的字符串。
> 
> **输入：** N = 4 M = 5 字符串[] = {“ 12121”，“ 23545”，“ 11111”，“ 71261”}
> **输出：** 216

**方法：**考虑形式为[ <sub>1</sub> s <sub>2</sub> s <sub>3</sub> s <sub>4 形式的字符串 **s**</sub> …s <sub>m</sub> ，其中 s <sub>1</sub> 是数组中任何字符串的第一个字母，s <sub>2</sub> 是以下任何一个数组的第二个字母 字符串，依此类推，问题的答案是 **count（i）**的乘积，其中 **count（i）**是给定给定索引中不同字母的计数 字符串。

下面是上述方法的实现：

## C ++

```

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

## 爪哇

```

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

## C＃

```

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

**Output:** 

```
4

```

***时间复杂度：** O（N * M）*
***辅助空间：** O（N）*

注意读者！ 现在不要停止学习。 通过 [**DSA 自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的 DSA 概念，并为行业做好准备。

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。