# 重新排列数组，使数组元素的反向二进制表示的十进制等价排序

> 原文:[https://www . geeksforgeeks . org/array-array-to-make-十进制等效物-数组元素的反向二进制表示-已排序/](https://www.geeksforgeeks.org/rearrange-array-to-make-decimal-equivalents-of-reversed-binary-representations-of-array-elements-sorted/)

给定一个由正整数 **N** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是重新排列数组，以便对所有数组元素的反向[二进制表示进行排序。](https://www.geeksforgeeks.org/binary-representation-of-a-given-number/)

> 如果两个或多个数组元素的反向二进制表示的十进制等价相等，则在重新排列数组时会考虑原始值。

**示例:**

> **输入:** arr[] = {43，52，61，41}
> **输出:** 52 41 61 43
> **解释:**
> 以下是数组元素的反向二进制表示:
> 
> 1.  43–>(101011)<sub>2</sub>–>反转–>53。
> 2.  52–>(110100)<sub>2</sub>–>反转–>11。
> 3.  61–>(111101)<sub>2</sub>–>反转–>47。
> 4.  41–>(101001)<sub>2</sub>–>反转–>37。
> 
> 因此，在将数组元素重新排列为{52，41，61，43}后，重新排列的数组元素的反向二进制表示按排序顺序排列。
> 
> **输入:** arr[] = {5，3，6，2，4}
> **输出:** 2 4 3 6 5

**方法:**按照以下步骤解决问题:

*   初始化一个数组，比如说**new warr[]**，插入所有数组元素作为数字的反向[二进制表示。](https://www.geeksforgeeks.org/binary-representation-of-a-given-number/)
*   [按递增顺序排列数组](https://www.geeksforgeeks.org/arrays-sort-in-java-with-examples/) **【纽瓦尔】**。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **【纽瓦尔】**并将所有元素复制到数组 **arr[]** 。
*   现在，将所有数组元素更新为数字的反向[二进制表示。](https://www.geeksforgeeks.org/binary-representation-of-a-given-number/)
*   完成以上步骤后，[打印数组 **arr[]**](https://www.geeksforgeeks.org/java-program-to-print-the-elements-of-an-array/) 的元素作为输出。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to reverse the bits of a number
int keyFunc(int n)
{

    // Stores the reversed number
    int rev = 0;

    while (n > 0)
    {

        // Divide rev by 2
        rev = rev << 1;

        // If the value of N is odd
        if (n & 1 == 1)
            rev = rev ^ 1;

        // Update the value of N
        n = n >> 1;
      }

    // Return the final value of rev
    return rev;
}

// Function for rearranging the array
// element according to the given rules
vector<vector<int>> getNew(vector<int> arr)
{

    // Stores the new array elements
    vector<vector<int>> ans;

    for (int i:arr)
        ans.push_back({keyFunc(i), i});

    return ans;
}

// Function for rearranging the array
vector<int> getArr(vector<vector<int> > arr){

    // Stores the new array
    vector<int> ans;

    for (auto i:arr)
        ans.push_back(i[1]);
    return ans;
}

// Function to sort the array by reversing
// binary representation
void sortArray(vector<int> arr)
{

  // Creating a new array
  vector<vector<int> > newArr = getNew(arr);

  // Sort the array with the key
  sort(newArr.begin(),newArr.end());

  // Get arr from newArr
  arr = getArr(newArr);

  // Print the sorted array
  int n = arr.size();
  cout<<"[";
  for(int i = 0; i < n - 1; i++)
    cout << arr[i] << ", ";
  cout << arr[n - 1] << "]";
}

// Driver Code
int main()
{

  vector<int> arr = {43, 52, 61, 41};
  sortArray(arr);

  return 0;
}

// This code is contributed by mohit kumar 29.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Function to reverse the bits of a number
static int keyFunc(int n)
{

    // Stores the reversed number
    int rev = 0;

    while (n > 0)
    {

        // Divide rev by 2
        rev = rev << 1;

        // If the value of N is odd
        if ((n & 1) == 1)
            rev = rev ^ 1;

        // Update the value of N
        n = n >> 1;
    }

    // Return the final value of rev
    return rev;
}

// Function for rearranging the array
// element according to the given rules
static int[][] getNew(int arr[])
{

    // Stores the new array elements
    int ans[][] = new int[arr.length][2];

    for(int i = 0; i < arr.length; i++)
        ans[i] = new int[]{ keyFunc(arr[i]), arr[i] };

    return ans;
}

// Function for rearranging the array
static int[] getArr(int[][] arr)
{

    // Stores the new array
    int ans[] = new int[arr.length];
    int idx = 0;
    for(int i[] : arr)
        ans[idx++] = i[1];

    return ans;
}

// Function to sort the array by reversing
// binary representation
static void sortArray(int arr[])
{

    // Creating a new array
    int[][] newArr = getNew(arr);

    // Sort the array with the key
    Arrays.sort(newArr, (a, b) -> {
        if (Integer.compare(a[0], b[0]) == 0)
            return Integer.compare(a[1], b[1]);

        return Integer.compare(a[0], b[0]);
    });

    // Get arr from newArr
    arr = getArr(newArr);

    // Print the sorted array
    int n = arr.length;
    System.out.print("[");
    for(int i = 0; i < n - 1; i++)
        System.out.print(arr[i] + ", ");

    System.out.print(arr[n - 1] + "]");
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 43, 52, 61, 41 };
    sortArray(arr);
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to reverse the bits of a number
def keyFunc(n):

    # Stores the reversed number
    rev = 0

    while (n > 0):

        # Divide rev by 2
        rev = rev << 1

        # If the value of N is odd
        if (n & 1 == 1):
            rev = rev ^ 1

        # Update the value of N
        n = n >> 1

    # Return the final value of rev
    return rev

# Function for rearranging the array
# element according to the given rules
def getNew(arr):

    # Stores the new array elements
    ans = []

    for i in arr:
        ans.append([keyFunc(i), i])
    return ans

# Function for rearranging the array
def getArr(arr):

    # Stores the new array
    ans = []

    for i in arr:
        ans.append(i[1])
    return ans

# Function to sort the array by reversing
# the binary representation
def sortArray(arr):

    # Creating a new array
    newArr = getNew(arr)

    # Sort the array with the key
    newArr.sort()

    # Get arr from newArr
    arr = getArr(newArr)

    # Print the sorted array
    print(arr)

# Driver Code

arr = [43, 52, 61, 41]
sortArray(arr)
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to reverse the bits of a number
function keyFunc(n) {

    // Stores the reversed number
    let rev = 0;

    while (n > 0) {

        // Divide rev by 2
        rev = rev << 1;

        // If the value of N is odd
        if (n & 1 == 1)
            rev = rev ^ 1;

        // Update the value of N
        n = n >> 1;
    }

    // Return the final value of rev
    return rev;
}

// Function for rearranging the array
// element according to the given rules
function getNew(arr) {

    // Stores the new array elements
    let ans = [];

    for (let i of arr)
        ans.push([keyFunc(i), i]);

    return ans;
}

// Function for rearranging the array
function getArr(arr) {

    // Stores the new array
    let ans = [];

    for (let i of arr)
        ans.push(i[1]);
    return ans;
}

// Function to sort the array by reversing
// binary representation
function sortArray(arr) {

    // Creating a new array
    let newArr = getNew(arr);

    // Sort the array with the key
    newArr.sort();

    // Get arr from newArr
    arr = getArr(newArr);

    // Print the sorted array
    let n = arr.length;
    document.write("[");
    for (let i = 0; i < n - 1; i++)
        document.write(arr[i] + ", ");
    document.write(arr[n - 1] + "]");
}

// Driver Code

let arr = [43, 52, 61, 41];
sortArray(arr);

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output:** 

```
[52, 41, 61, 43]
```

***时间复杂度:** O(N * log N)*
***辅助空间:** O(N)*

**空间优化方法:**按照以下步骤解决问题:

*   声明一个接受数组元素作为参数的函数，并返回其反向二进制表示的十进制等价形式。
*   [排序时使用函数作为键对数组进行排序。](https://www.geeksforgeeks.org/python-program-to-sort-a-list-of-tuples-by-second-item/)
*   [打印数组元素作为输出。](https://www.geeksforgeeks.org/print-lists-in-python-4-different-ways/)

下面是上述方法的实现:

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to reverse the bits of number
def keyFunc(n):

    # Stores the reversed number
    rev = 0

    while (n > 0):

        # Divide rev by 2
        rev = rev << 1

        # If the value of N is odd
        if (n & 1 == 1):
            rev = rev ^ 1

        # Update the value of N
        n = n >> 1

    # Return the final value of rev
    return rev

# Function to sort the array by reversing
# binary representation
def sortArray(arr):

    # Sort the array with the key
    arr = sorted(arr, key = keyFunc)

    # Print the sorted array
    print(arr)

# Driver Code

arr = [43, 52, 61, 41]
sortArray(arr)
```

**Output:** 

```
[52, 41, 61, 43]
```

***时间复杂度:** O(N * log N)*
***辅助空间:** O(1)*