# 查找范围[L，R]中与给定数组元素互质的数字

> 原文:[https://www . geeksforgeeks . org/find-numbers-in-range-l-r-与给定数组元素互素/](https://www.geeksforgeeks.org/find-numbers-in-range-l-r-that-are-coprime-with-given-array-elements/)

给定一个由 **N** 个不同正整数和一个范围**【L，R】**组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找到给定范围**【L，R】**中与所有数组元素[互素的元素](https://www.geeksforgeeks.org/check-for-an-array-element-that-is-co-prime-with-all-others/)。

**示例:**

> **输入:** L = 3，R = 11，arr[ ] = {4，7，9，6，13，21}
> ***输出:** {* 5，11 *}*
> ***解释:***
> *范围内与所有数组元素同素的元素为{5，11}。*
> 
> **输入:** L = 1，R = 10，arr[ ] = {3，5}
> ***输出:** {1，2，4，7，8}*

**方法:**给定的问题可以通过将每个数组元素的所有[因子](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/)存储在[哈希集中](https://www.geeksforgeeks.org/hashset-in-java/)来解决。让另一个 **HashSet** 出现，比如说 **S** 由**【L，R】**范围内的数字组成，现在的任务是去掉从这个 HashSet **S** 计算出的除数的倍数，得到结果数。按照以下步骤解决问题:

*   将每个数组元素的[因子存储在一个](https://www.geeksforgeeks.org/count-the-divisors-or-multiples-present-in-the-array-for-each-element/)[无序集合](https://www.geeksforgeeks.org/unordered_set-in-cpp-stl/)中，比如 **S** 。
*   将范围**【L，R】**中的所有值存储在另一个哈希集中，比如 **M** 。
*   [遍历无序集合](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/) **S** ，对于 **S** 中的每个元素，说出**值**，如果 **M** 中存在**值**的倍数，则从集合 **M** 中移除所有倍数。
*   完成上述步骤后，将 HashSet **M** 中存储的所有元素打印为所需的结果编号。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find all the elements in
// the range [L, R] which are co prime
// with all array elements
void elementsCoprimeWithArr(
    int A[], int N, int L, int R)
{
    // Store all the divisors of array
    // element in S
    unordered_set<int> S;

    // Find the divisors
    for (int i = 0; i < N; i++) {

        int curr_ele = A[i];

        for (int j = 1;
             j <= sqrt(curr_ele) + 1; j++) {
            if (curr_ele % j == 0) {
                S.insert(j);
                S.insert(curr_ele / j);
            }
        }
    }

    // Stores all possible required number
    // satisfying the given criteria
    unordered_set<int> store;

    // Insert all element [L, R]
    for (int i = L; i <= R; i++)
        store.insert(i);

    S.erase(1);

    // Traverse the set
    for (auto it : S) {

        int ele = it;

        int index = 1;

        // Remove the multiples of ele
        while (index * ele <= R) {
            store.erase(index * ele);
            index++;
        }
    }

    // Print the resultant numbers
    for (auto i : store) {
        cout << i << " ";
    }
}

// Driver Code
int main()
{
    int arr[] = { 3, 5 };
    int L = 1, R = 10;
    int N = sizeof(arr) / sizeof(arr[0]);

    elementsCoprimeWithArr(arr, N, L, R);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG
{

// Function to find all the elements in
// the range [L, R] which are co prime
// with all array elements
static void elementsCoprimeWithArr(
    int A[], int N, int L, int R)
{

    // Store all the divisors of array
    // element in S
    HashSet<Integer> S = new HashSet<Integer>();

    // Find the divisors
    for (int i = 0; i < N; i++) {

        int curr_ele = A[i];

        for (int j = 1;
             j <= Math.sqrt(curr_ele) + 1; j++) {
            if (curr_ele % j == 0) {
                S.add(j);
                S.add(curr_ele / j);
            }
        }
    }

    // Stores all possible required number
    // satisfying the given criteria
    HashSet<Integer> store= new HashSet<Integer>();

    // Insert all element [L, R]
    for (int i = L; i <= R; i++)
        store.add(i);

    S.remove(1);

    // Traverse the set
    for (int it : S) {

        int ele = it;

        int index = 1;

        // Remove the multiples of ele
        while (index * ele <= R) {
            store.remove(index * ele);
            index++;
        }
    }

    // Print the resultant numbers
    for (int i : store) {
        System.out.print(i+ " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 3, 5 };
    int L = 1, R = 10;
    int N = arr.length;

    elementsCoprimeWithArr(arr, N, L, R);
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# python 3 program for the above approach
import math

# Function to find all the elements in
# the range [L, R] which are co prime
# with all array elements
def elementsCoprimeWithArr(
        A, N, L, R):

    # Store all the divisors of array
    # element in S
    S = []

    # Find the divisors
    for i in range(N):

        curr_ele = A[i]

        for j in range(1, (int)(math.sqrt(curr_ele)) + 1):
            if (curr_ele % j == 0):
                S.append(j)
                S.append(curr_ele // j)

    # Stores all possible required number
    # satisfying the given criteria
    store = []
    S = set(S)

    # Insert all element [L, R]
    for i in range(L, R+1):
        store.append(i)

    S.remove(1)

    # / Traverse the set
    for it in S:

        ele = it

        index = 1

        # Remove the multiples of ele
        while (index * ele <= R):

            store.remove(index * ele)
            index += 1

    # Print the resultant numbers
    for i in store:
        print(i, end=" ")

# Driver Code
if __name__ == "__main__":

    arr = [3, 5]
    L = 1
    R = 10
    N = len(arr)

    elementsCoprimeWithArr(arr, N, L, R)

    # This code is contributed by ukasp.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG
{

// Function to find all the elements in
// the range [L, R] which are co prime
// with all array elements
static void elementsCoprimeWithArr(
    int []A, int N, int L, int R)
{

    // Store all the divisors of array
    // element in S
    HashSet<int> S = new HashSet<int>();

    // Find the divisors
    for (int i = 0; i < N; i++) {

        int curr_ele = A[i];

        for (int j = 1;
             j <= Math.Sqrt(curr_ele) + 1; j++) {
            if (curr_ele % j == 0) {
                S.Add(j);
                S.Add(curr_ele / j);
            }
        }
    }

    // Stores all possible required number
    // satisfying the given criteria
    HashSet<int> store= new HashSet<int>();

    // Insert all element [L, R]
    for (int i = L; i <= R; i++)
        store.Add(i);

    S.Remove(1);

    // Traverse the set
    foreach (int it in S) {

        int ele = it;

        int index = 1;

        // Remove the multiples of ele
        while (index * ele <= R) {
            store.Remove(index * ele);
            index++;
        }
    }

    // Print the resultant numbers
    foreach (int i in store) {
        Console.Write(i+ " ");
    }
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 3, 5 };
    int L = 1, R = 10;
    int N = arr.Length;

    elementsCoprimeWithArr(arr, N, L, R);
}
}

// This code is contributed by shikhasingrajput
```

**Output:** 

```
8 7 2 1 4
```

***时间复杂度:** O(N*sqrt(M))，其中 M 为* [*最大阵元*](https://www.geeksforgeeks.org/c-program-find-largest-element-array/) *。*
***辅助空间:** O(最大值(R–L，N))*