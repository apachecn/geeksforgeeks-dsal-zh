# 重新排列数组，使相同索引子集的和不同于原始数组中的和

> 原文:[https://www . geeksforgeeks . org/重新排列数组，使得相同索引子集的和不同于它们在原始数组中的和/](https://www.geeksforgeeks.org/rearrange-an-array-such-that-sum-of-same-indexed-subsets-differ-from-their-sum-in-the-original-array/)

给定一个由 **N** 个不同整数组成的数组 **A[]** ，任务是重新排列给定的数组，使得每个大小小于 **N** 的相同索引非空子集的和不等于它们在原始数组中的和。
**示例:**

> **输入:** A[] = {1000，100，10，1}
> **输出:** 100 10 1 1000
> **解释:**
> 原始数组 A[] = {1000，100，10，1}
> 最终数组 B[] = {100，10，1，1000}
> 大小为 1 的子集:
> 
> ```
> A[0] = 1000  B[0] = 100
> A[1] = 100   B[1] = 10
> A[2] = 10    B[2] = 1
> A[3] = 1     B[3] = 1000
> ```
> 
> 大小为 2 的子集:
> 
> ```
> {A[0], A[1]} = 1100  {B[0], B[1]} = 110
> {A[0], A[2]} = 1010  {B[0], B[2]} = 101
> {A[1], A[2]} = 110   {B[1], B[2]} = 11
> .....
> Similarly, all same-indexed subsets of size 2 have a different sum.
> ```
> 
> 大小为 3 的子集:
> 
> ```
> {A[0], A[1], A[2]} = 1110  {B[0], B[1], B[2]} = 111
> {A[0], A[2], A[3]} = 1011 {B[0], B[2], B[3]} = 1101
> {A[1], A[2], A[3]} = 111  {B[1], B[2], B[3]} = 1011
> ```
> 
> 因此，没有相同索引的子集具有相等的和。
> **输入:** A[] = {1，2，3，4，5}
> **输出:** 5 1 2 3 4

**方法:**
想法是简单地用一个更小的元素替换除一个之外的每个数组元素。按照以下步骤解决问题:

*   将数组元素成对 **{A[i]，i}** 存储。
*   [按数组元素的升序](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)对数组进行排序
*   现在，遍历排序后的顺序，将每个元素插入其下一个较大元素的原始索引处(即索引 **v[(i + 1) % n]处)。第二**)。这确保了除了一个索引之外的每个索引现在都有一个比存储在其中的前一个值更小的元素。

> **证明:**
> 让 S = { arr <sub>1</sub> ，arr <sub>2</sub> ，…，arr <sub>k</sub> }成为子集。
> 如果 **u 最初不属于 S** ，则在将 **u** 插入 S 时，子集的总和发生变化。
> 同样，如果 **u 属于 S，**让 **S'** 包含 **S** 中不存在的所有元素。这意味着 **u 不属于 S'** 。然后，通过上面相同的推理，子集 S’的和不同于它的原始和。

以下是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to rearrange the array such
// that no same-indexed subset have sum
// equal to that in the original array
void printNewArray(vector<int> a, int n)
{
    // Initialize a vector
    vector<pair<int, int> > v;

    // Iterate the array
    for (int i = 0; i < n; i++) {

        v.push_back({ a[i], i });
    }

    // Sort the vector
    sort(v.begin(), v.end());

    int ans[n];

    // Shift of elements to the
    // index of its next cyclic element
    for (int i = 0; i < n; i++) {
        ans[v[(i + 1) % n].second]
            = v[i].first;
    }

    // Print the answer
    for (int i = 0; i < n; i++) {
        cout << ans[i] << " ";
    }
}

// Driver Code
int main()
{
    vector<int> a = { 4, 1, 2, 5, 3 };

    int n = a.size();

    printNewArray(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;
import java.util.*;

class GFG{

static class pair
{
    int first, second;

    pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to rearrange the array such
// that no same-indexed subset have sum
// equal to that in the original array
static void printNewArray(List<Integer> a, int n)
{

    // Initialize a vector
    List<pair> v = new ArrayList<>();

    // Iterate the array
    for(int i = 0; i < n; i++)
    {
        v.add(new pair(a.get(i), i));
    }

    // Sort the vector
    Collections.sort(v, (pair s1, pair s2) ->
    {
        return s1.first - s2.first;
    });

    int ans[] = new int[n];

    // Shift of elements to the
    // index of its next cyclic element
    for(int i = 0; i < n; i++)
    {
        ans[v.get((i + 1) % n).second] = v.get(i).first;
    }

    // Print the answer
    for(int i = 0; i < n; i++)
    {
        System.out.print(ans[i] + " ");
    }
}

// Driver Code
public static void main(String args[])
{
    List<Integer> a = Arrays.asList(4, 1, 2, 5, 3);

    int n = a.size();
    printNewArray(a, n);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 Program to implement
# the above approach

# Function to rearrange the array such
# that no same-indexed subset have sum
# equal to that in the original array
def printNewArray(a, n):

    # Initialize a vector
    v = []

    # Iterate the array
    for i in range (n):
        v.append((a[i], i ))

    # Sort the vector
    v.sort()

    ans = [0] * n

    # Shift of elements to the
    # index of its next cyclic element
    for i in range (n):
        ans[v[(i + 1) % n][1]] = v[i][0]

    # Print the answer
    for i in range (n):
        print (ans[i], end = " ")

# Driver Code
if __name__ == "__main__": 
    a = [4, 1, 2, 5, 3]
    n = len(a)
    printNewArray(a, n)

# This code is contributed by Chitranayal
```

## C#

```
// C# Program to implement
// the above approach
using System;
using System.Collections.Generic;
class GFG
{

    // Function to rearrange the array such
    // that no same-indexed subset have sum
    // equal to that in the original array
    static void printNewArray(List<int> a, int n)
    {

        // Initialize a vector
        List<Tuple<int, int>> v = new List<Tuple<int, int>>();

        // Iterate the array
        for (int i = 0; i < n; i++)
        {

            v.Add(new Tuple<int, int>(a[i],i));
        }

        // Sort the vector
        v.Sort();     
        int[] ans = new int[n];

        // Shift of elements to the
        // index of its next cyclic element
        for (int i = 0; i < n; i++)
        {
            ans[v[(i + 1) % n].Item2]
                = v[i].Item1;
        }

        // Print the answer
        for (int i = 0; i < n; i++)
        {
            Console.Write(ans[i] + " ");
        }
    }

  // Driver code
  static void Main()
  {
    List<int> a = new List<int>(new int[]{4, 1, 2, 5, 3});
    int n = a.Count;
    printNewArray(a, n);
  }
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>

// Javascript Program to implement
// the above approach

// Function to rearrange the array such
// that no same-indexed subset have sum
// equal to that in the original array
function printNewArray(a, n)
{
    // Initialize a vector
    var v = [];

    // Iterate the array
    for (var i = 0; i < n; i++) {

        v.push([ a[i], i]);
    }

    // Sort the vector
    v.sort();

    var ans = Array(n);

    // Shift of elements to the
    // index of its next cyclic element
    for (var i = 0; i < n; i++) {
        ans[v[(i + 1) % n][1]]
            = v[i][0];
    }

    // Print the answer
    for (var i = 0; i < n; i++) {
        document.write( ans[i] + " ");
    }
}

// Driver Code
var a = [4, 1, 2, 5, 3];
var n = a.length;
printNewArray(a, n);

</script>
```

**Output:** 

```
3 5 1 4 2
```

***时间复杂度:** O(N log N)*
***辅助空间:** O(N)*