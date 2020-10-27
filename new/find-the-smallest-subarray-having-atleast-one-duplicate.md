# 查找具有至少一个重复的最小子数组

给定一个数组[rrG0] N 个元素，则任务是查找给定数组中包含至少一个重复元素的最小子数组的长度。 子数组由数组的连续元素形成。 如果不存在这样的数组，则打印“ -1”。

**示例：**

```
Input: arr = {1, 2, 3, 1, 5, 4, 5}
Output: 3
Explanation:

Input: arr = {4, 7, 11, 3, 1, 2, 4}
Output: 7
Explanation:

```

**天真的方法：**

*   诀窍是找到两个相等值的所有对。 由于这两个元素的值相等，因此包围它们的子数组将至少具有一个重复项，并且将是答案的候选者之一。
*   **的简单解决方案**是使用两个嵌套循环查找每对元素。如果两个元素相等，则更新到目前为止获得的最大长度。

下面是上述方法的实现：

## C++

```cpp

// C++ program to find 
// the smallest subarray having 
// atleast one duplicate 
#include <bits/stdc++.h> 
using namespace std; 

// Function to calculate 
// SubArray Length 
int subArrayLength(int arr[], int n) 
{ 

    int minLen = INT_MAX; 

    for (int i = 1; i < n; i++) { 
        for (int j = 0; j < i; j++) { 
            // If the two elements are equal, 
            // then the subarray arr[i..j] 
            // will definitely have a duplicate 
            if (arr[i] == arr[j]) { 
                // Update the minimum length 
                // obtained so far 
                minLen = min(minLen, i - j + 1); 
            } 
        } 
    } 
    if (minLen == INT_MAX) { 
        return -1; 
    } 

    return minLen; 
} 
// Driver Code 
int main() 
{ 
    int n = 7; 
    int arr[] = { 1, 2, 3, 1, 5, 4, 5 }; 

    int ans = subArrayLength(arr, n); 
    cout << ans << '\n'; 

    return 0; 
} 

```

## Java

```java

// Java program to find  
// the smallest subarray having  
// atleast one duplicate 

class GFG 
{ 

    final static int INT_MAX = Integer.MAX_VALUE; 

    // Function to calculate  
    // SubArray Length  
    static int subArrayLength(int arr[], int n)  
    {  

        int minLen = INT_MAX;  

        for (int i = 1; i < n; i++)  
        {  
            for (int j = 0; j < i; j++)  
            {  
                // If the two elements are equal,  
                // then the subarray arr[i..j]  
                // will definitely have a duplicate  
                if (arr[i] == arr[j])  
                {  
                    // Update the minimum length  
                    // obtained so far  
                    minLen = Math.min(minLen, i - j + 1);  
                }  
            }  
        }  
        if (minLen == INT_MAX) 
        {  
            return -1;  
        }  

        return minLen;  
    }  

    // Driver Code  
    public static void main(String[] args) 
    {  
        int n = 7;  
        int arr[] = { 1, 2, 3, 1, 5, 4, 5 };  

        int ans = subArrayLength(arr, n);  
        System.out.println(ans);  

    }  
} 

// This code is contributed by AnkitRai01 

```

## 蟒蛇

```

# Python program for above approach 
n = 7
arr = [1, 2, 3, 1, 5, 4, 5] 
minLen = n + 1

for i in range(1, n): 
    for j in range(0, i): 
        if arr[i]== arr[j]: 
            minLen = min(minLen, i-j + 1) 

if minLen == n + 1: 
       print("-1") 
else: 
       print(minLen) 

```

## C#

```cs

// C# program to find  
// the smallest subarray having  
// atleast one duplicate 
using System; 

class GFG 
{ 

    static int INT_MAX = int.MaxValue; 

    // Function to calculate  
    // SubArray Length  
    static int subArrayLength(int []arr, int n)  
    {  

        int minLen = INT_MAX;  

        for (int i = 1; i < n; i++)  
        {  
            for (int j = 0; j < i; j++)  
            {  
                // If the two elements are equal,  
                // then the subarray arr[i..j]  
                // will definitely have a duplicate  
                if (arr[i] == arr[j])  
                {  
                    // Update the minimum length  
                    // obtained so far  
                    minLen = Math.Min(minLen, i - j + 1);  
                }  
            }  
        }  
        if (minLen == INT_MAX) 
        {  
            return -1;  
        }  

        return minLen;  
    }  

    // Driver Code  
    public static void Main() 
    {  
        int n = 7;  
        int []arr = { 1, 2, 3, 1, 5, 4, 5 };  

        int ans = subArrayLength(arr, n);  
        Console.WriteLine(ans);  

    }  
} 

// This code is contributed by AnkitRai01 

```

**Output:**

```
3

```

**时间复杂度：** O（N <sup>2</sup> ）

**有效方法：**

使用**散列**技术的思想，可以在 **O（N）**时间和 **O（N）**辅助空间中解决此问题。 想法是以线性方式遍历数组的每个元素，对于每个元素，使用哈希图找到其最后一次出现，然后使用最后一次出现与当前索引之间的差来更新最小长度的值。 同样，用当前索引的值更新元素最后一次出现的值。

下面是上述方法的实现：

## C++

```cpp

// C++ program to find 
// the smallest subarray having 
// atleast one duplicate 
#include <bits/stdc++.h> 
using namespace std; 

// Function to calculate 
// SubArray Length 
int subArrayLength(int arr[], int n) 
{ 

    int minLen = INT_MAX; 
    // Last stores the index of the last 
    // occurrence of the corresponding value 
    unordered_map<int, int> last; 

    for (int i = 0; i < n; i++) { 
        // If the element has already occurred 
        if (last[arr[i]] != 0) { 
            minLen = min(minLen, i - last[arr[i]] + 2); 
        } 
        last[arr[i]] = i + 1; 
    } 
    if (minLen == INT_MAX) { 
        return -1; 
    } 

    return minLen; 
} 

// Driver Code 
int main() 
{ 
    int n = 7; 
    int arr[] = { 1, 2, 3, 1, 5, 4, 5 }; 

    int ans = subArrayLength(arr, n); 
    cout << ans << '\n'; 

    return 0; 
} 

```

## Java

```java

// Java program to find 
// the smallest subarray having 
// atleast one duplicate 
import java.util.*; 

class GFG  
{ 

    // Function to calculate 
    // SubArray Length 
    static int subArrayLength(int arr[], int n) 
    { 

        int minLen = Integer.MAX_VALUE; 

        // Last stores the index of the last 
        // occurrence of the corresponding value 
        HashMap<Integer, Integer> last = new HashMap<Integer, Integer>(); 

        for (int i = 0; i < n; i++)  
        { 
            // If the element has already occurred 
            if (last.containsKey(arr[i]) && last.get(arr[i]) != 0)  
            { 
                minLen = Math.min(minLen, i - last.get(arr[i]) + 2); 
            } 
            last.put(arr[i], i + 1); 
        } 
        if (minLen == Integer.MAX_VALUE) 
        { 
            return -1; 
        } 

        return minLen; 
    } 

    // Driver Code 
    public static void main(String[] args)  
    { 
        int n = 7; 
        int arr[] = { 1, 2, 3, 1, 5, 4, 5 }; 

        int ans = subArrayLength(arr, n); 
        System.out.print(ans); 
    } 
} 

// This code is contributed by 29AjayKumar 

```

## 蟒蛇

```

# Python program for above approach 

n = 7
arr = [1, 2, 3, 1, 5, 4, 5] 

last = dict() 

minLen = n + 1

for i in range(0, n): 
    if arr[i] in last: 
        minLen = min(minLen, i-last[arr[i]]+2) 

    last[arr[i]]= i + 1    

if minLen == n + 1: 
       print("-1") 
else: 
       print(minLen) 

```

## C#

```cs

// C# program to find 
// the smallest subarray having 
// atleast one duplicate 
using System; 
using System.Collections.Generic; 

class GFG  
{ 

    // Function to calculate 
    // SubArray Length 
    static int subArrayLength(int []arr, int n) 
    { 

        int minLen = int.MaxValue; 

        // Last stores the index of the last 
        // occurrence of the corresponding value 
        Dictionary<int, int> last = new Dictionary<int, int>(); 

        for (int i = 0; i < n; i++)  
        { 
            // If the element has already occurred 
            if (last.ContainsKey(arr[i]) && last[arr[i]] != 0)  
            { 
                minLen = Math.Min(minLen, i - last[arr[i]] + 2); 
            } 
            if(last.ContainsKey(arr[i])) 
                last[arr[i]] = i + 1; 
            else
                last.Add(arr[i], i + 1); 
        } 
        if (minLen == int.MaxValue) 
        { 
            return -1; 
        } 

        return minLen; 
    } 

    // Driver Code 
    public static void Main(String[] args)  
    { 
        int n = 7; 
        int []arr = { 1, 2, 3, 1, 5, 4, 5 }; 

        int ans = subArrayLength(arr, n); 
        Console.Write(ans); 
    } 
} 

// This code is contributed by PrinciRaj1992 

```

**Output:**

```
3

```

**时间复杂度：** O（N），其中 N 是数组的大小



* * *

* * *



