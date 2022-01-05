# 从给定字符串中删除重复项的 Python 程序

> 原文:[https://www . geesforgeks . org/python-从给定字符串中删除重复项的程序/](https://www.geeksforgeeks.org/python-program-to-remove-duplicates-from-a-given-string/)

给定一个字符串 **S** ，任务是删除给定字符串中的所有重复项。
以下是删除字符串中重复项的不同方法。

## 计算机编程语言

```
string="geeksforgeeks"
k2=[]
for ele in k:
    if ele not in k2:
        k2.append(ele)
for i in range(0,len(k2)):
    print(k2[i],end="")
```

**方法 1(简单)**

## 蟒蛇 3

```
string="geeksforgeeks"
p=""
for char in string:
    if char not in p:
        p=p+char
print(p)
k=list("geeksforgeeks")
```

**输出:**

```
geksfor
```

**时间复杂度:**O(n * n)
T3】辅助空间: O(1)
保持元素顺序与输入相同。

**方法 2(使用 BST)**
使用[设置](https://www.geeksforgeeks.org/set-in-cpp-stl/)，实现二叉查找树的自平衡。

## 蟒蛇 3

```
# Python program to remove duplicate character
# from character array and print in sorted
# order
def removeDuplicate(str, n):
    s = set()

    # Create a set using String characters
    for i in str:
        s.add(i)

    # Print content of the set
    st = ""
    for i in s:
        st = st+i
    return st

# Driver code
str = "geeksforgeeks"
n = len(str)
print(removeDuplicate(list(str), n))

# This code is contributed by rajsanghavi9.
```

**输出:**

```
  efgkors
```

**时间复杂度**:O(n Log n)
T3】辅助空间 : O(n)

感谢阿尼维什·蒂瓦里 提出这种方法。

它不会保持元素的顺序与输入相同，而是按排序顺序打印它们。

**方法 3(使用排序)**
**算法:**

```
  1) Sort the elements.
  2) Now in a loop, remove duplicates by comparing the 
      current character with previous character.
  3)  Remove extra characters at the end of the resultant string.
```

**示例:**

```
Input string:  geeksforgeeks
1) Sort the characters
   eeeefggkkorss
2) Remove duplicates
    efgkorskkorss
3) Remove extra characters
     efgkors
```

请注意，此方法不保持输入字符串的原始顺序。例如，如果我们要删除 geeksforgeeks 的重复项，并保持字符的顺序不变，那么输出应该是 geksfor，但是上面的函数返回 efgkos。我们可以通过存储原始订单来修改此方法。

**实施:**

## 计算机编程语言

```
# Python program to remove duplicates, the order of
# characters is not maintained in this program

# Utility function to convert string to list
def toMutable(string):
    temp = []
    for x in string:
        temp.append(x)
    return temp

# Utility function to convert string to list
def toString(List):
    return ''.join(List)

# Function to remove duplicates in a sorted array
def removeDupsSorted(List):
    res_ind = 1
    ip_ind = 1

    # In place removal of duplicate characters
    while ip_ind != len(List):
        if List[ip_ind] != List[ip_ind-1]:
            List[res_ind] = List[ip_ind]
            res_ind += 1
        ip_ind+=1

    # After above step string is efgkorskkorss.
    # Removing extra kkorss after string
    string = toString(List[0:res_ind])

    return string

# Function removes duplicate characters from the string
# This function work in-place and fills null characters
# in the extra space left
def removeDups(string):
    # Convert string to list
    List = toMutable(string)

    # Sort the character list
    List.sort()

    # Remove duplicates from sorted
    return removeDupsSorted(List)

# Driver program to test the above functions
string = "geeksforgeeks"
print removeDups(string)

# This code is contributed by Bhavya Jain
```

**输出:**

```
efgkors
```

**时间复杂度:** O(n log n)如果我们用一些 n log n 排序算法来代替快速排序。

**辅助空间:** O(1)

**方法 4(使用散列法)**

**算法:**

```
1: Initialize:
    str  =  "test string" /* input string */
    ip_ind =  0          /* index to  keep track of location of next
                             character in input string */
    res_ind  =  0         /* index to  keep track of location of
                            next character in the resultant string */
    bin_hash[0..255] = {0,0, ….} /* Binary hash to see if character is 
                                        already processed or not */
2: Do following for each character *(str + ip_ind) in input string:
              (a) if bin_hash is not set for *(str + ip_ind) then
                   // if program sees the character *(str + ip_ind) first time
                         (i)  Set bin_hash for *(str + ip_ind)
                         (ii)  Move *(str  + ip_ind) to the resultant string.
                              This is done in-place.
                         (iii) res_ind++
              (b) ip_ind++
  /* String obtained after this step is "te stringing" */
3: Remove extra characters at the end of the resultant string.
  /*  String obtained after this step is "te string" */
```

**实施:**

## 计算机编程语言

```
# Python program to remove duplicate characters from an
# input string
NO_OF_CHARS = 256

# Since strings in Python are immutable and cannot be changed
# This utility function will convert the string to list
def toMutable(string):
    List = []
    for i in string:
        List.append(i)
    return List

# Utility function that changes list to string
def toString(List):
    return ''.join(List)

# Function removes duplicate characters from the string
# This function work in-place and fills null characters
# in the extra space left
def removeDups(string):
    bin_hash = [0] * NO_OF_CHARS
    ip_ind = 0
    res_ind = 0
    temp = ''
    mutableString = toMutable(string)

    # In place removal of duplicate characters
    while ip_ind != len(mutableString):
        temp = mutableString[ip_ind]
        if bin_hash[ord(temp)] == 0:
            bin_hash[ord(temp)] = 1
            mutableString[res_ind] = mutableString[ip_ind]
            res_ind+=1
        ip_ind+=1

     # After above step string is stringiittg.
     # Removing extra iittg after string
    return toString(mutableString[0:res_ind])

# Driver program to test the above functions
string = "geeksforgeeks"
print(removeDups(string))

# A shorter version for this program is as follows
# import collections
# print ''.join(collections.OrderedDict.fromkeys(string))

# This code is contributed by Bhavya Jain
```

**输出:**

```
geksfor
```

**时间复杂度:** O(n)

**要点:**

*   方法 2 没有将字符保持为原始字符串，但是方法 4 保持了。
*   假设输入字符串中可能的字符数是 256。应该相应地改变字符数。
*   calloc()代替 malloc()用于计数数组(count)的内存分配，以将分配的内存初始化为“”。也可以使用 malloc()后跟 memset()。
*   如果给定数组中整数的范围，上述算法也适用于整数数组输入。一个示例问题是，假设输入数组只包含 1000 到 1100 之间的整数，则找出输入数组中出现的最大数字

**方法 5** (使用**索引 Of()** 方法):
T5】先决条件:T7】Java**索引 Of()** 方法

## 蟒蛇 3

```
# Python 3 program to create a unique string

# Function to make the string unique

def unique(s):

    st = ""
    length = len(s)

    # loop to traverse the string and
    # check for repeating chars using
    # IndexOf() method in Java
    for i in range(length):

        # character at i'th index of s
        c = s[i]

        # if c is present in str, it returns
        # the index of c, else it returns - 1
        # print(st.index(c))
        if c not in st:
            # adding c to str if -1 is returned
            st += c

    return st

# Driver code
if __name__ == "__main__":

    # Input string with repeating chars
    s = "geeksforgeeks"

    print(unique(s))

    # This code is contributed by ukasp.
```

**输出:**

```
geksfor
```

感谢 [**debjitdbb**](https://auth.geeksforgeeks.org/user/debjitdbb/articles) 提出这个方法。
更多详细信息，请参考完整文章[删除给定字符串中的重复项](https://www.geeksforgeeks.org/remove-duplicates-from-a-given-string/)！