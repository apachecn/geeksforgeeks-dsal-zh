# 计算频率等于其值的元素

> 原文：[https://www.geeksforgeeks.org/count-the-elements-having-frequency-equals-to-its-value/](https://www.geeksforgeeks.org/count-the-elements-having-frequency-equals-to-its-value/)



给定一个大小为`N`的整数`arr[]`数组，任务是对频率等于其值的频率的所有元素进行计数。

**示例**：

> **输入**：`arr[] = {3, 2, 2, 3, 4, 3}`
>
> **输出**：2
>
> 元素 2 的频率为 2，
>
> 元素 3 的频率为 3，
>
> 元素 4 的频率为 1，
>
> 2 和 3 是具有与其值相同频率的元素。
> 
> **输入**：`arr[] = {1, 2, 3, 4, 5, 6}`
> **输出**：1

**方法**：使用[映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)存储数组的每个元素的[频率](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)，最后计数频率等于其值的所有那些元素。

下面是上述方法的实现：

## C++

```cpp

// C++ program to count the elements
// having frequency equals to its value

#include <bits/stdc++.h>
using namespace std;

// Function to find the count
int find_maxm(int arr[], int n)
{
    // Hash map for counting frquency
    map<int, int> mpp;

    for (int i = 0; i < n; i++) {

        // Counting freq of each element
        mpp[arr[i]] += 1;
    }

    int ans = 0;
    for (auto x : mpp) {
        int value = x.first;
        int freq = x.second;

        // Check if value equls to frequency
        // and increment the count
        if (value == freq) {
            ans++;
        }
    }

    return ans;
}

// Driver code
int main()
{
    int arr[] = { 3, 2, 2, 3, 4, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call
    cout << find_maxm(arr, n);

    return 0;
}

```

## Java

```java

// Java program to count the elements
// having frequency equals to its value
import java.util.*;

class GFG{

// Function to find the count
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
    for (Map.Entry<Integer,Integer> x : mp.entrySet()){
        int value = x.getKey();
        int freq = x.getValue();

        // Check if value equls to frequency
        // and increment the count
        if (value == freq) {
            ans++;
        }
    }

    return ans;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 3, 2, 2, 3, 4, 3 };
    int n = arr.length;

    // Function call
    System.out.print(find_maxm(arr, n)); 
}
}

// This code is contributed by Princi Singh

```

## Python3

```py

# Python3 program to count the elements
# having frequency equals to its value

# Function to find the count
def find_maxm(arr, n):

    # Hash map for counting frquency
    mpp = {}

    for i in range (0, n):

        # Counting freq of each element
        if arr[i] in mpp:
            mpp[arr[i]] = mpp[arr[i]] + 1
        else:
            mpp[arr[i]] = 1

    ans = 0

    for key in mpp:
        value = key
        freq = mpp[key]

        # Check if value equls to frequency
        # and increment the count
        if value == freq:
            ans = ans + 1

    return ans

# Driver code
if __name__ == "__main__":

    arr = [ 3, 2, 2, 3, 4, 3 ]
    n = len(arr)

    # Function call
    print(find_maxm(arr, n))

# This code is contributed by akhilsaini

```

## C#

```cs

// C# program to count the elements
// having frequency equals to its value
using System;
using System.Collections.Generic;

class GFG{

// Function to find the count
static int find_maxm(int []arr, int n)
{
    // Hash map for counting frquency
    Dictionary<int,int> mp = new Dictionary<int,int>();

    for (int i = 0; i < n; i++) {

        // Counting freq of each element
        if(mp.ContainsKey(arr[i])){
            mp[arr[i]] = mp[arr[i]] + 1;
        }else{
            mp.Add(arr[i], 1);
    }
    }

    int ans = 0;
    foreach (KeyValuePair<int,int> x in mp){
        int value = x.Key;
        int freq = x.Value;

        // Check if value equls to frequency
        // and increment the count
        if (value == freq) {
            ans++;
        }
    }

    return ans;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 3, 2, 2, 3, 4, 3 };
    int n = arr.Length;

    // Function call
    Console.Write(find_maxm(arr, n)); 
}
}

// This code is contributed by PrinciRaj1992

```

**输出**： 

```
2

```



* * *

* * *



