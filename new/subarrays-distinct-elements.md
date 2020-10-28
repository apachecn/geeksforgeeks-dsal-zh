# 具有不同元素的子阵列

给定一个数组，任务是计算所有元素都不同的连续子数组的长度之和。

**示例**：

```
Input :  arr[] = {1, 2, 3}
Output : 10
{1, 2, 3} is a subarray of length 3 with 
distinct elements. Total length of length
three = 3.
{1, 2}, {2, 3} are 2 subarray of length 2 
with distinct elements. Total length of 
lengths two = 2 + 2 = 4
{1}, {2}, {3} are 3 subarrays of length 1
with distinct element. Total lengths of 
length one = 1 + 1 + 1 = 3
Sum of lengths = 3 + 4 + 3 = 10

Input :  arr[] = {1, 2, 1}
Output : 7

Input :  arr[] = {1, 2, 3, 4}
Output : 20

```

一种简单的**解决方案**是考虑所有子阵列，并针对每个[子阵列检查其是否具有不同的元素或不使用哈希](http://quiz.geeksforgeeks.org/print-distinct-elements-given-integer-array/)。 并添加具有不同元素的所有子数组的长度。 如果我们使用哈希查找不同的元素，则在哈希搜索和插入操作花费 O（1）时间的假设下，此方法花费 O（n <sup>2</sup> ）时间。

**有效解决方案**基于以下事实：如果我们知道子数组 arr [i..j]中的所有元素都是不同的，则此子数组中不同元素子数组的所有长度之和为（（j- i + 1）*（j-i + 2））/ 2。 怎么样？ 子数组的可能长度为 1、2、3，……，j – i +1。 因此，总和为（（j – i +1）*（j – i +2））/ 2。

我们首先找到从第一个元素开始的最大子数组（具有不同的元素）。 我们使用上面的公式计算此子数组中的长度总和。 为了找到不同元素的下一个子数组，除非（i + 1，j）是不同的，否则我们增加起点 i 和终点 j。 如果不可能，那么我们再次增加 i 并以相同的方式前进。

以下是此方法的实现：

## C++

```cpp

// C++ program to calculate sum of lengths of subarrays 
// of distinct elements. 
#include<bits/stdc++.h> 
using namespace std; 

// Returns sum of lengths of all subarrays with distinct 
// elements. 
int sumoflength(int arr[], int n) 
{ 
    // For maintaining distinct elements. 
    unordered_set<int> s; 

    // Initialize ending point and result 
    int j = 0, ans = 0; 

    // Fix starting point 
    for (int i=0; i<n; i++) 
    { 
        // Find ending point for current subarray with 
        // distinct elements. 
        while (j < n && s.find(arr[j]) == s.end()) 
        { 
            s.insert(arr[j]); 
            j++; 
        } 

        // Calculating and adding all possible length 
        // subarrays in arr[i..j] 
        ans += ((j - i) * (j - i + 1))/2; 

        // Remove arr[i] as we pick new stating point 
        // from next 
        s.erase(arr[i]); 
    } 

    return ans; 
} 

// Driven Code 
int main() 
{ 
    int arr[] = {1, 2, 3, 4}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    cout << sumoflength(arr, n) << endl; 
    return 0; 
} 

```

## Java

```java

// Java program to calculate sum of lengths of subarrays  
// of distinct elements.  
import java.util.*; 

class geeks 
{ 

    // Returns sum of lengths of all subarrays 
    // with distinct elements. 
    public static int sumoflength(int[] arr, int n)  
    { 

        // For maintaining distinct elements. 
        Set<Integer> s = new HashSet<>(); 

        // Initialize ending point and result 
        int j = 0, ans = 0; 

        // Fix starting point 
        for (int i = 0; i < n; i++) 
        { 
            while (j < n && !s.contains(arr[j])) 
            { 
                s.add(arr[i]); 
                j++; 
            } 

            // Calculating and adding all possible length 
            // subarrays in arr[i..j] 
            ans += ((j - i) * (j - i + 1)) / 2; 

            // Remove arr[i] as we pick new stating point 
            // from next 
            s.remove(arr[i]); 
        } 

        return ans; 
    } 

    // Driver Code 
    public static void main(String[] args)  
    { 
        int[] arr = { 1, 2, 3, 4 }; 
        int n = arr.length; 

        System.out.println(sumoflength(arr, n)); 
    } 
} 

// This code is contributed by 
// sanjeev2552 

```

## Python 3

```

# Python 3 program to calculate sum of  
# lengths of subarrays of distinct elements. 

# Returns sum of lengths of all subarrays  
# with distinct elements. 
def sumoflength(arr, n): 

    # For maintaining distinct elements. 
    s = [] 

    # Initialize ending point and result 
    j = 0
    ans = 0

    # Fix starting point 
    for i in range(n): 

        # Find ending point for current  
        # subarray with distinct elements. 
        while (j < n and (arr[j] not in s)): 
            s.append(arr[j]) 
            j += 1

        # Calculating and adding all possible  
        # length subarrays in arr[i..j] 
        ans += ((j - i) * (j - i + 1)) // 2

        # Remove arr[i] as we pick new  
        # stating point from next 
        s.remove(arr[i]) 

    return ans 

# Driven Code 
if __name__=="__main__": 

    arr = [1, 2, 3, 4] 
    n = len(arr) 
    print(sumoflength(arr, n)) 

# This code is contributed by ita_c 

```c

## C#

```cs

// C# program to calculate sum of lengths of subarrays  
// of distinct elements 
using System; 
using System.Collections.Generic; 

public class geeks 
{ 

    // Returns sum of lengths of all subarrays 
    // with distinct elements. 
    public static int sumoflength(int[] arr, int n)  
    { 

        // For maintaining distinct elements. 
        HashSet<int> s = new HashSet<int>(); 

        // Initialize ending point and result 
        int j = 0, ans = 0; 

        // Fix starting point 
        for (int i = 0; i < n; i++) 
        { 
            while (j < n && !s.Contains(arr[j])) 
            { 
                s.Add(arr[i]); 
                j++; 
            } 

            // Calculating and adding all possible length 
            // subarrays in arr[i..j] 
            ans += ((j - i) * (j - i + 1)) / 2; 

            // Remove arr[i] as we pick new stating point 
            // from next 
            s.Remove(arr[i]); 
        } 

        return ans; 
    } 

    // Driver Code 
    public static void Main(String[] args)  
    { 
        int[] arr = { 1, 2, 3, 4 }; 
        int n = arr.Length; 

        Console.WriteLine(sumoflength(arr, n)); 
    } 
} 

/* This code is contributed by PrinciRaj1992 */

```

**Output:**

```
20

```

该解决方案的时间复杂度为 O（n）。 请注意，当 j 在所有外部循环中从 0 变为 n 时，内部循环总共运行 n 次。 因此，我们执行与 O（n）相同的 O（2n）操作。

本文由 **[Anuj Chauhan（anuj0503）](https://web.facebook.com/anuj0503)** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

