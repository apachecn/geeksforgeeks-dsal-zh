# 从立方体为回文的范围内计数数字

> 原文:[https://www . geesforgeks . org/count-numbers-from-a-range-who-cube-a-回文/](https://www.geeksforgeeks.org/count-numbers-from-a-range-whose-cube-is-a-palindrome/)

给定一个由形式为 **{L，R}** 的 **N** 个查询组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **Q[][]** ，每个查询的任务是从范围**【L，R】**中找到数字的总数，其立方体是一个[回文](https://www.geeksforgeeks.org/tag/palindrome/)。

**示例:**

> **输入:** Q[][] = {{2，10}，{10，20}}
> **输出:**
> 2
> 1
> **解释:**
> 查询 1:立方是回文的[2，10]中的数字是 2，7
> 查询 2:立方是回文的[10，20]中唯一的数字是 11
> 
> **输入:** Q[][] = {{1，50}，{13，15}}
> **输出:**
> 4
> 0
> **解释:**
> 查询 1:范围[1，50]中的数字，其立方是回文，为{1，2，7，11}。
> 查询 2:在[13，15]范围内没有这样的数字。

**方法:**解决问题最简单的思路就是使用[包含-排除原理](https://www.geeksforgeeks.org/inclusion-exclusion-various-applications/)和[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)技术来解决这个问题。按照以下步骤解决给定的问题:

*   初始化一个数组 **arr[]** ，在每个**I<sup>th</sup>T5<sup>T7】索引处存储[I**的立方体是否为回文**](https://www.geeksforgeeks.org/check-if-a-number-is-palindrome/)。</sup>**
*   遍历数组**arr【】**并针对每一个**I<sup>th</sup>T5<sup>T7】索引，检查 [**i** 的立方体是否为回文](https://www.geeksforgeeks.org/program-to-check-the-number-is-palindrome-or-not/)。</sup>**
    *   如果发现为真，则设置 **arr[i] = 1** 。
    *   否则，设置 **arr[i] = 0** 。
*   将数组 **arr[]** 转换为[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **Q[][]** ，通过计算**arr[R]–arr[L-1]**从立方体为回文的**【L，R】**范围内计数。

下面是上述方法的实现。

## C++

```
// C++ program of the above approach
#include <bits/stdc++.h>
using namespace std;

int arr[10005];

// Function to check if n is
// a pallindrome number or not
int isPalindrome(int n)
{
    // Temporarily store n
    int temp = n;

    // Stores reverse of n
    int res = 0;

    // Iterate until temp reduces to 0
    while (temp != 0) {
        // Extract the last digit
        int rem = temp % 10;

        // Add to the start
        res = res * 10 + rem;

        // Remove the last digit
        temp /= 10;
    }

    // If the number and its
    // reverse are equal
    if (res == n) {
        return 1;
    }

    // Otherwise
    else
        return 0;
}

// Function to precompute and store
// the count of numbers whose cube
// is a palindrome number
void precompute()
{
    // Iterate upto 10^4
    for (int i = 1; i <= 10000; i++) {

        // Check if i*i*i is a
        // pallindrome or not
        if (isPalindrome(i * i * i))
            arr[i] = 1;
        else
            arr[i] = 0;
    }

    // Convert arr[] to prefix sum array
    for (int i = 1; i <= 10000; i++) {
        arr[i] = arr[i] + arr[i - 1];
    }
}

// Driver Code
int main()
{
    // Given queries
    vector<pair<int, int> > Q = { { 2, 7 }, { 10, 25 } };

    precompute();

    for (auto it : Q) {

        // Using inclusion-exclusion
        // principle, count required numbers
        cout << arr[it.second] - arr[it.first - 1] << "\n";
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the above approach
import java.io.*;
import java.util.*;
public class Pair {
  private final int key;
  private final int value;

  public Pair(int aKey, int aValue)
  {
    key = aKey;
    value = aValue;
  }

  public int key() { return key; }
  public int value() { return value; }
}

class GFG {
  static int[] arr = new int[10005];

  // Function to check if n is
  // a pallindrome number or not
  static int isPalindrome(int n)
  {

    // Temporarily store n
    int temp = n;

    // Stores reverse of n
    int res = 0;

    // Iterate until temp reduces to 0
    while (temp != 0)
    {

      // Extract the last digit
      int rem = temp % 10;

      // Add to the start
      res = res * 10 + rem;

      // Remove the last digit
      temp /= 10;
    }

    // If the number and its
    // reverse are equal
    if (res == n) {
      return 1;
    }

    // Otherwise
    else
      return 0;
  }

  // Function to precompute and store
  // the count of numbers whose cube
  // is a palindrome number
  static void precompute()
  {

    // Iterate upto 10^4
    for (int i = 1; i <= 10000; i++) {

      // Check if i*i*i is a
      // pallindrome or not
      if (isPalindrome(i * i * i)!= 0)
        arr[i] = 1;
      else
        arr[i] = 0;
    }

    // Convert arr[] to prefix sum array
    for (int i = 1; i <= 10000; i++) {
      arr[i] = arr[i] + arr[i - 1];
    }
  }

  // Driver Code
  public static void main(String[] args)
  {

    // Given queries
    ArrayList<Pair> Q = new ArrayList<Pair>();
    Pair pair = new Pair(2, 7);
    Q.add(pair);
    Pair pair2 = new Pair(10, 25);
    Q.add(pair2);

    precompute();

    for (int i = 0; i < Q.size(); i++)  {

      // Using inclusion-exclusion
      // principle, count required numbers
      System.out.println(arr[Q.get(i).value()] - arr[Q.get(i).key()-1]);
    }
  }
}

// This code is contributed by Dharanendra L V
```

**Output:** 

```
2
1
```

***时间复杂度:** O(N)*
***辅助空间:** O(maxm)，其中 **maxm** 表示查询*中 **R** 的最大值