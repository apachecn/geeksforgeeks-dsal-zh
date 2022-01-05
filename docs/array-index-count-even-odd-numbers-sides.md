# 两边偶数或奇数计数相同的数组索引

> 原文:[https://www . geesforgeks . org/array-index-count-偶数-奇数-sides/](https://www.geeksforgeeks.org/array-index-count-even-odd-numbers-sides/)

给定一个 N 个整数的数组。我们需要找到一个索引，使得它左边偶数的频率等于它右边偶数的频率，或者它左边奇数的频率等于它右边奇数的频率。如果数组中不存在这样的索引，打印-1 否则打印所需的索引。注意-(如果存在多个索引，则返回第一个索引)

**示例:**

```
Input : arr[] = {4, 3, 2, 1, 2, 4}  
Output : index = 2
Explanation: At index 2, there is one
odd number on its left and one odd on
its right.

Input :arr[] = { 1, 2, 4, 5, 8, 3, 12}
Output : index = 3 
```

**方法一:(简易进场)**
跑两个圈。对于每一个元素，计算其左右两边的偶数和奇数。

## C++

```
// CPP program to find an index which has
// same number of even elements on left and
// right, Or same number of odd elements on
// left and right.
#include <iostream>
using namespace std;

// Function to find index
int findIndex(int arr[], int n) {

  for (int i = 0; i < n; i++) {
    int odd_left = 0, even_left = 0;
    int odd_right = 0, even_right = 0;

    // To count Even and Odd numbers of left side
    for (int j = 0; j < i; j++) {
      if (arr[j] % 2 == 0)
        even_left++;
      else
        odd_left++;
    }

    // To count Even and Odd numbers of right side
    for (int k = n - 1; k > i; k--) {
      if (arr[k] % 2 == 0)
        even_right++;
      else
        odd_right++;
    }

    // To check Even Or Odd of Both sides are equal or not
    if (even_right == even_left || odd_right == odd_left)
      return i;
  }

  return -1;
}

// Driver's Function
int main() {
  int arr[] = {4, 3, 2, 1, 2};
  int n = sizeof(arr) / sizeof(arr[0]);
  int index = findIndex(arr, n);

  ((index == -1) ? cout << "-1" :
          cout << "index = " << index);
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find
// an index which has
// same number of even
// elements on left and
// right, Or same number
// of odd elements on
// left and right.

class GFG{

// Function to find index
static int findIndex(int arr[], int n) {

for (int i = 0; i < n; i++) {

    int odd_left = 0, even_left = 0;
    int odd_right = 0, even_right = 0;

    // To count Even and Odd
        // numbers of left side
    for (int j = 0; j < i; j++) {
    if (arr[j] % 2 == 0)
        even_left++;
    else
        odd_left++;
    }

    // To count Even and Odd
        // numbers of right side
    for (int k = n - 1; k > i; k--) {
    if (arr[k] % 2 == 0)
        even_right++;
    else
        odd_right++;
    }

    // To check Even Or Odd of Both
        // sides are equal or not
    if (even_right == even_left || odd_right == odd_left)
    return i;
}

return -1;

}

// Driver's Function
public static void main(String[] args) {

int arr[] = {4, 3, 2, 1, 2};
int n = arr.length;
int index = findIndex(arr, n);

if (index == -1)
    System.out.println("-1");
else{
    System.out.print("index = ");
    System.out.print(index);
}
}
}

// This code is contributed by
// Smitha Dinesh Semwal
```

## 蟒蛇 3

```
'''Python program to find
   an index which has
   same number of even
   elements on left and
   right, Or same number
   of odd elements on
   left and right.'''

# Function to find index
def findIndex(arr,n):

    for i in range(n):

        odd_left = 0
        even_left = 0
        odd_right = 0
        even_right = 0

        # To count Even and Odd
        # numbers of left side
        for j in range(i):
            if (arr[j] % 2 == 0):
                even_left=even_left+1
            else:
                odd_left=odd_left+1

        # To count Even and Odd
        # numbers of right side
        for k in range(n - 1, i, -1):
            if (arr[k] % 2 == 0):
                even_right=even_right+1
            else:
                odd_right=odd_right+1

        # To check Even Or Odd of Both
        # sides are equal or not
        if (even_right == even_left and odd_right == odd_left):
            return i

    return -1

# Driver's Function

arr = [4, 3, 2, 1, 2]
n = len(arr)
index = findIndex(arr, n)

if (index == -1):
    print("-1")
else:
    print("index = ", index)

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to find an index which has
// same number of even elements on left
// and right, Or same number of odd
// elements on left and right.
using System;

class GFG{

    // Function to find index
    static int findIndex(int []arr, int n) {

        for (int i = 0; i < n; i++) {

            int odd_left = 0, even_left = 0;
            int odd_right = 0, even_right = 0;

            // To count Even and Odd
            // numbers of left side
            for (int j = 0; j < i; j++) {
                if (arr[j] % 2 == 0)
                    even_left++;
                else
                    odd_left++;
            }

            // To count Even and Odd
            // numbers of right side
            for (int k = n - 1; k > i; k--) {
                if (arr[k] % 2 == 0)
                    even_right++;
                else
                    odd_right++;
            }

            // To check Even Or Odd of Both
            // sides are equal or not
            if (even_right == even_left ||
                        odd_right == odd_left)
                return i;
        }

        return -1;
    }

    // Driver's Function
    public static void Main() {

        int []arr = {4, 3, 2, 1, 2};
        int n = arr.Length;

        int index = findIndex(arr, n);

        if (index == -1)
            Console.Write("-1");
        else{
            Console.Write("index = ");
            Console.Write(index);
        }
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find an index which has
// same number of even elements on left and
// right, Or same number of odd elements on
// left and right.

// Function to find index
function findIndex($arr, $n)
{

    for ($i = 0; $i < $n; $i++)
    {
        $odd_left = 0;
        $even_left = 0;
        $odd_right = 0;
        $even_right = 0;

        // To count Even and Odd
        // numbers of left side
        for ($j = 0; $j < $i; $j++)
        {
            if ($arr[$j] % 2 == 0)
                $even_left++;
            else
                $odd_left++;
        }

            // To count Even and Odd
            // numbers of right side
            for ($k = $n - 1; $k > $i; $k--)
            {
                if ($arr[$k] % 2 == 0)
                    $even_right++;
                else
                    $odd_right++;
            }

        // To check Even Or Odd of
        // Both sides are equal or not
        if ($even_right == $even_left ||
                $odd_right == $odd_left)
        return $i;
    }

    return -1;
}

// Drivers Code
{
    $arr = array(4, 3, 2, 1, 2);
    $n = sizeof($arr) / sizeof($arr[0]);
    $index = findIndex($arr, $n);

    if($index == -1)
    echo "-1";
    else
    echo ("index = $index" );
    return 0;
}

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// Javascript program to find an index which has
// same number of even elements on left and
// right, Or same number of odd elements on
// left and right.

// Function to find index
function findIndex(arr, n) {

for (let i = 0; i < n; i++) {
    let odd_left = 0, even_left = 0;
    let odd_right = 0, even_right = 0;

    // To count Even and Odd numbers of left side
    for (let j = 0; j < i; j++) {
    if (arr[j] % 2 == 0)
        even_left++;
    else
        odd_left++;
    }

    // To count Even and Odd numbers of right side
    for (let k = n - 1; k > i; k--) {
    if (arr[k] % 2 == 0)
        even_right++;
    else
        odd_right++;
    }

    // To check Even Or Odd of Both sides are equal or not
    if (even_right == even_left || odd_right == odd_left)
    return i;
}

return -1;
}

// Driver's Function

let arr = [4, 3, 2, 1, 2];
let n = arr.length;
let index = findIndex(arr, n);

if (index == -1)
            document.write("-1");
        else{
            document.write("index = ");
            document.write(index);
        }

//This code is contributed by Mayank Tyagi
</script>
```

**Output:** 

```
index = 2
```