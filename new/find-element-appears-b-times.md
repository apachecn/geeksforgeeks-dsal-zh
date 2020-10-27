# 查找出现 b 次的唯一元素

给定一个数组，其中每个元素出现一次，除了一个元素出现 b（a> b）次。 找到发生 b 次的元素。

**示例**：

```
Input : arr[]  = [1, 1, 2, 2, 2, 3, 3, 3]
         a = 3, b = 2
Output : 1

```

将每个数字相加一次，然后将总和乘以 a，我们将得到数组每个元素之和的乘积。 将其存储为 a_sum。 从 a_sum 中减去整个数组的总和，然后将结果除以（a-b）。 我们得到的数字是必需的数字（在数组中出现 b 次）。

## C++

```cpp

// CPP program to find the only element that  
// appears b times 
#include <bits/stdc++.h> 
using namespace std; 

int appearsbTimes(int arr[], int n, int a, int b) 
{ 
    unordered_set<int> s; 

    int a_sum = 0, sum = 0; 

    for (int i = 0; i < n; i++) { 
        if (s.find(arr[i]) == s.end()) { 
            s.insert(arr[i]); 
            a_sum += arr[i]; 
        } 

        sum += arr[i]; 
    } 

    a_sum = a * a_sum; 

    return ((a_sum - sum) / (a - b)); 
} 

int main() 
{ 
    int arr[] = { 1, 1, 2, 2, 2, 3, 3, 3 }; 
    int a = 3, b = 2; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    cout << appearsbTimes(arr, n, a, b); 
    return 0; 
} 

```

## Java

```java

// Java program to find the only element that  
// appears b times 
import java.util.*; 

class GFG  
{ 
static int appearsbTimes(int arr[], int n,  
                         int a, int b) 
{ 
    HashSet<Integer> s = new HashSet<Integer>(); 

    int a_sum = 0, sum = 0; 

    for (int i = 0; i < n; i++) 
    { 
        if (!s.contains(arr[i])) 
        { 
            s.add(arr[i]); 
            a_sum += arr[i]; 
        } 

        sum += arr[i]; 
    } 
    a_sum = a * a_sum; 

    return ((a_sum - sum) / (a - b)); 
} 

// Driver Code 
public static void main(String[] args)  
{ 
    int arr[] = { 1, 1, 2, 2, 2, 3, 3, 3 }; 
    int a = 3, b = 2; 
    int n = arr.length; 
    System.out.println(appearsbTimes(arr, n, a, b)); 
} 
} 

// This code is contributed by 29AjayKumar 

```

## Python3

```py

# Python3 program to find the only  
# element that appears b times 
def appearsbTimes(arr, n, a, b): 

    s = dict() 

    a_Sum = 0
    Sum = 0

    for i in range(n): 
        if (arr[i] not in s.keys()): 
            s[arr[i]] = 1
            a_Sum += arr[i] 

        Sum += arr[i] 

    a_Sum = a * a_Sum 

    return ((a_Sum - Sum) // (a - b)) 

# Driver code 
arr = [1, 1, 2, 2, 2, 3, 3, 3] 
a, b = 3, 2
n = len(arr) 
print(appearsbTimes(arr, n, a, b)) 

# This code is contributed by mohit kumar 

```

## C#

```cs

// C# program to find the only element that  
// appears b times 
using System; 
using System.Collections.Generic; 

class GFG  
{ 

static int appearsbTimes(int []arr, int n,  
                        int a, int b) 
{ 
    HashSet<int> s = new HashSet<int>(); 

    int a_sum = 0, sum = 0; 

    for (int i = 0; i < n; i++) 
    { 
        if (!s.Contains(arr[i])) 
        { 
            s.Add(arr[i]); 
            a_sum += arr[i]; 
        } 

        sum += arr[i]; 
    } 
    a_sum = a * a_sum; 

    return ((a_sum - sum) / (a - b)); 
} 

// Driver Code 
public static void Main(String[] args)  
{ 
    int []arr = { 1, 1, 2, 2, 2, 3, 3, 3 }; 
    int a = 3, b = 2; 
    int n = arr.Length; 
    Console.WriteLine(appearsbTimes(arr, n, a, b)); 
} 
} 

// This code is contributed by Princi Singh 

```

**Output:**

```
1

```

请参考下面的文章以了解更多方法。

[查找出现 k 次的唯一元素。](https://www.geeksforgeeks.org/find-unique-element-element-occurs-k-times-except-one/)



* * *

* * *



