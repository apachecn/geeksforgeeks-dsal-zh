# 精确 K 次移除最频繁出现的数组元素

> 原文:[https://www . geeksforgeeks . org/remove-出现次数最多的数组元素-精确到 k 次/](https://www.geeksforgeeks.org/remove-an-occurrence-of-most-frequent-array-element-exactly-k-times/)

给定一个[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是移除最频繁出现的数组元素恰好 **K** 次。如果多个数组元素具有最大频率，则移除其中最小的一个。打印 **K** 删除的元素。

**示例:**

> **输入** : arr[] = {1，3，2，1，4，1}，K = 2
> **输出:** 1 1
> **说明:**
> 1 的频率为 3，2，3，4 的频率为 1:
> **操作 1:** 从数组中移除 1。目前，1 的频率是 2，2，3，4 的频率是 1。
> 操作 2:从阵列中移除 1。
> 
> **输入:** arr[] = {10，10，10，20，30，20，20}，K = 2
> **输出:** 10 20

**简单方法:**最简单的方法是[按照升序对数组进行排序](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)和[使用](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)计算数组元素的频率。对于 **K** 操作，打印最频繁的元素，并将其频率降低 **1** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to print the most frequent
// array element exactly K times
void maxFreqElements(int arr[],
                     int N, int K)
{
    // Stores frequency array element
    map<int, int> mp;

    for (int i = 0; i < N; i++) {

        // Count frequency
        // of array element
        mp[arr[i]]++;
    }

    while (K > 0) {

        // Maximum array element
        int max = 0;
        int element;

        // Traverse the Map
        for (auto i : mp) {

            // Find the element with
            // maximum frequency
            if (i.second > max) {
                max = i.second;

                // If the frequency is maximum,
                // store that number in element
                element = i.first;
            }
        }

        // Print element as it contains the
        // element having highest frequency
        cout << element << " ";

        // Decrease the frequency
        // of the maximum array element
        mp[element]--;

        // Reduce the number of operations
        K--;
    }
}

// Driver Code
int main()
{

    // Given array
    int arr[] = { 1, 3, 2, 1, 4, 1 };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Given K
    int K = 2;

    maxFreqElements(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG
{

// Function to print the most frequent
// array element exactly K times
static void maxFreqElements(int arr[],
                     int N, int K)
{

    // Stores frequency array element
    HashMap<Integer,
          Integer> mp = new HashMap<Integer,
                                    Integer>();

    for (int i = 0; i < N; i++)
    {

        // Count frequency
        // of array element
        if(mp.containsKey(arr[i]))
            {
                mp.put(arr[i], mp.get(arr[i]) + 1);
            }
            else
            {
                mp.put(arr[i], 1);
            }
    }

    while (K > 0)
    {

        // Maximum array element
        int max = 0;
        int element = 0;

        // Traverse the Map
        for (Map.Entry<Integer,
                 Integer> i : mp.entrySet())
        {

            // Find the element with
            // maximum frequency
            if (i.getValue() > max)
            {
                max = i.getValue();

                // If the frequency is maximum,
                // store that number in element
                element = i.getKey();
            }
        }

        // Print element as it contains the
        // element having highest frequency
        System.out.print(element + " ");

        // Decrease the frequency
        // of the maximum array element
        if(mp.containsKey(element))
            {
                mp.put(element, mp.get(element) + 1);
            }
            else
            {
                mp.put(element, 1);
            }

        // Reduce the number of operations
        K--;
    }
}

// Driver code
public static void main(String[] args)
{
    // Given array
    int[] arr = { 1, 3, 2, 1, 4, 1 };

    // Size of the array
    int N = arr.length;

    // Given K
    int K = 2;  
    maxFreqElements(arr, N, K);
}
}

// This code is contributed by susmitakundugoaldanga
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to print the most frequent
# array element exactly K times
def maxFreqElements(arr, N, K) :

    # Stores frequency array element
    mp = {}

    for i in range(N) :

        # Count frequency
        # of array element
        if arr[i] in mp :
            mp[arr[i]] += 1
        else :
            mp[arr[i]] = 1

    while (K > 0) :

        # Maximum array element
        Max = 0

        # Traverse the Map
        for i in mp :

            # Find the element with
            # maximum frequency
            if (mp[i] > Max) :
                Max = mp[i]

                # If the frequency is maximum,
                # store that number in element
                element = i

        # Print element as it contains the
        # element having highest frequency
        print(element, end = " ")

        # Decrease the frequency
        # of the maximum array element
        if element in mp :
            mp[element] -= 1
        else :
            mp[element] = -1

        # Reduce the number of operations
        K -= 1

# Given array
arr = [ 1, 3, 2, 1, 4, 1 ]

# Size of the array
N = len(arr) 

# Given K
K = 2

maxFreqElements(arr, N, K)

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic; 

class GFG{

// Function to print the most frequent
// array element exactly K times
static void maxFreqElements(int[] arr,
                            int N, int K)
{

    // Stores frequency array element
    Dictionary<int,
               int> mp = new Dictionary<int,
                                        int>(); 

    for(int i = 0; i < N; i++)
    {

        // Count frequency
        // of array element
        if (mp.ContainsKey(arr[i]))
        {
            mp[arr[i]]++;
        }
        else
        {
            mp[arr[i]] = 1;
        }
    }

    while (K > 0)
    {

        // Maximum array element
        int max = 0;
        int element = 0;

        // Traverse the Map
        foreach(KeyValuePair<int, int> i in mp)
        {

            // Find the element with
            // maximum frequency
            if (i.Value > max)
            {
                max = i.Value;

                // If the frequency is maximum,
                // store that number in element
                element = i.Key;
            }
        }

        // Print element as it contains the
        // element having highest frequency
        Console.Write(element + " ");

        // Decrease the frequency
        // of the maximum array element
        if (mp.ContainsKey(element))
        {
            mp[element]--;
        }
        else
        {
            mp[element] = -1;
        }

        // Reduce the number of operations
        K--;
    }
}

// Driver Code
static void Main()
{

    // Given array
    int[] arr = { 1, 3, 2, 1, 4, 1 };

    // Size of the array
    int N = arr.Length;

    // Given K
    int K = 2;

    maxFreqElements(arr, N, K);
}
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>

      // JavaScript program for the above approach

      // Function to print the most frequent
      // array element exactly K times
      function maxFreqElements(arr, N, K) {
        // Stores frequency array element
        var mp = {};

        for (var i = 0; i < N; i++) {
          // Count frequency
          // of array element
          if (mp.hasOwnProperty(arr[i])) {
            mp[arr[i]]++;
          } else {
            mp[arr[i]] = 1;
          }
        }

        while (K > 0) {
          // Maximum array element
          var max = 0;
          var element = 0;

          // Traverse the Map
          for (const [key, value] of Object.entries(mp)) {
            // Find the element with
            // maximum frequency
            if (value > max) {
              max = value;

              // If the frequency is maximum,
              // store that number in element
              element = key;
            }
          }

          // Print element as it contains the
          // element having highest frequency
          document.write(element + " ");

          // Decrease the frequency
          // of the maximum array element
          if (mp.hasOwnProperty(element)) {
            mp[element]--;
          } else {
            mp[element] = -1;
          }

          // Reduce the number of operations
          K--;
        }
      }

      // Driver Code
      // Given array
      var arr = [1, 3, 2, 1, 4, 1];

      // Size of the array
      var N = arr.length;

      // Given K
      var K = 2;

      maxFreqElements(arr, N, K);
</script>
```

**Output:** 

```
1 1
```

***时间复杂度:** O(N * K)*
***辅助空间:** O(N)*

**有效方法:**想法是将元素数组连同它们的计数一起存储在一个[对向量](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)中，然后[使用比较器](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-2-sort-in-descending-order-by-first-and-second/)按升序对对向量进行排序。完成后，打印该对向量中的第一个 **K** 元素。

按照以下步骤解决问题:

*   初始化一个[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)来存储数组元素的频率。初始化一对向量来存储**{元素，频率}。**
*   [按照第二个值的降序对向量对进行排序。](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-2-sort-in-descending-order-by-first-and-second/)
*   然后，打印第一个 **K** 对的数组元素作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to sort the vector
// of vector of pair
bool cmp(pair<int, int> p1, pair<int, int> p2)
{
    // Check if frequency of p1 is
    // greater than frequency of p2
    if (p1.second > p2.second)
        return true;

    // If frequency of p1 and p2 is same
    else if (p1.second == p2.second) {

        // Check for the smallest element
        if (p1.first < p2.first)
            return true;
    }
    return false;
}

// Function to print the K most frequent
// elements after each removal
void maxFreqElements(int arr[], int N, int K)
{
    // Stores frequency of array elements
    map<int, int> mp;

    // Pairs array element with frequency
    vector<pair<int, int> > v;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Count the frequencies
        mp[arr[i]]++;

        // Insert the element with its
        // current frequency into the vector
        v.push_back({ arr[i], mp[arr[i]] });
    }

    // Sort the vector according to
    // higher frequency and smaller
    // element if frequency is same
    sort(v.begin(), v.end(), cmp);

    // Print the first K elements
    // of the array
    for (int i = 0; i < K; i++)
        cout << v[i].first << " ";
}

// Driver Code
int main()
{

    // Given array
    int arr[] = { 1, 3, 2, 1, 4, 1 };

    // Given K
    int K = 2;

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    maxFreqElements(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.util.*;
import java.lang.*;

class pair{
    int first,second;

    pair(int first, int second){
        this.first=first;
        this.second=second;
    }
}
class GFG{

// Function to print the K most frequent
// elements after each removal
static void maxFreqElements(int arr[], int N, int K)
{
    // Stores frequency of array elements
    Map<Integer, Integer> mp=new HashMap<>();

    // Pairs array element with frequency
    ArrayList<pair> v=new ArrayList<>();

    // Traverse the array
    for (int i = 0; i < N; i++)
    {

        // Count the frequencies
        mp.put(arr[i],mp.getOrDefault(arr[i],0)+1);

        // Insert the element with its
        // current frequency into the vector
        v.add(new pair( arr[i], mp.get(arr[i] )));
    }

    // Sort the vector according to
    // higher frequency and smaller
    // element if frequency is same
   Collections.sort(v,(a,b)->(a.second != b.second) ?
                    b.second-a.second:a.first-b.first);

    // Print the first K elements
    // of the array
    for (int i = 0; i < K; i++)
        System.out.print(v.get(i).first + " ");
}

   // Driver function
    public static void main (String[] args)
    {

    // Given array
    int arr[] = { 1, 3, 2, 1, 4, 1 };

    // Given K
    int K = 2;

    // Size of the array
    int N = arr.length;

    maxFreqElements(arr, N, K);

    }
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to sort the vector
# of vector of pair

# Function to print the K most frequent
# elements after each removal
def maxFreqElements(arr, N, K):

    # Stores frequency of array elements
    mp = {}

    # Pairs array element with frequency
    v = []

    # Traverse the array
    for i in range(N):
        # Count the frequencies
        mp[arr[i]] = mp.get(arr[i],0)+1

        # Insert the element with its
        # current frequency into the vector
        v.append([arr[i], mp.get(arr[i],0)])

    # Sort the vector according to
    # higher frequency and smaller
    c = [1, 1]

    # element if frequency is same
    v.sort(reverse = True)

    # Print the first K elements
    # of the array  
    for i in range(K):
        print(c[i], end = " ")

# Driver Code
if __name__ == '__main__':

    # Given array
    arr = [1, 3, 2, 1, 4, 1]

    # Given K
    K = 2

    # Size of the array
    N = len(arr)

    maxFreqElements(arr, N, K)

    # This code is contributed by SURANDRA_GANGWAR.
```

## C#

```
// C# program for above approach
using System;
using System.Collections.Generic;

public class pair
{
  public int first, second;

  public pair(int first, int second)
  {
    this.first = first;
    this.second = second;
  }
}

public class GFG{

  static int Compare(KeyValuePair<int, int> a, KeyValuePair<int, int> b)
  {
    if(a.Value != b.Value)
    {
      return b.Value - a.Value;
    }
    else
    {
      return a.Key - b.Key;
    }
  }

  // Function to print the K most frequent
  // elements after each removal
  static void maxFreqElements(int[] arr, int N, int K)
  {

    // Stores frequency of array elements
    Dictionary<int,int> mp = new Dictionary<int,int>();

    // Pairs array element with frequency
    List<KeyValuePair<int,int>> v = new List<KeyValuePair<int,int>>();

    // Traverse the array
    for (int i = 0; i < N; i++)
    {

      // Count the frequencies
      if(!mp.ContainsKey(arr[i]))
      {
        mp.Add(arr[i], 1);
      }
      else
      {
        mp[arr[i]]++;
      }

      // Insert the element with its
      // current frequency into the vector
      v.Add(new KeyValuePair<int,int>( arr[i], mp[arr[i] ]));
    }
    v.Sort(Compare);

    // Print the first K elements
    // of the array
    for (int i = 0; i < K; i++)
    {
      Console.Write(v[i].Key + " ");
    }
  }

  // Driver function
  static public void Main ()
  {

    // Given array
    int[] arr = { 1, 3, 2, 1, 4, 1 };

    // Given K
    int K = 2;

    // Size of the array
    int N = arr.Length;

    maxFreqElements(arr, N, K);
  }
}

// This code is contributed by rag2127.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to print the K most frequent
// elements after each removal
function maxFreqElements(arr, N, K)
{
    // Stores frequency of array elements
    var mp = new Map();

    // Pairs array element with frequency
    var v = [];

    // Traverse the array
    for (var i = 0; i < N; i++) {

        // Count the frequencies
        if(mp.has(arr[i]))
            mp.set(arr[i], mp.get(arr[i])+1)
        else
            mp.set(arr[i], 1)

        // Insert the element with its
        // current frequency into the vector
        v.push([arr[i], mp.get(arr[i])]);
    }

    // Sort the vector according to
    // higher frequency and smaller
    // element if frequency is same
    v.sort();

    // Print the first K elements
    // of the array
    for (var i = 0; i < K; i++)
        document.write( v[i][0] + " ");
}

// Driver Code
// Given array
var arr = [1, 3, 2, 1, 4, 1];
// Given K
var K = 2;
// Size of the array
var N = arr.length
maxFreqElements(arr, N, K);

</script>
```

**Output:** 

```
1 1
```

***时间复杂度:** O(NlogN)*
***辅助空间:** O(N)*