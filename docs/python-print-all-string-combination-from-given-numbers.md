# Python |打印给定数字的所有字符串组合

> 原文:[https://www . geesforgeks . org/python-print-all-string-combination-from-给定-numbers/](https://www.geeksforgeeks.org/python-print-all-string-combination-from-given-numbers/)

给定一个整数 *N* 作为输入，任务是按照字典顺序打印其中的所有字符串组合。

**示例:**

```
Input :  191
Output : aia sa
Explanation: 
The Possible String digit are 
1, 9 and 1 --> aia
19 and 1 --> sa

Input : 1119
Output : aaai aas aki kai ks

```

**进场:**

*   获取字符串，并按照给定的顺序找到它的所有组合列表。
*   查找整数在 0 到 25 范围内的列表。
*   将整数转换成字母。
*   按字典顺序排序。

```
# Python program to print all string
# combination from given numbers

# Function to find the combination
def Number_to_String(String):

    # length of string 
    length = len(String)

    # temporary lists
    temp1 =[]
    temp2 =[]

    # alphabets Sequence
    alphabet ="abcdefghijklmnopqrstuvwxyz"

    # Power variable
    power = 2**(length-1)

    for i in range(0, power):

        # temporary String
        sub = ""
        Shift = i 
        x = 0
        sub += String[x]
        x += 1
        for j in range(length - 1):
            if Shift&1:
                sub+=" "
            Shift = Shift>>1
            sub += String[x]
            x += 1 
        temp1.append(list(map(int, sub.split())))

    # Integer to String     
    for index in temp1: 
        substring =""
        for j in index:
            if j > 0 and j <= 26: 
                substring += alphabet[j-1]
        if len(substring) == len(index):
            temp2.append(substring)

    # lexicographical order sorting
    print(*sorted(temp2), sep =" ")

# Driver Code
Number_to_String("191")
Number_to_String("1991")
Number_to_String("1532")
Number_to_String("1191")
```

**Output:**

```
aia sa
aiia sia
aecb ocb
aaia asa kia

```