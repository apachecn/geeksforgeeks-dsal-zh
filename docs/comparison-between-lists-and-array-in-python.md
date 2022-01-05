# Python 中列表和数组的比较

> 原文:[https://www . geesforgeks . org/python 中列表和数组的比较/](https://www.geeksforgeeks.org/comparison-between-lists-and-array-in-python/)

### Python 列表

Python 编程语言有四种集合数据类型，即**列表、元组、集合和字典**。列表是一个可变的有序集合，也就是说，列表的元素可以被改变，并且它保持其条目的插入顺序。由于保持顺序的特性，列表的每个元素都有一个固定的索引，并且允许列表有重复的元素。在 Python 中，列表非常有用，因为它能够包含非同构元素。

以下是可以在列表中执行的一些操作:

```
# Python program to demonstrate
# some operations on list

# Declaring a List of integers 
IntList = [10, 20, 30] 
print("List of numbers: ")

# Printing the list 
print(IntList) 

# Declaring a List of strings
StrList = ["Geeks", "For", "Geeks"] 
print("List of Strings: ")

# Printing the list 
print(StrList) 

# Declaring a list of non-homogeneous elements
Non_homogeneous_list = [10, "Geeks", 20.890,\
                        "for", 30, "geeks"]
print("List of non-homogeneous elements: ")

# Printing the list
print(Non_homogeneous_list)

# Printing size of a list
print("Size of the Non-homogeneous list: ",\
            len(Non_homogeneous_list))

# Declaring a list
NewList = ["Geeks", "for", "Geeks"]
print("Original List: ", NewList)

# Adding an item to the list

# Adding an item in the list 
# using the append method
NewList.append("the")

# Printing the modified list
print("After adding an element the"\
                     "list becomes: ")
print(NewList)

# Adding an item in the list using the insert 
# method to add an element at a specific position
NewList.insert(3, "is")

# Printing the modified list
print("After adding an element at"\
        "index 3 the list becomes: ")
print(NewList) 

# Adding multiple items to the list at the
# end using extend method
NewList.extend(["best", "CS", "website"]) 

# Printing the modified list
print("After adding 3 elements at the"\
              "end, the list becomes: ")
print(NewList)

# Removing an item from the list

# Removing an element by 
# writing the element itself
NewList.remove("the")

# Printing the modified list
print("After removing an element"\
               "the list becomes: ")
print(NewList)

# Removing an element by 
# specifying its position
NewList.pop(3)

# Printing the modified list
print("After removing an element "\
    "from index 3 the list becomes: ")
print(NewList)
```

**输出:**

```
List of numbers: 
[10, 20, 30]
List of Strings: 
['Geeks', 'For', 'Geeks']
List of non-homogeneous elements: 
[10, 'Geeks', 20.89, 'for', 30, 'geeks']
Size of the Non-homogeneous list:  6
Original List:  ['Geeks', 'for', 'Geeks']
After adding an element thelist becomes: 
['Geeks', 'for', 'Geeks', 'the']
After adding an element atindex 3 the list becomes: 
['Geeks', 'for', 'Geeks', 'is', 'the']
After adding 3 elements at theend, the list becomes: 
['Geeks', 'for', 'Geeks', 'is', 'the', 'best', 'CS', 'website']
After removing an elementthe list becomes: 
['Geeks', 'for', 'Geeks', 'is', 'best', 'CS', 'website']
After removing an element from index 3 the list becomes: 
['Geeks', 'for', 'Geeks', 'best', 'CS', 'website']

```

要获得更多关于 python 列表的深入知识，请点击这里的。

### Python 数组

Python 数组也是一个集合，但是它的项目存储在连续的内存位置。它只能存储同类元素(相同数据类型的元素)。数组在对元素执行数学运算时非常有用。与列表不同，数组不能直接声明。要创建数组，必须导入`array`模块，声明的语法与列表的语法不同。

以下是可以在阵列上执行的一些操作:

```
# Python program to demonstrate
# some operations on arrays

# importing array module 
import array as arr

# declaring an array of integer type
# 'i' signifies integer type and
# elements inside [] are the array elements 
a1 = arr.array('i', [10, 20, 30])

# printing array with 
# data type and elements
print("Array a1: ", a1)

# printing elements of array
print ("Elements of the array"\
         "a1 is : ", end = " ") 
for i in range (len(a1)): 
    print (a1[i], end =", ")
print()

# Declaring an array of float type
# 'd' signifies integer type and
# elements inside [] are the array elements 
a2 = arr.array('d', [1.5, 2.4, 3.9])

# printing elements of array
print ("Elements of the array"\
          "a2 is : ", end = " ") 
for i in range (len(a2)): 
    print (a2[i], end =", ")
print()

# Adding an item to the array

# Printing the elements of array a1
print ("Original elements of the"\
       "array a1 is : ", end = " ") 
print(*a1)

# Adding an element at the end of
# array by using the append method
a1.append(40)

# printing the modified array
print ("Elements of the array a1"\
           "after adding an element"\
           "at last: ", end = " ")
print(*a1)

# Adding an element to the array at a 
# specific index using the insert method
a1.insert(3, 35)

# printing the modified array
print ("Elements of the array a1"\
           "after adding an element"\
           "at index 3: ", end = " ")
print(*a1)

# Removing an element from the array

# Removing an element by writing the elements itself
a1.remove(20)

# Printing the modified array
print("Array a1 after removing"\
        "element 20: ", end = " ")
print(*a1)

# Removing an element of a specific index
# Removing the element of array a1 present at index 2
a1.pop(2)

# Printing the modified array
print("Array a1 after removing"\
"element of index 2: ", end = " ")
print(*a1)
```

**输出:**

```
Array a1:  array('i', [10, 20, 30])
Elements of the arraya1 is :  10, 20, 30, 
Elements of the arraya2 is :  1.5, 2.4, 3.9, 
Original elements of thearray a1 is :  10 20 30
Elements of the array a1after adding an elementat last:  10 20 30 40
Elements of the array a1after adding an elementat index 3:  10 20 30 35 40
Array a1 after removingelement 20:  10 30 35 40
Array a1 after removingelement of index 2:  10 30 40

```

要获得更多关于 python 数组的深入知识，请点击这里的。

### Python 列表和数组的相似之处

**数组和列表都用于存储数据:**两个集合的目的都是存储数据。虽然列表用于存储同类和非同类数据，但数组只能存储同类数据。

```
# Python program to demonstrate data 
# storing similarities in array and list

# importing array module 
import array as arr

# Declaring a Homogeneous List of strings
Homogeneous_List = ["Geeks", "For", "Geeks"] 
print("List of Strings: ")

# Printing the list 
print(Homogeneous_List) 

# Declaring a list of 
# non-homogeneous elements
Non_homogeneous_list = [10, "Geeks",\
        20.890, "for", 30, "geeks"]
print("List of non-homogeneous elements: ")

# Printing the list
print(Non_homogeneous_list)

# declaring an array of float type
# 'd' signifies integer type and
# elements inside [] are the array elements 
Homogeneous_array = arr.array('d',\
                [1.5, 2.4, 3.9])

# printing elements of array
print ("Elements of the array is"\
                " : ", end = " ") 
for i in range (len(Homogeneous_array)): 
    print (Homogeneous_array[i], end =", ")
```

**输出:**

```
List of Strings: 
['Geeks', 'For', 'Geeks']
List of non-homogeneous elements: 
[10, 'Geeks', 20.89, 'for', 30, 'geeks']
Elements of the array is :  1.5, 2.4, 3.9,

```

**列表和数组都是可变的:**列表和数组都可以修改它们的元素，即它们是可变的。

```
# Python program to demonstrate 
# both the list and array is mutable

# importing array module 
import array as arr

# Declaring a list
List1 = ["Geeks", 1, "Geeks"]

# Printing original list
print("Original list: ", List1)

# Changing the value of the 
# element at a specific index
List1[1] = "for"

# Printing modified list
print("\nModified list: ", List1)

# Declaring an array with integers values
Array1 = arr.array('i', \
   [10, 20, 30, 37, 50, ])  

# Printing original array 
print ("\nOriginal array: ", end =" ") 
for i in range (len(Array1)): 
    print (Array1[i], end =" ") 

# Updating an element in the array 
Array1[3] = 40

# Printing modified Array:
print("\nModified array: ", end ="") 
for i in range (len(Array1)): 
    print (Array1[i], end =" ") 
```

**输出:**

```
Original list:  ['Geeks', 1, 'Geeks']

Modified list:  ['Geeks', 'for', 'Geeks']

Original array:  10 20 30 37 50 
Modified array: 10 20 30 40 50

```