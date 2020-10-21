# 正数元素位于偶数位置，负数元素位于奇数位置（不保持相对顺序）

> 原文： [https://www.geeksforgeeks.org/positive-elements-even-negative-odd-positions/](https://www.geeksforgeeks.org/positive-elements-even-negative-odd-positions/)

给您一个数组，您必须编写一个程序来转换该数组，以使正元素出现在数组的偶数位置，而负元素出现在数组的奇数位置。 我们必须做到这一点。

正值和负值的数目可能不相等，多余的值必须保持原样。

**示例**：

```
Input : arr[] = {1, -3, 5, 6, -3, 6, 7, -4, 9, 10}
Output : arr[] = {1, -3, 5, -3, 6, 6, 7, -4, 9, 10}

Input : arr[] = {-1, 3, -5, 6, 3, 6, -7, -4, -9, 10}
Output : arr[] = {3, -1, 6, -5, 3, -7, 6, -4, 10, -9}

```



这个想法是使用[快速排序](https://www.geeksforgeeks.org/quick-sort/)的 [Hoare 分区](https://www.geeksforgeeks.org/hoares-vs-lomuto-partition-scheme-quicksort/)处理。

我们采用正面和负面两个指标。 我们将正指针设置在数组的开头，将负指针设置在数组的第一个位置。

我们将正指针向前移动两步，直到找到负元素。 同样，我们将负指针向前移动两个位置，直到在其位置找到正值。

如果正负指针位于数组中，则我们将交换这些索引处的值，否则将停止执行该过程。

## C++ 

```cpp

// C++ program to rearrange positive and negative 
// numbers 
#include <bits/stdc++.h> 
using namespace std; 

void rearrange(int a[], int size) 
{ 
    int positive = 0, negative = 1; 

    while (true) { 

        /* Move forward the positive pointer till  
         negative number number not encountered */
        while (positive < size && a[positive] >= 0) 
            positive += 2; 

        /* Move forward the negative pointer till  
         positive number number not encountered   */
        while (negative < size && a[negative] <= 0) 
            negative += 2; 

        // Swap array elements to fix their position. 
        if (positive < size && negative < size) 
            swap(a[positive], a[negative]); 

        /* Break from the while loop when any index  
            exceeds the size of the array */
        else
            break; 
    } 
} 

// Driver code 
int main() 
{ 
    int arr[] = { 1, -3, 5, 6, -3, 6, 7, -4, 9, 10 }; 
    int n = (sizeof(arr) / sizeof(arr[0])); 

    rearrange(arr, n);  
    for (int i = 0; i < n; i++) 
        cout << arr[i] << " "; 

    return 0; 
} 

```

## Java

```java

// Java program to rearrange positive 
// and negative numbers 
import java.io.*; 

class GFG { 

static void rearrange(int a[], int size) 
{ 
  int positive = 0, negative = 1, temp; 

    while (true) { 

    /* Move forward the positive pointer till 
    negative number number not encountered */
    while (positive < size && a[positive] >= 0) 
        positive += 2; 

    /* Move forward the negative pointer till 
        positive number number not encountered */
    while (negative < size && a[negative] <= 0) 
        negative += 2; 

    // Swap array elements to fix their position. 
    if (positive < size && negative < size) { 
        temp = a[positive]; 
        a[positive] = a[negative]; 
        a[negative] = temp; 
    } 

    /* Break from the while loop when any index 
    exceeds the size of the array */
    else
        break; 
    } 
} 

// Driver code 
public static void main(String args[]) { 
    int arr[] = {1, -3, 5, 6, -3, 6, 7, -4, 9, 10}; 
    int n = arr.length; 

    rearrange(arr, n); 
    for (int i = 0; i < n; i++) 
    System.out.print(arr[i] + " "); 
} 
} 

/*This code is contributed by Nikita Tiwari.*/

```

## Python3

```py

# Python 3 program to rearrange  
# positive and negative numbers 

def rearrange(a, size) : 

    positive = 0
    negative = 1

    while (True) : 

        # Move forward the positive 
        # pointer till negative number 
        # number not encountered  
        while (positive < size and a[positive] >= 0) : 
            positive = positive + 2

        # Move forward the negative  
        # pointer till positive number 
        # number not encountered  
        while (negative < size and a[negative] <= 0) : 
            negative = negative + 2

        # Swap array elements to fix 
        # their position. 
        if (positive < size and negative < size) : 
            temp = a[positive] 
            a[positive] = a[negative] 
            a[negative] = temp 

        # Break from the while loop when 
        # any index exceeds the size of  
        # the array  
        else : 
            break

# Driver code 
arr =[ 1, -3, 5, 6, -3, 6, 7, -4, 9, 10 ] 
n = len(arr) 

rearrange(arr, n) 
for i in range(0, n) : 
    print(arr[i], end = " ") 

# This code is contributed by Nikita Tiwari. 

```

## C# 

```cs

// C# program to rearrange positive 
// and negative numbers 
using System; 

class GFG { 

// Function to rearrange 
static void rearrange(int []a, int size) 
{ 
int positive = 0, negative = 1, temp; 

    while (true) { 

    // Move forward the positive pointer till 
    // negative number number not encountered  
    while (positive < size && a[positive] >= 0) 
        positive += 2; 

    // Move forward the negative pointer till 
    // positive number number not encountered  
    while (negative < size && a[negative] <= 0) 
        negative += 2; 

    // Swap array elements to fix their position. 
    if (positive < size && negative < size) { 
        temp = a[positive]; 
        a[positive] = a[negative]; 
        a[negative] = temp; 
    } 

    // Break from the while loop when any  
    // index exceeds the size of the array  
    else
        break; 
    } 
} 

// Driver Code 
public static void Main(String []args) { 
    int []arr = {1, -3, 5, 6, -3, 6, 7, -4, 9, 10}; 
    int n = arr.Length; 

    rearrange(arr, n); 
    for (int i = 0; i < n; i++) 
    Console.Write(arr[i] + " "); 
} 
} 

// This code is contributed by Nitin Mittal. 

```

## PHP

```php

<?php  
// PHP program to rearrange positive  
// and negative numbers 

function rearrange(&$a, $size) 
{ 
    $positive = 0; 
    $negative = 1; 

    while (true)  
    { 

        /* Move forward the positive  
        pointer till negative number  
        number not encountered */
        while ($positive < $size &&  
               $a[$positive] >= 0) 
            $positive += 2; 

        /* Move forward the negative  
        pointer till positive number 
        number not encountered */
        while ($negative < $size &&  
               $a[$negative] <= 0) 
            $negative += 2; 

        // Swap array elements to fix 
        // their position. 
        if ($positive < $size &&  
            $negative < $size) 
        { 
            $temp = $a[$positive]; 
            $a[$positive] = $a[$negative]; 
            $a[$negative] = $temp; 
        } 

        /* Break from the while loop  
        when any index exceeds the  
        size of the array */
        else
            break; 
    } 
} 

// Driver code 
$arr = array( 1, -3, 5, 6, -3,  
              6, 7, -4, 9, 10 ); 
$n = sizeof($arr); 

rearrange($arr, $n);  
for ($i = 0; $i < $n; $i++) 
    echo $arr[$i] ." "; 

// This code is contributed by ChitraNayal 
?> 

```

**输出**：

```
1 -3 5 -3 6 6 7 -4 9 10 

```

让我们在第一个示例上解释代码的工作。

`arr[] = {1, -3, 5, 6, -3, 6, 7, -4, 9, 10}`

我们声明两个变量为正负，正数指向第零个位置，负数指向第一个位置。

正`= 0`，负数`= 1`，

在第一次迭代中，由于`a[4]`小于零且正数`= 4`，正数会将 4 个位置移至第五个位置。

负数将移动 2 个位置，并以`a[3] > 0`指向第四位置。

我们将交换正和负位置值，因为它们小于数组的大小。

第一次迭代后，数组变为`arr[] = {1, -3, 5, -3, 6, 6, 7, -4, 9, 10}`。

现在在第四位置的正点和在第三位置的负点。

在第二次迭代中，正值将移动 6 位，其值将比数组的大小大。

负指针将向前移动两步，并将指向第五个位置。

当正指针值变得大于数组大小时，我们将不执行任何交换操作并退出`while`循环。

最终输出为`arr[] = {1, -3, 5, -3, 6, 6, 7, -4, 9, 10}`。

**不维持相对顺序的示例**：

`{-1, -2, -3, -4, -5, 6, 7, 8};`

**另一种方法**：

想法是找到一个不正确位置的正/负元素（即，在奇数位置为正，在偶数位置为负），然后找到符号相反的元素，即在剩余数组中的错误位置，然后交换这两个元素。

这是上述想法的实现。

## C++

```

// C++ program to rearrange positive 
// and negative numbers 
#include<iostream> 
using namespace std; 

// Swap function 
void swap(int* a, int i , int j) 
{ 
    int temp = a[i]; 
    a[i] = a[j]; 
    a[j] = temp; 
    return ; 
} 

// Print array function 
void printArray(int* a, int n) 
{ 
    for(int i = 0; i < n; i++) 
        cout << a[i] << " "; 
    cout << endl; 
    return ; 
} 

// Driver code 
int main() 
{ 
    int arr[] = { 1, -3, 5, 6, -3, 6, 7, -4, 9, 10 }; 
    int n = sizeof(arr)/sizeof(arr[0]); 

    //before modification 
    printArray(arr, n); 

    for(int i = 0; i < n; i++) 
    { 
        if(arr[i] >= 0 && i % 2 == 1) 
        {  
            // out of order positive element 
            for(int j = i + 1; j < n; j++) 
            { 
                if(arr[j] < 0 && j % 2 == 0) 
                {  
                    // find out of order negative  
                    // element in remaining array 
                    swap(arr, i, j); 
                    break ; 
                } 
            } 
        } 
        else if(arr[i] < 0 && i % 2 == 0) 
        { 
            // out of order negative element 
            for(int j = i + 1; j < n; j++) 
            { 
                if(arr[j] >= 0 && j % 2 == 1) 
                { 
                    // find out of order positive  
                    // element in remaining array 
                    swap(arr, i, j); 
                    break; 
                } 
            }  
        } 
    } 

    //after modification 
    printArray(arr, n);  
    return 0; 
} 

// This code is contributed by AnitAggarwal 

```

## Java

```java
// Java program to rearrange positive  
// and negative numbers 
import java.io.*; 
import java.util.*; 
  
class GFG  
{ 
  
    // Swap function 
    static void swap(int[] a, int i, int j) 
    { 
        int temp = a[i];  
        a[i] = a[j];  
        a[j] = temp;  
    } 
  
    // Print array function 
    static void printArray(int[] a, int n) 
    { 
        for (int i = 0; i < n; i++) 
            System.out.print(a[i] + " "); 
        System.out.println(); 
    }  
  
    // Driver code 
    public static void main(String args[])  
    { 
        int[] arr = { 1, -3, 5, 6, -3, 6, 7, -4, 9, 10 }; 
        int n = arr.length; 
              
        //before modification 
        printArray(arr, n);  
  
        for (int i = 0; i < n; i++) 
        { 
            if (arr[i] >= 0 && i % 2 == 1) 
            { 
                // out of order positive element  
                for (int j = i + 1; j < n; j++) 
                { 
                    if (arr[j] < 0 && j % 2 == 0)  
                    {  
                        // find out of order negative  
                        // element in remaining array  
                        swap(arr, i, j);  
                        break ;  
                    }  
                } 
            } 
  
            else if (arr[i] < 0 && i % 2 == 0) 
            { 
                // out of order negative element  
                for (int j = i + 1; j < n; j++)  
                {  
                    if (arr[j] >= 0 && j % 2 == 1)  
                    {  
                        // find out of order positive  
                        // element in remaining array  
                        swap(arr, i, j);  
                        break;  
                    }  
                }  
            } 
        }  
  
        //after modification 
        printArray(arr, n); 
    } 
} 
  
// This code is contributed by rachana soma 
```

## Python3

```py
# Python3 program to rearrange positive 
# and negative numbers 
  
# Print array function 
def printArray(a, n): 
    for i in a: 
        print(i, end = " ") 
    print() 
  
  
# Driver code 
arr = [1, -3, 5, 6, -3, 6, 7, -4, 9, 10] 
n = len(arr) 
  
# before modification 
printArray(arr, n) 
  
for i in range(n): 
  
    if(arr[i] >= 0 and i % 2 == 1): 
  
        # out of order positive element 
        for j in range(i + 1, n): 
  
            if(arr[j] < 0 and j % 2 == 0): 
                  
                # find out of order negative  
                # element in remaining array 
                arr[i], arr[j] = arr[j], arr[i] 
                break
              
    elif (arr[i] < 0 and i % 2 == 0): 
          
        # out of order negative element 
        for j in range(i + 1, n): 
  
            if(arr[j] >= 0 and j % 2 == 1): 
                  
                # find out of order positive  
                # element in remaining array 
                arr[i], arr[j] = arr[j], arr[i] 
                break
  
# after modification 
printArray(arr, n);  
  
# This code is contributed  
# by mohit kumar 
```

## C#

```cs
// C# program to rearrange positive  
// and negative numbers 
using System; 
  
class GFG  
{ 
  
    // Swap function 
    static void swap(int[] a, int i, int j) 
    { 
        int temp = a[i];  
        a[i] = a[j];  
        a[j] = temp;  
    } 
  
    // Print array function 
    static void printArray(int[] a, int n) 
    { 
        for (int i = 0; i < n; i++) 
            Console.Write(a[i] + " "); 
        Console.WriteLine(); 
    }  
  
    // Driver code 
    public static void Main()  
    { 
        int[] arr = { 1, -3, 5, 6, -3, 6, 7, -4, 9, 10 }; 
        int n = arr.Length; 
              
        //before modification 
        printArray(arr, n);  
  
        for (int i = 0; i < n; i++) 
        { 
            if (arr[i] >= 0 && i % 2 == 1) 
            { 
                // out of order positive element  
                for (int j = i + 1; j < n; j++) 
                { 
                    if (arr[j] < 0 && j % 2 == 0)  
                    {  
                        // find out of order negative  
                        // element in remaining array  
                        swap(arr, i, j);  
                        break ;  
                    }  
                } 
            } 
  
            else if (arr[i] < 0 && i % 2 == 0) 
            { 
                // out of order negative element  
                for (int j = i + 1; j < n; j++)  
                {  
                    if (arr[j] >= 0 && j % 2 == 1)  
                    {  
                        // find out of order positive  
                        // element in remaining array  
                        swap(arr, i, j);  
                        break;  
                    }  
                }  
            } 
        }  
  
        // after modification 
        printArray(arr, n); 
    } 
} 
  
// This code is contributed by Akanksha Rai 
```

输出：

```
1 -3 5 6 -3 6 7 -4 9 10 
1 -3 5 -3 6 6 7 -4 9 10 
```
