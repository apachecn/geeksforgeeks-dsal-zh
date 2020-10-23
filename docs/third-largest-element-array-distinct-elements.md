# 一系列不同元素中的第三大元素

> 原文： [https://www.geeksforgeeks.org/third-largest-element-array-distinct-elements/](https://www.geeksforgeeks.org/third-largest-element-array-distinct-elements/)

给定`n`个整数数组，找到第三大元素。 数组中的所有元素都是不同的整数。

**示例**：

```
Input: arr[] = {1, 14, 2, 16, 10, 20}
Output: The third Largest element is 14

Explanation: Largest element is 20, second largest element is 16 
and third largest element is 14

Input: arr[] = {19, -10, 20, 14, 2, 16, 10}
Output: The third Largest element is 16

Explanation: Largest element is 20, second largest element is 19 
and third largest element is 16

```



**朴素的方法**：任务是首先找到最大的元素，然后找到第二大的元素，然后将它们都排除，找到第三大的元素。 基本思想是对数组进行两次迭代，标记最大和第二大元素，然后将它们排除在外，同时找到第三最大元素，即不包括最大和第二大的最大元素。

*   **算法**：

    1.  首先，遍历数组并找到最大值。

    2.  将其与索引一起存储为第一大值。

    3.  现在遍历整个数组，找到第二大值，不包括最大值元素。

    4.  最后第三次遍历数组，找到第三大元素，即不包括最大值和第二大值。

*   ## C++ 

    ```

    // C++ program to find third Largest 
    // element in an array of distinct elements 
    #include <bits/stdc++.h> 

    void thirdLargest(int arr[], int arr_size) 
    { 
        /* There should be atleast three elements */
        if (arr_size < 3) 
        { 
            printf(" Invalid Input "); 
            return; 
        } 

        // Find first largest element 
        int first = arr[0]; 
        for (int i = 1; i < arr_size ; i++) 
            if (arr[i] > first) 
                first = arr[i]; 

        // Find second largest element 
        int second = INT_MIN; 
        for (int i = 0; i < arr_size ; i++) 
            if (arr[i] > second && arr[i] < first) 
                second = arr[i]; 

        // Find third largest element 
        int third = INT_MIN; 
        for (int i = 0; i < arr_size ; i++) 
            if (arr[i] > third && arr[i] < second) 
                third = arr[i]; 

        printf("The third Largest element is %d\n", third); 
    } 

    /* Driver program to test above function */
    int main() 
    { 
        int arr[] = {12, 13, 1, 10, 34, 16}; 
        int n = sizeof(arr)/sizeof(arr[0]); 
        thirdLargest(arr, n); 
        return 0; 
    } 

    ```

    ## Java

    ```

    // Java program to find third  
    // Largest element in an array 
    // of distinct elements 

    class GFG 
    { 
    static void thirdLargest(int arr[], 
                             int arr_size) 
    { 
        /* There should be  
        atleast three elements */
        if (arr_size < 3) 
        { 
            System.out.printf(" Invalid Input "); 
            return; 
        } 

        // Find first  
        // largest element 
        int first = arr[0]; 
        for (int i = 1; 
                 i < arr_size ; i++) 
            if (arr[i] > first) 
                first = arr[i]; 

        // Find second  
        // largest element 
        int second = Integer.MIN_VALUE; 
        for (int i = 0;  
                 i < arr_size ; i++) 
            if (arr[i] > second &&  
                arr[i] < first) 
                second = arr[i]; 

        // Find third 
        // largest element 
        int third = Integer.MIN_VALUE; 
        for (int i = 0;  
                 i < arr_size ; i++) 
            if (arr[i] > third &&  
                arr[i] < second) 
                third = arr[i]; 

        System.out.printf("The third Largest " +  
                      "element is %d\n", third); 
    } 

    // Driver code 
    public static void main(String []args) 
    { 
        int arr[] = {12, 13, 1,  
                     10, 34, 16}; 
        int n = arr.length; 
        thirdLargest(arr, n); 
    } 
    } 

    // This code is contributed 
    // by Smitha 

    ```

    ## Python3

    ```

    # Python 3 program to find  
    # third Largest element in  
    # an array of distinct elements 
    import sys 
    def thirdLargest(arr, arr_size): 

        # There should be  
        # atleast three elements  
        if (arr_size < 3): 

            print(" Invalid Input ") 
            return

        # Find first  
        # largest element 
        first = arr[0] 
        for i in range(1, arr_size): 
            if (arr[i] > first): 
                first = arr[i] 

        # Find second 
        # largest element 
        second = -sys.maxsize 
        for i in range(0, arr_size): 
            if (arr[i] > second and 
                arr[i] < first): 
                second = arr[i] 

        # Find third  
        # largest element 
        third = -sys.maxsize 
        for i in range(0, arr_size): 
            if (arr[i] > third and
                arr[i] < second): 
                third = arr[i] 

        print("The Third Largest",  
              "element is", third) 

    # Driver Code 
    arr = [12, 13, 1,  
           10, 34, 16] 
    n = len(arr) 
    thirdLargest(arr, n) 

    # This code is contributed  
    # by Smitha 

    ```

    ## C# 

    ```

    // C# program to find third  
    // Largest element in an array  
    // of distinct elements 
    using System; 

    class GFG 
    { 
    static void thirdLargest(int []arr, 
                             int arr_size) 
    { 
        /* There should be  
        atleast three elements */
        if (arr_size < 3) 
        { 
            Console.Write(" Invalid Input "); 
            return; 
        } 

        // Find first  
        // largest element 
        int first = arr[0]; 
        for (int i = 1; 
                 i < arr_size ; i++) 
            if (arr[i] > first) 
                first = arr[i]; 

        // Find second 
        // largest element 
        int second = -int.MaxValue; 
        for (int i = 0;  
                 i < arr_size ; i++) 
            if (arr[i] > second &&  
                arr[i] < first) 
                second = arr[i]; 

        // Find third  
        // largest element 
        int third = -int.MaxValue; 
        for (int i = 0; 
                 i < arr_size ; i++) 
            if (arr[i] > third &&  
                arr[i] < second) 
                third = arr[i]; 

        Console.Write("The third Largest " +  
                      "element is "+ third); 
    } 

    // Driver code 
    public static void Main() 
    { 
        int []arr = {12, 13, 1,      
                     10, 34, 16}; 
        int n = arr.Length; 
        thirdLargest(arr, n); 
    } 
    } 

    // This code is contributed by Smitha 

    ```

    ## PHP

    ```

    <?php 
    // PHP program to find third  
    // Largest element in an array 
    // of distinct elements 

    function thirdLargest($arr, $arr_size) 
    { 
        /* There should be atleast 
        three elements */
        if ($arr_size < 3) 
        { 
            echo " Invalid Input "; 
            return; 
        } 

        // Find first largest element 
        $first = $arr[0]; 
        for ($i = 1; $i < $arr_size ; $i++) 
            if ($arr[$i] > $first) 
                $first = $arr[$i]; 

        // Find second largest element 
        $second = PHP_INT_MIN; 
        for ($i = 0; $i < $arr_size ; $i++) 
            if ($arr[$i] > $second &&  
                   $arr[$i] < $first) 
                $second = $arr[$i]; 

        // Find third largest element 
        $third = PHP_INT_MIN; 
        for ($i = 0; $i < $arr_size ; $i++) 
            if ($arr[$i] > $third &&  
                  $arr[$i] < $second) 
                $third = $arr[$i]; 

        echo "The third Largest element is ",  
                                 $third,"\n"; 
    } 

    // Driver Code 
    $arr = array(12, 13, 1,  
                 10, 34, 16); 
    $n = sizeof($arr); 
    thirdLargest($arr, $n); 

    // This code is contributed by m_kit 
    ?> 

    ```

*   **输出**：

    ```
    The third Largest element is 13
    ```

*   **复杂度分析**：

    *   **时间复杂度**：`O(n)`。

        由于数组要重复三次并在固定时间内完成。

    *   **空间复杂度**：`O(1)`。

        不需要多余的空间，因为索引可以存储在恒定空间中。

**有效方法**：该问题涉及在单个遍历中查找数组中的第三大元素。 可以借助类似的问题[找到第二大元素](https://www.geeksforgeeks.org/find-second-largest-element-array/)来破解该问题。 因此，想法是从头到尾遍历数组，并跟踪直到该索引（存储在变量中）的三个最大元素。 因此，遍历整个数组后，变量将存储数组的三个最大元素的索引（或值）。

*   **算法**：

    1.  创建三个变量，`first`，`second`，`third`，以存储数组中三个最大元素的索引。 （最初将它们全部初始化为最小值）。

    2.  沿着输入数组从头到尾移动。

    3.  对于每个索引，请先检查元素是否大于`first`，然后再大于`second`和`third`。 如果元素较大，则首先更新`first`的值，然后将`first`分配给`second`，将`second`分配给`third`。 因此，最大的元素将被更新，以前存储为最大的元素将成为第二大元素，第二大的元素将成为第三大元素。

    4.  否则，如果元素大于`second`，则更新`second`的值，第二大元素变为第三大元素。

    5.  如果前两个条件失败，但是元素大于`third`，则更新`third`。

    6.  从头到尾遍历数组后，打印`third`值。

*   ## C++ 

```cpp

// C++ program to find third  
// Largest element in an array 
#include <bits/stdc++.h> 

void thirdLargest(int arr[], int arr_size) 
{ 
    /* There should be atleast three elements */
    if (arr_size < 3) 
    { 
        printf(" Invalid Input "); 
        return; 
    } 

    // Initialize first, second and third Largest element 
    int first = arr[0], second = INT_MIN, third = INT_MIN; 

    // Traverse array elements to find the third Largest 
    for (int i = 1; i < arr_size ; i ++) 
    { 
        /* If current element is greater than first, 
           then update first, second and third */
        if (arr[i] > first) 
        { 
            third  = second; 
            second = first; 
            first  = arr[i]; 
        } 

        /* If arr[i] is in between first and second */
        else if (arr[i] > second) 
        { 
            third = second; 
            second = arr[i]; 
        } 

        /* If arr[i] is in between second and third */
        else if (arr[i] > third) 
            third = arr[i]; 
    } 

    printf("The third Largest element is %d\n", third); 
} 

/* Driver program to test above function */
int main() 
{ 
    int arr[] = {12, 13, 1, 10, 34, 16}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    thirdLargest(arr, n); 
    return 0; 
} 

```

## Java

```java
// Java program to find third Largest element in an array 
class GFG { 
  
    static void thirdLargest(int arr[], int arr_size) { 
        /* There should be atleast three elements */
        if (arr_size < 3) { 
            System.out.printf(" Invalid Input "); 
            return; 
        } 
  
        // Initialize first, second and third Largest element 
        int first = arr[0], second = Integer.MIN_VALUE, 
                            third = Integer.MIN_VALUE; 
  
        // Traverse array elements to find the third Largest 
        for (int i = 1; i < arr_size; i++) { 
            /* If current element is greater than first, 
        then update first, second and third */
            if (arr[i] > first) { 
                third = second; 
                second = first; 
                first = arr[i]; 
            } /* If arr[i] is in between first and second */
            else if (arr[i] > second) { 
                third = second; 
                second = arr[i]; 
            } /* If arr[i] is in between second and third */
            else if (arr[i] > third) { 
                third = arr[i]; 
            } 
        } 
  
        System.out.printf("The third Largest element is %d\n", third); 
    } 
  
    /* Driver program to test above function */
    public static void main(String []args) { 
        int arr[] = {12, 13, 1, 10, 34, 16}; 
        int n = arr.length; 
        thirdLargest(arr, n); 
    } 
} 
//This code is contributed by 29AjayKumar
```

## Python3

```py
# Python3 program to find  
# third Largest element in  
# an array 
import sys 
def thirdLargest(arr, arr_size): 
  
    # There should be  
    # atleast three elements  
    if (arr_size < 3): 
      
        print(" Invalid Input ") 
        return
      
    # Initialize first, second 
    # and third Largest element 
    first = arr[0] 
    second = -sys.maxsize 
    third = -sys.maxsize 
  
    # Traverse array elements 
    # to find the third Largest 
    for i in range(1, arr_size): 
      
        # If current element is 
        # greater than first, 
        # then update first,  
        # second and third  
        if (arr[i] > first): 
          
            third = second 
            second = first 
            first = arr[i] 
          
  
        # If arr[i] is in between  
        # first and second  
        elif (arr[i] > second): 
          
            third = second 
            second = arr[i] 
          
        # If arr[i] is in between 
        # second and third  
        elif (arr[i] > third): 
            third = arr[i] 
      
    print("The third Largest" ,  
                  "element is", third) 
  
# Driver Code 
arr = [12, 13, 1, 
       10, 34, 16] 
n = len(arr) 
thirdLargest(arr, n) 
  
# This code is contributed 
# by Smitha
```

## C#

```cs
// C# program to find third Largest element in an array 
using System; 
class GFG { 
  
static void thirdLargest(int[] arr, int arr_size)  
{ 
    /* There should be atleast three elements */
    if (arr_size < 3) 
    { 
        Console.Write(" Invalid Input "); 
        return; 
          
    } 
  
    // Initialize first, second and third Largest element 
    int first = arr[0], second = int.MinValue, 
                            third = int.MinValue; 
  
    // Traverse array elements to find the third Largest 
    for (int i = 1; i < arr_size; i++)  
    { 
        /* If current element is greater than first, 
        then update first, second and third */
        if (arr[i] > first) { 
            third = second; 
            second = first; 
            first = arr[i]; 
        } 
          
        /* If arr[i] is in between first and second */
        else if (arr[i] > second) { 
            third = second; 
            second = arr[i]; 
        }  
        /* If arr[i] is in between second and third */
        else if (arr[i] > third) { 
            third = arr[i]; 
        } 
    } 
  
    Console.Write("The third Largest element is "+ third); 
} 
  
/* Driver program to test above function */
public static void Main() { 
        int[] arr = {12, 13, 1, 10, 34, 16}; 
        int n = arr.Length; 
        thirdLargest(arr, n); 
    } 
} 
  
// This code is contributed 
// by Ita_c
```

## PHP

```php
<?php 
// PHP program to find third  
// Largest element in an array 
  
function thirdLargest($arr, $arr_size) 
{ 
    /* There should be atleast 
       three elements */
    if ($arr_size < 3) 
    { 
        echo " Invalid Input "; 
        return; 
    } 
  
    // Initialize first, second and  
    // third Largest element 
    $first = $arr[0];  
    $second = PHP_INT_MIN; 
    $third = PHP_INT_MIN; 
  
    // Traverse array elements to 
    // find the third Largest 
    for ($i = 1; $i < $arr_size ; $i ++) 
    { 
        /* If current element is greater  
        than first, then update first,  
        second and third */
        if ($arr[$i] > $first) 
        { 
            $third = $second; 
            $second = $first; 
            $first = $arr[$i]; 
        } 
  
        /* If arr[i] is in between 
        first and second */
        else if ($arr[$i] > $second) 
        { 
            $third = $second; 
            $second = $arr[$i]; 
        } 
  
        /* If arr[i] is in between 
        second and third */
        else if ($arr[$i] > $third) 
            $third = $arr[$i]; 
    } 
  
    echo "The third Largest element is ",  
                                  $third; 
} 
  
// Driver Code 
$arr = array (12, 13, 1,  
              10, 34, 16); 
$n = sizeof($arr); 
thirdLargest($arr, $n); 
  
// This code is contributed by jit_t 
?>
```

输出：

```
The third Largest element is 13
```

复杂度分析：

+   时间复杂度：`O(n)`。
    
    由于数组要重复三次，并且要在固定时间内完成
+   空间复杂度：`O(1)`。
    
    由于索引可以存储在恒定空间中，因此不需要额外的空间。

练习题：扩展上述解决方案以在数组可能具有重复项时找到第三大解决方案。 例如，如果输入数组为`{10, 5, 15, 5, 15, 10, 1, 1}`，则输出应为 5。扩展解也应一次遍历。