# 至少一个非空子数组按位“与”的数字

> 原文:[https://www . geeksforgeeks . org/numbers-按位与至少一个非空子数组/](https://www.geeksforgeeks.org/numbers-that-are-bitwise-and-of-at-least-one-non-empty-sub-array/)

给定一个数组“arr”，任务是找到所有可能的整数，每个整数都是“arr”的至少一个非空子数组的按位“与”。

**示例:**

```
Input: arr = {11, 15, 7, 19}
Output: [3, 19, 7, 11, 15]
3 = arr[2] AND arr[3]
19 = arr[3]
7 = arr[2]
11 = arr[0]
15 = arr[1]

Input: arr = {5, 2, 8, 4, 1}
Output: [0, 1, 2, 4, 5, 8]
0 = arr[3] AND arr[4]
1 = arr[4]
2 = arr[1]
4 = arr[3]
5 = arr[0]
8 = arr[2]

```

**天真方法:**

*   大小为“N”的数组包含 N*(N+1)/2 个子数组。因此，对于小“N”，迭代所有可能的子数组，并将它们的每个“与”结果添加到一个集合中。
*   因为集合不包含重复项，所以每个值只存储一次。
*   最后，打印集合的内容。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

int main()
{
    int A[] = {11, 15, 7, 19};
    int N = sizeof(A) / sizeof(A[0]);

    // Set to store all possible AND values.
    unordered_set<int> s;
    int i, j, res;

    // Starting index of the sub-array.
    for (i = 0; i < N; ++i)

        // Ending index of the sub-array.
        for (j = i, res = INT_MAX; j < N; ++j)
        {
            res &= A[j];

            // AND value is added to the set.
            s.insert(res);
        }

    // The set contains all possible AND values.
    for (int i : s)
        cout << i << " ";

    return 0;
}

// This code is contributed by
// sanjeev2552
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.HashSet;
class CP {
    public static void main(String[] args)
    {
        int[] A = { 11, 15, 7, 19 };
        int N = A.length;

        // Set to store all possible AND values.
        HashSet<Integer> set = new HashSet<>();
        int i, j, res;

        // Starting index of the sub-array.
        for (i = 0; i < N; ++i)

            // Ending index of the sub-array.
            for (j = i, res = Integer.MAX_VALUE; j < N; ++j) {
                res &= A[j];

                // AND value is added to the set.
                set.add(res);
            }

        // The set contains all possible AND values.
        System.out.println(set);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach 

A = [11, 15, 7, 19]  
N = len(A) 

# Set to store all possible AND values. 
Set = set() 

# Starting index of the sub-array. 
for i in range(0, N): 

    # Ending index of the sub-array.
    res = 2147483647    # Integer.MAX_VALUE
    for j in range(i, N):  
        res &= A[j] 

        # AND value is added to the set. 
        Set.add(res) 

# The set contains all possible AND values. 
print(Set)

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the approach 
using System;
using System.Collections.Generic;

class CP { 

    public static void Main(String[] args) 
    { 
        int[] A = {11, 15, 7, 19}; 
        int N = A.Length; 

        // Set to store all possible AND values. 
        HashSet<int> set1 = new HashSet<int>(); 
        int i, j, res;

        // Starting index of the sub-array. 
        for (i = 0; i < N; ++i) 
        {
            // Ending index of the sub-array. 
            for (j = i, res = int.MaxValue; j < N; ++j)
            { 
                res &= A[j]; 

                // AND value is added to the set. 
                set1.Add(res); 
            }

        }

        // displaying the values
        foreach(int m in set1)
        {
            Console.Write(m + " ");
        }

    } 
} 
```

**Output:**

```
[3, 19, 7, 11, 15]

```

**时间复杂度:** O(N^2)

**高效法:**这个问题可以通过分治法高效解决。

*   将数组的每个元素视为一个单独的段。(“划分”步骤)
*   将所有子阵列的“与”值相加。
*   现在，对于“征服”步骤，继续合并连续的子阵列，并继续添加合并时获得的附加“与”值。
*   继续步骤 4，直到获得包含整个数组的单个段。

下面是上述方法的实现:

```
// Java implementation of the approach
import java.util.*;

public class CP {
    static int ar[];
    static int n;

    // Holds all possible AND results
    static HashSet<Integer> allPossibleAND;

    // driver code
    public static void main(String[] args)
    {
        ar = new int[] { 11, 15, 7, 19 };
        n = ar.length;

        allPossibleAND = new HashSet<>(); // initialization
        divideThenConquer(0, n - 1);

        System.out.println(allPossibleAND);
    }

    // recursive function which adds all
    // possible AND results to 'allPossibleAND'
    static Segment divideThenConquer(int l, int r)
    {

        // can't divide into 
        //further segments
        if (l == r)
        {
            allPossibleAND.add(ar[l]);

            // Therefore, return a segment
            // containing this single element.
            Segment ret = new Segment();
            ret.leftToRight.add(ar[l]);
            ret.rightToLeft.add(ar[l]);
            return ret;
        }

        // can be further divided into segments
        else {
            Segment left 
                = divideThenConquer(l, (l + r) / 2);
            Segment right 
                = divideThenConquer((l + r) / 2 + 1, r);

            // Now, add all possible AND results,
            // contained in these two segments

            /* ********************************
            This step may seem to be inefficient 
            and time consuming, but it is not.
            Read the 'Analysis' block below for 
            further clarification.
            *********************************** */
            for (int itr1 : left.rightToLeft)
                for (int itr2 : right.leftToRight)
                    allPossibleAND.add(itr1 & itr2);

            // 'conquer' step
            return mergeSegments(left, right);
        }
    }

    // returns the resulting segment after
    // merging segments 'a' and 'b'
    // 'conquer' step
    static Segment mergeSegments(Segment a, Segment b)
    {
        Segment res = new Segment();

        // The resulting segment will have
        // same prefix sequence as segment 'a'
        res.copyLR(a.leftToRight);

        // The resulting segment will have
        // same suffix sequence as segment 'b'
        res.copyRL(b.rightToLeft);

        Iterator<Integer> itr;

        itr = b.leftToRight.iterator();
        while (itr.hasNext())
            res.addToLR(itr.next());

        itr = a.rightToLeft.iterator();
        while (itr.hasNext())
            res.addToRL(itr.next());

        return res;
    }
}

class Segment {

    // These 'vectors' will always 
    // contain atmost 30 values.
    ArrayList<Integer> leftToRight 
        = new ArrayList<>();
    ArrayList<Integer> rightToLeft 
        = new ArrayList<>();

    void addToLR(int value)
    {
        int lastElement 
            = leftToRight.get(leftToRight.size() - 1);

        // value decreased after AND-ing with 'value'
        if ((lastElement & value) < lastElement)
            leftToRight.add(lastElement & value);
    }

    void addToRL(int value)
    {
        int lastElement 
            = rightToLeft.get(rightToLeft.size() - 1);

        // value decreased after AND-ing with 'value'
        if ((lastElement & value) < lastElement)
            rightToLeft.add(lastElement & value);
    }

    // copies 'lr' to 'leftToRight'
    void copyLR(ArrayList<Integer> lr)
    {
        Iterator<Integer> itr = lr.iterator();
        while (itr.hasNext())
            leftToRight.add(itr.next());
    }

    // copies 'rl' to 'rightToLeft'
    void copyRL(ArrayList<Integer> rl)
    {
        Iterator<Integer> itr = rl.iterator();
        while (itr.hasNext())
            rightToLeft.add(itr.next());
    }
}
```

**Output:**

```
[19, 3, 7, 11, 15]

```

**分析:**

该算法的主要优化是认识到任何数组元素最多可以产生 30 个不同的整数(因为需要 30 位来保存 1e9)。迷茫？？让我们一步一步来。

让我们从第 I 个元素 A[i]开始一个子数组。当后续元素与 Ai 进行“与”运算时，结果可以减少或保持不变(因为在“与”运算后，位永远不会从“0”变为“1”)。
在最坏的情况下，A[i]可以是 2^31-1(所有 30 位都是“1”)。由于元素是“与”的，因此可以获得 30 个不同的值，因为在最坏的情况下，
可能只有一个位从“1”变为“0”，即 11111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111

因此，对于每个“合并”操作，这些不同的值会合并形成另一个具有 30 个整数的集合。
因此，每次合并的**最坏情况时间复杂度**可以是 O(30 * 30) = O(900)。

**时间复杂度:** O(900*N*logN)。

PS:时间复杂度看起来可能太高，但实际上实际复杂度在 O(K*N*logN)左右，其中，K 远小于 900。这是因为，当“l”和“r”非常接近时，“前缀”和“后缀”数组的长度要少得多。