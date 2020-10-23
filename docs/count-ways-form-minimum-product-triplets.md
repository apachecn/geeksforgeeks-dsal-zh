# 计算构成最小乘积三元组的方法数量

> 原文： [https://www.geeksforgeeks.org/count-ways-form-minimum-product-triplets/](https://www.geeksforgeeks.org/count-ways-form-minimum-product-triplets/)

给定一个正整数数组。 我们需要找出索引`(i, j, k) (i < j < k)`的三元组，以使`a[i] * a[j] * a[k]`最小。

```
Examples:
Input : 5
        1 3 2 3 4
Output : 2
The triplets are (1, 3, 2)
and (1, 2, 3)

Input : 5
        2 2 2 2 2
Output : 5
In this example we choose three 2s 
out of five, and the number of ways 
to choose them is 5C3.

Input : 6
        1 3 3 1 3 2
Output : 1
There is only one way (1, 1, 2).

```



在此问题中出现以下情况。

1.  所有三个最小元素都相同。 例如`{1, 1, 1, 1, 2, 2, 3, 4}`。 对于这种情况的解决方案是`C(n, 3)`。

2.  两个元素是相同的。 例如`{1, 2, 2, 2, 3}`或`{1, 1, 2, 2}`。 在这种情况下，第一个（或最小元素）的出现次数不能超过 2。如果最小元素出现两次，则答案是第二个元素的计数（我们从第二个元素的所有出现中仅选择 1 个。如果最小元素出现一次，计数为`C(n, 2)`。

3.  这三个要素都是截然不同的。 例如`{1, 2, 3, 3, 5}`。 在这种情况下，答案是第三元素（或`C(n, 1)`）的出现次数。

我们首先按升序对数组进行排序。 然后从开始计算第 3 元素的 3 元素的频率。 假设频率为`count`。 出现以下情况。

*   如果第三个元素等于第一个元素，则否。 三元组的数量为`(count-2) * (count-1) * count / 6`，其中`count`是第 3 个元素的频率。

*   如果第三个元素等于第二个元素，则否。 三元组将为`(count-1) * count / 2`。 否则没有。 三元组将是计数值。

## C++ 

```cpp

// CPP program to count number of ways we can 
// form triplets with minimum product. 
#include <bits/stdc++.h> 
using namespace std; 

// function to calculate number of triples 
long long noOfTriples(long long arr[], int n) 
{ 
    // Sort the array 
    sort(arr, arr + n); 

    // Count occurrences of third element 
    long long count = 0; 
    for (long long i = 0; i < n; i++)  
        if (arr[i] == arr[2]) 
            count++; 

    // If all three elements are same (minimum 
    // element appears at least 3 times). Answer 
    // is nC3\. 
    if (arr[0] == arr[2]) 
        return (count - 2) * (count - 1) * (count) / 6; 

    // If minimum element appears once.   
    // Answer is nC2\. 
    else if (arr[1] == arr[2]) 
        return (count - 1) * (count) / 2; 

    // Minimum two elements are distinct. 
    // Answer is nC1\. 
    return count; 
} 

// Driver code 
int main() 
{ 
    long long arr[] = { 1, 3, 3, 4 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    cout << noOfTriples(arr, n); 
    return 0; 
} 

```

## Java

```java

// Java program to count number of ways we can 
// form triplets with minimum product. 
import java.util.Arrays; 

class GFG { 

    // function to calculate number of triples 
    static long noOfTriples(long arr[], int n) 
    { 

        // Sort the array 
        Arrays.sort(arr); 

        // Count occurrences of third element 
        long count = 0; 
        for (int i = 0; i < n; i++)  
            if (arr[i] == arr[2]) 
                count++; 

        // If all three elements are same (minimum 
        // element appears at least 3 times). Answer 
        // is nC3\. 
        if (arr[0] == arr[2]) 
            return (count - 2) * (count - 1) *  
                                      (count) / 6; 

        // If minimum element appears once.  
        // Answer is nC2\. 
        else if (arr[1] == arr[2]) 
            return (count - 1) * (count) / 2; 

        // Minimum two elements are distinct. 
        // Answer is nC1\. 
        return count; 
    } 

    //driver code 
    public static void main(String arg[]) 
    { 

        long arr[] = { 1, 3, 3, 4 }; 
        int n = arr.length; 

        System.out.print(noOfTriples(arr, n)); 
    } 
} 

// This code is contributed by Anant Agarwal. 

```

## Python3

```py

# Python3 program to count number 
# of ways we can form triplets  
# with minimum product. 

# function to calculate number of triples 
def noOfTriples (arr, n): 

    # Sort the array 
    arr.sort() 

    # Count occurrences of third element 
    count = 0
    for i in range(n): 
        if arr[i] == arr[2]: 
            count+=1

    # If all three elements are same  
    # (minimum element appears at l 
    # east 3 times). Answer is nC3\. 
    if arr[0] == arr[2]: 
        return (count - 2) * (count - 1) * (count) / 6

    # If minimum element appears once. 
    # Answer is nC2\. 
    elif arr[1] == arr[2]: 
        return (count - 1) * (count) / 2

    # Minimum two elements are distinct. 
    # Answer is nC1\. 
    return count 

# Driver code 
arr = [1, 3, 3, 4] 
n = len(arr) 
print (noOfTriples(arr, n)) 

# This code is contributed by "Abhishek Sharma 44" 

```

## C# 

```cs

// C# program to count number of ways 
// we can form triplets with minimum product. 
using System; 

class GFG { 

// function to calculate number of triples 
static long noOfTriples(long []arr, int n) 
{ 
    // Sort the array 
    Array.Sort(arr); 

    // Count occurrences of third element 
    long count = 0; 
    for (int i = 0; i < n; i++)  
        if (arr[i] == arr[2]) 
            count++; 

    // If all three elements are same (minimum 
    // element appears at least 3 times). Answer 
    // is nC3\. 
    if (arr[0] == arr[2]) 
        return (count - 2) * (count - 1) * (count) / 6; 

    // If minimum element appears once.   
    // Answer is nC2\. 
    else if (arr[1] == arr[2]) 
        return (count - 1) * (count) / 2; 

    // Minimum two elements are distinct. 
    // Answer is nC1\. 
    return count; 
} 

//driver code 
public static void Main() 
{ 
    long []arr = { 1, 3, 3, 4 }; 
    int n = arr.Length; 
    Console.Write(noOfTriples(arr, n)); 
} 
} 

//This code is contributed by Anant Agarwal. 

```

## PHP

```php

<?php 
// PHP program to count number of ways  
// we can form triplets with minimum 
// product. 

// function to calculate number of 
// triples 
function noOfTriples( $arr, $n) 
{ 
    // Sort the array 
    sort($arr); 

    // Count occurrences of third element 
    $count = 0; 
    for ( $i = 0; $i < $n; $i++)  
        if ($arr[$i] == $arr[2]) 
            $count++; 

    // If all three elements are same  
    // (minimum element appears at least  
    // 3 times). Answer is nC3\. 
    if ($arr[0] == $arr[2]) 
        return ($count - 2) * ($count - 1)   
                           * ($count) / 6; 

    // If minimum element appears once.  
    // Answer is nC2\. 
    else if ($arr[1] == $arr[2]) 
        return ($count - 1) * ($count) / 2; 

    // Minimum two elements are distinct. 
    // Answer is nC1\. 
    return $count; 
} 

// Driver code 
    $arr = array( 1, 3, 3, 4 ); 
    $n = count($arr); 
    echo noOfTriples($arr, $n); 

// This code is contributed by anuj_67\. 
?> 

```

Output:

```
1

```

时间复杂度：`O(N log N)`。

可以通过首先找到最小元素及其频率，如果频率小于 3，然后找到第二小值及其频率，来优化解决方案。 如果总频率小于 3，则找到第三小值及其频率。 此优化解决方案的时间复杂度为`O(n)`。



