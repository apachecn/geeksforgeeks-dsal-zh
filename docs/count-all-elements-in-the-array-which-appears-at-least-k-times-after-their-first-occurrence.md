# 统计数组中第一次出现后出现至少 K 次的所有元素

> 原文:[https://www . geesforgeks . org/count-数组中的所有元素在首次出现后至少出现 k 次/](https://www.geeksforgeeks.org/count-all-elements-in-the-array-which-appears-at-least-k-times-after-their-first-occurrence/)

给定一个由 **N** 整数元素和一个整数 **K** 组成的数组**。任务是计算所有不同的 **arr[i]** ，使得 **arr[i]** 在索引范围 **i + 1** 到**n–1**中至少出现 **K** 次。**

**示例:**

> **输入:** arr[] = {1，2，1，3}，K = 1
> **输出:** 1
> arr[0] = 1 是索引范围[1，3]中唯一至少出现一次的元素，即 arr[2]
> 
> **输入:** arr[] = {1，2，3，2，1，3，1，2，1}，K = 2
> **输出:** 2

**天真方法:**从 i = 0 到 n-1 开始，计算 arr[i]在 i+1 到 n-1 范围内的出现次数。如果计数大于或等于 K，将结果增加 1。创建一个散列数组以避免重复。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <iostream>
#include <map>
using namespace std;

// Function to return the count of
// all distinct valid elements
int countOccurrence(int n, int arr[], int k)
{
    int cnt, ans = 0;

    // To avoid duplicates
    map<int, bool> hash;

    // Traverse the complete array
    for (int i = 0; i < n; i++) {
        cnt = 0;

        // If current element is previously checked
        // don't check it again
        if (hash[arr[i]] == true)
            continue;

        // To avoid duplicates
        hash[arr[i]] = true;

        // Count occurrence of arr[i] in range [i + 1, n - 1]
        for (int j = i + 1; j < n; j++) {
            if (arr[j] == arr[i])
                cnt++;

            // If count becomes equal to K
            // break the loop
            if (cnt >= k)
                break;
        }

        // If cnt >= K
        // increment ans by 1
        if (cnt >= k)
            ans++;
    }

    return ans;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 1, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 1;
    cout << countOccurrence(n, arr, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.HashMap;

class GFG
{

    // Function to return the count of
    // all distinct valid elements
    public static int countOccurence(int n, int[] arr, int k)
    {
        int cnt, ans = 0;

        // To avoid duplicates
        HashMap<Integer, Boolean> hash = new HashMap<>();

        // Traverse the complete array
        for (int i = 0; i < n; i++)
        {
            cnt = 0;

            // If current element is previously checked
            // don't check it again
            if (hash.get(arr[i]) != null && hash.get(arr[i]) == true)
                continue;

                // To avoid duplicates
                hash.put(arr[i], true);

                // Count occurrence of arr[i] in range [i + 1, n - 1]
                for (int j = i + 1; j < n; j++)
                {
                    if (arr[j] == arr[i])
                        cnt++;

                    // If count becomes equal to K
                    // break the loop
                    if (cnt >= k)
                    break;
                }

                // If cnt >= K
                // increment ans by 1
                if (cnt >= k)
                    ans++;
        }

        return ans;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = {1, 2, 1, 3};
        int n = arr.length;
        int k = 1;
        System.out.println(countOccurence(n, arr, k));
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of
# all distinct valid elements
def countOccurrence(n, arr, k):

    cnt, ans = 0, 0

    # To avoid duplicates
    Hash = dict()

    # Traverse the complete array
    for i in range(n):
        cnt = 0

        # If current element is previously
        # checked don't check it again
        if (arr[i] in Hash.keys()):
            continue

        # To avoid duplicates
        Hash[arr[i]] = 1

        # Count occurrence of arr[i] in
        # range [i + 1, n - 1]
        for j in range(i + 1, n):
            if (arr[j] == arr[i]):
                cnt += 1

            # If count becomes equal to K
            # break the loop
            if (cnt >= k):
                break

        # If cnt >= K
        # increment ans by 1
        if (cnt >= k):
            ans += 1

    return ans

# Driver code
arr = [1, 2, 1, 3]
n = len(arr)
k = 1
print(countOccurrence(n, arr, k))

# This code is contributed
# by mohit kumar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to return the count of
// all distinct valid elements
public static int countOccurence(int n,
                                 int[] arr, int k)
{
    int cnt, ans = 0;

    // To avoid duplicates
    Dictionary<int,
               Boolean> hash = new Dictionary<int,
                                              Boolean>();

    // Traverse the complete array
    for (int i = 0; i < n; i++)
    {
        cnt = 0;

        // If current element is previously checked
        // don't check it again
        if (hash.ContainsKey(arr[i]) &&
            hash[arr[i]] == true)
            continue;

            // To avoid duplicates
            hash.Add(arr[i], true);

            // Count occurrence of arr[i]
            // in range [i + 1, n - 1]
            for (int j = i + 1; j < n; j++)
            {
                if (arr[j] == arr[i])
                    cnt++;

                // If count becomes equal to K
                // break the loop
                if (cnt >= k)
                break;
            }

            // If cnt >= K
            // increment ans by 1
            if (cnt >= k)
                ans++;
    }

    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    int[] arr = {1, 2, 1, 3};
    int n = arr.Length;
    int k = 1;
    Console.WriteLine(countOccurence(n, arr, k));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

    // Function to return the count of
    // all distinct valid elements
   function countOccurence(n, arr, k)
    {
        let cnt, ans = 0;

        // To avoid duplicates
        let hash = new Map();

        // Traverse the complete array
        for (let i = 0; i < n; i++)
        {
            cnt = 0;

            // If current element is previously checked
            // don't check it again
            if (hash.get(arr[i]) != null &&
            hash.get(arr[i]) == true)
                continue;

                // To avoid duplicates
                hash.set(arr[i], true);

                // Count occurrence of arr[i]
                // in range [i + 1, n - 1]
                for (let j = i + 1; j < n; j++)
                {
                    if (arr[j] == arr[i])
                        cnt++;

                    // If count becomes equal to K
                    // break the loop
                    if (cnt >= k)
                    break;
                }

                // If cnt >= K
                // increment ans by 1
                if (cnt >= k)
                    ans++;
        }

        return ans;
    }

    // Driver code

         let arr = [1, 2, 1, 3];
        let n = arr.length;
        let k = 1;
        document.write(countOccurence(n, arr, k));

</script>
```

**Output:** 

```
1
```

**时间复杂度:** O(n <sup>2</sup>

**高效方法:**声明另一个哈希映射来存储所有元素的出现，并从 n–1 到 0 开始。如果出现[arr[i]] ≥ k，则将计数增加 1，否则将 arr[i]的出现增加 1。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <iostream>
#include <map>
using namespace std;

// Function to return the count of
// all distinct valid elements
int countOccurrence(int n, int arr[], int k)
{
    int cnt, ans = 0;

    // To avoid duplicates
    map<int, bool> hash;

    // To store the count of arr[i]
    // in range [i + 1, n - 1]
    map<int, int> occurrence;

    for (int i = n - 1; i >= 0; i--) {

        // To avoid duplicates
        if (hash[arr[i]] == true)
            continue;

        // If occurrence in range i+1 to n becomes
        // equal to K then increment ans by 1
        if (occurrence[arr[i]] >= k) {
            ans++;
            hash[arr[i]] = true;
        }

        // Otherwise increase occurrence of arr[i] by 1
        else
            occurrence[arr[i]]++;
    }

    return ans;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 1, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 1;
    cout << countOccurrence(n, arr, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.HashMap;

class GFG
{

    // Function to return the count of
    // all distinct valid elements
    public static int countOccurence(int n, int[] arr, int k)
    {
        int ans = 0;

        // To avoid duplicates
        HashMap<Integer, Boolean> hash = new HashMap<>();

        // To store the count of arr[i]
        // in range [i + 1, n - 1]
        HashMap<Integer, Integer> occurence = new HashMap<>();

        for (int i = n-1; i>=0; i--)
        {

            // To avoid duplicates
            if (hash.get(arr[i]) != null &&
                hash.get(arr[i]) == true)
                continue;

            // If occurrence in range i+1 to n becomes
            // equal to K then increment ans by 1
            if (occurence.get(arr[i]) != null &&
                occurence.get(arr[i]) >= k)
            {
                ans++;
                hash.put(arr[i], true);
            }

            // Otherwise increase occurrence of arr[i] by 1
            else
            {
                if (occurence.get(arr[i]) == null)
                    occurence.put(arr[i], 1);
                else
                {
                    int temp = occurence.get(arr[i]);
                    occurence.put(arr[i], ++temp);
                }
            }
        }

        return ans;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = {1, 2, 1, 3};
        int n = arr.length;
        int k = 1;
        System.out.println(countOccurence(n, arr, k));
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of
# all distinct valid elements
def countOccurrence(n, arr, k) :

    ans = 0;

    # To avoid duplicates
    hash = dict.fromkeys(arr,0);

    # To store the count of arr[i]
    # in range [i + 1, n - 1]
    occurrence = dict.fromkeys(arr, 0);

    for i in range(n - 1, -1, -1) :

        # To avoid duplicates
        if (hash[arr[i]] == True) :
            continue;

        # If occurrence in range i+1 to n
        # becomes equal to K then increment
        # ans by 1
        if (occurrence[arr[i]] >= k) :
            ans += 1;
            hash[arr[i]] = True;

        # Otherwise increase occurrence
        # of arr[i] by 1
        else :
            occurrence[arr[i]] += 1;

    return ans;

# Driver code
if __name__ == "__main__" :

    arr = [ 1, 2, 1, 3 ];
    n = len(arr) ;
    k = 1;
    print(countOccurrence(n, arr, k));

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

    // Function to return the count of
    // all distinct valid elements
    public static int countOccurence(int n,
                                     int[] arr,
                                     int k)
    {
        int ans = 0;

        // To avoid duplicates
        Dictionary<int,
                   bool> hash = new Dictionary<int,
                                               bool>();

        // To store the count of arr[i]
        // in range [i + 1, n - 1]
        Dictionary<int,    
                   int> occurence = new Dictionary<int,
                                                   int>();

        for (int i = n - 1; i >= 0; i--)
        {

            // To avoid duplicates
            if (hash.ContainsKey(arr[i]) &&
                hash[arr[i]] == true)
                continue;

            // If occurrence in range i+1 to n becomes
            // equal to K then increment ans by 1
            if (occurence.ContainsKey(arr[i]) &&
                occurence[arr[i]] >= k)
            {
                ans++;
                hash.Add(arr[i], true);
            }

            // Otherwise increase occurrence of arr[i] by 1
            else
            {
                if (!occurence.ContainsKey(arr[i]))
                    occurence.Add(arr[i], 1);
                else
                {
                    int temp = occurence[arr[i]];
                    occurence.Add(arr[i], ++temp);
                }
            }
        }
        return ans;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int[] arr = {1, 2, 1, 3};
        int n = arr.Length;
        int k = 1;
        Console.WriteLine(countOccurence(n, arr, k));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the count of
// all distinct valid elements
function countOccurence(n, arr, k)
{
    let ans = 0;

    // To avoid duplicates
    let hash = new Map();

    // To store the count of arr[i]
    // in range [i + 1, n - 1]
    let occurence = new Map();

    for(let i = n - 1; i >= 0; i--)
    {

        // To avoid duplicates
        if (hash.get(arr[i]) != null &&
            hash.get(arr[i]) == true)
            continue;

        // If occurrence in range i+1 to n becomes
        // equal to K then increment ans by 1
        if (occurence.get(arr[i]) != null &&
            occurence.get(arr[i]) >= k)
        {
            ans++;
            hash.set(arr[i], true);
        }

        // Otherwise increase occurrence of arr[i] by 1
        else
        {
            if (occurence.get(arr[i]) == null)
                occurence.set(arr[i], 1);
            else
            {
                let temp = occurence.get(arr[i]);
                occurence.set(arr[i], ++temp);
            }
        }
    }
    return ans;
}

// Driver Code
let arr = [ 1, 2, 1, 3 ];
let n = arr.length;
let k = 1;

document.write(countOccurence(n, arr, k));

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
1
```

**时间复杂度:** O(n)