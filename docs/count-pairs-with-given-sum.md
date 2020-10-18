# 计算给定总和的对

> 原文： [https://www.geeksforgeeks.org/count-pairs-with-given-sum/](https://www.geeksforgeeks.org/count-pairs-with-given-sum/)

给定一个整数数组和一个数字`sum`，找到该数组中总和等于`sum`的整数对的数量。

**示例**：

```
Input  :  arr[] = {1, 5, 7, -1}, 
          sum = 6
Output :  2
Pairs with sum 6 are (1, 5) and (7, -1)

Input  :  arr[] = {1, 5, 7, -1, 5}, 
          sum = 6
Output :  3
Pairs with sum 6 are (1, 5), (7, -1) &
                     (1, 5)         

Input  :  arr[] = {1, 1, 1, 1}, 
          sum = 2
Output :  6
There are 3! pairs with sum 2.

Input  :  arr[] = {10, 12, 10, 15, -1, 7, 6, 
                   5, 4, 2, 1, 1, 1}, 
          sum = 11
Output :  9

```

预期时间复杂度`O(n)`。



一个**简单解决方案**遍历每个元素，并检查数组中是否有另一个数字可以添加到该数字以求和。

## C++ 

```cpp

// C++ implementation of simple method to find count of 
// pairs with given sum. 
#include <bits/stdc++.h> 
using namespace std; 

// Returns number of pairs in arr[0..n-1] with sum equal 
// to 'sum' 
int getPairsCount(int arr[], int n, int sum) 
{ 
    int count = 0; // Initialize result 

    // Consider all possible pairs and check their sums 
    for (int i=0; i<n; i++) 
        for (int j=i+1; j<n; j++) 
            if (arr[i]+arr[j] == sum) 
                count++; 

    return count; 
} 

// Driver function to test the above function 
int main() 
{ 
    int arr[] = {1, 5, 7, -1, 5} ; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    int sum = 6; 
    cout << "Count of pairs is " 
         << getPairsCount(arr, n, sum); 
    return 0; 
} 

```

## Java

```
// Java implementation of simple method to find count of 
// pairs with given sum. 
public class find 
{ 
    public static void main(String args[]) 
    { 
        int[] arr = { 1, 5, 7, -1, 5 }; 
        int sum = 6; 
        getPairsCount(arr, sum); 
    } 
  
    // Prints number of pairs in arr[0..n-1] with sum equal 
    // to 'sum' 
    public static void getPairsCount(int[] arr, int sum) 
    { 
  
        int count = 0;// Initialize result 
  
        // Consider all possible pairs and check their sums 
        for (int i = 0; i < arr.length; i++) 
            for (int j = i + 1; j < arr.length; j++) 
                if ((arr[i] + arr[j]) == sum) 
                    count++; 
  
        System.out.printf("Count of pairs is %d",count); 
    } 
} 
// This program is contributed by Jyotsna
```

## Python3

```
# Python3 implementation of simple method 
# to find count of pairs with given sum. 
  
# Returns number of pairs in arr[0..n-1]  
# with sum equal to 'sum' 
def getPairsCount(arr, n, sum): 
      
    count = 0 # Initialize result 
  
    # Consider all possible pairs 
    # and check their sums 
    for i in range(0, n): 
        for j in range(i + 1, n): 
            if arr[i] + arr[j] == sum: 
                count += 1
      
    return count 
  
# Driver function  
arr = [1, 5, 7, -1, 5] 
n = len(arr) 
sum = 6
print("Count of pairs is", 
      getPairsCount(arr, n, sum)) 
  
# This code is contributed by Smitha Dinesh Semwal
```

## C#

```
// C# implementation of simple  
// method to find count of  
// pairs with given sum.  
using System; 
  
class GFG 
{ 
public static void getPairsCount(int[] arr, 
                                 int sum)  
{  
  
    int count = 0; // Initialize result  
  
    // Consider all possible pairs  
    // and check their sums  
    for (int i = 0;  
             i < arr.Length; i++)  
        for (int j = i + 1;  
                 j < arr.Length; j++)  
            if ((arr[i] + arr[j]) == sum)  
                count++;  
  
    Console.WriteLine("Count of pairs is " +  
                                     count);  
}  
  
// Driver Code 
static public void Main () 
{ 
    int[] arr = { 1, 5, 7, -1, 5 };  
    int sum = 6;  
    getPairsCount(arr, sum);  
} 
} 
  
// This code is contributed 
// by Sach_Code
```

## PHP

```
<?php 
// PHP implementation of simple  
// method to find count of 
// pairs with given sum. 
  
// Returns number of pairs in  
// arr[0..n-1] with sum equal 
// to 'sum' 
function getPairsCount($arr, $n, $sum) 
{ 
    // Initialize result 
    $count = 0;  
  
    // Consider all possible pairs  
    // and check their sums 
    for ($i = 0; $i < $n; $i++) 
        for ($j = $i + 1; $j < $n; $j++) 
            if ($arr[$i] + $arr[$j] == $sum) 
                $count++; 
  
    return $count; 
} 
  
    // Driver Code 
    $arr = array(1, 5, 7, -1, 5) ; 
    $n = sizeof($arr); 
    $sum = 6; 
    echo "Count of pairs is "
         , getPairsCount($arr, $n, $sum); 
           
// This code is contributed by nitin mittal. 
?>
```

输出：

```
Count of pairs is 3
```

时间复杂度：`O(n2)`。

辅助空间：`O(1)`。

 
在`O(n)`时间内可能有更好的解决方案。

下面是算法。

+   创建一个映射以存储数组中每个数字的频率。 （需要单遍历）
+   在下一个遍历中，对于每个元素，检查是否可以将其与任何其他元素（除了自身！）组合以得出所需的总和。 相应地增加计数器。
+   第二次遍历完成后，我们将计数器中存储了所需值的两倍，因为每一对都被计数了两次。 因此，将计数除以 2 并返回。

下面是上述想法的实现：

## C++

```
// C++ implementation of simple method to find count of 
// pairs with given sum. 
#include <bits/stdc++.h> 
using namespace std; 
  
// Returns number of pairs in arr[0..n-1] with sum equal 
// to 'sum' 
int getPairsCount(int arr[], int n, int sum) 
{ 
    unordered_map<int, int> m; 
  
    // Store counts of all elements in map m 
    for (int i=0; i<n; i++) 
        m[arr[i]]++; 
  
    int twice_count = 0; 
  
    // iterate through each element and increment the 
    // count (Notice that every pair is counted twice) 
    for (int i=0; i<n; i++) 
    { 
        twice_count += m[sum-arr[i]]; 
  
        // if (arr[i], arr[i]) pair satisfies the condition, 
        // then we need to ensure that the count is 
        // decreased by one such that the (arr[i], arr[i]) 
        // pair is not considered 
        if (sum-arr[i] == arr[i]) 
            twice_count--; 
    } 
  
    // return the half of twice_count 
    return twice_count/2; 
} 
  
// Driver function to test the above function 
int main() 
{ 
    int arr[] = {1, 5, 7, -1, 5} ; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    int sum = 6; 
    cout << "Count of pairs is " 
         << getPairsCount(arr, n, sum); 
    return 0; 
}
```

## Java

```
/* Java implementation of simple method to find count of 
pairs with given sum*/
  
import java.util.HashMap; 
  
class Test 
{ 
    static int arr[] = new int[]{1, 5, 7, -1, 5} ; 
      
    // Returns number of pairs in arr[0..n-1] with sum equal 
    // to 'sum' 
    static int getPairsCount(int n, int sum) 
    { 
        HashMap<Integer, Integer> hm = new HashMap<>(); 
  
        // Store counts of all elements in map hm 
        for (int i=0; i<n; i++){ 
              
            // initializing value to 0, if key not found 
            if(!hm.containsKey(arr[i])) 
                hm.put(arr[i],0); 
                  
            hm.put(arr[i], hm.get(arr[i])+1); 
        } 
        int twice_count = 0; 
  
        // iterate through each element and increment the 
        // count (Notice that every pair is counted twice) 
        for (int i=0; i<n; i++) 
        { 
            if(hm.get(sum-arr[i]) != null) 
                twice_count += hm.get(sum-arr[i]); 
  
            // if (arr[i], arr[i]) pair satisfies the condition, 
            // then we need to ensure that the count is 
            // decreased by one such that the (arr[i], arr[i]) 
            // pair is not considered 
            if (sum-arr[i] == arr[i]) 
                twice_count--; 
        } 
  
        // return the half of twice_count 
        return twice_count/2; 
    } 
  
    // Driver method to test the above function 
    public static void main(String[] args) { 
          
        int sum = 6; 
        System.out.println("Count of pairs is " +  
                            getPairsCount(arr.length,sum)); 
          
    } 
} 
// This code is contributed by Gaurav Miglani
```

## Python3

```
# Python 3 implementation of simple method 
# to find count of pairs with given sum. 
import sys 
  
# Returns number of pairs in arr[0..n-1]  
# with sum equal to 'sum' 
def getPairsCount(arr, n, sum): 
      
    m = [0] * 1000
      
    # Store counts of all elements in map m 
    for i in range(0, n): 
        m[arr[i]] 
        m[arr[i]] += 1
  
    twice_count = 0
  
    # Iterate through each element and increment 
    # the count (Notice that every pair is  
    # counted twice) 
    for i in range(0, n): 
      
        twice_count += m[sum - arr[i]]  
  
        # if (arr[i], arr[i]) pair satisfies the 
        # condition, then we need to ensure that 
        # the count is  decreased by one such  
        # that the (arr[i], arr[i]) pair is not 
        # considered 
        if (sum - arr[i] == arr[i]): 
            twice_count -= 1
      
    # return the half of twice_count 
    return int(twice_count / 2)  
  
# Driver function  
arr = [1, 5, 7, -1, 5]  
n = len(arr) 
sum = 6
  
print("Count of pairs is", getPairsCount(arr, 
                                     n, sum)) 
  
# This code is contributed by  
# Smitha Dinesh Semwal
```

## C#

```
// C# implementation of simple method to 
// find count of pairs with given sum 
using System; 
using System.Collections.Generic; 
  
class GFG 
{ 
public static int[] arr = new int[]{1, 5, 7, -1, 5}; 
  
// Returns number of pairs in arr[0..n-1]  
// with sum equal to 'sum'  
public static int getPairsCount(int n, int sum) 
{ 
    Dictionary<int,  
               int> hm = new Dictionary<int,  
                                        int>(); 
  
    // Store counts of all elements  
    // in map hm  
    for (int i = 0; i < n; i++) 
    { 
  
        // initializing value to 0,  
        // if key not found  
        if (!hm.ContainsKey(arr[i])) 
        { 
            hm[arr[i]] = 0; 
        } 
  
        hm[arr[i]] = hm[arr[i]] + 1; 
    } 
    int twice_count = 0; 
  
    // iterate through each element and   
    // increment the count (Notice that  
    // every pair is counted twice)  
    for (int i = 0; i < n; i++) 
    { 
        if (hm[sum - arr[i]] != null) 
        { 
            twice_count += hm[sum - arr[i]]; 
        } 
  
        // if (arr[i], arr[i]) pair satisfies  
        // the condition, then we need to ensure  
        // that the count is decreased by one  
        // such that the (arr[i], arr[i])  
        // pair is not considered  
        if (sum - arr[i] == arr[i]) 
        { 
            twice_count--; 
        } 
    } 
  
    // return the half of twice_count  
    return twice_count / 2; 
} 
  
// Driver Code 
public static void Main(string[] args) 
{ 
    int sum = 6; 
    Console.WriteLine("Count of pairs is " +  
                       getPairsCount(arr.Length, sum)); 
} 
} 
  
// This code is contributed by Shrikant13
```

输出：

```
Count of pairs is 3
```

