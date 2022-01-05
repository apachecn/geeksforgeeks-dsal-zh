# Python3 将所有 0 移动到数组末尾的程序

> 原文:[https://www . geeksforgeeks . org/python 3-程序将全零移动到数组末尾/](https://www.geeksforgeeks.org/python3-program-to-move-all-zeroes-to-end-of-array/)

给定一个随机数数组，将给定数组的所有零推到数组的末尾。例如，如果给定的数组是{1，9，8，4，0，0，2，7，0，6，0}，则应该将其更改为{1，9，8，4，2，7，6，0，0，0，0}。所有其他元素的顺序应该相同。预期时间复杂度为 0(n)，额外空间为 0(1)。
**例:**

```
Input :  arr[] = {1, 2, 0, 4, 3, 0, 5, 0};
Output : arr[] = {1, 2, 4, 3, 5, 0, 0};

Input : arr[]  = {1, 2, 0, 0, 0, 3, 6};
Output : arr[] = {1, 2, 3, 6, 0, 0, 0};
```

有很多方法可以解决这个问题。下面是一个简单有趣的方法来解决这个问题。
从左到右遍历给定的数组“arr”。遍历时，保持数组中非零元素的计数。让计数成为“计数”。对于每个非零元素 arr[i]，将该元素置于' arr[count]'并递增' count '。在完成遍历后，所有非零元素已经被转移到前端，“计数”被设置为第一个 0 的索引。现在我们所需要做的就是运行一个循环，使所有元素从“计数”到数组结束都为零。
以下是上述方法的实现。

## 蟒蛇 3

```
# Python3 code to move all zeroes
# at the end of array

# Function which pushes all
# zeros to end of an array.
def pushZerosToEnd(arr, n):
    count = 0 # Count of non-zero elements

    # Traverse the array. If element 
    # encountered is non-zero, then
    # replace the element at index
    # 'count' with this element
    for i in range(n):
        if arr[i] != 0:

            # here count is incremented
            arr[count] = arr[i]
            count+=1

    # Now all non-zero elements have been
    # shifted to front and 'count' is set
    # as index of first 0\. Make all 
    # elements 0 from count to end.
    while count < n:
        arr[count] = 0
        count += 1

# Driver code
arr = [1, 9, 8, 4, 0, 0, 2, 7, 0, 6, 0, 9]
n = len(arr)
pushZerosToEnd(arr, n)
print("Array after pushing all zeros to end of array:")
print(arr)

# This code is contributed by "Abhishek Sharma 44"
```

**输出:**

```
Array after pushing all zeros to end of array :
1 9 8 4 2 7 6 9 0 0 0 0
```

**时间复杂度:** O(n)，其中 n 为输入数组中的元素个数。
**辅助空间:** O(1)

详情请参考[将所有零移到数组](https://www.geeksforgeeks.org/move-zeroes-end-array/)末尾的完整文章！