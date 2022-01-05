# 求前 N 个自然数的第 K 个置换序列

> 原文:[https://www . geeksforgeeks . org/find-the-k-th-排列-第 n 个自然数的序列/](https://www.geeksforgeeks.org/find-the-k-th-permutation-sequence-of-first-n-natural-numbers/)

给定两个**整数 N 和 K** ，在不使用 STL 函数的情况下，求出从 1 到 N 的数的第 K 个置换序列。
*注意:假设输入是这样的，N 个数的第 k 次排列总是可能的。*

**示例:**

> **输入:** N = 3，K = 4
> **输出:** 231
> **说明:**
> 从整数 1 到 3 的排列顺序的顺序列表是:123，132，213，231，312，321。所以，第四个置换序列是“231”。
> 
> **输入:** N = 2，K = 1
> **输出:** 12
> 说明:
> 对于 N = 2，只有 2 种排列可能 12 21。所以，第一个置换序列是“12”。

**天真方法:**
要解决上面提到的问题，简单的方法是找到所有的置换序列，并从中输出第 k 个。但是这种方法效率不高，耗时较长，因此可以优化。

**高效方法:**
要优化上面提到的方法，观察 *k* 的值可以直接用来寻找序列每个索引处的数字。

*   一个 *n* 长度序列的第一个位置被从 1 到 n 的每一个数字所占据**正好是 n！/ n 也就是(n-1)！次数**并按升序排列。因此第 k 个序列的第一个位置**将被索引= k / (n-1)处的数字占据！**(根据基于 1 的索引)。
*   当前找到的数字不能再次出现，因此它从原来的 n 个数字中删除，现在问题简化为找到(k % (n-1)！)剩余 n-1 个数字的第 n 个置换序列。
*   这个过程可以重复，直到我们只剩下一个数字，它将被放在最后一个 1 长度序列的第一个位置。
*   与 k 相比，这里涉及的阶乘值可能非常大。因此，用于避免如此大的阶乘的完整计算的技巧是，一旦**乘积 n * (n-1) * …变得大于 k** ，我们就不再需要找到实际的阶乘值，因为:

> 当部分阶乘值>为 k
> 时，k/n _ 实际阶乘值= 0
> 和 k/n _ 部分阶乘值= 0

下面是上述方法的实现:

## C++

```
// C++ program to Find the kth Permutation
// Sequence of first n natural numbers

#include <bits/stdc++.h>
using namespace std;

// Function to find the index of number
// at first position of
// kth sequence of set of size n
int findFirstNumIndex(int& k, int n)
{

    if (n == 1)
        return 0;
    n--;

    int first_num_index;
    // n_actual_fact = n!
    int n_partial_fact = n;

    while (k >= n_partial_fact
           && n > 1) {
        n_partial_fact
            = n_partial_fact
              * (n - 1);
        n--;
    }

    // First position of the
    // kth sequence will be
    // occupied by the number present
    // at index = k / (n-1)!
    first_num_index = k / n_partial_fact;

    k = k % n_partial_fact;

    return first_num_index;
}

// Function to find the
// kth permutation of n numbers
string findKthPermutation(int n, int k)
{
    // Store final answer
    string ans = "";

    set<int> s;

    // Insert all natural number
    // upto n in set
    for (int i = 1; i <= n; i++)
        s.insert(i);

    set<int>::iterator itr;

    // Mark the first position
    itr = s.begin();

    // subtract 1 to get 0 based indexing
    k = k - 1;

    for (int i = 0; i < n; i++) {

        int index
            = findFirstNumIndex(k, n - i);

        advance(itr, index);

        // itr now points to the
        // number at index in set s
        ans += (to_string(*itr));

        // remove current number from the set
        s.erase(itr);

        itr = s.begin();
    }
    return ans;
}

// Driver code
int main()
{

    int n = 3, k = 4;

    string kth_perm_seq
        = findKthPermutation(n, k);

    cout << kth_perm_seq << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Find
// the kth Permutation
// Sequence of first
// n natural numbers
import java.util.*;
class GFG{

// Function to find the index of
// number at first position of
// kth sequence of set of size n
static int findFirstNumIndex(int k,
                             int n)
{
  if (n == 1)
    return 0;
  n--;

  int first_num_index;

  // n_actual_fact = n!
  int n_partial_fact = n;

  while (k >= n_partial_fact && n > 1)
  {
    n_partial_fact = n_partial_fact *
                     (n - 1);
    n--;
  }

  // First position of the
  // kth sequence will be
  // occupied by the number present
  // at index = k / (n-1)!
  first_num_index = k / n_partial_fact;

  k = k % n_partial_fact;
  return first_num_index;
}

// Function to find the
// kth permutation of n numbers
static String findKthPermutation(int n,
                                 int k)
{
  // Store final answer
  String ans = "";

  HashSet<Integer> s = new HashSet<>();

  // Insert all natural number
  // upto n in set
  for (int i = 1; i <= n; i++)
    s.add(i);

  Vector<Integer> v = new Vector<>();
  v.addAll(s);

  // Mark the first position
  int itr = v.elementAt(0);

  // Subtract 1 to
  // get 0 based
  // indexing
  k = k - 1;

  for (int i = 0; i < n; i++)
  {
    int index = findFirstNumIndex(k,
                                  n - i);

    // itr now points to the
    // number at index in set s
    if(index < v.size())
    {
      ans += ((v.elementAt(index).toString()));
      v.remove(index);
    }
    else
      ans += String.valueOf(itr + 2);

    // Remove current number
    // from the set
    itr = v.elementAt(0);
  }
  return ans;
}

// Driver code
public static void main(String[] args)
{
  int n = 3, k = 4;
  String kth_perm_seq = findKthPermutation(n, k);
  System.out.print(kth_perm_seq + "\n");
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find the kth permutation
# Sequence of first n natural numbers

# Function to find the index of number
# at first position of kth sequence of
# set of size n
def findFirstNumIndex(k, n):

    if (n == 1):
        return 0, k

    n -= 1

    first_num_index = 0

    # n_actual_fact = n!
    n_partial_fact = n

    while (k >= n_partial_fact and n > 1):
        n_partial_fact = n_partial_fact * (n - 1)
        n -= 1

    # First position of the kth sequence
    # will be occupied by the number present
    # at index = k / (n-1)!
    first_num_index = k // n_partial_fact

    k = k % n_partial_fact

    return first_num_index, k

# Function to find the
# kth permutation of n numbers
def findKthPermutation(n, k):

    # Store final answer
    ans = ""

    s = set()

    # Insert all natural number
    # upto n in set
    for i in range(1, n + 1):
        s.add(i)

    # Subtract 1 to get 0 based indexing
    k = k - 1

    for i in range(n):

        # Mark the first position
        itr = list(s)

        index, k = findFirstNumIndex(k, n - i)

        # itr now points to the
        # number at index in set s
        ans += str(itr[index])

        # remove current number from the set
        itr.pop(index)

        s = set(itr)

    return ans

# Driver code
if __name__=='__main__':

    n = 3
    k = 4

    kth_perm_seq = findKthPermutation(n, k)

    print(kth_perm_seq)

# This code is contributed by rutvik_56
```

## C#

```
// C# program to Find
// the kth Permutation
// Sequence of first
// n natural numbers
using System;
using System.Collections.Generic;
class GFG{

// Function to find the index of
// number at first position of
// kth sequence of set of size n
static int findFirstNumIndex(int k,
                             int n)
{
  if (n == 1)
    return 0;
  n--;

  int first_num_index;

  // n_actual_fact = n!
  int n_partial_fact = n;

  while (k >= n_partial_fact && n > 1)
  {
    n_partial_fact = n_partial_fact *
                     (n - 1);
    n--;
  }

  // First position of the
  // kth sequence will be
  // occupied by the number present
  // at index = k / (n-1)!
  first_num_index = k / n_partial_fact;

  k = k % n_partial_fact;
  return first_num_index;
}

// Function to find the
// kth permutation of n numbers
static String findKthPermutation(int n,
                                 int k)
{
  // Store readonly answer
  String ans = "";

  HashSet<int> s = new HashSet<int>();

  // Insert all natural number
  // upto n in set
  for (int i = 1; i <= n; i++)
    s.Add(i);

  List<int> v = new List<int>(s);

  // Mark the first position
  int itr = v[0];

  // Subtract 1 to
  // get 0 based
  // indexing
  k = k - 1;

  for (int i = 0; i < n; i++)
  {
    int index = findFirstNumIndex(k, n - i);

    // itr now points to the
    // number at index in set s
    if(index < v.Count)
    {
      ans += ((v[index].ToString()));
      v.RemoveAt(index);
    }
    else
      ans += String.Join("", itr + 2);

    // Remove current number
    // from the set
    itr = v[0];
  }
  return ans;
}

// Driver code
public static void Main(String[] args)
{
  int n = 3, k = 4;
  String kth_perm_seq = findKthPermutation(n, k);
  Console.Write(kth_perm_seq + "\n");
}
}

// This code is contributed by Rajput-Ji
```

**Output:** 

```
231
```