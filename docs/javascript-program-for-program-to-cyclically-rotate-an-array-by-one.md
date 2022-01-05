# Javascript 程序，用于循环旋转一个数组

> 原文:[https://www . geesforgeks . org/JavaScript-逐个程序地循环旋转一个数组/](https://www.geeksforgeeks.org/javascript-program-for-program-to-cyclically-rotate-an-array-by-one/)

给定一个数组，将该数组顺时针旋转 1。

**示例:**

```
Input:  arr[] = {1, 2, 3, 4, 5}
Output: arr[] = {5, 1, 2, 3, 4}
```

以下是步骤。
1)将最后一个元素存储在一个变量中，比如 x。
2)将所有元素向前移动一个位置。
3)将数组的第一个元素替换为 x。

## java 描述语言

```
<script>

// JavaScript code for program 
// to cyclically rotate
// an array by one
function rotate(arr, n)
{
  var x = arr[n-1], i;
  for(i = n-1; i > 0; i--)
      arr[i] = arr[i-1];
  arr[0] = x;    
}

var arr = [1, 2, 3, 4, 5];
var n = arr.length;

document.write("Given array is <br>");
for(var i = 0; i< n; i++)
    document.write(arr[i] + " ");

rotate(arr, n);

document.write("<br>Rotated array is <br>");
for(var i = 0; i < n; i++)
    document.write(arr[i] + " ");

</script>
```

**Output**

```
Given array is 
1 2 3 4 5 

Rotated array is
5 1 2 3 4 
```