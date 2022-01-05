# 检查单词是否按照新的字母顺序排序

> 原文:[https://www . geeksforgeeks . org/check-如果单词是按照新的字母顺序排序的/](https://www.geeksforgeeks.org/check-if-words-are-sorted-according-to-new-order-of-alphabets/)

给定单词序列和字母表顺序。字母表的顺序是一些小写字母的排列。任务是检查给定的单词是否按照字母顺序按字典顺序排序。如果是，返回“真”，否则返回“假”。

**示例:**

> **输入:**字数= [“你好”、“leet code”]，订单=“habbcldefgijknmopqrstuvwxyz”
> T3】输出:真
> 
> **输入:**word =[“word”、“world”、“row”]，Order =“abccworldefghijkmnpqstuxyz”
> T3】输出: false
> **解释:**As‘d’在 Order 中排在‘l’之后，因而 word[0]>word[1]，因此顺序未排序。

**方法:**当且仅当相邻单词排序时，单词按字典顺序排序。这是因为顺序是可传递的，即如果 a < = b 和 b < = c，就意味着 a < = c。

所以我们的目标是检查所有相邻的单词 a 和 b 是否都有 a <= b。

为了检查对于两个相邻的单词 a 和 b，a <= b 是否成立，我们可以找到它们的第一个区别。例如，“见过”和“场景”的第一个区别是 e 和 c。之后，我们按顺序将这些字符与索引进行比较。

我们必须有效地处理空白字符。例如，如果我们比较“加”和“加”，这是(空)和“我”的第一个区别。

**以下是上述方法的实施:**

## 蟒蛇 3

```
# Function to check whether Words are sorted in given Order
def isAlienSorted(Words, Order):
    Order_index = {c: i for i, c in enumerate(Order)}

    for i in range(len(Words) - 1):
        word1 = Words[i]
        word2 = Words[i + 1]

        # Find the first difference word1[k] != word2[k].
        for k in range(min(len(word1), len(word2))):

            # If they compare false then it's not sorted.
            if word1[k] != word2[k]:
                if Order_index[word1[k]] > Order_index[word2[k]]:
                    return False
                break
        else:

            # If we didn't find a first difference, the
            # Words are like ("add", "addition").
            if len(word1) > len(word2):
                return False

    return True

# Program Code
Words = ["hello", "leetcode"]
Order = "habcldefgijkmnopqrstuvwxyz"

# Function call to print required answer
print(isAlienSorted(Words, Order))
```

**Output:**

```
True

```

**时间复杂度:** O(N)，其中 N 为所有单词中的字符总数。

**辅助空间:** O(1)