# Python 程序打印字符 ASCII 值最高和最低的句子中的单词

> 原文:[https://www . geesforgeks . org/python-program-to-print-words-from-from-a-a-句子-最高和最低 ascii 字符值/](https://www.geeksforgeeks.org/python-program-to-print-words-from-a-sentence-with-highest-and-lowest-ascii-value-of-characters/)

给定一个长度为 **N** 的[字符串](https://www.geeksforgeeks.org/python-strings/) **S** ，代表一个句子，任务是打印字符的 [ASCII](https://www.geeksforgeeks.org/program-print-ascii-value-character/) 值平均值最高和最低的单词。

**示例:**

> **输入:** S =“每时每刻都是新的开始”
> **输出:**
> ASCII 平均值最小的单词为“开始”。【ASCII 平均值最大的单词为“每”。
> **说明:**
> 单词“every”的字符 ASCII 值平均值=((101+118+101+114+121)/5 = 111)
> 单词“moment”的字符 ASCII 值平均值=:((109+111+109+101+110+116)/6 = 109.33333)
> ASCII 值平均值
> 因此，ASCII 值平均值最小的单词为“开始”，ASCII 值平均值最大的单词为“每”。
> 
> **输入:** S =“天蓝”
> **输出:**
> ASCII 平均值最小的单词为“蓝”。【ASCII 平均值最大的单词为“sky”。

**方法:**思路是使用 [split()](https://www.geeksforgeeks.org/python-string-split/) 功能。按照以下步骤解决问题:

*   [使用](https://www.geeksforgeeks.org/python-spilt-a-sentence-into-list-of-words/) [split()](https://www.geeksforgeeks.org/python-string-split/) 函数拆分字符串中由空格分隔的所有单词。将其存储在[T5 列表 T7 中，说 **lis[]。**](https://www.geeksforgeeks.org/python-list/)
*   初始化四个变量 **maxi、mini、maxId、**和 **minId** 、**T5】分别存储 ASCII 值平均值的最大值、ASCII 值平均值的最小值、列表 lis 中 ASCII 值平均值最大的单词的索引、列表**lis【】**中 ASCII 值平均值最小的单词的索引。**
*   定义一个函数，说 **averageValue()，**到[找到一个字符串的平均 ASCII 值](https://www.geeksforgeeks.org/average-of-ascii-values-of-characters-of-a-given-string/)。
*   [遍历列表](https://www.geeksforgeeks.org/iterate-over-a-list-in-python/)**lis【】**并执行以下操作:
    *   对于列表**中的每个**I<sup>th</sup>T3【单词】lis【】****并将其存储在变量中，比如 **curr。******
    *   **如果**最大值>，则**将**最大值**更新为**最大值=最大值**，并分配**最大值= i.****
    *   **如果 **curr < mini，**则更新 **mini** 为 **mini = curr** 并分配 **minId = i.****
*   **完成上述步骤后，打印文字**lis【minId】**和**lis【maxId】**及其字符**ASCII 值的最小和最大平均值。****

**以下是上述方法的实现:**

## **蟒蛇 3**

```
# Python implementation of the above approach

# Function to find the average
# of ASCII value of a word
def averageValue(s):

    # Stores the sum of ASCII
    # value of all characters
    sumChar = 0

   # Traverse the string
    for i in range(len(s)):

        # Increment sumChar by ord(s[i])
        sumChar += ord(s[i])

    # Return the average
    return sumChar // len(s)

# Function to find words with maximum
# and minimum average of ascii values
def printMinMax(string):

    # Stores the words of the
    # string S separated by spaces
    lis = list(string.split(" "))

    # Stores the index of word in
    # lis[] with maximum average
    maxId = 0

    # Stores the index of word in
    # lis[] with minimum average
    minId = 0

    # Stores the maximum average
    # of ASCII value of characters
    maxi = -1

    # Stores the minimum average
    # of ASCII value of characters
    mini = 1e9

    # Traverse the list lis
    for i in range(len(lis)):

        # Stores the average of
        # word at index i
        curr = averageValue(lis[i])

        # If curr is greater than maxi
        if(curr > maxi):

            # Update maxi and maxId
            maxi = curr
            maxId = i

        # If curr is lesser than mini
        if(curr < mini):

            # Update mini and minId
            mini = curr
            minId = i

    # Print string at minId in lis
    print("Minimum average ascii word = ", lis[minId])

    # Print string at maxId in lis
    print("Maximum average ascii word = ", lis[maxId])

# Driver Code

S = "every moment is fresh beginning"
printMinMax(S)
```

****Output:** 

```
Minimum average ascii word =  beginning
Maximum average ascii word =  every
```** 

*****时间复杂度:**O(N)*
T5**辅助空间:** O(1)**