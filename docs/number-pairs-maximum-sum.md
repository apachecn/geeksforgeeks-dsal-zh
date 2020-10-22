# 最大和的对数

> 原文： [https://www.geeksforgeeks.org/number-pairs-maximum-sum/](https://www.geeksforgeeks.org/number-pairs-maximum-sum/)

给定一个数组`arr[]`，计算`arr[i]`，`arr[j]`对的数目，使`arr[i] + arr[j]`最大，且`i < j`。

```
Example :
Input  : arr[] = {1, 1, 1, 2, 2, 2}
Output : 3
Explanation: The maximum possible pair 
sum where i<j is  4, which is given 
by 3 pairs, so the answer is 3
the pairs are (2, 2), (2, 2) and (2, 2)

Input  : arr[] = {1, 4, 3, 3, 5, 1}
Output : 1
Explanation: The pair 4, 5 yields the 
maximum sum i.e, 9 which is given by 1 pair only

```



**方法 1（朴素）**：

从 0 到`n`遍历一个循环`i`，即数组的长度，从`i + 1`到`n`遍历另一个循环`j`，以找到`i < j`的所有可能的对。 找到具有最大可能总和的当前对，再次遍历所有当前对，并保持当前对数量的计数，这使当前对总和等于最大值。

## C++ 

```cpp

// CPP program to count pairs with maximum sum. 
#include <bits/stdc++.h> 
using namespace std; 

// function to find the number of maximum pair sums 
int sum(int a[], int n) 
{ 
    // traverse through all the pairs 
    int maxSum = INT_MIN; 
    for (int i = 0; i < n; i++) 
        for (int j = i + 1; j < n; j++) 
            maxSum = max(maxSum, a[i] + a[j]); 

    // traverse through all pairs and keep a count 
    // of the number of maximum pairs 
    int c = 0; 
    for (int i = 0; i < n; i++) 
        for (int j = i + 1; j < n; j++) 
            if (a[i] + a[j] == maxSum) 
                c++; 
    return c; 
} 

// driver program to test the above function 
int main() 
{ 
    int array[] = { 1, 1, 1, 2, 2, 2 }; 
    int n = sizeof(array) / sizeof(array[0]); 
    cout << sum(array, n); 
    return 0; 
} 

```

## Java

```java
// Java program to count pairs 
// with maximum sum. 
class GFG { 
  
// function to find the number of 
// maximum pair sums 
static int sum(int a[], int n) 
{ 
    // traverse through all the pairs 
    int maxSum = Integer.MIN_VALUE; 
    for (int i = 0; i < n; i++) 
        for (int j = i + 1; j < n; j++) 
            maxSum = Math.max(maxSum, a[i] + 
                                    a[j]); 
  
    // traverse through all pairs and 
    // keep a count of the number of 
    // maximum pairs 
    int c = 0; 
    for (int i = 0; i < n; i++) 
        for (int j = i + 1; j < n; j++) 
            if (a[i] + a[j] == maxSum) 
                c++; 
    return c; 
} 
  
// driver program to test the above function 
public static void main(String[] args) 
{ 
    int array[] = { 1, 1, 1, 2, 2, 2 }; 
    int n = array.length; 
    System.out.println(sum(array, n)); 
} 
} 
  
// This code is contributed by Prerna Saini
```

## Python3

```py
# Python program to count pairs with  
# maximum sum 
  
def _sum( a, n): 
  
    # traverse through all the pairs 
    maxSum = -9999999
    for i in range(n): 
        for j in range(n): 
            maxSum = max(maxSum, a[i] + a[j]) 
      
    # traverse through all pairs and 
    # keep a count of the number 
    # of maximum pairs 
    c = 0
    for i in range(n): 
        for j in range(i+1, n): 
            if a[i] + a[j] == maxSum: 
                c+=1
    return c 
  
# driver code 
array = [ 1, 1, 1, 2, 2, 2 ] 
n = len(array) 
print(_sum(array, n)) 
  
# This code is contributed by "Abhishek Sharma 44"
```

## C#

```cs
// C# program to count pairs 
// with maximum sum. 
using System; 
  
class GFG { 
  
    // function to find the number of 
    // maximum pair sums 
    static int sum(int []a, int n) 
    { 
          
        // traverse through all the pairs 
        int maxSum = int.MinValue; 
          
        for (int i = 0; i < n; i++) 
            for (int j = i + 1; j < n; j++) 
                maxSum = Math.Max(maxSum, 
                              a[i] + a[j]); 
      
        // traverse through all pairs and 
        // keep a count of the number of 
        // maximum pairs 
        int c = 0; 
        for (int i = 0; i < n; i++) 
            for (int j = i + 1; j < n; j++) 
                if (a[i] + a[j] == maxSum) 
                    c++; 
        return c; 
    } 
      
    // driver program to test the above 
    // function 
    public static void Main() 
    { 
        int []array = { 1, 1, 1, 2, 2, 2 }; 
        int n = array.Length; 
        Console.WriteLine(sum(array, n)); 
    } 
} 
  
// This code is contributed by anuj_67.
```

## PHP

```php
<?php 
// PHP program to count pairs 
// with maximum sum. 
  
// function to find the number 
// of maximum pair sum 
function sum( $a, $n) 
{ 
      
    // traverse through all 
    // the pairs 
    $maxSum = PHP_INT_MIN; 
    for($i = 0; $i < $n; $i++) 
        for($j = $i + 1; $j < $n; $j++) 
            $maxSum = max($maxSum, $a[$i] + $a[$j]); 
  
    // traverse through all  
    // pairs and keep a count 
    // of the number of  
    // maximum pairs 
    $c = 0; 
    for($i = 0; $i < $n; $i++) 
        for($j = $i + 1; $j < $n; $j++) 
            if ($a[$i] + $a[$j] == $maxSum) 
                $c++; 
    return $c; 
} 
  
    // Driver Code 
    $array = array(1, 1, 1, 2, 2, 2); 
    $n = count($array); 
    echo sum($array, $n); 
      
// This code is contributed by anuj_67. 
?>
```

输出：

```
3
```

时间复杂度：`O(n^2)`。

方法 2（高效）：

如果我们仔细观察，我们会发现以下事实。

1.  最大元素始终是解决方案的一部分
2.  如果最大元素出现多次，则结果为`maxCount * (maxCount – 1) / 2`。 我们基本上需要从`maxCount`（`maxCountC2`）中选择 2 个元素。
3.  如果最大元素出现一次，则结果等于第二个最大元素的计数。 我们可以将最大值和第二个最大值形成一个配对。

## C++

```cpp
// CPP program to count pairs with maximum sum. 
#include <bits/stdc++.h> 
using namespace std; 
  
// function to find the number of maximum pair sums 
int sum(int a[], int n) 
{ 
    // Find maximum and second maximum elements. 
    // Also find their counts. 
    int maxVal = a[0], maxCount = 1; 
    int secondMax = INT_MIN, secondMaxCount; 
    for (int i = 1; i < n; i++) { 
        if (a[i] == maxVal) 
            maxCount++; 
        else if (a[i] > maxVal) { 
            secondMax = maxVal; 
            secondMaxCount = maxCount; 
            maxVal = a[i]; 
            maxCount = 1; 
        } 
        else if (a[i] == secondMax) { 
            secondMax = a[i]; 
            secondMaxCount++; 
        } 
        else if (a[i] > secondMax) { 
            secondMax = a[i]; 
            secondMaxCount = 1; 
        } 
    } 
  
    // If maximum element appears more than once. 
    if (maxCount > 1) 
        return maxCount * (maxCount - 1) / 2; 
  
    // If maximum element appears only once. 
    return secondMaxCount; 
} 
  
// driver program to test the above function 
int main() 
{ 
    int array[] = { 1, 1, 1, 2, 2, 2, 3 }; 
    int n = sizeof(array) / sizeof(array[0]); 
    cout << sum(array, n); 
    return 0; 
}
```

## Java

```java
// Java program to count pairs  
// with maximum sum. 
import java.io.*; 
class GFG { 
      
// function to find the number  
// of maximum pair sums 
static int sum(int a[], int n) 
{ 
    // Find maximum and second maximum  
    // elements. Also find their counts. 
    int maxVal = a[0], maxCount = 1; 
    int secondMax = Integer.MIN_VALUE, 
        secondMaxCount = 0; 
    for (int i = 1; i < n; i++) { 
        if (a[i] == maxVal) 
            maxCount++; 
        else if (a[i] > maxVal) { 
            secondMax = maxVal; 
            secondMaxCount = maxCount; 
            maxVal = a[i]; 
            maxCount = 1; 
        } 
        else if (a[i] == secondMax) { 
            secondMax = a[i]; 
            secondMaxCount++; 
        } 
        else if (a[i] > secondMax) { 
            secondMax = a[i]; 
            secondMaxCount = 1; 
        } 
    } 
  
    // If maximum element appears 
    // more than once. 
    if (maxCount > 1) 
        return maxCount * (maxCount - 1) / 2; 
  
    // If maximum element appears 
    // only once. 
    return secondMaxCount; 
} 
  
// driver program  
public static void main(String[] args) 
{ 
    int array[] = { 1, 1, 1, 2, 2, 2, 3 }; 
    int n = array.length; 
    System.out.println(sum(array, n)); 
} 
} 
  
// This code is contributed by Prerna Saini
```

## Python3

```py
# Python 3 program to count 
# pairs with maximum sum. 
import sys 
  
# Function to find the number 
# of maximum pair sums 
def sum(a, n): 
  
    # Find maximum and second maximum elements. 
    # Also find their counts. 
    maxVal = a[0]; maxCount = 1
    secondMax = sys.maxsize 
      
    for i in range(1, n) :  
          
        if (a[i] == maxVal) : 
            maxCount += 1
          
        elif (a[i] > maxVal) :  
            secondMax = maxVal 
            secondMaxCount = maxCount 
            maxVal = a[i] 
            maxCount = 1
          
        elif (a[i] == secondMax) :  
            secondMax = a[i] 
            secondMaxCount += 1
          
        elif (a[i] > secondMax) :  
            secondMax = a[i] 
            secondMaxCount = 1
          
    # If maximum element appears more than once. 
    if (maxCount > 1): 
        return maxCount * (maxCount - 1) / 2
  
    # If maximum element appears only once. 
    return secondMaxCount 
      
# Driver Code 
array = [1, 1, 1, 2, 2, 2, 3]  
n = len(array) 
print(sum(array, n)) 
  
  
# This code is contributed by Smitha Dinesh Semwal
```

## C#

```cs
// C# program to count pairs with maximum 
// sum. 
using System; 
  
class GFG { 
      
    // function to find the number  
    // of maximum pair sums 
    static int sum(int []a, int n) 
    { 
          
        // Find maximum and second maximum  
        // elements. Also find their counts. 
        int maxVal = a[0], maxCount = 1; 
        int secondMax = int.MinValue; 
        int secondMaxCount = 0; 
        for (int i = 1; i < n; i++)  
        { 
            if (a[i] == maxVal) 
                maxCount++; 
            else if (a[i] > maxVal) 
            { 
                secondMax = maxVal; 
                secondMaxCount = maxCount; 
                maxVal = a[i]; 
                maxCount = 1; 
            } 
            else if (a[i] == secondMax) 
            { 
                secondMax = a[i]; 
                secondMaxCount++; 
            } 
            else if (a[i] > secondMax) 
            { 
                secondMax = a[i]; 
                secondMaxCount = 1; 
            } 
        } 
      
        // If maximum element appears 
        // more than once. 
        if (maxCount > 1) 
            return maxCount * 
                       (maxCount - 1) / 2; 
      
        // If maximum element appears 
        // only once. 
        return secondMaxCount; 
    } 
      
    // driver program  
    public static void Main() 
    { 
        int []array = { 1, 1, 1, 2, 
                               2, 2, 3 }; 
        int n = array.Length; 
          
        Console.WriteLine(sum(array, n)); 
    } 
} 
  
// This code is contributed by anuj_67.
```

## PHP

```php
<?php 
// PHP program to count 
// pairs with maximum sum. 
  
// function to find the number 
// of maximum pair sums 
function sum( $a, $n) 
{ 
    // Find maximum and second  
    // maximum elements. Also  
    // find their counts. 
    $maxVal = $a[0]; $maxCount = 1; 
    $secondMax = PHP_INT_MIN;  
    $secondMaxCount; 
    for ( $i = 1; $i < $n; $i++)  
    { 
        if ($a[$i] == $maxVal) 
            $maxCount++; 
        else if ($a[$i] > $maxVal)  
        { 
            $secondMax = $maxVal; 
            $secondMaxCount = $maxCount; 
            $maxVal = $a[$i]; 
            $maxCount = 1; 
        } 
        else if ($a[$i] == $secondMax) 
        { 
            $secondMax = $a[$i]; 
            $secondMaxCount++; 
        } 
        else if ($a[$i] > $secondMax)  
        { 
            $secondMax = $a[$i]; 
            $secondMaxCount = 1; 
        } 
    } 
  
    // If maximum element appears 
    // more than once. 
    if ($maxCount > 1) 
        return $maxCount *  
              ($maxCount - 1) / 2; 
  
    // If maximum element  
    // appears only once. 
    return $secondMaxCount; 
} 
  
// Driver Code 
$array = array(1, 1, 1, 2, 
                2, 2, 3 ); 
$n = count($array); 
echo sum($array, $n); 
  
// This code is contributed by anuj_67. 
?>
```

输出：

```
3
```

时间复杂度：`O(n)`。