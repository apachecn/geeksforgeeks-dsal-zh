# 通过移除 M 个最小元素修改数组，保持剩余元素的顺序

> 原文:[https://www . geeksforgeeks . org/通过移除 m 个最小元素来修改数组-保持剩余元素的顺序/](https://www.geeksforgeeks.org/modify-array-by-removing-m-smallest-elements-maintaining-the-order-of-remaining-elements/)

给定一个正整数 **M** 和一个由 **N** 个不同正整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)，任务是从数组中移除第一个 **M** 个最小元素，这样剩余元素的相对顺序就不会改变。

**示例:**

> **输入:** *M = 5，*arr【】= {2】*，81，75，98，72，63，53，5，40，92}*
> **输出:***81 75 98 72 92*
> **解释:**
> *第一个 M(= 5)个最小的元素是{ 2，5，40，53，63}。删除这些元素后，修改后的数组是{81，75，98，72，92}。*
> 
> ***输入:** M = 1，arr[] = {8，3，6，10，5}*
> ***输出:** 8 6 10 5*

[**排序**](https://www.geeksforgeeks.org/sorting-algorithms/)**-基于方法:**给定的问题可以通过将每个数组元素与其索引配对，然后[对配对数组进行排序](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)来解决。按照以下步骤解决问题:

*   初始化[对](https://www.geeksforgeeks.org/pair-in-cpp-stl/) **A** 的[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)，并将**A【I】**初始化为**{ arr【I】，i}** 。
*   [按对](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)的第一个元素对向量 **A[]** 进行排序。
*   [通过配对](https://www.geeksforgeeks.org/sort-the-array-in-a-given-index-range/)的[第二个元素对**【M，N–1】**范围内的元素](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)进行排序。
*   现在，使用变量 **i** 迭代给定范围**【M，N–1】**，并打印**A【I】的值。首先**作为结果数组元素。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to print the array after
// removing the smallest M elements
void removeSmallestM(int arr[], int N,
                     int M)
{
    // Store pair of {element, index}
    vector<pair<int, int> > A;

    // Iterate over the range [0, N]
    for (int i = 0; i < N; i++) {
        A.emplace_back(arr[i], i);
    }

    // Sort with respect to the
    // first value
    sort(A.begin(), A.end());

    // Sort from the index M to N - 1
    // using comparator for sorting
    // by the second value
    sort(A.begin() + M, A.end(),
         [&](pair<int, int> a, pair<int, int> b) {
             return a.second < b.second;
         });

    // Traverse from M to N - 1
    for (int i = M; i < N; i++) {
        cout << A[i].first << " ";
    }
}

// Driver Code
int main()
{
    int M = 5;
    int arr[] = { 2, 81, 75, 98, 72,
                  63, 53, 5, 40, 92 };
    int N = sizeof(arr) / sizeof(arr[0]);
    removeSmallestM(arr, N, M);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to print the array after
# removing the smallest M elements
def removeSmallestM(arr, N, M):

    # Store pair of {element, index}
    A = []

    # Iterate over the range [0, N]
    for i in range(N):
        A.append([arr[i], i])

    # Sort with respect to the
    # first value
    A = sorted(A)

    B = []
    for i in range(M, N):
        B.append([A[i][1], A[i][0]])

    B = sorted(B)

    # Traverse from M to N - 1
    for i in range(len(B)):
        print(B[i][1], end = " ")

# Driver Code
if __name__ == '__main__':

    M = 5
    arr = [ 2, 81, 75, 98, 72,
            63, 53, 5, 40, 92 ]
    N = len(arr)

    removeSmallestM(arr, N, M)

# This code is contributed by mohit kumar 29
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to print the array after
// removing the smallest M elements
function removeSmallestM(arr, N, M) {
    // Store pair of {element, index}
    let A = [];

    // Iterate over the range [0, N]
    for (let i = 0; i < N; i++) {
        A.push([arr[i], i]);
    }

    // Sort with respect to the
    // first value
    A.sort((a, b) => a[0] - b[0]);

    // Sort from the index M to N - 1
    // using comparator for sorting
    // by the second value
    let B = [];
    for (let i = M; i < N; i++) {
        B.push([A[i][1], A[i][0]])
    }

     B.sort((a, b) => a[0] - b[0])

    for (let i = 0; i < B.length; i++) {
        document.write(B[i][1] + " ")
    }
}

// Driver Code

let M = 5;
let arr = [2, 81, 75, 98, 72,
    63, 53, 5, 40, 92];
let N = arr.length
removeSmallestM(arr, N, M);

</script>
```

**Output:** 

```
81 75 98 72 92
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*

[**HashMap**](https://www.geeksforgeeks.org/java-util-hashmap-in-java-with-examples/)**-基于方法:**给定的问题也可以通过使用 [HashMap](https://www.geeksforgeeks.org/java-util-hashmap-in-java/) 来存储数组中最小的 **M** 元素来解决。按照以下步骤解决问题:

*   初始化一个辅助[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)，说 **A** ，把所有数组元素 **arr[]** 都存储在里面。
*   [排序向量](https://www.geeksforgeeks.org/sorting-a-vector-in-c/) **A** 并初始化一个 HashMap，比如 **mp** 。
*   [使用变量 **i** ，](https://www.geeksforgeeks.org/range-based-loop-c/)[在范围](https://www.geeksforgeeks.org/hashmap-put-method-in-java/)**【0，M–1】**上迭代，并在哈希表中插入**A【I】**。
*   使用变量 **i** 迭代范围**【0，N–1】**，如果哈希表中不存在 **arr[i]** 的值，则打印 **arr[i]** 的值作为结果数组。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to print the array after
// removing the smallest M elements
void removeSmallestM(int arr[], int N,
                     int M)
{
    // Stores the copy of arr
    vector<int> A(arr, arr + N);

    // Sort the vector in increasing
    // order
    sort(A.begin(), A.end());

    // Stores the smallest M elements
    unordered_map<int, int> mp;

    for (int i = 0; i < M; i++) {

        // Insert A[i] in the map
        mp[A[i]] = 1;
    }

    for (int i = 0; i < N; i++) {
        // If current value is present
        // in the hashmap
        if (mp.find(arr[i]) == mp.end()) {
            // Print the value of
            // current element
            cout << arr[i] << " ";
        }
    }
}

// Driver Code
int main()
{
    int M = 5;
    int arr[] = { 2, 81, 75, 98, 72,
                  63, 53, 5, 40, 92 };
    int N = sizeof(arr) / sizeof(arr[0]);
    removeSmallestM(arr, N, M);

    return 0;
}
```

## 蟒蛇 3

```
# Python Program for the above approach

# Function to print the array after
# removing the smallest M elements
def removeSmallestM(arr, N, M) :

    # Stores the copy of arr
    A  = arr.copy()

    # Sort the vector in increasing
    # order
    A.sort()

    # Stores the smallest M elements
    mp = {}

    for i in range(M) :

        # Insert A[i] in the map
        mp[A[i]] = 1

    for i in range(N) :
        # If current value is present
        # in the hashmap
        if arr[i] not in mp :
            # Print the value of
            # current element
            print(arr[i], end = " ")

# Driver Code
M = 5
arr = [2, 81, 75, 98, 72, 63, 53, 5, 40, 92]
N = len(arr)
removeSmallestM(arr, N, M)

# This code is contributed by gfgking
```

## java 描述语言

```
<script>

        // JavaScript Program for the above approach

        // Function to print the array after
        // removing the smallest M elements
        function removeSmallestM(arr, N, M) {
            // Stores the copy of arr
            let A = [...arr];

            // Sort the vector in increasing
            // order
            A.sort(function (a, b) { return a - b; })

            // Stores the smallest M elements
            let mp = new Map();

            for (let i = 0; i < M; i++) {

                // Insert A[i] in the map
                mp.set(A[i], 1);
            }

            for (let i = 0; i < N; i++) {
                // If current value is present
                // in the hashmap
                if (mp.has(arr[i]) == false) {
                    // Print the value of
                    // current element
                    document.write(arr[i] + " ");
                }
            }
        }

        // Driver Code

        let M = 5;
        let arr = [2, 81, 75, 98, 72,
            63, 53, 5, 40, 92];
        let N = arr.length;
        removeSmallestM(arr, N, M);

    // This code is contributed by Potta Lokesh

</script>
```

**Output:** 

```
81 75 98 72 92
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*