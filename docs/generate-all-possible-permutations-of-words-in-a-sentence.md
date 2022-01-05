# 生成句子中所有可能的单词排列

> 原文:[https://www . geeksforgeeks . org/generate-所有可能的句子中单词排列/](https://www.geeksforgeeks.org/generate-all-possible-permutations-of-words-in-a-sentence/)

给定一个[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是打印一个句子中所有单词的[排列。](https://www.geeksforgeeks.org/print-all-permutations-of-a-string-in-java/)

**示例:**

> **输入:** S =【天蓝】
> T3】输出:T5】天蓝
> 天蓝是
> 天蓝
> 是蓝天
> 蓝天是
> 蓝是天空
> 
> **输入:** S = "做你爱做的"
> **输出:**
> 做你爱做的
> 做你爱做的
> 做你爱做的
> 做你爱做的
> 做你爱做的
> 做你爱做的
> 做你爱做的
> 做你爱做的
> 做你爱做的
> 做你爱做的
> 做你爱做的
> 做你爱做的
> 做你爱做的 爱什么
> 你爱什么做什么
> 你爱什么做什么
> 你爱什么做什么
> 你爱什么做什么
> 爱什么做什么
> 爱你做什么
> 爱你做什么
> 爱你做什么
> 爱你做什么
> 爱你做什么

**方法:**给定的问题可以使用[递归](https://www.geeksforgeeks.org/recursion/)来解决。按照以下步骤解决问题:

1.  [遍历句子](https://www.geeksforgeeks.org/split-a-sentence-into-words-in-cpp/)，使用 [**split()**](https://www.geeksforgeeks.org/python-string-split/) 将句子中出现的单词用空格分割，并存储在列表中。
2.  使用内置 python 函数 [**对列表进行置换。**](https://www.geeksforgeeks.org/permutation-and-combination-in-python/)
3.  [遍历排列](https://www.geeksforgeeks.org/print-all-possible-permutations-of-an-array-with-duplicates-using-backtracking/)并将每个排列转换为 [**列表。**](https://www.geeksforgeeks.org/python-list/)
4.  [打印这些列表](https://www.geeksforgeeks.org/print-lists-in-python-4-different-ways/)。

下面是上述方法的实现:

## 蟒蛇 3

```
# Python implementation of
# the above approach

from itertools import permutations

# Function to generate permutations
# of all words in a sentence
def calculatePermutations(sentence):

    # Stores all words in the sentence
    lis = list(sentence.split())

    # Stores all possible permutations
    # of words in this list
    permute = permutations(lis)

    # Iterate over all permutations
    for i in permute:

        # Convert the current
        # permutation into a list
        permutelist = list(i)

        # Print the words in the
        # list separated by spaces
        for j in permutelist:
            print(j, end = " ")

        # Print a new line
        print()

# Driver Code
if __name__ == '__main__':

    sentence = "sky is blue"
    calculatePermutations(sentence)
```

**Output:** 

```
sky is blue 
sky blue is 
is sky blue 
is blue sky 
blue sky is 
blue is sky
```

***时间复杂度:** O(N！)，其中 N 表示一个句子中的字数。*
***辅助空间:** O(N！)*