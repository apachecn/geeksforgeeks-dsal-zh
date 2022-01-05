# 删除给定元素后给定数组中值的变化

> 原文:[https://www . geeksforgeeks . org/删除给定元素后给定数组的中值变化/](https://www.geeksforgeeks.org/change-in-median-of-given-array-after-deleting-given-elements/)

给定两个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr1[]** 和 **arr2[]** 。对数组 **arr1[]** 进行排序。任务是将数组**arr 2【】**中的每个元素去除后，打印中位数的变化。

**注意:**数组 **arr2[]** 只有那些存在于数组 **arr1[]** 中的元素。

**示例:**

> **输入:** arr1[] = {2，4，6，8，10}，arr2[] = {4，6}
> **输出:** 1 1
> **解释:**
> 最初中位数为 6。
> 去掉 4 后，数组变成 arr1[] = {2，6，8，10}，中位数= 7，因此差为 7–6 = 1。
> 去掉 6 后，数组变成 arr1[] = {2，8，10}，中位数= 8，因此差为 8–7 = 1。
> 
> **输入:** arr1[] = {1，100，250，251}，arr2[] = {250，1}
> **输出:** -75 75.5
> **解释:**
> 最初中位数为 175。
> 去掉 250 后，数组变成 arr1[] = {1，100，251}，中位数= 100，因此差为 100–175 =-75。
> 去掉 1 后，数组变成 arr1[] = {100，251}，中值= 175.5，因此差为 175.5–100 = 75.5。

**方法:**思路是遍历数组的每个元素**arr 2【】**并从数组中移除每个元素**arr 1【】**并在数组中每次移除元素后存储[数组的中值](https://www.geeksforgeeks.org/median/)**arr 1【】**(比如**temp【】**)。从 **arr2[]** 中删除元素后，打印数组元素的连续差值，得到中位数的变化。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the median change
// after removing elements from arr2[]
void medianChange(vector<int>& arr1,
                  vector<int>& arr2)
{
    int N = arr1.size();

    // To store the median
    vector<float> median;

    // Store the current median

    // If N is odd
    if (N & 1) {
        median
            .push_back(arr1[N / 2] * 1.0);
    }

    // If N is even
    else {
        median
            .push_back((arr1[N / 2]
                        + arr1[(N - 1) / 2])
                       / 2.0);
    }

    for (auto& x : arr2) {

        // Find the current element
        // in arr1
        auto it = find(arr1.begin(),
                       arr1.end(),
                       x);

        // Erase the element
        arr1.erase(it);

        // Decrement N
        N--;

        // Find the new median
        // and append

        // If N is odd
        if (N & 1) {
            median
                .push_back(arr1[N / 2] * 1.0);
        }

        // If N is even
        else {
            median
                .push_back((arr1[N / 2]
                            + arr1[(N - 1) / 2])
                           / 2.0);
        }
    }

    // Print the corresponding
    // difference of median
    for (int i = 0;
         i < median.size() - 1;
         i++) {
        cout << median[i + 1] - median[i]
             << ' ';
    }
}

// Driven Code
int main()
{
    // Given arrays
    vector<int> arr1 = { 2, 4, 6, 8, 10 };
    vector<int> arr2 = { 4, 6 };

    // Function Call
    medianChange(arr1, arr2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;

class GFG{

// Function to find the median
// change after removing elements
// from arr2[]
public static void medianChange(List<Integer> arr1,
                                List<Integer> arr2)
{
    int N = arr1.size();

    // To store the median
    List<Integer> median = new ArrayList<>();

    // Store the current median

    // If N is odd
    if ((N & 1) != 0)
        median.add(arr1.get(N / 2) * 1);

    // If N is even
    else
        median.add((arr1.get(N / 2) +
                    arr1.get((N - 1) / 2)) / 2);

    for(int x = 0; x < arr2.size(); x++)
    {

        // Find the current element
        // in arr1
        int it = arr1.indexOf(arr2.get(x));

        // Erase the element
        arr1.remove(it);

        // Decrement N
        N--;

        // Find the new median
        // and append

        // If N is odd
        if ((N & 1) != 0)
        {
            median.add(arr1.get(N / 2) * 1);
        }

        // If N is even
        else
        {
            median.add((arr1.get(N / 2) +
                        arr1.get((N - 1) / 2)) / 2);
        }
    }

    // Print the corresponding
    // difference of median
    for(int i = 0; i < median.size() - 1; i++)
    {
        System.out.print(median.get(i + 1) -
                         median.get(i) + " ");
    }
}

// Driver Code             
public static void main(String[] args)
{

    // Given arrays
    List<Integer> arr1  = new ArrayList<Integer>(){
        { add(2); add(4); add(6); add(8); add(10); } };
    List<Integer> arr2 = new ArrayList<Integer>(){
        { add(4); add(6); } };

    // Function Call
    medianChange(arr1, arr2);
}
}

// This code is contributed by divyesh072019
```

## 蟒蛇 3

```
# Python3 program for the
# above approach

# Function to find the median
# change after removing elements
# from arr2[]
def medianChange(arr1, arr2):

    N = len(arr1)

    # To store the median
    median = []

    # Store the current median

    # If N is odd
    if (N & 1):
        median.append(arr1[N // 2] * 1)

    # If N is even
    else:
        median.append((arr1[N // 2] +
                       arr1[(N - 1) // 2]) // 2)

    for x in arr2:

        # Find the current
        # element in arr1
        it = arr1.index(x)

        # Erase the element
        arr1.pop(it)

        # Decrement N
        N -= 1

        # Find the new median
        # and append

        # If N is odd
        if (N & 1):
            median.append(arr1[N // 2] * 1)

        # If N is even
        else:
            median.append((arr1[N // 2] +
                           arr1[(N - 1) // 2]) // 2)

    # Print the corresponding
    # difference of median
    for i in range(len(median) - 1):
        print(median[i + 1] - median[i],
              end = ' ')

# Driver Code
if __name__ == "__main__":

    # Given arrays
    arr1 = [2, 4, 6,
            8, 10]
    arr2 = [4, 6]

    # Function Call
    medianChange(arr1, arr2)

# This code is contributed by Chitranayal
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the median change
// after removing elements from arr2[]
static void medianChange(List<int> arr1,
                         List<int> arr2)
{
    int N = arr1.Count;

    // To store the median
    List<double> median = new List<double>();

    // Store the current median

    // If N is odd
    if ((N & 1) != 0)
    {
        median.Add(arr1[N / 2] * 1.0);
    }

    // If N is even
    else
    {
        median.Add((arr1[N / 2] +
              arr1[(N - 1) / 2]) / 2.0);
    }

    foreach(int x in arr2)
    {

        // Find the current element
        // in arr1
        int it = arr1.IndexOf(x);

        // Erase the element
        arr1.RemoveAt(it);

        // Decrement N
        N--;

        // Find the new median
        // and append

        // If N is odd
        if ((N & 1) != 0)
        {
            median.Add(arr1[N / 2] * 1.0);
        }

        // If N is even
        else
        {
            median.Add((arr1[N / 2] +
                  arr1[(N - 1) / 2]) / 2.0);
        }
    }

    // Print the corresponding
    // difference of median
    for(int i = 0; i < median.Count - 1; i++)
    {
        Console.Write(median[i + 1] -
                      median[i] + " ");
    }
}

// Driver Code
static void Main()
{

    // Given arrays
    List<int> arr1 = new List<int>(
        new int[]{ 2, 4, 6, 8, 10 });
    List<int> arr2 = new List<int>(
        new int[]{ 4, 6 });

    // Function Call
    medianChange(arr1, arr2);
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

// JavaScript program for the
// above approach

// Function to find the median
// change after removing elements
// from arr2[]
function medianChange(arr1,arr2)
{
    let N = arr1.length;

    // To store the median
    let median = [];

    // Store the current median

    // If N is odd
    if ((N & 1))
        median.push((arr1[Math.floor(N / 2)] * 1));

    // If N is even
    else
        median.push(Math.floor((arr1[Math.floor(N / 2)] +
        arr1[Math.floor((N - 1) / 2)]) / 2));

    for(let x = 0; x < arr2.length; x++)
    {

        // Find the current element
        // in arr1
        let it = arr1.indexOf(arr2[x]);
        // Erase the element
        arr1.splice(it,1);

        // Decrement N
        N--;

        // Find the new median
        // and append

        // If N is odd
        if ((N & 1))
        {
            median.push(arr1[Math.floor(N / 2)] * 1);
        }

        // If N is even
        else
        {
            median.push(Math.floor((arr1[Math.floor(N / 2)] +
            arr1[Math.floor((N - 1) / 2)]) / 2));
        }
    }
    // Print the corresponding
    // difference of median
    for(let i = 0; i < median.length - 1; i++)
    {
        document.write((median[i + 1] -
                         median[i]) + " ");
    }
}
// Driver Code

// Given arrays
let arr1 = [2, 4, 6,
            8, 10];
let arr2 = [4, 6];

// Function Call
medianChange(arr1, arr2)

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
1 1
```

***时间复杂度:** O(M*N)*
***辅助空间** : O(M * N)*