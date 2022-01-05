# 重新排列数组中的数字，使相邻的数字不相同

> 原文:[https://www . geeksforgeeks . org/array-numbers-in-a-so-no-two-neighborgeks-numbers-相同/](https://www.geeksforgeeks.org/rearrange-numbers-in-an-array-such-that-no-two-adjacent-numbers-are-same/)

给定一个整数数组。任务是重新排列数组的元素，使数组中没有两个相邻的元素相同。

**示例:**

```
Input: arr[] = {1, 1, 1, 2, 2, 2}
Output: {2, 1, 2, 1, 2, 1}

Input: arr[] = {1, 1, 1, 1, 2, 2, 3, 3}
Output: {1, 3, 1, 3, 2, 1, 2, 1}
```

这个想法是把最高频率的元素放在第一位(贪婪的方法)。我们使用一个优先级队列(或二进制最大堆)并把所有元素按它们的频率排序(最高频率元素在根)。然后，我们一个接一个地从堆中取出频率最高的元素，并将其添加到结果中。在我们添加之后，我们降低元素的频率，并将这个元素暂时移出优先级队列，这样下次就不会拾取它了。

我们必须按照步骤来解决这个问题，它们是:

1.  建立一个存储元素及其频率的优先级队列或最大堆。
    …… Priority_queue 或 max_heap 是基于元素的频率构建的。
2.  创建一个临时键，用作先前访问过的元素(结果数组中的前一个元素。初始化它{ num = -1，freq = -1 }
3.  而 pq 不为空。
    *   弹出一个元素并将其添加到结果中。
    *   将弹出元素的频率减少“1”。
    *   如果频率> 0，则将前一个元素推回到 priority_queue。
    *   将当前元素作为下一次迭代的前一个元素。
4.  如果结果字符串和原始字符串的长度不相等，则打印“不可能”。否则打印结果。

下面是上述方法的实现:

## C++14

```
// C++14 program to rearrange numbers in
// an Array such that no two numbers are
// adjacent
#include <bits/stdc++.h>
using namespace std;

// Function to rearrange numbers in array such
// that no two adjacent numbers are same
void rearrangeArray(int arr[], int N)
{

    // Store frequencies of all elements
    // of the array
    map<int, int>mp, visited;

    for(int i = 0; i < N; i++)
    {
        mp[arr[i]]++;
    }

    priority_queue<pair<int, int>>pq;

    // Adding high freq elements
    // in descending order
    for(int i = 0; i < N ; i++)
    {
        int val = arr[i];

        if (mp[val] > 0 and visited[val] != 1)
        {
            pq.push({mp[val], val});
        }
        visited[val] = 1;
    }

    // 'result[]' that will store resultant value
    vector<int>result(N);

    // Work as the previous visited element
    // initial previous element will be ( '-1' and
    // it's frequency wiint also be '-1' )
    pair<int, int>prev = { -1, -1 };
    int l = 0;

    // Traverse queue
    while (pq.size() != 0)
    {

        // Pop top element from queue and add it
        // to result
        pair<int,int>k = pq.top();
        pq.pop();
        result[l] = k.second;

        // If frequency of previous element is less
        // than zero that means it is useless, we
        // need not to push it
        if (prev.first > 0)
        {
            pq.push(prev);
        }

        // Make current element as the previous
        // decrease frequency by 'one'
        k.first--;
        prev = k;
        l++;
    }

    for(auto it : result)
    {
        if (it == 0)
        {

            // If found 0, No valid result
            // array possible
            cout << "Not valid Array" << endl;
            return;
        }
    }

    for(auto it : result)
    {
        cout << it << ", ";
    }
}

// Driver Code
int main()
{
    int A[] = { 1, 1, 1, 1, 2, 2, 3, 3 };

    // Size of the array
    int N = sizeof(A) / sizeof(A[0]);

    rearrangeArray(A, N);
}

// This code is contributed by koulick_sadhu
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to rearrange numbers in an Array
// such that no two numbers are adjacent

import java.util.Comparator;
import java.util.PriorityQueue;

// Comparator class to sort in descending order
class KeyComparator implements Comparator<Key>
{

    // Overriding compare()method of Comparator
    public int compare(Key k1, Key k2)
    {
        if (k1.freq < k2.freq)
            return 1;
        else if (k1.freq > k2.freq)
            return -1;
        return 0;
    }
}

// Object of num and its freq
class Key
{
    int freq; // store frequency of character
    int num;
    Key(int freq, int num)
    {
        this.freq = freq;
        this.num = num;
    }
}

public class GFG
{

    // Function to rearrange numbers in array such
    // that no two adjacent numbers are same
    static void rearrangeArray(int[] arr)
    {
        int n = arr.length;

        // Store frequencies of all elements
        // of the array
        int[] count = new int[10000];
        int visited[] = new int[10000];

        for (int i = 0; i < n; i++)
            count[arr[i]]++;

        // Insert all characters with their frequencies
        // into a priority_queue
        PriorityQueue<Key> pq
            = new PriorityQueue<>(new KeyComparator());

        // Adding high freq elements in descending order
        for (int i = 0; i < n; i++)
        {
            int val = arr[i];

            if (count[val] > 0 && visited[val] != 1)
                pq.add(new Key(count[val], val));
            visited[val] = 1;
        }

        // 'result[]' that will store resultant value
        int result[] = new int[n];

        // work as the previous visited element
        // initial previous element will be ( '-1' and
        // it's frequency will also be '-1' )
        Key prev = new Key(-1, -1);

        // Traverse queue
        int l = 0;
        while (pq.size() != 0)
        {
            // pop top element from queue and add it
            // to result
            Key k = pq.peek();
            pq.poll();
            result[l] = k.num;

            // If frequency of previous element is less
            // than zero that means it is useless, we
            // need not to push it
            if (prev.freq > 0)
                pq.add(prev);

            // make current element as the previous
            // decrease frequency by 'one'
            (k.freq)--;
            prev = k;
            l++;
        }

        // If length of the resultant array and original
        // array is not same then the array is not valid
        if (l != result.length)
        {
            System.out.println(" Not valid Array ");
        }
        // Otherwise Print the result array
        else
        {
            for (int i : result)
            {
                System.out.print(i + " ");
            }
        }
    }

    // Driver Code
    public static void main(String args[])
    {
        int arr[] = new int[] { 1, 1, 1, 1, 2, 2, 3, 3 };

        rearrangeArray(arr);
    }
}
```

## 蟒蛇 3

```
# Python3 program to rearrange numbers in
# an Array such that no two numbers are
# adjacent

# Function to rearrange numbers in array such
# that no two adjacent numbers are same
def rearrangeArray(arr, N) :

    # Store frequencies of all elements
    # of the array
    mp = {}
    visited = {}    
    for i in range(N) :
        if(arr[i] in mp) :
            mp[arr[i]] += 1
        else :
            mp[arr[i]] = 1

    pq = []

    # Adding high freq elements
    # in descending order
    for i in range(N) :
        val = arr[i]
        if((val in mp) and ((val not in visited) or (visited[val] != 1))) :
            pq.append([mp[val], val])
        visited[val] = 1   
    pq.sort()
    pq.reverse()

    # 'result[]' that will store resultant value
    result = [0]*N

    # Work as the previous visited element
    # initial previous element will be ( '-1' and
    # it's frequency wiint also be '-1' )
    prev = [-1, -1]
    l = 0

    # Traverse queue
    while (len(pq) != 0) :

        # Pop top element from queue and add it
        # to result
        k = pq[0]
        pq.pop(0)
        result[l] = k[1]

        # If frequency of previous element is less
        # than zero that means it is useless, we
        # need not to push it
        if (prev[0] > 0) :

            pq.append(prev)
            pq.sort()
            pq.reverse()

        # Make current element as the previous
        # decrease frequency by 'one'
        prev = [k[0] - 1, k[1]]
        l += 1

    for it in result :
        if (it == 0) :

            # If found 0, No valid result
            # array possible
            print("Not valid Array")
            return   
    for it in result :
        print(it , end = " ")

A = [ 1, 1, 1, 1, 2, 2, 3, 3 ]

# Size of the array
N = len(A)
rearrangeArray(A, N)

#This code is contributed by divyesh072019.
```

## C#

```
// C# program to rearrange numbers in
// an Array such that no two numbers are
// adjacent
using System;
using System.Collections.Generic;
class GFG{

    // Function to rearrange numbers in array such
    // that no two adjacent numbers are same
    static void rearrangeArray(int[] arr, int N)
    {

        // Store frequencies of all elements
        // of the array
        Dictionary<int, int> mp = new Dictionary<int, int>();
        Dictionary<int, int> visited = new Dictionary<int, int>();

        for(int i = 0; i < N; i++)
        {
            if(mp.ContainsKey(arr[i]))
            {
                mp[arr[i]] += 1;
            }
            else{
                mp[arr[i]] = 1;
            }
        }

        List<Tuple<int, int>> pq = new List<Tuple<int,int>>();

        // Adding high freq elements
        // in descending order
        for(int i = 0; i < N ; i++)
        {
            int val = arr[i];

            if (mp.ContainsKey(val) && (!visited.ContainsKey(val) || visited[val] != 1))
            {
                pq.Add(new Tuple<int,int>(mp[val], val));
            }
            visited[val] = 1;
        }

        pq.Sort();
        pq.Reverse();

        // 'result[]' that will store resultant value
        int[] result = new int[N];

        // Work as the previous visited element
        // initial previous element will be ( '-1' and
        // it's frequency wiint also be '-1' )
        Tuple<int, int> prev = new Tuple<int,int>( -1, -1 );
        int l = 0;

        // Traverse queue
        while (pq.Count != 0)
        {

            // Pop top element from queue and add it
            // to result
            Tuple<int,int> k = pq[0];
            pq.RemoveAt(0);
            result[l] = k.Item2;

            // If frequency of previous element is less
            // than zero that means it is useless, we
            // need not to push it
            if (prev.Item1 > 0)
            {
                pq.Add(prev);
                pq.Sort();
                pq.Reverse();
            }

            // Make current element as the previous
            // decrease frequency by 'one'
            prev = new Tuple<int,int>(k.Item1 - 1, k.Item2);
            l++;
        }
        foreach(int it in result)
        {
            if (it == 0)
            {

                // If found 0, No valid result
                // array possible
                Console.WriteLine("Not valid Array");
                return;
            }
        }
        foreach(int it in result)
        {
            Console.Write(it + " ");
        }
    }

  // Driver code
  static void Main()
  {
    int[] A = { 1, 1, 1, 1, 2, 2, 3, 3 };

    // Size of the array
    int N = A.Length;
    rearrangeArray(A, N);
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>

// Javascript program to rearrange numbers in
// an Array such that no two numbers are
// adjacent

// Function to rearrange numbers in array such
// that no two adjacent numbers are same
function rearrangeArray(arr, N)
{

    // Store frequencies of all elements
    // of the array
    var mp = new Map();
    var visited = new Map();

    for(var i = 0; i < N; i++)
    {
        if(mp.has(arr[i]))
          mp.set(arr[i], mp.get(arr[i])+1)
        else
          mp.set(arr[i], 1)
    }

    var pq = [];

    // Adding high freq elements
    // in descending order
    for(var i = 0; i < N ; i++)
    {
        var val = arr[i];

        if (mp.get(val) > 0 && visited[val] != 1)
        {
            pq.push([mp.get(val), val]);
        }
        visited[val] = 1;
    }
    pq.sort();
    // 'result[]' that will store resultant value
    var result = Array(N).fill(0);

    // Work as the previous visited element
    // initial previous element will be ( '-1' and
    // it's frequency wiint also be '-1' )
    var prev = [-1, -1];
    var l = 0;

    // Traverse queue
    while (pq.length != 0)
    {

        // Pop top element from queue and add it
        // to result
        var k = pq[pq.length-1];
        pq.pop();
        result[l] = k[1];

        // If frequency of previous element is less
        // than zero that means it is useless, we
        // need not to push it
        if (prev[0] > 0)
        {
            pq.push(prev);
        }
        pq.sort();
        // Make current element as the previous
        // decrease frequency by 'one'
        k[0]--;
        prev = k;
        l++;
    }

    for(var it of result)
    {
        if (it == 0)
        {

            // If found 0, No valid result
            // array possible
            document.write("Not valid Array" + "<br>");
            return;
        }
    }

    for(var it of result)
    {
        document.write(it + " ");
    }
}

// Driver Code
var A = [1, 1, 1, 1, 2, 2, 3, 3];

// Size of the array
var N = A.length;

rearrangeArray(A, N);

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
1 3 1 2 1 3 2 1
```

**时间复杂度:**O(N * logN)
T3】辅助空间: O(N)