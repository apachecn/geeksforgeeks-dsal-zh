# 数组中的最大元素，等于其频率

给定一个大小为 **N** 的整数 **arr []** 数组，任务是在数组中查找其频率等于其值的最大元素

**示例：**

> **输入：** arr [] = {3，2，2，3，4，3}
> **输出：** 3
> 元素 2 的频率为 2
> 频率 元素 3 的频率为 3
> 元素 4 的频率为 1
> 。2 和 3 是与其值具有相同频率的元素，最大为 3。
> 
> **输入：** arr [] = {1、2、3、4、5、6}
> **输出：** 1

**方法：**使用[映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)存储数组的每个元素的[频率，最后找出那些频率等于其值的元素的最大值。](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)

下面是上述方法的实现：

## CPP

```

// C++ program to find the maximum element  
// whose frequency equals to it’s value 

#include <bits/stdc++.h> 
using namespace std; 

// Function to find the maximum element  
// whose frequency equals to it’s value 
int find_maxm(int arr[], int n) 
{ 
    // Hash map for counting frquency 
    map<int, int> mpp; 

    for (int i = 0; i < n; i++) { 
        // Counting freq of each element 
        mpp[arr[i]] += 1; 
    } 

    int ans = 0; 
    for (auto x : mpp) 
    { 
        int value = x.first; 
        int freq = x.second; 

        // Check if value equls to frequency 
        // and it is the maximum element or not 
        if (value == freq) { 
            ans = max(ans, value); 
        } 
    } 

    return ans; 
} 

// Driver code 
int main() 
{ 
    int arr[] = { 3, 2, 2, 3, 4, 3 }; 

    // Size of array 
    int n = sizeof(arr) / sizeof(arr[0]); 

    // Function call 
    cout << find_maxm(arr, n); 

    return 0; 
} 

```

## Java

```java

// Java program to find the maximum element  
// whose frequency equals to it’s value 
import java.util.*; 

class GFG{ 

// Function to find the maximum element  
// whose frequency equals to it’s value 
static int find_maxm(int arr[], int n) 
{ 
    // Hash map for counting frquency 
    HashMap<Integer,Integer> mp = new HashMap<Integer,Integer>(); 

    for (int i = 0; i < n; i++) { 

        // Counting freq of each element 
        if(mp.containsKey(arr[i])){ 
            mp.put(arr[i], mp.get(arr[i])+1); 
        }else{ 
            mp.put(arr[i], 1); 
    } 
    } 

    int ans = 0; 
    for (Map.Entry<Integer,Integer> x : mp.entrySet()) 
    { 
        int value = x.getKey(); 
        int freq = x.getValue(); 

        // Check if value equls to frequency 
        // and it is the maximum element or not 
        if (value == freq) { 
            ans = Math.max(ans, value); 
        } 
    } 

    return ans; 
} 

// Driver code 
public static void main(String[] args) 
{ 
    int arr[] = { 3, 2, 2, 3, 4, 3 }; 

    // Size of array 
    int n = arr.length; 

    // Function call 
    System.out.print(find_maxm(arr, n)); 

} 
} 

// This code is contributed by 29AjayKumar 

```

## Python3

```py

# Python3 program to find the maximum element  
# whose frequency equals to it’s value  

# Function to find the maximum element  
# whose frequency equals to it’s value  
def find_maxm(arr, n) : 

    # Hash map for counting frquency  
    mpp = {} 

    for i in range(0,n): 
        # Counting freq of each element  
        if(arr[i] in mpp): 
            mpp.update( {arr[i] : mpp[arr[i]] + 1} ) 
        else: 
            mpp[arr[i]] = 1

    ans = 0
    for value,freq in mpp.items(): 
        # Check if value equls to frequency  
        # and it is the maximum element or not  
        if (value == freq): 
            ans = max(ans, value) 

    return ans 

# Driver code  
arr = [ 3, 2, 2, 3, 4, 3 ] 

# Size of array  
n = len(arr) 

# Function call  
print(find_maxm(arr, n)) 

# This code is contributed by Sanjit_Prasad 

```

## C#

```cs

// C# program to find the maximum element  
// whose frequency equals to it’s value 
using System; 
using System.Collections.Generic; 

class GFG{ 

// Function to find the maximum element  
// whose frequency equals to it’s value 
static int find_maxm(int []arr, int n) 
{ 
    // Hash map for counting frquency 
    Dictionary<int,int> mp = new Dictionary<int,int>(); 

    for (int i = 0; i < n; i++) { 

        // Counting freq of each element 
        if(mp.ContainsKey(arr[i])){ 
            mp[arr[i]] = mp[arr[i]]+1; 
        }else{ 
            mp.Add(arr[i], 1); 
    } 
    } 

    int ans = 0; 
    foreach (KeyValuePair<int,int> x in mp) 
    { 
        int value = x.Key; 
        int freq = x.Value; 

        // Check if value equls to frequency 
        // and it is the maximum element or not 
        if (value == freq) { 
            ans = Math.Max(ans, value); 
        } 
    } 

    return ans; 
} 

// Driver code 
public static void Main(String[] args) 
{ 
    int []arr = { 3, 2, 2, 3, 4, 3 }; 

    // Size of array 
    int n = arr.Length; 

    // Function call 
    Console.Write(find_maxm(arr, n)); 
} 
} 

// This code is contributed by Rajput-Ji 

```

**Output:**

```
3

```



* * *

* * *



