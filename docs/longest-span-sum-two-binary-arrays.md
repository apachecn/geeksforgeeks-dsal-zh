# 两个二进制数组中具有相同总和的最长跨度

> 原文： [https://www.geeksforgeeks.org/longest-span-sum-two-binary-arrays/](https://www.geeksforgeeks.org/longest-span-sum-two-binary-arrays/)

给定两个具有相同大小`n`的二进制数组`arr1[]`和`arr2[]`。 求出最长公共跨度`(i, j)`的长度，其中`j >= i`，使得`arr1[i] + arr1[i + 1] + … + arr1[j] = arr2[i] + arr2[i + 1] + … + arr2[j]`。

预期时间复杂度为`Θ(n)`。

**示例**：

```
Input: arr1[] = {0, 1, 0, 0, 0, 0};
       arr2[] = {1, 0, 1, 0, 0, 1};
Output: 4
The longest span with same sum is from index 1 to 4.

Input: arr1[] = {0, 1, 0, 1, 1, 1, 1};
       arr2[] = {1, 1, 1, 1, 1, 0, 1};
Output: 6
The longest span with same sum is from index 1 to 6.

Input: arr1[] = {0, 0, 0};
       arr2[] = {1, 1, 1};
Output: 0

Input: arr1[] = {0, 0, 1, 0};
       arr2[] = {1, 1, 1, 1};
Output: 1

```

[](https://practice.geeksforgeeks.org/problem-page.php?pid=188)

## 强烈建议您在继续解决方案之前，单击这里进行练习。

**方法 1（简单解决方案）**：

通过考虑两个数组的相同子数组来一一对应。 对于所有子数组，计算总和，如果总和相同且当前长度大于最大长度，则更新最大长度。 下面是 C++ 实现的简单方法。

## C++ 

```cpp

// A Simple C++ program to find longest common 
// subarray of two binary arrays with same sum 
#include<bits/stdc++.h> 
using namespace std; 

// Returns length of the longest common subarray 
// with same sum 
int longestCommonSum(bool arr1[], bool arr2[], int n) 
{ 
    // Initialize result 
    int maxLen = 0; 

    // One by one pick all possible starting points 
    // of subarrays 
    for (int i=0; i<n; i++) 
    { 
       // Initialize sums of current subarrays 
       int sum1 = 0, sum2 = 0; 

       // Conider all points for starting with arr[i] 
       for (int j=i; j<n; j++) 
       { 
           // Update sums 
           sum1 += arr1[j]; 
           sum2 += arr2[j]; 

           // If sums are same and current length is 
           // more than maxLen, update maxLen 
           if (sum1 == sum2) 
           { 
             int len = j-i+1; 
             if (len > maxLen) 
                maxLen = len; 
           } 
       } 
    } 
    return maxLen; 
} 

// Driver program to test above function 
int main() 
{ 
    bool  arr1[] = {0, 1, 0, 1, 1, 1, 1}; 
    bool  arr2[] = {1, 1, 1, 1, 1, 0, 1}; 
    int n = sizeof(arr1)/sizeof(arr1[0]); 
    cout << "Length of the longest common span with same "
            "sum is "<< longestCommonSum(arr1, arr2, n); 
    return 0; 
} 

```

## Java

```
// A Simple Java program to find longest common 
// subarray of two binary arrays with same sum 
  
class Test 
{ 
    static int arr1[] = new int[]{0, 1, 0, 1, 1, 1, 1}; 
    static int arr2[] = new int[]{1, 1, 1, 1, 1, 0, 1}; 
      
    // Returns length of the longest common sum in arr1[] 
    // and arr2[]. Both are of same size n. 
    static int longestCommonSum(int n) 
    { 
        // Initialize result 
        int maxLen = 0; 
       
        // One by one pick all possible starting points 
        // of subarrays 
        for (int i=0; i<n; i++) 
        { 
           // Initialize sums of current subarrays 
           int sum1 = 0, sum2 = 0; 
       
           // Conider all points for starting with arr[i] 
           for (int j=i; j<n; j++) 
           { 
               // Update sums 
               sum1 += arr1[j]; 
               sum2 += arr2[j]; 
       
               // If sums are same and current length is 
               // more than maxLen, update maxLen 
               if (sum1 == sum2) 
               { 
                 int len = j-i+1; 
                 if (len > maxLen) 
                    maxLen = len; 
               } 
           } 
        } 
        return maxLen; 
    } 
      
    // Driver method to test the above function 
    public static void main(String[] args)  
    { 
        System.out.print("Length of the longest common span with same sum is "); 
        System.out.println(longestCommonSum(arr1.length)); 
    } 
}
```

## Python3

```
# A Simple python program to find longest common 
# subarray of two binary arrays with same sum 
  
# Returns length of the longest common subarray 
# with same sum 
def longestCommonSum(arr1, arr2, n): 
  
    # Initialize result 
    maxLen = 0
  
    # One by one pick all possible starting points 
    # of subarrays 
    for i in range(0,n): 
  
        # Initialize sums of current subarrays 
        sum1 = 0
        sum2 = 0
  
        # Conider all points for starting with arr[i] 
        for j in range(i,n): 
      
            # Update sums 
            sum1 += arr1[j] 
            sum2 += arr2[j] 
  
            # If sums are same and current length is 
            # more than maxLen, update maxLen 
            if (sum1 == sum2): 
                len = j-i+1
                if (len > maxLen): 
                    maxLen = len
      
    return maxLen 
  
  
# Driver program to test above function 
arr1 = [0, 1, 0, 1, 1, 1, 1] 
arr2 = [1, 1, 1, 1, 1, 0, 1] 
n = len(arr1) 
print("Length of the longest common span with same "
            "sum is",longestCommonSum(arr1, arr2, n)) 
  
# This code is contributed by 
# Smitha Dinesh Semwal
```

## C#

```
// A Simple C# program to find  
// longest common subarray of  
// two binary arrays with same sum 
using System; 
  
class GFG 
{ 
static int[] arr1 = new int[]{0, 1, 0, 1, 1, 1, 1}; 
static int[] arr2 = new int[]{1, 1, 1, 1, 1, 0, 1}; 
  
// Returns length of the longest  
// common sum in arr1[] and arr2[].  
// Both are of same size n. 
static int longestCommonSum(int n) 
{ 
    // Initialize result 
    int maxLen = 0; 
  
    // One by one pick all possible  
    // starting points of subarrays 
    for (int i = 0; i < n; i++) 
    { 
    // Initialize sums of current  
    // subarrays 
    int sum1 = 0, sum2 = 0; 
  
    // Conider all points for  
    // starting with arr[i] 
    for (int j = i; j < n; j++) 
    { 
        // Update sums 
        sum1 += arr1[j]; 
        sum2 += arr2[j]; 
  
        // If sums are same and current  
        // length is more than maxLen,  
        // update maxLen 
        if (sum1 == sum2) 
        { 
            int len = j - i + 1; 
            if (len > maxLen) 
                maxLen = len; 
        } 
    } 
    } 
    return maxLen; 
} 
  
// Driver Code 
public static void Main()  
{ 
    Console.Write("Length of the longest " +  
           "common span with same sum is "); 
    Console.Write(longestCommonSum(arr1.Length)); 
} 
} 
  
// This code is contributed  
// by ChitraNayal
```

## PHP

```
<?php 
// A Simple PHP program to find  
// longest common subarray of  
// two binary arrays with same sum 
  
// Returns length of the longest  
// common subarray with same sum 
function longestCommonSum($arr1, $arr2, $n) 
{ 
    // Initialize result 
    $maxLen = 0; 
  
    // One by one pick all possible  
    // starting points of subarrays 
    for ($i = 0; $i < $n; $i++) 
    { 
    // Initialize sums of  
    // current subarrays 
    $sum1 = 0; $sum2 = 0; 
  
    // Conider all points  
    // for starting with arr[i] 
    for ($j = $i; $j < $n; $j++) 
    { 
        // Update sums 
        $sum1 += $arr1[$j]; 
        $sum2 += $arr2[$j]; 
  
        // If sums are same and current  
        // length is more than maxLen,  
        // update maxLen 
        if ($sum1 == $sum2) 
        { 
            $len = $j - $i + 1; 
            if ($len > $maxLen) 
                $maxLen = $len; 
        } 
    } 
    } 
    return $maxLen; 
} 
  
// Driver Code 
$arr1 = array(0, 1, 0, 1, 1, 1, 1); 
$arr2 = array (1, 1, 1, 1, 1, 0, 1); 
$n = sizeof($arr1); 
echo "Length of the longest common span ".  
                  "with same ", "sum is ",  
       longestCommonSum($arr1, $arr2, $n); 
  
// This code is contributed by aj_36 
?>
```

输出：

```
Length of the longest common span with same sum is 6
```

时间复杂度：`O(n ^ 2)`。

辅助空间：`O(1)`。

 
方法 2（使用辅助阵列）：

该想法基于以下观察。

+   由于总共有`n`个元素，因此两个数组的最大和为`n`。
+   两个和之间的差从`-n`到`n`。 因此，总共有`2n +1`个可能的差值。
+   如果两个数组的前缀和之间的差在两个点处相同，则这两个点之间的子数组具有相同的和。

以下是完整算法。

1.  创建大小为`2n + 1`的辅助数组，以存储所有可能的差值的起点（请注意，差的可能值从`-n`到`n`不等，即，总共有`2n + 1`个可能值）。
2.  将所有差异的起始点初始化为`-1`。
3.  将`maxLen`初始化为 0，并将两个数组的前缀和都初始化为 0，`preSum1 = 0`，`preSum2 = 0`。
4.  从`i = 0`到`n-1`遍历两个数组。
    1.  更新前缀总和：`preSum1 += arr1[i]`，`preSum2 += arr2[i]`。
    2.  计算当前前缀总和的差：`curr_diff = preSum1 – preSum2`。
    3.  在差异数组中查找索引：`diffIndex = n + curr_diff`，`curr_diff`可以为负，并且可以一直到`-n`。
    4.  如果`curr_diff`为 0，则到目前为止`i + 1`为`maxLen`。
    5.  否则，如果第一次看到`curr_diff`，即当前`diff`的起始点为 -1，则将起始点更新为`i`。
    6.  否则（第一次未看到`curr_diff`），然后将`i`视为终点并找到当前相同总和跨度的长度。如果此长度更大，则更新`maxLen`。
5.  返回`maxLen`。

下面是上述算法的实现。

## C++

```
// A O(n) and O(n) extra space C++ program to find 
// longest common subarray of two binary arrays with 
// same sum 
#include<bits/stdc++.h> 
using namespace std; 
  
// Returns length of the longest common sum in arr1[] 
// and arr2[]. Both are of same size n. 
int longestCommonSum(bool arr1[], bool arr2[], int n) 
{ 
    // Initialize result 
    int maxLen = 0; 
  
    // Initialize prefix sums of two arrays 
    int preSum1 = 0, preSum2 = 0; 
  
    // Create an array to store staring and ending 
    // indexes of all possible diff values. diff[i] 
    // would store starting and ending points for 
    // difference "i-n" 
    int diff[2*n+1]; 
  
    // Initialize all starting and ending values as -1. 
    memset(diff, -1, sizeof(diff)); 
  
    // Traverse both arrays 
    for (int i=0; i<n; i++) 
    { 
        // Update prefix sums 
        preSum1 += arr1[i]; 
        preSum2 += arr2[i]; 
  
        // Comput current diff and index to be used 
        // in diff array. Note that diff can be negative 
        // and can have minimum value as -1. 
        int curr_diff = preSum1 - preSum2; 
        int diffIndex = n + curr_diff; 
  
        // If current diff is 0, then there are same number 
        // of 1's so far in both arrays, i.e., (i+1) is 
        // maximum length. 
        if (curr_diff == 0) 
            maxLen = i+1; 
  
        // If current diff is seen first time, then update 
        // starting index of diff. 
        else if ( diff[diffIndex] == -1) 
            diff[diffIndex] = i; 
  
        // Current diff is already seen 
        else
        { 
            // Find length of this same sum common span 
            int len = i - diff[diffIndex]; 
  
            // Update max len if needed 
            if (len > maxLen) 
                maxLen = len; 
        } 
    } 
    return maxLen; 
} 
  
// Driver code 
int main() 
{ 
    bool  arr1[] = {0, 1, 0, 1, 1, 1, 1}; 
    bool  arr2[] = {1, 1, 1, 1, 1, 0, 1}; 
    int n = sizeof(arr1)/sizeof(arr1[0]); 
    cout << "Length of the longest common span with same "
            "sum is "<< longestCommonSum(arr1, arr2, n); 
    return 0; 
}
```

## Java

```
// A O(n) and O(n) extra space Java program to find 
// longest common subarray of two binary arrays with 
// same sum 
  
class Test 
{ 
    static int arr1[] = new int[]{0, 1, 0, 1, 1, 1, 1}; 
    static int arr2[] = new int[]{1, 1, 1, 1, 1, 0, 1}; 
      
    // Returns length of the longest common sum in arr1[] 
    // and arr2[]. Both are of same size n. 
    static int longestCommonSum(int n) 
    { 
        // Initialize result 
        int maxLen = 0; 
       
        // Initialize prefix sums of two arrays 
        int preSum1 = 0, preSum2 = 0; 
       
        // Create an array to store staring and ending 
        // indexes of all possible diff values. diff[i] 
        // would store starting and ending points for 
        // difference "i-n" 
        int diff[] = new int[2*n+1]; 
       
        // Initialize all starting and ending values as -1. 
        for (int i = 0; i < diff.length; i++) { 
            diff[i] = -1; 
        } 
       
        // Traverse both arrays 
        for (int i=0; i<n; i++) 
        { 
            // Update prefix sums 
            preSum1 += arr1[i]; 
            preSum2 += arr2[i]; 
       
            // Comput current diff and index to be used 
            // in diff array. Note that diff can be negative 
            // and can have minimum value as -1. 
            int curr_diff = preSum1 - preSum2; 
            int diffIndex = n + curr_diff; 
       
            // If current diff is 0, then there are same number 
            // of 1's so far in both arrays, i.e., (i+1) is 
            // maximum length. 
            if (curr_diff == 0) 
                maxLen = i+1; 
       
            // If current diff is seen first time, then update 
            // starting index of diff. 
            else if ( diff[diffIndex] == -1) 
                diff[diffIndex] = i; 
       
            // Current diff is already seen 
            else
            { 
                // Find length of this same sum common span 
                int len = i - diff[diffIndex]; 
       
                // Update max len if needed 
                if (len > maxLen) 
                    maxLen = len; 
            } 
        } 
        return maxLen; 
    } 
      
    // Driver method to test the above function 
    public static void main(String[] args)  
    { 
        System.out.print("Length of the longest common span with same sum is "); 
        System.out.println(longestCommonSum(arr1.length)); 
    } 
}
```

## Python

```
# Python program to find longest common 
# subarray of two binary arrays with 
# same sum 
  
def longestCommonSum(arr1, arr2, n): 
    
    # Initialize result 
    maxLen = 0
      
    # Initialize prefix sums of two arrays 
    presum1 = presum2 = 0
      
    # Create a dictionary to store indices 
    # of all possible sums 
    diff = {} 
      
    # Traverse both arrays 
    for i in range(n): 
        
        # Update prefix sums 
        presum1 += arr1[i] 
        presum2 += arr2[i] 
          
        # Compute current diff which will be 
        # used as index in diff dictionary 
        curr_diff = presum1 - presum2 
          
        # If current diff is 0, then there  
        # are same number of 1's so far in  
        # both arrays, i.e., (i+1) is 
        # maximum length. 
        if curr_diff == 0: 
            maxLen = i+1  
        elif curr_diff not in diff: 
            # save the index for this diff 
            diff[curr_diff] = i 
        else:                   
            # calculate the span length 
            length = i - diff[curr_diff] 
            maxLen = max(maxLen, length) 
          
    return maxLen 
  
# Driver program     
arr1 = [0, 1, 0, 1, 1, 1, 1] 
arr2 = [1, 1, 1, 1, 1, 0, 1] 
print("Length of the longest common", 
    " span with same", end = " ") 
print("sum is",longestCommonSum(arr1,  
                   arr2, len(arr1))) 
  
# This code is contributed by Abhijeet Nautiyal
```

## C#

```
// A O(n) and O(n) extra space C# program  
// to find longest common subarray of two  
// binary arrays with same sum 
using System; 
  
class GFG 
{ 
static int[] arr1 = new int[]{0, 1, 0, 1, 1, 1, 1}; 
static int[] arr2 = new int[]{1, 1, 1, 1, 1, 0, 1}; 
  
// Returns length of the longest  
// common sum in arr1[] and arr2[]. 
// Both are of same size n. 
static int longestCommonSum(int n) 
{ 
    // Initialize result 
    int maxLen = 0; 
  
    // Initialize prefix sums of  
    // two arrays 
    int preSum1 = 0, preSum2 = 0; 
  
    // Create an array to store staring  
    // and ending indexes of all possible  
    // diff values. diff[i] would store  
    // starting and ending points for 
    // difference "i-n" 
    int[] diff = new int[2 * n + 1]; 
  
    // Initialize all starting and ending 
    // values as -1. 
    for (int i = 0; i < diff.Length; i++) 
    { 
        diff[i] = -1; 
    } 
  
    // Traverse both arrays 
    for (int i = 0; i < n; i++) 
    { 
        // Update prefix sums 
        preSum1 += arr1[i]; 
        preSum2 += arr2[i]; 
  
        // Compute current diff and index to  
        // be used in diff array. Note that  
        // diff can be negative and can have 
        // minimum value as -1. 
        int curr_diff = preSum1 - preSum2; 
        int diffIndex = n + curr_diff; 
  
        // If current diff is 0, then there  
        // are same number of 1's so far in  
        // both arrays, i.e., (i+1) is 
        // maximum length. 
        if (curr_diff == 0) 
            maxLen = i + 1; 
  
        // If current diff is seen first time,  
        // then update starting index of diff. 
        else if ( diff[diffIndex] == -1) 
            diff[diffIndex] = i; 
  
        // Current diff is already seen 
        else
        { 
            // Find length of this same  
            // sum common span 
            int len = i - diff[diffIndex]; 
  
            // Update max len if needed 
            if (len > maxLen) 
                maxLen = len; 
        } 
    } 
    return maxLen; 
} 
  
// Driver Code 
public static void Main()  
{ 
    Console.Write("Length of the longest common " +  
                         "span with same sum is "); 
    Console.WriteLine(longestCommonSum(arr1.Length)); 
} 
} 
  
// This code is contributed  
// by Akanksha Rai(Abby_akku)
```

输出：

```
Length of the longest common span with same sum is 6
```

时间复杂度：`Θ(n)`。

辅助空间：`Θ(n)`。

方法 3（使用哈希）：

1.  找到差异数组`arr[]`，使`arr[i] = arr1[i] – arr2[i]`。
2.  差异数组中 [0 和 1 数量相等的最大子数组](https://www.geeksforgeeks.org/largest-subarray-with-equal-number-of-0s-and-1s/)。

## C++

```
// C++ program to find largest subarray  
// with equal number of 0's and 1's. 
#include <bits/stdc++.h> 
using namespace std; 
  
// Returns largest common subarray with equal  
// number of 0s and 1s in both of t 
int longestCommonSum(bool arr1[], bool arr2[], int n) 
{ 
    // Find difference between the two 
    int arr[n]; 
    for (int i=0; i<n; i++) 
      arr[i] = arr1[i] - arr2[i]; 
      
    // Creates an empty hashMap hM 
    unordered_map<int, int> hM; 
  
    int sum = 0;     // Initialize sum of elements 
    int max_len = 0; // Initialize result 
  
    // Traverse through the given array 
    for (int i = 0; i < n; i++) 
    { 
        // Add current element to sum 
        sum += arr[i]; 
  
        // To handle sum=0 at last index 
        if (sum == 0) 
            max_len = i + 1; 
  
        // If this sum is seen before,  
        // then update max_len if required 
        if (hM.find(sum) != hM.end()) 
          max_len = max(max_len, i - hM[sum]); 
            
        else // Else put this sum in hash table 
            hM[sum] = i; 
    } 
  
    return max_len; 
} 
  
// Driver progra+m to test above function 
int main() 
{ 
    bool  arr1[] = {0, 1, 0, 1, 1, 1, 1}; 
    bool  arr2[] = {1, 1, 1, 1, 1, 0, 1}; 
    int n = sizeof(arr1)/sizeof(arr1[0]); 
    cout << longestCommonSum(arr1, arr2, n); 
    return 0; 
}
```

## Java

```
// Java program to find largest subarray  
// with equal number of 0's and 1's.  
import java.io.*; 
import java.util.*; 
  
class GFG  
{ 
  
    // Returns largest common subarray with equal  
    // number of 0s and 1s 
    static int longestCommonSum(int[] arr1, int[] arr2, int n) 
    { 
        // Find difference between the two 
        int[] arr = new int[n]; 
        for (int i = 0; i < n; i++)  
            arr[i] = arr1[i] - arr2[i]; 
  
        // Creates an empty hashMap hM  
        HashMap<Integer, Integer> hM = new HashMap<>(); 
  
        int sum = 0;     // Initialize sum of elements  
        int max_len = 0; // Initialize result  
  
        // Traverse through the given array  
        for (int i = 0; i < n; i++)  
        {  
            // Add current element to sum  
            sum += arr[i];  
  
            // To handle sum=0 at last index  
            if (sum == 0)  
                max_len = i + 1;  
  
            // If this sum is seen before,  
            // then update max_len if required  
            if (hM.containsKey(sum))  
                max_len = Math.max(max_len, i - hM.get(sum));  
              
            else // Else put this sum in hash table  
                hM.put(sum, i);  
        } 
        return max_len;  
    }  
  
    // Driver code 
    public static void main(String args[]) 
    { 
            int[] arr1 = {0, 1, 0, 1, 1, 1, 1};  
            int[] arr2 = {1, 1, 1, 1, 1, 0, 1}; 
            int n = arr1.length; 
            System.out.println(longestCommonSum(arr1, arr2, n));  
    } 
} 
  
// This code is contributed by rachana soma
```

输出：

```
6
```

