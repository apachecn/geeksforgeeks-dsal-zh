# 使用减少操作的金字塔形式(先增加后减少)连续数组

> 原文:[https://www . geesforgeks . org/金字塔形-递增-递减-连续-数组-使用-减少-运算/](https://www.geeksforgeeks.org/pyramid-form-increasing-decreasing-consecutive-array-using-reduce-operations/)

我们有 N(其中 N > 2)块不同高度的石头排成一排。任务是用给定的石头阵列制作金字塔。在金字塔中，石头的高度从 1 开始，增加 1，直到它达到某个值 x，然后减少 1，直到它再次达到 1，即石头应该是 1，2，3，4…x–1，x，x–1，x–2…1。所有其他不属于金字塔的石头都应该有 0 的高度。我们不能将任何石头从它们当前的位置移开，但是，通过支付 1 的费用，我们可以降低石头的高度。我们希望将建造金字塔的成本降到最低。输出建造这座金字塔的最低成本。
**例:**

```
Input  : 1 2 3 4 2 1
Output : 4
The best pyramid that can be formed in this case is: 
1 2 3 2 1 0
The cost is thus:
(4 - 2) + (2 - 1) + (1 - 0) = 4

Input  : 1 5 2
Output : 4
We make a pyramid 1 2 1

Input  : 1 2 1
Output : 0
We already have a pyramid, we do not need to do any 
further construction.
```

通过简单的逻辑，我们可以证明建造成本最小的金字塔就是高度最大的金字塔。此外，两座高度相同的寺庙建造成本相同。
这可以显示如下:
假设拆除所有高度为 0 的石头的成本是 x。
假设拆除高度为 h 到 0 的寺庙的成本是 y。
然后，如果可以用给定的石头建造高度为 h 的寺庙，其成本将是 x–y。
通过使用这一点，我们可以将我们的方法简化为两个主要步骤:
1。确定能形成的最大高度的金字塔。
2。计算建造这样一座金字塔的成本。
步骤 2 可以在 O(N)时间复杂度内完成，假设我们知道我们的金字塔放在哪里。
因此，我们的重点应该是降低步骤 1 的时间复杂度。
**天真的做法**
对于数组中的每个位置，我们可以假设金字塔从那个点开始。然后我们求出从 1 开始建造一个最大高度的神庙的成本，直到更高的高度是不可能的，也就是假设一个金字塔的高度 1 是最大的，然后假设 2 是最大的，以此类推。从这些成本中，我们选择最低的。
这种方法使用 O(N^3).的时间复杂度
**改进方法**
对于每个位置，假设它是一个寺庙的中心。移动到这个点的左右，试图找到太阳穴的最大高度。
这可以通过将位置 I 处的镜腿的最大高度设置为 H(i)来实现，其中 H(i)是该点处的石头高度。然后我们向左移动。如果此时石头的高度小于 H(I)–1，我们现在将最大高度设置为 H(I–1)+1。这样我们就可以确定每个位置的最大高度。
这种方法使用 O(N^2).的时间复杂度
**动态规划方法**
通过对上述算法稍加修改，我们可以尝试得到一个 O(N)的方法。从左边开始，向右移动，找到在那个位置可以创建的最大可能的高度金字塔。假设该位置右侧的阵列部分是左侧的镜像。如果 H(i)是 I 位置石头的高度，那么 maxHeight(i) = Minimum(H(i)，I，maxHeight(I–1))
这可以解释如下:
最大可能高度不能超过 H(i)，因为我们只能降低石头的高度，而不能增加。
最大可能高度不能超过 I，因为金字塔必须从高度 1 开始。
最大可能高度不能超过它之前的石头的最大可能高度–1，因为石头每走一步必须增加 1。
我们计算一个从右向左移动的相似值。然后我们取每个位置这些值的最小值。然后通过确定最大值，我们可以计算出建造金字塔的最小成本。

## C++

```
// Program to find minimum cost for pyramid
// from given array
#include <iostream>
using namespace std;

#define ull unsigned long long

// Returns minimum cost to form a pyramid
ull minPyramidCost(ull arr[], ull N)
{
    // Store the maximum possible pyramid height
    ull *left = new ull[N];
    ull *right = new ull[N];

    // Maximum height at start is 1
    left[0] = min(arr[0], (ull)1);

    // For each position calculate maximum height
    for (int i = 1; i < N; ++i)
        left[i] = min(arr[i],
                      min(left[i - 1] + 1, (ull)i + 1));

    // Maximum height at end is 1
    right[N - 1] = min(arr[N - 1], (ull)1);

    // For each position calculate maximum height
    for (int i = N - 2; i >= 0; --i)
        right[i] = min(arr[i],
                       min(right[i + 1] + 1, N - i));

    // Find minimum possible among calculated values
    ull tot[N];
    for (int i = 0; i < N; ++i)
        tot[i] = min(right[i], left[i]);

    // Find maximum height of pyramid
    ull max_ind = 0;
    for (int i = 0; i < N; ++i)
        if (tot[i] > tot[max_ind])
            max_ind = i;

    // Calculate cost of this pyramid
    ull cost = 0;
    ull height = tot[max_ind];

    // Calculate cost of left half
    for (int x = max_ind; x >= 0; --x)
    {
        cost += arr[x] - height;
        if (height > 0)
            --height;
    }

    // Calculate cost of right half
    height = tot[max_ind] - 1;
    for (int x = max_ind + 1; x < N; ++x)
    {
        cost += arr[x] - height;
        if (height > 0)
            --height;
    }
    return cost;
}

// Driver code
int main()
{
    ull arr[] = {1, 2, 3, 4, 2, 1};
    ull N = sizeof(arr)/sizeof(arr[0]);
    cout << minPyramidCost(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum cost for
// pyramid from given array
import java.util.*;

class GFG{

// Returns minimum cost to form a pyramid
static int minPyramidCost(int arr[], int N)
{

    // Store the maximum possible pyramid height
    int left[] = new int[N];
    int right[] = new int[N];

    // Maximum height at start is 1
    left[0] = Math.min(arr[0], 1);

    // For each position calculate maximum height
    for(int i = 1; i < N; ++i)
        left[i] = Math.min(arr[i],
                           Math.min(left[i - 1] + 1,
                                         i + 1));

    // Maximum height at end is 1
    right[N - 1] = Math.min(arr[N - 1], 1);

    // For each position calculate maximum height
    for(int i = N - 2; i >= 0; --i)
        right[i] = Math.min(arr[i],
                            Math.min(right[i + 1] + 1,
                                           N - i));

    // Find minimum possible among
    // calculated values
    int tot[] = new int[N];
    for(int i = 0; i < N; ++i)
        tot[i] = Math.min(right[i], left[i]);

    // Find maximum height of pyramid
    int max_ind = 0;
    for(int i = 0; i < N; ++i)
        if (tot[i] > tot[max_ind])
            max_ind = i;

    // Calculate cost of this pyramid
    int cost = 0;
    int height = tot[max_ind];

    // Calculate cost of left half
    for(int x = max_ind; x >= 0; --x)
    {
        cost += arr[x] - height;
        if (height > 0)
            --height;
    }

    // Calculate cost of right half
    height = tot[max_ind] - 1;
    for(int x = max_ind + 1; x < N; ++x)
    {
        cost += arr[x] - height;
        if (height > 0)
            --height;
    }
    return cost;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3, 4, 2, 1 };
    int N = arr.length;

    System.out.print(minPyramidCost(arr, N));
}
}

// This code is contributed by chitranayal   
```

## 蟒蛇 3

```
# Program to find minimum cost for pyramid
# from given array

# Returns minimum cost to form a pyramid
def minPyramidCost(arr: list, N):

    # Store the maximum possible pyramid height
    left = [0] * N
    right = [0] * N

    # Maximum height at start is 1
    left[0] = min(arr[0], 1)

    # For each position calculate maximum height
    for i in range(1, N):
        left[i] = min(arr[i],
                  min(left[i - 1] + 1, i + 1))

    # Maximum height at end is 1
    right[N - 1] = min(arr[N - 1], 1)

    # For each position calculate maximum height
    for i in range(N - 2, -1, -1):
        right[i] = min(arr[i],
                   min(right[i + 1] + 1, N - i))

    # Find minimum possible among calculated values
    tot = [0] * N
    for i in range(N):
        tot[i] = min(right[i], left[i])

    # Find maximum height of pyramid
    max_ind = 0
    for i in range(N):
        if tot[i] > tot[max_ind]:
            max_ind = i

    # Calculate cost of this pyramid
    cost = 0
    height = tot[max_ind]

    # Calculate cost of left half
    for x in range(max_ind, -1, -1):
        cost += arr[x] - height
        if height > 0:
            height -= 1

    # Calculate cost of right half
    height = tot[max_ind] - 1
    for x in range(max_ind + 1, N):
        cost += arr[x] - height
        if height > 0:
            height -= 1

    return cost

# Driver Code
if __name__ == "__main__":
    arr = [1, 2, 3, 4, 2, 1]
    N = len(arr)
    print(minPyramidCost(arr, N))

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to find minimum cost for
// pyramid from given array
using System;

public class GFG
{

    // Returns minimum cost to form a pyramid
static int minPyramidCost(int[] arr, int N)
{

    // Store the maximum possible pyramid height
    int[] left = new int[N];
    int[] right = new int[N];

    // Maximum height at start is 1
    left[0] = Math.Min(arr[0], 1);

    // For each position calculate maximum height
    for(int i = 1; i < N; ++i)
        left[i] = Math.Min(arr[i],
                           Math.Min(left[i - 1] + 1,
                                         i + 1));

    // Maximum height at end is 1
    right[N - 1] = Math.Min(arr[N - 1], 1);

    // For each position calculate maximum height
    for(int i = N - 2; i >= 0; --i)
        right[i] = Math.Min(arr[i],
                            Math.Min(right[i + 1] + 1,
                                           N - i));

    // Find minimum possible among
    // calculated values
    int[] tot = new int[N];
    for(int i = 0; i < N; ++i)
        tot[i] = Math.Min(right[i], left[i]);

    // Find maximum height of pyramid
    int max_ind = 0;
    for(int i = 0; i < N; ++i)
        if (tot[i] > tot[max_ind])
            max_ind = i;

    // Calculate cost of this pyramid
    int cost = 0;
    int height = tot[max_ind];

    // Calculate cost of left half
    for(int x = max_ind; x >= 0; --x)
    {
        cost += arr[x] - height;
        if (height > 0)
            --height;
    }

    // Calculate cost of right half
    height = tot[max_ind] - 1;
    for(int x = max_ind + 1; x < N; ++x)
    {
        cost += arr[x] - height;
        if (height > 0)
            --height;
    }
    return cost;
}

// Driver code
    static public void Main ()
    {
        int[] arr = { 1, 2, 3, 4, 2, 1 };
        int N = arr.Length;

        Console.WriteLine(minPyramidCost(arr, N));
    }
}

// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>
// Javascript program to find minimum cost for
// pyramid from given array

// Returns minimum cost to form a pyramid
function minPyramidCost(arr,N)
{

       // Store the maximum possible pyramid height
    let left = new Array(N);
    let right = new Array(N);

    // Maximum height at start is 1
    left[0] = Math.min(arr[0], 1);

    // For each position calculate maximum height
    for(let i = 1; i < N; ++i)
        left[i] = Math.min(arr[i],
                           Math.min(left[i - 1] + 1,
                                         i + 1));

    // Maximum height at end is 1
    right[N - 1] = Math.min(arr[N - 1], 1);

    // For each position calculate maximum height
    for(let i = N - 2; i >= 0; --i)
        right[i] = Math.min(arr[i],
                            Math.min(right[i + 1] + 1,
                                           N - i));

    // Find minimum possible among
    // calculated values
    let tot = new Array(N);
    for(let i = 0; i < N; ++i)
        tot[i] = Math.min(right[i], left[i]);

    // Find maximum height of pyramid
    let max_ind = 0;
    for(let i = 0; i < N; ++i)
        if (tot[i] > tot[max_ind])
            max_ind = i;

    // Calculate cost of this pyramid
    let cost = 0;
    let height = tot[max_ind];

    // Calculate cost of left half
    for(let x = max_ind; x >= 0; --x)
    {
        cost += arr[x] - height;
        if (height > 0)
            --height;
    }

    // Calculate cost of right half
    height = tot[max_ind] - 1;
    for(let x = max_ind + 1; x < N; ++x)
    {
        cost += arr[x] - height;
        if (height > 0)
            --height;
    }
    return cost;
    }

    // Driver code
    let arr=[1, 2, 3, 4, 2, 1 ];
    let  N = arr.length;
    document.write(minPyramidCost(arr, N));

    // This code is contributed by rag2127.

</script>
```

**输出:**

```
4
```

这种方法的时间复杂度为 0(N)。
本文由**阿迪蒂亚·卡马特**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。