# 逆排列

> 原文:[https://www.geeksforgeeks.org/inverse-permutation/](https://www.geeksforgeeks.org/inverse-permutation/)

给定一个大小为 n 的整数数组，范围从 1 到 n，我们需要找到该数组的逆排列。
**逆置换**是通过在数组中元素值指定的位置插入元素的位置而得到的置换。为了更好地理解，考虑下面的例子:
假设我们在一个数组中的位置 3 找到元素 4，然后在反向排列中，我们在位置 4(元素值)插入 3(元素 4 在数组中的位置)。
基本上，逆置换是一种置换，其中每个数和它所占据的位置的数被交换。
*数组应该包含从 1 到 array_size 的元素。*
**例 1 :**

```
Input  = {1, 4, 3, 2}
Output = {1, 4, 3, 2}
```

在这种情况下，对于元素 1，我们从 arr1 插入位置 1，即 arr2 中位置 1 的 1。对于 arr1 中的元素 4，我们在 arr2 的位置 4 插入 arr1 中的 2。类似地，对于 arr1 中的元素 2，我们在 arr2 中插入位置 2，即 4。

```
Example 2 :
Input  = {2, 3, 4, 5, 1}
Output = {5, 1, 2, 3, 4}
```

在这个例子中，对于元素 2，我们在 arr2 的位置 2 插入 arr1 的位置 2。同样，我们发现其他元素的逆排列。
考虑一个数组 arr，数组 arr 中有元素 1 到 n.
**方法 1 :**
在这个方法中，我们一个一个地取元素，按递增的顺序检查元素，并打印出找到那个元素的元素的位置。

## C++

```
// Naive CPP Program to find inverse permutation.
#include <bits/stdc++.h>
using namespace std;

// C++ function to find inverse permutations
void inversePermutation(int arr[], int size) {

  // Loop to select Elements one by one
  for (int i = 0; i < size; i++) {

    // Loop to print position of element
    // where we find an element
    for (int j = 0; j < size; j++) {

      // checking the element in increasing order
      if (arr[j] == i + 1) {

        // print position of element where
        // element is in inverse permutation
        cout << j + 1 << " ";
        break;
      }
    }
  }
}

// Driver program to test above function
int main() {
  int arr[] = {2, 3, 4, 5, 1};
  int size = sizeof(arr) / sizeof(arr[0]);
  inversePermutation(arr, size);
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Naive java Program to find inverse permutation.
import java.io.*;

class GFG {

    // java function to find inverse permutations
    static void inversePermutation(int arr[], int size)
    {
        int i ,j;
        // Loop to select Elements one by one
        for ( i = 0; i < size; i++)
        {

            // Loop to print position of element
            // where we find an element
            for ( j = 0; j < size; j++)
            {

                // checking the element in
                // increasing order
                if (arr[j] == i + 1)
                {
                    // print position of element
                    // where element is in inverse
                    // permutation
                    System.out.print( j + 1 + " ");
                    break;
                }
            }
        }
    }

    // Driver program to test above function

    public static void main (String[] args)
    {
        int arr[] = {2, 3, 4, 5, 1};
        int size = arr.length;
        inversePermutation(arr, size);

    }
}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# Naive Python3 Program to
# find inverse permutation.

# Function to find inverse permutations
def inversePermutation(arr, size):

    # Loop to select Elements one by one
    for i in range(0, size):

        # Loop to print position of element
        # where we find an element
        for j in range(0, size):

        # checking the element in increasing order
            if (arr[j] == i + 1):

                # print position of element where
                # element is in inverse permutation
                print(j + 1, end = " ")
                break

# Driver Code
arr = [2, 3, 4, 5, 1]
size = len(arr)

inversePermutation(arr, size)

#This code is contributed by Smitha Dinesh Semwal
```

## C#

```
// Naive C# Program to find inverse permutation.
using System;

class GFG {

    // java function to find inverse permutations
    static void inversePermutation(int []arr, int size)
    {
        int i ,j;
        // Loop to select Elements one by one
        for ( i = 0; i < size; i++)
        {

            // Loop to print position of element
            // where we find an element
            for ( j = 0; j < size; j++)
            {

                // checking the element in
                // increasing order
                if (arr[j] == i + 1)
                {
                    // print position of element
                    // where element is in inverse
                    // permutation
                    Console.Write( j + 1 + " ");
                    break;
                }
            }
        }
    }

    // Driver program to test above function

    public static void Main ()
    {
        int []arr = {2, 3, 4, 5, 1};
        int size = arr.Length;
        inversePermutation(arr, size);

    }
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Naive PHP Program to
// find inverse permutation.

// Function to find
// inverse permutations
function inversePermutation($arr, $size)
{
for ( $i = 0; $i < $size; $i++)
{

    // Loop to print position of element
    // where we find an element
    for ($j = 0; $j < $size; $j++)
    {

    // checking the element
    // in increasing order
    if ($arr[$j] == $i + 1)
    {

        // print position of element
        // where element is in
        // inverse permutation
        echo $j + 1 , " ";
        break;
    }
    }
}
}

// Driver Code
$arr = array(2, 3, 4, 5, 1);
$size = sizeof($arr);
inversePermutation($arr, $size);

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>

// Naive JavaScript program to find inverse permutation.

// JavaScript function to find inverse permutations
    function inversePermutation(arr, size)
    {
        let i ,j;

        // Loop to select Elements one by one
        for ( i = 0; i < size; i++)
        {

            // Loop to print position of element
            // where we find an element
            for ( j = 0; j < size; j++)
            {

                // checking the element in
                // increasing order
                if (arr[j] == i + 1)
                {
                    // print position of element
                    // where element is in inverse
                    // permutation
                    document.write( j + 1 + " ");
                    break;
                }
            }
        }
    }

// Driver code

        let arr = [2, 3, 4, 5, 1];
        let size = arr.length;
        inversePermutation(arr, size);

</script>
```

**输出:**

```
 5 1 2 3 4
```

**方法 2 :**
想法是使用另一个数组来存储索引和元素映射

## C++

```
// Efficient CPP Program to find inverse permutation.
#include <bits/stdc++.h>
using namespace std;

// C++ function to find inverse permutations
void inversePermutation(int arr[], int size) {

  // to store element to index mappings
  int arr2[size];

  // Inserting position at their
  // respective element in second array
  for (int i = 0; i < size; i++)
    arr2[arr[i] - 1] = i + 1;

  for (int i = 0; i < size; i++)
    cout << arr2[i] << " "; 
}

// Driver program to test above function
int main() {
  int arr[] = {2, 3, 4, 5, 1};
  int size = sizeof(arr) / sizeof(arr[0]);
  inversePermutation(arr, size);
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Efficient Java Program to find
// inverse permutation.
import java.io.*;

class GFG {

// function to find inverse permutations
static void inversePermutation(int arr[], int size) {

    // to store element to index mappings
    int arr2[] = new int[size];

    // Inserting position at their
    // respective element in second array
    for (int i = 0; i < size; i++)
    arr2[arr[i] - 1] = i + 1;

    for (int i = 0; i < size; i++)
    System.out.print(arr2[i] + " ");
}

// Driver program to test above function
public static void main(String args[]) {
    int arr[] = {2, 3, 4, 5, 1};
    int size = arr.length;
    inversePermutation(arr, size);
}
}

// This code is contributed by Nikita Tiwari.
```

## 蟒蛇 3

```
# Efficient Python 3 Program to find
# inverse permutation.

# function to find inverse permutations
def inversePermutation(arr, size) :

    # To store element to index mappings
    arr2 = [0] *(size)

    # Inserting position at their
    # respective element in second array
    for i in range(0, size) :
        arr2[arr[i] - 1] = i + 1

    for i in range(0, size) :
        print( arr2[i], end = " ")

# Driver program
arr = [2, 3, 4, 5, 1]
size = len(arr)

inversePermutation(arr, size)

# This code is contributed by Nikita Tiwari.
```

## C#

```
// Efficient C# Program to find
// inverse permutation.
using System;

class GFG {

// function to find inverse permutations
static void inversePermutation(int []arr, int size) {

    // to store element to index mappings
    int []arr2 = new int[size];

    // Inserting position at their
    // respective element in second array
    for (int i = 0; i < size; i++)
    arr2[arr[i] - 1] = i + 1;

    for (int i = 0; i < size; i++)
    Console.Write(arr2[i] + " ");
}

// Driver program to test above function
public static void Main() {
    int []arr = {2, 3, 4, 5, 1};
    int size = arr.Length;
    inversePermutation(arr, size);
}
}

// This code is contributed by vt_m.
```

```
Output : 5 1 2 3 4
```