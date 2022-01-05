# 打印 N 项关闭序列

> 原文:[https://www . geesforgeks . org/print-n-of-with-off-sequence/](https://www.geeksforgeeks.org/print-n-terms-of-withoff-sequence/)

Wythoff 数组是从[斐波那契](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)序列中导出的无限整数矩阵。矩阵中的每个正整数只出现一次。
T3【怀瑟夫阵:T5】

```
  1    2    3    5    8    13    ...

  4    7    11   18   29   47    ...

  6    10   16   26   42   68    ...

  9    15   24   39   63   102   ...

  12   20   32   52   84   136   ...

  14   23   37   60   97   157   ...

  .    .    .    .    .    .
  .    .    .    .    .    . 
```

如果 **A <sub>m，n</sub>** 表示第 **mth** 行和第**n**列中的元素，则

*   A <sub>m，1</sub> = [[mφ]φ]
*   A <sub>m，2</sub>=[【mφ】φ<sup>2</sup>
*   A <sub>m，n</sub> = A <sub>m，n-2</sub> + A <sub>m，n-1</sub> 代表 n > 2
*   φ = (1 + √5) / 2

如果我们从左上角元素开始以**反对角线**方式遍历矩阵，那么
**Wythoff 序列:**

> 1, 2, 4, 3, 7, 6, 5, 11, 10, 9….

对于给定的 **N** ，任务首先打印序列的 **N** 号。
**例:**

> **输入:** N = 10
> **输出:** 1、2、4、3、7、6、5、11、10、9
> **输入:** N = 15
> **输出:** 1、2、4、3、7、6、5、11、10、9、8、18、16、15、12

**进场:**
以上循环可修改为

*   T(n，-1) = n-1，如果 k = -1
*   T(n，0) = [n*φ]，如果 k = 0
*   T(n，k) = T(n，k-1) + T(n，k-2)，如果 k > 0
*   φ = (1 + √5) / 2

所以我们可以递归地找到 **T(n，k)** 的值，对于 **t = 0** 和对于**T =–**1 有两种基本情况。我们将这些值存储在**图**中，并在需要时使用它来减少计算。在我们得到数组后，我们必须以反对角线的方式遍历它，所以我们设置 **i=0** 和 **j=** 0 并减少 **j** 并增加 **i** 当 **j < 0** 时，我们初始化 **j = i** 和 **i = 0** 。
我们还保留一个计数，当显示一个数字时，该计数会增加。当计数达到要求的值时，我们中断数组。
以下是上述方法的实施:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to find Wythoff array
#include <bits/stdc++.h>
using namespace std;

// Function to find the n, k term of Wythoff array
int Wythoff(map<int, map<int, int> >& mp, int n, int k)
{
    // tau = (sqrt(5)+1)/2
    double tau = (sqrt(5) + 1) / 2.0, t_n_k;

    // Already_stored
    if (mp[n][k] != 0)
        return mp[n][k];

    // T(n, -1) = n-1.
    if (k == -1) {
        return n - 1;
    }

    // T(n, 0) = floor(n*tau).
    else if (k == 0) {
        t_n_k = floor(n * tau);
    }

    // T(n, k) = T(n, k-1) + T(n, k-2) for k>=1.
    else
    {
        t_n_k = Wythoff(mp, n, k - 1) +
                             Wythoff(mp, n, k - 2);
    }

    // Store
    mp[n][k] = t_n_k;

    // Return the ans
    return (int)t_n_k;
}

// Function to find  first n terms of Wythoff
// array by traversing in anti-diagonal
void Wythoff_Array(int n)
{
    int i = 0, j = 0, count = 0;

    // Map to store the Wythoff array
    map<int, map<int, int> > mp;

    while (count < n) {

        cout << Wythoff(mp, i + 1, j + 1);
        count++;

        if(count != n)
            cout << ", ";

        // Anti diagonal
        i++;
        j--;

        if (j < 0) {
            j = i;
            i = 0;
        }
    }
}

// Driver code
int main()
{
    int n = 15;

    // Function call
    Wythoff_Array(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find Wythoff array
import java.util.*;
public class GFG
{

  // Function to find the n, k term of Wythoff array
  static int Wythoff(HashMap<Integer,
                     HashMap<Integer, Integer>> mp,
                     int n, int k)
  {

    // tau = (sqrt(5)+1)/2
    double tau = (Math.sqrt(5) + 1) / 2.0, t_n_k;

    // Already_stored
    if (mp.containsKey(n) &&
        mp.get(n).containsKey(k) &&
        mp.get(n).get(k) != 0)
      return mp.get(n).get(k);

    // T(n, -1) = n-1.
    if (k == -1)
    {
      return n - 1;
    }

    // T(n, 0) = floor(n*tau).
    else if (k == 0)
    {
      t_n_k = Math.floor(n * tau);
    }

    // T(n, k) = T(n, k-1) + T(n, k-2) for k>=1.
    else
    {
      t_n_k = Wythoff(mp, n, k - 1) +
        Wythoff(mp, n, k - 2);
    }

    // Store
    mp.put(n, new HashMap<Integer, Integer>(k,(int)t_n_k));

    // Return the ans
    return (int)t_n_k;
  }

  // Function to find  first n terms of Wythoff
  // array by traversing in anti-diagonal
  static void Wythoff_Array(int n)
  {
    int i = 0, j = 0, count = 0;

    // Map to store the Wythoff array
    HashMap<Integer, HashMap<Integer,Integer>> mp =
      new HashMap<Integer, HashMap<Integer,Integer>>();
    while (count < n)
    {
      System.out.print(Wythoff(mp, i + 1, j + 1));
      count++;
      if(count != n)
        System.out.print(", ");

      // Anti diagonal
      i++;
      j--;

      if (j < 0)
      {
        j = i;
        i = 0;
      }
    }
  }

  // Driver code
  public static void main(String[] args)
  {
    int n = 15;

    // Function call
    Wythoff_Array(n);
  }
}

// This code is contributed by divyeshrabadiya07.
```

## 蟒蛇 3

```
# Python3 program to find Wythoff array
import math

# Function to find the n, k term of Wythoff array
def Wythoff(mp, n, k):

    # tau = (sqrt(5)+1)/2
    tau = (math.sqrt(5) + 1) / 2
    t_n_k = 0

    # Already_stored
    if ((n in mp) and (k in mp[n])):
        return mp[n][k];

    # T(n, -1) = n-1.
    if (k == -1):
        return n - 1;

    # T(n, 0) = floor(n*tau).
    elif (k == 0):
        t_n_k = math.floor(n * tau);

    # T(n, k) = T(n, k-1) + T(n, k-2) for k>=1.
    else:
        t_n_k = Wythoff(mp, n, k - 1) + Wythoff(mp, n, k - 2)

    # Store
    if n not in mp:
        mp[n] = dict()
    mp[n][k] = t_n_k;

    # Return the ans
    return int(t_n_k)

# Function to find  first n terms of Wythoff
# array by traversing in anti-diagonal
def Wythoff_Array(n):

    i = 0
    j = 0
    count = 0;

    # Map to store the Wythoff array
    mp = dict()

    while (count < n):

        print(Wythoff(mp, i + 1, j + 1), end = '')
        count += 1

        if(count != n):
            print(", ", end = '')

        # Anti diagonal
        i += 1
        j -= 1

        if (j < 0):
            j = i;
            i = 0;

# Driver code
if __name__=='__main__':

    n = 15;

    # Function call
    Wythoff_Array(n);

    # This code is contributed by rutvik_56
```

## C#

```
// C# program to find Wythoff array
using System;
using System.Collections.Generic;
class GFG
{

  // Function to find the n, k term of Wythoff array
  static int Wythoff(Dictionary<int, Dictionary<int, int>> mp, int n, int k)
  {

    // tau = (sqrt(5)+1)/2
    double tau = (Math.Sqrt(5) + 1) / 2.0, t_n_k;

    // Already_stored
    if (mp.ContainsKey(n) && mp[n].ContainsKey(k) && mp[n][k] != 0)
      return mp[n][k];

    // T(n, -1) = n-1.
    if (k == -1) {
      return n - 1;
    }

    // T(n, 0) = floor(n*tau).
    else if (k == 0)
    {
      t_n_k = Math.Floor(n * tau);
    }

    // T(n, k) = T(n, k-1) + T(n, k-2) for k>=1.
    else
    {
      t_n_k = Wythoff(mp, n, k - 1) + Wythoff(mp, n, k - 2);
    }

    // Store
    if(!mp.ContainsKey(n))
    {
      mp[n] = new Dictionary<int,int>();
    }
    mp[n][k] = (int)t_n_k;

    // Return the ans
    return (int)t_n_k;
  }

  // Function to find  first n terms of Wythoff
  // array by traversing in anti-diagonal
  static void Wythoff_Array(int n)
  {
    int i = 0, j = 0, count = 0;

    // Map to store the Wythoff array
    Dictionary<int, Dictionary<int,int>> mp = new Dictionary<int, Dictionary<int,int>>();
    while (count < n)
    {

      Console.Write(Wythoff(mp, i + 1, j + 1));
      count++;
      if(count != n)
        Console.Write(", ");

      // Anti diagonal
      i++;
      j--;

      if (j < 0) {
        j = i;
        i = 0;
      }
    }
  }

  // Driver code
  static void Main()
  {
    int n = 15;

    // Function call
    Wythoff_Array(n);
  }
}

// This code is contributed by divyesh072019.
```

**输出:**

```
1, 2, 4, 3, 7, 6, 5, 11, 10, 9, 8, 18, 16, 15, 12, 
```

**参考:**T2https://oeis.org/A035513