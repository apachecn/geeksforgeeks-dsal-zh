# 给定数组中不存在的最大 N 的正整数

> 原文:[https://www . geesforgeks . org/给定数组中不存在的正整数/](https://www.geeksforgeeks.org/positive-integers-up-to-n-that-are-not-present-in-given-array/)

给定一个[数组](https://www.geeksforgeeks.org/array-data-structure/) **a[]** 和一个整数 **N** ，任务是从范围**【1，N】**中找到给定数组中不存在的所有自然数。

**示例:**

> **输入:** N = 5，a[] = {1，2，4，5}
> **输出:** 3
> **解释:** 3 是范围[1，5]中唯一不在数组中的整数。
> 
> **输入:** N = 10，a[] = {1，3，4，6，8，10}
> **输出:** 2 5 7 9

**天真方法:**解决这个问题最简单的方法是遍历范围[1，N]，对于范围中的每个数字，[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并检查数组中是否存在。
***时间复杂度:** O(N * len)，其中 **len** 表示数组的长度。*
***辅助空间:** O(1)*

**高效方法:**上述方法可以使用 [HashSet](https://www.geeksforgeeks.org/hashset-in-java/) 进行优化。[遍历给定的数组](https://www.geeksforgeeks.org/iterating-arrays-java/)和[将所有数组元素插入到哈希表](https://www.geeksforgeeks.org/set-insert-function-in-c-stl/)中。然后，遍历范围[1，N]，对于每个元素，检查它是否存在于 **HashSet** 中，或者不使用 [contains()](https://www.geeksforgeeks.org/hashset-contains-method-in-java/) 方法，以计算 O(1)复杂度的搜索。
***时间复杂度:** O(N)*
***辅助空间:** O(N)*

**替代方法:**给定的问题可以使用 C++ 中的[位集来解决。按照以下步骤解决问题:](https://www.geeksforgeeks.org/c-bitset-and-its-application/)

1.  初始化一个[位组](https://www.geeksforgeeks.org/c-bitset-and-its-application/)变量，**设置**，长度为 **N** 。
2.  对于每个数组元素，使用 **bset.set(arr[i]-1，0)** 将其位设置为 false，其中它将位置**arr[I]–1**处的位设置为 **0** 。
3.  现在，从 **bset 开始迭代。_Find_first()** 到**bset . size()–1**使用变量，说 **i** 。
4.  打印 **i + 1** 并设置 **bset。_Find_next()** 。

下面是上述方法的实现。

## C++

```
// CPP program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find positive integers
// from 1 to N that are not present in the array
void findMissingNumbers(int arr[], int len)
{
    const int M = 15;

    // Declare bitset
    bitset<M> bset;

    // Iterate from 0 to M - 1
    for (int i = 0; i < M; i++) {
        bset.set(i);
    }

    // Iterate from 0 to len - 1
    for (int i = 0; i < len; i++) {
        bset.set(arr[i] - 1, 0);
    }

    // Iterate from bset._Find_first()
    // to bset.size() - 1
    for (int i = bset._Find_first();
         i < bset.size();
         i = bset._Find_next(i)) {

        if (i + 1 > len)
            break;

        cout << i + 1 << endl;
    }
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 4, 6, 8, 9 };
    int n = sizeof(arr) / sizeof(arr[0]);

    findMissingNumbers(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;
class GFG
{

    // Function to find positive integers
    // from 1 to N that are not present in the array
    static void findMissingNumbers(int[] arr, int len)
    {
        int M = 15;

        // Declare bitset
        BitSet bset = new BitSet(M);

        // Iterate from 0 to M - 1
        for (int i = 0; i < M; i++)
        {
            bset.set(i);
        }

        // Iterate from 0 to len - 1
        for (int i = 0; i < len; i++)
        {
            bset.set(arr[i] - 1, false);
        }

        // Iterate from bset._Find_first()
        // to bset.size() - 1
        for (int i = bset.nextSetBit(0); i >= 0;
             i = bset.nextSetBit(i + 1))
        {
            if (i + 1 > len)
                break;
            System.out.println(i + 1);
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = new int[] { 1, 2, 4, 6, 8, 9 };
        int n = arr.length;
        findMissingNumbers(arr, n);
    }
}

// This code is contributed by Dharanendra L V
```

## 蟒蛇 3

```
# Python 3 program for the above approach

#  Function to find positive integers
# from 1 to N that are not present in the array
def findMissingNumbers(arr, n):

    M = 15

    # Declare bitset
    bset = [0]*M

    # Iterate from 0 to M - 1
    for i in range(M):
        bset[i] = i

    # Iterate from 0 to n - 1
    for i in range(n):
        bset[arr[i] - 1] = 0

    bset = [i for i in bset if i != 0]

    # Iterate from bset._Find_first()
    # to bset.size() - 1

    for i in range(len(bset)):

        if (bset[i] + 1 > n):
            break

        print(bset[i] + 1)

# Driver Code
if __name__ == "__main__":

    arr = [1, 2, 4, 6, 8, 9]
    n = len(arr)

    findMissingNumbers(arr, n)

    # This code is contributed by ukasp.
```

**Output:** 

```
3
5
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)