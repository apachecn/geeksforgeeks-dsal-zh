# 计数可被`K`整除的数组中的对数 | 系列 2

> 原文：[https://www.geeksforgeeks.org/count-number-of-pairs-in-array-having-sum-divisible-by-k-set-2/](https://www.geeksforgeeks.org/count-number-of-pairs-in-array-having-sum-divisible-by-k-set-2/)

给定一个数组 A []和正整数 K，任务是计算其和可被 K 整除的数组中的对总数。

**示例**：

> **输入**：`A[] = {2, 2, 1, 7, 5, 5}, K = 4`
>
> **输出**：5
>
> 可能有五对和可被 4 整除，即`(2, 2)`，`(1, 7)`，`(7, 5)`，`(1, 3)`和`(5, 3)`
>
> **输入**：`A[] = {5, 9, 36, 74, 52, 31, 42}, K = 3`
>
> **输出**：7

**方法**：在先前的[文章](https://www.geeksforgeeks.org/count-pairs-in-array-whose-sum-is-divisible-by-k/)中，讨论了一种使用哈希的方法。 在本文中，讨论了使用哈希的另一种方法。

分析该语句，我们可以说我们需要对（a，b）进行配对，使得：

```
     (a + b) % K = 0
 =>    a%K + b%K = 0
 =>    a%K + b%K = K%K
 =>    b%K = K%K - a%K
 =>     b%K = (K - a%K) % K.     {Range of a%K => [0,K-1]}

```

这个想法是 ***一个*** 可以与（K-a％K）％K 配对。现在我们必须为每个 ***一个*** 存在于给定数组中。

该算法将创建一个散列图：

**键**：值％K 的可能余数，即 0 到 K-1。

**值**：值％K 的值计数 =键

逐步算法为：

1.  求 x = arr [i]％k。

2.  该数组元素可以与具有 mod 值 k-x 的数组元素配对。 数组元素的此频率计数存储在哈希中。 因此，添加该计数即可回答。

3.  x 在哈希中的增量计数。

4.  如果 x 的值为零，则只能与 mod 值为 0 的元素配对。

下面是上述方法的实现：

## C++

```cpp

// C++ Program to count pairs
// whose sum divisible by 'K'
#include <bits/stdc++.h>
using namespace std;

// Program to count pairs whose sum divisible
// by 'K'
int countKdivPairs(int A[], int n, int K)
{
    // Create a frequency array to count
    // occurrences of all remainders when
    // divided by K
    int freq[K] = { 0 };

    // To store count of pairs.
    int ans = 0;

    // Traverse the array, compute the remainder
    // and add k-remainder value hash count to ans
    for (int i = 0; i < n; i++) {
        int rem = A[i] % K;

        // Count number of ( A[i], (K - rem)%K ) pairs
          ans += freq[(K - rem) % K];

        // Increment count of remainder in hash map
        freq[rem]++;
    }

    return ans;
}

// Driver code
int main()
{

    int A[] = { 2, 2, 1, 7, 5, 3 };
    int n = sizeof(A) / sizeof(A[0]);
    int K = 4;
    cout << countKdivPairs(A, n, K);

    return 0;
}

```

## Java

```java

// JAVA Program to count pairs whose sum divisible
// by 'K'
class GFG 
{

  static int countKdivPairs(int A[], int n, int K)
  {
      // Create a frequency array to count
      // occurrences of all remainders when
      // divided by K
      int []freq = new int[K];

      // To store count of pairs.
      int ans = 0;

      // Traverse the array, compute the remainder
      // and add k-remainder value hash count to ans
      for (int i = 0; i < n; i++)
      {
          int rem = A[i] % K;

          // Count number of ( A[i], (K - rem)%K ) pairs
          ans += freq[(K - rem) % K];

          // Increment count of remainder in hash map
          freq[rem]++;
      }

      return ans;
  }

// Driver code
  public static void main(String[] args) 
  {
      int A[] = { 2, 2, 1, 7, 5, 3 };
      int n = A.length;
      int K = 4;
      System.out.println(countKdivPairs(A, n, K));
  }
}

// This code is contributed by Princi Singh, Yadvendra Naveen

```

## Python3

```py

# Python Program to count pairs whose sum divisible
# by 'K'
def countKdivPairs(A, n, K):

    # Create a frequency array to count
    # occurrences of all remainders when
    # divided by K
    freq = [0 for i in range(K)]

    # To store count of pairs.
    ans = 0

    # Traverse the array, compute the remainder
    # and add k-remainder value hash count to ans
    for i in range(n):
        rem = A[i] % K

        # Count number of ( A[i], (K - rem)%K ) pairs
        ans += freq[(K - rem) % K]

        # Increment count of remainder in hash map
        freq[rem] += 1

    return ans

# Driver code
if __name__ == '__main__':
    A = [2, 2, 1, 7, 5, 3]
    n = len(A)
    K = 4
    print(countKdivPairs(A, n, K))

# This code is contributed by
# Surendra_Gangwar, Yadvendra Naveen

```

## C#

```cs

// C# Program to count pairs
// whose sum divisible by 'K'
using System;

class GFG 
{

// Program to count pairs whose sum divisible
// by 'K'
static int countKdivPairs(int []A, int n, int K)
{
    // Create a frequency array to count
    // occurrences of all remainders when
    // divided by K
    int []freq = new int[K];

    // To store count of pairs.
    int ans = 0;

    // Traverse the array, compute the remainder
    // and add k-remainder value hash count to ans
    for (int i = 0; i < n; i++)
    {
        int rem = A[i] % K;

        // Count number of ( A[i], (K - rem)%K ) pairs
          ans += freq[(K - rem) % K];

        // Increment count of remainder in hash map
        freq[rem]++;
    }

    return ans;
}

// Driver code
public static void Main(String[] args) 
{
    int []A = { 2, 2, 1, 7, 5, 3 };
    int n = A.Length;
    int K = 4;
    Console.WriteLine(countKdivPairs(A, n, K));
}
}

// This code contributed by Rajput-Ji, Yadvendra Naveen

```

**Output:** 

```
5

```

**时间复杂度**：`O(n)`

**辅助空间**：`O(K)`



* * *

* * *



