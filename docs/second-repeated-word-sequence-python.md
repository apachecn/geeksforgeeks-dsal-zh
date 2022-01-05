# Python 中序列中重复次数第二多的单词

> 原文:[https://www . geesforgeks . org/second-repeated-word-sequence-python/](https://www.geeksforgeeks.org/second-repeated-word-sequence-python/)

给定一个字符串序列，任务是找出给定序列中第二个重复(或最频繁)的字符串。(考虑到没有两个单词是重复次数第二多的，总会有一个单词)。
示例:

```
Input : {"aaa", "bbb", "ccc", "bbb", 
         "aaa", "aaa"}
Output : bbb

Input : {"geeks", "for", "geeks", "for", 
          "geeks", "aaa"}
Output : for
```

此问题已有解决方案请参考[序列中重复次数第二多的单词](https://www.geeksforgeeks.org/second-repeated-word-sequence/)链接。我们可以使用[计数器(迭代器)](https://www.geeksforgeeks.org/counters-in-python-set-1/)方法在 Python 中快速解决这个问题。
方法很简单–

1.  使用**计数器(迭代器)**方法创建一个字典，其中包含单词作为关键字，其频率作为值。
2.  现在获取字典中所有值的列表，并按降序排序。从排序列表中选择第二个元素，因为它将是第二大元素。
3.  现在再次遍历字典并打印其值等于第二大元素的键。

## 蟒蛇 3

```
# Python code to print Second most repeated
# word in a sequence in Python
from collections import Counter

def secondFrequent(input):

    # Convert given list into dictionary
    # it's output will be like {'ccc':1,'aaa':3,'bbb':2}
    dict = Counter(input)

    # Get the list of all values and sort it in ascending order
    value = sorted(dict.values(), reverse=True)

    # Pick second largest element
    secondLarge = value[1]

    # Traverse dictionary and print key whose
    # value is equal to second large element
    for (key, val) in dict.items():
        if val == secondLarge:
            print(key)
            return

# Driver program
if __name__ == "__main__":
    input = ['aaa', 'bbb', 'ccc', 'bbb', 'aaa', 'aaa']
    secondFrequent(input)
```

**输出:**

```
bbb
```

**替代实施:**

## 蟒蛇 3

```
# returns the second most repeated word
from collections import Counter
class Solution:
    def secFrequent(self, arr, n):
        all_freq = dict(Counter(arr))
        store = []
        for w in sorted(all_freq, key=all_freq.get):
            # if add key=all_freq.get will sort according to values
            # without key=all_freq.get will sort according to keys
            if w not in store:
                store.append(w)

        return store[-2]
 # driver code or main function
if __name__ == '__main__':
    t = int(input())
    for _ in range(t):
        n = int(input().strip())
        arr = input().strip().split(" ")
        ob = Solution()
        ans = ob.secFrequent(arr,n)
        print(ans)

contributed by Pratyush Pratap Singh
```

**Output**

```
bbb

```