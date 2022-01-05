# 最高 2 次方不超过非重复数组元素

> 原文:[https://www . geeksforgeeks . org/最高 2 次方不超过非重复数组元素/](https://www.geeksforgeeks.org/highest-powers-of-2-not-exceeding-non-repeating-array-elements/)

给定一个大小为 **N** 的[阵](https://www.geeksforgeeks.org/array-data-structure/)***arr【】***，任务是为每个[非重复阵元](https://www.geeksforgeeks.org/non-repeating-element/)寻找不超过该元的[最高 2 次方。按升序打印 2](https://www.geeksforgeeks.org/highest-power-2-less-equal-given-number/) 的[次幂。如果数组不包含任何](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/)[非重复元素](https://www.geeksforgeeks.org/non-repeating-element/)，则打印*****【0】***。**

****示例:****

> ****输入:** arr[ ] = { 4，5，4，3，3，4 }
> **输出:** 4
> **解释:**数组中唯一的非重复元素是 5。所以 2 不超过 5 的最高幂是 4。**
> 
> ****输入:** arr[ ] = { 1，1，7，6，3 }
> **输出:** 2 4 4**

****天真法:**解决这个问题最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个数组元素，检查它是否不重复。要使元素不重复，请将它们添加到另一个数组中。然后，对于新数组中的每个元素，找到不超过该元素的 2 的最高[次方，并按升序打印。
***时间复杂度:** O(N <sup>2</sup> * log arr[i])，其中 arr[i]为数组最大个数。*
***辅助空间:** O(N)*](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/)**

****高效方法:**最佳思路是使用 [**哈希**](https://www.geeksforgeeks.org/hashing-data-structure/) 。按照以下步骤解决问题:**

*   **[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)***arr【】***并将每个数组元素的[频率存储在](https://www.geeksforgeeks.org/count-frequencies-elements-array-o1-extra-space-time/)[映射](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/)中。**
*   **现在，[遍历地图](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/)检查任一元素的频率是否为 **1** 。**
*   **对于所有这些元素，找到不超过该元素的 2 的最高[次幂，并将其存储在](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/)[向量](http://www.geeksforgeeks.org/vector-in-cpp-stl/)中。**
*   **[按升序排列向量](https://www.geeksforgeeks.org/sorting-a-vector-in-c/)并打印向量中存在的元素。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the highest power of 2 for
// every non-repeating element in the array
void uniqueElement(int arr[], int N)
{

    // Stores the frequency
    // of array elements
    unordered_map<int, int> freq;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Update frequency of each
        // element of the array
        freq[arr[i]]++;
    }

    // Stores the non-repeating
    // array elements
    vector<int> v;

    // Traverse the Map
    for (auto i : freq) {

        if (i.second == 1) {

            // Calculate log base 2
            // of the current element
            int lg = log2(i.first);

            // Highest power of 2 <= i.first
            int p = pow(2, lg);

            // Insert it into the vector
            v.push_back(p);
        }
    }

    // If no element is non-repeating
    if (v.size() == 0) {
        cout << "0";
        return;
    }

    // Sort the powers of 2 obtained
    sort(v.begin(), v.end());

    // Print the elements in the vector
    for (auto i : v)
        cout << i << " ";
}

// Driver Code
int main()
{
    int arr[] = { 4, 5, 4, 3, 3, 4 };

    // Size of array
    int N = sizeof(arr) / sizeof(arr[0]);

    uniqueElement(arr, N);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;
class GFG{

  // Function to find the highest power of 2 for
  // every non-repeating element in the array
  static void uniqueElement(int arr[], int N)
  {

    // Stores the frequency
    // of array elements
    HashMap<Integer, Integer> freq
      = new HashMap<Integer, Integer>();

    for (int i = 0; i < N; i++)
    {
      if (freq.containsKey(arr[i]))
      {
        freq.put(arr[i], freq.get(arr[i]) + 1);
      }
      else
      {
        freq.put(arr[i], 1);
      }
    }

    // Stores the non-repeating
    // array elements
    ArrayList<Integer> v
      = new ArrayList<Integer>();

    // Traverse the Map
    for (Map.Entry i : freq.entrySet()) {

      if ((int)i.getValue() == 1) {

        // Calculate log base 2
        // of the current element
        int lg = (int)(Math.log((int)i.getKey()) / Math.log(2));

        // Highest power of 2 <= i.first
        int p = (int)Math.pow(2, lg);

        // Insert it into the vector
        v.add(p);
      }
    }

    // If no element is non-repeating
    if (v.size() == 0) {
      System.out.print("0");
      return;
    }

    // Sort the powers of 2 obtained
    Collections.sort(v);

    // Print the elements in the vector
    for (int i : v)
      System.out.print( i + " ");
  }

  // Driver Code
  public static void main(String[] args)
  {
    int arr[] = { 4, 5, 4, 3, 3, 4 };

    // Size of array
    int N = arr.length;
    uniqueElement(arr, N);
  }
}

// This code is contributed by code_hunt.
```

## **蟒蛇 3**

```
# Python3 program for the above approach
import math

# Function to find the highest power of 2 for
# every non-repeating element in the array
def uniqueElement(arr, N):

    # Stores the frequency
    # of array elements
    freq = {}

    # Traverse the array
    for i in range(N) :

        # Update frequency
        # of arr[i]
        if arr[i] in freq :
            freq[arr[i]] += 1;
        else :
            freq[arr[i]] = 1;

    # Stores the non-repeating
    # array elements
    v = []

    # Traverse the Map
    for i in freq :
        if (freq[i] == 1) :

            # Calculate log base 2
            # of the current element
            lg = int(math.log2(i))

            # Highest power of 2 <= i.first
            p = pow(2, lg)

            # Insert it into the vector
            v.append(p)

    # If no element is non-repeating
    if (len(v) == 0) :
        print("0")
        return

    # Sort the powers of 2 obtained
    v.sort()

    # Print elements in the vector
    for i in v :
        print(i, end = " ")

# Driver Code
arr = [ 4, 5, 4, 3, 3, 4 ]

# Size of array
N = len(arr)
uniqueElement(arr, N)

# This code is contributed by sanjoy_62.
```

## **C#**

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG{

  // Function to find the highest power of 2 for
  // every non-repeating element in the array
  static void uniqueElement(int []arr, int N)
  {

    // Stores the frequency
    // of array elements
    Dictionary<int, int> freq
      = new Dictionary<int, int>();

    for (int i = 0; i < N; i++)
    {
      if (freq.ContainsKey(arr[i]))
      {
        freq[arr[i]] = freq[arr[i]] + 1;
      }
      else
      {
        freq.Add(arr[i], 1);
      }
    }

    // Stores the non-repeating
    // array elements
    List<int> v
      = new List<int>();

    // Traverse the Map
    foreach(KeyValuePair<int, int> i in freq) {

      if ((int)i.Value == 1) {

        // Calculate log base 2
        // of the current element
        int lg = (int)(Math.Log((int)i.Key) / Math.Log(2));

        // Highest power of 2 <= i.first
        int p = (int)Math.Pow(2, lg);

        // Insert it into the vector
        v.Add(p);
      }
    }

    // If no element is non-repeating
    if (v.Count == 0) {
      Console.Write("0");
      return;
    }

    // Sort the powers of 2 obtained
    v.Sort();

    // Print the elements in the vector
    foreach (int i in v)
      Console.Write( i + " ");
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int []arr = { 4, 5, 4, 3, 3, 4 };

    // Size of array
    int N = arr.Length;
    uniqueElement(arr, N);
  }
}

// This code is contributed by 29AjayKumar
```

## **java 描述语言**

```
<script>
// Javascript program to implement
// the above approach

// Function to find the highest power of 2 for
// every non-repeating element in the array
function uniqueElement(arr, N)
{

    // Stores the frequency
    // of array elements
    var freq = new Map();

    // Traverse the array
    for (var i = 0; i < N; i++) {

        // Update frequency of each
        // element of the array
        if(freq.has(arr[i]))
        {
            freq.set(arr[i], freq.get(arr[i])+1);
        }
        else
        {
            freq.set(arr[i], 1);
        }
    }

    // Stores the non-repeating
    // array elements
    var v = [];

    // Traverse the Map
    freq.forEach((value, key) => {
         if (value== 1) {

            // Calculate log base 2
            // of the current element
            var lg = parseInt(Math.log2(key));

            // Highest power of 2 <= i.first
            var p = Math.pow(2, lg);

            // Insert it into the vector
            v.push(p);
        }
    });

    // If no element is non-repeating
    if (v.length == 0) {
        document.write( "0");
        return;
    }

    // Sort the powers of 2 obtained
    v.sort((a,b) => a-b)

    // Print the elements in the vector
    for(var i =0; i<v.length; i++)
    {
        document.write(v[i] + " ");
    }

}

// Driver Code
var arr = [4, 5, 4, 3, 3, 4 ];
// Size of array
var N = arr.length;
uniqueElement(arr, N);

</script>
```

****Output:** 

```
4
```** 

*****时间复杂度:** O(N * log(MAXM))，其中 MAXM 为* [*最大元素呈现数组*](https://www.geeksforgeeks.org/c-program-find-largest-element-array/) *。*
***辅助空间:** O(N)***