# 找到给定子序列的最小长度子阵列

> 原文:[https://www . geesforgeks . org/find-最小长度子数组-其中有给定的子序列/](https://www.geeksforgeeks.org/find-minimum-length-sub-array-which-has-given-sub-sequence-in-it/)

给定一个由 **N** 个元素组成的数组 **arr[]** ，任务是找出最小子数组的长度，该子数组中有序列 **{0，1，2，3，4}** 作为子序列。

**例:**

> **输入:** arr[] = {0，1，2，3，4，2，0，3，4}
> **输出:** 5
> 所需的斯巴鲁是{0，1，2，3，4}最小长度。
> 整个数组也包含序列
> ，但长度不是最小的。
> 
> **输入:** arr[] = {0，1，1，0，1，2，0，3，4}
> **输出:** 6

**进场:**

*   保持一个大小为 **5** (等于序列的大小)的数组 **pref[]** ，其中 **pref[i]** 存储给定数组中 **i** 的计数。
*   只有当**pref[Array[I]–1]>0 时，我们才能增加任何数字的 pref 计数。**这是因为，为了有完整的序列作为数组的子序列，序列的所有先前元素必须出现在当前元素之前。此外，存储到目前为止找到的这些元素的索引。
*   每当我们看到 **4** ，即子序列的可能结束，并且**pref【3】>0**暗示我们已经在数组中找到序列。现在将该索引标记为终点和起点，以及从 **3** 到 **0** 的所有其他数字。应用二分搜索法找到序列中下一个元素的最近索引，这将给出当前有效子数组的大小。
*   答案是上一步中找到的所有有效子阵列的最小大小。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

#define MAX_INT 1000000

// Function to return the minimum length
// of a sub-array which contains
// {0, 1, 2, 3, 4} as a sub-sequence
int solve(int Array[], int N)
{
    // To store the indices where 0, 1, 2,
    // 3 and 4 are present
    vector<int> pos[5];

    // To store if there exist a valid prefix
    // of sequence in array
    int pref[5] = { 0 };

    // Base Case
    if (Array[0] == 0) {
        pref[0] = 1;
        pos[0].push_back(0);
    }

    int ans = MAX_INT;

    for (int i = 1; i < N; i++) {

        // If current element is 0
        if (Array[i] == 0) {

            // Update the count of 0s till now
            pref[0]++;

            // Push the index of the new 0
            pos[0].push_back(i);
        }
        else {

            // To check if previous element of the
            // given sequence is found till now
            if (pref[Array[i] - 1] > 0) {
                pref[Array[i]]++;
                pos[Array[i]].push_back(i);

                // If it is the end of sequence
                if (Array[i] == 4) {
                    int end = i;
                    int start = i;

                    // Iterate for other elements of the sequence
                    for (int j = 3; j >= 0; j--) {
                        int s = 0;
                        int e = pos[j].size() - 1;
                        int temp = -1;

                        // Binary Search to find closest occurrence
                        // less than equal to starting point
                        while (s <= e) {
                            int m = (s + e) / 2;
                            if (pos[j][m] <= start) {
                                temp = pos[j][m];
                                s = m + 1;
                            }
                            else {
                                e = m - 1;
                            }
                        }

                        // Update the starting point
                        start = temp;
                    }

                    ans = min(ans, end - start + 1);
                }
            }
        }
    }

    return ans;
}

// Driver code
int main()
{
    int Array[] = { 0, 1, 2, 3, 4, 2, 0, 3, 4 };
    int N = sizeof(Array) / sizeof(Array[0]);

    cout << solve(Array, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
static int MAX_INT = 1000000;

// Function to return the minimum length
// of a sub-array which contains
// {0, 1, 2, 3, 4} as a sub-sequence
static int solve(int[] array, int N)
{

    // To store the indices where 0, 1, 2,
    // 3 and 4 are present
    int[][] pos = new int[5][10000];

    // To store if there exist a valid prefix
    // of sequence in array
    int[] pref = new int[5];

    // Base Case
    if (array[0] == 0)
    {
        pref[0] = 1;
        pos[0][pos[0].length - 1] = 0;
    }

    int ans = MAX_INT;

    for (int i = 1; i < N; i++)
    {

        // If current element is 0
        if (array[i] == 0)
        {

            // Update the count of 0s till now
            pref[0]++;

            // Push the index of the new 0
            pos[0][pos[0].length - 1] = i;
        }

        else
        {

            // To check if previous element of the
            // given sequence is found till now
            if (pref[array[i] - 1] > 0)
            {
                pref[array[i]]++;
                pos[array[i]][pos[array[i]].length - 1] = i;

                // If it is the end of sequence
                if (array[i] == 4)
                {
                    int end = i;
                    int start = i;

                    // Iterate for other elements of the sequence
                    for (int j = 3; j >= 0; j--)
                    {
                        int s = 0;
                        int e = pos[j].length - 1;
                        int temp = -1;

                        // Binary Search to find closest occurrence
                        // less than equal to starting point
                        while (s <= e)
                        {
                            int m = (s + e) / 2;
                            if (pos[j][m] <= start)
                            {
                                temp = pos[j][m];
                                s = m + 1;
                            }
                            else
                                e = m - 1;
                        }

                        // Update the starting point
                        start = temp;
                    }
                    ans = Math.min(ans, end - start + 1);
                }
            }
        }
    }
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int[] array = { 0, 1, 2, 3, 4, 2, 0, 3, 4 };
    int N = array.length;

    System.out.println(solve(array, N));
}
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of the approach

MAX_INT=1000000

# Function to return the minimum length
# of a sub-array which contains
# 0, 1, 2, 3, 4 as a sub-sequence
def solve(Array, N):

    # To store the indices where 0, 1, 2,
    # 3 and 4 are present
    pos=[[] for i in range(5)]

    # To store if there exist a valid prefix
    # of sequence in array
    pref=[0 for i in range(5)]

    # Base Case
    if (Array[0] == 0):
        pref[0] = 1
        pos[0].append(0)

    ans = MAX_INT

    for i in range(N):

        # If current element is 0
        if (Array[i] == 0):

            # Update the count of 0s till now
            pref[0]+=1

            # Push the index of the new 0
            pos[0].append(i)

        else :

            # To check if previous element of the
            # given sequence is found till now
            if (pref[Array[i] - 1] > 0):
                pref[Array[i]]+=1
                pos[Array[i]].append(i)

                # If it is the end of sequence
                if (Array[i] == 4) :
                    end = i
                    start = i

                    # Iterate for other elements of the sequence
                    for j in range(3,-1,-1):
                        s = 0
                        e = len(pos[j]) - 1
                        temp = -1

                        # Binary Search to find closest occurrence
                        # less than equal to starting point
                        while (s <= e):
                            m = (s + e) // 2
                            if (pos[j][m] <= start) :
                                temp = pos[j][m]
                                s = m + 1

                            else :
                                e = m - 1

                        # Update the starting point
                        start = temp

                    ans = min(ans, end - start + 1)

    return ans

# Driver code

Array = [ 0, 1, 2, 3, 4, 2, 0, 3, 4]
N = len(Array)

print(solve(Array, N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
static int MAX_INT = 1000000;

// Function to return the minimum length
// of a sub-array which contains
// {0, 1, 2, 3, 4} as a sub-sequence
static int solve(int[] array, int N)
{

    // To store the indices where 0, 1, 2,
    // 3 and 4 are present
    int[,] pos = new int[5,10000];

    // To store if there exist a valid prefix
    // of sequence in array
    int[] pref = new int[5];

    // Base Case
    if (array[0] == 0)
    {
        pref[0] = 1;
        pos[0,pos.GetLength(0)- 1] = 0;
    }

    int ans = MAX_INT;

    for (int i = 1; i < N; i++)
    {

        // If current element is 0
        if (array[i] == 0)
        {

            // Update the count of 0s till now
            pref[0]++;

            // Push the index of the new 0
            pos[0,pos.GetLength(0) - 1] = i;
        }

        else
        {

            // To check if previous element of the
            // given sequence is found till now
            if (pref[array[i] - 1] > 0)
            {
                pref[array[i]]++;
                pos[array[i],pos.GetLength(1) - 1] = i;

                // If it is the end of sequence
                if (array[i] == 4)
                {
                    int end = i;
                    int start = i;

                    // Iterate for other elements of the sequence
                    for (int j = 3; j >= 0; j--)
                    {
                        int s = 0;
                        int e = pos.GetLength(1) - 1;
                        int temp = -1;

                        // Binary Search to find closest occurrence
                        // less than equal to starting point
                        while (s <= e)
                        {
                            int m = (s + e) / 2;
                            if (pos[j,m] <= start)
                            {
                                temp = pos[j,m];
                                s = m + 1;
                            }
                            else
                                e = m - 1;
                        }

                        // Update the starting point
                        start = temp;
                    }
                    ans = Math.Min(ans, end - start + 1);
                }
            }
        }
    }
    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    int[] array = { 0, 1, 2, 3, 4, 2, 0, 3, 4 };
    int N = array.Length;

    Console.WriteLine(solve(array, N));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

let MAX_INT = 1000000;

// Function to return the minimum length
// of a sub-array which contains
// {0, 1, 2, 3, 4} as a sub-sequence
function solve(array,N)
{
    // To store the indices where 0, 1, 2,
    // 3 and 4 are present
    let pos = new Array(5);
    for(let i=0;i<5;i++)
    {
        pos[i]=new Array(10000);
        for(let j=0;j<10000;j++)
        {
            pos[i][j]=0;
        }
    }

    // To store if there exist a valid prefix
    // of sequence in array
    let pref = new Array(5);
      for(let i=0;i<5;i++)
    {
        pref[i]=0;
    }

    // Base Case
    if (array[0] == 0)
    {
        pref[0] = 1;
        pos[0][pos[0].length - 1] = 0;
    }

    let ans = MAX_INT;

    for (let i = 1; i < N; i++)
    {

        // If current element is 0
        if (array[i] == 0)
        {

            // Update the count of 0s till now
            pref[0]++;

            // Push the index of the new 0
            pos[0][pos[0].length - 1] = i;
        }

        else
        {

            // To check if previous element of the
            // given sequence is found till now
            if (pref[array[i] - 1] > 0)
            {
                pref[array[i]]++;
                pos[array[i]][pos[array[i]].length - 1] = i;

                // If it is the end of sequence
                if (array[i] == 4)
                {
                    let end = i;
                    let start = i;

                    // Iterate for other elements of the sequence
                    for (let j = 3; j >= 0; j--)
                    {
                        let s = 0;
                        let e = pos[j].length - 1;
                        let temp = -1;

                        // Binary Search to find closest occurrence
                        // less than equal to starting point
                        while (s <= e)
                        {
                            let m = Math.floor((s + e) / 2);
                            if (pos[j][m] <= start)
                            {
                                temp = pos[j][m];
                                s = m + 1;
                            }
                            else
                                e = m - 1;
                        }

                        // Update the starting point
                        start = temp;
                    }
                    ans = Math.min(ans, end - start + 1);
                }
            }
        }
    }
    return ans;
}

// Driver Code
let array=[0, 1, 2, 3, 4, 2, 0, 3, 4];
let N = array.length;
document.write(solve(array, N));

// This code is contributed by patel2127
</script>
```

**Output:** 

```
5
```