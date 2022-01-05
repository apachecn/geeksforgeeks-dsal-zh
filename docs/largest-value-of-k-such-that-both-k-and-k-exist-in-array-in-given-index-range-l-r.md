# K 的最大值，使得 K 和-K 都存在于给定索引范围内的数组中[L，R]

> 原文:[https://www . geesforgeks . org/k 的最大值，使得 k 和 k 都存在于给定索引范围的数组中-l-r/](https://www.geeksforgeeks.org/largest-value-of-k-such-that-both-k-and-k-exist-in-array-in-given-index-range-l-r/)

给定一个由 **N** 整数和 **2** 整数 **L** 和 **R** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)、 **arr[]** ，任务是返回大于 **0** 和 **L <的最大整数 **K** ，使得两个值 **K** 和**-如果没有这样的整数，则返回 **0** 。****

**示例:**

> **输入:** N = 5，arr[] = {3，2，-2，5，-3}，L = 2，R = 3
> **输出:** 3
> **解释:**范围[2，3]中 K 的最大值，使得数组中 K 和-K 都存在于 arr[0]时为 3，arr[4]时为-3。
> 
> **输入:** N = 4，arr[] = {1，2，3，-4}，L = 1，R = 4
> **输出:** 0

**方法:**思路是[遍历数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/)[将元素加入到集合](https://www.geeksforgeeks.org/set-insert-function-in-c-stl/)中，同时检查其负值，即**arr【I】*-1**进入集合。如果找到，则[将其推入矢量**中【可能】【**](https://www.geeksforgeeks.org/vectorpush_back-vectorpop_back-c-stl/) 】。按照以下步骤解决问题:

*   [初始化一个无序集<int>**s【】**T3】来存储元素。](https://www.geeksforgeeks.org/unordered_set-in-cpp-stl/)
*   [初始化一个向量**可能的[]**](https://www.geeksforgeeks.org/initialize-a-vector-in-cpp-different-ways/) 来存储可能的答案。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N)** ，并执行以下步骤:
    *   [如果集合**s【】**](https://www.geeksforgeeks.org/set-find-function-in-c-stl/)**中存在**-arr【I】**，则将值**ABS(arr【I】)**推送到向量**中(可能[])。****
    *   **否则将元素**arr【I】**添加到集合 **s[]中。****
*   **将变量**和**初始化为 **0** 来存储答案。**
*   **[使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，大小)**，其中**大小**是向量**可能的大小[]、**，并执行以下步骤:

    *   如果**可能【I】**大于等于 **L** 且小于等于 **R，**则更新 **ans** 的值作为 **ans** 或**可能【I】的最大值。**** 
*   **执行上述步骤后，打印**和**的值作为答案。**

**下面是上述方法的实现。**

## **C++14**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum value of K
int findMax(int N, int arr[], int L, int R)
{

    // Using a set to store the elements
    unordered_set<int> s;

    // Vector to store the possible answers
    vector<int> possible;

    // Store the answer
    int ans = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // If set has it's negation,
        // check if it is max
        if (s.find(arr[i] * -1) != s.end())
            possible.push_back(abs(arr[i]));
        else
            s.insert(arr[i]);
    }

    // Find the maximum possible answer
    for (int i = 0; i < possible.size(); i++) {
        if (possible[i] >= L and possible[i] <= R)
            ans = max(ans, possible[i]);
    }

    return ans;
}

// Driver Code
int main()
{

    int arr[] = { 3, 2, -2, 5, -3 },
        N = 5, L = 2, R = 3;

    int max = findMax(N, arr, L, R);

    // Display the output
    cout << max << endl;

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;

public class GFG
{

// Function to find the maximum value of K
static int findMax(int N, int []arr, int L, int R)
{

    // Using a set to store the elements
    HashSet<Integer> s = new HashSet<Integer>();

    // ArrayList to store the possible answers
    ArrayList<Integer> possible
            = new ArrayList<Integer>();

    // Store the answer
    int ans = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // If set has it's negation,
        // check if it is max
        if (s.contains(arr[i] * -1))
            possible.add(Math.abs(arr[i]));
        else
            s.add(arr[i]);
    }

    // Find the maximum possible answer
    for (int i = 0; i < possible.size(); i++) {
        if (possible.get(i) >= L && possible.get(i) <= R) {
            ans = Math.max(ans, possible.get(i));
        }
    }

    return ans;
}

// Driver Code
public static void main(String args[])
{

    int []arr = { 3, 2, -2, 5, -3 };
    int N = 5, L = 2, R = 3;

    int max = findMax(N, arr, L, R);

    // Display the output
    System.out.println(max);

}
}

// This code is contributed by Samim Hossain Mondal.
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Function to find the maximum value of K
def findMax(N, arr, L, R) :

    # Using a set to store the elements
    s = set();

    # Vector to store the possible answers
    possible = [];

    # Store the answer
    ans = 0;

    # Traverse the array
    for i in range(N) :

        # If set has it's negation,
        # check if it is max
        if arr[i] * -1 in s  :
            possible.append(abs(arr[i]));
        else :
            s.add(arr[i]);

    # Find the maximum possible answer
    for i in range(len(possible)) :
        if (possible[i] >= L and possible[i] <= R) :
            ans = max(ans, possible[i]);

    return ans;

# Driver Code
if __name__ ==  "__main__" :

    arr = [ 3, 2, -2, 5, -3 ];
    N = 5; L = 2; R = 3;

    Max = findMax(N, arr, L, R);

    # Display the output
    print(Max);

    # This code is contributed by Ankthon
```

## **C#**

```
// Java program for the above approach
using System;
using System.Collections;
using System.Collections.Generic;

public class GFG
{
// Function to find the maximum value of K
static int findMax(int N, int []arr, int L, int R)
{

    // Using a set to store the elements
    HashSet<int> s = new HashSet<int>();

    // ArrayList to store the possible answers
    ArrayList possible = new ArrayList();

    // Store the answer
    int ans = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // If set has it's negation,
        // check if it is max
        if (s.Contains(arr[i] * -1))
            possible.Add(Math.Abs(arr[i]));
        else
            s.Add(arr[i]);
    }

    // Find the maximum possible answer
    for (int i = 0; i < possible.Count; i++) {
        if ((int)possible[i] >= L && (int)possible[i] <= R) {
            ans = Math.Max(ans, (int)possible[i]);
        }
    }

    return ans;
}

// Driver Code
public static void Main()
{

    int []arr = { 3, 2, -2, 5, -3 };
    int N = 5, L = 2, R = 3;

    int max = findMax(N, arr, L, R);

    // Display the output
    Console.Write(max);;

}
}

// This code is contributed by Samim Hossain Mondal.
```

## **java 描述语言**

```
<script>

        // JavaScript Program to implement
        // the above approach

        // Function to find the maximum value of K
        function findMax(N, arr, L, R) {

            // Using a set to store the elements
            let s = new Set();

            // Vector to store the possible answers
            let possible = [];

            // Store the answer
            let ans = 0;

            // Traverse the array
            for (let i = 0; i < N; i++) {

                // If set has it's negation,
                // check if it is max
                if (s.has(arr[i] * -1))
                    possible.push(Math.abs(arr[i]));
                else
                    s.add(arr[i]);
            }

            // Find the maximum possible answer
            for (let i = 0; i < possible.length; i++) {
                if (possible[i] >= L && possible[i] <= R)
                    ans = Math.max(ans, possible[i]);
            }

            return ans;
        }

        // Driver Code
        let arr = [3, 2, -2, 5, -3];
        let N = 5, L = 2, R = 3;

        let max = findMax(N, arr, L, R);

        // Display the output
        document.write(max + '<br');

    // This code is contributed by Potta Lokesh
    </script>
```

****Output**

```
3
```** 

*****时间复杂度:**O(N)*
T5**辅助空间:** O(N)**