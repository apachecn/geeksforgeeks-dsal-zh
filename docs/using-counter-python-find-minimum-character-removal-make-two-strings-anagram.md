# 使用 Python 中的 Counter()查找最小字符去除量制作两串字谜

> 原文:[https://www . geesforgeks . org/using-counter-python-find-minimum-character-remove-make-two-strings-anagram/](https://www.geeksforgeeks.org/using-counter-python-find-minimum-character-removal-make-two-strings-anagram/)

给定两个小写字符串，任务是使它们成为[字谜](https://www.geeksforgeeks.org/check-whether-two-strings-are-anagram-of-each-other/)。唯一允许的操作是从任何字符串中删除一个字符。找到要删除的最小字符数以使两个字符串都成为字谜？
如果两个字符串以任何顺序包含相同的数据集，那么字符串被称为**字谜**。

示例:

```
Input : str1 = "bcadeh" str2 = "hea"
Output: 3
We need to remove b, c and d from str1.

Input : str1 = "cddgk" str2 = "gcd"
Output: 2

Input : str1 = "bca" str2 = "acb"
Output: 0

```

此问题已有解决方案请参考[删除最小字符数，使两个字符串成为字谜](https://www.geeksforgeeks.org/remove-minimum-number-characters-two-strings-become-anagram/)链接。我们将使用数据结构的[计数器()](https://www.geeksforgeeks.org/counters-in-python-set-1/)和[字典数据结构](https://www.youtube.com/watch?v=z7z_e5-l2yE&t=28s)和**交集**属性在 python 中快速解决这个问题。方法很简单，

1.  使用 **Counter(iterable)** 方法将每个字符串转换为字典数据结构。
2.  计算两个字典中的键数(count1，count2)并计算两个字典中共有的键数。
3.  如果没有找到公共键，这意味着我们需要从两个字符串中删除 **count1 + count2** 字符。
4.  否则**(最大(count1，count 2)–count common)**将是要删除的字符数

    ```
    # Function remove minimum number of characters so that 
    # two strings become anagram 
    from collections import Counter 
    def removeChars(str1, str2): 

        # make dictionaries from both strings 
        dict1 = Counter(str1) 
        dict2 = Counter(str2) 

        # extract keys from dict1 and dict2 
        keys1 = dict1.keys() 
        keys2 = dict2.keys() 

        # count number of keys in both lists of keys 
        count1 = len(keys1) 
        count2 = len(keys2) 

        # convert list of keys in set to find common keys 
        set1 = set(keys1) 
        commonKeys = len(set1.intersection(keys2)) 

        if (commonKeys == 0): 
            return count1 + count2 
        else: 
            return (max(count1, count2)-commonKeys) 

    # Driver program 
    if __name__ == "__main__": 
        str1 ='bcadeh'
        str2 ='hea'
        print (removeChars(str1, str2)) 
    ```

    输出:

    ```
    3

    ```

     **备选方案:**

    1.  使用 **Counter(iterable)** 方法将每个字符串转换为字典数据结构。
    2.  从两个字典中找出共同的元素
    3.  将公共字典中的值相加，得到公共元素的总数。

        ```
        # Function remove minimum number of characters so that 
        # two strings become anagram 
        from collections import Counter 
        def removeChars(a, b): 

            # make dictionaries from both strings 
            c1 = Counter(a) 
            c2 = Counter(b) 

            # finding the common elements from both dictonary 
            common = c1&c2 
            value = 0

            # adding up the key from common dictionary in order 
            # to get the total number of common elements 
            for key in common: 
                value = value + common[key] 

            # returning the number of elements to be 
            # removed to form an anagram 
            return (len(a)-2*value+ len(b))         

        # Driver program 
        if __name__ == "__main__": 
            str1 ='bcadeh'
            str2 ='hea'
            print (removeChars(str1, str2)) 
        ```

        输出:

        ```
        3

        ```