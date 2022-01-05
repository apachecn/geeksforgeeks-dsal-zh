# 从 GCD 为 K 的两个给定数组中生成一个 N 长度的序列

> 原文:[https://www . geesforgeks . org/generate-an-n-length-sequence-from-two-给定-array-what-gcd-is-k/](https://www.geeksforgeeks.org/generate-an-n-length-sequence-from-two-given-arrays-whose-gcd-is-k/)

给定两个大小均为 **N** 的[阵列](https://www.geeksforgeeks.org/array-data-structure/) **A[]** 和**B[]**，任务是生成长度为 **N** 的序列，该序列包含来自两个阵列的元素，使得生成序列的 [GCD](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) 为 **K** 。如果无法生成这样的序列，则打印**-1”**。

**示例:**

> **输入:** A[] = {5，3，6，2，9}，B[] = {21，7，14，12，28}，K = 3
> **输出:** 21，3，6，12，9
> **解释:**T8】ans[0]= 21(= B[0])
> ans[1]= 3(= A[1])
> ans[2]= 6(= A[2])【t1t
> 
> **输入:** A[] = {3，4，5，6，7}，B[] = {8，7，5，2，3}，K = 2
> **输出:** -1

**天真方法:**解决问题最简单的方法就是使用[递归](https://www.geeksforgeeks.org/recursion/)。递归检查给定条件的所有可能组合。
按照以下步骤解决问题:

*   定义一个函数来递归生成所有可能的组合，并执行以下步骤:
    *   基本条件是当当前组合的长度等于 **N** 时，检查当前组合的 GCD 是否等于**k**
    *   如果 GCD 等于 **K** ，打印组合并返回**真**。否则，返回**假**。
    *   将数组**中的一个元素【A】**添加到组合中，然后继续。
    *   在递归调用后移除添加的元素。
    *   将数组 **B[]** 中的一个元素添加到组合中，然后继续。
    *   在递归调用后移除添加的元素。
*   如果任意组合的 GCD 不等于 **K** ，则打印 **-1。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate
// GCD of two integers
int GCD(int a, int b)
{
    if (!b)
        return a;
    return GCD(b, a % b);
}

// Function to calculate
// GCD of a given array
int GCDArr(vector<int> a)
{
    int ans = a[0];
    for (int i:a)
        ans = GCD(ans, i);
    return ans;
}

// Utility function to check for
// all the possible combinations
bool findSubseqUtil(vector<int>  a,vector<int>  b,
                    vector<int>  &ans,int k,int i)
{

    // If an N-length sequence
    // is obtained
    if (ans.size() == a.size())
    {

        // If GCD of the sequence is K
        if (GCDArr(ans) == k)
        {
           cout << "[";
           int m = ans.size();
           for(int i = 0; i < m - 1; i++)
             cout << ans[i] << ", ";
           cout << ans[m - 1] << "]";
            return true;
          }

        // Otherwise
        else
            return false;
      }

    // Add an element from the first array
    ans.push_back(a[i]);

    // Recursively proceed further
    bool temp = findSubseqUtil(a, b, ans, k, i + 1);

    // If combination satisfies
    // the necessary condition
    if (temp)
        return true;

    // Remove the element
    // from the combination
    ans.pop_back();

    // Add an element from the second array
    ans.push_back(b[i]);

    // Recursive proceed further
    temp = findSubseqUtil(a, b, ans, k, i + 1);

    // If combination satisfies
    // the necessary condition
    if (temp)
        return true;

    // Remove the element
    // from the combination
    ans.pop_back();
    return false;
}

// Function to check all the
// possible combinations
void findSubseq(vector<int> A, vector<int>  B,
                int K, int i)
{

    // Stores the subsequence
    vector<int>  ans;

    findSubseqUtil(A, B, ans, K, i);

    // If GCD is not equal to K
    // for any combination
    if (!ans.size())
        cout << -1;
}

// Driver Code
int main()
{

  // Given arrays
  vector<int> A = {5, 3, 6, 2, 9};
  vector<int>  B = {21, 7, 14, 12, 28};

  // Given value of K
  int K = 3;

  // Function call to generate
  // the required subsequence
  findSubseq(A, B, K, 0);

  return 0;
}

// This code is contributed by mohit kumar 29.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import java.lang.*;
class GFG
{

  // Function to calculate
  // GCD of two integers
  static int GCD(int a, int b)
  {
    if (b < 1)
      return a;
    return GCD(b, a % b);
  }

  // Function to calculate
  // GCD of a given array
  static int GCDArr(ArrayList<Integer> a)
  {
    int ans = a.get(0);
    for(int i : a) ans = GCD(ans, i);
    return ans;
  }

  // Utility function to check for
  // all the possible combinations
  static boolean findSubseqUtil(ArrayList<Integer> a, ArrayList<Integer> b,
                                ArrayList<Integer> ans, int k, int i)
  {

    // If an N-length sequence
    // is obtained
    if (ans.size() == a.size()) {

      // If GCD of the sequence is K
      if (GCDArr(ans) == k) {
        System.out.print("[");
        int m = ans.size();
        for (int j = 0; j < m - 1; j++)
          System.out.print(ans.get(j) + ", ");
        System.out.print(ans.get(m-1) + "]");
        return true;
      }

      // Otherwise
      else
        return false;
    }

    // Add an element from the first array
    ans.add(a.get(i));

    // Recursively proceed further
    boolean temp = findSubseqUtil(a, b, ans, k, i + 1);

    // If combination satisfies
    // the necessary condition
    if (temp)
      return true;

    // Remove the element
    // from the combination
    ans.remove(ans.size() - 1);

    // Add an element from the second array
    ans.add(b.get(i));

    // Recursive proceed further
    temp = findSubseqUtil(a, b, ans, k, i + 1);

    // If combination satisfies
    // the necessary condition
    if (temp)
      return true;

    // Remove the element
    // from the combination
    ans.remove(ans.size() - 1);
    return false;
  }

  // Function to check all the
  // possible combinations
  static void findSubseq(ArrayList<Integer> A, ArrayList<Integer> B, int K,
                         int i)
  {

    // Stores the subsequence
    ArrayList<Integer> ans = new ArrayList<Integer>();

    findSubseqUtil(A, B, ans, K, i);

    // If GCD is not equal to K
    // for any combination
    if (ans.size() < 1)
      System.out.println(-1);
  }

  // Driver code
  public static void main(String[] args)
  {
    // Given arrays
    ArrayList<Integer> A = new ArrayList<>();
    A.add(5);
    A.add(3);
    A.add(6);
    A.add(2);
    A.add(9);

    ArrayList<Integer> B = new ArrayList<Integer>();
    B.add(21);
    B.add(7);
    B.add(14);
    B.add(12);
    B.add(28);

    // Given value of K
    int K = 3;

    // Function call to generate
    // the required subsequence
    findSubseq(A, B, K, 0);
  }
}

// This code is contributed by sanjoy_62.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate
# GCD of two integers

def GCD(a, b):
    if not b:
        return a
    return GCD(b, a % b)

# Function to calculate
# GCD of a given array

def GCDArr(a):
    ans = a[0]
    for i in a:
        ans = GCD(ans, i)
    return ans

# Utility function to check for
# all the possible combinations

def findSubseqUtil(a, b, ans, k, i):

    # If an N-length sequence
    # is obtained
    if len(ans) == len(a):

        # If GCD of the sequence is K
        if GCDArr(ans) == k:
            print(ans)
            return True

        # Otherwise
        else:
            return False

    # Add an element from the first array
    ans.append(a[i])

    # Recursively proceed further
    temp = findSubseqUtil(a, b, ans, k, i+1)

    # If combination satisfies
    # the necessary condition
    if temp == True:
        return True

    # Remove the element
    # from the combination
    ans.pop()

    # Add an element from the second array
    ans.append(b[i])

    # Recursive proceed further
    temp = findSubseqUtil(a, b, ans, k, i+1)

    # If combination satisfies
    # the necessary condition
    if temp == True:
        return True

    # Remove the element
    # from the combination
    ans.pop()

# Function to check all the
# possible combinations

def findSubseq(A, B, K, i):

    # Stores the subsequence
    ans = []

    findSubseqUtil(A, B, ans, K, i)

    # If GCD is not equal to K
    # for any combination
    if not ans:
        print(-1)

# Driver Code

# Given arrays
A = [5, 3, 6, 2, 9]
B = [21, 7, 14, 12, 28]

# Given value of K
K = 3

# Function call to generate
# the required subsequence
ans = findSubseq(A, B, K, 0)
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG
{

  // Function to calculate
  // GCD of two integers
  static int GCD(int a, int b)
  {
    if (b < 1)
      return a;
    return GCD(b, a % b);
  }

  // Function to calculate
  // GCD of a given array
  static int GCDArr(List<int> a)
  {
    int ans = a[0];
    foreach(int i in a) ans = GCD(ans, i);
    return ans;
  }

  // Utility function to check for
  // all the possible combinations
  static bool findSubseqUtil(List<int> a, List<int> b,
                             List<int> ans, int k, int i)
  {

    // If an N-length sequence
    // is obtained
    if (ans.Count == a.Count) {

      // If GCD of the sequence is K
      if (GCDArr(ans) == k) {
        Console.Write("[");
        int m = ans.Count;
        for (int j = 0; j < m - 1; j++)
          Console.Write(ans[j] + ", ");
        Console.Write(ans[m - 1] + "]");
        return true;
      }

      // Otherwise
      else
        return false;
    }

    // Add an element from the first array
    ans.Add(a[i]);

    // Recursively proceed further
    bool temp = findSubseqUtil(a, b, ans, k, i + 1);

    // If combination satisfies
    // the necessary condition
    if (temp)
      return true;

    // Remove the element
    // from the combination
    ans.RemoveAt(ans.Count - 1);

    // Add an element from the second array
    ans.Add(b[i]);

    // Recursive proceed further
    temp = findSubseqUtil(a, b, ans, k, i + 1);

    // If combination satisfies
    // the necessary condition
    if (temp)
      return true;

    // Remove the element
    // from the combination
    ans.RemoveAt(ans.Count - 1);
    return false;
  }

  // Function to check all the
  // possible combinations
  static void findSubseq(List<int> A, List<int> B, int K,
                         int i)
  {

    // Stores the subsequence
    List<int> ans = new List<int>();

    findSubseqUtil(A, B, ans, K, i);

    // If GCD is not equal to K
    // for any combination
    if (ans.Count < 1)
      Console.WriteLine(-1);
  }

  // Driver Code
  public static void Main()
  {

    // Given arrays
    List<int> A = new List<int>{ 5, 3, 6, 2, 9 };
    List<int> B = new List<int>{ 21, 7, 14, 12, 28 };

    // Given value of K
    int K = 3;

    // Function call to generate
    // the required subsequence
    findSubseq(A, B, K, 0);
  }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to calculate
  // GCD of two integers
function GCD(a,b)
{
    if (b < 1)
      return a;
    return GCD(b, a % b);
}

// Function to calculate
  // GCD of a given array
function GCDArr(a)
{
    let ans = a[0];
    for(let i=0;i<a.length;i++)
        ans = GCD(ans, a[i]);
    return ans;
}

// Utility function to check for
  // all the possible combinations
function findSubseqUtil(a,b,ans,k,i)
{
    // If an N-length sequence
    // is obtained
    if (ans.length == a.length) {

      // If GCD of the sequence is K
      if (GCDArr(ans) == k) {
        document.write("[");
        let m = ans.length;
        for (let j = 0; j < m - 1; j++)
          document.write(ans[j] + ", ");
        document.write(ans[m-1] + "]");
        return true;
      }

      // Otherwise
      else
        return false;
    }

    // Add an element from the first array
    ans.push(a[i]);

    // Recursively proceed further
    let temp = findSubseqUtil(a, b, ans, k, i + 1);

    // If combination satisfies
    // the necessary condition
    if (temp)
      return true;

    // Remove the element
    // from the combination
    ans.splice(ans.length - 1,1);

    // Add an element from the second array
    ans.push(b[i]);

    // Recursive proceed further
    temp = findSubseqUtil(a, b, ans, k, i + 1);

    // If combination satisfies
    // the necessary condition
    if (temp)
      return true;

    // Remove the element
    // from the combination
    ans.splice(ans.length - 1,1);
    return false;
}

// Function to check all the
  // possible combinations
function findSubseq(A,B,K,i)
{
    // Stores the subsequence
    let ans = [];

    findSubseqUtil(A, B, ans, K, i);

    // If GCD is not equal to K
    // for any combination
    if (ans.length < 1)
      document.write(-1);
}

// Driver code

// Given arrays
let A = [5, 3, 6, 2, 9];
let B = [21, 7, 14, 12, 28];

// Given value of K
let K = 3;

// Function call to generate
// the required subsequence
findSubseq(A, B, K, 0);

// This code is contributed by patel2127

</script>
```

**Output:** 

```
[21, 3, 6, 12, 9]
```

***时间复杂度:**O(2<sup>N</sup>* N * logN)*
***辅助空间:** O(N)*

**高效方法:**要优化上述方法，请按照以下步骤解决问题:

*   序列的 [GCD 将等于 **K** ，前提是序列中存在的所有元素都可以被 **K** 整除。](https://www.geeksforgeeks.org/gcd-two-array-numbers/)
*   同时遍历阵列，并执行以下步骤:
    *   检查数组 **A[]** 中的当前元素是否可以被 **K** 整除。如果发现为真，则进行递归调用。否则，退回**假。**
    *   检查数组 **B[]** 中的当前元素是否可以被 **K** 整除。如果发现为真，则进行递归调用。否则，退回**假**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

int GCD(int a, int b)
{
    if (b == 0)
        return a;

    return GCD(b, a % b);
}

// Function to calculate
// GCD of given array
int GCDArr(vector<int> a)
{
    int ans = a[0];
    for(auto val : a)
    {
        ans = GCD(ans, val);
    }
    return ans;
}

// Utility function to check for
// all the combinations
bool findSubseqUtil(int a[], int b[], vector<int> ans,
                    int k, int i, int N)
{

    // If a sequence of size N
    // is obtained
    if (ans.size() == N)
    {

        // If gcd of current
        // combination is K
        if (GCDArr(ans) == k)
        {
            for(auto val : ans)
                cout << val << " ";

            return true;
        }
        else
        {
            return false;
        }
    }

    // If current element from
    // first array is divisible by K
    if (a[i] % k == 0)
    {
        ans.push_back(a[i]);

        // Recursively proceed further
        bool temp = findSubseqUtil(a, b, ans, k,
                                   i + 1, N);

        // If current combination
        // satisfies given condition
        if (temp == true)
            return true;

        // Remove the element
        // from the combination
        ans.pop_back();
    }

    // If current element from
    // second array is divisible by K
    if (b[i] % k == 0)
    {
        ans.push_back(b[i]);

        // Recursively proceed further
        bool temp = findSubseqUtil(a, b, ans, k,
                                   i + 1, N);

        // If current combination
        // satisfies given condition
        if (temp == true)
            return true;

        // Remove the element
        // from the combination
        ans.pop_back();
    }
    return false;
}

// Function to check for all
// possible combinations
void findSubseq(int A[], int B[], int K,
                int i, int N)
{

    // Stores the subsequence
    vector<int> ans;

    bool ret = findSubseqUtil(A, B, ans,
                              K, i, N);

    // If GCD of any sequence
    // is not equal to K
    if (ret == false)
        cout << -1 << "\n";
}

// Driver Code
int main()
{

    // Given arrays
    int A[] = { 5, 3, 6, 2, 9 };
    int B[] = { 21, 7, 14, 12, 28 };

    // size of the array
    int N = sizeof(A) / sizeof(A[0]);

    // Given value of K
    int K = 3;

    // Function call to generate a
    // subsequence whose GCD is K
    findSubseq(A, B, K, 0, N);

    return 0;
}

// This code is contributed by Kingash
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

static int GCD(int a, int b)
{
    if (b == 0)
        return a;

    return GCD(b, a % b);
}

// Function to calculate
// GCD of given array
static int GCDArr(ArrayList<Integer> a)
{
    int ans = a.get(0);
    for(int val : a)
    {
        ans = GCD(ans, val);
    }
    return ans;
}

// Utility function to check for
// all the combinations
static boolean findSubseqUtil(int a[], int b[],
                              ArrayList<Integer> ans,
                              int k, int i)
{

    // If a sequence of size N
    // is obtained
    if (ans.size() == a.length)
    {

        // If gcd of current
        // combination is K
        if (GCDArr(ans) == k)
        {
            System.out.println(ans);
            return true;
        }
        else
        {
            return false;
        }
    }

    // If current element from
    // first array is divisible by K
    if (a[i] % k == 0)
    {
        ans.add(a[i]);

        // Recursively proceed further
        boolean temp = findSubseqUtil(a, b, ans,
                                      k, i + 1);

        // If current combination
        // satisfies given condition
        if (temp == true)
            return true;

        // Remove the element
        // from the combination
        ans.remove(ans.size() - 1);
    }

    // If current element from
    // second array is divisible by K
    if (b[i] % k == 0)
    {
        ans.add(b[i]);

        // Recursively proceed further
        boolean temp = findSubseqUtil(a, b, ans,
                                      k, i + 1);

        // If current combination
        // satisfies given condition
        if (temp == true)
            return true;

        // Remove the element
        // from the combination
        ans.remove(ans.size() - 1);
    }
    return false;
}

// Function to check for all
// possible combinations
static void findSubseq(int A[], int B[],
                       int K, int i)
{

    // Stores the subsequence
    ArrayList<Integer> ans = new ArrayList<>();

    boolean ret = findSubseqUtil(A, B, ans, K, i);

    // If GCD of any sequence
    // is not equal to K
    if (ret == false)
        System.out.println(-1);
}

// Driver Code
public static void main(String[] args)
{

    // Given arrays
    int A[] = { 5, 3, 6, 2, 9 };
    int B[] = { 21, 7, 14, 12, 28 };

    // Given value of K
    int K = 3;

    // Function call to generate a
    // subsequence whose GCD is K
    findSubseq(A, B, K, 0);
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate
# GCD of two integers

def GCD(a, b):
    if not b:
        return a
    return GCD(b, a % b)

# Function to calculate
# GCD of given array
def GCDArr(a):
    ans = a[0]
    for i in a:
        ans = GCD(ans, i)
    return ans

# Utility function to check for
# all the combinations
def findSubseqUtil(a, b, ans, k, i):

    # If a sequence of size N
    # is obtained
    if len(ans) == len(a):

        # If gcd of current
        # combination is K
        if GCDArr(ans) == k:
            print(ans)
            return True

        else:
            return False

    # If current element from
    # first array is divisible by K
    if not a[i] % K:
        ans.append(a[i])

        # Recursively proceed further
        temp = findSubseqUtil(a, b, ans, k, i+1)

        # If current combination
        # satisfies given condition
        if temp == True:
            return True

        # Remove the element
        # from the combination
        ans.pop()

    # If current element from
    # second array is divisible by K
    if not b[i] % k:

        ans.append(b[i])

        # Recursively proceed further
        temp = findSubseqUtil(a, b, ans, k, i+1)

        # If current combination
        # satisfies given condition
        if temp == True:
            return True

        # Remove the element
        # from the combination
        ans.pop()

    return False

# Function to check for all
# possible combinations
def findSubseq(A, B, K, i):

    # Stores the subsequence
    ans = []

    findSubseqUtil(A, B, ans, K, i)

    # If GCD of any sequence
    # is not equal to K
    if not ans:
        print(-1)

# Driver Code

# Given arrays
A = [5, 3, 6, 2, 9]
B = [21, 7, 14, 12, 28]

# Given value of K
K = 3

# Function call to generate a
# subsequence whose GCD is K
ans = findSubseq(A, B, K, 0)
```

## C#

```
// C# program for the above approach

using System;
using System.Collections.Generic;

class GFG{

static int GCD(int a, int b)
{
    if (b == 0)
        return a;

    return GCD(b, a % b);
}

// Function to calculate
// GCD of given array
static int GCDArr(List<int> a)
{
    int ans = a[0];
    foreach (int val in a)
    {
        ans = GCD(ans, val);
    }
    return ans;
}

// Utility function to check for
// all the combinations
static bool findSubseqUtil(int []a, int []b, List<int> ans,
                    int k, int i, int N)
{

    // If a sequence of size N
    // is obtained
    if (ans.Count == N)
    {

        // If gcd of current
        // combination is K
        if (GCDArr(ans) == k)
        {
            foreach(int val in ans)
               Console.Write(val+" ");

            return true;
        }
        else
        {
            return false;
        }
    }

    // If current element from
    // first array is divisible by K
    if (a[i] % k == 0)
    {
        ans.Add(a[i]);

        // Recursively proceed further
        bool temp = findSubseqUtil(a, b, ans, k,
                                   i + 1, N);

        // If current combination
        // satisfies given condition
        if (temp == true)
            return true;

        // Remove the element
        // from the combination
        ans.RemoveAt(ans.Count - 1);
    }

    // If current element from
    // second array is divisible by K
    if (b[i] % k == 0)
    {
        ans.Add(b[i]);

        // Recursively proceed further
        bool temp = findSubseqUtil(a, b, ans, k,
                                   i + 1, N);

        // If current combination
        // satisfies given condition
        if (temp == true)
            return true;

        // Remove the element
        // from the combination
        ans.RemoveAt(ans.Count - 1);
    }
    return false;
}

// Function to check for all
// possible combinations
static void findSubseq(int []A, int []B, int K,
                int i, int N)
{

    // Stores the subsequence
    List<int> ans = new List<int>();

    bool ret = findSubseqUtil(A, B, ans,
                              K, i, N);

    // If GCD of any sequence
    // is not equal to K
    if (ret == false)
        Console.Write(-1);
}

// Driver Code
public static void Main()
{

    // Given arrays
    int []A = { 5, 3, 6, 2, 9 };
    int []B = { 21, 7, 14, 12, 28 };

    // size of the array
    int N = A.Length;

    // Given value of K
    int K = 3;

    // Function call to generate a
    // subsequence whose GCD is K
    findSubseq(A, B, K, 0, N);
}
}

// This code is contributed by ipg2016107.
```

## java 描述语言

```
<script>

      // JavaScript program for the above approach

      function GCD(a, b) {
        if (b === 0) return a;

        return GCD(b, a % b);
      }

      // Function to calculate
      // GCD of given array
      function GCDArr(a) {
        var ans = a[0];
        for (const val of a) {
          ans = GCD(ans, val);
        }
        return ans;
      }

      // Utility function to check for
      // all the combinations
      function findSubseqUtil(a, b, ans, k, i, N) {
        // If a sequence of size N
        // is obtained
        if (ans.length === N) {
          // If gcd of current
          // combination is K
          if (GCDArr(ans) === k) {
            document.write("[" + ans + "]");
            return true;
          } else {
            return false;
          }
        }

        // If current element from
        // first array is divisible by K
        if (a[i] % k === 0) {
          ans.push(a[i]);

          // Recursively proceed further
          var temp = findSubseqUtil(a, b, ans, k, i + 1, N);

          // If current combination
          // satisfies given condition
          if (temp === true) return true;

          // Remove the element
          // from the combination
          delete ans[ans.length - 1];
        }

        // If current element from
        // second array is divisible by K
        if (b[i] % k === 0) {
          ans.push(b[i]);

          // Recursively proceed further
          var temp = findSubseqUtil(a, b, ans, k, i + 1, N);

          // If current combination
          // satisfies given condition
          if (temp === true) return true;

          // Remove the element
          // from the combination
          delete ans[ans.length - 1];
        }
        return false;
      }

      // Function to check for all
      // possible combinations
      function findSubseq(A, B, K, i, N) {
        // Stores the subsequence
        var ans = [];

        var ret = findSubseqUtil(A, B, ans, K, i, N);

        // If GCD of any sequence
        // is not equal to K
        if (ret === false) document.write(-1);
      }

      // Driver Code
      // Given arrays
      var A = [5, 3, 6, 2, 9];
      var B = [21, 7, 14, 12, 28];

      // size of the array
      var N = A.length;

      // Given value of K
      var K = 3;

      // Function call to generate a
      // subsequence whose GCD is K
      findSubseq(A, B, K, 0, N);

</script>
```

**Output:** 

```
[21, 3, 6, 12, 9]
```

***时间复杂度:**O(2<sup>N</sup>* N * logN)*
***辅助空间:** O(N)*