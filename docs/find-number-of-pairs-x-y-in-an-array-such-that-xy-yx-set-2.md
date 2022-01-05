# 找出数组中的对数(x，y ),使得 x^y > y^x |集合 2

> 原文:[https://www . geesforgeks . org/find-对数-x-y-in-a-so-xy-yx-set-2/](https://www.geeksforgeeks.org/find-number-of-pairs-x-y-in-an-array-such-that-xy-yx-set-2/)

给定两个正整数数组 **X[]** 和 **Y[]** ,求对的个数，使得 **x^y > y^x** 其中 x 是来自 X[]的元素，y 是来自 Y[]的元素。
**示例:**

> **输入:** X[] = {2，1，6}，Y = {1，5 }
> T3】输出: 3
> **解释:**
> 这 3 个可能的对是:
> (2，1)=>2<sup>1</sup>T35】1<sup>2</sup>T14】(2，5)=>2<sup>5</sup>(= 32)>5 18}，Y[] = {11，15，9}
> **输出:** 2
> **解释:**
> 可能的对是(10，11)和(10，15)。

**对于幼稚进场【O(M*N)】和【O(N logN + M logN)】进场，请参考** [**本文第 1 集**](https://www.geeksforgeeks.org/find-number-pairs-xy-yx/) **。**
**高效途径:**以上两种途径可以在 **O(N)时间复杂度**上进一步优化。
这种方法利用**后缀和**的概念来寻找解决方案。我们可以观察到，如果 y > x，那么 x^y > y^x.不过，下面的基本情况和例外情况需要考虑:

*   如果 x = 0，则可能 y 的计数为 0。
*   如果 x = 1，那么计数可能的 Y 是 0 的频率是 Y[]是要求的答案。
*   如果 x = 2，2 <sup>3</sup> < 3 <sup>2</sup> 和 2 <sup>4</sup> = 4 <sup>2</sup> 。因此，对于 x = 2，我们不能有一个有效的 y = {2，3，4}对。因此，频率 0、1 和 Y[]中所有数字 gt 4 的总和给出了所需有效对的计数
*   如果 x = 3，Y[]中除 3 之外的所有频率的总和给出了可能对的所需计数。

按照以下步骤解决问题:

*   存储 **Y** 数组中每个元素的频率。
*   存储包含频率的数组的后缀和。
*   对于不属于任何基本情况的 X[]中的每个元素 X，Y 的可能数量将是**后缀[X+1]+Y[]中 0 的计数+Y[]中 1 的计数**。对于基本情况，如上所述计算相应的对。
*   打印配对总数。

下面是上述方法的实现:

## C++

```
// C++ program to finds the number of
// pairs (x, y) from X[] and Y[]
// such that x^y > y^x

#include <bits/stdc++.h>
using namespace std;

// Function to return the count of pairs
int countPairs(int X[], int Y[], int m,
               int n)
{
    vector<int> suffix(1005);
    long long total_pairs = 0;
    for (int i = 0; i < n; i++)
        suffix[Y[i]]++;

    // Compute suffix sums till i = 3
    for (int i = 1e3; i >= 3; i--)
        suffix[i] += suffix[i + 1];

    for (int i = 0; i < m; i++) {

        // Base Case: x = 0
        if (X[i] == 0)

            // No valid pairs
            continue;

        // Base Case: x = 1
        else if (X[i] == 1) {

            // Store the count of 0's
            total_pairs += suffix[0];
            continue;
        }

        // Base Case: x = 2
        else if (X[i] == 2)

            // Store suffix sum upto 5
            total_pairs += suffix[5];

        // Base Case: x = 3
        else if (X[i] == 3)

            // Store count of 2 and
            // suffix sum upto 4
            total_pairs += suffix[2]
                           + suffix[4];

        // For all other values of x
        else
            total_pairs += suffix[X[i] + 1];

        // For all x >=2, every y = 0
        // and every y = 1 makes a valid pair
        total_pairs += suffix[0] + suffix[1];
    }

    // Return the count of pairs
    return total_pairs;
}

// Driver Program
int main()
{
    int X[] = { 10, 19, 18 };
    int Y[] = { 11, 15, 9 };

    int m = sizeof(X) / sizeof(X[0]);
    int n = sizeof(Y) / sizeof(Y[0]);

    cout << countPairs(X, Y, m, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to finds the number of
// pairs (x, y) from X[] and Y[]
// such that x^y > y^x
class GFG{

// Function to return the count of pairs
static int countPairs(int X[], int Y[], int m,
                      int n)
{
    int []suffix = new int[1005];
    long total_pairs = 0;

    for(int i = 0; i < n; i++)
        suffix[Y[i]]++;

    // Compute suffix sums till i = 3
    for(int i = (int)1e3; i >= 3; i--)
        suffix[i] += suffix[i + 1];

    for(int i = 0; i < m; i++)
    {

        // Base Case: x = 0
        if (X[i] == 0)

            // No valid pairs
            continue;

        // Base Case: x = 1
        else if (X[i] == 1)
        {

            // Store the count of 0's
            total_pairs += suffix[0];
            continue;
        }

        // Base Case: x = 2
        else if (X[i] == 2)

            // Store suffix sum upto 5
            total_pairs += suffix[5];

        // Base Case: x = 3
        else if (X[i] == 3)

            // Store count of 2 and
            // suffix sum upto 4
            total_pairs += suffix[2] +
                           suffix[4];

        // For all other values of x
        else
            total_pairs += suffix[X[i] + 1];

        // For all x >=2, every y = 0
        // and every y = 1 makes a valid pair
        total_pairs += suffix[0] + suffix[1];
    }

    // Return the count of pairs
    return (int) total_pairs;
}

// Driver code
public static void main(String[] args)
{
    int X[] = { 10, 19, 18 };
    int Y[] = { 11, 15, 9 };

    int m = X.length;
    int n = Y.length;

    System.out.print(countPairs(X, Y, m, n));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to finds the number of
# pairs (x, y) from X[] and Y[]
# such that x^y > y^x

# Function to return the count of pairs
def countPairs(X, Y, m, n):

    suffix = [0] * 1005
    total_pairs = 0

    for i in range(n):
        suffix[Y[i]] += 1

    # Compute suffix sums till i = 3
    for i in range(int(1e3), 2, -1 ):
        suffix[i] += suffix[i + 1]

    for i in range(m):

        # Base Case: x = 0
        if(X[i] == 0):

            # No valid pairs
            continue

        # Base Case: x = 1
        elif(X[i] == 1):

            # Store the count of 0's
            total_pairs += suffix[0]
            continue

        # Base Case: x = 2
        elif(X[i] == 2):

            # Store suffix sum upto 5
            total_pairs += suffix[5]

        # Base Case: x = 3
        elif(X[i] == 3):

            # Store count of 2 and
            # suffix sum upto 4
            total_pairs += (suffix[2] +
                            suffix[4])

        # For all other values of x
        else:
            total_pairs += suffix[X[i] + 1]

        # For all x >=2, every y = 0
        # and every y = 1 makes a valid pair
        total_pairs += suffix[0] + suffix[1]

    # Return the count of pairs
    return total_pairs

# Driver code
if __name__ == '__main__':

    X = [ 10, 19, 18 ]
    Y = [ 11, 15, 9 ]

    m = len(X)
    n = len(Y)

    print(countPairs(X, Y, m, n))

# This code is contributed by Shivam Singh
```

## C#

```
// C# program to finds the number of
// pairs (x, y) from []X and []Y
// such that x^y > y^x
using System;
class GFG{

    // Function to return the count of pairs
    static int countPairs(int[] X, int[] Y, int m, int n)
    {
        int[] suffix = new int[1005];
        long total_pairs = 0;
        for (int i = 0; i < n; i++)
            suffix[Y[i]]++;

        // Compute suffix sums till i = 3
        for (int i = (int)1e3; i >= 3; i--)
            suffix[i] += suffix[i + 1];

        for (int i = 0; i < m; i++)
        {

            // Base Case: x = 0
            if (X[i] == 0)

                // No valid pairs
                continue;

            // Base Case: x = 1
            else if (X[i] == 1)
            {

                // Store the count of 0's
                total_pairs += suffix[0];
                continue;
            }

            // Base Case: x = 2
            else if (X[i] == 2)

                // Store suffix sum upto 5
                total_pairs += suffix[5];

            // Base Case: x = 3
            else if (X[i] == 3)

                // Store count of 2 and
                // suffix sum upto 4
                total_pairs += suffix[2] + suffix[4];

            // For all other values of x
            else
                total_pairs += suffix[X[i] + 1];

            // For all x >=2, every y = 0
            // and every y = 1 makes a valid pair
            total_pairs += suffix[0] + suffix[1];
        }

        // Return the count of pairs
        return (int)total_pairs;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int[] X = {10, 19, 18};
        int[] Y = {11, 15, 9};
        int m = X.Length;
        int n = Y.Length;
        Console.Write(countPairs(X, Y, m, n));
    }
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to return the count of pairs
function countPairs(X, Y, m, n)
{
    let suffix = Array.from({length: 1005}, (_, i) => 0);
    let total_pairs = 0;

    for(let i = 0; i < n; i++)
        suffix[Y[i]]++;

    // Compute suffix sums till i = 3
    for(let i = 1e3; i >= 3; i--)
        suffix[i] += suffix[i + 1];

    for(let i = 0; i < m; i++)
    {

        // Base Case: x = 0
        if (X[i] == 0)

            // No valid pairs
            continue;

        // Base Case: x = 1
        else if (X[i] == 1)
        {

            // Store the count of 0's
            total_pairs += suffix[0];
            continue;
        }

        // Base Case: x = 2
        else if (X[i] == 2)

            // Store suffix sum upto 5
            total_pairs += suffix[5];

        // Base Case: x = 3
        else if (X[i] == 3)

            // Store count of 2 and
            // suffix sum upto 4
            total_pairs += suffix[2] +
                           suffix[4];

        // For all other values of x
        else
            total_pairs += suffix[X[i] + 1];

        // For all x >=2, every y = 0
        // and every y = 1 makes a valid pair
        total_pairs += suffix[0] + suffix[1];
    }

    // Return the count of pairs
    return total_pairs;
}

// Driver code

    let X = [ 10, 19, 18 ];
    let Y = [ 11, 15, 9 ];

    let m = X.length;
    let n = Y.length;

    document.write(countPairs(X, Y, m, n));

// This code is contributed by susmitakundugoaldanga.
</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)