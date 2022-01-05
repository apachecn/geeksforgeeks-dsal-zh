# 子阵列异或相等的阵列中的三元组数量

> 原文:[https://www . geeksforgeeks . org/数组中具有子数组的三元组数量-xor-equal/](https://www.geeksforgeeks.org/number-of-triplets-in-array-having-subarray-xor-equal/)

给定整数数组 **Arr** 。任务是计算三胞胎 **(i，j，k)** 的数量，使得**a<sub>I</sub>^ a<sub>I+1</sub>^ a<sub>I+2</sub>^。^ a<sub>j-1</sub>= a<sub>j</sub>^ a<sub>j+1</sub>^ a<sub>j+2</sub>^…..^ A <sub>k</sub>** ， **0 ≤i < j≤ k < N** ，其中 **N** 为数组的大小。
其中 **^** 是两个数的**按位异或**。

**示例:**

> **输入:** Arr = {5，2，7}
> **输出:** 2
> 三元组是(0，2，2)自 5 ^ 2 = 7 和(0，1，2)自 2 ^ 7 = 5。
> 
> **输入:** Arr = {1，2，3，4，5}
> **输出:** 5

**蛮力方法:**一个简单的解决方案是运行三个嵌套循环，遍历 **i** 、 **j** 和 **k** 的所有可能值，然后运行另一个循环来计算第一和第二子阵列的 xor。
本方案时间复杂度为 **O(N <sup>4</sup> )** 。

## C++

```
// A simple C++ program to find Number of triplets
// in array having subarray xor equal
#include <bits/stdc++.h>
using namespace std;

// Function to return the count
int xor_triplet(int arr[], int n)
{
    // Initialise result
    int ans = 0;

    // Pick 1st element of the triplet
    for (int i = 0; i < n; i++) {

        // Pick 2nd element of the triplet
        for (int j = i + 1; j < n; j++) {

            // Pick 3rd element of the triplet
            for (int k = j; k < n; k++) {

                int xor1 = 0, xor2 = 0;

                // Taking xor in the
                // first subarray
                for (int x = i; x < j; x++) {
                    xor1 ^= arr[x];
                }

                // Taking xor in the
                // second subarray
                for (int x = j; x <= k; x++) {
                    xor2 ^= arr[x];
                }

                // If both xor is equal
                if (xor1 == xor2) {
                    ans++;
                }
            }
        }
    }
    return ans;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function Calling
    cout << xor_triplet(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find Number of triplets
// in array having subarray xor equal
class GFG
{

// Function to return the count
static int xor_triplet(int arr[], int n)
{
    // Initialise result
    int ans = 0;

    // Pick 1st element of the triplet
    for (int i = 0; i < n; i++)
    {

        // Pick 2nd element of the triplet
        for (int j = i + 1; j < n; j++)
        {

            // Pick 3rd element of the triplet
            for (int k = j; k < n; k++)
            {
                int xor1 = 0, xor2 = 0;

                // Taking xor in the
                // first subarray
                for (int x = i; x < j; x++)
                {
                    xor1 ^= arr[x];
                }

                // Taking xor in the
                // second subarray
                for (int x = j; x <= k; x++)
                {
                    xor2 ^= arr[x];
                }

                // If both xor is equal
                if (xor1 == xor2)
                {
                    ans++;
                }
            }
        }
    }
    return ans;
}

// Driver Code
public static void main (String[] args)
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int n = arr.length;

    // Function Calling
    System.out.println(xor_triplet(arr, n));
}
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# A simple python3 program to find Number of triplets
# in array having subarray xor equal

# Function to return the count
def xor_triplet(arr, n):

    # Initialise result
    ans = 0;

    # Pick 1st element of the triplet
    for i in range(n):

        # Pick 2nd element of the triplet
        for j in range(i + 1, n):

            # Pick 3rd element of the triplet
            for k in range(j, n):

                xor1 = 0; xor2 = 0;

                # Taking xor in the
                # first subarray
                for x in range(i, j):
                    xor1 ^= arr[x];

                # Taking xor in the
                # second subarray
                for x in range(j, k + 1):
                    xor2 ^= arr[x];

                # If both xor is equal
                if (xor1 == xor2):
                    ans += 1;

    return ans;

# Driver Code
if __name__ == '__main__':
    arr = [1, 2, 3, 4, 5];
    n = len(arr);

    # Function Calling
    print(xor_triplet(arr, n));

# This code is contributed by PrinciRaj1992
```

## C#

```
// C# program to find Number of triplets
// in array having subarray xor equal
using System;

class GFG
{

// Function to return the count
static int xor_triplet(int []arr, int n)
{
    // Initialise result
    int ans = 0;

    // Pick 1st element of the triplet
    for (int i = 0; i < n; i++)
    {

        // Pick 2nd element of the triplet
        for (int j = i + 1; j < n; j++)
        {

            // Pick 3rd element of the triplet
            for (int k = j; k < n; k++)
            {
                int xor1 = 0, xor2 = 0;

                // Taking xor in the
                // first subarray
                for (int x = i; x < j; x++)
                {
                    xor1 ^= arr[x];
                }

                // Taking xor in the
                // second subarray
                for (int x = j; x <= k; x++)
                {
                    xor2 ^= arr[x];
                }

                // If both xor is equal
                if (xor1 == xor2)
                {
                    ans++;
                }
            }
        }
    }
    return ans;
}

// Driver Code
public static void Main (String[] args)
{
    int []arr = { 1, 2, 3, 4, 5 };
    int n = arr.Length;

    // Function Calling
    Console.WriteLine(xor_triplet(arr, n));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// A simple Javascript program to find Number of triplets
// in array having subarray xor equal

// Function to return the count
function xor_triplet(arr, n) {
    // Initialise result
    let ans = 0;

    // Pick 1st element of the triplet
    for (let i = 0; i < n; i++) {

        // Pick 2nd element of the triplet
        for (let j = i + 1; j < n; j++) {

            // Pick 3rd element of the triplet
            for (let k = j; k < n; k++) {

                let xor1 = 0, xor2 = 0;

                // Taking xor in the
                // first subarray
                for (let x = i; x < j; x++) {
                    xor1 ^= arr[x];
                }

                // Taking xor in the
                // second subarray
                for (let x = j; x <= k; x++) {
                    xor2 ^= arr[x];
                }

                // If both xor is equal
                if (xor1 == xor2) {
                    ans++;
                }
            }
        }
    }
    return ans;
}

// Driver Code

let arr = [1, 2, 3, 4, 5];
let n = arr.length;

// Function Calling
document.write(xor_triplet(arr, n))

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output**

```
5
```

时间复杂度:O(N <sup>4</sup> )

辅助空间:0(1)

**有效方法:**

*   一个有效的解决方案是使用 [**Trie**](https://www.geeksforgeeks.org/trie-insert-and-search/) 。
*   一个观察是如果从 **i** 到 **k** 的子阵列有 **A <sub>i</sub> ^ A <sub>i+1</sub> ^ …^ A <sub>k</sub> = 0** 然后我们可以选择任意一个 **j** ，这样 **i < j < = k** 就会一直满足我们的条件。
*   这个观察结果将用于计算三胞胎的数量。
*   我们将对数组中的元素进行累积异或运算，并检查这个**异或值**是否存在于**特里**中。
    1.  如果异或已经存在于 **Trie** 中，那么我们已经遇到了一个具有 **0** 异或的子阵列，并对所有三元组进行计数。
    2.  否则将异或值推入**特里**。

下面是上述方法的实现:

## C++

```
// C++ trie based program to find the Number of
// triplets in array having subarray xor equal
#include <bits/stdc++.h>
using namespace std;

// maximum number of bits
// in an integer <= 1e9
#define lg 31

// Structure of a Trie Node
struct TrieNode {

    // [0] index is bit 0
    // and [1] index is bit 1
    TrieNode* children[2];

    // Sum of indexes
    // inserted at at a node
    int sum_of_indexes;

    // Number of indexes
    // inserted at a node
    int number_of_indexes;

    // Constructor to initialize
    // a newly created node
    TrieNode()
    {

        this->children[0] = nullptr;
        this->children[1] = nullptr;
        this->sum_of_indexes = 0;
        this->number_of_indexes = 0;
    }
};

// Function to insert curr_xor
// into the trie
void insert(TrieNode* node,
            int num,
            int index)
{

    // Iterate from the 31st bit
    // to the 0th bit of curr_xor
    // number
    for (int bits = lg; bits >= 0; bits--) {

        // Check if the current
        // bit is set or not
        int curr_bit = (num >> bits) & 1;

        // If this node isn't already
        // present in the trie structure
        // insert it into the trie.
        if (node->children[curr_bit]
            == nullptr) {
            node->children[curr_bit]
                = new TrieNode();
        }

        node = node->children[curr_bit];
    }

    // Increase the sum of
    // indexes by the current
    // index value
    node->sum_of_indexes += index;

    // Increase the number
    // of indexes by 1
    node->number_of_indexes++;
}

// Function to check if curr_xor
// is present in trie or not
int query(TrieNode* node,
          int num,
          int index)
{

    // Iterate from the 31st bit
    // to the 0th bit of curr_xor number
    for (int bits = lg; bits >= 0; bits--) {

        // Check if the current bit
        // is set or not
        int curr_bit = (num >> bits) & 1;

        // If this node isn't already
        // present in the trie structure
        // that means no sub array till
        // current index has 0 xor so
        // return 0
        if (node->children[curr_bit]
            == nullptr) {
            return 0;
        }

        node = node->children[curr_bit];
    }

    // Calculate the number of index
    // inserted at final node
    int sz = node->number_of_indexes;

    // Calculate the sum of index
    // inserted at final node
    int sum = node->sum_of_indexes;

    int ans = (sz * index) - (sum);

    return ans;
}

// Function to return the count of
// valid triplets
int no_of_triplets(int arr[], int n)
{

    // To store cumulative xor
    int curr_xor = 0;

    int number_of_triplets = 0;

    // The root of the trie
    TrieNode* root = new TrieNode();

    for (int i = 0; i < n; i++) {

        int x = arr[i];

        // Insert the curr_xor in the trie
        insert(root, curr_xor, i);

        // Update the cumulative xor
        curr_xor ^= x;

        // Check if the cumulative xor
        // is present in the trie or not
        // if present then add
        // (sz * index) - sum
        number_of_triplets
            += query(root, curr_xor, i);
    }

    return number_of_triplets;
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 5, 2, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << no_of_triplets(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java trie based program to find the Number of
// triplets in array having subarray xor equal
class GFG
{

// maximum number of bits
// in an integer <= 1e9
static int lg = 31;

// Structure of a Trie Node
static class TrieNode
{

    // [0] index is bit 0
    // and [1] index is bit 1
    TrieNode children[];

    // Sum of indexes
    // inserted at at a node
    int sum_of_indexes;

    // Number of indexes
    // inserted at a node
    int number_of_indexes;

    // Constructor to initialize
    // a newly created node
    TrieNode()
    {
        children = new TrieNode[2];
        this.children[0] = null;
        this.children[1] = null;
        this.sum_of_indexes = 0;
        this.number_of_indexes = 0;
    }
};

// Function to insert curr_xor
// into the trie
static void insert(TrieNode node,
                    int num,
                    int index)
{

    // Iterate from the 31st bit
    // to the 0th bit of curr_xor
    // number
    for (int bits = lg; bits >= 0; bits--)
    {

        // Check if the current
        // bit is set or not
        int curr_bit = (num >> bits) & 1;

        // If this node isn't already
        // present in the trie structure
        // insert it into the trie.
        if (node.children[curr_bit]
            == null)
        {
            node.children[curr_bit]
                = new TrieNode();
        }

        node = node.children[curr_bit];
    }

    // Increase the sum of
    // indexes by the current
    // index value
    node.sum_of_indexes += index;

    // Increase the number
    // of indexes by 1
    node.number_of_indexes++;
}

// Function to check if curr_xor
// is present in trie or not
static int query(TrieNode node,
                  int num,
                  int index)
{

    // Iterate from the 31st bit
    // to the 0th bit of curr_xor number
    for (int bits = lg; bits >= 0; bits--)
    {

        // Check if the current bit
        // is set or not
        int curr_bit = (num >> bits) & 1;

        // If this node isn't already
        // present in the trie structure
        // that means no sub array till
        // current index has 0 xor so
        // return 0
        if (node.children[curr_bit]
            == null)
        {
            return 0;
        }

        node = node.children[curr_bit];
    }

    // Calculate the number of index
    // inserted at final node
    int sz = node.number_of_indexes;

    // Calculate the sum of index
    // inserted at final node
    int sum = node.sum_of_indexes;

    int ans = (sz * index) - (sum);

    return ans;
}

// Function to return the count of
// valid triplets
static int no_of_triplets(int arr[], int n)
{

    // To store cumulative xor
    int curr_xor = 0;

    int number_of_triplets = 0;

    // The root of the trie
    TrieNode root = new TrieNode();

    for (int i = 0; i < n; i++)
    {

        int x = arr[i];

        // Insert the curr_xor in the trie
        insert(root, curr_xor, i);

        // Update the cumulative xor
        curr_xor ^= x;

        // Check if the cumulative xor
        // is present in the trie or not
        // if present then add
        // (sz * index) - sum
        number_of_triplets
            += query(root, curr_xor, i);
    }

    return number_of_triplets;
}

// Driver Code
public static void main(String args[])
{
    // Given array
    int arr[] = { 5, 2, 7 };
    int n = arr.length;

    System.out.println(no_of_triplets(arr, n));
}
}

// This code is contributed by Arnab Kundu
```

**Output**

```
2
```

**时间复杂度:**O(31 * N)
T3】辅助空间 : O(N)。