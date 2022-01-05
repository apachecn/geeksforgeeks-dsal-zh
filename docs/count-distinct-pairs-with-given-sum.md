# 用给定的和计数不同的对

> 原文:[https://www . geesforgeks . org/count-distinct-pairs-with-given-sum/](https://www.geeksforgeeks.org/count-distinct-pairs-with-given-sum/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和一个整数 **K** ，任务是找出数组中不同对的计数，其和等于 **K** 。

**示例:**

> **输入:** arr[] = { 5，6，5，7，7，8 }，K = 13
> **输出:** 2
> **解释:**
> 和 K =(13)成对的是{ (arr[0]，arr[5])，(arr[1]，arr[3])，(arr[1]，arr[4]) }，即{(5，8)，(6，7)，(6，7)}。
> 因此，具有和 K( = 13)的不同对是{ (arr[0]，arr[5])，(arr[1]，arr[3]) }。
> 因此，要求输出为 2。
> 
> **输入:** arr[] = { 2，6，7，1，8，3 }，K = 10
> **输出:** : 2
> **解释:**
> 和 K( = 13)不同的对是{ (arr[0]，arr[4])，(arr[2]，arr[5]) }。
> 因此，要求的输出为 2。

**天真方法:**解决这个问题最简单的方法就是使用[双指针技术](https://www.geeksforgeeks.org/two-pointers-technique/)。想法是[排序数组](https://www.geeksforgeeks.org/sort-c-stl/)和[从给定数组](https://www.geeksforgeeks.org/remove-consecutive-duplicates-string/)中移除所有连续的重复元素。最后，[统计给定数组中和等于 K](https://www.geeksforgeeks.org/count-pairs-with-given-sum-set-2/) 的对。按照以下步骤解决问题:

*   初始化一个变量，比如说 **cntPairs** ，用 sum **K** 存储数组中不同对的计数。
*   [按递增顺序排列数组](https://www.geeksforgeeks.org/sort-c-stl/)。
*   初始化两个变量，比如说 **i = 0** ，**j = N–1**作为左右指针遍历数组的索引。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并检查以下条件:
    *   **如果 arr[i] + arr[j] == K:** [删除连续的重复数组元素](https://www.geeksforgeeks.org/remove-consecutive-duplicates-string/)，并将**对**增加 **1** 。更新 **i = i + 1** 和**j = j–1**。
    *   如果 **arr[i] + arr[j] < K** 则更新 **i = i + 1** 。
    *   否则，更新**j = j–1**。
*   最后，打印 **cntPairs** 的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count distinct pairs
// in array whose sum equal to K
int cntDisPairs(int arr[],
                int N, int K)
{
    // Stores count of distinct pairs
    // whose sum equal to K
    int cntPairs = 0;

    // Sort the array
    sort(arr, arr + N);

    // Stores index of
    // the left pointer
    int i = 0;

    // Stores index of
    // the right pointer
    int j = N - 1;

    // Calculate count of distinct
    // pairs whose sum equal to K
    while (i < j) {

        // If sum of current pair
        // is equal to K
        if (arr[i] + arr[j] == K) {

            // Remove consecutive duplicate
            // array elements
            while (i < j && arr[i] == arr[i + 1]) {

                // Update i
                i++;
            }

            // Remove consecutive duplicate
            // array elements
            while (i < j && arr[j] == arr[j - 1]) {

                // Update j
                j--;
            }

            // Update cntPairs
            cntPairs += 1;

            // Update i
            i++;

            // Update j
            j--;
        }

        // if sum of current pair
        // less than K
        else if (arr[i] + arr[j] < K) {

            // Update i
            i++;
        }
        else {

            // Update j
            j--;
        }
    }
    return cntPairs;
}

// Driver Code
int main()
{
    int arr[] = { 5, 6, 5, 7, 7, 8 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 13;
    cout << cntDisPairs(arr, N, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to count distinct pairs
// in array whose sum equal to K
static int cntDisPairs(int arr[],
                int N, int K)
{
    // Stores count of distinct pairs
    // whose sum equal to K
    int cntPairs = 0;

    // Sort the array
    Arrays.sort(arr);

    // Stores index of
    // the left pointer
    int i = 0;

    // Stores index of
    // the right pointer
    int j = N - 1;

    // Calculate count of distinct
    // pairs whose sum equal to K
    while (i < j) {

        // If sum of current pair
        // is equal to K
        if (arr[i] + arr[j] == K) {

            // Remove consecutive duplicate
            // array elements
            while (i < j && arr[i] == arr[i + 1]) {

                // Update i
                i++;
            }

            // Remove consecutive duplicate
            // array elements
            while (i < j && arr[j] == arr[j - 1]) {

                // Update j
                j--;
            }

            // Update cntPairs
            cntPairs += 1;

            // Update i
            i++;

            // Update j
            j--;
        }

        // if sum of current pair
        // less than K
        else if (arr[i] + arr[j] < K) {

            // Update i
            i++;
        }
        else {

            // Update j
            j--;
        }
    }
    return cntPairs;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 5, 6, 5, 7, 7, 8 };
    int N = arr.length;
    int K = 13;
    System.out.print(cntDisPairs(arr, N, K));
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to count distinct pairs
# in array whose sum equal to K
def cntDisPairs(arr, N, K):

    # Stores count of distinct pairs
    # whose sum equal to K
    cntPairs = 0

    # Sort the array
    arr = sorted(arr)

    # Stores index of
    # the left pointer
    i = 0

    # Stores index of
    # the right pointer
    j = N - 1

    # Calculate count of distinct
    # pairs whose sum equal to K
    while (i < j):

        # If sum of current pair
        # is equal to K
        if (arr[i] + arr[j] == K):

            # Remove consecutive duplicate
            # array elements
            while (i < j and arr[i] == arr[i + 1]):

                # Update i
                i += 1

            # Remove consecutive duplicate
            # array elements
            while (i < j and arr[j] == arr[j - 1]):

                # Update j
                j -= 1

            # Update cntPairs
            cntPairs += 1

            # Update i
            i += 1

            # Update j
            j -= 1

        # If sum of current pair
        # less than K
        elif (arr[i] + arr[j] < K):

            # Update i
            i += 1
        else:

            # Update j
            j -= 1

    return cntPairs

# Driver Code
if __name__ == '__main__':

    arr = [ 5, 6, 5, 7, 7, 8 ]
    N = len(arr)
    K = 13

    print(cntDisPairs(arr, N, K))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

// Function to count distinct pairs
// in array whose sum equal to K
static int cntDisPairs(int []arr,
                       int N, int K)
{

    // Stores count of distinct pairs
    // whose sum equal to K
    int cntPairs = 0;

    // Sort the array
    Array.Sort(arr);

    // Stores index of
    // the left pointer
    int i = 0;

    // Stores index of
    // the right pointer
    int j = N - 1;

    // Calculate count of distinct
    // pairs whose sum equal to K
    while (i < j)
    {

        // If sum of current pair
        // is equal to K
        if (arr[i] + arr[j] == K)
        {

            // Remove consecutive duplicate
            // array elements
            while (i < j && arr[i] == arr[i + 1])
            {

                // Update i
                i++;
            }

            // Remove consecutive duplicate
            // array elements
            while (i < j && arr[j] == arr[j - 1])
            {

                // Update j
                j--;
            }

            // Update cntPairs
            cntPairs += 1;

            // Update i
            i++;

            // Update j
            j--;
        }

        // If sum of current pair
        // less than K
        else if (arr[i] + arr[j] < K)
        {

            // Update i
            i++;
        }
        else
        {

            // Update j
            j--;
        }
    }
    return cntPairs;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 5, 6, 5, 7, 7, 8 };
    int N = arr.Length;
    int K = 13;

    Console.WriteLine(cntDisPairs(arr, N, K));
}
}

// This code is contributed by jana_sayantan
```

## java 描述语言

```
<script>

// javascript program to implement
// the above approach

// Function to count distinct pairs
// in array whose sum equal to K
function cntDisPairs(arr,N , K)
{
    // Stores count of distinct pairs
    // whose sum equal to K
    var cntPairs = 0;

    // Sort the array
    arr.sort();

    // Stores index of
    // the left pointer
    var i = 0;

    // Stores index of
    // the right pointer
    var j = N - 1;

    // Calculate count of distinct
    // pairs whose sum equal to K
    while (i < j) {

        // If sum of current pair
        // is equal to K
        if (arr[i] + arr[j] == K) {

            // Remove consecutive duplicate
            // array elements
            while (i < j && arr[i] == arr[i + 1]) {

                // Update i
                i++;
            }

            // Remove consecutive duplicate
            // array elements
            while (i < j && arr[j] == arr[j - 1]) {

                // Update j
                j--;
            }

            // Update cntPairs
            cntPairs += 1;

            // Update i
            i++;

            // Update j
            j--;
        }

        // if sum of current pair
        // less than K
        else if (arr[i] + arr[j] < K) {

            // Update i
            i++;
        }
        else {

            // Update j
            j--;
        }
    }
    return cntPairs;
}

// Driver Code

var arr = [ 5, 6, 5, 7, 7, 8 ];
var N = arr.length;
var K = 13;
document.write(cntDisPairs(arr, N, K));

// This code contributed by shikhasingrajput

</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N * log(N))*
***辅助空间:** O(1)*

**高效方法:**上述方法可以使用散列法进行优化。按照以下步骤解决问题:

*   使用两套，一套用于数字，一套用于以前见过的配对。
*   遍历数组，查看 set 中是否存在(target–arr[i])，seen 中是否不存在 arr[I]。
*   如果是，则在 seen 中同时添加 arr[i]和(target–arr[I])，并添加 1 进行计数。

下面是上述方法的实现:

## C++

```
// C++ program to implement
#include <bits/stdc++.h>
using namespace std;

int cntDisPairs(vector<int> arr, int target) {
    unordered_set<int> set;
    unordered_set<int> seen;

    int count = 0;

    for(int num : arr) {
        if(set.find(target-num) != set.end() && seen.find(num) == seen.end() ) {
            count++;
            seen.insert(num);
            seen.insert(target-num);
        }
        set.insert(num);
    }
    return count;
}

int main()
{
    vector<int> arr = { 1, 5, 1, 5};
    int K = 6;
    cout << cntDisPairs(arr, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG
{

// Function to count distinct pairs
// in array whose sum equal to K
static int cntDisPairs(int arr[],
                int N, int K)
{

    // Stores count of distinct pairs
    // whose sum equal to K
    int cntPairs = 0;

    // Store frequency of each distinct
    // element of the array
    HashMap<Integer,Integer> cntFre = new HashMap<Integer,Integer>();

    for (int i = 0; i < N; i++)
    {

        // Update frequency
        // of arr[i]
        if(cntFre.containsKey(arr[i]))
            cntFre.put(arr[i], cntFre.get(arr[i]) + 1);

        else
            cntFre.put(arr[i], 1);
    }

    // Traverse the map
    for (Map.Entry<Integer,Integer> it : cntFre.entrySet())
    {

        // Stores key value
        // of the map
        int i = it.getKey();

        // If i is the half of K
        if (2 * i == K)
        {

            // If frequency of i
            // greater than  1
            if (cntFre.get(i) > 1)
                cntPairs += 2;
        }

        else
        {
            if (cntFre.containsKey(K - i))
            {

                // Update cntPairs
                cntPairs += 1;
            }
        }
    }

    // Update cntPairs
    cntPairs = cntPairs / 2;
    return cntPairs;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 5, 6, 5, 7, 7, 8 };
    int N = arr.length;
    int K = 13;
    System.out.print(cntDisPairs(arr, N, K));
}
}

// This code  is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to count distinct pairs
# in array whose sum equal to K
def cntDisPairs(arr, N, K):

    # Stores count of distinct pairs
    # whose sum equal to K
    cntPairs = 0

    # Store frequency of each distinct
    # element of the array
    cntFre = {}

    for i in arr:

        # Update frequency
        # of arr[i]
        if i in cntFre:
            cntFre[i] += 1
        else:
            cntFre[i] = 1

    # Traverse the map
    for key, value in cntFre.items():

        # Stores key value
        # of the map
        i = key

        # If i is the half of K
        if (2 * i == K):

            # If frequency of i
            # greater than  1
            if (cntFre[i] > 1):
                cntPairs += 2
        else:
            if (cntFre[K - i]):

                # Update cntPairs
                cntPairs += 1

    # Update cntPairs
    cntPairs = cntPairs / 2

    return cntPairs

# Driver Code
arr = [ 5, 6, 5, 7, 7, 8 ]
N = len(arr)
K = 13

print(int(cntDisPairs(arr, N, K)))

# This code is contributed by Dharanendra L V
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;
class GFG
{

  // Function to count distinct pairs
  // in array whose sum equal to K
  static int cntDisPairs(int []arr,
                         int N, int K)
  {

    // Stores count of distinct pairs
    // whose sum equal to K
    int cntPairs = 0;

    // Store frequency of each distinct
    // element of the array
    Dictionary<int,int> cntFre = new Dictionary<int,int>();

    for (int i = 0; i < N; i++)
    {

      // Update frequency
      // of arr[i]
      if(cntFre.ContainsKey(arr[i]))
        cntFre[arr[i]] = cntFre[arr[i]] + 1;

      else
        cntFre.Add(arr[i], 1);
    }

    // Traverse the map
    foreach (KeyValuePair<int,int> it in cntFre)
    {

      // Stores key value
      // of the map
      int i = it.Key;

      // If i is the half of K
      if (2 * i == K)
      {

        // If frequency of i
        // greater than  1
        if (cntFre[i] > 1)
          cntPairs += 2;
      }

      else
      {
        if (cntFre.ContainsKey(K - i))
        {

          // Update cntPairs
          cntPairs += 1;
        }
      }
    }

    // Update cntPairs
    cntPairs = cntPairs / 2;
    return cntPairs;
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int []arr = { 5, 6, 5, 7, 7, 8 };
    int N = arr.Length;
    int K = 13;
    Console.Write(cntDisPairs(arr, N, K));
  }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// javascript program to implement
// the above approach

    // Function to count distinct pairs
    // in array whose sum equal to K
    function cntDisPairs(arr , N , K) {

        // Stores count of distinct pairs
        // whose sum equal to K
        var cntPairs = 0;

        // Store frequency of each distinct
        // element of the array
        var cntFre =new  Map();

        for (i = 0; i < N; i++) {

            // Update frequency
            // of arr[i]
            if (cntFre.has(arr[i]))
                cntFre.set(arr[i], cntFre.get(arr[i]) + 1);

            else
                cntFre.set(arr[i], 1);
        }

        // Traverse the map
        for (var it of cntFre) {

            // Stores key value
            // of the map
            var i = it[0];

            // If i is the half of K
            if (2 * i == K) {

                // If frequency of i
                // greater than 1
                if (cntFre[i] > 1)
                    cntPairs += 2;
            }

            else {
                if (cntFre.has(K - i)) {

                    // Update cntPairs
                    cntPairs += 1;
                }
            }
        }

        // Update cntPairs
        cntPairs = cntPairs / 2;
        return cntPairs;
    }

    // Driver Code

        var arr = [ 5, 6, 5, 7, 7, 8 ];
        var N = arr.length;
        var K = 13;
        document.write(cntDisPairs(arr, N, K));

// This code is contributed by umadevi9616
</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)