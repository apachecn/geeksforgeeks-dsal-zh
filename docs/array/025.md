# 拆分数组并将第一部分添加到末尾

> 原文： [https://www.geeksforgeeks.org/split-array-add-first-part-end/](https://www.geeksforgeeks.org/split-array-add-first-part-end/)

有一个给定的数组，并将其从指定位置拆分，然后将数组的第一部分加到末尾。

![Split the array and add the first part to the end](img/668cfee1ece2e0524c6a867d516a9ad2.png)

**示例**：

```
Input : arr[] = {12, 10, 5, 6, 52, 36}
            k = 2
Output : arr[] = {5, 6, 52, 36, 12, 10}
Explanation : Split from index 2 and first 
part {12, 10} add to the end .

Input : arr[] = {3, 1, 2}
           k = 1
Output : arr[] = {1, 2, 3}
Explanation : Split from index 1 and first
part add to the end.

```



**简单解决方案**：

我们一对一旋转数组。

## C++ 

```cpp

// CPP program to split array and move first 
// part to end. 
#include <bits/stdc++.h> 
using namespace std; 

void splitArr(int arr[], int n, int k) 
{ 
    for (int i = 0; i < k; i++) { 

        // Rotate array by 1\. 
        int x = arr[0]; 
        for (int j = 0; j < n - 1; ++j) 
            arr[j] = arr[j + 1]; 
        arr[n - 1] = x; 
    } 
} 

// Driver code 
int main() 
{ 
    int arr[] = { 12, 10, 5, 6, 52, 36 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    int position = 2; 

    splitArr(arr, 6, position); 

    for (int i = 0; i < n; ++i) 
        printf("%d ", arr[i]); 

    return 0; 
} 

```

## Java

```java
// Java program to split array and move first 
// part to end. 
  
import java.util.*; 
import java.lang.*; 
class GFG { 
    public static void splitArr(int arr[], int n, int k) 
    { 
        for (int i = 0; i < k; i++) { 
  
            // Rotate array by 1. 
            int x = arr[0]; 
            for (int j = 0; j < n - 1; ++j) 
                arr[j] = arr[j + 1]; 
            arr[n - 1] = x; 
        } 
    } 
  
    // Driver code 
    public static void main(String[] args) 
    { 
        int arr[] = { 12, 10, 5, 6, 52, 36 }; 
        int n = arr.length; 
        int position = 2; 
  
        splitArr(arr, 6, position); 
  
        for (int i = 0; i < n; ++i) 
            System.out.print(arr[i] + " "); 
    } 
} 
  
// Code Contributed by Mohit Gupta_OMG <(0_o)> 
```

## Python3

```py
# Python program to split array and move first 
# part to end. 
  
def splitArr(arr, n, k):  
    for i in range(0, k):  
        x = arr[0] 
        for j in range(0, n-1): 
            arr[j] = arr[j + 1] 
          
        arr[n-1] = x 
          
  
# main 
arr = [12, 10, 5, 6, 52, 36] 
n = len(arr) 
position = 2
  
splitArr(arr, n, position) 
  
for i in range(0, n):  
    print(arr[i], end = ' ') 
  
# Code Contributed by Mohit Gupta_OMG <(0_o)>    
```


## C#

```cs
// C# program to split array  
// and move first part to end. 
using System; 
  
class GFG { 
      
    // Function to spilt array and 
    // move first part to end 
    public static void splitArr(int[] arr, int n, 
                                int k) 
    { 
        for (int i = 0; i < k; i++)  
        { 
  
            // Rotate array by 1. 
            int x = arr[0]; 
            for (int j = 0; j < n - 1; ++j) 
                arr[j] = arr[j + 1]; 
            arr[n - 1] = x; 
        } 
    } 
  
    // Driver code 
    public static void Main() 
    { 
        int[] arr = {12, 10, 5, 6, 52, 36}; 
        int n = arr.Length; 
        int position = 2; 
        splitArr(arr, 6, position); 
  
        for (int i = 0; i < n; ++i) 
            Console.Write(arr[i] + " "); 
    } 
} 
  
// This code is contributed by Shrikant13. 
```

## PHP

```php
<?php 
// PHP program to split array  
// and move first part to end. 
  
function splitArr(&$arr, $n, $k) 
{ 
    for ($i = 0; $i < $k; $i++)  
    { 
  
        // Rotate array by 1. 
        $x = $arr[0]; 
        for ($j = 0; $j < $n - 1; ++$j) 
            $arr[$j] = $arr[$j + 1]; 
        $arr[$n - 1] = $x; 
    } 
} 
  
// Driver code 
$arr = array(12, 10, 5, 6, 52, 36); 
$n = sizeof($arr); 
$position = 2; 
  
splitArr($arr, 6, $position); 
  
for ($i = 0; $i < $n; ++$i) 
    echo $arr[$i]." "; 
  
// This code is contributed 
// by ChitraNayal 
?> 
```

输出：

```
5 6 52 36 12 10
```

上述解决方案的时间复杂度为`O(nk)`。

另一种方法：另一种方法是制作一个具有两倍大小的临时数组，然后将数组元素复制到新数组中两次，然后通过将旋转作为起始索引直到数组的长度，将元素从新数组复制到我们的数组中。

下面是上述方法的实现。

## C++

```cpp
// CPP program to split array and move first 
// part to end. 
#include <bits/stdc++.h> 
using namespace std; 
  
// Function to spilt array and  
// move first part to end  
void splitArr(int arr[], int length, int rotation) 
{ 
    int tmp[length * 2] = {0}; 
  
    for(int i = 0; i < length; i++) 
    { 
        tmp[i] = arr[i]; 
        tmp[i + length] = arr[i]; 
    } 
  
    for(int i = rotation; i < rotation + length; i++) 
    { 
        arr[i - rotation] = tmp[i]; 
    } 
} 
  
// Driver code 
int main() 
{ 
    int arr[] = { 12, 10, 5, 6, 52, 36 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    int position = 2; 
  
    splitArr(arr, n, position); 
  
    for (int i = 0; i < n; ++i) 
        printf("%d ", arr[i]); 
  
    return 0; 
} 
  
// This code is contributed by YashKhandelwal8 
```

## Java

```java
// Java program to split array and move first 
// part to end. 
import java.util.*; 
import java.lang.*; 
class GFG { 
      
    // Function to spilt array and 
    // move first part to end 
    public static void SplitAndAdd(int[] A,int length,int rotation){ 
          
        //make a temporary array with double the size  
        int[] tmp = new int[length*2]; 
          
        // copy array element in to new array twice 
        System.arraycopy(A, 0, tmp, 0, length); 
        System.arraycopy(A, 0, tmp, length, length); 
        for(int i=rotation;i<rotation+length;i++) 
            A[i-rotation]=tmp[i]; 
    } 
  
  
    // Driver code 
    public static void main(String[] args) 
    { 
        int arr[] = { 12, 10, 5, 6, 52, 36 }; 
        int n = arr.length; 
        int position = 2; 
  
        SplitAndAdd(arr, n, position); 
  
        for (int i = 0; i < n; ++i) 
            System.out.print(arr[i] + " "); 
    } 
} 
```

## Python3

```py
# Python3 program to split array and  
# move first part to end. 
  
# Function to spilt array and  
# move first part to end 
def SplitAndAdd(A, length, rotation): 
  
    # make a temporary array with double  
    # the size and each index is initialized to 0  
    tmp = [ 0 for i in range(length * 2)]  
  
    # copy array element in to new array twice 
    for i in range(length): 
        tmp[i] = A[i] 
        tmp[i + length] = A[i] 
  
    for i in range(rotation,  
                   rotation + length, 1):  
        A[i - rotation] = tmp[i];  
       
# Driver code  
arr = [12, 10, 5, 6, 52, 36]  
n = len(arr)  
position = 2
SplitAndAdd(arr, n, position);  
for i in range(n): 
    print(arr[i], end = " ") 
print()  
  
# This code is contributed by SOUMYA SEN  
```

## C#


```cs
// C# program to split array  
// and move first part to end.  
using System; 
  
class GFG 
{ 
  
    // Function to spilt array and  
    // move first part to end  
    public static void SplitAndAdd(int[] A,  
                                   int length, 
                                   int rotation) 
    { 
  
        // make a temporary array with double the size  
        int[] tmp = new int[length * 2]; 
  
        // copy array element in to new array twice  
        Array.Copy(A, 0, tmp, 0, length); 
        Array.Copy(A, 0, tmp, length, length); 
        for (int i = rotation; i < rotation + length; i++) 
        { 
            A[i - rotation] = tmp[i]; 
        } 
    } 
  
    // Driver code  
    public static void Main(string[] args) 
    { 
        int[] arr = new int[] {12, 10, 5, 6, 52, 36}; 
        int n = arr.Length; 
        int position = 2; 
  
        SplitAndAdd(arr, n, position); 
  
        for (int i = 0; i < n; ++i) 
        { 
            Console.Write(arr[i] + " "); 
        } 
    } 
} 
  
// This code is contributed by kumar65 
```

输出：

```
5 6 52 36 12 10
```

下面的文章讨论了一种有效的`O(n)`解决方案：[拆分数组并将第一部分添加到末尾 | 系列 2](https://www.geeksforgeeks.org/split-the-array-and-add-the-first-part-to-the-end-set-2/)。

这个问题只不过是数组旋转问题，我们可以在此处应用优化的`O(n)`数组旋转方法。

+   [数组旋转程序](https://www.geeksforgeeks.org/array-rotation/)
+   [数组旋转的块交换算法](https://www.geeksforgeeks.org/block-swap-algorithm-for-array-rotation/)
+   [数组旋转的逆向算法](https://www.geeksforgeeks.org/program-for-array-rotation-continued-reversal-algorithm/)
+   [快速找到数组的多个左旋转 | 系列 1](https://www.geeksforgeeks.org/quickly-find-multiple-left-rotations-of-an-array/)
+   [在`O(n)`时间和`O(1)`空间中打印数组的左旋转](https://www.geeksforgeeks.org/print-left-rotation-array/)