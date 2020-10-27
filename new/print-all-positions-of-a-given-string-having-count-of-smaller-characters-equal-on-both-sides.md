# 打印给定字符串的所有位置，该字符串的小写字符数在两侧均相等

给定[字符串](https://www.geeksforgeeks.org/string-data-structure/)， **str** ，任务是查找给定字符串的索引，以使该索引左侧和右侧的按字典顺序排列的较小字符数相等且非 -零。

**示例：**

> **输入：** str =“ aabacdabbb” 2 是 2，索引 2 的右侧也是 2。
> 索引 4 左侧的小字符计数是 4，索引 4 的右侧也是 4 。
> 
> **输入：**“ geeksforgeeks”
> **输出：** 5
> **说明：**
> 索引 5 左侧较小字符的计数为 2 并且索引 5 的右侧也为 2。
> 因此，所需的输出为 5。

**天真的方法：**解决此问题的最简单方法是[遍历给定的字符串](https://www.geeksforgeeks.org/strings-in-c-2/)并计算给定字符串每个索引左侧和右侧的按字典顺序排列的较小字符数 。 对于每个索引，请检查当前索引左侧和右侧在字典上较小的字符数是否相等。 如果发现为真，则打印当前索引。

***时间复杂度：**（N <sup>2</sup> ）*Â
***辅助空间：** O（1）*

**高效方法：**要优化上述方法，其思想是使用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)。 请按照以下步骤解决问题：

*   初始化一个数组，例如说 **cntFre []** ，以存储给定字符串的每个字符的频率
*   [遍历给定的字符串](https://www.geeksforgeeks.org/strings-in-c-2/)，并存储给定字符串的每个字符的频率。
*   初始化一个数组，例如说 **cntLeftFreq []** ，以存储出现在给定字符串当前索引左侧的所有字符的频率。
*   [遍历给定的字符串](https://www.geeksforgeeks.org/strings-in-c-2/)，并存储出现在当前索引左侧的所有按字典顺序排列的较小字符的频率。
*   对于每个索引，请检查当前索引左侧和右侧的按字典顺序排列的较小字符数是否相等。 如果发现为 true，则打印给定字符串的当前索引。

下面是上述方法的实现：

## C ++

```

// C++ program to implement 
// the above approach 

#include <bits/stdc++.h> 
using namespace std; 

// Function to find indexes 
// of the given string that  
// satisfy the condition 
void printIndexes(string str) 
{ 
    // Stores length of  
    // given string 
    int N = str.length(); 

    // Stores frequncy of 
    // each character of str 
    int cntFreq[256] = {0}; 

    for (int i = 0; i < N;  
                      i++) { 

        // Update frequency of 
        // current character 
        cntFreq[str[i]]++; 

    } 

    // cntLeftFreq[i] Stores frequncy 
    // of characters present on 
    // the left side of index i. 
    int cntLeftFreq[256] = {0}; 

    // Traverse the given string 
    for (int i = 0; i < N; i++) { 

        // Stores count of smaller 
        // characters on left side of i. 
        int cntLeft = 0; 

        // Stores count of smaller 
        // characters on Right side of i. 
        int cntRight = 0; 

        // Traverse smaller characters 
        // on left side of index i. 
        for (int j = str[i] - 1;  
                    j >= 0; j--) { 

            // Update cntLeft    
            cntLeft += cntLeftFreq[j]; 

            // Update cntRight 
            cntRight += cntFreq[j] 
                   - cntLeftFreq[j]; 
        } 

        // Update cntLeftFreq[str[i]] 
        cntLeftFreq[str[i]]++; 

        // If count of smaller elements 
        // on both sides equal 
        if (cntLeft == cntRight && 
                 cntLeft != 0) { 

            // Print current index; 
            cout<<i<<" "; 
        } 

    } 
} 

// Driver Code  
int main() 
{ 
    string str = "aabacdabbb"; 
    printIndexes(str); 
} 

```

## Python3

```

# Python3 program to implement 
# the above approach 

# Function to find indexes 
# of the given that 
# satisfy the condition 
def printIndexes(strr): 

    # Stores length of 
    # given string 
    N = len(strr) 

    # Stores frequncy of 
    # each character of strr 
    cntFreq = [0] * 256

    for i in range(N): 

        # Update frequency of 
        # current character 
        cntFreq[ord(strr[i])] += 1

    # cntLeftFreq[i] Stores frequncy 
    # of characters present on 
    # the left side of index i. 
    cntLeftFreq = [0] * 256

    # Traverse the given strring 
    for i in range(N): 

        # Stores count of smaller 
        # characters on left side of i. 
        cntLeft = 0

        # Stores count of smaller 
        # characters on Right side of i. 
        cntRight = 0

        # Traverse smaller characters 
        # on left side of index i. 
        for j in range(ord(strr[i]) - 1, -1, -1): 

            # Update cntLeft 
            cntLeft += cntLeftFreq[j] 

            # Update cntRight 
            cntRight += (cntFreq[j] - 
                     cntLeftFreq[j]) 

        # Update cntLeftFreq[strr[i]] 
        cntLeftFreq[ord(strr[i])] += 1

        # If count of smaller elements 
        # on both sides equal 
        if (cntLeft == cntRight and cntLeft != 0): 

            # Print current index 
            print(i, end = " ") 

# Driver Code 
if __name__ == '__main__': 

    strr = "aabacdabbb"

    printIndexes(strr) 

# This code is contributed by mohit kumar 29

```

**Output:** 

```
2 4

```

***时间复杂度：** O（N * 256）*
***辅助空间：** O（256）*

注意读者！ 现在不要停止学习。 通过 [**DSA 自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的 DSA 概念，并为行业做好准备。

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。