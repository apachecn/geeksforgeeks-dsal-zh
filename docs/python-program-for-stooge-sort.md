# 用于走狗排序的 Python 程序

> 原文:[https://www . geeksforgeeks . org/python-程序换走狗-sort/](https://www.geeksforgeeks.org/python-program-for-stooge-sort/)

Stooge 排序是一种递归排序算法。其定义如下(用于升序排序)。

```
Step 1 : If value at index 0 is greater than
         value at last index, swap them.
Step 2:  Recursively,
       a) Stooge sort the initial 2/3rd of the array.
       b) Stooge sort the last 2/3rd of the array.
       c) Stooge sort the initial 2/3rd again to confirm.

```

## 蟒 3

```
# Python program to implement stooge sort

def stoogesort(arr, l, h):
    if l >= h:
        return

    # If first element is smaller
    # than last,swap them
    if arr[l]>arr[h]:
        t = arr[l]
        arr[l] = arr[h]
        arr[h] = t

    # If there are more than 2 elements in
    # the array
    if h-l+1 > 2:
        t = (int)((h-l+1)/3)

        # Recursively sort first 2/3 elements
        stoogesort(arr, l, (h-t))

        # Recursively sort last 2/3 elements
        stoogesort(arr, l+t, (h))

        # Recursively sort first 2/3 elements
        # again to confirm
        stoogesort(arr, l, (h-t))

# deriver 
arr = [2, 4, 5, 3, 1]
n = len(arr)

stoogesort(arr, 0, n-1)

for i in range(0, n):
    print(arr[i], end = \' \')

# Code Contributed by Mohit Gupta_OMG <(0_o)>
```

**输出:**

```
1 2 3 4 5 

```

详情请参考[走狗排序](https://www.geeksforgeeks.org/stooge-sort/)完整文章！