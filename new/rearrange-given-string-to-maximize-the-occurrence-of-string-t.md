# 重新排列给定的字符串以最大化出现字符串`t`

> 原文：[https://www.geeksforgeeks.org/rearrange-given-string-to-maximize-the-occurrence-of-string-t/](https://www.geeksforgeeks.org/rearrange-given-string-to-maximize-the-occurrence-of-string-t/)

给定两个二进制字符串`s`和`t`。 任务是重新排列字符串`s`，使得在`s`中作为子字符串的字符串`t`的出现最大。

**示例**：

> **输入**：`s = "101101", t = "110"`
>
> **输出**：110110
> 
> **输入**：`s = "10", t = "11100"`
>
> **输出**：10
> 
> **输入**：`s = "11000100", t = "101"`
>
> **输出**：10101000

**方法**：如果无法在字符串`s`中出现字符串`t`，则输出`s`的任何排列。 否则，使用`t`开始重新排列的字符串。 现在，我们将使字符串`s`中字符串`t`的下一个出现尽可能左，以使出现次数最大化。 为此，我们将找到与长度相同的字符串`t`。

的前缀匹配的字符串`t`的最大后缀。 可以通过“前缀功能”，“Z 功能”或“哈希”找到。

下面是上述方法的实现：

```
# Python3 implementation of the approach
from collections import defaultdict
# Function to return the length of maximum
# proper suffix which is also proper prefix
def Prefix_Array(t):
m = len(t)
arr =[-1]*m
k =-1
for i in range(1, m):
while k>-1 and t[k + 1]!= t[i]:
k = arr[k]
if t[k + 1]== t[i]:
k+= 1
arr[i]= k
return arr[-1]
# Function to return the rearranged string
def Rearranged(ds, dt):
check = Prefix_Array(t)
# If there is no proper suffix which is
# also a proper prefix
if check ==-1:
if ds['1']<dt['1'] or ds['0']<dt['0']:
return s
# If count of 1's in string t is 0
if dt['1']== 0 and ds['0']!= 0:
n = ds['0']//dt['0']
temp = t * n
ds['0']-= n * dt['0']
while ds['1']>0:
temp+='1'
ds['1']-= 1
while ds['0']>0:
temp+='0'
ds['0']-= 1
# Return the rearranged string
return temp
# If count of 0's in string t is 0
if dt['0']== 0 and ds['1']!= 0:
n = ds['1']//dt['1']
temp = t * n
ds['1']-= n * dt['1']
while ds['1']>0:
temp+='1'
ds['1']-= 1
while ds['0']>0:
temp+='0'
ds['0']-= 1
# Return the rearranged string
return temp
# If both 1's and 0's are present in
# string t
m1 = ds['1']//dt['1']
m2 = ds['0']//dt['0']
n = min(m1, m2)
temp = t * n
ds['1']-= n * dt['1']
ds['0']-= n * dt['0']
while ds['1']>0:
temp+='1'
ds['1']-= 1
while ds['0']>0:
temp+='0'
ds['0']-= 1
return temp
# If there is a suffix which is
# also a prefix in string t
else:
if ds['1']<dt['1'] or ds['0']<dt['0']:
return s
# Append the remaining string each time
r = t[check + 1:]
dr = defaultdict(int)
for v in r:
dr[v]+= 1
temp = t
ds['1']-= dt['1']
ds['0']-= dt['0']
# If we can't form the string t
# by the remaining 0's and 1's
if ds['1']<dr['1'] or ds['0']<dr['0']:
while ds['1']>0:
temp+='1'
ds['1']-= 1
while ds['0']>0:
temp+='0'
ds['0']-= 1
return temp
# If count of 1's in string r is 0
if dr['1']== 0 and ds['0']!= 0:
n = ds['0']//dr['0']
temp+= r * n
ds['0']-= n * dr['0']
while ds['1']>0:
temp+='1'
ds['1']-= 1
while ds['0']>0:
temp+='0'
ds['0']-= 1
return temp
# If count of 0's in string r is 0
if dr['0']== 0 and ds['1']!= 0:
n = ds['1']//dr['1']
temp+= r * n
ds['1']-= n * dr['1']
while ds['1']>0:
temp+='1'
ds['1']-= 1
while ds['0']>0:
temp+='0'
ds['0']-= 1
return temp
# If string r have both 0's and 1's
m1 = ds['1']//dr['1']
m2 = ds['0']//dr['0']
n = min(m1, m2)
temp+= r * n
ds['1']-= n * dr['1']
ds['0']-= n * dr['0']
while ds['1']>0:
temp+='1'
ds['1']-= 1
while ds['0']>0:
temp+='0'
ds['0']-= 1
return temp
# Driver code
if __name__=="__main__":
s ="10101000"
t ="101"
# Count of 0's and 1's in string s
ds = defaultdict(int)
# Count of 0's and 1's in string t
dt = defaultdict(int)
for i in s:
ds[i]= ds[i]+1
for i in t:
dt[i]= dt[i]+1
print(Rearranged(ds, dt))
```

**输出**：

```
10101000

```



* * *

* * *



