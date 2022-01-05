# 检查是否可以通过合并 2 个非空排列形成一个数组

> 原文:[https://www . geesforgeks . org/check-if-a-array-can-formed-by-merging-2-non-empty-arranges/](https://www.geeksforgeeks.org/check-if-an-array-can-be-formed-by-merging-2-non-empty-permutations/)

给定一个长度为 **N** 的数组 **arr[]** ，任务是检查它是否可以通过合并两个相同或不同长度的[排列](https://www.geeksforgeeks.org/check-if-an-array-is-a-permutation-of-numbers-from-1-to-n/)而形成。如果可以合并，打印**是**。否则，打印**否**。

> [长度为 3 的排列](https://www.geeksforgeeks.org/check-if-an-array-is-a-permutation-of-numbers-from-1-to-n/)为{1，2，3}、{2，3，1}、{1，3，2}、{3，1，2}、{3，2，1}、{2，1，3}。

**示例:**

> **输入:** arr = [1，3，2，4，3，1，2]
> **输出:** YES
> **解释:**
> 给定的数组可以通过合并长度为 4 的排列[1，3，2，4]和长度为 3 的排列[3，1，2]而形成
> 
> **输入:** arr = [1，2，3，2，3，2，1]
> **输出:**否

**方法:**
我们可以观察到长度为 **N** 的排列的[最小排除符(MEX)](https://www.geeksforgeeks.org/combinatorial-game-theory-set-3-grundy-numbersnimbers-and-mex/) 为 **N+1** 。
所以，如果第一个排列的长度是 **l** ，那么前缀**arr【0……l-1】**的 MEX 就是 **l+1** ，后缀**a【l……N】**的 MEX 就是**N–l+1**。
那么，我们可以计算前缀和后缀的 MEX，如果满足上述条件，答案将是**“是”**。否则，答案将是**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the
// above approach
#include<bits/stdc++.h>
using namespace std;
void if_merged_permutations(int a[],
                            int n)
{
  int pre_mex[n];

  // Calculate the mex of the
  // array a[0...i]
  int freq[n + 1];

  memset(freq, 0, sizeof(freq));

  for(int i = 0; i < n; i++)
  {
    pre_mex[i] = 1;
  }

  // Mex of empty
  // array is 1
  int mex = 1;

  // Calculating the frequency
  // of array elements
  for(int i = 0; i < n; i++)
  {
    freq[a[i]]++;
    if(freq[a[i]] > 1)
    {
      // In a permutation
      // each element is
      // present one time,
      // So there is no chance
      // of getting permutations
      // for the prefix of
      // length greater than i
      break;
    }

    // The current element
    // is the mex
    if(a[i] == mex)
    {
      // While mex is present
      // in the array
      while(freq[mex] != 0)
      {
        mex++;
      }
    }
    pre_mex[i] = mex;
  }

  int suf_mex[n];

  for(int i = 0; i < n; i++)
  {
    suf_mex[i] = 1;
  }

  // Calculate the mex of the
  // array a[i..n]
  memset(freq, 0, sizeof(freq));

  // Mex of empty
  // array is 1
  mex = 1;

  // Calculating the frequency
  // of array elements
  for(int i = n - 1; i > -1; i--)
  {
    freq[a[i]]++;
    if(freq[a[i]] > 1)
    {
      // In a permutation each
      // element is present
      // one time, So there is
      // no chance of getting
      // permutations for the
      // suffix of length lesser
      // than i
      continue;
    }

    // The current element is
    // the mex
    if(a[i] == mex)
    {
      // While mex is present
      // in the array
      while(freq[mex] != 0)
      {
        mex++;
      }
    }
    suf_mex[i] = mex;
  }

  // Now check if there is atleast
  // one index i such that mex of
  // the prefix a[0..i]= i +
  // 2(0 based indexing) and  mex
  // of the suffix a[i + 1..n]= n-i
  for(int i = 0; i < n - 1; i++)
  {
    if(pre_mex[i] == i + 2 &&
       suf_mex[i + 1] == n - i)
    {
      cout << "YES" << endl;
      return;
    }
  }
  cout << "NO" << endl;
}

// Driver code
int main()
{
    int a[] = {1, 3, 2,
               4, 3, 1, 2};
    int n = sizeof(a)/ sizeof(a[0]);
    if_merged_permutations(a, n);   
}

//This code is contributed by avanitrachhadiya2155
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG{

static void if_merged_permutations(int a[],
                                   int n)
{
  int[] pre_mex = new int[n];

  // Calculate the mex of the
  // array a[0...i]
  int[] freq = new int[n + 1];

  for(int i = 0; i < n; i++)
  {
    pre_mex[i] = 1;
  }

  // Mex of empty
  // array is 1
  int mex = 1;

  // Calculating the frequency
  // of array elements
  for(int i = 0; i < n; i++)
  {
    freq[a[i]]++;

    if (freq[a[i]] > 1)
    {

      // In a permutation
      // each element is
      // present one time,
      // So there is no chance
      // of getting permutations
      // for the prefix of
      // length greater than i
      break;
    }

    // The current element
    // is the mex
    if (a[i] == mex)
    {

      // While mex is present
      // in the array
      while (freq[mex] != 0)
      {
        mex++;
      }
    }
    pre_mex[i] = mex;
  }

  int[] suf_mex = new int[n];

  for(int i = 0; i < n; i++)
  {
    suf_mex[i] = 1;
  }

  // Calculate the mex of the
  // array a[i..n]
  Arrays.fill(freq, 0);

  // Mex of empty
  // array is 1
  mex = 1;

  // Calculating the frequency
  // of array elements
  for(int i = n - 1; i > -1; i--)
  {
    freq[a[i]]++;

    if (freq[a[i]] > 1)
    {

      // In a permutation each
      // element is present
      // one time, So there is
      // no chance of getting
      // permutations for the
      // suffix of length lesser
      // than i
      continue;
    }

    // The current element is
    // the mex
    if (a[i] == mex)
    {

      // While mex is present
      // in the array
      while (freq[mex] != 0)
      {
        mex++;
      }
    }
    suf_mex[i] = mex;
  }

  // Now check if there is atleast
  // one index i such that mex of
  // the prefix a[0..i]= i +
  // 2(0 based indexing) and  mex
  // of the suffix a[i + 1..n]= n-i
  for(int i = 0; i < n - 1; i++)
  {
    if (pre_mex[i] == i + 2 &&
        suf_mex[i + 1] == n - i)
    {
      System.out.println("YES");
      return;
    }
  }
  System.out.println("NO");
}

// Driver code
public static void main(String[] args)
{
  int a[] = { 1, 3, 2, 4, 3, 1, 2 };
  int n = a.length;

  if_merged_permutations(a, n);   
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for above approach
def if_merged_permutations(a, n):
    pre_mex =[1 for i in range(n)]

    # Calculate the mex of the
    # array a[0...i]
    freq =[0 for i in range(n + 1)]

    # Mex of empty array is 1
    mex = 1

    # Calculating the frequency
    # of array elements
    for i in range(n):
        freq[a[i]]+= 1
        if freq[a[i]]>1:
            # In a permutation
            # each element is
            # present one time,
            # So there is no chance
            # of getting permutations
            # for the prefix of
            # length greater than i
            break

        # The current element
        # is the mex   
        if a[i]== mex:

            # While mex is present
            # in the array
            while freq[mex]!= 0 :
                mex+= 1
        pre_mex[i]= mex

    suf_mex =[1 for i in range(n)]

    # Calculate the mex of the
    # array a[i..n]
    freq =[0 for i in range(n + 1)]

    # Mex of empty array is 1
    mex = 1

    # Calculating the frequency
    # of array elements
    for i in range(n-1, -1, -1):
        freq[a[i]]+= 1
        if freq[a[i]]>1:

            # In a permutation each
            # element is present
            # one time, So there is
            # no chance of getting
            # permutations for the
            # suffix of length lesser
            # than i
            break

        # The current element is
        # the mex
        if a[i]== mex:
            # While mex is present
            # in the array
            while freq[mex]!= 0 :
                mex+= 1
        suf_mex[i]= mex

    # Now check if there is atleast
    # one index i such that mex of
    # the prefix a[0..i]= i +
    # 2(0 based indexing) and  mex
    # of the suffix a[i + 1..n]= n-i

    for i in range(n-1):
        if pre_mex[i]== i + 2 and suf_mex[i + 1]== n-i:
            print("YES")
            return
    print("NO")

a =[1, 3, 2, 4, 3, 1, 2]   
n = len(a)       
if_merged_permutations(a, n)
```

## C#

```
// C# program for above approach
using System;

class GFG{

static void if_merged_permutations(int[] a,
                                   int n)
{
    int[] pre_mex = new int[n];

    // Calculate the mex of the
    // array a[0...i]
    int[] freq = new int[n + 1];

    for(int i = 0; i < n; i++)
    {
        pre_mex[i] = 1;
    }

    // Mex of empty
    // array is 1
    int mex = 1;

    // Calculating the frequency
    // of array elements
    for(int i = 0; i < n; i++)
    {
        freq[a[i]]++;

        if (freq[a[i]] > 1)
        {

            // In a permutation
            // each element is
            // present one time,
            // So there is no chance
            // of getting permutations
            // for the prefix of
            // length greater than i
            break;
        }

        // The current element
        // is the mex
        if (a[i] == mex)
        {

            // While mex is present
            // in the array
            while (freq[mex] != 0)
            {
                mex++;
            }
        }
        pre_mex[i] = mex;
    }

    int[] suf_mex = new int[n];

    for(int i = 0; i < n; i++)
    {
        suf_mex[i] = 1;
    }

    // Calculate the mex of the
    // array a[i..n]
    Array.Fill(freq, 0);

    // Mex of empty
    // array is 1
    mex = 1;

    // Calculating the frequency
    // of array elements
    for(int i = n - 1; i > -1; i--)
    {
        freq[a[i]]++;

        if (freq[a[i]] > 1)
        {

            // In a permutation each
            // element is present
            // one time, So there is
            // no chance of getting
            // permutations for the
            // suffix of length lesser
            // than i
            continue;
        }

        // The current element is
        // the mex
        if (a[i] == mex)
        {

            // While mex is present
            // in the array
            while (freq[mex] != 0)
            {
                mex++;
            }
        }
        suf_mex[i] = mex;
    }

    // Now check if there is atleast
    // one index i such that mex of
    // the prefix a[0..i]= i +
    // 2(0 based indexing) and  mex
    // of the suffix a[i + 1..n]= n-i
    for(int i = 0; i < n - 1; i++)
    {
        if (pre_mex[i] == i + 2 &&
            suf_mex[i + 1] == n - i)
        {
            Console.WriteLine("YES");
            return;
        }
    }
    Console.WriteLine("NO");
}

// Driver Code
static void Main()
{
    int[] a = { 1, 3, 2, 4, 3, 1, 2 };
    int n = a.Length;

    if_merged_permutations(a, n);
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

// JavaScript program for above approach

function if_merged_permutations(a, n)
{
    var pre_mex = Array(n).fill(0);

    // Calculate the mex of the
    // array a[0...i]
    var freq = Array(n+1).fill(0);

    for(var i = 0; i < n; i++)
    {
        pre_mex[i] = 1;
    }

    // Mex of empty
    // array is 1
    var mex = 1;

    // Calculating the frequency
    // of array elements
    for(var i = 0; i < n; i++)
    {
        freq[a[i]]++;

        if (freq[a[i]] > 1)
        {

            // In a permutation
            // each element is
            // present one time,
            // So there is no chance
            // of getting permutations
            // for the prefix of
            // length greater than i
            break;
        }

        // The current element
        // is the mex
        if (a[i] == mex)
        {

            // While mex is present
            // in the array
            while (freq[mex] != 0)
            {
                mex++;
            }
        }
        pre_mex[i] = mex;
    }

    var suf_mex = Array(n).fill(0);;

    for(var i = 0; i < n; i++)
    {
        suf_mex[i] = 1;
    }

    // Calculate the mex of the
    // array a[i..n]
    freq = Array(n).fill(0);

    // Mex of empty
    // array is 1
    mex = 1;

    // Calculating the frequency
    // of array elements
    for(var i = n - 1; i > -1; i--)
    {
        freq[a[i]]++;

        if (freq[a[i]] > 1)
        {

            // In a permutation each
            // element is present
            // one time, So there is
            // no chance of getting
            // permutations for the
            // suffix of length lesser
            // than i
            continue;
        }

        // The current element is
        // the mex
        if (a[i] == mex)
        {

            // While mex is present
            // in the array
            while (freq[mex] != 0)
            {
                mex++;
            }
        }
        suf_mex[i] = mex;
    }

    // Now check if there is atleast
    // one index i such that mex of
    // the prefix a[0..i]= i +
    // 2(0 based indexing) and  mex
    // of the suffix a[i + 1..n]= n-i
    for(var i = 0; i < n - 1; i++)
    {
        if (pre_mex[i] == i + 2 &&
            suf_mex[i + 1] == n - i)
        {
            document.write("YES");
            return;
        }
    }
    document.write("NO");
}

// Driver Code
var a = [1, 3, 2, 4, 3, 1, 2];
var n = a.length;

if_merged_permutations(a, n);

</script>
```

**Output:** 

```
YES
```

**时间复杂度:** *O(N)*