# Python 字典查找字符串中的镜像字符

> 原文:[https://www . geesforgeks . org/python-dictionary-find-mirror-characters-string/](https://www.geeksforgeeks.org/python-dictionary-find-mirror-characters-string/)

给定一个字符串和一个数字 N，我们需要按照字母顺序将字符从第 N 个位置镜像到字符串的长度。在镜像操作中，我们将“a”改为“z”，“b”改为“y”等等。
示例:

```
Input : N = 3
        paradox
Output : paizwlc
We mirror characters from position 3 to end.

Input : N = 6
        pneumonia
Output : pneumlmrz
```

对于这个问题，我们有一个现有的解决方案，请参考[字符串的镜像字符](https://www.geeksforgeeks.org/mirror-characters-string/)链接。我们可以使用[字典数据结构](https://www.youtube.com/watch?v=z7z_e5-l2yE&t=82s)在 Python 中解决这个问题。“a”的镜像值是“z”，“b”是“y”等，因此我们创建了一个字典数据结构，并将字母表的反向序列一对一地映射到字母表的原始序列上。现在遍历给定字符串中长度为 k 的字符，并使用字典将字符更改为它们的镜像值。

## 蟒蛇 3

```
# function to mirror characters of a string

def mirrorChars(input,k):

    # create dictionary
    original = 'abcdefghijklmnopqrstuvwxyz'
    reverse = 'zyxwvutsrqponmlkjihgfedcba'
    dictChars = dict(zip(original,reverse))

    # separate out string after length k to change
    # characters in mirror
    prefix = input[0:k-1]
    suffix = input[k-1:]
    mirror = ''

    # change into mirror
    for i in range(0,len(suffix)):
         mirror = mirror + dictChars[suffix[i]]

    # concat prefix and mirrored part
    print (prefix+mirror)

# Driver program
if __name__ == "__main__":
    input = 'paradox'
    k = 3
    mirrorChars(input,k)
```

**输出:**

```
paizwlc
```