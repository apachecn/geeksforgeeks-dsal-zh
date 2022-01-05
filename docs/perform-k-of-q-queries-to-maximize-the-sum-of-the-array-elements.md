# 执行 K 对 Q 的查询，最大化数组元素的总和

> 原文:[https://www . geesforgeks . org/perform-k-of-q-query-to-max-the-sum-the-array-elements/](https://www.geeksforgeeks.org/perform-k-of-q-queries-to-maximize-the-sum-of-the-array-elements/)

给定一个由 **N** 个整数和一个整数 **K** 组成的数组 **arr[]** 。还给出了 **Q** 查询，有两个数字 **L** 和 **R** 。对于每个查询，可以通过 **1** 增加索引范围**【L，R】**中数组的所有元素。任务是从 Q 个查询中准确选择 **K 个**查询，使得末端数组的和最大化。执行 **K** 这样的查询后，打印**和**。

**示例:**

> **输入:** arr[] = {1，1，2，2，2，3}，
> que[] = {{0，4}，{1，2}，{2，5}，{2，3}，{2，4}}，
> K = 3
> T5】输出: 23
> 我们选择第一个、第三个和第五个查询。
> 执行第一次查询后- > arr[] = {2，2，3，3，3，3}
> 执行第三次查询后- > arr[] = {2，2，4，4，4，4，4，4}，
> 执行第五次查询后- > arr[] = {2，2，5，5，5，4}
> 数组和为 2 + 2 + 5 + 5 + 5 + 4 = 23。
> 
> **输入:** arr[] = {4，5，4，21，22}，
> 比[] = {{1，2}，{2，2}，{2，4}，{2，2}}，
> K = 2
> **输出:** 61

**幼稚法:**幼稚法是用动态规划和组合学，从 q 中选择任意 K 个查询，给出数组最大和的组合就是答案。

**时间复杂度** : O(N*N*K)

**高效方法:**因为我们需要最大化数组末尾的和。我们只需要选择那些影响数组中最大元素数量的查询，即范围更大的查询。如果选择了**(R–L+1)**，每个查询都会增加总和。执行此类查询后的数组元素之和将是**(数组的初始和+(K 个查询的贡献))**。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to perform K queries out
// of Q to maximize the final sum
int getFinalSum(int a[], int n, pair<int, int> queries[],
                int q, int k)
{
    int answer = 0;

    // Get the initial sum
    // of the array
    for (int i = 0; i < n; i++)
        answer += a[i];

    vector<int> contribution;

    // Stores the contriution of every query
    for (int i = 0; i < q; i++) {
        contribution.push_back(queries[i].second
                               - queries[i].first + 1);
    }

    // Sort the contribution of queries
    // in descending order
    sort(contribution.begin(), contribution.end(),
         greater<int>());

    int i = 0;

    // Get the K most contributions
    while (i < k) {
        answer += contribution[i];
        i++;
    }

    return answer;
}

// Driver code
int main()
{
    int a[] = { 1, 1, 2, 2, 2, 3 };
    int n = sizeof(a) / sizeof(a[0]);

    pair<int, int> queries[] = { { 0, 4 },
                                 { 1, 2 },
                                 { 2, 5 },
                                 { 2, 3 },
                                 { 2, 4 } };
    int q = sizeof(queries) / sizeof(queries[0]);

    int k = 3;

    cout << getFinalSum(a, n, queries, q, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

//pair class
static class pair
{
    int first,second;
    pair(int f,int s)
    {
        first = f;
        second = s;
    }
}

// Function to perform K queries out
// of Q to maximize the final sum
static int getFinalSum(int a[], int n, pair queries[],
                                    int q, int k)
{
    int answer = 0;

    // Get the initial sum
    // of the array
    for (int i = 0; i < n; i++)
        answer += a[i];

    Vector<Integer> contribution = new Vector<Integer>();

    // Stores the contriution of every query
    for (int i = 0; i < q; i++)
    {
        contribution.add(queries[i].second
                            - queries[i].first + 1);
    }

    //comparator
    Comparator<Integer> Comp = new Comparator<Integer>()
    {
            public int compare(Integer e1,Integer e2)
            {
                if(e1 > e2)
                return -1;
                else
                return 1;
            }
        };

    // Sort the contribution of queries
    // in descending order
    Collections.sort(contribution,Comp);

    int i = 0;

    // Get the K most contributions
    while (i < k)
    {
        answer += (int) contribution.get(i);
        i++;
    }

    return answer;
}

// Driver code
public static void main(String args[])
{
    int a[] = { 1, 1, 2, 2, 2, 3 };
    int n = a.length;

    pair queries[] = new pair[5];
    queries[0] = new pair( 0, 4 );
    queries[1] = new pair( 1, 2 );
    queries[2] = new pair( 2, 5 );
    queries[3] = new pair( 2, 3 );
    queries[4] = new pair( 2, 4 );
    int q = queries.length;

    int k = 3;
    System.out.println( getFinalSum(a, n, queries, q, k));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to perform K queries out
# of Q to maximize the final sum
def getFinalSum(a, n, queries, q, k):
    answer = 0

    # Get the initial sum
    # of the array
    for i in range(n):
        answer += a[i]

    contribution = []

    # Stores the contriution of every query
    for i in range(q):
        contribution.append(queries[i][1]-
                            queries[i][0] + 1)

    # Sort the contribution of queries
    # in descending order
    contribution.sort(reverse = True)

    i = 0

    # Get the K most contributions
    while (i < k):
        answer += contribution[i]
        i += 1

    return answer

# Driver code
if __name__ == '__main__':
    a = [1, 1, 2, 2, 2, 3]
    n = len(a)

    queries = [[0, 4], [1, 2],
               [2, 5], [2, 3],
               [2, 4]]
    q = len(queries);

    k = 3

    print(getFinalSum(a, n, queries, q, k))

# This code is contributed by
# Surendra_Gangwar
```

## java 描述语言

```
<script>
    // JavaScript implementation of the approach

    // Function to perform K queries out
    // of Q to maximize the final sum
    const getFinalSum = (a, n, queries, q, k) => {
        let answer = 0;

        // Get the initial sum
        // of the array
        for (let i = 0; i < n; i++)
            answer += a[i];

        let contribution = [];

        // Stores the contriution of every query
        for (let i = 0; i < q; i++) {
            contribution.push(queries[i][1] - queries[i][0] + 1);
        }

        // Sort the contribution of queries
        // in descending order
        contribution.sort((a, b) => b - a);

        let i = 0;

        // Get the K most contributions
        while (i < k) {
            answer += contribution[i];
            i++;
        }

        return answer;
    }

    // Driver code

    const a = [1, 1, 2, 2, 2, 3];
    const n = a.length;

    const queries = [
        [0, 4],
        [1, 2],
        [2, 5],
        [2, 3],
        [2, 4]
    ];
    const q = queries.length;

    let k = 3;

    document.write(getFinalSum(a, n, queries, q, k));

    // This code is contributed by rakeshsahni

</script>
```

**Output:** 

```
23
```