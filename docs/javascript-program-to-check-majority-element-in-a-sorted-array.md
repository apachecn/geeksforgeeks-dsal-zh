# 检查排序数组中多数元素的 Javascript 程序

> 原文:[https://www . geesforgeks . org/JavaScript-程序检查-排序数组中的多数元素/](https://www.geeksforgeeks.org/javascript-program-to-check-majority-element-in-a-sorted-array/)

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

**输出:**

```
4 appears more than 3 times in arr[]
```

**时间复杂度:** O(n)

**方法 2(使用二分搜索法)**
使用二分搜索法方法找到给定数字的第一个出现。二分搜索法的标准在这里很重要。

## java 描述语言

```
<script>
    // Javascript Program to check for majority
    // element in a sorted array */

    // If x is present in arr[low...high]
    // then returns the index of first
    // occurrence of x, otherwise returns -1
    function _binarySearch(arr, low, high, x)
    {
        if (high >= low) {
            let mid = parseInt((low + high) / 2, 10);
            //low + (high - low)/2;

            // Check if arr[mid] is the first
            // occurrence of x.    arr[mid] is
            // first occurrence if x is one of
            // the following is true:
            // (i) mid == 0 and arr[mid] == x
            // (ii) arr[mid-1] < x and arr[mid] == x

            if ((mid == 0 || x > arr[mid - 1]) && (arr[mid] == x))
                return mid;
            else if (x > arr[mid])
                return _binarySearch(arr, (mid + 1), high, x);
            else
                return _binarySearch(arr, low, (mid - 1), x);
        }

        return -1;
    }

    // This function returns true if the x is
    // present more than n/2 times in arr[]
    // of size n
    function isMajority(arr, n, x)
    {

        // Find the index of first occurrence
        // of x in arr[]
        let i = _binarySearch(arr, 0, n - 1, x);

        // If element is not present at all,
        // return false
        if (i == -1)
            return false;

        // check if the element is present
        // more than n/2 times
        if (((i + parseInt(n / 2, 10)) <= (n - 1)) && arr[i + parseInt(n / 2, 10)] == x)
            return true;
        else
            return false;
    }

    let arr = [ 1, 2, 3, 3, 3, 3, 10 ];
    let n = arr.length;
    let x = 3;
    if (isMajority(arr, n, x) == true)
      document.write(x + " appears more than " + parseInt(n / 2, 10) + " times in arr[]");
    else
      document.write(x + " does not appear more than " + parseInt(n / 2, 10) + " times in arr[]");

</script>
```

**Output**

```
3 appears more than 3 times in arr[]
```

***时间复杂度** : O(1)*
***辅助空间:** O(1)*

更多细节请参考完整的文章[检查排序数组](https://www.geeksforgeeks.org/check-for-majority-element-in-a-sorted-array/)中的多数元素！