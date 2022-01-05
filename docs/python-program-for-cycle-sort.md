# 循环排序 Python 程序

> 原文:[https://www . geeksforgeeks . org/python-循环排序程序/](https://www.geeksforgeeks.org/python-program-for-cycle-sort/)

循环排序是一种就地排序算法，[不稳定排序算法](https://en.wikipedia.org/wiki/Sorting_algorithm#Stability)，这是一种比较排序，就对原始阵列的总写入次数而言，理论上是最佳的。

*   就内存写入次数而言，它是最佳的。它[最小化要排序的内存写入次数](https://www.geeksforgeeks.org/which-sorting-algorithm-makes-minimum-number-of-writes/)(每个值要么被写入零次，如果它已经在它的正确位置，要么被写入一次到它的正确位置。)
*   It is based on the idea that array to be sorted can be divided into cycles. Cycles can be visualized as a graph. We have n nodes and an edge directed from node i to node j if the element at i-th index must be present at j-th index in the sorted array.
    Cycle in arr[] = {4, 5, 2, 1, 5}
    ![cycle-sort](img/cd55c6aa03070152c4b2fe40ebe28d91.png)

    在 arr[]中循环= {4，3，2，1}
    ![cyclc-sort2](img/8499cbd17431ddffddd2b78678ab22a3.png)

我们一个一个考虑所有的周期。我们首先考虑包含第一个元素的循环。我们找到第一个元素的正确位置，把它放在正确的位置，比如 j。我们考虑 arr[j]的旧值，找到它的正确位置，我们一直这样做，直到当前周期的所有元素都放在正确的位置，也就是说，我们没有回到周期的起点。

## 蟒蛇 3

```
# Python program to impleament cycle sort

def cycleSort(array):
  writes = 0

  # Loop through the array to find cycles to rotate.
  for cycleStart in range(0, len(array) - 1):
    item = array[cycleStart]

    # Find where to put the item.
    pos = cycleStart
    for i in range(cycleStart + 1, len(array)):
      if array[i] < item:
        pos += 1

    # If the item is already there, this is not a cycle.
    if pos == cycleStart:
      continue

    # Otherwise, put the item there or right after any duplicates.
    while item == array[pos]:
      pos += 1
    array[pos], item = item, array[pos]
    writes += 1

    # Rotate the rest of the cycle.
    while pos != cycleStart:

      # Find where to put the item.
      pos = cycleStart
      for i in range(cycleStart + 1, len(array)):
        if array[i] < item:
          pos += 1

      # Put the item there or right after any duplicates.
      while item == array[pos]:
        pos += 1
      array[pos], item = item, array[pos]
      writes += 1

  return writes

#  driver code 
arr = [1, 8, 3, 9, 10, 10, 2, 4 ]
n = len(arr) 
cycleSort(arr)

print("After sort : ")
for i in range(0, n) : 
    print(arr[i], end = \' \')

# Code Contributed by Mohit Gupta_OMG <(0_o)>
```

**输出:**

```
After sort : 
1 2 3 4 8 9 10 10 

```

详情请参考[循环排序](https://www.geeksforgeeks.org/cycle-sort/)整篇文章！