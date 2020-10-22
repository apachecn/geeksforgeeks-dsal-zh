# 合并两个有`O(1)`额外空间的排序数组

> 原文： [https://www.geeksforgeeks.org/merge-two-sorted-arrays-o1-extra-space/](https://www.geeksforgeeks.org/merge-two-sorted-arrays-o1-extra-space/)

我们给了两个排序数组。 我们需要合并这两个数组，以使初始编号（完成排序后）在第一个数组中，而其余的数字在第二个数组中。`O(1)`中允许有多余的空间。

例：

```
Input: ar1[] = {10};
       ar2[] = {2, 3};
Output: ar1[] = {2}
        ar2[] = {3, 10}  

Input: ar1[] = {1, 5, 9, 10, 15, 20};
       ar2[] = {2, 3, 8, 13};
Output: ar1[] = {1, 2, 3, 5, 8, 9}
        ar2[] = {10, 13, 15, 20} 

```



如果允许我们使用额外的空间，则此任务很简单，并且为`O(m + n)`。 但是，如果不允许有多余的空间，并且看起来在最坏的情况下不到`O(m * n)`，那么看起来就变得非常复杂。

这个想法是从`ar2[]`的最后一个元素开始，然后在`ar1[]`中搜索它。 如果`ar1[]`中有一个更大的元素，那么我们将`ar1[]`的最后一个元素移到`ar2[]`。 为了使`ar1[]`和`ar2[]`保持排序，我们需要将`ar2[]`的最后一个元素放置在`ar1[]`中的正确位置。 为此，我们可以使用[插入排序](http://geeksquiz.com/insertion-sort/)插入类型。 下面是算法：

```
1) Iterate through every element of ar2[] starting from last 
   element. Do following for every element ar2[i]
    a) Store last element of ar1[i]: last = ar1[i]
    b) Loop from last element of ar1[] while element ar1[j] is 
       smaller than ar2[i].
          ar1[j+1] = ar1[j] // Move element one position ahead
          j--
    c) If any element of ar1[] was moved or (j != m-1)
          ar1[j+1] = ar2[i] 
          ar2[i] = last  

```

在上面的循环中，`ar1[]`和`ar2[]`中的元素始终保持排序状态。

下面是上述算法的实现。

## C++ 

```cpp

// C++ program to merge two sorted arrays with O(1) extra space. 
#include <bits/stdc++.h> 
using namespace std; 

// Merge ar1[] and ar2[] with O(1) extra space 
void merge(int ar1[], int ar2[], int m, int n) 
{ 
    // Iterate through all elements of ar2[] starting from 
    // the last element 
    for (int i=n-1; i>=0; i--) 
    { 
        /* Find the smallest element greater than ar2[i]. Move all 
           elements one position ahead till the smallest greater 
           element is not found */
        int j, last = ar1[m-1]; 
        for (j=m-2; j >= 0 && ar1[j] > ar2[i]; j--) 
            ar1[j+1] = ar1[j]; 

        // If there was a greater element 
        if (j != m-2 || last > ar2[i]) 
        { 
            ar1[j+1] = ar2[i]; 
            ar2[i] = last; 
        } 
    } 
} 

// Driver program 
int main(void) 
{ 
    int ar1[] = {1, 5, 9, 10, 15, 20}; 
    int ar2[] = {2, 3, 8, 13}; 
    int m = sizeof(ar1)/sizeof(ar1[0]); 
    int n = sizeof(ar2)/sizeof(ar2[0]); 
    merge(ar1, ar2, m, n); 

    cout << "After Merging nFirst Array: "; 
    for (int i=0; i<m; i++) 
        cout << ar1[i] << " "; 
    cout << "nSecond Array: "; 
    for (int i=0; i<n; i++) 
        cout << ar2[i] << " "; 
   return 0; 
} 

```

## Java

```java
// Java program program to merge two  
// sorted arrays with O(1) extra space. 
  
import java.util.Arrays; 
  
class Test 
{ 
    static int arr1[] = new int[]{1, 5, 9, 10, 15, 20}; 
    static int arr2[] = new int[]{2, 3, 8, 13}; 
      
    static void merge(int m, int n) 
    { 
        // Iterate through all elements of ar2[] starting from 
        // the last element 
        for (int i=n-1; i>=0; i--) 
        { 
            /* Find the smallest element greater than ar2[i]. Move all 
               elements one position ahead till the smallest greater 
               element is not found */
            int j, last = arr1[m-1]; 
            for (j=m-2; j >= 0 && arr1[j] > arr2[i]; j--) 
                arr1[j+1] = arr1[j]; 
       
            // If there was a greater element 
            if (j != m-2 || last > arr2[i]) 
            { 
                arr1[j+1] = arr2[i]; 
                arr2[i] = last; 
            } 
        } 
    } 
      
    // Driver method to test the above function 
    public static void main(String[] args)  
    { 
        merge(arr1.length,arr2.length); 
        System.out.print("After Merging nFirst Array: "); 
        System.out.println(Arrays.toString(arr1)); 
        System.out.print("Second Array:  "); 
        System.out.println(Arrays.toString(arr2)); 
    } 
}
```

## Python3

```py
# Python program to merge 
# two sorted arrays 
# with O(1) extra space. 
  
# Merge ar1[] and ar2[] 
# with O(1) extra space 
def merge(ar1, ar2, m, n): 
  
    # Iterate through all 
    # elements of ar2[] starting from 
    # the last element 
    for i in range(n-1, -1, -1): 
      
        # Find the smallest element 
        # greater than ar2[i]. Move all 
        # elements one position ahead 
        # till the smallest greater 
        # element is not found  
        last = ar1[m-1] 
        j=m-2
        while(j >= 0 and ar1[j] > ar2[i]): 
            ar1[j+1] = ar1[j] 
            j-=1
   
        # If there was a greater element 
        if (j != m-2 or last > ar2[i]): 
          
            ar1[j+1] = ar2[i] 
            ar2[i] = last 
   
# Driver program 
  
ar1 = [1, 5, 9, 10, 15, 20] 
ar2 = [2, 3, 8, 13] 
m = len(ar1) 
n = len(ar2) 
  
merge(ar1, ar2, m, n) 
   
print("After Merging \nFirst Array:", end="") 
for i in range(m): 
    print(ar1[i] , " ", end="") 
  
print("\nSecond Array: ", end="") 
for i in range(n): 
    print(ar2[i] , " ", end="") 
  
# This code is contributed 
# by Anant Agarwal.
```

## C#

```cs
// C# program program to merge two  
// sorted arrays with O(1) extra space.  
using System; 
  
// Java program program to merge two  
// sorted arrays with O(1) extra space.  
  
  
public class Test  
{  
    static int []arr1 = new int[]{1, 5, 9, 10, 15, 20};  
    static int []arr2 = new int[]{2, 3, 8, 13};  
      
    static void merge(int m, int n)  
    {  
        // Iterate through all elements of ar2[] starting from  
        // the last element  
        for (int i=n-1; i>=0; i--)  
        {  
            /* Find the smallest element greater than ar2[i]. Move all  
            elements one position ahead till the smallest greater  
            element is not found */
            int j, last = arr1[m-1];  
            for (j=m-2; j >= 0 && arr1[j] > arr2[i]; j--)  
                arr1[j+1] = arr1[j];  
      
            // If there was a greater element  
            if (j != m-2 || last > arr2[i])  
            {  
                arr1[j+1] = arr2[i];  
                arr2[i] = last;  
            }  
        }  
    }  
      
    // Driver method to test the above function  
    public static void Main()  
    {  
        merge(arr1.Length,arr2.Length);  
        Console.Write("After Merging \nFirst Array: ");  
        for(int i =0; i< arr1.Length;i++){ 
            Console.Write(arr1[i]+" "); 
        } 
        Console.Write("\nSecond Array: ");  
        for(int i =0; i< arr2.Length;i++){ 
            Console.Write(arr2[i]+" "); 
        } 
    }  
}  
  
/*This code is contributed by 29AjayKumar*/
```

## PHP

```php
<?php  
// PHP program to merge two sorted arrays with O(1) extra space. 
   
// Merge ar1[] and ar2[] with O(1) extra space 
function merge(&$ar1, &$ar2, $m, $n) 
{ 
    // Iterate through all elements of ar2[] starting from 
    // the last element 
    for ($i = $n-1; $i >= 0; $i--) 
    { 
        /* Find the smallest element greater than ar2[i]. Move all 
           elements one position ahead till the smallest greater 
           element is not found */
        $last = $ar1[$m-1]; 
        for ($j = $m-2; $j >= 0 && $ar1[$j] > $ar2[$i]; $j--) 
            $ar1[$j+1] = $ar1[$j]; 
   
        // If there was a greater element 
        if ($j != $m-2 || $last > $ar2[$i]) 
        { 
            $ar1[$j+1] = $ar2[$i]; 
            $ar2[$i] = $last; 
        } 
    } 
} 
   
// Driver program 
  
$ar1 = array(1, 5, 9, 10, 15, 20); 
$ar2 = array(2, 3, 8, 13); 
$m = sizeof($ar1)/sizeof($ar1[0]); 
$n = sizeof($ar2)/sizeof($ar2[0]); 
merge($ar1, $ar2, $m, $n); 
  
echo "After Merging \nFirst Array: "; 
for ($i=0; $i<$m; $i++) 
    echo $ar1[$i] . " "; 
echo "\nSecond Array: "; 
for ($i=0; $i<$n; $i++) 
    echo $ar2[$i] ." "; 
return 0; 
?>
```

输出：

```
After Merging 
First Array: 1 2 3 5 8 9 
Second Array: 10 13 15 20 
```

时间复杂度：代码/算法的最坏情况下的时间复杂度为`O(m * n)`。 当`ar1[]`的所有元素都大于`ar2x[]`的所有元素时，会发生最坏的情况。

演示：

![](https://media.geeksforgeeks.org/wp-content/cdn-uploads/Merge-two-sorted-Arrays.png)

```
<!— Initial Arrays:
ar1[] = {1, 5, 9, 10, 15, 20};
ar2[] = {2, 3, 8, 13};

After First Iteration:
ar1[] = {1, 5, 9, 10, 13, 15};
ar2[] = {2, 3, 8, 20};
// 20 is moved from ar1[] to ar2[]
// 13 from ar2[] is inserted in ar1[]

After Second Iteration:
ar1[] = {1, 5, 8, 9, 10, 13};
ar2[] = {2, 3, 15, 20};
// 15 is moved from ar1[] to ar2[]
// 8 from ar2[] is inserted in ar1[]

After Third Iteration:
ar1[] = {1, 3, 5, 8, 9, 10};
ar2[] = {2, 13, 15, 20};
// 13 is moved from ar1[] to ar2[]
// 3 from ar2[] is inserted in ar1[]
```

[使用`O(1)`空间有效合并两个排序数组](https://www.geeksforgeeks.org/efficiently-merging-two-sorted-arrays-wtih-o1-extra-space/)。