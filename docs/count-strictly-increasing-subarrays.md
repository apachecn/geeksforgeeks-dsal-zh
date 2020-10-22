# 计算严格增加的子数组数量

> 原文： [https://www.geeksforgeeks.org/count-strictly-increasing-subarrays/](https://www.geeksforgeeks.org/count-strictly-increasing-subarrays/)

给定一个整数数组，[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)（大小大于 1）的计数严格增加。

预期时间复杂度：`O(n)`。

预期额外空间：`O(1)`。

例子：

```
Input: arr[] = {1, 4, 3}
Output: 1
There is only one subarray {1, 4}

Input: arr[] = {1, 2, 3, 4}
Output: 6
There are 6 subarrays {1, 2}, {1, 2, 3}, {1, 2, 3, 4}
                      {2, 3}, {2, 3, 4} and {3, 4}

Input: arr[] = {1, 2, 2, 4}
Output: 2
There are 2 subarrays {1, 2} and {2, 4}

```

[](https://practice.geeksforgeeks.org/problem-page.php?pid=405)

## 强烈建议您在继续解决方案之前，单击这里进行练习。

**简单解决方案**是[生成所有可能的子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)，并针对每个子数组检查子数组是否严格增加。 该解决方案的最坏情况下时间复杂度将为`O(n^3)`。

**更好的解决方案**使用以下事实：如果子数组`arr [i: j]`没有严格增加，则子数组`arr[i: j + 1], arr[i: j + 2], .. arr[i: n-1]`不能严格增加。 下面是基于上述思想的程序。

## C++ 

```cpp

// C++ program to count number of strictly 
// increasing subarrays 
#include<bits/stdc++.h> 
using namespace std; 

int countIncreasing(int arr[], int n) 
{ 
    // Initialize count of subarrays as 0 
    int cnt = 0; 

    // Pick starting point 
    for (int i=0; i<n; i++) 
    { 
        // Pick ending point 
        for (int j=i+1; j<n; j++) 
        { 
            if (arr[j] > arr[j-1]) 
                cnt++; 

            // If subarray arr[i..j] is not strictly  
            // increasing, then subarrays after it , i.e.,  
            // arr[i..j+1], arr[i..j+2], .... cannot 
            // be strictly increasing 
            else
                break; 
        } 
    } 
    return cnt; 
} 

// Driver program 
int main() 
{ 
  int arr[] = {1, 2, 2, 4}; 
  int n = sizeof(arr)/sizeof(arr[0]); 
  cout << "Count of strictly increasing subarrays is "
       << countIncreasing(arr, n); 
  return 0; 
} 

```

## Java

```java
// Java program to count number of strictly 
// increasing subarrays 
  
  
class Test 
{ 
    static int arr[] = new int[]{1, 2, 2, 4}; 
      
    static int countIncreasing(int n) 
    { 
        // Initialize count of subarrays as 0 
        int cnt = 0; 
       
        // Pick starting point 
        for (int i=0; i<n; i++) 
        { 
            // Pick ending point 
            for (int j=i+1; j<n; j++) 
            { 
                if (arr[j] > arr[j-1]) 
                    cnt++; 
       
                // If subarray arr[i..j] is not strictly  
                // increasing, then subarrays after it , i.e.,  
                // arr[i..j+1], arr[i..j+2], .... cannot 
                // be strictly increasing 
                else
                    break; 
            } 
        } 
        return cnt; 
    } 
    // Driver method to test the above function 
    public static void main(String[] args)  
    { 
        System.out.println("Count of strictly increasing subarrays is " +  
                                               countIncreasing(arr.length)); 
    } 
}
```

## Python3

```py
# Python3 program to count number 
# of strictly increasing subarrays 
  
def countIncreasing(arr, n): 
      
    # Initialize count of subarrays as 0 
    cnt = 0
  
    # Pick starting point 
    for i in range(0, n) : 
          
        # Pick ending point 
        for j in range(i + 1, n) : 
            if arr[j] > arr[j - 1] : 
                cnt += 1
  
            # If subarray arr[i..j] is not strictly  
            # increasing, then subarrays after it , i.e.,  
            # arr[i..j+1], arr[i..j+2], .... cannot 
            # be strictly increasing 
            else: 
                break
    return cnt 
  
  
# Driver code 
arr = [1, 2, 2, 4] 
n = len(arr) 
print ("Count of strictly increasing subarrays is", 
                            countIncreasing(arr, n)) 
  
# This code is contributed by Shreyanshi Arun.
```

## C#

```cs
// C# program to count number of  
// strictly increasing subarrays 
using System; 
  
class Test 
{ 
    static int []arr = new int[]{1, 2, 2, 4}; 
      
    static int countIncreasing(int n) 
    { 
        // Initialize count of subarrays as 0 
        int cnt = 0; 
      
        // Pick starting point 
        for (int i = 0; i < n; i++) 
        { 
            // Pick ending point 
            for (int j = i + 1; j < n; j++) 
            { 
                if (arr[j] > arr[j - 1]) 
                    cnt++; 
      
                // If subarray arr[i..j] is not strictly  
                // increasing, then subarrays after it ,  
                // i.e.,  arr[i..j+1], arr[i..j+2], ....  
                // cannot be strictly increasing 
                else
                    break; 
            } 
        } 
        return cnt; 
    } 
      
    // Driver Code 
    public static void Main(String[] args)  
    { 
        Console.Write("Count of strictly increasing" +  
            "subarrays is " + countIncreasing(arr.Length)); 
    } 
} 
  
// This code is contribute by parashar.
```

## PHP

```php
<?php 
// PHP program to count number of 
// strictly increasing subarrays 
  
function countIncreasing( $arr, $n) 
{ 
      
    // Initialize count of subarrays  
    // as 0 
    $cnt = 0; 
  
    // Pick starting point 
    for ( $i = 0; $i < $n; $i++) 
    { 
        // Pick ending point 
        for ( $j = $i+1; $j < $n; $j++) 
        { 
            if ($arr[$j] > $arr[$j-1]) 
                $cnt++; 
  
            // If subarray arr[i..j] is 
            // not strictly increasing, 
            // then subarrays after it, 
            // i.e., arr[i..j+1],  
            // arr[i..j+2], .... cannot 
            // be strictly increasing 
            else
                break; 
        } 
    } 
    return $cnt; 
} 
  
// Driver program 
  
$arr = array(1, 2, 2, 4); 
$n = count($arr); 
echo "Count of strictly increasing ", 
                     "subarrays is ", 
            countIncreasing($arr, $n); 
  
// This code is contribute by anuj_67. 
?>
```

输出：

```
Count of strictly increasing subarrays is 2
```

