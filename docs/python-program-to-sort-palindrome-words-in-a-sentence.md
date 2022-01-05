# Python 程序对句子中的回文单词进行排序

> 原文:[https://www . geesforgeks . org/python-程序-排序-回文-句中词/](https://www.geeksforgeeks.org/python-program-to-sort-palindrome-words-in-a-sentence/)

给定一个代表一个句子的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是按照[排序顺序](https://www.geeksforgeeks.org/given-sorted-dictionary-find-precedence-characters/)对句子中出现的所有[回文单词](https://www.geeksforgeeks.org/java-program-count-number-palindrome-words-sentence/)重新排序。

**示例:**

> **输入:** S =“请向夫人提知级”
> **输出:**请向夫人提知级
> **说明:**这里的“提”、“夫人”、“级”都是回文词。对它们进行排序会生成序列{“level”、“夫人”、“refer”}。
> 
> **输入:** S =“参考爸爸”
> T3】输出:爸爸参考

**方法:**按照以下步骤解决问题:

*   [迭代字符串的字符](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)。
*   [使用 **split()** 将句子中的单词用空格分割并存储为列表](https://www.geeksforgeeks.org/python-string-split-including-spaces/)，比如 **lis。**
*   将句子 **S** 中出现的所有[回文单词](https://www.geeksforgeeks.org/remove-palindromic-words-given-sentence/)存储在一个列表中，比如说**纽利斯[]。**
*   使用[排序()](https://www.geeksforgeeks.org/python-list-sort/)功能对列表**进行排序。**
*   初始化一个指针，说 **j = 0** 。
*   [遍历列表](https://www.geeksforgeeks.org/iterate-over-words-of-a-string-in-python/) **列表**，将所有[回文](https://www.geeksforgeeks.org/java-program-count-number-palindrome-words-sentence/)替换为**新行【j】**，并将 **j** 增加 **1** 。
*   [打印更新后的句子](https://www.geeksforgeeks.org/recursively-print-all-sentences-that-can-be-formed-from-list-of-word-lists/)

下面是上述方法的实现:

## 蟒蛇 3

```
# Python implementation of above program

# Function to check if a
# string is a palindrome or not
def palindrome(string):
    if(string == string[::-1]):
        return True
    else:
        return False

# Function to print the updated sentence
def printSortedPalindromes(sentence):

    # Stores palindromic words
    newlist = []

    # Stores the words split by spaces
    lis = list(sentence.split())

    # Traversing the list
    for i in lis:

        # If current word is palindrome
        if(palindrome(i)):

            # Update newlist
            newlist.append(i)

    # Sort the words in newlist
    newlist.sort()

    # Pointer to iterate newlis
    j = 0

    # Traverse the list
    for i in range(len(lis)):

        # If current word is palindrome
        if(palindrome(lis[i])):

            # Replacing word with
            # current word in newlist
            lis[i] = newlist[j]

            # Increment j by 1
            j = j + 1

    # Print the updated sentence
    for i in lis:
        print(i, end =" ")

# Driver Code

sentence = "please refer to the madam to know the level"

printSortedPalindromes(sentence)
```

**Output:**

```
please level to the madam to know the refer

```

***时间复杂度:** O(N * logN)*
***辅助空间:** O(N)*