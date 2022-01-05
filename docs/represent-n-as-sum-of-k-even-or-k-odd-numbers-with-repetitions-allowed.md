# 将 N 表示为 K 个偶数或 K 个奇数的和，允许重复

> 原文:[https://www . geesforgeks . org/representative-n-as-sum-k-偶数或-k-奇数-带重复-允许/](https://www.geeksforgeeks.org/represent-n-as-sum-of-k-even-or-k-odd-numbers-with-repetitions-allowed/)

给定两个整数 **N** 和 **K** ，任务是找到一个大小为 K 的数组，其中只包含偶数或奇数元素，数组中所有元素的和为 N。如果没有这样的数组，则打印“否”。
**例:**

> **输入:** N = 18，K = 3
> T3】输出:6 6 6
> T6】输入: N = 19，K = 5
> T9】输出: 3 3 3 3 7

**方法:**思路是选择最小的偶数或奇数 K-1 次，最后借助总和计算最后一个数。如果最后一个数对于偶数也是偶数，对于最小的奇数也是奇数。那么就有可能选择这样的阵列。否则，就不可能有这样的数组。
以下是上述办法的实施情况:

## C++

```
// C++ implementation to find an
// array of size K with all the
// even or odd elements in the array

#include <bits/stdc++.h>
using namespace std;

// Function to find the array with
// all the even / odd elements
void getArrayOfSizeK(int n, int k)
{
    vector<int> ans;

    // If array could be constructed
    // by adding odd elements
    // we need to find the kth
    // element is odd or even

    // if array of odd elements
    // would be the answer then
    // k-1 elements would be 1

    // First let's check
    // kth is odd or even
    int odd = n - ((k - 1) * 1);

    // if last element is also
    // an odd number then
    // we can choose odd
    // elements for our answer
    if (odd > 0
        && odd % 2 != 0) {

        // Add 1 in the array (k-1) times
        for (int i = 0; i < k - 1; i++) {
            ans.push_back(1);
        }

        // Add last odd element
        ans.push_back(odd);
    }

    // If array of even elements
    // would be the answer then
    // k-1 elements would be 2
    int even = n - ((k - 1) * 2);

    // if last element is also
    // an even number then
    // we can choose even
    // elements for our answer
    if (even > 0
        && even % 2 == 0
        && ans.size() == 0) {

        // Add 2 in the array (k-1) times
        for (int i = 0; i < k - 1; i++) {
            ans.push_back(2);
        }

        // Add last even element
        ans.push_back(even);
    }

    // Printing the array
    if (ans.size() > 0) {
        for (int i = 0; i < k; i++) {
            cout << ans[i] << " ";
        }
    }
    else {
        cout << "NO" << endl;
    }
}

// Driver Code
int main()
{
    int n = 10, k = 3;
    getArrayOfSizeK(n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find an
// array of size K with all the
// even or odd elements in the array
import java.util.*;

class GFG{

// Function to find the array with
// all the even / odd elements
static void getArrayOfSizeK(int n, int k)
{
    Vector<Integer> ans = new Vector<Integer>();

    // If array could be constructed
    // by adding odd elements
    // we need to find the kth
    // element is odd or even

    // If array of odd elements
    // would be the answer then
    // k-1 elements would be 1

    // First let's check
    // kth is odd or even
    int odd = n - ((k - 1) * 1);

    // If last element is also
    // an odd number then
    // we can choose odd
    // elements for our answer
    if (odd > 0 && odd % 2 != 0)
    {

        // Add 1 in the array (k-1) times
        for(int i = 0; i < k - 1; i++)
        {
           ans.add(1);
        }

        // Add last odd element
        ans.add(odd);
    }

    // If array of even elements
    // would be the answer then
    // k-1 elements would be 2
    int even = n - ((k - 1) * 2);

    // If last element is also
    // an even number then
    // we can choose even
    // elements for our answer
    if (even > 0 && even % 2 == 0 &&
                  ans.size() == 0)
    {

        // Add 2 in the array (k-1) times
        for(int i = 0; i < k - 1; i++)
        {
           ans.add(2);
        }

        // Add last even element
        ans.add(even);
    }

    // Printing the array
    if (ans.size() > 0)
    {
        for(int i = 0; i < k; i++)
        {
           System.out.print(ans.get(i) + " ");
        }
    }
    else
    {
        System.out.println("NO");
    }
}

// Driver code
public static void main(String args[])
{
    int n = 10, k = 3;

    getArrayOfSizeK(n, k);
}
}

// This code is contributed by Surendra_Gangwar
```

## 蟒蛇 3

```
# Python 3 implementation to find an
# array of size K with all the
# even or odd elements in the array

# Function to find the array with
# all the even / odd elements
def getArrayOfSizeK(n, k):

    ans = []

    # If array could be constructed
    # by adding odd elements
    # we need to find the kth
    # element is odd or even

    # if array of odd elements
    # would be the answer then
    # k-1 elements would be 1

    # First let's check
    # kth is odd or even
    odd = n - ((k - 1) * 1)

    # if last element is also
    # an odd number then
    # we can choose odd
    # elements for our answer
    if (odd > 0
        and odd % 2 != 0):

        # Add 1 in the array (k-1) times
        for i in range(k - 1):
            ans.append(1)

        # Add last odd element
        ans.append(odd)

    # If array of even elements
    # would be the answer then
    # k-1 elements would be 2
    even = n - ((k - 1) * 2)

    # if last element is also
    # an even number then
    # we can choose even
    # elements for our answer
    if (even > 0
        and even % 2 == 0
        and len(ans) == 0):

        # Add 2 in the array (k-1) times
        for i in range(k - 1):
            ans.append(2)

        # Add last even element
        ans.append(even)

    # Printing the array
    if (len(ans) > 0):
        for i in range( k):
            print (ans[i], end = " ")

    else :
        print ("NO")

# Driver Code
if __name__=="__main__":
    n, k = 10, 3
    getArrayOfSizeK(n, k)

# This code is contributed by chitranayal
```

## C#

```
// C# implementation to find an
// array of size K with all the
// even or odd elements in the array
using System;
using System.Collections.Generic;

class GFG{

// Function to find the array with
// all the even / odd elements
static void getArrayOfSizeK(int n, int k)
{
    List<int> ans = new List<int>();

    // If array could be constructed
    // by adding odd elements
    // we need to find the kth
    // element is odd or even

    // If array of odd elements
    // would be the answer then
    // k-1 elements would be 1

    // First let's check
    // kth is odd or even
    int odd = n - ((k - 1) * 1);

    // If last element is also
    // an odd number then
    // we can choose odd
    // elements for our answer
    if (odd > 0 && odd % 2 != 0)
    {

        // Add 1 in the array (k-1) times
        for(int i = 0; i < k - 1; i++)
        {
           ans.Add(1);
        }

        // Add last odd element
        ans.Add(odd);
    }

    // If array of even elements
    // would be the answer then
    // k-1 elements would be 2
    int even = n - ((k - 1) * 2);

    // If last element is also
    // an even number then
    // we can choose even
    // elements for our answer
    if (even > 0 && even % 2 == 0 &&
                   ans.Count == 0)
    {

        // Add 2 in the array (k-1) times
        for(int i = 0; i < k - 1; i++)
        {
           ans.Add(2);
        }

        // Add last even element
        ans.Add(even);
    }

    // Printing the array
    if (ans.Count > 0)
    {
        for(int i = 0; i < k; i++)
        {
           Console.Write(ans[i] + " ");
        }
    }
    else
    {
        Console.WriteLine("NO");
    }
}

// Driver code
public static void Main(String []args)
{
    int n = 10, k = 3;

    getArrayOfSizeK(n, k);
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>
// Javascript implementation to find an
// array of size K with all the
// even or odd elements in the array

// Function to find the array with
// all the even / odd elements
function getArrayOfSizeK(n, k)
{
    let ans = [];

    // If array could be constructed
    // by adding odd elements
    // we need to find the kth
    // element is odd or even

    // If array of odd elements
    // would be the answer then
    // k-1 elements would be 1

    // First let's check
    // kth is odd or even
    let odd = n - ((k - 1) * 1);

    // If last element is also
    // an odd number then
    // we can choose odd
    // elements for our answer
    if (odd > 0 && odd % 2 != 0)
    {

        // Add 1 in the array (k-1) times
        for(let i = 0; i < k - 1; i++)
        {
           ans.push(1);
        }

        // Add last odd element
        ans.push(odd);
    }

    // If array of even elements
    // would be the answer then
    // k-1 elements would be 2
    let even = n - ((k - 1) * 2);

    // If last element is also
    // an even number then
    // we can choose even
    // elements for our answer
    if (even > 0 && even % 2 == 0 &&
                  ans.length == 0)
    {

        // Add 2 in the array (k-1) times
        for(let i = 0; i < k - 1; i++)
        {
           ans.push(2);
        }

        // Add last even element
        ans.push(even);
    }

    // Printing the array
    if (ans.length > 0)
    {
        for(let i = 0; i < k; i++)
        {
           document.write(ans[i] + " ");
        }
    }
    else
    {
        document.write("NO");
    }
}

  // Driver Code
    let n = 10, k = 3;
    getArrayOfSizeK(n, k);

  // This code is contributed by target_2.
</script>
```

**Output:** 

```
2 2 6
```