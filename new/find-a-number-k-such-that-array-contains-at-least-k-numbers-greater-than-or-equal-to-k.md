# 找到一个数字`K`，以便数组包含至少 K 个大于或等于 K 的数字

> 原文：[https://www.geeksforgeeks.org/find-a-number-k-such-that-array-contains-at-least-k-numbers-greater-than-or-equal-to-k/](https://www.geeksforgeeks.org/find-a-number-k-such-that-array-contains-at-least-k-numbers-greater-than-or-equal-to-k/)

给定大小为`N`的非负整数的数组`arr[]`，任务是找到一个整数`H`，以便该数组中至少有`K`个整数大于或等于`K`。

**示例**：

> **输入**：`arr[] = [3, 0, 6, 1, 5]`
>
> **输出**：3
>
> **说明**：有 3 个数字 大于或等于 3 的数组，即 3、6 和 5。
> 
> **输入**：`arr[] = [9, 10, 7, 5, 0, 10, 2, 0]`
>
> **输出**：5

**方法**：使用[散列](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)，

整数`K`不能大于`arr[]`的大小。 因此，请维护频率数组（哈希表）中每个元素的频率。 然后从末尾遍历频率数组，并返回与条件匹配的第一个索引。

下面是上述方法的实现。

## C++

```cpp

// C++ program for the above approach 

#include <bits/stdc++.h> 
using namespace std; 

int getNumberK(vector<int>& S) 
{ 
    // vector to store freq. 
    vector<int> freq(S.size() + 1, 
                     0); 

    // Filling freq vector. 
    for (int i = 0; i < S.size(); 
         i++) { 

        if (S[i] < S.size()) 
            freq[S[i]]++; 
        else
            freq[S.size()]++; 
    } 

    int total = 0; 

    // Finding K number. 
    for (int i = S.size(); i >= 0; 
         i--) { 

        total += freq[i]; 
        if (total >= i) 
            return i; 
    } 

    // No K number found. 
    return 0; 
} 

// Driver code 
int main() 
{ 
    vector<int> arr{ 3, 0, 6, 1, 5 }; 
    cout << getNumberK(arr) << '\n'; 
    return 0; 
} 

```

## Java

```java

// Java program for the above approach 
import java.util.*; 

class GFG{ 

static int getNumberK(ArrayList<Integer> S) 
{ 

    // To store freq. 
    int[] freq = new int[S.size() + 1]; 

    // Filling freq vector. 
    for(int i = 0; i < S.size(); i++) 
    { 
        if (S.get(i) < S.size()) 
            freq[S.get(i)]++; 
        else
            freq[S.size()]++; 
    } 

    int total = 0; 

    // Finding K number. 
    for(int i = S.size(); i >= 0; i--) 
    { 
        total += freq[i]; 
        if (total >= i) 
            return i; 
    } 

    // No K number found. 
    return 0; 
} 

// Driver code 
public static void main(String[] args) 
{ 
    ArrayList<Integer> arr =  
          new ArrayList<>(Arrays.asList(3, 0, 6, 1, 5)); 

    System.out.println(getNumberK(arr)); 
} 
} 

// This code is contributed by offbeat 

```

## Python3

```py

# Python3 program for the above approach 
def getNumberK(S):  

    # Vector to store freq.  
    freq = [0] * (len(S) + 1) 

    # Filling freq vector.  
    for i in range(len(S)):  
        if (S[i] < len(S)):  
            freq[S[i]] += 1
        else: 
            freq[len(S)] += 1

    total = 0

    # Finding K number.  
    for i in range(len(S), -1, -1):  
        total += freq[i]  

        if (total >= i): 
            return i  

    # No K number found.  
    return 0

# Driver code  
arr = [ 3, 0, 6, 1, 5 ]  

print(getNumberK(arr)) 

# This code is contributed by code_hunt 

```

## C#

```cs

// C# program for the above approach 
using System; 
using System.Collections.Generic; 

class GFG{ 

static int getNumberK(List<int> S) 
{ 

    // To store freq. 
    int[] freq = new int[S.Count + 1]; 

    // Filling freq vector. 
    for(int i = 0; i < S.Count; i++) 
    { 
        if (S[i] < S.Count) 
            freq[S[i]]++; 
        else
            freq[S.Count]++; 
    } 

    int total = 0; 

    // Finding K number. 
    for(int i = S.Count; i >= 0; i--) 
    { 
        total += freq[i]; 
        if (total >= i) 
            return i; 
    } 

    // No K number found. 
    return 0; 
} 

// Driver code 
public static void Main(String[] args) 
{ 
    List<int> arr = new List<int>{ 3, 0, 6, 1, 5 }; 

    Console.WriteLine(getNumberK(arr)); 
} 
} 

// This code is contributed by Amit Katiyar 

```

**输出**： 

```
3

```

**时间复杂度**`O(n)`。

**空间复杂度**`O(n)`。



* * *

* * *



