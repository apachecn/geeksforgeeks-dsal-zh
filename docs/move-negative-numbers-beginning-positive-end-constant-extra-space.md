# 以恒定的额外空间将所有负数移动到开头，正数移动到结尾

> 原文:[https://www . geesforgeks . org/move-负数-开始-正数-结束-常量-额外空间/](https://www.geeksforgeeks.org/move-negative-numbers-beginning-positive-end-constant-extra-space/)

数组包含随机顺序的正数和负数。重新排列数组元素，使所有负数出现在所有正数之前。

**示例:**

```
Input: -12, 11, -13, -5, 6, -7, 5, -3, -6
Output: -12 -13 -5 -7 -3 -6 11 6 5
```

**注意:**这里元素的顺序不重要。

**方法 1:**
思路是简单套用 [](https://www.geeksforgeeks.org/quick-sort/) 快速排序的[分区过程。](https://www.geeksforgeeks.org/quick-sort/)

## C++

```
// A C++ program to put all negative
// numbers before positive numbers
#include <bits/stdc++.h>
using namespace std;

void rearrange(int arr[], int n)
{
    int j = 0;
    for (int i = 0; i < n; i++) {
        if (arr[i] < 0) {
            if (i != j)
                swap(arr[i], arr[j]);
            j++;
        }
    }
}

// A utility function to print an array
void printArray(int arr[], int n)
{
    for (int i = 0; i < n; i++)
        printf("%d ", arr[i]);
}

// Driver code
int main()
{
    int arr[] = { -1, 2, -3, 4, 5, 6, -7, 8, 9 };
    int n = sizeof(arr) / sizeof(arr[0]);
    rearrange(arr, n);
    printArray(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to put all negative
// numbers before positive numbers
import java.io.*;

class GFG {

    static void rearrange(int arr[], int n)
    {
        int j = 0, temp;
        for (int i = 0; i < n; i++) {
            if (arr[i] < 0) {
                if (i != j) {
                    temp = arr[i];
                    arr[i] = arr[j];
                    arr[j] = temp;
                }
                j++;
            }
        }
    }

    // A utility function to print an array
    static void printArray(int arr[], int n)
    {
        for (int i = 0; i < n; i++)
            System.out.print(arr[i] + " ");
    }

    // Driver code
    public static void main(String args[])
    {
        int arr[] = { -1, 2, -3, 4, 5, 6, -7, 8, 9 };
        int n = arr.length;

        rearrange(arr, n);
        printArray(arr, n);
    }
}

// This code is contributed by Nikita Tiwari.
```

## 蟒蛇 3

```
# A Python 3 program to put
# all negative numbers before
# positive numbers

def rearrange(arr, n ) :

    # Please refer partition() in
    # below post
    # https://www.geeksforgeeks.org / quick-sort / j = 0
    j = 0
    for i in range(0, n) :
        if (arr[i] < 0) :
            temp = arr[i]
            arr[i] = arr[j]
            arr[j]= temp
            j = j + 1
    print(arr)

# Driver code
arr = [-1, 2, -3, 4, 5, 6, -7, 8, 9]
n = len(arr)
rearrange(arr, n)

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to put all negative
// numbers before positive numbers
using System;

class GFG {
    static void rearrange(int[] arr, int n)
    {

        int j = 0, temp;
        for (int i = 0; i < n; i++) {
            if (arr[i] < 0) {
                temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
                j++;
            }
        }
    }

    // A utility function to print an array
    static void printArray(int[] arr, int n)
    {
        for (int i = 0; i < n; i++)
            Console.Write(arr[i] + " ");
    }

    // Driver code
    public static void Main()
    {
        int[] arr = { -1, 2, -3, 4, 5, 6, -7, 8, 9 };
        int n = arr.Length;

        rearrange(arr, n);
        printArray(arr, n);
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A PHP program to put all negative
// numbers before positive numbers

function rearrange(&$arr, $n)
{
    $j = 0;
    for ($i = 0; $i < $n; $i++)
    {
        if ($arr[$i] < 0)
        {
            if ($i != $j)
            {
                $temp = $arr[$i];
                $arr[$i] = $arr[$j];
                $arr[$j] = $temp;
            }
            $j++;
        }
    }
}

// A utility function to print an array
function printArray(&$arr, $n)
{
    for ($i = 0; $i < $n; $i++)
        echo $arr[$i]." ";
}

// Driver code
$arr = array(-1, 2, -3, 4, 5, 6, -7, 8, 9 );
$n = sizeof($arr);
rearrange($arr, $n);
printArray($arr, $n);

// This code is contributed by ChitraNayal
?>
```

## java 描述语言

```
<script>
// A JavaScript program to put all negative
// numbers before positive numbers

function rearrange(arr, n)
{
    let j = 0;
    for (let i = 0; i < n; i++) {
        if (arr[i] < 0) {
            if (i != j){
                let temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
            j++;
        }
    }
}

// A utility function to print an array
function printArray(arr, n)
{
    for (let i = 0; i < n; i++)
        document.write(arr[i] + " ");
}

// Driver code
    let arr = [ -1, 2, -3, 4, 5, 6, -7, 8, 9 ];
    let n = arr.length;
    rearrange(arr, n);
    printArray(arr, n);

// This code is contributed by Surbhi Tyagi.
</script>
```

**Output**

```
-1 -3 -7 4 5 6 2 8 9
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)

**双指针方法:**解决这个问题的思路是用恒定的空间和线性时间，通过使用[双指针](https://www.geeksforgeeks.org/two-pointers-technique/)或双变量方法，我们简单地取两个变量，如左和右，保存 0 和 N-1 索引。只需要检查一下:

1.  检查如果左指针和右指针元素为负，则简单地增加左指针。
2.  否则，如果左边的元素是正的，右边的元素是负的，那么简单地交换元素，同时增加和减少左右指针。
3.  否则，如果左边的元素是正的，右边的元素也是正的，那么简单地减少右边的指针。
4.  重复以上 3 步，直到左指针≤右指针。

下面是上述方法的实现:

## C++

```
// C++ program of the above
// approach

#include <iostream>
using namespace std;

// Function to shift all the
// negative elements on left side
void shiftall(int arr[], int left,
              int right)
{

  // Loop to iterate over the
  // array from left to the right
  while (left<=right)
  {
    // Condition to check if the left
    // and the right elements are
    // negative
    if (arr[left] < 0 && arr[right] < 0)
      left+=1;

    // Condition to check if the left
    // pointer element is positive and
    // the right pointer element is negative
    else if (arr[left]>0 && arr[right]<0)
    {
      int temp=arr[left];
      arr[left]=arr[right];
      arr[right]=temp;
      left+=1;
      right-=1;
    }

    // Condition to check if both the
    // elements are positive
    else if (arr[left]>0 && arr[right] >0)
      right-=1;
    else{
      left += 1;
      right -= 1;
    }
  }
}

// Function to print the array
void display(int arr[], int right){

  // Loop to iterate over the element
  // of the given array
  for (int i=0;i<=right;++i){
    cout<<arr[i]<<" ";
  }
  cout<<endl;
}

// Driver Code
int main()
{
  int arr[] = {-12, 11, -13, -5,
               6, -7, 5, -3, 11};
  int arr_size = sizeof(arr) /
                sizeof(arr[0]);

  // Function Call
  shiftall(arr,0,arr_size-1);
  display(arr,arr_size-1);
  return 0;
}

//added by Dhruv Goyal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the above
// approach
import java.io.*;

class GFG{

// Function to shift all the
// negative elements on left side
static void shiftall(int[] arr, int left,
                     int right)
{

    // Loop to iterate over the
    // array from left to the right
    while (left <= right)
    {

        // Condition to check if the left
        // and the right elements are
        // negative
        if (arr[left] < 0 && arr[right] < 0)
            left++;

        // Condition to check if the left
        // pointer element is positive and
        // the right pointer element is negative
        else if (arr[left] > 0 && arr[right] < 0)
        {
            int temp = arr[left];
            arr[left] = arr[right];
            arr[right] = temp;
            left++;
            right--;
        }

        // Condition to check if both the
        // elements are positive
        else if (arr[left] > 0 && arr[right] > 0)
            right--;
        else
        {
            left++;
            right--;
        }
    }
}

// Function to print the array
static void display(int[] arr, int right)
{

    // Loop to iterate over the element
    // of the given array
    for(int i = 0; i <= right; ++i)
        System.out.print(arr[i] + " ");

    System.out.println();
}

// Drive code
public static void main(String[] args)
{
    int[] arr = { -12, 11, -13, -5,
                   6, -7, 5, -3, 11 };

    int arr_size = arr.length;

    // Function Call
    shiftall(arr, 0, arr_size - 1);
    display(arr, arr_size - 1);
}
}

// This code is contributed by dhruvgoyal267
```

## 蟒蛇 3

```
# Python3 program of the
# above approach

# Function to shift all the
# the negative elements to
# the left of the array
def shiftall(arr,left,right):

  # Loop to iterate while the
  # left pointer is less than
  # the right pointer
  while left<=right:

    # Condition to check if the left
    # and right pointer negative
    if arr[left] < 0 and arr[right] < 0:
      left+=1

    # Condition to check if the left
    # pointer element is positive and
    # the right pointer element is
    # negative
    elif arr[left]>0 and arr[right]<0:
      arr[left], arr[right] = \
              arr[right],arr[left]
      left+=1
      right-=1

    # Condition to check if the left
    # pointer is positive and right
    # pointer as well
    elif arr[left]>0 and arr[right]>0:
      right-=1
    else:
      left+=1
      right-=1

# Function to print the array
def display(arr):
  for i in range(len(arr)):
    print(arr[i], end=" ")
  print()

# Driver Code
if __name__ == "__main__":
  arr=[-12, 11, -13, -5, \
       6, -7, 5, -3, 11]
  n=len(arr)
  shiftall(arr,0,n-1)
  display(arr)

# Sumit Singh
```

## C#

```
// C# program of the above
// approach
using System.IO;
using System;
class GFG
{
    // Function to shift all the
    // negative elements on left side
    static void shiftall(int[] arr, int left,int right)
    {

        // Loop to iterate over the
        // array from left to the right
        while (left <= right)
        {

            // Condition to check if the left
            // and the right elements are
            // negative
            if (arr[left] < 0 && arr[right] < 0)
                left++;

            // Condition to check if the left
            // pointer element is positive and
            // the right pointer element is negative
            else if (arr[left] > 0 && arr[right] < 0)
            {
                int temp = arr[left];
                arr[left] = arr[right];
                arr[right] = temp;
                left++;
                right--;
            }

            // Condition to check if both the
            // elements are positive
            else if (arr[left] > 0 && arr[right] > 0)
                right--;
            else
            {
                left++;
                right--;
            }
        }
    }

    // Function to print the array
    static void display(int[] arr, int right)
    {

        // Loop to iterate over the element
        // of the given array
        for(int i = 0; i <= right; ++i)
        {
            Console.Write(arr[i] + " ");

        }
        Console.WriteLine();
    }

    // Drive code                  
    static void Main()
    {
        int[] arr = {-12, 11, -13, -5, 6, -7, 5, -3, 11};
        int arr_size = arr.Length;
        shiftall(arr, 0, arr_size - 1);
        display(arr, arr_size - 1);
    }
}

// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>

// Javascript program of the above
// approach

// Function to shift all the
// negative elements on left side
function shiftall(arr, left, right)
{

    // Loop to iterate over the
    // array from left to the right
    while (left <= right)
    {

        // Condition to check if the left
        // and the right elements are
        // negative
        if (arr[left] < 0 && arr[right] < 0)
            left += 1;

        // Condition to check if the left
        // pointer element is positive and
        // the right pointer element is negative
        else if(arr[left] > 0 && arr[right] < 0)
        {
            let temp = arr[left];
            arr[left] = arr[right];
            arr[right] = temp;
            left += 1;
            right -= 1;
        }

        // Condition to check if both the
        // elements are positive
        else if (arr[left] > 0 && arr[right] > 0)
            right -= 1;
        else
        {
            left += 1;
            right -= 1;
        }
    }
}

// Function to print the array
function display(arr, right)
{

    // Loop to iterate over the element
    // of the given array
    for(let i = 0; i < right; i++)
        document.write(arr[i] + " ");
}

// Driver Code
let arr = [ -12, 11, -13, -5,
             6, -7, 5, -3, 11 ];
let arr_size = arr.length;

// Function Call
shiftall(arr, 0, arr_size - 1);
display(arr, arr_size);

// This code is contributed by annianni

</script>
```

**Output**

```
-12 -3 -13 -5 -7 6 5 11 11
```

这是一种就地重排算法，用于排列不保持元素顺序的正数和负数。

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

如果我们需要保持元素的顺序，这个问题就变得困难了。详见[用不变的额外空间](https://www.geeksforgeeks.org/rearrange-positive-and-negative-numbers/)重新排列正负数。

本文由 **Apoorva** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客网的主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。