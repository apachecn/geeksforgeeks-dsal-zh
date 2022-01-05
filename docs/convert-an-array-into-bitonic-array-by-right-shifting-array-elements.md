# 通过右移数组元素将数组转换为二进制数组

> 原文:[https://www . geeksforgeeks . org/通过右移数组元素将数组转换为二进制数组/](https://www.geeksforgeeks.org/convert-an-array-into-bitonic-array-by-right-shifting-array-elements/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是对数组元素执行[个右移位操作](https://www.geeksforgeeks.org/bitwise-shift-operators-in-java/)，将给定数组转换成[个双音素数组](https://www.geeksforgeeks.org/program-to-check-if-an-array-is-bitonic-or-not/)。

**示例:**

> **输入:** arr[] = {7，3，4，5，3}
> **输出:** 56 96 128 80 48
> **解释:**
> 对数组元素执行如下操作:
> 
> *   7 → 00000111 → 3 次右移→ 00111000 → 56
> *   3 → 00000011 → 5 次右移→ 01100000 → 96
> *   4 → 00000100 → 5 次右移→ 10000000 → 128
> *   5 → 00000101 → 4 右移→ 01010000 → 80
> *   3 → 00000011 → 4 右移→ 00110000 → 48
> 
> 经过上述操作后，修改后的数组是{56，96，128，80，48}，这是 Bitonic 数组。
> 
> **输入:** arr[] = {255，243，23，141，46}
> **输出:** -1

**方法:**按照给定的步骤解决问题

*   使用右移操作，最大化数组的[中间元素，即**arr【N/2】**。](https://www.geeksforgeeks.org/start-end-start2-preferrable-method-calculating-middle-array-start-end2/)
*   [遍历给定的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]，**通过对数组元素执行右移操作(如果需要)以升序转换数组的前半部分。
*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]，**通过对数组元素的右移操作(如果需要)以降序转换数组的后半部分。
*   完成上述步骤后，[检查数组是否为二进制](https://www.geeksforgeeks.org/program-to-check-if-an-array-is-bitonic-or-not/)。然后[打印数组](https://www.geeksforgeeks.org/c-program-to-print-an-array-using-recursion/) **arr[]** 作为结果数组。
*   否则，打印**-1”**。

下面是上述方法的实现:

## 蟒蛇 3

```
# Python program for the above approach

# Function to check if an
# array arr[] is Bitonic or not
def isPeak(arr):

    # Traverse the first half of arr[]
    for i in range(len(arr)//2, len(arr)-1):
        if arr[i] < arr[i + 1]:
            return False

    # Traverse the second half of arr[]
    for i in range(len(arr)//2):
        if arr[i] > arr[i + 1]:
            return False

    # Return true if arr[] is bitonic
    return True

# Function to maximize the value of N
# by performing right shift operations
def maximize(n):

    Ele = n
    ans = n

    for idx in range(7):

        # Right shift by 1
        if Ele & 1:
            Ele >>= 1
            Ele += 2**32
        else:
            Ele >>= 1

        # Update the value of ans
        ans = max(ans, Ele)

    return ans

# Function to arrange array in descending
# order by right shift operations
def makeDec(arr):

    # Maximise the array arr[0]
    prev = maximize(arr[0])
    arr[0] = prev

    # Iterate through array arr[]
    for i in range(1, len(arr)):

        optEle = arr[i]

        # Flag to find the first
        # element less than prev
        flag = True

        # Update Ele as arr[i]
        Ele = arr[i]

        for idx in range(7):

            # Right shift by 1
            if Ele & 1:
                Ele >>= 1
                Ele += 2**32
            else:
                Ele >>= 1

            if Ele < prev and flag:

                  # Update the optEle
                optEle = Ele

                # Unset the flag
                flag = False

            if Ele < prev:

                  # Update the optEle
                optEle = max(optEle, Ele)

          # Update the array arr[i]
        arr[i] = optEle

        # Update the value of prev
        prev = arr[i]

    # Return the array
    return arr

# Function to find the peak
# element of the array arr[]
def makePeak(arr):

    # First half of the array
    first = arr[:len(arr)//2 + 1]
    first.reverse()

    # Second half of the array
    second = arr[len(arr)//2:]

    # Merg both halves
    ans = makeDec(first)[::-1] + makeDec(second)[1:]

    # Function Call
    if isPeak(ans):
        return ans

    return -1

# Driver Code

# Given array
arr = [7, 3, 4, 5, 3]

# Function Call
print(makePeak(arr))
```

**Output:**

```
[1879048192, 3221225472, 4294967296, 2684354560, 1610612736]

```

***时间复杂度:** O(N * log(M))，其中 M 为*[*arr 的最大元素[]*](https://www.geeksforgeeks.org/c-program-find-largest-element-array/) *。*
***辅助空间:** O(1)*