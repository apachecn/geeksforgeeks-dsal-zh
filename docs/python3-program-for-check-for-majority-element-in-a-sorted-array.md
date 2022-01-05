# 检查排序数组中多数元素的 Python3 程序

> 原文:[https://www . geesforgeks . org/python 3-排序数组中多数元素的检查程序/](https://www.geeksforgeeks.org/python3-program-for-check-for-majority-element-in-a-sorted-array/)

**问题:**写一个函数，找出给定的整数 x 在 n 个整数的排序数组中出现的次数是否超过 n/2 次。
基本上，我们需要编写一个函数，比如 isMajority()，该函数以数组(arr[])、数组大小(n)和要搜索的数字(x)为参数，如果 x 是[多数元素](https://www.geeksforgeeks.org/majority-element/)(出现次数超过 n/2 次)，则返回 true。

**示例:**

```
Input: arr[] = {1, 2, 3, 3, 3, 3, 10}, x = 3
Output: True (x appears more than n/2 times in the given array)

Input: arr[] = {1, 1, 2, 4, 4, 4, 6, 6}, x = 4
Output: False (x doesn't appear more than n/2 times in the given array)

Input: arr[] = {1, 1, 1, 2, 2}, x = 1
Output: True (x appears more than n/2 times in the given array)
```

**方法 1(使用线性搜索)**
线性搜索元素的第一次出现，一旦找到它(让在索引 I 处)，检查索引 i + n/2 处的元素。如果 i+n/2 处存在元素，则返回 1，否则返回 0。

## 蟒蛇 3

```
'''Python3 Program to check for majority element in a sorted array'''

def isMajority(arr, n, x):
    # get last index according to n (even or odd) */
    last_index = (n//2 + 1) if n % 2 == 0 else (n//2)

    # search for first occurrence of x in arr[]*/
    for i in range(last_index):
        # check if x is present and is present more than n / 2 times */
        if arr[i] == x and arr[i + n//2] == x:
            return 1

# Driver program to check above function */
arr = [1, 2, 3, 4, 4, 4, 4]
n = len(arr)
x = 4
if (isMajority(arr, n, x)):
    print ("% d appears more than % d times in arr[]"
                                            %(x, n//2))
else:
    print ("% d does not appear more than % d times in arr[]"
                                                    %(x, n//2))

# This code is contributed by shreyanshi_arun.
```

**输出:**

```
4 appears more than 3 times in arr[]
```

**时间复杂度:** O(n)

**方法 2(使用二分搜索法)**
使用二分搜索法方法找到给定数字的第一个出现。二分搜索法的标准在这里很重要。

## 蟒蛇 3

```
'''Python3 Program to check for majority element in a sorted array'''

# This function returns true if the x is present more than n / 2
# times in arr[] of size n */
def isMajority(arr, n, x):

    # Find the index of first occurrence of x in arr[] */
    i = _binarySearch(arr, 0, n-1, x)

    # If element is not present at all, return false*/
    if i == -1:
        return False

    # check if the element is present more than n / 2 times */
    if ((i + n//2) <= (n -1)) and arr[i + n//2] == x:
        return True
    else:
        return False

# If x is present in arr[low...high] then returns the index of
# first occurrence of x, otherwise returns -1 */
def _binarySearch(arr, low, high, x):
    if high >= low:
        mid = (low + high)//2 # low + (high - low)//2;

        ''' Check if arr[mid] is the first occurrence of x.
            arr[mid] is first occurrence if x is one of the following
            is true:
            (i) mid == 0 and arr[mid] == x
            (ii) arr[mid-1] < x and arr[mid] == x'''

        if (mid == 0 or x > arr[mid-1]) and (arr[mid] == x):
            return mid
        elif x > arr[mid]:
            return _binarySearch(arr, (mid + 1), high, x)
        else:
            return _binarySearch(arr, low, (mid -1), x)
    return -1

# Driver program to check above functions */
arr = [1, 2, 3, 3, 3, 3, 10]
n = len(arr)
x = 3
if (isMajority(arr, n, x)):
    print ("% d appears more than % d times in arr[]"
                                            % (x, n//2))
else:
    print ("% d does not appear more than % d times in arr[]"
                                                    % (x, n//2))

# This code is contributed by shreyanshi_arun.
```

**输出:**

```
3 appears more than 3 times in arr[]
```

**时间复杂度:** O(Logn)
**算法范式:**分而治之

**方法 3:** 如果已经给定数组已排序并且存在多数元素，那么检查某个特定元素是否像检查数组的中间元素是否是我们要检查的数字一样简单。

由于多数元素在数组中出现的次数超过 n/2 次，因此它将始终是中间元素。我们可以使用这个逻辑来检查给定的数字是否是多数元素。

## 蟒蛇 3

```
def isMajorityElement(arr, 
                      n, key):

   if (arr[n // 2] == key):
        return True

   return False

# Driver code 
if __name__ == "__main__":

    arr = [1, 2, 3, 3,
           3, 3, 10]
    n = len(arr)
    x = 3

    if (isMajorityElement(arr, n, x)):
        print(x, " appears more than ", 
              n // 2 , " times in arr[]")
    else:
        print(x, " does not appear more than", 
              n // 2, " times in arr[]")

# This code is contributed by Chitranayal
```

**Output**

```
3 appears more than 3 times in arr[]
```

***时间复杂度** : O(1)*
***辅助空间:** O(1)*

更多细节请参考完整的文章[检查排序数组](https://www.geeksforgeeks.org/check-for-majority-element-in-a-sorted-array/)中的多数元素！