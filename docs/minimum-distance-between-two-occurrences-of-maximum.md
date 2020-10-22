# 最大值的两次出现之间的最小距离

> 原文： [https://www.geeksforgeeks.org/minimum-distance-between-two-occurrences-of-maximum/](https://www.geeksforgeeks.org/minimum-distance-between-two-occurrences-of-maximum/)

您将获得一个`n`元素数组，其基本条件是最大元素的出现不止一次。 您必须找到最大值之间的最小距离。 （`n > = 2`）。

例子：

```
Input : arr[] = {3, 5, 2, 3, 5, 3, 5}
Output : Minimum Distance = 2
Explanation : Greatest element is 5 and its index 
are 1, 4 and 6\. Resulting minimum distance of 2 
from position 4 to 6.

Input : arr[] = {1, 1, 1, 1, 1, 1}
Output : Minimum Distance = 1
Explanation : Greatest element is 1 and its index 
are 0, 1, 2, 3, 4 and 5\. Resulting minimum distance
of 1.

```



**基本方法**在 `O(n^2)`中运行。 首先，我们找到最大元素。 然后，对于等于最大元素的每个元素，我们找到最接近的最大元素。

一个有效的**解决方案**在数组的单个遍历中完成了我们的工作。 我们初始化`maximum_element = arr[0]`，`min_distance = n`和`index = 0`。之后，对于每个元素，我们应检查元素是否等于，大于或小于最大元素。 根据三种情况，我们有以下选择：

*   **情况 a**：如果`element`等于`maximum_element`，则更新`min_dis = min(min_dis,  i-index)`并更新`index = i`；

*   **情况 b**：如果元素大于`maximum_element`，则更新`maximum_element = arr[i]`，`index = i`，`min_dis = n`。

*   **情况 c**：如果`element`小于`maximum_element`，则迭代到下一个元素。

## C

```c

// C program to find Min distance  
// of maximum element 
#include<bits/stdc++.h> 
using namespace std; 

//function to return min distance 
int minDistance (int arr[], int n) 
{ 
    int maximum_element = arr[0]; 
    int min_dis = n; 
    int index = 0; 

    for (int i=1; i<n; i++) 
    { 
        // case a 
        if (maximum_element == arr[i]) 
        { 
            min_dis = min(min_dis, (i-index)); 
            index = i; 
        } 

        // case b 
        else if (maximum_element < arr[i]) 
        { 
            maximum_element = arr[i]; 
            min_dis = n; 
            index = i; 
        } 

        // case c 
        else
            continue; 
    } 

    return min_dis; 
} 

// driver program 
int main() 
{ 
    int arr[] = {6, 3, 1, 3, 6, 4, 6}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    cout << "Minimum distance = " 
         << minDistance(arr, n); 
    return 0; 
}  

```

## Java

```java

// Java program to find Min distance  
// of maximum element 
class GFG  
{ 

    // function to return min distance 
    static int minDistance (int arr[], int n) 
    { 
        int maximum_element = arr[0]; 
        int min_dis = n; 
        int index = 0; 

        for (int i=1; i<n; i++) 
        { 

            // case a 
            if (maximum_element == arr[i]) 
            { 
                min_dis = Math.min(min_dis, (i-index)); 
                index = i; 
            } 

            // case b 
            else if (maximum_element < arr[i]) 
            { 
                maximum_element = arr[i]; 
                min_dis = n; 
                index = i; 
            } 

            // case c 
            else
                continue; 
        } 

        return min_dis; 
    } 

    // Driver code 
    public static void main (String[] args) 
    { 
        int arr[] = {6, 3, 1, 3, 6, 4, 6}; 
        int n = arr.length; 
        System.out.print("Minimum distance = "+minDistance(arr, n)); 
    } 
} 

// This code is contributed by Anant Agarwal. 

```

## Python3

```py

# Python3 program to find Min  
# distance of maximum element 

# Function to return min distance 
def minDistance (arr, n): 

    maximum_element = arr[0] 
    min_dis = n 
    index = 0

    for i in range(1, n): 

        # case a 
        if (maximum_element == arr[i]): 

            min_dis = min(min_dis, (i - index)) 
            index = i 

        # case b 
        elif (maximum_element < arr[i]): 

            maximum_element = arr[i] 
            min_dis = n 
            index = i 

        # case c 
        else: 
            continue

    return min_dis 

# driver program 
arr = [6, 3, 1, 3, 6, 4, 6] 
n = len(arr) 
print("Minimum distance =", minDistance(arr, n)) 

# This code is contributed by Smitha Dinesh Semwal 

```

## C# 

```cs

// C# program to find Min distance  
// of maximum element 
using System; 

class GFG { 

    // function to return min distance 
    static int minDistance (int []arr, int n) 
    { 
        int maximum_element = arr[0]; 
        int min_dis = n; 
        int index = 0; 

        for (int i = 1; i < n; i++) 
        { 

            // case a 
            if (maximum_element == arr[i]) 
            { 
                min_dis = Math.Min(min_dis,  
                                (i - index)); 
                index = i; 
            } 

            // case b 
            else if (maximum_element < arr[i]) 
            { 
                maximum_element = arr[i]; 
                min_dis = n; 
                index = i; 
            } 

            // case c 
            else
                continue; 
        } 

        return min_dis; 
    } 

    // Driver code 
    public static void Main () 
    { 
        int []arr = {6, 3, 1, 3, 6, 4, 6}; 
        int n = arr.Length; 

        Console.WriteLine("Minimum distance = "
                        + minDistance(arr, n)); 
    } 
} 

// This code is contributed by vt_m. 

```

## PHP

```php

<?php 
// PHP program to find Min distance  
// of maximum element 

//function to return min distance 
function minDistance($arr, $n) 
{ 
    $maximum_element = $arr[0]; 
    $min_dis = $n; 
    $index = 0; 

    for ($i = 1; $i < $n; $i++) 
    { 

        // case a 
        if ($maximum_element == $arr[$i]) 
        { 
            $min_dis = min($min_dis, ($i - $index)); 
            $index = $i; 
        } 

        // case b 
        else if ($maximum_element < $arr[$i]) 
        { 
            $maximum_element = $arr[$i]; 
            $min_dis = $n; 
            $index = $i; 
        } 

        // case c 
        else
            continue; 
    } 

return $min_dis; 
} 

    // Driver Code 
    $arr = array(6, 3, 1, 3, 6, 4, 6); 
    $n = count($arr); 
    echo "Minimum distance = "
          .minDistance($arr,$n);  

// This code is contributed by Sam007 
?> 

```

Output :

```
Minimum distance = 2
```



* * *

* * *



