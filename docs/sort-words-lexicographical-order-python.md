# 在 Python 中按照字典顺序对单词进行排序

> 原文:[https://www . geesforgeks . org/sort-words-辞书-order-python/](https://www.geeksforgeeks.org/sort-words-lexicographical-order-python/)

给定一个字符串，我们需要按照字典顺序(字典顺序)对单词进行排序。

示例:

```
Input :  "hello python program how are you"
Output :  are
          hello
          how
          program
          python
          you

Input :   "Coders loves the algorithms"
Output :  Coders
          algorithms
          loves
          the

```

注:第一个字母是大写字母的单词将按字母顺序打印。

**方法:**
这个程序中使用的方法非常简单。使用 Split()函数拆分字符串。之后，使用 sort()按照字典顺序对单词进行排序。通过循环迭代单词并打印每个已经排序的单词。

```
# Python program to sort the words in lexicographical
# order

def sortLexo(my_string):

    # Split the my_string till where space is found.
    words = my_string.split()

    # sort() will sort the strings.
    words.sort()

    # Iterate i through 'words' to print the words
    # in alphabetical manner.
    for i in words:
        print( i ) 

# Driver code 
if __name__ == '__main__':

    my_string = "hello this is example how to sort " \
              "the word in alphabetical manner"
    # Calling function
    sortLexo(my_string)
```

输出:

```
alphabetical
example
hello
how
in
is
manner
sort
the
this
to
word

```