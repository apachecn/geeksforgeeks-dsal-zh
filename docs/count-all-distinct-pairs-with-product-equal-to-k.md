# 计算乘积等于 K 的所有不同对

> 原文:[https://www . geesforgeks . org/count-all-distinct-pairs-with-product-equal-to-k/](https://www.geeksforgeeks.org/count-all-distinct-pairs-with-product-equal-to-k/)

给定一个大小为 **N** 的整数数组**arr【】**和一个正整数 **K** ，任务是用等于 K 的乘积对数组中所有不同的对进行计数。
**示例:**

> **输入:** arr[] = {1，5，3，4，2}，K = 3
> **输出:** 1
> **说明:**
> 只有一对(1，3)积= K = 3。
> **输入:** arr[] = {1，2，16，4，4}，K = 16
> **输出:** 2
> **说明:**
> 有两对(1，16)和(4，4)，乘积= K = 16。

***高效方法:*** 想法是使用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)。

1.  最初，将数组中的所有元素插入到[散列表](https://www.geeksforgeeks.org/java-util-hashmap-in-java-with-examples/)中。插入时，如果 hashmap 中已经存在特定元素，则忽略。
2.  现在，我们在散列中有所有唯一的元素。因此，对于数组 arr[i]中的每个元素，我们检查 hashmap 中是否存在 **arr[i] / K** 。
3.  如果该值存在，那么我们增加计数并从散列中移除该特定元素(以获得唯一的对)。

以下是上述方法的实现:

## C++

```
// C++ program to count the number of pairs
// whose product is equal to K

#include <algorithm>
#include <iostream>
using namespace std;
#define MAX 100000

// Function to count the number of pairs
// whose product is equal to K
int countPairsWithProductK(int arr[], int n, int k)
{
    // Initialize the count
    int count = 0;

    // Initialize empty hashmap.
    bool hashmap[MAX] = { false };

    // Insert array elements to hashmap
    for (int i = 0; i < n; i++)
        hashmap[arr[i]] = true;

    for (int i = 0; i < n; i++) {
        int x = arr[i];

        double index = 1.0 * k / arr[i];

        // Checking if the index is a whole number
        // and present in the hashmap
        if (index >= 0
            && ((index - (int)(index)) == 0)
            && hashmap[k / x])

            count++;
        hashmap[x] = false;
    }
    return count;
}

// Driver code
int main()
{
    int arr[] = { 1, 5, 3, 4, 2 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 3;

    cout << countPairsWithProductK(arr, N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the number of pairs
// whose product is equal to K

class GFG
{
    static int MAX = 100000;

    // Function to count the number of pairs
    // whose product is equal to K
    static int countPairsWithProductK(int arr[], int n, int k)
    {
        // Initialize the count
        int count = 0;
        int i;

        // Initialize empty hashmap.
        boolean hashmap[] = new boolean[MAX];

        // Insert array elements to hashmap
        for (i = 0; i < n; i++)
            hashmap[arr[i]] = true;

        for (i = 0; i < n; i++) {
            int x = arr[i];

            double index = 1.0 * k / arr[i];

            // Checking if the index is a whole number
            // and present in the hashmap
            if (index >= 0
                && ((index - (int)(index)) == 0)
                && hashmap[k / x])

                count++;
            hashmap[x] = false;
        }
        return count;
    }

    // Driver code
    public static void main(String []args)
    {
        int arr[] = { 1, 5, 3, 4, 2 };
        int N = arr.length;
        int K = 3;

        System.out.print(countPairsWithProductK(arr, N, K));

    }
}
```

## 蟒蛇 3

```
# Python3 program to count the number of pairs
# whose product is equal to K
MAX = 100000;

# Function to count the number of pairs
# whose product is equal to K
def countPairsWithProductK(arr, n, k) :

    # Initialize the count
    count = 0;

    # Initialize empty hashmap.
    hashmap = [False]*MAX ;

    # Insert array elements to hashmap
    for i in range(n) :
        hashmap[arr[i]] = True;

    for i in range(n) :
        x = arr[i];

        index = 1.0 * k / arr[i];

        # Checking if the index is a whole number
        # and present in the hashmap
        if (index >= 0
            and ((index - int(index)) == 0)
            and hashmap[k // x]) :

                count += 1;

        hashmap[x] = False;

    return count;

# Driver code
if __name__ == "__main__" :
    arr = [ 1, 5, 3, 4, 2 ];
    N = len(arr);
    K = 3;

    print(countPairsWithProductK(arr, N, K));

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to count the number of pairs
// whose product is equal to K     
using System;

class GFG
{
    static int MAX = 100000;

    // Function to count the number of pairs
    // whose product is equal to K
    static int countPairsWithProductK(int []arr, int n, int k)
    {
        // Initialize the count
        int count = 0;
        int i;

        // Initialize empty hashmap.
        bool []hashmap = new bool[MAX];

        // Insert array elements to hashmap
        for (i = 0; i < n; i++)
            hashmap[arr[i]] = true;

        for (i = 0; i < n; i++) {
            int x = arr[i];

            double index = 1.0 * k / arr[i];

            // Checking if the index is a whole number
            // and present in the hashmap
            if (index >= 0
                && ((index - (int)(index)) == 0)
                && hashmap[k / x])

                count++;
            hashmap[x] = false;
        }
        return count;
    }

    // Driver code
    public static void Main(String []args)
    {
        int []arr = { 1, 5, 3, 4, 2 };
        int N = arr.Length;
        int K = 3;

        Console.Write(countPairsWithProductK(arr, N, K));         
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to count the number of pairs
// whose product is equal to K

    let MAX = 100000;

    // Function to count the number of pairs
    // whose product is equal to K
    function countPairsWithProductK(arr,n,k)
    {
        // Initialize the count
        let count = 0;
        let i;

        // Initialize empty hashmap.
        let hashmap = new Array(MAX);

        // Insert array elements to hashmap
        for (i = 0; i < n; i++)
            hashmap[arr[i]] = true;

        for (i = 0; i < n; i++) {
            let x = arr[i];

            let index = 1.0 * k / arr[i];

            // Checking if the index is a whole number
            // and present in the hashmap
            if (index >= 0
                && ((index - Math.floor(index)) == 0)
                && hashmap[k / x])

                count++;
            hashmap[x] = false;
        }
        return count;
    }

    // Driver code
    let arr=[1, 5, 3, 4, 2];
    let N = arr.length;
    let K = 3;
    document.write(countPairsWithProductK(arr, N, K));

// This code is contributed by rag2127

</script>
```

**Output:** 

```
1
```

**时间复杂度:** O(N * log(N))

**辅助空间:** O(MAX)