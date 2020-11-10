# 最小化包含另一个字符串`T`的所有字符的字符串`S`的前缀长度

> 原文：[https://www.geeksforgeeks.org/minimize-length-of-prefix-of-string-s-containing-all-characters-of-another-string-t/](https://www.geeksforgeeks.org/minimize-length-of-prefix-of-string-s-containing-all-characters-of-another-string-t/)



给定两个字符串`S`和`T`，任务是从`S`中查找最小长度前缀，该前缀由字符串`T`的所有字符组成 。 如果`S`不包含字符串`T`的所有字符，则打印 **-1**。

**示例**：

> **输入**：`S = "MarvoloGaunt", T = "Tom"`
>
> **输出**：12
>
> **解释**：长度 12 的前缀`MarvoloGaunt`包含`Tom`的所有元素
> 
> **输入**：`S = "TheWorld", T = "Dio"`
>
> **输出**：-1
>
> **说明**：
>
> 字符串`"TheWorld"`不包含字符串`"Dio"`中的字符`"i"`

**朴素的方法**：

解决问题的最简单方法是迭代字符串`S`，并比较前缀和`T`中每个字母的频率 并返回经过的长度（如果找到所需的前缀）。 否则，返回 -1。

**时间复杂度**：`O(N ^ 2)`

**辅助空间**：`O(1)`

**有效方法**：

要优化上述方法，请按照以下步骤操作：

1.  将`T`的频率存储在字典`dictCount`中。

2.  将计数大于 0 的唯一字母数存储为`nUnique`。

3.  迭代`[0, N]`，并以`ch`的形式获得`S`的索引`i`字符。

4.  从`dictCount`（如果存在）中减少`ch`的计数。 如果该计数变为 0，则将`nUnique`减少 1。

5.  如果`nUnique`达到 0，则返回到此为止遍历的长度。

6.  完全遍历`S`之后，如果`nUnique`仍超过 0，则打印 **-1**。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach 
#include <bits/stdc++.h>
using namespace std;

int getPrefixLength(string srcStr, 
                    string targetStr)
{

    // Base Case - if T is empty, 
    // it matches 0 length prefix 
    if (targetStr.length() == 0) 
        return 0;

    // Convert strings to lower 
    // case for uniformity 
    transform(srcStr.begin(), 
              srcStr.end(), 
              srcStr.begin(), ::tolower);
    transform(targetStr.begin(), 
              targetStr.end(), 
              targetStr.begin(), ::tolower); 

    map<char, int> dictCount;
    int nUnique = 0;

    // Update dictCount to the 
    // letter count of T 
    for(char ch: targetStr)
    {

        // If new character is found, 
        // initialize its entry, 
        // and increase nUnique 
        if (dictCount.find(ch) == 
            dictCount.end())
        {
            nUnique += 1;
            dictCount[ch] = 0;
        }

        // Increase count of ch 
        dictCount[ch] += 1;
    }

    // Iterate from 0 to N 
    for(int i = 0; i < srcStr.length(); i++)
    {

        // i-th character 
        char ch = srcStr[i]; 

        // Skip if ch not in targetStr 
        if (dictCount.find(ch) ==
            dictCount.end()) 
            continue;

        // Decrease Count 
        dictCount[ch] -= 1;

        // If the count of ch reaches 0, 
        // we do not need more ch, 
        // and can decrease nUnique 
        if (dictCount[ch] == 0) 
            nUnique -= 1;

        // If nUnique reaches 0, 
        // we have found required prefix 
        if (nUnique == 0)
            return (i + 1); 
    }

    // Otherwise 
    return -1;
}

// Driver code   
int main()
{
    string S = "MarvoloGaunt";
    string T = "Tom";

    cout << getPrefixLength(S, T); 

    return 0;
}

// This code is contributed by divyeshrabadiya07

```

## Python3

```py

# Python3 program for the above approach

def getPrefixLength(srcStr, targetStr):

    # Base Case - if T is empty,
    # it matches 0 length prefix
    if(len(targetStr) == 0):
        return 0

    # Convert strings to lower
    # case for uniformity
    srcStr = srcStr.lower()
    targetStr = targetStr.lower()

    dictCount = dict([])
    nUnique = 0

    # Update dictCount to the
    # letter count of T
    for ch in targetStr:

        # If new character is found,
        # initialize its entry,
        # and increase nUnique
        if(ch not in dictCount):
            nUnique += 1
            dictCount[ch] = 0

        # Increase count of ch
        dictCount[ch] += 1

    # Iterate from 0 to N
    for i in range(len(srcStr)):

        # i-th character
        ch = srcStr[i]

        # Skip if ch not in targetStr
        if(ch not in dictCount):
            continue
        # Decrease Count
        dictCount[ch] -= 1

        # If the count of ch reaches 0,
        # we do not need more ch,
        # and can decrease nUnique
        if(dictCount[ch] == 0):
            nUnique -= 1

        # If nUnique reaches 0,
        # we have found required prefix
        if(nUnique == 0):
            return (i + 1)

    # Otherwise
    return -1

# Driver Code
if __name__ == "__main__":

    S = "MarvoloGaunt"
    T = "Tom"

    print(getPrefixLength(S, T))

```

**输出**： 

```
12

```

**时间复杂度**：`O(n)`

**辅助空间**：`O(1)`



* * *

* * *



