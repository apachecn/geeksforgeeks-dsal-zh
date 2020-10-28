# 用相同的按位 AND，OR 和 XOR 值计数子序列

我们给定了 n 个元素的数组 arr。 我们需要计算非空子序列的数量，以使这些单个子序列的按位与，或和异或值相同。 例如，如果（x | y | z）等于（x＆y＆z）和（x ^ y ^ z），我们需要计算一个子序列（x，y，z）。 对于单个元素子序列，我们将元素本身视为 XOR，AND 和 OR 的结果。 因此，所有单元素子序列始终被视为结果的一部分。

例子：

```
Input :  a = [1, 3, 7]
Output : 3
Explanation: 
There are 7 non empty subsequence .
subsequence   OR  AND  XOR
{1}            1    1    1
{3}            3    3    3
{7}            7    7    7
{1, 3}         3    1    2
{1, 7}         7    1    6
{3, 7}         7    3    4
{1, 3, 7}      7    1    5
Out of 7, there are 3 subsequences {1}
{3} {7} which have same values of AND, 
OR and XOR. 

Input :  a[] = [0, 0, 0]
Output : 7
Explanation:  All 7 non empty subsequences 
have same values of AND, OR and XOR. 

Input : a[] = [2, 2, 2, 3, 4]
Output : 6
Explanation:  subsequence {2}, {2}, {2},
{2, 2, 2}, {3}, {4} have same values of
AND, OR and XOR. 

```

1）如果给定数组中出现 n 个零，则将有 2 个 <sup>n</sup> –由这些零贡献的 1 个子序列。

2）如果存在 n 个非零元素 x，那么将有 2 个 <sup>n-1</sup> 子序列由该元素的出现所贡献。 请注意，在非零元素的情况下，对于位运算符，只有奇数次的出现会导致相同的结果。

查找数组中每个元素的计数，然后应用上述公式。

## C++

```cpp

#include <bits/stdc++.h> 
using namespace std; 

// function for finding count of  possible subsequence 
int countSubseq(int arr[], int n) 
{ 
    int count = 0; 

    // creating a map to count the frequency of each element 
    unordered_map<int, int> mp; 

    // store frequency of each element 
    for (int i = 0; i < n; i++) 
        mp[arr[i]]++; 

    // iterate through the map 
    for (auto i : mp) { 

        // add all possible combination for key equal zero 
        if (i.first == 0) 
            count += pow(2, i.second) - 1; 

        // add all (odd number of elements) possible  
        // combination for key other than zero 
        else
            count += pow(2, i.second - 1); 
    } 
    return count; 
} 

// driver function 
int main() 
{ 
    int arr[] = { 2, 2, 2, 5, 6 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    cout << countSubseq(arr, n); 
    return 0; 
} 

```

## Java

```java

import java .io.*;  
import java.util.*; 

class GFG { 

// function for finding count of  possible subsequence 
static int countSubseq(int arr[], int n) 
{ 
    int count = 0; 

    // creating a map to count the frequency of each element 
    HashMap<Integer,Integer>mp=new HashMap<Integer,Integer>(); 

    // store frequency of each element 
    for (int i = 0; i < n; i++) 
        if (mp.containsKey(arr[i])) 
            mp.put(arr[i],mp.get(arr[i])+1); 
        else
            mp.put(arr[i],1); 

    // iterate through the map 
    for (Map.Entry<Integer,Integer>entry:mp.entrySet()) { 

        // add all possible combination for key equal zero 
        if (entry.getKey() == 0) 
            count += Math.pow(2, entry.getValue()) - 1; 

        // add all (odd number of elements) possible  
        // combination for key other than zero 
        else
            count += Math.pow(2, entry.getValue()- 1); 
    } 
    return count; 
} 

// driver function 
public static void main(String[] args) 
{ 
    int arr[] = { 2, 2, 2, 5, 6 }; 
    int n=arr.length; 
    System.out.println(countSubseq(arr, n)); 
} 
} 

// This code is contributed by apurva raj 

```

## C#

```cs

using System; 
using System.Collections.Generic; 
class GFG{ 

// function for finding count of possible subsequence 
static int countSubseq(int []arr, int n) 
{ 
    int count = 0; 

    // creating a map to count the frequency of each element 
     Dictionary<int, int> mp = new Dictionary<int,int>(); 

    // store frequency of each element 
     for (int i = 0; i < n; i++)  
        {  
            if (mp.ContainsKey(arr[i]))   
            {  
                var val = mp[arr[i]];  
                mp.Remove(arr[i]);  
                mp.Add(arr[i], val + 1);   
            }   
            else
            {  
                mp.Add(arr[i], 1);  
            }  
        } 

    // iterate through the map 
    foreach(KeyValuePair<int, int> entry in mp) { 

        // add all possible combination for key equal zero 
        if (entry.Key == 0) 
            count += (int)(Math.Pow(2, entry.Value - 1)); 

        // add all (odd number of elements) possible  
        // combination for key other than zero 
        else
            count += (int)(Math.Pow(2, entry.Value - 1)); 
    } 
    return count; 
} 

// Driver function 
public static void Main(String []args)   
    { 
    int []arr = { 2, 2, 2, 5, 6 }; 
    int n = arr.Length; 
    Console.WriteLine(countSubseq(arr, n)); 
} 
} 

// This code is contributed by shivanisinghss2110 

```

## Python3

```py

# function for finding count of possible subsequence 
def countSubseq(arr, n): 
    count = 0

    # creating a map to count the frequency of each element 
    mp = {} 

    # store frequency of each element 
    for x in arr: 
        if x in mp.keys(): 
            mp[x]+=1
        else: 
            mp[x]=1

    # iterate through the map 
    for i in mp.keys(): 

        # add all possible combination for key equal zero 
        if (i == 0): 
            count += pow(2, mp[i]) - 1

        # add all (odd number of elements) possible  
        # combination for key other than zero 
        else: 
            count += pow(2, mp[i] - 1) 
    return count 

# Driver function 
arr= [2, 2, 2, 5, 6 ] 
n = len(arr) 
print(countSubseq(arr, n)) 

# This code is contributed by apurva raj 

```

**Output:**

```
6

```



* * *

* * *



