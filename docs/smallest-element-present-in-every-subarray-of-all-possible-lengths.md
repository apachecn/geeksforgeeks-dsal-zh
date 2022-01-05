# 存在于所有可能长度的每个子阵列中的最小元素

> 原文:[https://www . geeksforgeeks . org/所有可能长度的每个子阵列中存在的最小元素/](https://www.geeksforgeeks.org/smallest-element-present-in-every-subarray-of-all-possible-lengths/)

给定一个长度为 **N** 的[阵列](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，子阵列每一个可能长度的任务是找到该长度的每个子阵列中存在的最小元素。

**示例:**

> **输入:** N = 10，arr[] = {2，3，5，3，2，3，1，3，2，7}
> **输出:**-1-1 3 2 2 1 1 1 1
> **解释:**
> 对于长度= 1，长度为 1 的每个子阵列中没有共同的元素。因此，输出为-1。
> 对于长度= 2，在长度为 2 的每个子阵列中没有共同的元素。因此，输出为-1。
> 对于长度= 3，每个子阵列中的公共元素为 3。因此，输出为 3。
> 对于长度= 4，2 和 3 在长度为 4 的每个子阵列中都是常见的。2 是较小的，是所需的输出。
> 同样，对于长度 5 和 6，这些长度的每个子阵列中最小的公共元素是 2。
> 对于长度 7、8、9 和 10，这些长度的每个子阵列中最小的公共元素是 1。
> 
> **输入:** N = 3，arr[] = {2，2，2 }
> T3】输出: 2 2 2

**天真法:**思路是针对 **K** ( 1 ≤ K ≤ N)的每个可能值，在所有大小为 **K** 的子阵中找到公共元素，打印出最小的公共元素。按照以下步骤解决问题:

1.  将长度为 **K** 的每个子阵列的每个唯一数字的计数相加。
2.  检查计数是否等于子阵列的数量，即**N–K–1**。
3.  如果发现是真的，那么该特定元素出现在大小为 **K** 的每个子阵列中。
4.  对于多个这样的元素，打印其中最小的元素。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to add count of numbers
// in the map for a subarray of length k
void uniqueElements(int arr[], int start, int K,
                    map<int, int>& mp)
{
    // Set to store unique elements
    set<int> st;

    // Add elements to the set
    for (int i = 0; i < K; i++)
        st.insert(arr[start + i]);

    // Iterator of the set
    set<int>::iterator itr = st.begin();

    // Adding count in map
    for (; itr != st.end(); itr++)
        mp[*itr]++;
}

// Function to check if there is any number
// which repeats itself in every subarray
// of length K
void checkAnswer(map<int, int>& mp, int N, int K)
{
    // Check all number starting from 1
    for (int i = 1; i <= N; i++) {

        // Check if i occurred n-k+1 times
        if (mp[i] == (N - K + 1)) {

            // Print the smallest number
            cout << i << " ";
            return;
        }
    }

    // Print -1, if no such number found
    cout << -1 << " ";
}

// Function to count frequency of each
// number in each subarray of length K
void smallestPresentNumber(int arr[], int N, int K)
{
    map<int, int> mp;

    // Traverse all subarrays of length K
    for (int i = 0; i <= N - K; i++) {
        uniqueElements(arr, i, K, mp);
    }

    // Check and print the smallest number
    // present in every subarray and print it
    checkAnswer(mp, N, K);
}

// Function to generate the value of K
void generateK(int arr[], int N)
{
    for (int k = 1; k <= N; k++)

        // Function call
        smallestPresentNumber(arr, N, k);
}

// Driver Code
int main()
{

    // Given array
    int arr[] = { 2, 3, 5, 3, 2, 3, 1, 3, 2, 7 };

    // Size of array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call
    generateK(arr, N);

    return (0);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import java.lang.*;

class GFG
{

  // Function to add count of numbers
  // in the map for a subarray of length k
  static void uniqueElements(int arr[], int start, int K,
                             Map<Integer,Integer> mp)
  {
    // Set to store unique elements
    Set<Integer> st=new HashSet<>();

    // Add elements to the set
    for (int i = 0; i < K; i++)
      st.add(arr[start + i]);

    // Iterator of the set
    Iterator itr = st.iterator();

    // Adding count in map
    while(itr.hasNext())
    {
      Integer t = (Integer)itr.next();
      mp.put(t,mp.getOrDefault(t, 0) + 1);
    }

  }

  // Function to check if there is any number
  // which repeats itself in every subarray
  // of length K
  static void checkAnswer(Map<Integer,Integer> mp, int N, int K)
  {

    // Check all number starting from 1
    for (int i = 1; i <= N; i++)
    {

      // Check if i occurred n-k+1 times
      if(mp.containsKey(i))   
        if (mp.get(i) == (N - K + 1))
        {

          // Print the smallest number
          System.out.print(i + " ");
          return;
        }
    }

    // Print -1, if no such number found
    System.out.print(-1 + " ");
  }

  // Function to count frequency of each
  // number in each subarray of length K
  static void smallestPresentNumber(int arr[], int N, int K)
  {
    Map<Integer, Integer> mp = new HashMap<>();

    // Traverse all subarrays of length K
    for (int i = 0; i <= N - K; i++)
    {
      uniqueElements(arr, i, K, mp);
    }

    // Check and print the smallest number
    // present in every subarray and print it
    checkAnswer(mp, N, K);
  }

  // Function to generate the value of K
  static void generateK(int arr[], int N)
  {
    for (int k = 1; k <= N; k++)

      // Function call
      smallestPresentNumber(arr, N, k);
  }

  // Driver code
  public static void main (String[] args)
  {
    // Given array
    int arr[] = { 2, 3, 5, 3, 2, 3, 1, 3, 2, 7 };

    // Size of array
    int N = arr.length;

    // Function call
    generateK(arr, N);

  }
}

// This code is contributed by offbeat.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to add count of numbers
# in the map for a subarray of length k
def uniqueElements(arr, start, K, mp) :

    # Set to store unique elements
    st = set();

    # Add elements to the set
    for i in range(K) :
        st.add(arr[start + i]);

    # Adding count in map
    for itr in st:
        if itr in mp :
            mp[itr] += 1;
        else:
            mp[itr] = 1;

# Function to check if there is any number
# which repeats itself in every subarray
# of length K
def checkAnswer(mp, N, K) :

    # Check all number starting from 1
    for i in range(1, N + 1) :

        if i in mp :

            # Check if i occurred n-k+1 times
            if (mp[i] == (N - K + 1)) :

                # Print the smallest number
                print(i, end = " ");
                return;

    # Print -1, if no such number found
    print(-1, end = " ");

# Function to count frequency of each
# number in each subarray of length K
def smallestPresentNumber(arr, N,  K) :
    mp = {};

    # Traverse all subarrays of length K
    for i in range(N - K + 1) :
        uniqueElements(arr, i, K, mp);

    # Check and print the smallest number
    # present in every subarray and print it
    checkAnswer(mp, N, K);

# Function to generate the value of K
def generateK(arr, N) :

    for k in range(1, N + 1) :

        # Function call
        smallestPresentNumber(arr, N, k);

# Driver Code
if __name__ == "__main__" :

    # Given array
    arr = [ 2, 3, 5, 3, 2, 3, 1, 3, 2, 7 ];

    # Size of array
    N = len(arr);

    # Function call
    generateK(arr, N);

    # This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

  // Function to add count of numbers
  // in the map for a subarray of length k
  static void uniqueElements(int[] arr, int start,
                             int K, Dictionary<int, int> mp)
  {

    // Set to store unique elements
    HashSet<int> st = new HashSet<int>();

    // Add elements to the set
    for (int i = 0; i < K; i++)
      st.Add(arr[start + i]);

    // Adding count in map
    foreach(int itr in st)
    {
      if(mp.ContainsKey(itr))
      {
        mp[itr]++;
      }
      else{
        mp[itr] = 1;
      }
    }
  }

  // Function to check if there is any number
  // which repeats itself in every subarray
  // of length K
  static void checkAnswer(Dictionary<int, int> mp, int N, int K)
  {

    // Check all number starting from 1
    for (int i = 1; i <= N; i++)
    {

      // Check if i occurred n-k+1 times
      if(mp.ContainsKey(i))   
        if (mp[i] == (N - K + 1))
        {

          // Print the smallest number
          Console.Write(i + " ");
          return;
        }
    }

    // Print -1, if no such number found
    Console.Write(-1 + " ");
  }

  // Function to count frequency of each
  // number in each subarray of length K
  static void smallestPresentNumber(int[] arr, int N, int K)
  {
    Dictionary<int, int> mp = new Dictionary<int, int>();

    // Traverse all subarrays of length K
    for (int i = 0; i <= N - K; i++)
    {
      uniqueElements(arr, i, K, mp);
    }

    // Check and print the smallest number
    // present in every subarray and print it
    checkAnswer(mp, N, K);
  }

  // Function to generate the value of K
  static void generateK(int[] arr, int N)
  {
    for (int k = 1; k <= N; k++)

      // Function call
      smallestPresentNumber(arr, N, k);
  }

  // Driver code
  static void Main()
  {

    // Given array
    int[] arr = { 2, 3, 5, 3, 2, 3, 1, 3, 2, 7 };

    // Size of array
    int N = arr.Length;

    // Function call
    generateK(arr, N);
  }
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

  // Function to add count of numbers
  // in the map for a subarray of length k
  function uniqueElements(arr, start, K, mp)
  {

    // Set to store unique elements
    let st = new Set();

    // add elements to the set
    for (let i = 0; i < K; i++)
      st.add(arr[start + i]);

    // adding count in map
    for(let itr of st)
    {
      if(mp.has(itr))
      {
        mp.set(itr, mp.get(itr) + 1);
      }
      else{
        mp.set(itr, 1);
      }
    }
  }

  // Function to check if there is any number
  // which repeats itself in every subarray
  // of length K
  function checkAnswer(mp, N, K)
  {

    // Check all number starting from 1
    for (let i = 1; i <= N; i++)
    {

      // Check if i occurred n-k+1 times
      if(mp.has(i))   
        if (mp.get(i) == (N - K + 1))
        {

          // Print the smallest number
          document.write(i + " ");
          return;
        }
    }

    // Print -1, if no such number found
    document.write(-1 + " ");
  }

  // Function to count frequency of each
  // number in each subarray of length K
  function smallestPresentNumber(arr, N, K)
  {
    let mp = new Map();

    // Traverse all subarrays of length K
    for (let i = 0; i <= N - K; i++)
    {
      uniqueElements(arr, i, K, mp);
    }

    // Check and print the smallest number
    // present in every subarray and print it
    checkAnswer(mp, N, K);
  }

  // Function to generate the value of K
  function generateK(arr, N)
  {
    for (let k = 1; k <= N; k++)

      // Function call
      smallestPresentNumber(arr, N, k);
  }

  // Driver code

    // Given array
    let arr = [ 2, 3, 5, 3, 2, 3, 1, 3, 2, 7 ];

    // Size of array
    let N = arr.length;

    // Function call
    generateK(arr, N);

// This code is contributed by gfgking
</script>
```

**Output:** 

```
-1 -1 3 2 2 2 1 1 1 1
```

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(N)*

**有效方法:**如果使用一个数组存储数组中存在特定数字的所有索引，并找到最小长度，使其出现在每个长度子数组中 **1 ≤ K ≤ N** ，则可以优化上述方法。

按照以下步骤解决问题:

1.  初始化一个数组，比如说**索引[]** ，以存储与该索引号对应的特定数字所在的索引。
2.  现在，对于给定数组中的每个数字，求最小长度，使它出现在该长度的每个子数组中。
3.  最小长度可以通过找到给定数组中特定数字重复的最大间隔来找到。同样，对于数组的其他数字也要找到相同的值。
4.  用 **-1** 初始化大小为 **N+1** 的**答案[]** 数组，其中**答案【I】**代表长度为 **K** 的子数组的答案。
5.  现在，**索引【】**数组给出了每个长度子数组中存在的数字，比如说 **K** ，然后如果**答案【K】**是 **-1** ，则用相同的数字更新**答案【K】**。
6.  遍历之后，更新**答案【】**数组，这样如果一个数字出现在所有长度为 **K** 的子数组中，那么这个特定的数字也会出现在所有长度大于 **K** 的子数组中。
7.  更新**答案[]** 数组后，打印该数组中存在的所有元素，作为每个长度子数组 **K** 的答案。

下面是上述方法的实现:

## C++

```
// C++ program of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to print the common
// elements for all subarray lengths
void printAnswer(int answer[], int N)
{
    for (int i = 1; i <= N; i++) {
        cout << answer[i] << " ";
    }
}

// Function to find and store the
// minimum element present in all
// subarrays of all lengths from 1 to n
void updateAnswerArray(int answer[], int N)
{
    int i = 0;

    // Skip lengths for which
    // answer[i] is -1
    while (answer[i] == -1)
        i++;

    // Initialize minimum as the first
    // element where answer[i] is not -1
    int minimum = answer[i];

    // Updating the answer array
    while (i <= N) {

        // If answer[i] is -1, then minimum
        // can be substituted in that place
        if (answer[i] == -1)
            answer[i] = minimum;

        // Find minimum answer
        else
            answer[i] = min(minimum, answer[i]);
        minimum = min(minimum, answer[i]);
        i++;
    }
}

// Function to find the minimum number
// corresponding to every subarray of
// length K, for every K from 1 to N
void lengthOfSubarray(vector<int> indices[],
                      set<int> st, int N)
{
    // Stores the minimum common
    // elements for all subarray lengths
    int answer[N + 1];

    // Initialize with -1.
    memset(answer, -1, sizeof(answer));

    // Find for every element, the minimum length
    // such that the number is present in every
    // subsequence of that particular length or more
    for (auto itr : st) {

        // To store first occurence and
        // gaps between occurences
        int start = -1;
        int gap = -1;

        // To cover the distance between last
        // occurence and the end of the array
        indices[itr].push_back(N);

        // To find the distance
        // between any two occurences
        for (int i = 0; i < indices[itr].size(); i++) {
            gap = max(gap, indices[itr][i] - start);
            start = indices[itr][i];
        }
        if (answer[gap] == -1)
            answer[gap] = itr;
    }

    // Update and store the answer
    updateAnswerArray(answer, N);

    // Print the required answer
    printAnswer(answer, N);
}

// Function to find the smallest
// element common in all subarrays for
// every possible subarray lengths
void smallestPresentNumber(int arr[], int N)
{
    // Initializing indices array
    vector<int> indices[N + 1];

    // Store the numbers present
    // in the array
    set<int> elements;

    // Push the index in the indices[A[i]] and
    // also store the numbers in set to get
    // the numbers present in input array
    for (int i = 0; i < N; i++) {
        indices[arr[i]].push_back(i);
        elements.insert(arr[i]);
    }

    // Function call to calculate length of
    // subarray for which a number is present
    // in every subarray of that length
    lengthOfSubarray(indices, elements, N);
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 2, 3, 5, 3, 2, 3, 1, 3, 2, 7 };

    // Size of array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    smallestPresentNumber(arr, N);

    return (0);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.util.*;
import java.lang.*;

class GFG
{

  // Function to print the common
  // elements for all subarray lengths
  static void printAnswer(int answer[], int N)
  {
    for (int i = 1; i <= N; i++)
    {
      System.out.print(answer[i]+" ");
    }
  }

  // Function to find and store the
  // minimum element present in all
  // subarrays of all lengths from 1 to n
  static void updateAnswerArray(int answer[], int N)
  {
    int i = 0;

    // Skip lengths for which
    // answer[i] is -1
    while (answer[i] == -1)
      i++;

    // Initialize minimum as the first
    // element where answer[i] is not -1
    int minimum = answer[i];

    // Updating the answer array
    while (i <= N) {

      // If answer[i] is -1, then minimum
      // can be substituted in that place
      if (answer[i] == -1)
        answer[i] = minimum;

      // Find minimum answer
      else
        answer[i] = Math.min(minimum, answer[i]);
      minimum = Math.min(minimum, answer[i]);
      i++;
    }
  }

  // Function to find the minimum number
  // corresponding to every subarray of
  // length K, for every K from 1 to N
  static void lengthOfSubarray(ArrayList<ArrayList<Integer>> indices,
                               Set<Integer> st, int N)
  {
    // Stores the minimum common
    // elements for all subarray lengths
    int[] answer = new int[N + 1];

    // Initialize with -1.
    Arrays.fill(answer, -1);

    // Find for every element, the minimum length
    // such that the number is present in every
    // subsequence of that particular length or more
    Iterator itr = st.iterator();
    while (itr.hasNext())
    {

      // To store first occurence and
      // gaps between occurences
      int start = -1;
      int gap = -1;
      int t = (int)itr.next();

      // To cover the distance between last
      // occurence and the end of the array
      indices.get(t).add(N);

      // To find the distance
      // between any two occurences
      for (int i = 0; i < indices.get(t).size(); i++)
      {
        gap = Math.max(gap, indices.get(t).get(i) - start);
        start = indices.get(t).get(i);
      }
      if (answer[gap] == -1)
        answer[gap] = t;
    }

    // Update and store the answer
    updateAnswerArray(answer, N);

    // Print the required answer
    printAnswer(answer, N);
  }

  // Function to find the smallest
  // element common in all subarrays for
  // every possible subarray lengths
  static void smallestPresentNumber(int arr[], int N)
  {
    // Initializing indices array
    ArrayList<ArrayList<Integer>> indices = new ArrayList<>();

    for(int i = 0; i <= N; i++)
      indices.add(new ArrayList<Integer>());

    // Store the numbers present
    // in the array
    Set<Integer> elements = new HashSet<>();

    // Push the index in the indices[A[i]] and
    // also store the numbers in set to get
    // the numbers present in input array
    for (int i = 0; i < N; i++)
    {
      indices.get(arr[i]).add(i);
      elements.add(arr[i]);
    }

    // Function call to calculate length of
    // subarray for which a number is present
    // in every subarray of that length
    lengthOfSubarray(indices, elements, N);
  }

  // Driver function
  public static void main (String[] args)
  {

    // Given array
    int arr[] = { 2, 3, 5, 3, 2, 3, 1, 3, 2, 7 };

    // Size of array
    int N = arr.length;

    // Function Call
    smallestPresentNumber(arr, N);
  }
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python program of the above approach

# Function to print the common
# elements for all subarray lengths
def printAnswer(answer, N):
    for i in range(N + 1):
        print(answer[i], end = " ")

# Function to find and store the
# minimum element present in all
# subarrays of all lengths from 1 to n
def updateAnswerArray(answer, N):
    i = 0

    # Skip lengths for which
    # answer[i] is -1
    while(answer[i] == -1):
        i += 1

    # Initialize minimum as the first
    # element where answer[i] is not -1
    minimum = answer[i]

    # Updating the answer array
    while(i <= N):

        # If answer[i] is -1, then minimum
        # can be substituted in that place
        if(answer[i] == -1):
            answer[i] = minimum

        # Find minimum answer
        else:
            answer[i] = min(minimum, answer[i])
        minimum = min(minimum, answer[i])
        i += 1

# Function to find the minimum number
# corresponding to every subarray of
# length K, for every K from 1 to N
def lengthOfSubarray(indices, st, N):

    # Stores the minimum common
    # elements for all subarray lengths
    #Initialize with -1.
    answer = [-1 for i in range(N + 1)]

    # Find for every element, the minimum length
    # such that the number is present in every
    # subsequence of that particular length or more
    for itr in st:

        # To store first occurence and
        # gaps between occurences
        start = -1
        gap = -1

        # To cover the distance between last
        # occurence and the end of the array
        indices[itr].append(N)

        # To find the distance
        # between any two occurences
        for i in range(len(indices[itr])):
            gap = max(gap, indices[itr][i] - start)
            start = indices[itr][i]

        if(answer[gap] == -1):
            answer[gap] = itr

    # Update and store the answer
    updateAnswerArray(answer, N)

    # Print the required answer
    printAnswer(answer, N)

# Function to find the smallest
# element common in all subarrays for
# every possible subarray lengths
def smallestPresentNumber(arr, N):

    # Initializing indices array
    indices = [[] for i in range(N + 1)]

    # Store the numbers present
    # in the array
    elements = []

    # Push the index in the indices[A[i]] and
    # also store the numbers in set to get
    # the numbers present in input array
    for i in range(N):
        indices[arr[i]].append(i)
        elements.append(arr[i])

    elements = list(set(elements))

    # Function call to calculate length of
    # subarray for which a number is present
    # in every subarray of that length
    lengthOfSubarray(indices, elements, N)

# Driver Code

# Given array
arr = [2, 3, 5, 3, 2, 3, 1, 3, 2, 7]

# Size of array
N = len(arr)

# Function Call
smallestPresentNumber(arr, N)

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program for above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to print the common
// elements for all subarray lengths
static void printAnswer(int[] answer, int N)
{
    for(int i = 1; i <= N; i++)
    {
        Console.Write(answer[i] + " ");
    }
}

// Function to find and store the
// minimum element present in all
// subarrays of all lengths from 1 to n
static void updateAnswerArray(int[] answer, int N)
{
    int i = 0;

    // Skip lengths for which
    // answer[i] is -1
    while (answer[i] == -1)
        i++;

    // Initialize minimum as the first
    // element where answer[i] is not -1
    int minimum = answer[i];

    // Updating the answer array
    while (i <= N)
    {

        // If answer[i] is -1, then minimum
        // can be substituted in that place
        if (answer[i] == -1)
            answer[i] = minimum;

        // Find minimum answer
        else
            answer[i] = Math.Min(minimum, answer[i]);
            minimum = Math.Min(minimum, answer[i]);
            i++;
    }
}

// Function to find the minimum number
// corresponding to every subarray of
// length K, for every K from 1 to N
static void lengthOfSubarray(List<List<int>> indices,
                               HashSet<int> st, int N)
{
    // Stores the minimum common
    // elements for all subarray lengths
    int[] answer = new int[N + 1];

    // Initialize with -1.
    Array.Fill(answer, -1);

    // Find for every element, the minimum length
    // such that the number is present in every
    // subsequence of that particular length or more
    foreach(int itr in st)
    {

        // To store first occurence and
        // gaps between occurences
        int start = -1;
        int gap = -1;
        int t = itr;

        // To cover the distance between last
        // occurence and the end of the array
        indices[t].Add(N);

        // To find the distance
        // between any two occurences
        for(int i = 0; i < indices[t].Count; i++)
        {
            gap = Math.Max(gap, indices[t][i] - start);
            start = indices[t][i];
        }
        if (answer[gap] == -1)
            answer[gap] = t;
    }

    // Update and store the answer
    updateAnswerArray(answer, N);

    // Print the required answer
    printAnswer(answer, N);
}

// Function to find the smallest
// element common in all subarrays for
// every possible subarray lengths
static void smallestPresentNumber(int[] arr, int N)
{

    // Initializing indices array
    List<List<int>> indices = new List<List<int>>();

    for(int i = 0; i <= N; i++)
        indices.Add(new List<int>());

    // Store the numbers present
    // in the array
    HashSet<int> elements = new HashSet<int>();

    // Push the index in the indices[A[i]] and
    // also store the numbers in set to get
    // the numbers present in input array
    for(int i = 0; i < N; i++)
    {
        indices[arr[i]].Add(i);
        elements.Add(arr[i]);
    }

    // Function call to calculate length of
    // subarray for which a number is present
    // in every subarray of that length
    lengthOfSubarray(indices, elements, N);
}

// Driver code
static void Main()
{

    // Given array
    int[] arr = { 2, 3, 5, 3, 2, 3, 1, 3, 2, 7 };

    // Size of array
    int N = arr.Length;

    // Function Call
    smallestPresentNumber(arr, N);
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

// Javascript program of the above approach

// Function to print the common
// elements for all subarray lengths
function printAnswer(answer, N)
{
    for(let i = 1; i <= N; i++)
    {
        document.write(answer[i] + " ");
    }
}

// Function to find and store the
// minimum element present in all
// subarrays of all lengths from 1 to n
function updateAnswerArray(answer, N)
{
    let i = 0;

    // Skip lengths for which
    // answer[i] is -1
    while (answer[i] == -1)
        i++;

    // Initialize minimum as the first
    // element where answer[i] is not -1
    let minimum = answer[i];

    // Updating the answer array
    while (i <= N)
    {

        // If answer[i] is -1, then minimum
        // can be substituted in that place
        if (answer[i] == -1)
            answer[i] = minimum;

        // Find minimum answer
        else
            answer[i] = Math.min(minimum, answer[i]);

        minimum = Math.min(minimum, answer[i]);
        i++;
    }
}

// Function to find the minimum number
// corresponding to every subarray of
// length K, for every K from 1 to N
function lengthOfSubarray(indices, st, N)
{

    // Stores the minimum common
    // elements for all subarray lengths
    let answer = new Array(N + 1).fill(-1);

    // Find for every element, the minimum length
    // such that the number is present in every
    // subsequence of that particular length or more
    for(let itr of st)
    {

        // To store first occurence and
        // gaps between occurences
        let start = -1;
        let gap = -1;

        // To cover the distance between last
        // occurence and the end of the array
        indices[itr].push(N);

        // To find the distance
        // between any two occurences
        for(let i = 0; i < indices[itr].length; i++)
        {
            gap = Math.max(
                gap, indices[itr][i] - start);
            start = indices[itr][i];
        }
        if (answer[gap] == -1)
            answer[gap] = itr;
    }

    // Update and store the answer
    updateAnswerArray(answer, N);

    // Print the required answer
    printAnswer(answer, N);
}

// Function to find the smallest
// element common in all subarrays for
// every possible subarray lengths
function smallestPresentNumber(arr, N)
{

    // Initializing indices array
    let indices = new Array(N + 1).fill(0).map(() => []);

    // Store the numbers present
    // in the array
    let elements = new Set();

    // Push the index in the indices[A[i]] and
    // also store the numbers in set to get
    // the numbers present in input array
    for(let i = 0; i < N; i++)
    {
        indices[arr[i]].push(i);
        elements.add(arr[i]);
    }

    // Function call to calculate length of
    // subarray for which a number is present
    // in every subarray of that length
    lengthOfSubarray(indices, elements, N);
}

// Driver Code

// Given array
let arr = [ 2, 3, 5, 3, 2,
            3, 1, 3, 2, 7 ];

// Size of array
let N = arr.length;

// Function Call
smallestPresentNumber(arr, N);

// This code is contributed by gfgking

</script>
```

**Output:** 

```
-1 -1 3 2 2 2 1 1 1 1
```

***时间复杂度:** O(NlogN)*
***辅助空间:** O(N)*