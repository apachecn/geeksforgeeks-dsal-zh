# 使用内置排序功能重新排列正数和负数

> 原文： [https://www.geeksforgeeks.org/rearrange-positive-negative-numbers-using-inbuilt-sort-function/](https://www.geeksforgeeks.org/rearrange-positive-negative-numbers-using-inbuilt-sort-function/)

给定正负数数组，请排列它们，使所有负整数出现在数组中所有正整数之前，而无需使用任何其他数据结构（例如哈希表，数组等）。应保持外观的顺序。

**示例**：

```
Input :  arr[] = [12, 11, -13, -5, 6, -7, 5, -3, -6]
Output : arr[] = [-13, -5, -7, -3, -6, 12, 11, 6, 5]

Input :  arr[] = [-12, 11, 0, -5, 6, -7, 5, -3, -6]
Output : arr[] =  [-12, -5, -7, -3, -6, 0, 11, 6, 5]

```



以前的方法：在中已经讨论了一些方法。 它们充其量已实现。

**方法 3**：还有另一种方法。 在 C++  STL 中，有一个内置函数[`std::sort()`](https://www.geeksforgeeks.org/sort-c-stl/)。 我们可以修改`comp()`函数以获得所需的结果。 因为我们必须先放置负数，然后再放置正数。 我们还必须在正数和负数之间保持零（如果存在）。

此代码中的`comp()`函数以所需顺序重新排列给定的数组。 在`bool comp(int a, int b)`中，如果`arr[]`中的整数`'a'`具有第`j`个索引，整数`'b'`具有第`i`个索引元素，则`j  > i`。 `comp()`函数将以这种方式调用。 如果`comp()`返回`true`，则将完成交换。

```

// CPP program to rearrange positive  
// and negative integers keeping  
// order of elements. 
#include <bits/stdc++.h> 

using namespace std; 

bool comp(int a, int b) 
{ 

// swap not needed 
if((a > 0 && b > 0) ||  
   (a < 0 && b < 0) ||  
   (a > 0 && b < 0 )) 
return false; 

// swap needed 
if(a < 0 && b > 0)  
return true; 

// swap not needed 
if((a == 0 && b < 0) ||  
   (a > 0 && b == 0)) 
return false; 

// swap needed 
if((a == 0 && b > 0) ||  
   (a < 0 && b == 0)) 
return true; 

} 

void rearrange(int arr[], int n) 
{ 
    sort(arr, arr + n, comp); 
} 

// Driver code 
int main() 
{ 
    int arr[] = { -12, 11, -13, -5,  
                  6, -7, 5, -3, -6 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    rearrange(arr, n); 
    for (int i = 0; i < n; i++) 
        cout << " " << arr[i]; 

    return 0; 
} 

```

**输出**：

```
-12 -13 -5 -7 -3 -6 11 6 5

```

**输出**：

```
 -12 -13 -5 -7 -3 -6 11 6 5

```

**时间复杂度**与排序即`O(n log n)`相同。 由于我们使用的是标准排序功能。 但这确实更快，因为内置排序功能使用[内省排序](https://www.geeksforgeeks.org/c-qsort-vs-c-sort/)。

**方法 4**：还有另一种方法可以解决此问题。 我们递归遍历数组，将其切成两半（`array[start..start]`和`array[(start + 1).. end]`，然后继续拆分数组，直到到达最后一个元素，然后开始将其合并回去，其想法是在任何时候使数组保持正负整数的正确顺序，合并逻辑为：

1.  如果`arr[start]`为负数，则按原样合并其余数组，以保持负数的顺序。 这样做的原因是，由于我们要从递归调用中追溯，因此我们开始在数组中从右向左移动，从而自然地保持了原始序列。

2.  如果`arr[start]`为正，则合并数组的其余部分，但是右旋数组的一半`[(start + 1) .. end]`。 旋转的想法是合并数组，以便使正`array[start]`始终与正元素合并。 但是，这里唯一的事情是合并后的数组将在左侧具有所有正元素，在右侧具有负元素。 因此，我们在每次递归中都颠倒了顺序，以得到负元素的原始序列，然后再得到正元素。

可以观察到，因为我们在每次递归中与正的第一个元素合并的同时反转了数组，所以正元素的顺序虽然排在负元素之后，但顺序相反。 因此，作为最后一步，我们只反转最终数组的正半部分，然后得到预期的序列。

下面是上述方法的实现：

## CPP

```

// C++ implementation of the above approach 
#include <iostream> 

void printArray(int array[], int length) 
{ 
    std::cout << "["; 

    for(int i = 0; i < length; i++) 
    { 
        std::cout << array[i]; 

        if(i < (length - 1)) 
            std::cout << ", "; 
        else
            std::cout << "]" << std::endl; 
    } 
} 

void reverse(int array[], int start, int end) 
{ 
    while(start < end) 
    { 
        int temp = array[start]; 
        array[start] = array[end]; 
        array[end] = temp; 
        start++; 
        end--; 
    } 
} 

// Rearrange the array with all negative integers 
// on left and positive integers on right  
// use recursion to split the array with first element 
// as one half and the rest array as another and then  
// merge it with head of the array in each step   
void rearrange(int array[], int start, int end) 
{ 
    // exit condition  
    if(start == end) 
        return; 

    // rearrange the array except the first 
    // element in each recursive call  
    rearrange(array, (start + 1), end); 

    // If the first element of the array is positive,  
    // then right-rotate the array by one place first 
    // and then reverse the merged array. 
    if(array[start] >= 0) 
    { 
        reverse(array, (start + 1), end); 
        reverse(array, start, end); 
    } 
} 

// Driver code 
int main() 
{ 
    int array[] = {-12, -11, -13, -5, -6, 7, 5, 3, 6}; 
    int length = (sizeof(array) / sizeof(array[0])); 
    int countNegative = 0; 

    for(int i = 0; i < length; i++) 
    { 
        if(array[i] < 0) 
            countNegative++; 
    } 

    std::cout << "array: "; 
    printArray(array, length); 
    rearrange(array, 0, (length - 1)); 

    reverse(array, countNegative, (length - 1)); 

    std::cout << "rearranged array: "; 
    printArray(array, length); 
    return 0; 
} 

```

输出：

```
-12 -13 -5 -7 -3 -6 11 6 5
```

时间复杂度与排序相同，即`O(n log n)`。由于我们使用的是标准排序功能。但这确实更快，因为内置排序功能使用了内省排序。

方法 4：还有另一种方法可以解决此问题。我们以递归方式遍历数组，将其切成两半`array[0 .. start]`和`array[start + 1 .. end]`，然后继续拆分数组，直到到达最后一个元素。然后开始合并它这个想法是在任何时候使数组保持负整数和正整数的适当顺序，合并逻辑将是：

1.  如果`array[start]`为负数，则按原样合并其余数组，以保持负数的顺序。这样做的原因是，由于我们要从递归调用中追溯，因此我们开始在数组中从右向左移动，从而自然地保持了原始序列。
2.  如果`array[start]`为正，则合并数组的其余部分，但是在右旋转`array[start + 1 .. end]`的一半后。旋转的想法是合并数组，以使正`array[start]`始终与正元素合并。但是，这里唯一的事情是合并后的数组将在左侧具有所有正元素，在右侧具有负元素。因此，我们在每次递归中都颠倒了顺序，以得到负元素的原始序列，然后再得到正元素。

可以观察到，因为在每次递归中与正的第一个元素合并时我们都对数组进行了反转，所以正元素的顺序虽然排在负元素之后，但顺序却相反。因此，作为最后一步，我们只反转最终数组的正半部分，然后得到预期的序列。

下面是上述方法的实现：

## C++

```cpp
// C++ implementation of 
// the above approach
#include <iostream>
 
void printArray(int array[], int length)
{
    std::cout << "[";
     
    for(int i = 0; i < length; i++)
    {
        std::cout << array[i];
         
        if(i < (length - 1))
            std::cout << ", ";
        else
            std::cout << "]" << std::endl;
    }
}
 
void reverse(int array[], int start, int end)
{
    while(start < end)
    {
        int temp = array[start];
        array[start] = array[end];
        array[end] = temp;
        start++;
        end--;
    }
}
 
// Rearrange the array with all negative integers
// on left and positive integers on right 
// use recursion to split the array with first element
// as one half and the rest array as another and then 
// merge it with head of the array in each step  
void rearrange(int array[], int start, int end)
{
    // exit condition 
    if(start == end)
        return;
     
    // rearrange the array except the first
    // element in each recursive call 
    rearrange(array, (start + 1), end);
     
    // If the first element of the array is positive, 
    // then right-rotate the array by one place first
    // and then reverse the merged array.
    if(array[start] >= 0)
    {
        reverse(array, (start + 1), end);
        reverse(array, start, end);
    }
}
 
// Driver code
int main()
{
    int array[] = {-12, -11, -13, -5, -6, 7, 5, 3, 6};
    int length = (sizeof(array) / sizeof(array[0]));
    int countNegative = 0;
     
    for(int i = 0; i < length; i++)
    {
        if(array[i] < 0)
            countNegative++;
    }
     
    std::cout << "array: ";
    printArray(array, length);
    rearrange(array, 0, (length - 1));
     
    reverse(array, countNegative, (length - 1));
     
    std::cout << "rearranged array: ";
    printArray(array, length);
    return 0;
}
```

## Python3

```py
# Python3 implementation of the above approach
def printArray(array, length):
    print("[", end = "")
 
    for i in range(length):
        print(array[i], end = "")
 
        if(i < (length - 1)):
            print(",", end = " ")
        else:
            print("]")
 
def reverse(array, start, end):
    while(start < end):
        temp = array[start]
        array[start] = array[end]
        array[end] = temp
        start += 1
        end -= 1
 
# Rearrange the array with all negative integers
# on left and positive integers on right
# use recursion to split the array with first element
# as one half and the rest array as another and then
# merge it with head of the array in each step
def rearrange(array, start, end):
     
    # exit condition
    if(start == end):
        return
 
    # rearrange the array except the first
    # element in each recursive call
    rearrange(array, (start + 1), end)
 
    # If the first element of the array is positive,
    # then right-rotate the array by one place first
    # and then reverse the merged array.
    if(array[start] >= 0):
        reverse(array, (start + 1), end)
        reverse(array, start, end)
 
# Driver code
if __name__ == '__main__':
    array = [-12, -11, -13, -5, -6, 7, 5, 3, 6]
    length = len(array)
    countNegative = 0
 
    for i in range(length):
        if(array[i] < 0):
            countNegative += 1
 
    print("array: ", end = "")
    printArray(array, length)
    rearrange(array, 0, (length - 1))
 
    reverse(array, countNegative, (length - 1))
 
    print("rearranged array: ", end = "")
    printArray(array, length)
 
# This code is contributed by mohit kumar 29
```

## C#

```cs
// C# implementation of 
// the above approach
using System;
class GFG{
 
static void printArray(int []array, 
                       int length)
{
  Console.Write("[");
 
  for(int i = 0; i < length; i++)
  {
    Console.Write(array[i]);
 
    if(i < (length - 1))
      Console.Write(",");
    else
      Console.Write("]\n");
  }
}
  
static void reverse(int []array, 
                    int start, int end)
{
  while(start < end)
  {
    int temp = array[start];
    array[start] = array[end];
    array[end] = temp;
    start++;
    end--;
  }
}
  
// Rearrange the array with 
// all negative integers on left 
// and positive integers on right 
// use recursion to split the 
// array with first element
// as one half and the rest 
// array as another and then 
// merge it with head of 
// the array in each step  
static void rearrange(int []array, 
                      int start, int end)
{
  // exit condition 
  if(start == end)
    return;
 
  // rearrange the array 
  // except the first element 
  // in each recursive call 
  rearrange(array, 
            (start + 1), end);
 
  // If the first element of 
  // the array is positive, 
  // then right-rotate the 
  // array by one place first
  // and then reverse the merged array.
  if(array[start] >= 0)
  {
    reverse(array, (start + 1), end);
    reverse(array, start, end);
  }
}
      
// Driver code
public static void Main(string[] args) 
{
 
  int []array = {-12, -11, -13, 
                 -5, -6, 7, 5, 3, 6};
  int length = array.Length;
  int countNegative = 0;
 
  for(int i = 0; i < length; i++)
  {
    if(array[i] < 0)
      countNegative++;
  }
   
  Console.Write("array: ");
  printArray(array, length);
  rearrange(array, 0, (length - 1));
  reverse(array, countNegative, (length - 1));
  Console.Write("rearranged array: ");
  printArray(array, length);
}
}
 
// This code is contributed by Rutvik_56
```
输出：

```
array: [-12, -11, -13, -5, -6, 7, 5, 3, 6]
rearranged array: [-12, -11, -13, -5, -6, 7, 5, 3, 6]
```

时间复杂度：`O(N)`。