# TCS 全国预选赛 2 号编码题。

> 原文:[https://www . geesforgeks . org/TCS-national-qualifier-2-coding-question/](https://www.geeksforgeeks.org/tcs-national-qualifier-2-coding-question/)

给你一个字符串，你的任务是打印每个字符的频率。

**解决问题的方向:**

1.从 STDIN 获取字符串。

```
aaaabbBcddee
```

2.使用 set()获取给定字符串中的所有不同字符。

```
set ={a, b, B, c, d, e}  # unordered set
```

3.对不同的字符(len(set))进行迭代，因为我们只需要打印一次一个字符，它就计入了输入字符串

```
range 0 to 5 i.e total 6 element
```

4.在每次迭代中，取第一个字符，打印它和它的计数。

```
now for 0
input_string[0]  is 'a' and its count is 4
```

5 .删除第一个字符的所有出现，这将使下一个字符成为第一个字符。

```
remove 'a' by replacing all 'a' in string by ""
new input string will be
bbBcddee
```

6.重复同样的过程，转到步骤 4。
7。要么在每次迭代时将值打印到 STDOUT(python 3)，要么一次性打印(python2)，您的输出将与

```
a4b2B1c1d2e2
```

**示例:**

```
Input : aaaabbBcddee
Output :a4b2B1c1d2e2

Input :aazzZ
Output :a2z2Z1 
```

## 计算机编程语言

```
# Python2 code here
input_string = raw_input()
temp_string =""
for _ in range(len(set(input_string))):
    temp_string += input_string[0] + str(input_string.count(input_string[0]))
    input_string = input_string.replace(input_string[0], "")
print temp_string
```

## 蟒蛇 3

```
# Python3 code here
input_string = input()
for _ in range(len(set(input_string))):
    print(input_string[0]+str(input_string.count(input_string[0])), end ="")
    input_string = input_string.replace(input_string[0], "")
```