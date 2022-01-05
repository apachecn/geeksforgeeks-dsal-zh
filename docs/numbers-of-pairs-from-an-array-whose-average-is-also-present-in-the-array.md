# 数组中平均值也存在于数组中的对的数量

> 原文:[https://www . geeksforgeeks . org/来自阵列的配对数，其平均值也存在于阵列中/](https://www.geeksforgeeks.org/numbers-of-pairs-from-an-array-whose-average-is-also-present-in-the-array/)

给定由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是计算数组中不同对 **(arr[i]，arr[j])** 的数量，使得对的平均值也存在于数组中。
***注:**将 **(arr[i]、arr[j])** 和 **(arr[j]、arr[i])** 视为同一对。*

**示例:**

> **输入:** arr[] = {2，1，3}
> **输出:** 1
> **解释:**给定数组中唯一存在平均值的一对是(1，3)(平均值= 2)。
> 
> **输入:** arr[] = {4，2，5，1，3，5}
> **输出:** 7

**天真方法:**按照以下步骤解决问题:

*   初始化一个变量，比如说**计数**为 **0** 来存储数组中存在平均值的所有对的计数。
*   将所有数组元素插入一个[集合](https://www.geeksforgeeks.org/hashset-in-java/) **S** 。
*   [遍历集合](https://www.geeksforgeeks.org/how-to-traverse-a-c-set-in-reverse-direction/) **S** ，对于集合**S**[中的每个元素，生成给定数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)的所有可能的对，如果任何对的总和与集合中的当前元素相同，则将**计数**的值增加 **1** 。
*   完成上述步骤后，打印**计数**的值作为成对计数的结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the number of
// pairs from the array having sum S
int getCountPairs(vector<int> arr, int N, int S)
{

    // Stores the total count of
    // pairs whose sum is 2*S
    int count = 0;

    // Generate all possible pairs
    // and check their sums
    for(int i = 0; i < arr.size(); i++)
    {
        for(int j = i + 1; j < arr.size(); j++)
        {

            // If the sum is S, then
            // increment the count
            if ((arr[i] + arr[j]) == S)
                count++;
        }
    }

    // Return the total
    // count of pairs
    return count;
}

// Function to count of pairs having
// whose average exists in the array
int countPairs(vector<int> arr, int N)
{

    // Initialize the count
    int count = 0;

    // Use set to remove duplicates
    unordered_set<int> S;

    // Add elements in the set
    for(int i = 0; i < N; i++)
        S.insert(arr[i]);

    for(int ele : S)
    {
        int sum = 2 * ele;

        // For every sum, count
        // all possible pairs
        count += getCountPairs(arr, N, sum);
    }

    // Return the total count
    return count;
}

// Driver Code
int main()
{
    vector<int> arr = { 4, 2, 5, 1, 3, 5 };
    int N = arr.size();
    cout << countPairs(arr, N);

    return 0;
}

// This code is contributed by Kingash
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.util.*;

class GFG {

    // Function to count the number of
    // pairs from the array having sum S
    public static int getCountPairs(
        int arr[], int N, int S)
    {
        // Stores the total count of
        // pairs whose sum is 2*S
        int count = 0;

        // Generate all possible pairs
        // and check their sums
        for (int i = 0;
             i < arr.length; i++) {

            for (int j = i + 1;
                 j < arr.length; j++) {

                // If the sum is S, then
                // increment the count
                if ((arr[i] + arr[j]) == S)
                    count++;
            }
        }

        // Return the total
        // count of pairs
        return count;
    }

    // Function to count of pairs having
    // whose average exists in the array
    public static int countPairs(
        int arr[], int N)
    {
        // Initialize the count
        int count = 0;

        // Use set to remove duplicates
        HashSet<Integer> S = new HashSet<>();

        // Add elements in the set
        for (int i = 0; i < N; i++)
            S.add(arr[i]);

        for (int ele : S) {

            int sum = 2 * ele;

            // For every sum, count
            // all possible pairs
            count += getCountPairs(
                arr, N, sum);
        }

        // Return the total count
        return count;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 4, 2, 5, 1, 3, 5 };
        int N = arr.length;
        System.out.print(
            countPairs(arr, N));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the number of
# pairs from the array having sum S
def getCountPairs(arr, N, S):

    # Stores the total count of
    # pairs whose sum is 2*S
    count = 0

    # Generate all possible pairs
    # and check their sums
    for i in range(len(arr)):
        for j in range(i + 1, len(arr)):

            # If the sum is S, then
            # increment the count
            if ((arr[i] + arr[j]) == S):
                count += 1

    # Return the total
    # count of pairs
    return count

# Function to count of pairs having
# whose average exists in the array
def countPairs(arr, N):

    # Initialize the count
    count = 0

    # Use set to remove duplicates
    S = set([])

    # Add elements in the set
    for i in range(N):
        S.add(arr[i])

    for ele in S:
        sum = 2 * ele

        # For every sum, count
        # all possible pairs
        count += getCountPairs(arr, N, sum)

    # Return the total count
    return count

# Driver Code
if __name__ == "__main__":

    arr = [ 4, 2, 5, 1, 3, 5 ]
    N = len(arr)

    print(countPairs(arr, N))

# This code is contributed by ukasp
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG
{

    // Function to count the number of
    // pairs from the array having sum S
    public static int getCountPairs(
        int []arr, int N, int S)
    {

        // Stores the total count of
        // pairs whose sum is 2*S
        int count = 0;

        // Generate all possible pairs
        // and check their sums
        for (int i = 0;
             i < arr.Length; i++) {

            for (int j = i + 1;
                 j < arr.Length; j++) {

                // If the sum is S, then
                // increment the count
                if ((arr[i] + arr[j]) == S)
                    count++;
            }
        }

        // Return the total
        // count of pairs
        return count;
    }

    // Function to count of pairs having
    // whose average exists in the array
    public static int countPairs(
        int []arr, int N)
    {
        // Initialize the count
        int count = 0;

        // Use set to remove duplicates
        HashSet<int> S = new HashSet<int>();

        // Add elements in the set
        for (int i = 0; i < N; i++)
            S.Add(arr[i]);

        foreach (int ele in S) {

            int sum = 2 * ele;

            // For every sum, count
            // all possible pairs
            count += getCountPairs(
                arr, N, sum);
        }

        // Return the total count
        return count;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int []arr = { 4, 2, 5, 1, 3, 5 };
        int N = arr.Length;
        Console.Write(
            countPairs(arr, N));
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

    // Function to count the number of
    // pairs from the array having sum S
    function getCountPairs(
        arr, N, S)
    {
        // Stores the total count of
        // pairs whose sum is 2*S
        let count = 0;

        // Generate all possible pairs
        // and check their sums
        for (let i = 0;
             i < arr.length; i++) {

            for (let j = i + 1;
                 j < arr.length; j++) {

                // If the sum is S, then
                // increment the count
                if ((arr[i] + arr[j]) == S)
                    count++;
            }
        }

        // Return the total
        // count of pairs
        return count;
    }

    // Function to count of pairs having
    // whose average exists in the array
    function countPairs(arr, N)
    {
        // Initialize the count
        let count = 0;

        // Use set to remove duplicates
        let S = [];

        // Add elements in the set
        for (let i = 0; i < N; i++)
            S.push(arr[i]);

        for (let ele in S) {

            let sum = 2 * ele;

            // For every sum, count
            // all possible pairs
            count += getCountPairs(
                arr, N, sum);
        }

        // Return the total count
        return count;
    }

// Driver code

         let arr = [ 4, 2, 5, 1, 3, 5 ];
        let N = arr.length;
        document.write(
            countPairs(arr, N));

// This code is contributed by code_hunt.
</script>
```

**Output:** 

```
7
```

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(N)*

**有效方法:**上述方法也可以通过将给定数组中所有可能对的[和的频率存储在](https://www.geeksforgeeks.org/find-the-sum-of-all-possible-pairs-in-an-array-of-n-elements/)[哈希映射](https://www.geeksforgeeks.org/java-util-hashmap-in-java/)中并相应地找到数组中每个元素的计数来优化。按照以下步骤解决问题:

*   初始化一个变量，比如说**计数**为 **0** 来存储数组中存在平均值的所有对的计数。
*   将所有数组元素插入一个[集合](https://www.geeksforgeeks.org/hashset-in-java/) **S** 。
*   初始化一个 HashMap，比如说 **M** ，它存储给定数组中所有可能对的[和的频率。](https://www.geeksforgeeks.org/find-the-sum-of-all-possible-pairs-in-an-array-of-n-elements/)
*   [遍历集合](https://www.geeksforgeeks.org/how-to-traverse-a-c-set-in-reverse-direction/) **S** ，对于集合 **S** 中的每一个元素(比如说 **X** )，用值 **(M[X]/2)** 更新**的值。**
*   完成上述步骤后，打印**计数**的值作为成对计数的结果。

下面是上述方法的实现:

## C++

```
// CPP program for the above approach
#include<bits/stdc++.h>
using namespace std;

    // Function to count the total count
    // of pairs having sum S
    int getCountPairs(int arr[],
                             int N, int S)
    {
        map<int,int> mp;

        // Store the total count of all
        // elements in map mp
        for (int i = 0; i < N; i++) {

            mp[arr[i]]++;
        }

        // Stores the total count of
        // total pairs
        int twice_count = 0;

        // Iterate through each element
        // and increment the count
        for (int i = 0; i < N; i++) {

            // If the value (S - arr[i])
            // exists in the map hm
            if (mp.find(S - arr[i]) != mp.end()) {

                // Update the twice count
                twice_count += mp[S - arr[i]];
            }

            if (S - arr[i] == arr[i])
                twice_count--;
        }

        // Return the half of twice_count
        return twice_count / 2;
    }

    // Function to count of pairs having
    // whose average exists in the array
    int countPairs(
        int arr[], int N)
    {
        // Stores the total count of
        // pairs
        int count = 0;

        // Use set to remove duplicates
        set<int> S;

        // Insert all the element in
        // the set S
        for (int i = 0; i < N; i++)
            S.insert(arr[i]);

        for (int ele : S) {

            int sum = 2 * ele;

            // For every sum find the
            // getCountPairs
            count += getCountPairs(
                arr, N, sum);
        }

        // Return the total count of
        // pairs
        return count;
    }

    // Driver Code
    int main()
    {
        int N = 6;
        int arr[] = { 4, 2, 5, 1, 3, 5 };
        cout<<(countPairs(arr, N));
    }

// This code is contributed by ipg2016107.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.util.*;

class GFG {

    // Function to count the total count
    // of pairs having sum S
    static int getCountPairs(int arr[],
                             int N, int S)
    {
        HashMap<Integer, Integer> mp
            = new HashMap<>();

        // Store the total count of all
        // elements in map mp
        for (int i = 0; i < N; i++) {

            // Initialize value to 0,
            // if key not found
            if (!mp.containsKey(arr[i]))
                mp.put(arr[i], 0);

            mp.put(arr[i],
                   mp.get(arr[i]) + 1);
        }

        // Stores the total count of
        // total pairs
        int twice_count = 0;

        // Iterate through each element
        // and increment the count
        for (int i = 0; i < N; i++) {

            // If the value (S - arr[i])
            // exists in the map hm
            if (mp.get(S - arr[i])
                != null) {

                // Update the twice count
                twice_count += mp.get(
                    S - arr[i]);
            }

            if (S - arr[i] == arr[i])
                twice_count--;
        }

        // Return the half of twice_count
        return twice_count / 2;
    }

    // Function to count of pairs having
    // whose average exists in the array
    public static int countPairs(
        int arr[], int N)
    {
        // Stores the total count of
        // pairs
        int count = 0;

        // Use set to remove duplicates
        HashSet<Integer> S = new HashSet<>();

        // Insert all the element in
        // the set S
        for (int i = 0; i < N; i++)
            S.add(arr[i]);

        for (int ele : S) {

            int sum = 2 * ele;

            // For every sum find the
            // getCountPairs
            count += getCountPairs(
                arr, N, sum);
        }

        // Return the total count of
        // pairs
        return count;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 6;
        int arr[] = { 4, 2, 5, 1, 3, 5 };
        System.out.println(
            countPairs(arr, N));
    }
}
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to count the total count
// of pairs having sum S
function getCountPairs(arr,N,S)
{
    let mp = new Map();

        // Store the total count of all
        // elements in map mp
        for (let i = 0; i < N; i++) {

            // Initialize value to 0,
            // if key not found
            if (!mp.has(arr[i]))
                mp.set(arr[i], 0);

            mp.set(arr[i],
                   mp.get(arr[i]) + 1);
        }

        // Stores the total count of
        // total pairs
        let twice_count = 0;

        // Iterate through each element
        // and increment the count
        for (let i = 0; i < N; i++) {

            // If the value (S - arr[i])
            // exists in the map hm
            if (mp.get(S - arr[i])
                != null) {

                // Update the twice count
                twice_count += mp.get(
                    S - arr[i]);
            }

            if (S - arr[i] == arr[i])
                twice_count--;
        }

        // Return the half of twice_count
        return Math.floor(twice_count / 2);
}

// Function to count of pairs having
// whose average exists in the array
function countPairs(arr,N)
{
    // Stores the total count of
        // pairs
        let count = 0;

        // Use set to remove duplicates
        let S = new Set();

        // Insert all the element in
        // the set S
        for (let i = 0; i < N; i++)
            S.add(arr[i]);

        for (let ele of S.values()) {

            let sum = 2 * ele;

            // For every sum find the
            // getCountPairs
            count += getCountPairs(
                arr, N, sum);
        }

        // Return the total count of
        // pairs
        return count;
}

// Driver Code
let  N = 6;
let arr=[4, 2, 5, 1, 3, 5 ];
document.write(countPairs(arr, N));

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
7
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*