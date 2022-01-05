# 冒泡排序的 Python 程序

> 原文:[https://www . geeksforgeeks . org/python-program-for-bubble-sort/](https://www.geeksforgeeks.org/python-program-for-bubble-sort/)

冒泡排序是最简单的排序算法，如果相邻元素的顺序错误，可以通过重复交换它们来工作。

## 计算机编程语言

```
# Python program for implementation of Bubble Sort

def bubbleSort(arr):
    n = len(arr)

    # Traverse through all array elements
    for i in range(n-1):
    # range(n) also work but outer loop will
    # repeat one time more than needed.

        # Last i elements are already in place
        for j in range(0, n-i-1):

            # traverse the array from 0 to n-i-1
            # Swap if the element found is greater
            # than the next element
            if arr[j] > arr[j + 1] :
                arr[j], arr[j + 1] = arr[j + 1], arr[j]

# Driver code to test above
arr = [64, 34, 25, 12, 22, 11, 90]

bubbleSort(arr)

print ("Sorted array is:")
for i in range(len(arr)):
    print ("% d" % arr[i]),
```

**输出:**

```
Sorted array is:
 2
 10
 12
 18
 18
 39
 72
 85
```

更多详情请参考[气泡排序](https://www.geeksforgeeks.org/bubble-sort/)整篇文章！

## 计算机编程语言

```
def bubblesort(elements):
  # Looping from size of array from last index[-1] to index [0]
  for n in range(len(elements)-1, 0, -1):
    for i in range(n):
      if elements[i] > elements[i + 1]:
        # swapping data if the element is less than next element in the array
        elements[i], elements[i + 1] = elements[i + 1], elements[i]
elements = [39,12,18,85,72,10,2,18]

print("Unsorted list is,") 
print( elements)
bubblesort(elements)
print("Sorted Array is, ")
print(elements)
```

**输出:**

```
Unsorted list is,
[39, 12, 18, 85, 72, 10, 2, 18]
Sorted Array is, 
[2, 10, 12, 18, 18, 39, 72, 85]
```