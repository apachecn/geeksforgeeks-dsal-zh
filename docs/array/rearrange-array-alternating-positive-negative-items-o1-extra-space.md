# 重新排列数组，交替出现正数和负数项，辅助空间为`O(1)` | 系列 1

> 原文： [https://www.geeksforgeeks.org/rearrange-array-alternating-positive-negative-items-o1-extra-space/](https://www.geeksforgeeks.org/rearrange-array-alternating-positive-negative-items-o1-extra-space/)

给定正负数组，以其他方式排列它们，使每个正数后跟负数，反之亦然，以保持外观顺序。

正数和负数不必相等。 如果有更多正数，它们将出现在数组的末尾。 如果还有更多负数，它们也会出现在数组的末尾。

**示例**：

```
Input:  arr[] = {1, 2, 3, -4, -1, 4}
Output: arr[] = {-4, 1, -1, 2, 3, 4}

Input:  arr[] = {-5, -2, 5, 2, 4, 7, 1, 8, 0, -8}
output: arr[] = {-5, 5, -2, 2, -8, 4, 7, 1, 8, 0} 
```

这个问题在很多地方都被问过（请参阅[这里](https://www.geeksforgeeks.org/amazon-interview-set-118-campus-internship/)和[这里](https://www.geeksforgeeks.org/amazon-interview-set-114-campus-internship/)）

如果允许`O(n)`多余的空间，则可以轻松解决上述问题。 由于`O(1)`的额外空间和出现顺序的限制，它变得很有趣。

这个想法是从左到右处理数组。 在处理时，在剩余的未处理数组中找到第一个不合适的元素。 如果元素为负且索引为奇数，或者为正且索引为偶数，则该元素不合适。 一旦找到不适当的元素，我们将在它后面找到带有相反符号的第一个元素。 我们在这两个元素（包括这两个）之间右旋转子数组。

以下是上述想法的实现。

## C++ 

```cpp

/*  C++ program to rearrange positive and negative integers in alternate 
    fashion while keeping the order of positive and negative numbers. */
#include <iostream> 
#include <assert.h> 
using namespace std; 

// Utility function to right rotate all elements between [outofplace, cur] 
void rightrotate(int arr[], int n, int outofplace, int cur) 
{ 
    char tmp = arr[cur]; 
    for (int i = cur; i > outofplace; i--) 
        arr[i] = arr[i-1]; 
    arr[outofplace] = tmp; 
} 

void rearrange(int arr[], int n) 
{ 
    int outofplace = -1; 

    for (int index = 0; index < n; index ++) 
    { 
        if (outofplace >= 0) 
        { 
            // find the item which must be moved into the out-of-place 
            // entry if out-of-place entry is positive and current 
            // entry is negative OR if out-of-place entry is negative 
            // and current entry is negative then right rotate 
            // 
            // [...-3, -4, -5, 6...] -->   [...6, -3, -4, -5...] 
            //      ^                          ^ 
            //      |                          | 
            //     outofplace      -->      outofplace 
            // 
            if (((arr[index] >= 0) && (arr[outofplace] < 0)) 
                || ((arr[index] < 0) && (arr[outofplace] >= 0))) 
            { 
                rightrotate(arr, n, outofplace, index); 

                // the new out-of-place entry is now 2 steps ahead 
                if (index - outofplace >= 2) 
                    outofplace = outofplace + 2; 
                else
                    outofplace = -1; 
            } 
        } 

        // if no entry has been flagged out-of-place 
        if (outofplace == -1) 
        { 
            // check if current entry is out-of-place 
            if (((arr[index] >= 0) && (!(index & 0x01))) 
                || ((arr[index] < 0) && (index & 0x01))) 
            { 
                outofplace = index; 
            } 
        } 
    } 
} 

// A utility function to print an array 'arr[]' of size 'n' 
void printArray(int arr[], int n) 
{ 
    for (int i = 0; i < n; i++) 
      cout << arr[i] << " "; 
    cout << endl; 
} 

// Driver program to test abive function 
int main() 
{ 
    //int arr[n] = {-5, 3, 4, 5, -6, -2, 8, 9, -1, -4}; 
    //int arr[] = {-5, -3, -4, -5, -6, 2 , 8, 9, 1 , 4}; 
    //int arr[] = {5, 3, 4, 2, 1, -2 , -8, -9, -1 , -4}; 
    //int arr[] = {-5, 3, -4, -7, -1, -2 , -8, -9, 1 , -4}; 
    int arr[] = {-5, -2, 5, 2, 4, 7, 1, 8, 0, -8}; 
    int n = sizeof(arr)/sizeof(arr[0]); 

    cout << "Given array is \n"; 
    printArray(arr, n); 

    rearrange(arr, n); 

    cout << "Rearranged array is \n"; 
    printArray(arr, n); 

    return 0; 
} 

```

## Java

```java
class RearrangeArray  
{ 
    // Utility function to right rotate all elements  
    // between [outofplace, cur] 
    void rightrotate(int arr[], int n, int outofplace, int cur)  
    { 
        int tmp = arr[cur]; 
        for (int i = cur; i > outofplace; i--) 
            arr[i] = arr[i - 1]; 
        arr[outofplace] = tmp; 
    } 
  
    void rearrange(int arr[], int n)  
    { 
        int outofplace = -1; 
  
        for (int index = 0; index < n; index++)  
        { 
            if (outofplace >= 0)  
            { 
                // find the item which must be moved into the out-of-place 
                // entry if out-of-place entry is positive and current 
                // entry is negative OR if out-of-place entry is negative 
                // and current entry is negative then right rotate 
                // 
                // [...-3, -4, -5, 6...] -->   [...6, -3, -4, -5...] 
                //      ^                          ^ 
                //      |                          | 
                //     outofplace      -->      outofplace 
                // 
                if (((arr[index] >= 0) && (arr[outofplace] < 0)) 
                        || ((arr[index] < 0) && (arr[outofplace] >= 0)))  
                { 
                    rightrotate(arr, n, outofplace, index); 
  
                    // the new out-of-place entry is now 2 steps ahead 
                    if (index - outofplace > 2)  
                        outofplace = outofplace + 2; 
                    else
                        outofplace = -1; 
                } 
            } 
  
            // if no entry has been flagged out-of-place 
            if (outofplace == -1)  
            { 
                // check if current entry is out-of-place 
                if (((arr[index] >= 0) && ((index & 0x01)==0)) 
                        || ((arr[index] < 0) && (index & 0x01)==1)) 
                    outofplace = index; 
            } 
        } 
    } 
   
    // A utility function to print an array 'arr[]' of size 'n' 
    void printArray(int arr[], int n)  
    { 
        for (int i = 0; i < n; i++) 
            System.out.print(arr[i] + " "); 
        System.out.println(""); 
    } 
  
    public static void main(String[] args)  
    { 
        RearrangeArray rearrange = new RearrangeArray(); 
        //int arr[n] = {-5, 3, 4, 5, -6, -2, 8, 9, -1, -4}; 
        //int arr[] = {-5, -3, -4, -5, -6, 2 , 8, 9, 1 , 4}; 
        //int arr[] = {5, 3, 4, 2, 1, -2 , -8, -9, -1 , -4}; 
        //int arr[] = {-5, 3, -4, -7, -1, -2 , -8, -9, 1 , -4}; 
        int arr[] = {-5, -2, 5, 2, 4, 7, 1, 8, 0, -8}; 
        int n = arr.length; 
  
        System.out.println("Given array is "); 
        rearrange.printArray(arr, n); 
  
        rearrange.rearrange(arr, n); 
  
        System.out.println("RearrangeD array is "); 
        rearrange.printArray(arr, n); 
    } 
} 
  
// This code has been contributed by Mayank Jaiswal 
```

## Python3

```py
# Python3 program to rearrange  
# positive and negative integers  
# in alternate fashion and  
# maintaining the order of positive  
# and negative numbers 
  
# rotates the array to right by once 
# from index 'outOfPlace to cur' 
def rightRotate(arr, n, outOfPlace, cur): 
    temp = arr[cur] 
    for i in range(cur, outOfPlace, -1): 
        arr[i] = arr[i - 1] 
    arr[outOfPlace] = temp 
    return arr 
  
def rearrange(arr, n): 
    outOfPlace = -1
    for index in range(n): 
        if(outOfPlace >= 0): 
  
            # if element at outOfPlace place in  
            # negative and if element at index 
            # is positive we can rotate the  
            # array to right or if element 
            # at outOfPlace place in positive and 
            # if element at index is negative we  
            # can rotate the array to right 
            if((arr[index] >= 0 and arr[outOfPlace] < 0) or 
               (arr[index] < 0 and arr[outOfPlace] >= 0)): 
                arr = rightRotate(arr, n, outOfPlace, index) 
                if(index-outOfPlace > 2): 
                    outOfPlace += 2
                else: 
                    outOfPlace =- 1
                      
        if(outOfPlace == -1): 
              
            # conditions for A[index] to  
            # be in out of place 
            if((arr[index] >= 0 and index % 2 == 0) or 
               (arr[index] < 0 and index % 2 == 1)): 
                outOfPlace = index 
    return arr 
  
# Driver Code 
arr = [-5, -2, 5, 2, 4,  
        7, 1, 8, 0, -8] 
  
print("Given Array is:") 
print(arr) 
  
print("\nRearranged array is:") 
print(rearrange(arr, len(arr))) 
  
# This code is contributed 
# by Charan Sai 
```

## C#

```cs
// Rearrange array in alternating positive 
// & negative items with O(1) extra space 
using System; 
  
class GFG 
{ 
    // Utility function to right rotate 
    // all elements between [outofplace, cur] 
    static void rightrotate(int []arr, int n, 
                            int outofplace, int cur)  
    { 
        int tmp = arr[cur]; 
        for (int i = cur; i > outofplace; i--) 
            arr[i] = arr[i - 1]; 
        arr[outofplace] = tmp; 
    } 
  
    static void rearrange(int []arr, int n)  
    { 
        int outofplace = -1; 
  
        for (int index = 0; index < n; index++)  
        { 
            if (outofplace >= 0)  
            { 
                // find the item which must be moved 
                // into the out-of-place entry if out-of- 
                // place entry is positive and current 
                // entry is negative OR if out-of-place 
                // entry is negative and current entry  
                // is negative then right rotate 
                // [...-3, -4, -5, 6...] --> [...6, -3, -4, -5...] 
                //     ^                         ^ 
                //     |                         | 
                //     outofplace     -->     outofplace 
                // 
                if (((arr[index] >= 0) && 
                     (arr[outofplace] < 0)) || 
                     ((arr[index] < 0) && 
                     (arr[outofplace] >= 0)))  
                { 
                    rightrotate(arr, n, outofplace, index); 
  
                    // the new out-of-place entry  
                    // is now 2 steps ahead 
                    if (index - outofplace > 2)  
                        outofplace = outofplace + 2; 
                    else
                        outofplace = -1; 
                } 
            } 
  
            // if no entry has been flagged out-of-place 
            if (outofplace == -1)  
            { 
                // check if current entry is out-of-place 
                if (((arr[index] >= 0) && 
                    ((index & 0x01)==0)) ||  
                    ((arr[index] < 0) && 
                    (index & 0x01)==1)) 
                    outofplace = index; 
            } 
        } 
    } 
  
    // A utility function to print an 
    // array 'arr[]' of size 'n' 
    static void printArray(int []arr, int n)  
    { 
        for (int i = 0; i < n; i++) 
            Console.Write(arr[i] + " "); 
        Console.WriteLine(""); 
    } 
  
    // Driver code 
    public static void Main()  
    { 
        int []arr = {-5, -2, 5, 2, 4, 
                      7, 1, 8, 0, -8}; 
        int n = arr.Length; 
  
        Console.WriteLine("Given array is "); 
        printArray(arr, n); 
  
        rearrange(arr, n); 
  
        Console.WriteLine("RearrangeD array is "); 
        printArray(arr, n); 
    } 
} 
  
// This code is contributed by Sam007 
```

## PHP

```php
<?php  
// PHP program to rearrange positive and  
// negative integers in alternate fashion  
// while keeping the order of positive  
// and negative numbers.  
  
// Utility function to right rotate all 
// elements between [outofplace, cur] 
function rightrotate(&$arr, $n,  
                      $outofplace, $cur) 
{ 
    $tmp = $arr[$cur]; 
    for ($i = $cur; $i > $outofplace; $i--) 
        $arr[$i] = $arr[$i - 1]; 
    $arr[$outofplace] = $tmp; 
} 
  
function rearrange(&$arr, $n) 
{ 
    $outofplace = -1; 
  
    for ($index = 0; $index < $n; $index ++) 
    { 
        if ($outofplace >= 0) 
        { 
            // find the item which must be moved  
            // into the out-of-place entry if  
            // out-of-place entry is positive and 
            // current entry is negative OR if  
            // out-of-place entry is negative 
            // and current entry is negative then  
            // right rotate 
            // [...-3, -4, -5, 6...] --> [...6, -3, -4, -5...] 
            //     ^                         ^ 
            //     |                         | 
            //     outofplace     -->     outofplace 
            // 
            if ((($arr[$index] >= 0) && ($arr[$outofplace] < 0)) ||  
                (($arr[$index] < 0) && ($arr[$outofplace] >= 0))) 
            { 
                rightrotate($arr, $n, $outofplace, $index); 
  
                // the new out-of-place entry is  
                // now 2 steps ahead 
                if ($index - $outofplace > 2) 
                    $outofplace = $outofplace + 2; 
                else
                    $outofplace = -1; 
            } 
        } 
  
        // if no entry has been flagged out-of-place 
        if ($outofplace == -1) 
        { 
            // check if current entry is out-of-place 
            if ((($arr[$index] >= 0) && (!($index & 0x01))) 
                || (($arr[$index] < 0) && ($index & 0x01))) 
            { 
                $outofplace = $index; 
            } 
        } 
    } 
} 
  
// A utility function to print an 
// array 'arr[]' of size 'n' 
function printArray(&$arr, $n) 
{ 
    for ($i = 0; $i < $n; $i++) 
    echo $arr[$i]." "; 
    echo "\n"; 
} 
  
// Driver Code 
  
// arr = array(-5, 3, 4, 5, -6, -2, 8, 9, -1, -4); 
// arr = array(-5, -3, -4, -5, -6, 2 , 8, 9, 1 , 4); 
// arr = array(5, 3, 4, 2, 1, -2 , -8, -9, -1 , -4); 
// arr = array(-5, 3, -4, -7, -1, -2 , -8, -9, 1 , -4); 
$arr = array(-5, -2, 5, 2, 4, 7, 1, 8, 0, -8); 
$n = sizeof($arr); 
  
echo "Given array is \n"; 
printArray($arr, $n); 
  
rearrange($arr, $n); 
  
echo "Rearranged array is \n"; 
printArray($arr, $n); 
  
// This code is contributed by ChitraNayal 
?> 
```

输出：

```
Given array is
-5 -2 5 2 4 7 1 8 0 -8
Rearranged array is
-5 5 -2 2 -8 4 7 1 8 0
```

