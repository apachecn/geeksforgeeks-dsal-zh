# 在排序的二进制数组中计数 1 的 Javascript 程序

> 原文:[https://www . geeksforgeeks . org/JavaScript-程序到计数-一元排序-二进制-数组/](https://www.geeksforgeeks.org/javascript-program-to-count-1s-in-a-sorted-binary-array/)

给定一个按非递增顺序排序的二进制数组，计算其中 1 的个数。

**示例:**

```
Input: arr[] = {1, 1, 0, 0, 0, 0, 0}
Output: 2

Input: arr[] = {1, 1, 1, 1, 1, 1, 1}
Output: 7

Input: arr[] = {0, 0, 0, 0, 0, 0, 0}
Output: 0
```

一个简单的解决方案是线性遍历数组。简单解的时间复杂度为 O(n)。我们可以使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)找到以 O(Logn)为单位的时间计数。想法是使用二分搜索法查找 1 的最后一次出现。一旦我们找到索引的最后一次出现，我们返回索引+ 1 作为计数。
以下是上述想法的实现。

## java 描述语言

```
<script>

// Javascript program to count one's in a boolean array

/* Returns counts of 1's in arr[low..high].  The array is
   assumed to be sorted in non-increasing order */
function countOnes( arr, low, high)
{
  if (high >= low)
  {
    // get the middle index
    let mid = Math.trunc(low + (high - low)/2);

    // check if the element at middle index is last 1
    if ( (mid == high || arr[mid+1] == 0) && (arr[mid] == 1))
      return mid+1;

    // If element is not last 1, recur for right side
    if (arr[mid] == 1)
      return countOnes(arr, (mid + 1), high);

    // else recur for left side
    return countOnes(arr, low, (mid -1));
  }
  return 0;
}
    // Driver program 

   let arr = [ 1, 1, 1, 1, 0, 0, 0 ];
   let n = arr.length;
   document.write("Count of 1's in given array is " + 
                    countOnes(arr, 0, n-1));

</script>
```

**Output**

```
Count of 1's in given array is 4
```