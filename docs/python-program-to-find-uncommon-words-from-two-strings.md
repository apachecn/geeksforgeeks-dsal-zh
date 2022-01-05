# Python 程序从两个字符串中查找生僻字

> 原文:[https://www . geesforgeks . org/python-程序-从两个字符串中查找不常见单词/](https://www.geeksforgeeks.org/python-program-to-find-uncommon-words-from-two-strings/)

以字符串形式给出两个句子 **A** 和 **B** 。任务是返回所有**生僻字**的列表。如果一个单词在任何一个句子中出现**一次**，而在另一个句子中没有出现，那么这个单词就不常见了。

**注意:**一个句子是一串用空格分隔的单词。每个单词只由小写字母组成。

**示例**:

```
Input : A = "Geeks for Geeks" 
        B = "Learning from Geeks for Geeks"
Output : ['Learning', 'from']

Input : A = "apple banana mango" 
        B = "banana fruits mango"
Output : ['apple', 'fruits']

```

**方法:**每一个不常见的单词在任何一个字符串中都恰好出现一次。所以，我们做一个散列来计算每个单词的出现次数，然后返回一个恰好出现一次的单词列表。

下面是上述方法的实现:

```
# Python3 program to find a list of uncommon words

# Function to return all uncommon words
def UncommonWords(A, B):

    # count will contain all the word counts
    count = {}

    # insert words of string A to hash
    for word in A.split():
        count[word] = count.get(word, 0) + 1

    # insert words of string B to hash
    for word in B.split():
        count[word] = count.get(word, 0) + 1

    # return required list of words
    return [word for word in count if count[word] == 1]

# Driver Code
A = "Geeks for Geeks"
B = "Learning from Geeks for Geeks"

# Print required answer
print(UncommonWords(A, B))
```

**Output:**

```
['from', 'Learning']

```

 **解决这个问题的另一种方法:**

```
def uncommon(a,b):
    list_a = a.split()
    list_b = b.split()
    uc = ''
    for i in list_a:
        if i not in list_b:
            uc = uc+" "+i
    for j in list_b:
        if j not in list_a:
            uc = uc+" "+j

    return uc

# Driver code
a = "apple banana mango"
b = "banana fruits mango"
print(uncommon(a,b))
```

**Output:**

```
['apple','fruits']

```

**还有另一种方式——使用内置函数“symmetric _ difference()”**

```
def uncommon(a,b):
  a=a.split()
  b=b.split()
  k=set(a).symmetric_difference(set(b))
  return k

#Driver code
if __name__=="__main__":
  a="apple banana mango" 
  b="banana fruits mango"
  print(list(uncommon(a,b)))
```

**Output:**

```
['apple', 'fruits']

```

**解决这个问题的另一种方法**

```
def uncommon(A, B):
    un_comm = [i for i in "".join(B).split() if i not in "".join(A).split()]
    return un_comm

#Driver code
A = "Geeks for Geeks" 
B = "Learning from Geeks for Geeks"
print(uncommon(A, B))
```

**Output:**

```
['Learning', 'from']

```