# 两个排序数组的并集和交集

> 原文： [https://www.geeksforgeeks.org/union-and-intersection-of-two-sorted-arrays-2/](https://www.geeksforgeeks.org/union-and-intersection-of-two-sorted-arrays-2/)

给定两个排序的数组，找到它们的并集和交集。

**示例**：

```
Input : arr1[] = {1, 3, 4, 5, 7}
        arr2[] = {2, 3, 5, 6} 
Output : Union : {1, 2, 3, 4, 5, 6, 7} 
         Intersection : {3, 5}

Input : arr1[] = {2, 5, 6}
        arr2[] = {4, 6, 8, 10} 
Output : Union : {2, 4, 5, 6, 8, 10} 
         Intersection : {6}

```

[](https://practice.geeksforgeeks.org/problem-page.php?pid=537)

## 强烈建议您在继续解决方案之前，单击这里进行练习。

**数组`arr1[]`和`arr2[]`的并集**：

要查找两个排序数组的并集，请遵循以下合并过程：

1.  使用两个索引变量`i`和`j`，初始值`i = 0`，`j = 0`。

2.  如果`arr1[i]`小于`arr2[j]`，则打印`arr1[i]`并递增`i`。

3.  如果`arr1[i]`大于`arr2[j]`，则打印`arr2[j]`并递增`j`。

4.  如果两者相同，则打印其中的任何一个并递增`i`和`j`。

5.  打印较大数组的其余元素。

下面是上述方法的实现：

## C++ 

```cpp

// C++ program to find union of 
// two sorted arrays 
#include <bits/stdc++.h> 
using namespace std; 

/* Function prints union of arr1[] and arr2[] 
   m is the number of elements in arr1[] 
   n is the number of elements in arr2[] */
int printUnion(int arr1[], int arr2[], int m, int n) 
{ 
  int i = 0, j = 0; 
  while (i < m && j < n) 
  { 
    if (arr1[i] < arr2[j]) 
       cout << arr1[i++] << " "; 

    else if (arr2[j] < arr1[i]) 
       cout << arr2[j++] << " "; 

    else
    { 
       cout << arr2[j++] << " "; 
       i++; 
    } 
  } 

  /* Print remaining elements of the larger array */
  while(i < m) 
     cout << arr1[i++] << " "; 

  while(j < n) 
    cout << arr2[j++] << " "; 
} 

/* Driver program to test above function */
int main() 
{ 
  int arr1[] = {1, 2, 4, 5, 6}; 
  int arr2[] = {2, 3, 5, 7}; 

  int m = sizeof(arr1)/sizeof(arr1[0]); 
  int n = sizeof(arr2)/sizeof(arr2[0]); 

  // Function calling 
  printUnion(arr1, arr2, m, n); 

  return 0; 
} 

```

## C

```c
// C program to find union of 
// two sorted arrays 
#include <stdio.h> 
  
/* Function prints union of arr1[] and arr2[] 
   m is the number of elements in arr1[] 
   n is the number of elements in arr2[] */
int printUnion(int arr1[], int arr2[], int m, int n) 
{ 
    int i = 0, j = 0; 
    while (i < m && j < n) { 
        if (arr1[i] < arr2[j]) 
            printf(" %d ", arr1[i++]); 
        else if (arr2[j] < arr1[i]) 
            printf(" %d ", arr2[j++]); 
        else { 
            printf(" %d ", arr2[j++]); 
            i++; 
        } 
    } 
  
    /* Print remaining elements of the larger array */
    while (i < m) 
        printf(" %d ", arr1[i++]); 
    while (j < n) 
        printf(" %d ", arr2[j++]); 
} 
  
/* Driver program to test above function */
int main() 
{ 
    int arr1[] = { 1, 2, 4, 5, 6 }; 
    int arr2[] = { 2, 3, 5, 7 }; 
    int m = sizeof(arr1) / sizeof(arr1[0]); 
    int n = sizeof(arr2) / sizeof(arr2[0]); 
    printUnion(arr1, arr2, m, n); 
    getchar(); 
    return 0; 
}
```

## Java

```java
// Java program to find union of 
// two sorted arrays 
  
class FindUnion { 
    /* Function prints union of arr1[] and arr2[] 
    m is the number of elements in arr1[] 
    n is the number of elements in arr2[] */
    static int printUnion(int arr1[], int arr2[], int m, int n) 
    { 
        int i = 0, j = 0; 
        while (i < m && j < n) { 
            if (arr1[i] < arr2[j]) 
                System.out.print(arr1[i++] + " "); 
            else if (arr2[j] < arr1[i]) 
                System.out.print(arr2[j++] + " "); 
            else { 
                System.out.print(arr2[j++] + " "); 
                i++; 
            } 
        } 
  
        /* Print remaining elements of  
         the larger array */
        while (i < m) 
            System.out.print(arr1[i++] + " "); 
        while (j < n) 
            System.out.print(arr2[j++] + " "); 
  
        return 0; 
    } 
  
    public static void main(String args[]) 
    { 
        int arr1[] = { 1, 2, 4, 5, 6 }; 
        int arr2[] = { 2, 3, 5, 7 }; 
        int m = arr1.length; 
        int n = arr2.length; 
        printUnion(arr1, arr2, m, n); 
    } 
}
```

## Python

```py
# Python program to find union of 
# two sorted arrays 
# Function prints union of arr1[] and arr2[] 
# m is the number of elements in arr1[] 
# n is the number of elements in arr2[] 
def printUnion(arr1, arr2, m, n): 
    i, j = 0, 0
    while i < m and j < n: 
        if arr1[i] < arr2[j]: 
            print(arr1[i]) 
            i += 1
        elif arr2[j] < arr1[i]: 
            print(arr2[j]) 
            j+= 1
        else: 
            print(arr2[j]) 
            j += 1
            i += 1
  
    # Print remaining elements of the larger array 
    while i < m: 
        print(arr1[i]) 
        i += 1
  
    while j < n: 
        print(arr2[j]) 
        j += 1
  
# Driver program to test above function 
arr1 = [1, 2, 4, 5, 6] 
arr2 = [2, 3, 5, 7] 
m = len(arr1) 
n = len(arr2) 
printUnion(arr1, arr2, m, n) 
  
# This code is contributed by Pratik Chhajer
```

## C#

```cs
// C# program to find union of 
// two sorted arrays 
  
using System; 
  
class GFG { 
    /* Function prints union of arr1[] and arr2[] 
    m is the number of elements in arr1[] 
    n is the number of elements in arr2[] */
    static int printUnion(int[] arr1, 
                          int[] arr2, int m, int n) 
    { 
        int i = 0, j = 0; 
  
        while (i < m && j < n) { 
            if (arr1[i] < arr2[j]) 
                Console.Write(arr1[i++] + " "); 
            else if (arr2[j] < arr1[i]) 
                Console.Write(arr2[j++] + " "); 
            else { 
                Console.Write(arr2[j++] + " "); 
                i++; 
            } 
        } 
  
        /* Print remaining elements of  
        the larger array */
        while (i < m) 
            Console.Write(arr1[i++] + " "); 
        while (j < n) 
            Console.Write(arr2[j++] + " "); 
  
        return 0; 
    } 
  
    public static void Main() 
    { 
        int[] arr1 = { 1, 2, 4, 5, 6 }; 
        int[] arr2 = { 2, 3, 5, 7 }; 
        int m = arr1.Length; 
        int n = arr2.Length; 
  
        printUnion(arr1, arr2, m, n); 
    } 
} 
  
// This code is contributed by Sam007
```

## PHP

```php
<?php 
// PHP program to find union of 
// two sorted arrays 
  
/* Function prints union of  
  arr1[] and arr2[] m is the 
  number of elements in arr1[] 
  n is the number of elements 
  in arr2[] */
function printUnion($arr1, $arr2, 
                         $m, $n) 
{ 
    $i = 0; $j = 0; 
    while ($i < $m && $j < $n) 
    { 
        if ($arr1[$i] < $arr2[$j]) 
            echo($arr1[$i++] . " "); 
          
        else if ($arr2[$j] < $arr1[$i]) 
            echo($arr2[$j++] . " "); 
          
        else
        { 
            echo($arr2[$j++] . " "); 
            $i++; 
        } 
    } 
      
    // Print remaining elements 
    // of the larger array 
    while($i < $m) 
        echo($arr1[$i++] . " "); 
      
    while($j < $n) 
        echo($arr2[$j++] . " "); 
} 
  
// Driver Code 
$arr1 = array(1, 2, 4, 5, 6); 
$arr2 = array(2, 3, 5, 7); 
  
$m = sizeof($arr1); 
$n = sizeof($arr2); 
  
// Function calling 
printUnion($arr1, $arr2, $m, $n); 
  
// This code is contributed by Ajit. 
?>
```

输出：

```
1 2 3 4 5 6 7 
```

时间复杂度：`O(m + n)`。

处理任何数组中的重复项：上面的代码不处理任何数组中的重复项。 要处理重复项，只需检查每个元素相邻元素是否相等。

下面是此方法的实现。

## Java

```java
// Java program to find union of two 
// sorted arrays (Handling Duplicates) 
class FindUnion { 
  
    static void UnionArray(int arr1[], 
                           int arr2[]) 
    { 
        // Taking max element present in either array 
        int m = arr1[arr1.length - 1]; 
        int n = arr2[arr2.length - 1]; 
  
        int ans = 0; 
  
        if (m > n) { 
            ans = m; 
        } 
        else
            ans = n; 
  
        // Finding elements from 1st array 
        // (non duplicates only). Using 
        // another array for storing union 
        // elements of both arrays 
        // Assuming max element present 
        // in array is not more than 10^7 
        int newtable[] = new int[ans + 1]; 
  
        // First element is always 
        // present in final answer 
        System.out.print(arr1[0] + " "); 
  
        // Incrementing the First element's count 
        // in it's corresponding index in newtable 
        ++newtable[arr1[0]]; 
  
        // Starting traversing the first 
        // array from 1st index till last 
        for (int i = 1; i < arr1.length; i++) { 
            // Checking whether current element 
            // is not equal to it's previous element 
            if (arr1[i] != arr1[i - 1]) { 
                System.out.print(arr1[i] + " "); 
                ++newtable[arr1[i]]; 
            } 
        } 
  
        // Finding only non common 
        // elements from 2nd array 
        for (int j = 0; j < arr2.length; j++) { 
            // By checking whether it's already 
            // present in newtable or not 
            if (newtable[arr2[j]] == 0) { 
                System.out.print(arr2[j] + " "); 
                ++newtable[arr2[j]]; 
            } 
        } 
    } 
  
    // Driver Code 
    public static void main(String args[]) 
    { 
        int arr1[] = { 1, 2, 2, 2, 3 }; 
        int arr2[] = { 2, 3, 4, 5 }; 
  
        UnionArray(arr1, arr2); 
    } 
}
```

## Python3

```py
# Python3 program to find union of two  
# sorted arrays (Handling Duplicates)  
def UnionArray(arr1, arr2):  
      
    # Taking max element present in either array  
    m = arr1[-1]  
    n = arr2[-1]  
    ans = 0
          
    if m > n:  
        ans = m  
    else: 
        ans = n  
          
    # Finding elements from 1st array  
    # (non duplicates only). Using  
    # another array for storing union  
    # elements of both arrays  
    # Assuming max element present  
    # in array is not more than 10 ^ 7  
    newtable = [0] * (ans + 1)  
          
    # First element is always  
    # present in final answer  
    print(arr1[0], end = " ")  
          
    # Incrementing the First element's count  
    # in it's corresponding index in newtable  
    newtable[arr1[0]] += 1
          
    # Starting traversing the first  
    # array from 1st index till last  
    for i in range(1, len(arr1)):  
          
        # Checking whether current element  
        # is not equal to it's previous element  
        if arr1[i] != arr1[i - 1]:  
              
            print(arr1[i], end = " ")  
            newtable[arr1[i]] += 1
              
    # Finding only non common  
    # elements from 2nd array          
    for j in range(0, len(arr2)):  
          
        # By checking whether it's already  
        # present in newtable or not  
        if newtable[arr2[j]] == 0:  
              
            print(arr2[j], end = " ")  
            newtable[arr2[j]] += 1
      
# Driver Code  
if __name__ == "__main__":  
      
    arr1 = [1, 2, 2, 2, 3] 
    arr2 = [2, 3, 4, 5] 
          
    UnionArray(arr1, arr2)  
  
# This code is contributed by Rituraj Jain
```

## C#

```cs
// C# program to find union of two 
// sorted arrays (Handling Duplicates) 
using System; 
  
class GFG { 
  
    static void UnionArray(int[] arr1, 
                           int[] arr2) 
    { 
  
        // Taking max element present 
        // in either array 
        int m = arr1[arr1.Length - 1]; 
        int n = arr2[arr2.Length - 1]; 
  
        int ans = 0; 
  
        if (m > n) 
            ans = m; 
        else
            ans = n; 
  
        // Finding elements from 1st array 
        // (non duplicates only). Using 
        // another array for storing union 
        // elements of both arrays 
        // Assuming max element present 
        // in array is not more than 10^7 
        int[] newtable = new int[ans + 1]; 
  
        // First element is always 
        // present in final answer 
        Console.Write(arr1[0] + " "); 
  
        // Incrementing the First element's 
        // count in it's corresponding 
        // index in newtable 
        ++newtable[arr1[0]]; 
  
        // Starting traversing the first 
        // array from 1st index till last 
        for (int i = 1; i < arr1.Length; i++) { 
            // Checking whether current 
            // element is not equal to 
            // it's previous element 
            if (arr1[i] != arr1[i - 1]) { 
                Console.Write(arr1[i] + " "); 
                ++newtable[arr1[i]]; 
            } 
        } 
  
        // Finding only non common 
        // elements from 2nd array 
        for (int j = 0; j < arr2.Length; j++) { 
            // By checking whether it's already 
            // present in newtable or not 
            if (newtable[arr2[j]] == 0) { 
                Console.Write(arr2[j] + " "); 
                ++newtable[arr2[j]]; 
            } 
        } 
    } 
  
    // Driver Code 
    public static void Main() 
    { 
        int[] arr1 = { 1, 2, 2, 2, 3 }; 
        int[] arr2 = { 2, 3, 4, 5 }; 
  
        UnionArray(arr1, arr2); 
    } 
} 
  
// This code is contributed by anuj_67.
```

感谢 Rajat Rawat 提出了此解决方案。
 

数组`arr1[]`和`arr2[]`的交集

要找到 2 个排序数组的交集，请遵循以下方法：
 

1.  使用两个索引变量`i`和`j`，初始值`i = 0`，`j = 0`
2.  如果`arr1[i]`小于`arr2[j]`，则递增`i`。
3.  如果`arr1[i]`大于`arr2[j]`，则递增`j`。
4.  如果两者相同，则打印它们中的任何一个并增加`i`和。

下面是上述方法的实现：

## C++

```cpp
// C++ program to find intersection of 
// two sorted arrays 
#include <bits/stdc++.h> 
using namespace std; 
  
/* Function prints Intersection of arr1[] and arr2[] 
m is the number of elements in arr1[] 
n is the number of elements in arr2[] */
int printIntersection(int arr1[], int arr2[], int m, int n) 
{ 
    int i = 0, j = 0; 
    while (i < m && j < n) { 
        if (arr1[i] < arr2[j]) 
            i++; 
        else if (arr2[j] < arr1[i]) 
            j++; 
        else /* if arr1[i] == arr2[j] */
        { 
            cout << arr2[j] << " "; 
            i++; 
            j++; 
        } 
    } 
} 
  
/* Driver program to test above function */
int main() 
{ 
    int arr1[] = { 1, 2, 4, 5, 6 }; 
    int arr2[] = { 2, 3, 5, 7 }; 
  
    int m = sizeof(arr1) / sizeof(arr1[0]); 
    int n = sizeof(arr2) / sizeof(arr2[0]); 
  
    // Function calling 
    printIntersection(arr1, arr2, m, n); 
  
    return 0; 
}
```

## C

```c
// C program to find intersection of 
// two sorted arrays 
#include <stdio.h> 
  
/* Function prints Intersection of arr1[] and arr2[] 
   m is the number of elements in arr1[] 
   n is the number of elements in arr2[] */
int printIntersection(int arr1[], int arr2[], int m, int n) 
{ 
    int i = 0, j = 0; 
    while (i < m && j < n) { 
        if (arr1[i] < arr2[j]) 
            i++; 
        else if (arr2[j] < arr1[i]) 
            j++; 
        else /* if arr1[i] == arr2[j] */
        { 
            printf(" %d ", arr2[j++]); 
            i++; 
        } 
    } 
} 
  
/* Driver program to test above function */
int main() 
{ 
    int arr1[] = { 1, 2, 4, 5, 6 }; 
    int arr2[] = { 2, 3, 5, 7 }; 
    int m = sizeof(arr1) / sizeof(arr1[0]); 
    int n = sizeof(arr2) / sizeof(arr2[0]); 
    printIntersection(arr1, arr2, m, n); 
    getchar(); 
    return 0; 
}
```

## Java

```java
// Java program to find intersection of 
// two sorted arrays 
  
class FindIntersection { 
    /* Function prints Intersection of arr1[] and arr2[] 
       m is the number of elements in arr1[] 
       n is the number of elements in arr2[] */
    static void printIntersection(int arr1[], int arr2[], int m, int n) 
    { 
        int i = 0, j = 0; 
        while (i < m && j < n) { 
            if (arr1[i] < arr2[j]) 
                i++; 
            else if (arr2[j] < arr1[i]) 
                j++; 
            else { 
                System.out.print(arr2[j++] + " "); 
                i++; 
            } 
        } 
    } 
  
    public static void main(String args[]) 
    { 
        int arr1[] = { 1, 2, 4, 5, 6 }; 
        int arr2[] = { 2, 3, 5, 7 }; 
        int m = arr1.length; 
        int n = arr2.length; 
        printIntersection(arr1, arr2, m, n); 
    } 
}
```

## Python

```py
# Python program to find intersection of 
# two sorted arrays 
# Function prints Intersection of arr1[] and arr2[] 
# m is the number of elements in arr1[] 
# n is the number of elements in arr2[] 
def printIntersection(arr1, arr2, m, n): 
    i, j = 0, 0
    while i < m and j < n: 
        if arr1[i] < arr2[j]: 
            i += 1
        elif arr2[j] < arr1[i]: 
            j+= 1
        else: 
            print(arr2[j]) 
            j += 1
            i += 1
  
# Driver program to test above function 
arr1 = [1, 2, 4, 5, 6] 
arr2 = [2, 3, 5, 7] 
m = len(arr1) 
n = len(arr2) 
printIntersection(arr1, arr2, m, n) 
  
# This code is contributed by Pratik Chhajer
```

## C#

```cs
// C# program to find Intersection of 
// two sorted arrays 
  
using System; 
  
class GFG { 
  
    /* Function prints Intersection of arr1[] 
    and arr2[] m is the number of elements in arr1[] 
    n is the number of elements in arr2[] */
    static void printIntersection(int[] arr1, 
                                  int[] arr2, int m, int n) 
    { 
        int i = 0, j = 0; 
  
        while (i < m && j < n) { 
            if (arr1[i] < arr2[j]) 
                i++; 
            else if (arr2[j] < arr1[i]) 
                j++; 
            else { 
                Console.Write(arr2[j++] + " "); 
                i++; 
            } 
        } 
    } 
  
    // driver code 
    public static void Main() 
    { 
        int[] arr1 = { 1, 2, 4, 5, 6 }; 
        int[] arr2 = { 2, 3, 5, 7 }; 
        int m = arr1.Length; 
        int n = arr2.Length; 
  
        printIntersection(arr1, arr2, m, n); 
    } 
} 
  
// This code is contributed by Sam007
```

## PHP

```php
<?php 
// PHP program to find intersection of 
// two sorted arrays 
  
/* Function prints Intersection  
   of arr1[] and arr2[] m is the 
   number of elements in arr1[]  
   n is the number of elements 
   in arr2[] */
function printIntersection($arr1, $arr2, 
                                $m, $n) 
{ 
    $i = 0 ; 
    $j = 0; 
    while ($i < $m && $j < $n) 
    { 
        if ($arr1[$i] < $arr2[$j]) 
            $i++; 
        else if ($arr2[$j] < $arr1[$i]) 
            $j++; 
              
        /* if arr1[i] == arr2[j] */
        else 
        { 
            echo $arr2[$j], " "; 
            $i++; 
            $j++; 
        } 
    } 
} 
  
// Driver Code 
$arr1 = array(1, 2, 4, 5, 6); 
$arr2 = array(2, 3, 5, 7); 
  
$m = count($arr1); 
$n = count($arr2); 
  
// Function calling 
printIntersection($arr1, $arr2, $m, $n); 
  
// This code is contributed by anuj_67. 
?>
```

输出：

```
2 5
```

时间复杂度：`O(m + n)`。

处理数组中的重复项：

上面的代码不处理数组中的重复元素。 相交不应计入重复元素。 要处理重复项，只需检查相交列表中是否已存在当前元素。 下面是此方法的实现。

## Python3

```py
# Python3 program to find Intersection of two 
# Sorted Arrays (Handling Duplicates) 
def IntersectionArray(a, b, n, m): 
    ''' 
    :param a: given sorted array a 
    :param n: size of sorted array a 
    :param b: given sorted array b 
    :param m: size of sorted array b 
    :return: array of intersection of two array or -1 
    '''
  
    Intersection = [] 
    i = j = 0
      
    while i < n and j < m: 
        if a[i] == b[j]: 
  
            # If duplicate already present in Intersection list 
            if len(Intersection) > 0 and Intersection[-1] == a[i]: 
                i+= 1
                j+= 1
  
            # If no duplicate is present in Intersection list 
            else: 
                Intersection.append(a[i]) 
                i+= 1
                j+= 1
        elif a[i] < b[j]: 
            i+= 1
        else: 
            j+= 1
              
    if not len(Intersection): 
        return [-1] 
    return Intersection 
  
# Driver Code 
if __name__ == "__main__": 
  
    arr1 = [1, 2, 2, 3, 4] 
    arr2 = [2, 2, 4, 6, 7, 8] 
      
    l = IntersectionArray(arr1, arr2, len(arr1), len(arr2)) 
    print(*l) 
  
# This code is contributed by Abhishek Kumar
```

输出：

```
2 4
```

时间复杂度：`O(m + n)`。

辅助空间：`O(min(m, n))`。

当两个给定数组的大小之间的差异很大时，另一种有用的方法。

这个想法是遍历较短的数组，并对大数组中的短数组的每个元素进行二进制搜索（请注意，数组已排序）。 该解决方案的时间复杂度为`O(min(mLogn, nLogm))`。 当较大长度与较小长度的比率大于对数阶时，此解决方案比上述方法更好。

<https://www.youtube.com/watch?v=EQQp4B_CU5Q>

请参阅以下文章以了解未排序的数组：

[查找两个未排序数组的并集和交集](https://www.geeksforgeeks.org/find-union-and-intersection-of-two-unsorted-arrays/)。