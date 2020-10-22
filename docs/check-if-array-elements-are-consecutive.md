# 检查数组元素是否连续 | 新增方法 3

> 原文： [https://www.geeksforgeeks.org/check-if-array-elements-are-consecutive/](https://www.geeksforgeeks.org/check-if-array-elements-are-consecutive/)

给定一个未排序的数字数组，编写一个函数，如果该数组包含连续的数字，则该函数返回`true`。

**示例**：

1.  如果数组为`{5, 2, 3, 1, 4}`，则该函数应返回`true`，因为数组具有从 1 到 5 的连续数字 。

2.  如果数组为`{83, 78, 80, 81, 79, 82}`，则该函数应返回`true`，因为数组具有从 78 到 83 的连续数字。

3.  如果数组是`{34, 23, 52, 12, 3}`, 则该函数应返回`false`，因为元素不连续。

4.  如果数组是`{7, 6, 5, 5, 5, 3, 4}`，则该函数应返回`false`，因为 5 和 5 不连续。



**方法 1（使用排序）**：

1.  对所有元素进行排序。

2.  对排序后的数组进行线性扫描。 如果当前元素和下一个元素之间的差不是 1，则返回`false`。 如果所有差异均为 1，则返回`true`。

时间复杂度：`O(nLogn)`。

**方法 2（使用访问数组）**：

这个想法是要检查以下两个条件。 如果满足以下两个条件，则返回`true`。

1.  `max-min + 1 = n`其中`max`是数组中的最大元素，`min`是数组中的最小元素，`n`是数组中的元素数。

2.  所有元素都是不同的。

要检查所有元素是否都不同，我们可以创建大小为`n`的`visited[]`数组。 我们可以使用`arr[i]-min`作为`Visited[]`中的索引，将输入数组`arr[]`的第`i`个元素映射到访问数组。

## C++ 

```cpp

#include<stdio.h> 
#include<stdlib.h> 

/* Helper functions to get minimum and maximum in an array */
int getMin(int arr[], int n); 
int getMax(int arr[], int n); 

/* The function checks if the array elements are consecutive 
  If elements are consecutive, then returns true, else returns 
  false */
bool areConsecutive(int arr[], int n) 
{ 
  if ( n <  1 ) 
    return false; 

  /* 1) Get the minimum element in array */
  int min = getMin(arr, n); 

  /* 2) Get the maximum element in array */
  int max = getMax(arr, n); 

  /* 3) max - min + 1 is equal to n,  then only check all elements */
  if (max - min  + 1 == n) 
  { 
      /* Create a temp array to hold visited flag of all elements. 
         Note that, calloc is used here so that all values are initialized  
         as false */ 
      bool *visited = (bool *) calloc (n, sizeof(bool)); 
      int i; 
      for (i = 0; i < n; i++) 
      { 
         /* If we see an element again, then return false */
         if ( visited[arr[i] - min] != false ) 
           return false; 

         /* If visited first time, then mark the element as visited */
         visited[arr[i] - min] = true; 
      } 

      /* If all elements occur once, then return true */
      return true; 
  } 

  return false; // if (max - min  + 1 != n) 
} 

/* UTILITY FUNCTIONS */
int getMin(int arr[], int n) 
{ 
  int min = arr[0]; 
  for (int i = 1; i < n; i++) 
   if (arr[i] < min) 
     min = arr[i]; 
  return min; 
} 

int getMax(int arr[], int n) 
{ 
  int max = arr[0]; 
  for (int i = 1; i < n; i++) 
   if (arr[i] > max) 
     max = arr[i]; 
  return max; 
} 

/* Driver program to test above functions */
int main() 
{ 
    int arr[]= {5, 4, 2, 3, 1, 6}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    if(areConsecutive(arr, n) == true) 
        printf(" Array elements are consecutive "); 
    else
        printf(" Array elements are not consecutive "); 
    getchar(); 
    return 0; 
} 

```

## Java

```java

class AreConsecutive  
{ 
    /* The function checks if the array elements are consecutive 
       If elements are consecutive, then returns true, else returns 
       false */
    boolean areConsecutive(int arr[], int n)  
    { 
        if (n < 1) 
            return false; 

        /* 1) Get the minimum element in array */
        int min = getMin(arr, n); 

        /* 2) Get the maximum element in array */
        int max = getMax(arr, n); 

        /* 3) max - min + 1 is equal to n,  then only check all elements */
        if (max - min + 1 == n)  
        { 
            /* Create a temp array to hold visited flag of all elements. 
               Note that, calloc is used here so that all values are initialized  
               as false */
            boolean visited[] = new boolean[n]; 
            int i; 
            for (i = 0; i < n; i++)  
            { 
                /* If we see an element again, then return false */
                if (visited[arr[i] - min] != false) 
                    return false; 

                /* If visited first time, then mark the element as visited */
                visited[arr[i] - min] = true; 
            } 

            /* If all elements occur once, then return true */
            return true; 
        } 
        return false; // if (max - min  + 1 != n) 
    } 

    /* UTILITY FUNCTIONS */
    int getMin(int arr[], int n)  
    { 
        int min = arr[0]; 
        for (int i = 1; i < n; i++)  
        { 
            if (arr[i] < min) 
                min = arr[i]; 
        } 
        return min; 
    } 

    int getMax(int arr[], int n)  
    { 
        int max = arr[0]; 
        for (int i = 1; i < n; i++)  
        { 
            if (arr[i] > max) 
                max = arr[i]; 
        } 
        return max; 
    } 

    /* Driver program to test above functions */
    public static void main(String[] args)  
    { 
        AreConsecutive consecutive = new AreConsecutive(); 
        int arr[] = {5, 4, 2, 3, 1, 6}; 
        int n = arr.length; 
        if (consecutive.areConsecutive(arr, n) == true) 
            System.out.println("Array elements are consecutive"); 
        else
            System.out.println("Array elements are not consecutive"); 
    } 
} 

// This code has been contributed by Mayank Jaiswal 

```

## Python3

```py

# Helper functions to get Minimum and 
# Maximum in an array  

# The function checks if the array elements  
# are consecutive. If elements are consecutive,  
# then returns true, else returns false  
def areConsecutive(arr, n): 

    if ( n < 1 ): 
        return False

    # 1) Get the Minimum element in array */ 
    Min = min(arr) 

    # 2) Get the Maximum element in array */ 
    Max = max(arr) 

    # 3) Max - Min + 1 is equal to n,  
    # then only check all elements */ 
    if (Max - Min + 1 == n): 

        # Create a temp array to hold visited  
        # flag of all elements. Note that, calloc  
        # is used here so that all values are  
        # initialized as false 
        visited = [False for i in range(n)] 

        for i in range(n): 

            # If we see an element again,  
            # then return false */ 
            if (visited[arr[i] - Min] != False): 
                return False

            # If visited first time, then mark 
            # the element as visited */ 
            visited[arr[i] - Min] = True

        # If all elements occur once, 
        # then return true */ 
        return True

    return False # if (Max - Min + 1 != n) 

# Driver Code 
arr = [5, 4, 2, 3, 1, 6] 
n = len(arr) 
if(areConsecutive(arr, n) == True): 
    print("Array elements are consecutive ") 
else: 
    print("Array elements are not consecutive ") 

# This code is contributed by mohit kumar 

```

## C# 

```cs

using System; 

class GFG { 

    /* The function checks if the array elements 
    are consecutive If elements are consecutive, 
    then returns true, else returns    false */
    static bool areConsecutive(int []arr, int n)  
    { 
        if (n < 1) 
            return false; 

        /* 1) Get the minimum element in array */
        int min = getMin(arr, n); 

        /* 2) Get the maximum element in array */
        int max = getMax(arr, n); 

        /* 3) max - min + 1 is equal to n, then  
        only check all elements */
        if (max - min + 1 == n)  
        { 

            /* Create a temp array to hold visited 
            flag of all elements. Note that, calloc 
            is used here so that all values are 
            initialized as false */
            bool []visited = new bool[n]; 
            int i; 

            for (i = 0; i < n; i++)  
            { 

                /* If we see an element again, then 
                return false */
                if (visited[arr[i] - min] != false) 
                    return false; 

                /* If visited first time, then mark  
                the element as visited */
                visited[arr[i] - min] = true; 
            } 

            /* If all elements occur once, then 
            return true */
            return true; 
        } 
        return false; // if (max - min + 1 != n) 
    } 

    /* UTILITY FUNCTIONS */
    static int getMin(int []arr, int n)  
    { 
        int min = arr[0]; 

        for (int i = 1; i < n; i++)  
        { 
            if (arr[i] < min) 
                min = arr[i]; 
        } 

        return min; 
    } 

    static int getMax(int []arr, int n)  
    { 
        int max = arr[0]; 

        for (int i = 1; i < n; i++)  
        { 
            if (arr[i] > max) 
                max = arr[i]; 
        } 

        return max; 
    } 

    /* Driver program to test above functions */
    public static void Main()  
    { 
        int []arr = {5, 4, 2, 3, 1, 6}; 
        int n = arr.Length; 

        if (areConsecutive(arr, n) == true) 
            Console.Write("Array elements are"
                              + " consecutive"); 
        else
            Console.Write("Array elements are"
                         + " not consecutive"); 
    } 
} 

// This code is contributed by nitin mittal. 

```

## PHP

```php

<?php 
// PHP Program for above approach 

// The function checks if the array elements  
// are consecutive. If elements are consecutive,  
// then returns true, else returns false  
function areConsecutive($arr, $n)  
{  
    if ( $n < 1 )  
        return false;  

    // 1) Get the minimum element in array  
    $min = getMin($arr, $n);  

    // 2) Get the maximum element in array  
    $max = getMax($arr, $n);  

    // 3) $max - $min + 1 is equal to $n,  
    // then only check all elements  
    if ($max - $min + 1 == $n)  
    {  

        // Create a temp array to hold  
        // visited flag of all elements. 
        $visited = array();  
        for ($i = 0; $i < $n; $i++)  
        {  
            $visited[$i] = false;  
        }  
        for ($i = 0; $i < $n; $i++)  
        {  
            // If we see an element again,  
            // then return false  
            if ( $visited[$arr[$i] - $min] != false )  
            return false;  

            // If visited first time, then mark  
            // the element as visited 
            $visited[$arr[$i] - $min] = true;  
        }  

        // If all elements occur once,  
        // then return true  
        return true;  
    }  

    return false; // if ($max - $min + 1 != $n)  
}  

// UTILITY FUNCTIONS  
function getMin($arr, $n)  
{  
    $min = $arr[0];  
    for ($i = 1; $i < $n; $i++)  
        if ($arr[$i] < $min)  
            $min = $arr[$i];  
    return $min;  
}  

function getMax($arr, $n)  
{  
    $max = $arr[0];  
    for ($i = 1; $i < $n; $i++)  
        if ($arr[$i] > $max)  
            $max = $arr[$i];  
    return $max;  
}  

// Driver Code 
$arr = array(5, 4, 2, 3, 1, 6);  
$n = count($arr); 
if(areConsecutive($arr, $n) == true)  
    echo "Array elements are consecutive ";  
else
    echo "Array elements are not consecutive ";  

// This code is contributed by rathbhupendra 
?> 

```

**时间复杂度**：`O(n)`。

**额外空间**：`O(n)`。

**方法 3（将访问的数组元素标记为负）**：

此方法具有`O(n)`时间复杂度和`O(1)`额外空间，但是它更改了原始数组，并且仅当所有数字均为正。 我们可以通过添加一个额外的步骤来获得原始数组。 它是方法 2 的扩展，具有相同的两个步骤。

1.  `max-min + 1 = n`其中`max`是数组中的最大元素，`min`是数组中的最小元素，`n`是数组中的元素数。

2.  所有元素都是不同的。

在此方法中，步骤 2 的实现与方法 2 不同。我们没有创建新的数组，而是修改了输入数组`arr[]`来跟踪访问的元素。 这个想法是遍历数组，对于每个索引`i`（其中`0 ≤ i < n`），将`arr[arr[i] – min]]`设为负值。 如果我们再次看到负值，则说明存在重复。

## C++

```cpp
#include<stdio.h> 
#include<stdlib.h> 
  
/* Helper functions to get minimum and maximum in an array */
int getMin(int arr[], int n); 
int getMax(int arr[], int n); 
  
/* The function checks if the array elements are consecutive 
  If elements are consecutive, then returns true, else returns 
  false */
bool areConsecutive(int arr[], int n) 
{ 
  
    if ( n <  1 ) 
        return false; 
  
    /* 1) Get the minimum element in array */
    int min = getMin(arr, n); 
  
    /* 2) Get the maximum element in array */
    int max = getMax(arr, n); 
  
    /* 3) max - min + 1 is equal to n then only check all elements */
    if (max - min  + 1 == n) 
    { 
        int i; 
        for(i = 0; i < n; i++) 
        { 
            int j; 
  
            if (arr[i] < 0) 
                j = -arr[i] - min; 
            else
                j = arr[i] - min; 
  
            // if the value at index j is negative then 
            // there is repetition 
            if (arr[j] > 0) 
                arr[j] = -arr[j]; 
            else
                return false; 
        } 
  
        /* If we do not see a negative value then all elements 
           are distinct */
        return true; 
    } 
  
    return false; // if (max - min  + 1 != n) 
} 
  
/* UTILITY FUNCTIONS */
int getMin(int arr[], int n) 
{ 
    int min = arr[0]; 
    for (int i = 1; i < n; i++) 
        if (arr[i] < min) 
            min = arr[i]; 
    return min; 
} 
  
int getMax(int arr[], int n) 
{ 
    int max = arr[0]; 
    for (int i = 1; i < n; i++) 
        if (arr[i] > max) 
            max = arr[i]; 
    return max; 
} 
  
/* Driver program to test above functions */
int main() 
{ 
    int arr[]= {1, 4, 5, 3, 2, 6}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    if(areConsecutive(arr, n) == true) 
        printf(" Array elements are consecutive "); 
    else
        printf(" Array elements are not consecutive "); 
    getchar(); 
    return 0; 
}
```

## Java

```java
class AreConsecutive  
{ 
    /* The function checks if the array elements are consecutive 
       If elements are consecutive, then returns true, else returns 
       false */
    boolean areConsecutive(int arr[], int n)  
    { 
        if (n < 1) 
            return false; 
  
        /* 1) Get the minimum element in array */
        int min = getMin(arr, n); 
  
        /* 2) Get the maximum element in array */
        int max = getMax(arr, n); 
  
        /* 3) max-min+1 is equal to n then only check all elements */
        if (max - min + 1 == n)  
        { 
            int i; 
            for (i = 0; i < n; i++)  
            { 
                int j; 
  
                if (arr[i] < 0) 
                    j = -arr[i] - min; 
                else
                    j = arr[i] - min; 
  
                // if the value at index j is negative then 
                // there is repitition 
                if (arr[j] > 0)  
                    arr[j] = -arr[j]; 
                else
                    return false; 
            } 
  
            /* If we do not see a negative value then all elements 
               are distinct */
            return true; 
        } 
  
        return false; // if (max-min+1 != n) 
    } 
  
    /* UTILITY FUNCTIONS */
    int getMin(int arr[], int n)  
    { 
        int min = arr[0]; 
        for (int i = 1; i < n; i++)  
        { 
            if (arr[i] < min) 
                min = arr[i]; 
        } 
        return min; 
    } 
  
    int getMax(int arr[], int n)  
    { 
        int max = arr[0]; 
        for (int i = 1; i < n; i++)  
        { 
            if (arr[i] > max) 
                max = arr[i]; 
        } 
        return max; 
    } 
  
    /* Driver program to test above functions */
    public static void main(String[] args)  
    { 
        AreConsecutive consecutive = new AreConsecutive(); 
        int arr[] = {5, 4, 2, 3, 1, 6}; 
        int n = arr.length; 
        if (consecutive.areConsecutive(arr, n) == true) 
            System.out.println("Array elements are consecutive"); 
        else
            System.out.println("Array elements are not consecutive"); 
    } 
} 
  
// This code is contributed by Mayank Jaiswal
```

## Python 3

```
# Helper functions to get minimum and  
# maximum in an array  
  
# The function checks if the array  
# elements are consecutive. If elements  
# are consecutive, then returns true,  
# else returns false  
def areConsecutive(arr, n): 
  
    if ( n < 1 ): 
        return False
  
    # 1) Get the minimum element in array  
    min = getMin(arr, n) 
  
    # 2) Get the maximum element in array  
    max = getMax(arr, n) 
  
    # 3) max - min + 1 is equal to n  
    # then only check all elements  
    if (max - min + 1 == n): 
  
        for i in range(n): 
  
            if (arr[i] < 0): 
                j = -arr[i] - min
            else: 
                j = arr[i] - min
  
            # if the value at index j is negative  
            # then there is repetition 
            if (arr[j] > 0): 
                arr[j] = -arr[j] 
            else: 
                return False
  
        # If we do not see a negative value  
        # then all elements are distinct  
        return True
  
    return False     # if (max - min + 1 != n) 
  
# UTILITY FUNCTIONS  
def getMin(arr, n): 
      
    min = arr[0] 
    for i in range(1, n): 
        if (arr[i] < min): 
            min = arr[i] 
    return min
  
def getMax(arr, n): 
    max = arr[0] 
    for i in range(1, n): 
        if (arr[i] > max): 
            max = arr[i] 
    return max
  
# Driver Code 
if __name__ == "__main__": 
      
    arr = [1, 4, 5, 3, 2, 6] 
    n = len(arr) 
    if(areConsecutive(arr, n) == True): 
        print(" Array elements are consecutive ") 
    else: 
        print(" Array elements are not consecutive ") 
  
# This code is contributed by ita_c
```

## C#

```cs
using System; 
  
class GFG { 
      
    /* The function checks if the array  
    elements are consecutive If elements 
    are consecutive, then returns true,  
    else returns false */
    static bool areConsecutive(int []arr, int n)  
    { 
        if (n < 1) 
            return false; 
  
        /* 1) Get the minimum element in 
        array */
        int min = getMin(arr, n); 
  
        /* 2) Get the maximum element in 
        array */
        int max = getMax(arr, n); 
  
        /* 3) max-min+1 is equal to n then 
        only check all elements */
        if (max - min + 1 == n)  
        { 
            int i; 
            for (i = 0; i < n; i++)  
            { 
                int j; 
  
                if (arr[i] < 0) 
                    j = -arr[i] - min; 
                else
                    j = arr[i] - min; 
  
                // if the value at index j 
                // is negative then 
                // there is repitition 
                if (arr[j] > 0)  
                    arr[j] = -arr[j]; 
                else
                    return false; 
            } 
  
            /* If we do not see a negative  
            value then all elements 
            are distinct */
            return true; 
        } 
  
        // if (max-min+1 != n) 
        return false;  
    } 
  
    /* UTILITY FUNCTIONS */
    static int getMin(int []arr, int n)  
    { 
        int min = arr[0]; 
        for (int i = 1; i < n; i++)  
        { 
            if (arr[i] < min) 
                min = arr[i]; 
        } 
        return min; 
    } 
  
    static int getMax(int []arr, int n)  
    { 
        int max = arr[0]; 
        for (int i = 1; i < n; i++)  
        { 
            if (arr[i] > max) 
                max = arr[i]; 
        } 
        return max; 
    } 
  
    /* Driver program to test above 
    functions */
    public static void Main()  
    { 
        int []arr = {5, 4, 2, 3, 1, 6}; 
        int n = arr.Length; 
          
        if (areConsecutive(arr, n) == true) 
            Console.Write("Array elements "
                      + "are consecutive"); 
        else
            Console.Write("Array elements "
                  + "are not consecutive"); 
    } 
} 
  
// This code is contributed by nitin mittal.
```

## PHP

```php
<?php 
  
/* The function checks if the array elements 
are consecutive If elements are consecutive, 
then returns true, else returns false */
function areConsecutive( $arr, $n) 
{ 
  
    if ( $n < 1 ) 
        return false; 
  
    /* 1) Get the minimum element in array */
    $min = getMin($arr, $n); 
  
    /* 2) Get the maximum element in array */
    $max = getMax($arr, $n); 
  
    /* 3) max - min + 1 is equal to n then  
          only check all elements */
    if ($max - $min + 1 == $n) 
    { 
    $i; 
        for($i = 0; $i < $n; $i++) 
        { 
            $j; 
  
            if ($arr[$i] < 0) 
                $j = -$arr[$i] - $min; 
            else
                $j = $arr[$i] - $min; 
  
            // if the value at index j is 
            // negative then there is 
            // repetition 
            if ($arr[$j] > 0) 
                $arr[$j] = -$arr[$j]; 
            else
                return false; 
        } 
  
        /* If we do not see a negative value 
        then all elements are distinct */
        return true; 
    } 
  
    return false; // if (max - min + 1 != n) 
} 
  
/* UTILITY FUNCTIONS */
function getMin( $arr, $n) 
{ 
    $min = $arr[0]; 
    for ( $i = 1; $i < $n; $i++) 
        if ($arr[$i] < $min) 
            $min = $arr[$i]; 
    return $min; 
} 
  
function getMax( $arr, $n) 
{ 
    $max = $arr[0]; 
    for ( $i = 1; $i < $n; $i++) 
        if ($arr[$i] > $max) 
            $max = $arr[$i]; 
    return $max; 
} 
  
/* Driver program to test above functions */
    $arr= array(1, 4, 5, 3, 2, 6); 
    $n = count($arr); 
    if(areConsecutive($arr, $n) == true) 
        echo " Array elements are consecutive "; 
    else
        echo " Array elements are not consecutive "; 
  
  
// This code is contributed by anuj_67. 
?>
```

请注意，此方法可能不适用于负数。 例如，它为`{2, 1, 0, -3, -1, -2}`返回`false`。

时间复杂度：`O(n)`。

额外空间：`O(1)`。