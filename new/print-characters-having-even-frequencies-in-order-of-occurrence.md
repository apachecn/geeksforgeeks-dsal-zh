# 按出现顺序打印具有偶数频率的字符

给定仅包含小写字符的字符串 **str** 。 任务是按照出现的顺序打印频率均匀的字符。

**注意**：重复出现的偶数频率按出现的次数打印。

**示例：**

> **输入：** str =“ geeksforgeeks”
> **输出：** geeksgeeks
> 
> | 字符 | 频率 |
> | --- | --- |
> | 'G' | 2 |
> | 是 | 4 |
> | '至' | 2 |
> | ‘s’ | 2 |
> | 'F' | 1 |
> | '的' | 1 |
> | ‘r’ | 1 |
> 
> 仅有“ g”，“ e”，“ k”和“ s”是频率偶数的字符。
> 
> **输入：** str =“飞机”
> **输出：** aeae

**方法：**创建一个频率数组，以存储给定字符串 **str** 的每个字符的频率。 再次遍历字符串 **str** ，并检查该字符的频率是否为偶数。 如果是，则打印字符。

下面是上述方法的实现：

## C ++

```

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

#define SIZE 26 

// Function to print the even frequency characters 
// in the order of their occurrence 
void printChar(string str, int n) 
{ 

    // To store the frequency of each of 
    // the character of the string 
    int freq[SIZE]; 

    // Initialize all elements of freq[] to 0 
    memset(freq, 0, sizeof(freq)); 

    // Update the frequency of each character 
    for (int i = 0; i < n; i++) 
        freq[str[i] - 'a']++; 

    // Traverse str character by character 
    for (int i = 0; i < n; i++) { 

        // If frequency of current character is even 
        if (freq[str[i] - 'a'] % 2 == 0) { 
            cout << str[i]; 
        } 
    } 
} 

// Driver code 
int main() 
{ 
    string str = "geeksforgeeks"; 
    int n = str.length(); 
    printChar(str, n); 

    return 0; 
} 

```

## 爪哇

```

// Java implementation of the approach 
import java.util.*; 

class GFG  
{ 
static int SIZE = 26; 

// Function to print the even frequency characters 
// in the order of their occurrence 
static void printChar(String str, int n) 
{ 

    // To store the frequency of each of 
    // the character of the string 
    int []freq = new int[SIZE]; 

    // Update the frequency of each character 
    for (int i = 0; i < n; i++) 
        freq[str.charAt(i) - 'a']++; 

    // Traverse str character by character 
    for (int i = 0; i < n; i++)  
    { 

        // If frequency of current character is even 
        if (freq[str.charAt(i) - 'a'] % 2 == 0) 
        { 
            System.out.print(str.charAt(i)); 
        } 
    } 
} 

// Driver code 
public static void main(String[] args) 
{ 
    String str = "geeksforgeeks"; 
    int n = str.length(); 
    printChar(str, n); 
} 
}  

// This code is contributed by 29AjayKumar 

```

## Python3

```

# Python3 implementation of the approach 
SIZE = 26

# Function to print the even frequency characters 
# in the order of their occurrence 
def printChar(string, n): 

    # To store the frequency of each of 
    # the character of the stringing 
    # Initialize all elements of freq[] to 0 
    freq = [0] * SIZE 

    # Update the frequency of each character 
    for i in range(0, n): 
        freq[ord(string[i]) - ord('a')] += 1

    # Traverse string character by character 
    for i in range(0, n):  

        # If frequency of current character is even 
        if (freq[ord(string[i]) - 
                 ord('a')] % 2 == 0): 
            print(string[i], end = "") 

# Driver code 
if __name__ == '__main__': 
    string = "geeksforgeeks"
    n = len(string) 
    printChar(string, n) 

# This code is contributed by Ashutosh450 

```

## C＃

```

// C# implementation of the approach 
using System; 
using System.Collections.Generic; 

class GFG  
{ 
static int SIZE = 26; 

// Function to print the even frequency characters 
// in the order of their occurrence 
static void printChar(String str, int n) 
{ 

    // To store the frequency of each of 
    // the character of the string 
    int []freq = new int[SIZE]; 

    // Update the frequency of each character 
    for (int i = 0; i < n; i++) 
        freq[str[i] - 'a']++; 

    // Traverse str character by character 
    for (int i = 0; i < n; i++)  
    { 

        // If frequency of current character is even 
        if (freq[str[i] - 'a'] % 2 == 0) 
        { 
            Console.Write(str[i]); 
        } 
    } 
} 

// Driver code 
public static void Main(String[] args) 
{ 
    String str = "geeksforgeeks"; 
    int n = str.Length; 
    printChar(str, n); 
} 
} 

// This code is contributed by Princi Singh 

```

**Output:**

```
geeksgeeks

```

**时间复杂度：** O（n）
**辅助空间：** O（1）

注意读者！ 现在不要停止学习。 通过 [**DSA 自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的 DSA 概念，并为行业做好准备。

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。