# Python 列表排序()方法

> 原文:[https://www.geeksforgeeks.org/python-list-sort-method/](https://www.geeksforgeeks.org/python-list-sort-method/)

Python list sort()函数可用于按照升序、降序或用户定义的顺序对一个[列表](https://www.geeksforgeeks.org/python-list/)进行排序。

### **按升序排列列表**

> **语法:**
> 
> List_name.sort()
> 
> 这将按升序对给定列表进行排序。该函数可用于对整数、浮点数、字符串等列表进行排序。

### 示例 1: **按升序排列列表**

## 蟒蛇 3

```
numbers = [1, 3, 4, 2]

# Sorting list of Integers in ascending
numbers.sort()

print(numbers)
```

**输出:**

```
[1, 2, 3, 4]
```

### 示例 1.1

## 蟒蛇 3

```
strs = ["geeks", "code", "ide", "practice"]

# Sorting list of Integers in ascending
strs.sort()

print(strs)
```

**输出:**

```
['code', 'geeks', 'ide', 'practice']
```

### **按降序排列列表**

> **语法:**
> 
> 列表名称排序(反向=真)
> 
> 这将按降序对给定列表进行排序。

### 示例 2: **按降序排列列表**

## 蟒蛇 3

```
numbers = [1, 3, 4, 2]

# Sorting list of Integers in descending
numbers.sort(reverse = True)

print(numbers)
```

**输出:**

```
[4, 3, 2, 1]
```

### **使用自定义顺序排序**

> **语法:**
> 
> list_name.sort(key=…，reverse =…)–它根据用户的选择进行排序
> 
> **参数:**
> 
> *   **反转:**反转=真将对列表进行降序排序。默认值为反向=假
> *   **键:**指定分类标准的功能

### 示例 3: **使用用户定义的顺序排序**

## 计算机编程语言

```
# Python program to demonstrate sorting by user's
# choice

# function to return the second element of the
# two elements passed as the parameter
def sortSecond(val):
    return val[1] 

# list1 to demonstrate the use of sorting 
# using using second key 
list1 = [(1, 2), (3, 3), (1, 1)]

# sorts the array in ascending according to 
# second element
list1.sort(key = sortSecond) 
print(list1)

# sorts the array in descending according to
# second element
list1.sort(key = sortSecond, reverse = True)
print(list1)
```

**输出:**

```
[(1, 1), (1, 2), (3, 3)]
[(3, 3), (1, 2), (1, 1)]
```