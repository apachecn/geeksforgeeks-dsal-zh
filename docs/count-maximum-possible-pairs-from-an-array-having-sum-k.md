# 从具有和 K 的数组中计数最大可能的对

> 原文:[https://www . geesforgeks . org/count-最大可能对-from-a-array-having-sum-k/](https://www.geeksforgeeks.org/count-maximum-possible-pairs-from-an-array-having-sum-k/)

给定一个由 **N** 个整数和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是从给定的数组中找到最大数量的具有总和 **K** 的对。

注意:每个数组元素都可以是一对数组的一部分。

**示例:**

> **输入:** arr[] = {1，2，3，4}，K = 5
> **输出:** 2
> **说明:**数组中 K 之和为(1，4)和(2，3)的对。
> 
> **输入:** arr[] = {3，1，3，4，3}，K = 6
> **输出:** 1
> **说明:**与数组中的和 K 配对为(3，3)。

**两点法:**思路是使用[两点法](https://www.geeksforgeeks.org/two-pointers-technique/)。按照以下步骤解决问题:

*   将变量**和**初始化为 **0** ，以存储最大对数和 **K** 。
*   [按升序排列数组](https://www.geeksforgeeks.org/arrays-sort-in-java-with-examples/)**【arr】**。
*   将两个索引变量 **L** 初始化为 **0** ，将 **R** 初始化为**(N–1)**，在排序后的数组中查找候选元素。
*   迭代直到 **L 小于 R** 并执行以下操作:
    *   检查**arr【L】****arr【R】**之和是否为 K。如果发现为真，则将 **ans** 和 **L** 增加 **1** ，将 **R** 减少 **1** 。
    *   如果**arr【L】**和**arr【R】**之和小于 **K** ，则以 **1** 递增 **L** 。
    *   否则，将 **R** 减 **1** 。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the maximum number
// of pairs from given array with sum K
void maxPairs(int nums[], int n, int k)
{

  // Sort array in increasing order
  sort(nums, nums + n);

  // Stores the final result
  int result = 0;

  // Initialize the left and right pointers
  int start = 0, end = n - 1;

  // Traverse array until start < end
  while (start < end) {

    if (nums[start] + nums[end] > k)

      // Decrement right by 1
      end--;

    else if (nums[start] + nums[end] < k)

      // Increment left by 1
      start++;

    // Increment result and left
    // pointer by 1 and decrement
    // right pointer by 1
    else
    {
      start++;
      end--;
      result++;
    }
  }

  // Print the result
  cout << result << endl;;
}

// Driver Code
int main()
{
  int arr[] = { 1, 2, 3, 4 };
  int n = sizeof(arr)/sizeof(arr[0]);
  int K = 5;

  // Function Call
  maxPairs(arr, n, K);

  return 0;
}

// This code is contributed by AnkThon
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG {

    // Function to count the maximum number
    // of pairs from given array with sum K
    public static void maxPairs(int[] nums, int k)
    {
        // Sort array in increasing order
        Arrays.sort(nums);

        // Stores the final result
        int result = 0;

        // Initialize the left and right pointers
        int start = 0, end = nums.length - 1;

        // Traverse array until start < end
        while (start < end) {

            if (nums[start] + nums[end] > k)

                // Decrement right by 1
                end--;

            else if (nums[start] + nums[end] < k)

                // Increment left by 1
                start++;

            // Increment result and left
            // pointer by 1 and decrement
            // right pointer by 1
            else {
                start++;
                end--;
                result++;
            }
        }

        // Print the result
        System.out.println(result);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 1, 2, 3, 4 };
        int K = 5;

        // Function Call
        maxPairs(arr, K);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the maximum number
# of pairs from given array with sum K
def maxPairs(nums, k):

    # Sort array in increasing order
    nums = sorted(nums)

    # Stores the final result
    result = 0

    # Initialize the left and right pointers
    start, end = 0, len(nums) - 1

    # Traverse array until start < end
    while (start < end):
        if (nums[start] + nums[end] > k):

            # Decrement right by 1
            end -= 1

        elif (nums[start] + nums[end] < k):

            # Increment left by 1
            start += 1

        # Increment result and left
        # pointer by 1 and decrement
        # right pointer by 1
        else:
            start += 1
            end -= 1
            result += 1

    # Print the result
    print(result)

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 2, 3, 4 ]
    K = 5

    # Function Call
    maxPairs(arr, K)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

    // Function to count the maximum number
    // of pairs from given array with sum K
    public static void maxPairs(int[] nums, int k)
    {

        // Sort array in increasing order
        Array.Sort(nums);

        // Stores the final result
        int result = 0;

        // Initialize the left and right pointers
        int start = 0, end = nums.Length - 1;

        // Traverse array until start < end
        while (start < end) {

            if (nums[start] + nums[end] > k)

                // Decrement right by 1
                end--;

            else if (nums[start] + nums[end] < k)

                // Increment left by 1
                start++;

            // Increment result and left
            // pointer by 1 and decrement
            // right pointer by 1
            else
            {
                start++;
                end--;
                result++;
            }
        }

        // Print the result
        Console.Write(result);
    }

// Driver Code   
public static void Main()
{
  int[] arr = { 1, 2, 3, 4 };
  int K = 5;

  // Function Call
  maxPairs(arr, K);
}
}

// This code is contributed by susmitakundugoaldanga
```

## java 描述语言

```
<script>

    // JavaScript program for above approach

    // Function to count the maximum number
    // of pairs from given array with sum K
    function maxPairs(nums, k)
    {
        // Sort array in increasing order
        nums.sort();

        // Stores the final result
        let result = 0;

        // Initialize the left and right pointers
        let start = 0, end = nums.length - 1;

        // Traverse array until start < end
        while (start < end) {

            if (nums[start] + nums[end] > k)

                // Decrement right by 1
                end--;

            else if (nums[start] + nums[end] < k)

                // Increment left by 1
                start++;

            // Increment result and left
            // pointer by 1 and decrement
            // right pointer by 1
            else {
                start++;
                end--;
                result++;
            }
        }

        // Print the result
        document.write(result);
    }

// Driver Code

           let arr = [ 1, 2, 3, 4 ];
        let K = 5;

        // Function Call
        maxPairs(arr, K);

</script>
```

**输出:**

```
2
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(1)*

**高效方法:**要优化上述方法，思路是使用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)。按照以下步骤解决问题:

*   初始化一个变量，比如说**和**，用总和 **K** 存储最大的对数。
*   初始化一个[哈希表](https://www.geeksforgeeks.org/hashing-set-3-open-addressing/)，比如 **S** ，以[存储**arr【】**中元素](https://www.geeksforgeeks.org/count-frequencies-elements-array-o1-extra-space-time/)的频率。
*   [使用变量遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**，说出 **i** ，并执行以下步骤:
    *   如果**(K-arr[I])**的频率为正，则将 **ans** 增加 **1** ，将**(K-arr[I])**的频率减少 **1** 。
    *   否则，在散列表中插入频率为 **1** 的**arr【I】**。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
#include <string.h>
using namespace std;

// Function to find the maximum number
// of pairs with a sum K such that
// same element can't be used twice
void maxPairs(vector<int> nums, int k)
{

    // Initialize a hashm
    map<int, int> m;

    // Store the final result
    int result = 0;

    // Iterate over the array nums[]
    for(auto i : nums)
    {

        // Decrement its frequency
        // in m and increment
        // the result by 1
        if (m.find(i) != m.end() && m[i] > 0)
        {
            m[i] = m[i] - 1;
            result++;
        }

        // Increment its frequency by 1
        // if it is already present in m.
        // Otherwise, set its frequency to 1
        else
        {
            m[k - i] = m[k - i] + 1;
        }
    }

    // Print the result
    cout << result;
}

// Driver Code
int main()
{
    vector<int> arr = { 1, 2, 3, 4 };
    int K = 5;

    // Function Call
    maxPairs(arr, K);
}

// This code is contributed by grand_master
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG {

    // Function to find the maximum number
    // of pairs with a sum K such that
    // same element can't be used twice
    public static void maxPairs(
        int[] nums, int k)
    {

        // Initialize a hashmap
        Map<Integer, Integer> map
            = new HashMap<>();

        // Store the final result
        int result = 0;

        // Iterate over the array nums[]
        for (int i : nums) {

            // Decrement its frequency
            // in map and increment
            // the result by 1
            if (map.containsKey(i) &&
                map.get(i) > 0)
            {

                map.put(i, map.get(i) - 1);
                result++;
            }

            // Increment its frequency by 1
            // if it is already present in map.
            // Otherwise, set its frequency to 1
            else
            {
                map.put(k - i,
                        map.getOrDefault(k - i, 0) + 1);
            }
        }

        // Print the result
        System.out.println(result);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 1, 2, 3, 4 };
        int K = 5;

        // Function Call
        maxPairs(arr, K);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the maximum number
# of pairs with a sum K such that
# same element can't be used twice
def maxPairs(nums, k) :

    # Initialize a hashm
    m = {}

    # Store the final result
    result = 0

    # Iterate over the array nums[]
    for i in nums :

        # Decrement its frequency
        # in m and increment
        # the result by 1
        if ((i in m) and m[i] > 0) :       
            m[i] = m[i] - 1
            result += 1

        # Increment its frequency by 1
        # if it is already present in m.
        # Otherwise, set its frequency to 1
        else :

            if k - i in m :
                m[k - i] += 1
            else :
                m[k - i] = 1

    # Print the result
    print(result)

# Driver code   
arr = [ 1, 2, 3, 4 ]
K = 5

# Function Call
maxPairs(arr, K)

# This code is contributed by divyesh072019
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

    // Function to find the maximum number
    // of pairs with a sum K such that
    // same element can't be used twice
    public static void maxPairs(
        int[] nums, int k)
    {

        // Initialize a hashmap
        Dictionary<int, int> map
            = new Dictionary<int, int>();

        // Store the readonly result
        int result = 0;

        // Iterate over the array nums[]
        foreach (int i in nums)
        {

            // Decrement its frequency
            // in map and increment
            // the result by 1
            if (map.ContainsKey(i) &&
                map[i] > 0)
            {

                map[i] = map[i] - 1;
                result++;
            }

            // Increment its frequency by 1
            // if it is already present in map.
            // Otherwise, set its frequency to 1
            else
            {
              if (!map.ContainsKey(k - i))
                  map.Add(k - i, 1);
              else
                  map[i] = map[i] + 1;
            }
        }

        // Print the result
        Console.WriteLine(result);
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int[] arr = {1, 2, 3, 4};
        int K = 5;

        // Function Call
        maxPairs(arr, K);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the maximum number
// of pairs with a sum K such that
// same element can't be used twice
function maxPairs(nums, k)
{

    // Initialize a hashm
    var m = new Map();

    // Store the final result
    var result = 0;

    // Iterate over the array nums[]
    nums.forEach(i => {

        // Decrement its frequency
        // in m and increment
        // the result by 1
        if (m.has(i) && m.get(i) > 0)
        {
            m.set(i, m.get(i)-1);
            result++;
        }

        // Increment its frequency by 1
        // if it is already present in m.
        // Otherwise, set its frequency to 1
        else
        {
            if(m.has(k-i))
                m.set(k-i, m.get(k-i)+1)
            else
                m.set(k-i, 1)
        }
    });

    // Print the result
    document.write( result);
}

// Driver Code
var arr = [1, 2, 3, 4];
var K = 5;
// Function Call
maxPairs(arr, K);

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)