# 最大数目等于 0 和 1 的子数组

> 原文： [https://www.geeksforgeeks.org/largest-subarray-with-equal-number-of-0s-and-1s/](https://www.geeksforgeeks.org/largest-subarray-with-equal-number-of-0s-and-1s/)

给定一个仅包含 0 和 1 的数组，找到包含相等的 0 和 1 的最大子数组。 预期时间复杂度为`O(n)`。

**示例**：

```
Input: arr[] = {1, 0, 1, 1, 1, 0, 0}
Output: 1 to 6 
(Starting and Ending indexes of output subarray)

Input: arr[] = {1, 1, 1, 1}
Output: No such subarray

Input: arr[] = {0, 0, 1, 1, 0}
Output: 0 to 3 Or 1 to 4

```



**方法 1**：暴力。

**方法**：这些类型问题中的暴力方法是生成所有可能的子数组。 然后，首先检查子数组的 **0** 和 **1** 的数目是否相等。 为了简化此过程，将 **0 作为 -1**， **1** 保持原样，对子数组分别**累积总和**。 **累积总和等于 0** 的点表示从开始到该点的子数组具有相等数量的 **0** 和 **1**。 现在，由于这是一个有效的子数组，请将其大小与迄今为止找到的此类子数组的最大大小进行比较。

**算法**：

1.  使用起始指针表示子数组的起始点。

2.  取一个变量`sum = 0`，它将取所有子数组元素的累加和。

3.  如果起始点的值`= 1`则用 **1** 初始化，否则用 **-1** 初始化。

4.  现在开始一个内部循环，并按照相同的逻辑开始累积元素的总和。

5.  如果累积总和`= 0`，则表示子数组的 **0 的数量等于 1**。

6.  现在，将其大小与最大子数组的大小进行比较，如果更大，则将此类子数组的第一个索引存储在变量中并更新大小的值。

7.  打印具有上述算法返回的**起始索引和大小**的子数组。

**伪代码**：

```
Run a loop from i=0 to n-1
  if(arr[i]==1)
  sum=1
  else
  sum=-1
  Run inner loop from j=i+1 to n-1
      sum+=arr[j]
      if(sum==0)
        if(j-i+1>max_size)
           start_index=i
           max_size=j-i+1
Run a loop from i=start_index till max_size-1
print(arr[i])    

```

## C++ 

```cpp

// A simple C++ program to find the largest 
// subarray with equal number of 0s and 1s 
#include <bits/stdc++.h> 

using namespace std; 

// This function Prints the starting and ending 
// indexes of the largest subarray with equal 
// number of 0s and 1s. Also returns the size 
// of such subarray. 

int findSubArray(int arr[], int n) 
{ 
    int sum = 0; 
    int maxsize = -1, startindex; 

    // Pick a starting point as i 
    for (int i = 0; i < n - 1; i++) { 
        sum = (arr[i] == 0) ? -1 : 1; 

        // Consider all subarrays starting from i 
        for (int j = i + 1; j < n; j++) { 
            (arr[j] == 0) ? (sum += -1) : (sum += 1); 

            // If this is a 0 sum subarray, then 
            // compare it with maximum size subarray 
            // calculated so far 
            if (sum == 0 && maxsize < j - i + 1) { 
                maxsize = j - i + 1; 
                startindex = i; 
            } 
        } 
    } 
    if (maxsize == -1) 
        cout << "No such subarray"; 
    else
        cout << startindex << " to "
             << startindex + maxsize - 1; 

    return maxsize; 
} 

/* Driver code*/
int main() 
{ 
    int arr[] = { 1, 0, 0, 1, 0, 1, 1 }; 
    int size = sizeof(arr) / sizeof(arr[0]); 

    findSubArray(arr, size); 
    return 0; 
} 

// This code is contributed by rathbhupendra 

```

## C

```c

// A simple program to find the largest subarray 
// with equal number of 0s and 1s 

#include <stdio.h> 

// This function Prints the starting and ending 
// indexes of the largest subarray with equal 
// number of 0s and 1s. Also returns the size 
// of such subarray. 

int findSubArray(int arr[], int n) 
{ 
    int sum = 0; 
    int maxsize = -1, startindex; 

    // Pick a starting point as i 

    for (int i = 0; i < n - 1; i++) { 
        sum = (arr[i] == 0) ? -1 : 1; 

        // Consider all subarrays starting from i 

        for (int j = i + 1; j < n; j++) { 
            (arr[j] == 0) ? (sum += -1) : (sum += 1); 

            // If this is a 0 sum subarray, then 
            // compare it with maximum size subarray 
            // calculated so far 

            if (sum == 0 && maxsize < j - i + 1) { 
                maxsize = j - i + 1; 
                startindex = i; 
            } 
        } 
    } 
    if (maxsize == -1) 
        printf("No such subarray"); 
    else
        printf("%d to %d", startindex, startindex + maxsize - 1); 

    return maxsize; 
} 

/* Driver program to test above functions*/

int main() 
{ 
    int arr[] = { 1, 0, 0, 1, 0, 1, 1 }; 
    int size = sizeof(arr) / sizeof(arr[0]); 

    findSubArray(arr, size); 
    return 0; 
} 

```

## Java

```java

class LargestSubArray { 

    // This function Prints the starting and ending 
    // indexes of the largest subarray with equal 
    // number of 0s and 1s. Also returns the size 
    // of such subarray. 

    int findSubArray(int arr[], int n) 
    { 
        int sum = 0; 
        int maxsize = -1, startindex = 0; 
        int endindex = 0; 

        // Pick a starting point as i 

        for (int i = 0; i < n - 1; i++) { 
            sum = (arr[i] == 0) ? -1 : 1; 

            // Consider all subarrays starting from i 

            for (int j = i + 1; j < n; j++) { 
                if (arr[j] == 0) 
                    sum += -1; 
                else
                    sum += 1; 

                // If this is a 0 sum subarray, then 
                // compare it with maximum size subarray 
                // calculated so far 

                if (sum == 0 && maxsize < j - i + 1) { 
                    maxsize = j - i + 1; 
                    startindex = i; 
                } 
            } 
        } 
        endindex = startindex + maxsize - 1; 
        if (maxsize == -1) 
            System.out.println("No such subarray"); 
        else
            System.out.println(startindex + " to " + endindex); 

        return maxsize; 
    } 

    /* Driver program to test the above functions */

    public static void main(String[] args) 
    { 
        LargestSubArray sub; 
        sub = new LargestSubArray(); 
        int arr[] = { 1, 0, 0, 1, 0, 1, 1 }; 
        int size = arr.length; 

        sub.findSubArray(arr, size); 
    } 
} 

```

## Python3

```py

# A simple program to find the largest subarray 
# with equal number of 0s and 1s 

# This function Prints the starting and ending 
# indexes of the largest subarray with equal  
# number of 0s and 1s. Also returns the size  
# of such subarray. 
def findSubArray(arr, n): 

    sum = 0
    maxsize = -1

    # Pick a starting point as i 

    for i in range(0, n-1): 

        sum = -1 if(arr[i] == 0) else 1

        # Consider all subarrays starting from i 

        for j in range(i + 1, n): 

            sum = sum + (-1) if (arr[j] == 0) else sum + 1

            # If this is a 0 sum subarray, then  
            # compare it with maximum size subarray 
            # calculated so far 

            if (sum == 0 and maxsize < j-i + 1): 

                maxsize = j - i + 1
                startindex = i 

    if (maxsize == -1): 
        print("No such subarray"); 
    else: 
        print(startindex, "to", startindex + maxsize-1); 

    return maxsize 

# Driver program to test above functions 
arr = [1, 0, 0, 1, 0, 1, 1] 
size = len(arr) 
findSubArray(arr, size) 

# This code is contributed by Smitha Dinesh Semwal 

```

## C# 

```cs

// A simple program to find the largest subarray 
// with equal number of 0s and 1s 
using System; 

class GFG { 

    // This function Prints the starting and ending 
    // indexes of the largest subarray with equal 
    // number of 0s and 1s. Also returns the size 
    // of such subarray. 

    static int findSubArray(int[] arr, int n) 
    { 
        int sum = 0; 
        int maxsize = -1, startindex = 0; 
        int endindex = 0; 

        // Pick a starting point as i 
        for (int i = 0; i < n - 1; i++) { 
            sum = (arr[i] == 0) ? -1 : 1; 

            // Consider all subarrays starting from i 

            for (int j = i + 1; j < n; j++) { 
                if (arr[j] == 0) 
                    sum += -1; 
                else
                    sum += 1; 

                // If this is a 0 sum subarray, then 
                // compare it with maximum size subarray 
                // calculated so far 

                if (sum == 0 && maxsize < j - i + 1) { 
                    maxsize = j - i + 1; 
                    startindex = i; 
                } 
            } 
        } 
        endindex = startindex + maxsize - 1; 
        if (maxsize == -1) 
            Console.WriteLine("No such subarray"); 
        else
            Console.WriteLine(startindex + " to " + endindex); 

        return maxsize; 
    } 

    // Driver program 
    public static void Main() 
    { 

        int[] arr = { 1, 0, 0, 1, 0, 1, 1 }; 
        int size = arr.Length; 
        findSubArray(arr, size); 
    } 
} 

// This code is contributed by Sam007 

```

## PHP

```php

<?php  
// A simple program to find the  
// largest subarray with equal  
// number of 0s and 1s 

// This function Prints the starting  
// and ending indexes of the largest  
// subarray with equal number of 0s  
// and 1s. Also returns the size of  
// such subarray. 
function findSubArray(&$arr, $n) 
{ 
    $sum = 0; 
    $maxsize = -1; 

    // Pick a starting point as i 

    for ($i = 0; $i < $n - 1; $i++) 
    { 
        $sum = ($arr[$i] == 0) ? -1 : 1; 

        // Consider all subarrays 
        // starting from i 
        for ($j = $i + 1; $j < $n; $j++) 
        { 
            ($arr[$j] == 0) ?  
               ($sum += -1) : ($sum += 1); 

            // If this is a 0 sum subarray,  
            // then compare it with maximum  
            // size subarray calculated so far 

            if ($sum == 0 && $maxsize < $j - $i + 1) 
            { 
                $maxsize = $j - $i + 1; 
                $startindex = $i; 
            } 
        } 
    } 
    if ($maxsize == -1) 
        echo "No such subarray"; 
    else
        echo $startindex. " to " . 
            ($startindex + $maxsize - 1); 

    return $maxsize; 
} 

// Driver Code 
$arr = array(1, 0, 0, 1, 0, 1, 1); 
$size = sizeof($arr); 

findSubArray($arr, $size); 

// This coed is contributed  
// by ChitraNayal 
?> 

```

**输出**：

```
 0 to 5

```

**复杂度分析**：

*   **时间复杂度**：`O(n ^ 2)`。

    由于所有可能的子数组都是使用一对嵌套循环生成的。

*   **辅助空间**：`O(1)`。

    因为没有使用占用辅助空间的额外数据结构。

**方法 2**：[`HashMap`](http://www.geeksforgeeks.org/java-util-hashmap-in-java/) 。

**方法**：**以 0 为 -1 的累积和概念**将有助于我们优化该方法。 在求和时，有两种情况可以有一个子数组，其子数组的个数分别为 0 和 1。

1.  当累积总和`= 0`时，表示从索引（**0**）到当前索引的子数组具有相等数量的 **0 和 1**。

2.  当我们遇到之前已经遇到的累加总和值时，这意味着从**先前索引加一**到**当前索引**的子数组具有等于 0 和 1 的数量，他们给出的**总和为 0**。

简而言之，此问题等效于在`array[]`中找到两个索引`i & j`，使得`array[i] = array[j]`和（`j-i`）最大。 为了存储每个唯一累积总和值的第一次出现，我们使用`hash_map`，如果再次获得该值，我们可以找到子数组的大小，并将其与迄今为止找到的最大大小进行比较。

**算法**：

1.  令输入数组为大小为`n`的`arr[]`，`max_size`为输出子数组的大小。

2.  创建大小为`n`的临时数组`sumleft[]`。 将所有从`arr[0]`到`arr[i]`的元素的和存储在`sumleft[i]`中。

3.  有两种情况，输出子数组可能从第 0 个索引开始，也可能从其他索引开始。 我们将返回通过两种情况获得的最大值。

4.  要找到从第 0 个索引开始的最大长度子数组，请扫描`sumleft[]`并在`sumleft[i] = 0`的情况下找到最大`i`。

5.  现在，我们需要找到子数组`sum`等于 0 且起始索引不为 0 的子数组。此问题等效于在`sumleft[]`中找到两个索引`i & j`，使得`sumleft[i] = sumleft[j]`和`ji`最大。 为了解决这个问题，我们创建了一个大小为`max-min + 1`的哈希表，其中`min`是`sumleft[]`中的最小值，而`max`是`sumleft[]`中的最大值。 将`sumleft[]`中所有不同值的最左边出现的值散列。 哈希的大小选择为`max-min + 1`，因为`sumleft[]`中可能存在许多不同的可能值。 将哈希中的所有值初始化为 -1。

6.  要填充并使用`hash[]`，请将`sumleft[]`从 0 遍历到`n-1`。 如果`hash[]`中不存在值，则将其索引存储在`hash`中。 如果存在该值，则计算`sumleft[]`的当前索引与先前在`hash[]`中存储的值的差。 如果此差异大于`maxsize`，则更新`maxsize`。

7.  为了处理极端情况（全 1 和全 0），我们将`maxsize`初始化为 -1。 如果`maxsize`保持为 -1，则打印不存在此类子数组。

**伪代码**：

```
int sum_left[n]
Run a loop from i=0 to n-1
  if(arr[i]==0)
  sumleft[i] = sumleft[i-1]+-1
  else
  sumleft[i] = sumleft[i-1]+-1
        if (sumleft[i]  max)
            max = sumleft[i];

Run a loop from i=0 to n-1
 if (sumleft[i] == 0)
        {
           maxsize = i+1;
           startindex = 0;
        }

        // Case 2: fill hash table value. If already
        then use it

        if (hash[sumleft[i]-min] == -1)
            hash[sumleft[i]-min] = i;
        else
        {
            if ((i - hash[sumleft[i]-min]) > maxsize)
            {
                maxsize = i - hash[sumleft[i]-min];
                startindex = hash[sumleft[i]-min] + 1;
            }
        }

return maxsize

```

## C

```c

// A O(n) program to find the largest subarray 
// with equal number of 0s and 1s 

#include <stdio.h> 
#include <stdlib.h> 

// A utility function to get maximum of two 
// integers 

int max(int a, int b) { return a > b ? a : b; } 

// This function Prints the starting and ending 
// indexes of the largest subarray with equal 
// number of 0s and 1s. Also returns the size 
// of such subarray. 

int findSubArray(int arr[], int n) 
{ 
    // variables to store result values 

    int maxsize = -1, startindex; 

    // Create an auxiliary array sunmleft[]. 
    // sumleft[i] will be sum of array 
    // elements from arr[0] to arr[i] 

    int sumleft[n]; 

    // For min and max values in sumleft[] 

    int min, max; 
    int i; 

    // Fill sumleft array and get min and max 
    // values in it.  Consider 0 values in arr[] 
    // as -1 

    sumleft[0] = ((arr[0] == 0) ? -1 : 1); 
    min = arr[0]; 
    max = arr[0]; 
    for (i = 1; i < n; i++) { 
        sumleft[i] = sumleft[i - 1] 
                     + ((arr[i] == 0) ? -1 : 1); 
        if (sumleft[i] < min) 
            min = sumleft[i]; 
        if (sumleft[i] > max) 
            max = sumleft[i]; 
    } 

    // Now calculate the max value of j - i such 
    // that sumleft[i] = sumleft[j]. The idea is 
    // to create a hash table to store indexes of all 
    // visited values. 
    // If you see a value again, that it is a case of 
    // sumleft[i] = sumleft[j]. Check if this j-i is 
    // more than maxsize. 
    // The optimum size of hash will be max-min+1 as 
    // these many different values of sumleft[i] are 
    // possible. Since we use optimum size, we need 
    // to shift all values in sumleft[] by min before 
    // using them as an index in hash[]. 

    int hash[max - min + 1]; 

    // Initialize hash table 

    for (i = 0; i < max - min + 1; i++) 
        hash[i] = -1; 

    for (i = 0; i < n; i++) { 
        // Case 1: when the subarray starts from 
        // index 0 

        if (sumleft[i] == 0) { 
            maxsize = i + 1; 
            startindex = 0; 
        } 

        // Case 2: fill hash table value. If already 
        // filled, then use it 

        if (hash[sumleft[i] - min] == -1) 
            hash[sumleft[i] - min] = i; 
        else { 
            if ((i - hash[sumleft[i] - min]) > maxsize) { 
                maxsize = i - hash[sumleft[i] - min]; 
                startindex = hash[sumleft[i] - min] + 1; 
            } 
        } 
    } 
    if (maxsize == -1) 
        printf("No such subarray"); 
    else
        printf("%d to %d", startindex, 
               startindex + maxsize - 1); 

    return maxsize; 
} 

/* Driver program to test above functions */
int main() 
{ 
    int arr[] = { 1, 0, 0, 1, 0, 1, 1 }; 
    int size = sizeof(arr) / sizeof(arr[0]); 

    findSubArray(arr, size); 
    return 0; 
} 

```

## C++  / STL

```

// C++ program to find largest subarray with equal number of 
// 0's and 1's. 

#include <bits/stdc++.h> 
using namespace std; 

// Returns largest subarray with equal number of 0s and 1s 

int maxLen(int arr[], int n) 
{ 
    // Creates an empty hashMap hM 

    unordered_map<int, int> hM; 

    int sum = 0; // Initialize sum of elements 
    int max_len = 0; // Initialize result 
    int ending_index = -1; 

    for (int i = 0; i < n; i++) 
        arr[i] = (arr[i] == 0) ? -1 : 1; 

    // Traverse through the given array 

    for (int i = 0; i < n; i++) { 
        // Add current element to sum 

        sum += arr[i]; 

        // To handle sum=0 at last index 

        if (sum == 0) { 
            max_len = i + 1; 
            ending_index = i; 
        } 

        // If this sum is seen before, then update max_len 
        // if required 

        if (hM.find(sum + n) != hM.end()) { 
            if (max_len < i - hM[sum + n]) { 
                max_len = i - hM[sum + n]; 
                ending_index = i; 
            } 
        } 
        else // Else put this sum in hash table 
            hM[sum + n] = i; 
    } 

    for (int i = 0; i < n; i++) 
        arr[i] = (arr[i] == -1) ? 0 : 1; 

    printf("%d to %d\n", 
           ending_index - max_len + 1, ending_index); 

    return max_len; 
} 

// Driver method 

int main() 
{ 
    int arr[] = { 1, 0, 0, 1, 0, 1, 1 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 

    maxLen(arr, n); 
    return 0; 
} 

// This code is contributed by Aditya Goel 

```

## Java

```java

import java.util.HashMap; 

class LargestSubArray1 { 

    // Returns largest subarray with 
    // equal number of 0s and 1s 

    int maxLen(int arr[], int n) 
    { 
        // Creates an empty hashMap hM 

        HashMap<Integer, Integer> hM 
            = new HashMap<Integer, Integer>(); 

        // Initialize sum of elements 
        int sum = 0; 

        // Initialize result 
        int max_len = 0; 
        int ending_index = -1; 
        int start_index = 0; 

        for (int i = 0; i < n; i++) { 
            arr[i] = (arr[i] == 0) ? -1 : 1; 
        } 

        // Traverse through the given array 

        for (int i = 0; i < n; i++) { 
            // Add current element to sum 

            sum += arr[i]; 

            // To handle sum=0 at last index 

            if (sum == 0) { 
                max_len = i + 1; 
                ending_index = i; 
            } 

            // If this sum is seen before, 
            // then update max_len if required 
            if (hM.containsKey(sum + n)) { 
                if (max_len < i - hM.get(sum + n)) { 
                    max_len = i - hM.get(sum + n); 
                    ending_index = i; 
                } 
            } 
            else // Else put this sum in hash table 
                hM.put(sum + n, i); 
        } 

        for (int i = 0; i < n; i++) { 
            arr[i] = (arr[i] == -1) ? 0 : 1; 
        } 

        int end = ending_index - max_len + 1; 
        System.out.println(end + " to " + ending_index); 

        return max_len; 
    } 

    /* Driver program to test the above functions */
    public static void main(String[] args) 
    { 
        LargestSubArray1 sub = new LargestSubArray1(); 
        int arr[] = { 1, 0, 0, 1, 0, 1, 1 }; 
        int n = arr.length; 

        sub.maxLen(arr, n); 
    } 
} 

// This code has been by Mayank Jaiswal(mayank_24) 

```

## Python3

```py

# Python 3 program to find largest  
# subarray with equal number of  
# 0's and 1's.  

# Returns largest subarray with  
# equal number of 0s and 1s  
def maxLen(arr, n):  

    # NOTE: Dictonary in python in  
    # implemented as Hash Maps.  
    # Create an empty hash map (dictionary)  
    hash_map = {}   
    curr_sum = 0 
    max_len = 0 
    ending_index = -1 

    for i in range (0, n):  
        if(arr[i] == 0):  
            arr[i] = -1 
        else:  
            arr[i] = 1 

    # Traverse through the given array  
    for i in range (0, n):  

        # Add current element to sum  
        curr_sum = curr_sum + arr[i]  

        # To handle sum = 0 at last index  
        if (curr_sum == 0):  
            max_len = i + 1 
            ending_index = i  

        # If this sum is seen before,  
        if curr_sum in hash_map: 

            # If max_len is smaller than new subarray 
            # Update max_len and ending_index 
            if max_len < i - hash_map[curr_sum]: 
                max_len = i - hash_map[curr_sum] 
                ending_index = i 
        else:  

            # else put this sum in dictionary  
            hash_map[curr_sum] = i   

    for i in range (0, n):  
        if(arr[i] == -1):  
            arr[i] = 0 
        else:  
            arr[i] = 1 

    print (ending_index - max_len + 1, end =" ") 
    print ("to", end = " ") 
    print (ending_index) 

    return max_len 

# Driver Code  
arr = [1, 0, 0, 1, 0, 1, 1]  
n = len(arr)   

maxLen(arr, n)  

# This code is contributed  
# by Tarun Garg 

```

## C#

```cs

// C# program to find the largest subarray 
// with equal number of 0s and 1s 
using System; 
using System.Collections.Generic; 

class LargestSubArray1 { 

    // Returns largest subarray with 
    // equal number of 0s and 1s 
    public virtual int maxLen(int[] arr, int n) 
    { 

        // Creates an empty Dictionary hM 
        Dictionary<int, 
                   int> 
            hM = new Dictionary<int, 
                                int>(); 

        int sum = 0; // Initialize sum of elements 
        int max_len = 0; // Initialize result 
        int ending_index = -1; 
        int start_index = 0; 

        for (int i = 0; i < n; i++) { 
            arr[i] = (arr[i] == 0) ? -1 : 1; 
        } 

        // Traverse through the given array 
        for (int i = 0; i < n; i++) { 
            // Add current element to sum 
            sum += arr[i]; 

            // To handle sum=0 at last index 
            if (sum == 0) { 
                max_len = i + 1; 
                ending_index = i; 
            } 

            // If this sum is seen before, 
            // then update max_len 
            // if required 
            if (hM.ContainsKey(sum + n)) { 
                if (max_len < i - hM[sum + n]) { 
                    max_len = i - hM[sum + n]; 
                    ending_index = i; 
                } 
            } 

            else // Else put this sum in hash table 
            { 
                hM[sum + n] = i; 
            } 
        } 

        for (int i = 0; i < n; i++) { 
            arr[i] = (arr[i] == -1) ? 0 : 1; 
        } 

        int end = ending_index - max_len + 1; 
        Console.WriteLine(end + " to " + ending_index); 

        return max_len; 
    } 

    // Driver Code 
    public static void Main(string[] args) 
    { 

        LargestSubArray1 sub = new LargestSubArray1(); 
        int[] arr = new int[] { 
            1, 
            0, 
            0, 
            1, 
            0, 
            1, 
            1 
        }; 

        int n = arr.Length; 
        sub.maxLen(arr, n); 
    } 
} 

// This code is contributed by Shrikant13 

```

**输出**：

```

0 to 5

```

**复杂度分析**：

*   **时间复杂度**：`O(n)`。

    由于给定数组仅被遍历一次。

*   **辅助空间**：`O(n)`。

    由于使用了 **hash_map** ，因此需要额外的空间。

*感谢 Aashish Barnwal 提出此解决方案。*

