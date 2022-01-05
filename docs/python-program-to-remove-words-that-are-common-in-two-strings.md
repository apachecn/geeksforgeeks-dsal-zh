# Python 程序删除两个字符串中常见的单词

> 原文:[https://www . geesforgeks . org/python-program-to-remove-two-string 中常见的单词/](https://www.geeksforgeeks.org/python-program-to-remove-words-that-are-common-in-two-strings/)

给定代表句子的两个字符串 **S1** 和 **S2** ，任务是在删除两个句子中存在的所有单词后打印这两个句子。

> **输入:** S1 =“天蓝于色”，S2 =“拉吉喜欢天蓝于色”
> **输出:**在
> 拉吉喜欢
> **解释:**常用词为**【天蓝于色】。**从两个句子中删除这些单词会将句子修改为指定的输出。
> 
> **输入:**S1 =**“**在 GeeksforGeeks 中学习数据结构和算法**、**S2 =**“**Geeks forgeeks 是 Geeks 的计算机科学门户**”**
> **输出:**在
> 中学习数据结构和算法是计算机科学门户。

**方法使用** [**哈希**](https://www.geeksforgeeks.org/hashing-data-structure/) **:** 问题可以使用 [**计数器()**](https://www.geeksforgeeks.org/python-counter-objects-elements/) 功能解决。按照以下步骤解决问题:

*   由于一个句子中的所有单词都是用空格分隔的，所以使用[**【split()**](https://www.geeksforgeeks.org/python-string-split/)将单词用空格分隔，并将其存储在**列表**中。
*   初始化两个列表，说出**句子 1** 和**句子 2** ，存储两个给定句子的单词。
*   使用**计数器()**功能统计两个句子的单词频率，并将其存储在词典**频率 1** 和**频率 2** 中。
*   [遍历列表](https://www.geeksforgeeks.org/iterate-over-a-list-in-python/) **句子 1** 并删除出现在[词典](https://www.geeksforgeeks.org/python-dictionary/) **频率 2** 中的单词。
*   [遍历列表](https://www.geeksforgeeks.org/iterate-over-a-list-in-python/) **句子 2** 并删除出现在[词典](https://www.geeksforgeeks.org/python-dictionary/) **频率 1** 中的单词。
*   打印两个列表。

下面是上述方法的实现:

## 蟒蛇 3

```
# Python program for the above approach
from collections import Counter

# Function to remove common
# words from two strings
def removeCommonWords(sent1, sent2):

    # Store the words present
    # in both the sentences
    sentence1 = list(sent1.split())
    sentence2 = list(sent2.split())

    # Calculate frequency of words
    # using Counter() function
    frequency1 = Counter(sentence1)
    frequency2 = Counter(sentence2)

    word = 0

    # Iterate the list consisting
    # of words in the first sentence 
    for i in range(len(sentence1)):

        # If word is present
        # in both the strings
        if sentence1[word] in frequency2.keys():

              # Remove the word
            sentence1.pop(word)

            # Decrease the frequency of the word
            word = word-1
        word += 1

    word = 0

    # Iterate the list consisting of
    # words in the second sentence 
    for i in range(len(sentence2)):

        # If word is present
        # in both the strings
        if sentence2[word] in frequency1.keys():

              # Remove the word
            sentence2.pop(word)

            # Decrease the removed word
            word = word-1

        word += 1

    # Print the remaining
    # words in the two sentences
    print(*sentence1)
    print(*sentence2)

# Driver Code

sentence1 = "sky is blue in color"
sentence2 = "raj likes sky blue color"

removeCommonWords(sentence1, sentence2)
```

**Output:**

```
is in
raj likes

```

 ***时间复杂度:** O((max(N，M)) <sup>2</sup> )
**辅助空间:** O(max(N，M))*

**方法使用** [**设置**](https://www.geeksforgeeks.org/python-sets/) **和** [**列出**](https://www.geeksforgeeks.org/python-list/) **:** 按照以下步骤解决问题:

*   由于一个句子中的所有单词都是用空格分隔的，所以使用[**【split()**](https://www.geeksforgeeks.org/python-string-split/)将单词用空格分隔，并将其存储在**列表**中。
*   初始化两个列表，说出**句子 1** 和**句子 2** ，存储两个给定句子的单词。
*   将两个列表转换成集合，比如**森 1** 和**森 2** 。
*   现在，找到两个集合**的 [**集合交集，存储两个句子中常见的单词，说**常见的**。**](https://www.geeksforgeeks.org/intersection-function-python/)**
*   **[遍历列表](https://www.geeksforgeeks.org/iterate-over-a-list-in-python/) **句子 1** 和[T5】弹出](https://www.geeksforgeeks.org/python-list-pop/) 两个句子的集合交集中存在的所有单词。**
*   **对第二句重复同样的内容。**
*   **最后，打印两个**列表**中的剩余单词。**

**下面是上述方法的实现:**

## **蟒蛇 3**

```
# Python program to implement
# the above approach

# Function to return the words which
# are common in both the sentences
def commonWords(sent1, sent2):

    # Splitting the words in a set
    sen1 = set(sent1)
    sen2 = set(sent2)

    # Stores the list of common words
    common = list(sen1.intersection(sen2))

    # Return the list
    return common

# Function to remove all the words
# that are common in both the strings
def removeCommonWords(sent1, sent2):

    # Stores the words of the
    # sentences in separate lists
    sentence1 = list(sent1.split())
    sentence2 = list(sent2.split())

    # Find the words that are
    # common in both the sentences
    commonlist = commonWords(sentence1, 
                             sentence2)

    word = 0

    # Iterate the list of words
    # of the first sentence
    for i in range(len(sentence1)):

        # If word is common in both lists
        if sentence1[word] in commonlist:

              # Remove the word
            sentence1.pop(word)

            # Decrease the removed word
            word = word - 1
        word += 1

    word = 0

    # Iterate the list of words
    # of the second sentence
    for i in range(len(sentence2)):

        # If word is common in both lists
        if sentence2[word] in commonlist:

              # Remove the word
            sentence2.pop(word)

            # Decrease the removed word
            word = word-1
        word += 1

    # Print the remaining words
    # in both the sentences
    print(*sentence1)
    print(*sentence2)

# Driver Code

S1 = "sky is blue in color"
S2 = "Raj likes sky blue color"

removeCommonWords(S1, S2)
```

****Output:**

```
is in
Raj likes

```** 

 *****时间复杂度:** O(max(N，M))
**辅助空间:** O(max(N，M))***