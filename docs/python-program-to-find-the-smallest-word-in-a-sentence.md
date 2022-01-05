# Python 程序查找句子中最小的单词

> 原文:[https://www . geesforgeks . org/python-program-to-find-最小的一句话单词/](https://www.geeksforgeeks.org/python-program-to-find-the-smallest-word-in-a-sentence/)

给定一个由小写英文字母组成的字符串**，任务是打印给定字符串中最小的单词。**

****示例:****

> ****输入:** S =【天是蓝的】
> T3】输出:是“
> **说明:**
> 的“天空”长度为 3。
> 长度为“是”2。
> 蓝色的长度为 4。
> 所以，最小的字是“是”。**
> 
> ****输入:** S =“极客为极客”
> T3】输出:“为”**

****基于搜索的方法:** 参考 [<u>这篇</u>](https://www.geeksforgeeks.org/program-find-smallest-largest-word-string/) 的文章，通过执行以下步骤来解决这个问题:**

*   **迭代字符串的字符。**
*   **检查当前遇到的字符是空格还是字符串的结尾。**
*   **如果发现当前字符是这样，则更新获得的最大单词长度。**
*   **最后，打印使用 [<u>substr()</u>](https://www.geeksforgeeks.org/substring-in-cpp/) 方法获得的最长单词。**

*****时间复杂度:** O(N)，其中 N 是字符串的长度。*
***辅助空间:** O(1)***

****进场使用** [**<u>排序()</u>**](https://www.geeksforgeeks.org/sorted-function-python/) **方法:**思路是将 [<u>中的单词串拆分成</u>](https://www.geeksforgeeks.org/python-string-split/)<u>[列表](https://www.geeksforgeeks.org/python-list/)和[排序列表](https://www.geeksforgeeks.org/python-list-sort/)按照单词长度的递增顺序使用[排序()](https://www.geeksforgeeks.org/sorted-function-python/)方法。最后，打印列表中的第一个字符串。</u>**

**下面是上述方法的实现:**

## **蟒蛇 3**

```
# Python3 program for the above approach

# Function to print the
# smallest word in the string s

def smallestWord(s):

    # Using sorted() method
    s = sorted(s, key = len)

    # Print first word
    print(s[0])

# Driver Code
if __name__ == "__main__":

    # Given string
    s = "sky is blue"

    # Convert string to list
    l = list(s.split(" "))

    smallestWord(l)
```

****Output:**

```
is

```** 

*****时间复杂度:** O(N * LogN)*
***辅助空间:** O(1)***