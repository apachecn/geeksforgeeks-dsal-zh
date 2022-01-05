# 仅通过插入元素

使长度为 K 的所有子阵列的和相等

> 原文:[https://www . geesforgeks . org/modify-给定数组使所有长度为 k 的子数组之和相等/](https://www.geeksforgeeks.org/modify-given-array-to-make-the-sum-of-all-subarrays-of-length-k-equal/)

给定一个长度为 **N** 的数组 **arr[]** ，使得(1 < = arr[i] < = N)，任务是通过仅插入范围**【1，N】**内的元素来修改数组，使得长度为 **K** 的所有子数组之和相等。如果可能，打印修改后的数组。否则打印“不可能”。
**举例:**

> **输入:** arr[] = {1，2，2，1}，K = 2
> **输出:**1 2 1 2 1
> T6】解释:
> 在第二个和第三个元素之间插入 1。
> 现在所有长度为 K 的子阵的和等于 3。
> **输入:** arr[] = {1，2，3，4}，K = 3
> **输出:**不可能

**进场:**

*   由于不允许移除元素，因此能够实现这种修改的数组的唯一情况是数组中最多有 K 个不同的元素。
*   因此，首先检查给定数组中是否有 K 个以上的不同元素。如果是，则打印“不可能”。
*   否则，将给定数组的所有不同元素存储在一个 T2 向量中。
*   如果不同元素的数量小于 K，那么在向量中添加/重复一些元素，使向量的大小等于 K。
*   向量现在有 K 个元素。现在以相同的顺序重复向量的元素，以显示修改后的数组。这样做是为了显示长度为 K 的所有子阵列具有相同的和。

下面是上述方法的实现

## C++

```
// C++ implementation of above approach

#include <bits/stdc++.h>
using namespace std;

// Function that prints another array
// whose all subarray of length k
// have an equal sum
void MakeArray(int a[], int n, int k)
{
    unordered_map<int, int> mp;

    // Store all distinct elements in
    // the unordered map
    for (int i = 0; i < n; i++) {
        if (mp.find(a[i]) == mp.end())
            mp[a[i]] = 1;
    }

    // Condition if the number of
    // distinct elements is greater
    // than k
    if (mp.size() > k) {
        cout << "Not possible\n";
        return;
    }

    vector<int> ans;

    // Push all distinct elements
    // in a vector
    for (auto i : mp) {
        ans.push_back(i.first);
    }

    // Push 1 while the size of
    // vector not equal to k
    while (ans.size() < k) {
        ans.push_back(1);
    }

    // Print the vector 2 times
    for (int i = 0; i < 2; i++) {
        for (int j = 0; j < k; j++)
            cout << ans[j] << " ";
    }
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 2, 1 };
    int K = 2;
    int size = sizeof(arr) / sizeof(arr[0]);

    MakeArray(arr, size, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.*;
class GFG{

// Function that prints another array
// whose all subarray of length k
// have an equal sum
static void MakeArray(int a[], int n, int k)
{
    HashMap<Integer,
              Integer> mp = new HashMap<Integer,
                                        Integer>();

    // Store all distinct elements in
    // the unordered map
    for (int i = 0; i < n; i++)
    {
        if (!mp.containsKey(a[i]))
            mp.put(a[i], 1);
    }

    // Condition if the number of
    // distinct elements is greater
    // than k
    if (mp.size() > k)
    {
        System.out.print("Not possible\n");
        return;
    }

    Vector<Integer> ans = new Vector<Integer>();

    // Push all distinct elements
    // in a vector
    for (Map.Entry<Integer,Integer> i : mp.entrySet())
    {
        ans.add(i.getKey());
    }

    // Push 1 while the size of
    // vector not equal to k
    while (ans.size() < k)
    {
        ans.add(1);
    }

    // Print the vector 2 times
    for (int i = 0; i < 2; i++)
    {
        for (int j = 0; j < k; j++)
            System.out.print(ans.get(j) + " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 2, 1 };
    int K = 2;
    int size = arr.length;

    MakeArray(arr, size, K);
}
}

// This code is contributed by Rohit_ranjan
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# Function that prints another array
# whose all subarray of length k
# have an equal sum
def MakeArray(a, n, k):
    mp = dict()

    # Store all distinct elements in
    # the unordered map
    for i in a:
        if i not in mp:
            mp[a[i]] = 1

    # Condition if the number of
    # distinct elements is greater
    # than k
    if(len(mp) > k):
       print("Not possible")
       return

    ans = []

    # Push all distinct elements
    # in a vector
    for i in mp:
        ans.append(i)

    # Push 1 while the size of
    # vector not equal to k
    while(len(ans) < k):
          ans.append(1)

    # Print the vector 2 times
    for i in range(2):
        for j in range(k):
            print(ans[j], end = " ")

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 2, 2, 1 ]
    K = 2
    size = len(arr)

    MakeArray(arr, size, K)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of above approach
using System;
using System.Collections.Generic;

class GFG{

// Function that prints another array
// whose all subarray of length k
// have an equal sum
static void MakeArray(int []a, int n, int k)
{
    Dictionary<int,
               int> mp = new Dictionary<int,
                                        int>();

    // Store all distinct elements in
    // the unordered map
    for(int i = 0; i < n; i++)
    {
        if (!mp.ContainsKey(a[i]))
             mp.Add(a[i], 1);
    }

    // Condition if the number of
    // distinct elements is greater
    // than k
    if (mp.Count > k)
    {
        Console.Write("Not possible\n");
        return;
    }

    List<int> ans = new List<int>();

    // Push all distinct elements
    // in a vector
    foreach(KeyValuePair<int, int> i in mp)
    {
        ans.Add(i.Key);
    }

    // Push 1 while the size of
    // vector not equal to k
    while (ans.Count < k)
    {
        ans.Add(1);
    }

    // Print the vector 2 times
    for(int i = 0; i < 2; i++)
    {
        for(int j = 0; j < k; j++)
            Console.Write(ans[j] + " ");
    }
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 1, 2, 2, 1 };
    int K = 2;
    int size = arr.Length;

    MakeArray(arr, size, K);
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// Function that prints another array
// whose all subarray of length k
// have an equal sum
function MakeArray(a, n, k)
{
    var mp = new Map();

    // Store all distinct elements in
    // the unordered map
    for (var i = 0; i < n; i++) {
        if (!mp.has(a[i]))
            mp.set(a[i], 1);
    }

    // Condition if the number of
    // distinct elements is greater
    // than k
    if (mp.count > k) {
        document.write( "Not possible<br>");
        return;
    }

    var ans = [];

    // Push all distinct elements
    // in a vector
    mp.forEach((value, key) => {
        ans.push(key);
    });

    // Push 1 while the size of
    // vector not equal to k
    while (ans.length < k) {
        ans.push(1);
    }

    // Print the vector 2 times
    for (var i = 0; i < 2; i++) {
        for (var j = 0; j < k; j++)
            document.write( ans[j] + " ");
    }
}

// Driver Code
var arr = [1, 2, 2, 1];
var K = 2;
var size = arr.length;
MakeArray(arr, size, K);

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
2 1 2 1
```