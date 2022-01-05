# 通过用另一个数组中的元素替换字符串的 GCD 来对字符串数组进行排序

> 原文:[https://www . geesforgeks . org/sort-a-array-of-string-by-replacements-with-gcd-with-elements-from-other-array/](https://www.geeksforgeeks.org/sort-an-array-of-strings-by-replacements-with-their-gcd-with-elements-from-another-array/)

给定两个大小分别为 **N** 和 **M** 的[字符串](https://www.geeksforgeeks.org/python-strings/)**arr【】】**和**k【】**的[数组，任务是在将每个数组元素**arr【I】**替换为**arr【I】**和**的**](https://www.geeksforgeeks.org/introduction-to-arrays/) **[GCD](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 后[对数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)arr【】进行排序**

**注:**两个弦 **A** 和 **B** 的 [GCD](https://www.geeksforgeeks.org/program-to-find-greatest-common-divisor-gcd-of-n-strings/) 是最小的弦，当串联多次后，就等于 **A** 和 **B** 。如果不存在这样的字符串，返回一个[空字符串。](https://www.geeksforgeeks.org/python-empty-string-to-none-conversion/)

**示例:**

> **输入:** arr[] = { '极客'，' for '，'极客' }，k[] = { '极客'，' for' }
> **输出:** { ' '，' for '，'极客' }
> **解释:**
> arr[0] = GCD('极客'，' for') = ' '
> arr[1] = GCD('for '，' for') = 'for'
> arr[2] = GCD('极客'，'极客'
> 
> **输入:** arr[] = { 'aacd '，' abdc '，' acac '，' aaaa' }，k[] = {'aa '，' ac'}
> **输出:** -1

**进场:**给定的问题可以解决[贪婪的](https://www.geeksforgeeks.org/greedy-algorithms/)。按照以下步骤解决问题:

*   初始化一个变量，比如**prev =**([空字符串](https://www.geeksforgeeks.org/python-empty-string-to-none-conversion/)，以存储排序后的前一个字符串。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于范围**【0，N–1】**内的 **i**
    *   在**【0，M–1】**范围内，用**k【j】、**计算**arr【I】**的每一串 [GCD。](https://www.geeksforgeeks.org/program-to-find-greatest-common-divisor-gcd-of-n-strings/)
    *   找到最小的字符串说，**optere**[在字母顺序上大于](https://www.geeksforgeeks.org/compare-two-strings-lexicographically-in-java/) **prev**
    *   更新**arr[I]= Optere**
    *   更新 **prev = arr[i]**
*   如果[数组按升序排序](https://www.geeksforgeeks.org/program-check-array-sorted-not-iterative-recursive/)。[打印数组](https://www.geeksforgeeks.org/c-program-to-print-an-array-using-recursion/)
*   否则，打印 **-1。**

下面是实现。

## 蟒蛇 3

```
# Python implementation of the 
# above approach

# Function to find gcd of two numbers
def GCD(a, b):
    if(b == 0):
        return a
    else:
        return GCD(b, a % b)

# Function to find GCD of two strings 
def StringGCD(a, b):

    # Length of gcd of two strings
    gcd = GCD(len(a), len(b))

    if a[:gcd] == b[:gcd]:
        if a*(len(b)//gcd) == b*(len(a)//gcd):
            return a[:gcd]

    # GCD of strings does not exist
    return ' '

# Function to check if the array is
# sorted in increasing order or not
def isIncreasing(arr):

    for i in range(len(arr)-1):
        if arr[i] >= arr[i + 1]:
            return False

    return True

# Function to check if arr[] can
# be sorted in increasing order
def sortByGcd(arr, k):

      # Previous string
    prev = ''

    # Iterate through the array
    for i in range(len(arr)):

        # Initialize optimal
        # element by arr[i]
        optEle = arr[i]

        # Flag to find first
        # string > prev
        flag = True

        for idx in range(len(k)):

            # Gcd of two strings
            Ele = StringGCD(arr[i], k[idx])

            # If Ele > prev and flag is set
            if Ele > prev and flag:

                  # Update optEle
                optEle = Ele

                # Update Flag
                flag = False

            # If Ele > prev
            if Ele > prev:

                # Update optEle
                optEle = min(optEle, Ele)

        # Update arr[i] by optEle
        arr[i] = optEle

        # Update prev by arr[i]
        prev = arr[i]

    # Check is arr[] is sorted in ascending order
    if isIncreasing(arr):
        return arr

    # Sorted order is not possible
    else:
        return -1

# Driver Code

arr = ['geeks', 'for', 'geeks']
k = ['geeks', 'for']
print(sortByGcd(arr, k))
```

***时间复杂度:** O(N * K * log(min(N，K))*
***辅助空间:** O(1)*