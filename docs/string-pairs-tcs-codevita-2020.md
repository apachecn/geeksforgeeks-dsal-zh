# 字符串对| TCS Codevita 2020

> 哎哎哎:# t0]https://www . geeksforgeeks . org/string-pairs-TCS-code life-2020/

一个人把数字列表交给了字符串先生，但是字符串先生只理解字符串。在字符串中，他也只理解元音。String 先生需要你的帮助找到加起来达到某个数字 **D** 的对子总数。

计算数字 **D** 的规则如下:

*   取所有数字，并将其转换为文本表示。
*   接下来，从所有文本表示中总结元音的数量，即 **{a，e，I，o，u}** 。这个总和是数字 **D** 。
*   现在，一旦数字 **D** 已知，找出输入中所有无序的数对，其和等于 **D** 。

**问题陈述:**给定一个由 **N** ( **1 ≤ N ≤ 100** )整数组成的数组**arr【】**，任务是将每个数组元素( *1 ≤ arr[i] ≤ 100* )转换为它们各自的文本表示，并打印数组中所有可能对的计数的小写表示，这些对的总和等于它们的文本表示中存在的元音总数。如果计数超过 100，打印*“大于 100”*。
**注:**对于数字 100，将其转换为文字表示为**百**而非**百**。

**示例:**

> **输入:** arr[] = {1，2，3，4，5}
> **输出:**一
> **解释:**
> 1 - >一- > o，e (2 元音)
> 2 - >二- > o (1 元音)
> 3 - >三- > e，e (2 元音)
> 4 - >四- > o，o
> 现在从给定的数组中，只有单个无序对{4，5}的总和为 9。因此，计数为 1。因此，要求的输出是“**一**”。
> 
> **输入:** arr[] = {7，4，2，}
> **输出:**零
> **解释:**
> 7 - >七- > e，e (2 个元音)
> 4 - >四- > o，u (2 个元音)
> 2 - >二- > o (1 个元音)
> 它们的文本表示中的元音总数= {2 + 2 + 1
> 现在从给定的数组中，不存在加起来等于 5 的对。所以，答案是“**零**”。

**方法:**按照以下步骤解决这个问题:

*   在**地图**中存储从 **0** 到 **100** 的每个数字的文本表示。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个数组元素，将每个数字转换为其文本形式。
*   找出文本形式中存在的元音总数，并将其存储在一个变量中，比如 **D** 。
*   现在，[从给定的数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)中生成所有可能的对。
*   用总和 **D** 数出所有对。
*   如果计数超过 100，**“大于 100”**。否则，打印其文本形式。

下面是上述方法的实现:

## 蟒蛇 3

```
# Python3 program for the above approach

# Import combinations
from itertools import combinations

# Function to check the string pair
def string_pair(n, nums):
    words = {0: 'zero', 1: 'one', 2: 'two', 3: 'three',
             4: 'four', 5: 'five', 6: 'six', 7: 'seven',
             8: 'eight', 9: 'nine', 10: 'ten', 11: 'eleven',
             12: 'twelve', 13: 'thirteen', 14: 'fourteen',
             15: 'fifteen', 16: 'sixteen', 17: 'seventeen',
             18: 'eighteen', 19: 'nineteen', 20: 'twenty',
             21: 'twentyone', 22: 'twentytwo', 23: 'twentythree',
             24: 'twentyfour', 25: 'twentyfive', 26: 'twentysix',
             27: 'twentyseven', 28: 'twentyeight', 29: 'twentynine',
             30: 'thirty', 31: 'thirtyone', 32: 'thirtytwo',
             33: 'thirtythree', 34: 'thirtyfour', 35: 'thirtyfive',
             36: 'thirtysix', 37: 'thirtyseven', 38: 'thirtyeight',
             39: 'thirtynine', 40: 'forty', 41: 'fortyone',
             42: 'fortytwo', 43: 'fortythree', 44: 'fortyfour',
             45: 'fortyfive', 46: 'fortysix', 47: 'fortyseven',
             48: 'fortyeight', 49: 'fortynine', 50: 'fifty',
             51: 'fiftyone', 52: 'fiftytwo', 53: 'fiftythree',
             54: 'fiftyfour', 55: 'fiftyfive', 56: 'fiftysix',
             57: 'fiftyseven', 58: 'fiftyeight', 59: 'fiftynine',
             60: 'sixty', 61: 'sixtyone', 62: 'sixtytwo',
             63: 'sixtythree', 64: 'sixtyfour', 65: 'sixtyfive',
             66: 'sixtysix', 67: 'sixtyseven', 68: 'sixtyeight',
             69: 'sixtynine', 70: 'seventy', 71: 'seventyone',
             72: 'seventytwo', 73: 'seventythree', 74: 'seventyfour',
             75: 'seventyfive', 76: 'seventysix', 77: 'seventyseven',
             78: 'seventyeight', 79: 'seventynine', 80: 'eighty',
             81: 'eightyone', 82: 'eightytwo', 83: 'eightythree',
             84: 'eightyfour', 85: 'eightyfive', 86: 'eightysix',
             87: 'eightyseven', 88: 'eightyeight', 89: 'eightynine',
             90: 'ninety', 91: 'ninetyone', 92: 'ninetytwo',
             93: 'ninetythree', 94: 'ninetyfour', 95: 'ninetyfive',
             96: 'ninetysix', 97: 'ninetyseven', 98: 'ninetyeight',
             99: 'ninetynine', 100: 'hundred'}

    # Map the string into list of integers
    nums = list(map(int, nums))

    # Temporary lists to store list of count
    ls, ls1 = [], []
    count, c = 0, 0

    # Iterating through the numbers
    for i in nums:

        # Stores the textual form of i
        s = words[i]
        for a in range(len(s)):
            vo = ['a', 'e', 'i', 'o', 'u']

            # If it is vowel
            if s[a] in vo:

                # Increment the count
                count += 1

        # Append the count
        ls.append(count)
        count = 0

    # D = sum(count of vowels)
    d = sum(ls)
    for i in nums:

      # To find the numbers less
      # that or equal to d,
      # so as to find the pair sum
        if i <= d:

            # Append the numbers
            # whose sum can be d
            ls1.append(i)

    # Stores all possible pairs in the
    # form of an object list of tuples
    comb = combinations(ls1, 2)

    # Traverse all the pairs
    for i in list(comb):

        # If sum is equal to d
        if sum(i) == d:

            # Increment count
            c += 1

    # If count exceeds 100
    if c <= 100:
        print(words)

    # Otherwise
    else:
        print("greater 100")

# Driver Code
if __name__ == '__main__':

    # Given Length of string
    n = 5

    # Given array
    arr = [1, 2, 3, 4, 5]

    # Function Call
    string_pair(n, arr)
```

**Output:**

```
one

```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N <sup>2</sup> )*