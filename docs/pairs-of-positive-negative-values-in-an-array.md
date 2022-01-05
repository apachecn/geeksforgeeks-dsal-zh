# 数组中的正负对

> 原文:[https://www . geesforgeks . org/数组中的正负值对/](https://www.geeksforgeeks.org/pairs-of-positive-negative-values-in-an-array/)

给定一个由**个不同的**个整数组成的数组，打印该数组中所有具有正负值的数字对。我们需要按出现的顺序打印配对。任何元素首先出现的对应该首先打印。

**示例:**

```
Input  :  arr[] = { 1, -3, 2, 3, 6, -1 }
Output : -1 1 -3 3

Input  :  arr[] = { 4, 8, 9, -4, 1, -1, -8, -9 }
Output : -1 1 -4 4 -8 8 -9 9
```

**方法 1(简单:O(n<sup>2</sup>)**
思路是用两个嵌套循环。对于每个元素 arr[i]，从索引 i + 1 到 n–1 找到 arr[i]的负数，并将其存储在另一个数组中。对于输出，对存储的元素进行排序，并打印存储元素的负正值。

下面是该方法的实现:

## C++

```
// Simple CPP program to find pairs of positive
// and negative values present in an array.
#include <bits/stdc++.h>
using namespace std;

// Print pair with negative and positive value
void printPairs(int arr[], int n)
{
    vector<int> v;

    // For each element of array.
    for (int i = 0; i < n; i++)

        // Try to find the negative value of
        // arr[i] from i + 1 to n
        for (int j = i + 1; j < n; j++)

            // If absolute values are equal print pair.
            if (abs(arr[i]) == abs(arr[j]))
                v.push_back(abs(arr[i]));     

    // If size of vector is 0, therefore there is no
    // element with positive negative value, print "0"
    if (v.size() == 0)
       return;

    // Sort the vector
    sort(v.begin(), v.end());

    // Print the pair with negative positive value.
    for (int i = 0; i < v.size(); i++)
        cout << -v[i] << " " << v[i];   
}

// Driven Program
int main()
{
    int arr[] = { 4, 8, 9, -4, 1, -1, -8, -9 };
    int n = sizeof(arr) / sizeof(arr[0]);
    printPairs(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find pairs of positive
// and negative values present in an array.
import java.util.*;
import java.lang.*;

class GFG {

    // Print pair with negative and positive value
    public static void printPairs(int arr[] , int n)
    {
        Vector<Integer> v = new Vector<Integer>();
        // For each element of array.
        for (int i = 0; i < n; i++)

            // Try to find the negative value of
            // arr[i] from i + 1 to n
            for (int j = i + 1; j < n; j++)

                // If absolute values are equal
                // print pair.
                if (Math.abs(arr[i]) ==
                                  Math.abs(arr[j]))
                    v.add(Math.abs(arr[i]));

        // If size of vector is 0, therefore there
        // is no element with positive negative
        // value, print "0"
        if (v.size() == 0)
            return;    

        // Sort the vector
        Collections.sort(v);

        // Print the pair with negative positive
        // value.
        for (int i = 0; i < v.size(); i++)
            System.out.print(-v.get(i) + " " +
                                      v.get(i));
    }

    // Driven Program
    public static void main(String[] args)
    {
        int arr[] = { 4, 8, 9, -4, 1, -1, -8, -9 };
        int n = arr.length;
        printPairs(arr, n);
    }
}

// This code is contributed by Prasad Kshirsagar.
```

## 蟒蛇 3

```
# Simple Python 3 program to find
# pairs of positive and negative
# values present in an array.

# Print pair with negative and
# positive value
def printPairs(arr, n):
    v = []

    # For each element of array.
    for i in range(n):

        # Try to find the negative value
        # of arr[i] from i + 1 to n
        for j in range( i + 1,n) :

            # If absolute values are
            # equal print pair.
            if (abs(arr[i]) == abs(arr[j])) :
                v.append(abs(arr[i]))

    # If size of vector is 0, therefore
    # there is no element with positive
    # negative value, print "0"
    if (len(v) == 0):
        return;

    # Sort the vector
    v.sort()

    # Print the pair with negative
    # positive value.
    for i in range(len( v)):
        print(-v[i], "" , v[i], end = " ")

# Driver Code
if __name__ == "__main__":
    arr = [ 4, 8, 9, -4, 1, -1, -8, -9 ]
    n = len(arr)
    printPairs(arr, n)

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to find pairs of positive
// and negative values present in an array.
using System;
using System.Collections.Generic;

class GFG
{

    // Print pair with negative and positive value
    public static void printPairs(int []arr , int n)
    {
        List<int> v = new List<int>();

        // For each element of array.
        for (int i = 0; i < n; i++)

            // Try to find the negative value of
            // arr[i] from i + 1 to n
            for (int j = i + 1; j < n; j++)

                // If absolute values are equal
                // print pair.
                if (Math.Abs(arr[i]) ==
                                Math.Abs(arr[j]))
                    v.Add(Math.Abs(arr[i]));

        // If size of vector is 0, therefore there
        // is no element with positive negative
        // value, print "0"
        if (v.Count == 0)
            return;    

        // Sort the vector
        v.Sort();

        // Print the pair with negative positive
        // value.
        for (int i = 0; i < v.Count; i++)
            Console.Write(-v[i] + " " +
                                    v[i]);
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []arr = { 4, 8, 9, -4, 1, -1, -8, -9 };
        int n = arr.Length;
        printPairs(arr, n);
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program to find pairs of positive
// and negative values present in an array.

    // Print pair with negative and positive value
    function printPairs(arr,n)
    {
        let  v = [];

        // For each element of array.
        for (let i = 0; i < n; i++)

            // Try to find the negative value of
            // arr[i] from i + 1 to n
            for (let j = i + 1; j < n; j++)

                // If absolute values are equal
                // print pair.
                if (Math.abs(arr[i]) ==
                                  Math.abs(arr[j]))
                    v.push(Math.abs(arr[i]));

        // If size of vector is 0, therefore there
        // is no element with positive negative
        // value, print "0"
        if (v.length == 0)
            return;   

        // Sort the vector
        v.sort(function(a, b){return a-b;});

        // Print the pair with negative positive
        // value.
        for (let i = 0; i < v.length; i++)
            document.write(-v[i] + " " +
                                      v[i]);
    }

    // Driven Program
    let arr=[4, 8, 9, -4, 1, -1, -8, -9];
    let n = arr.length;
    printPairs(arr, n);

    // This code is contributed by rag2127
</script>
```

**Output:** 

```
-1 1-4 4-8 8-9 9
```

**方法 2 (Hashing)**
思路是用 Hashing。遍历给定的数组，增加哈希表绝对值的计数。如果计数变为 2，将其绝对值存储在另一个向量中。最后对向量进行排序。如果向量的大小为 0，则打印“0”，否则对于向量中的每个项，首先打印其负值和正值。

下面是该方法的实现:

## C++

```
// Efficient CPP program to find pairs of
// positive and negative values present in
// an array.
#include <bits/stdc++.h>
using namespace std;

// Print pair with negative and positive value
void printPairs(int arr[], int n)
{
    vector<int> v;
    unordered_map<int, bool> cnt;

    // For each element of array.
    for (int i = 0; i < n; i++) {

        // If element has not encounter early,
        // mark it on cnt array.
        if (cnt[abs(arr[i])] == 0)
            cnt[abs(arr[i])] = 1;

        // If seen before, push it in vector (
        // given that elements are distinct)
        else {
            v.push_back(abs(arr[i]));
            cnt[abs(arr[i])] = 0;
        }
    }

    if (v.size() == 0)
        return;

    sort(v.begin(), v.end());
    for (int i = 0; i < v.size(); i++)
        cout << -v[i] << " " << v[i] << " ";
}

// Driven Program
int main()
{
    int arr[] = { 4, 8, 9, -4, 1, -1, -8, -9 };
    int n = sizeof(arr) / sizeof(arr[0]);
    printPairs(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Efficient Java program to find pairs of
// positive and negative values present in
// an array.
import java.util.*;

class GFG
{

// Print pair with negative
// and positive value
static void printPairs(int arr[], int n)
{
    ArrayList<Integer> v = new ArrayList<Integer> ();
    HashMap<Integer,
            Integer> cnt = new HashMap<Integer,
                                       Integer>();

    // For each element of array.
    for (int i = 0; i < n; i++)
    {

        // If element has  encounter early,
        // then increment its count
        if (cnt.containsKey(Math.abs(arr[i])))
            cnt.put(Math.abs(arr[i]) , cnt.get(Math.abs(arr[i])) + 1);

        // If element has not seen before,
          // then initialize its count to 1
        else
        {

            cnt.put(Math.abs(arr[i]), 1);
        }
        if( cnt.get(Math.abs(arr[i])) == 2 ){
          v.add(Math.abs(arr[i]));
        }
    }

    if (v.size() == 0)
        return;

    Collections.sort(v);
    for (int i = 0; i < v.size(); i++)
        System.out.print("-" + v.get(i) +
                         " " + v.get(i) + " ");
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 4, 8, 9, -4, 1, -1, -8, -9 };
    int n = arr.length;
    printPairs(arr, n);
}
}

// This code is contributed by Prerna Saini
```

## 蟒蛇 3

```
# Efficient Python3 program to find pairs of 
# positive and negative values present in
# an array. 

# Print pair with negative and
# positive value
def printPairs(arr, n):

    s = set()
    ret = []

    # For each element of array.
    for i in arr:
        if abs(i) in s:
            ret.append(abs(i))
        else:
            s.add(abs(i))

    ret.sort()

    for i in range(0, len(ret)):
        print(-ret[i], "", ret[i], end = " ")

# Driver Code
if __name__ == "__main__":

    arr = [ 4, 8, 9, -4, 1, -1, -8, -9 ]
    n = len(arr)

    printPairs(arr, n)

# This code is contributed by RohitOberoi
```

## C#

```
// Efficient C# program to find pairs of
// positive and negative values present in
// an array.
using System;
using System.Collections.Generic;
class GFG
{

    // Print pair with negative and positive value
    static void printPairs(int[] arr, int n)
    {
        List<int> v = new List<int>();
        Dictionary<int, bool> cnt = new Dictionary<int, bool>();

        // For each element of array.
        for (int i = 0; i < n; i++)
        {

            // If element has not encounter early,
            // mark it on cnt array.
            if(!cnt.ContainsKey(Math.Abs(arr[i])))
            {
                cnt[Math.Abs(arr[i])] = true;
            }
            else if(cnt[Math.Abs(arr[i])] == false)
            {
                cnt[Math.Abs(arr[i])] = true;
            }
            else
            {
                v.Add(Math.Abs(arr[i]));
                cnt[Math.Abs(arr[i])] = false;
            }
        }

        if (v.Count == 0)
            return;

        v.Sort();
        for (int i = 0; i < v.Count; i++)
            Console.Write(-v[i] + " " + v[i] + " ");
    }

  // Driver code
  static void Main()
  {
    int[] arr = { 4, 8, 9, -4, 1, -1, -8, -9 };
    int n = arr.Length;
    printPairs(arr, n);
  }
}

// This code is contributed by divyeshrabadiya07
```

**Output:** 

```
-1 1 -4 4 -8 8 -9 9
```

本文由 **Anuj Chauhan** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。