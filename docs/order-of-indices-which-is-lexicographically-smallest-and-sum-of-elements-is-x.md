# 从词汇学上来说最小的索引顺序和元素的总和是< = X

> 原文:[https://www . geeksforgeeks . org/indexes-of-is-x/](https://www.geeksforgeeks.org/order-of-indices-which-is-lexicographically-smallest-and-sum-of-elements-is-x/)

给定一个数组 **arr[]** 和一个整数 **X** ，任务是找到这样的索引:

1.  找到的指数上的元素之和≤ X
2.  索引的数量是可能的最大值。
3.  索引的顺序在字典上是最小的，即{0，0，1}在字典上小于{1，0，0}

**注意**任何指标都可以选择多次。
**例:**

> **输入:** arr[] = {6，8，5，4，7}，X = 11
> **输出:** 0 2
> 最佳答案是[0，2]，因为它在字典上是最小的。
> 所选指数 A[0] + A[2] = 6 + 5 = 11 之和≤ 11。
> 这里，【2，3】、【2，2】或【3，3】也给出了最大
> 数量的所选索引，但它们在词典学上不是最小的。
> **输入:** arr[] = {9，6，8，5，7，4}，X = 35
> **输出:**1 3 5 5 5 5 5 5 5

**方法:**这个问题看起来像是[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)的变种，但事实证明可以通过简单的贪婪算法来解决。
设第一个最小值的指数为 m，那么所做指数的最大值为 n = X / A[m]。所以 ans = [m，m，m，…，m]，其中 m 的个数为 n，是选择的最大指数个数的阶，总和= n×A[m]。我们也确定最优答案中有 n 个值，并且不超过这个值。
现在，我们可以用相同数量的选择索引获得一个字典序更小的顺序，如果我们可以找到一个小于 m 的索引 I，这样我们可以用一个值为 A[i]的索引代替值为 A[m]的索引，而不超过 X 的和，那么我们可以用 I 代替 ans 中的第一个元素，使顺序字典序更小。为了使它在词典上尽可能小，我们希望索引 I 尽可能小，然后，我们希望尽可能多地使用它。

> 例如，X = 11，A = [6，8，5，4，7]。
> 最小值在指数 3，A[3] = 4。所以 n = 11 / 4 = 2，ans = [3，3]，总和= 4 x 2 = 8。
> 为了使其在字典上更小，我们将按顺序检查 3 之前的索引。
> 第一个是 6。自 8–4+6 = 10<11。我们找到了一个较小的顺序[0，3]。
> 如果我们再次应用 6，我们将得到 10–4+6 = 12>11。所以我们继续检查下一个索引值 8，它太大了。所以我们继续检查 5。由于 10–4+5 = 11<= 11，我们找到一个较小的顺序[0，2]。由于没有剩余的替换空间，11–11 = 0，我们到此为止。最终答案是[0，2]。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the chosen indices
vector<int> solve(int X, vector<int>& A)
{
    int min = INT_MAX;
    int ind = -1;

    for (int i = 0; i < A.size(); i++) {
        if (A[i] < min) {
            min = A[i];
            ind = i;
        }
    }

    // Maximum indices chosen
    int maxIndChosen = X / min;

    vector<int> ans;

    if (maxIndChosen == 0) {
        return ans;
    }

    for (int i = 0; i < maxIndChosen; i++) {
        ans.push_back(ind);
    }

    int temp = maxIndChosen;
    int sum = maxIndChosen * A[ind];

    // Try to replace the first element in ans by i,
    // making the order lexicographically smaller
    for (int i = 0; i < ind; i++) {

        // If no further replacement possible return
        if (sum - X == 0 || temp == 0)
            break;

        // If found an index smaller than ind and sum
        // not exceeding X then remove index of smallest
        // value from ans and then add index i to ans
        while ((sum - A[ind] + A[i]) <= X && temp != 0) {
            ans.erase(ans.begin());
            ans.push_back(i);
            temp--;
            sum += (A[i] - A[ind]);
        }
    }

    sort(ans.begin(), ans.end());

    return ans;
}

// Driver code
int main()
{
    vector<int> A = { 5, 6, 4, 8 };
    int X = 18;

    vector<int> ans = solve(X, A);

    // Print the chosen indices
    for (int i = 0; i < ans.size(); i++)
        cout << ans[i] << " ";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the chosen indices
static Vector<Integer> solve(int X, Vector<Integer> A)
{
    int min = Integer.MAX_VALUE;
    int ind = -1;

    for (int i = 0; i < A.size(); i++)
    {
        if (A.get(i) < min)
        {
            min = A.get(i);
            ind = i;
        }
    }

    // Maximum indices chosen
    int maxIndChosen = X / min;

    Vector<Integer> ans = new Vector<>();

    if (maxIndChosen == 0)
    {
        return ans;
    }

    for (int i = 0; i < maxIndChosen; i++)
    {
        ans.add(ind);
    }

    int temp = maxIndChosen;
    int sum = maxIndChosen * A.get(ind);

    // Try to replace the first element in ans by i,
    // making the order lexicographically smaller
    for (int i = 0; i < ind; i++) {

        // If no further replacement possible return
        if (sum - X == 0 || temp == 0)
            break;

        // If found an index smaller than ind and sum
        // not exceeding X then remove index of smallest
        // value from ans and then add index i to ans
        while ((sum - A.get(ind) + A.get(i)) <= X && temp != 0)
        {
            ans.remove(0);
            ans.add(i);
            temp--;
            sum += (A.get(i) - A.get(ind));
        }
    }

    Collections.sort(ans);

    return ans;
}

// Driver code
public static void main(String args[])
{
    Integer arr[] = { 5, 6, 4, 8 };
    Vector<Integer> A = new Vector<Integer>(Arrays.asList(arr));
    int X = 18;

    Vector<Integer> ans = solve(X, A);

    // Print the chosen indices
    for (int i = 0; i < ans.size(); i++)
        System.out.print(ans.get(i)+" ");
}
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import sys;

# Function to return the chosen indices
def solve(X, A) :

    minimum = sys.maxsize;
    ind = -1;

    for i in range(len(A)) :
        if (A[i] < minimum ) :
            minimum = A[i];
            ind = i;

    # Maximum indices chosen
    maxIndChosen = X // minimum ;

    ans = [];

    if (maxIndChosen == 0) :
        return ans;

    for i in range(maxIndChosen) :
        ans.append(ind);

    temp = maxIndChosen;
    sum = maxIndChosen * A[ind];

    # Try to replace the first element in ans by i,
    # making the order lexicographically smaller
    for i in range(ind) :

        # If no further replacement possible return
        if (sum - X == 0 or temp == 0) :
            break;

        # If found an index smaller than ind and sum
        # not exceeding X then remove index of smallest
        # value from ans and then add index i to ans
        while ((sum - A[ind] + A[i]) <= X and temp != 0) :
            del(ans[0]);
            ans.append(i);
            temp -= 1;
            sum += (A[i] - A[ind]);

    ans.sort();
    return ans;

# Driver code
if __name__ == "__main__" :

    A = [ 5, 6, 4, 8 ];
    X = 18;

    ans = solve(X, A);

    # Print the chosen indices
    for i in range(len(ans)) :
        print(ans[i],end= " ");

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to return the chosen indices
static List<int> solve(int X, List<int> A)
{
    int min = int.MaxValue;
    int ind = -1;

    for (int i = 0; i < A.Count; i++)
    {
        if (A[i] < min)
        {
            min = A[i];
            ind = i;
        }
    }

    // Maximum indices chosen
    int maxIndChosen = X / min;

    List<int> ans = new List<int>();

    if (maxIndChosen == 0)
    {
        return ans;
    }

    for (int i = 0; i < maxIndChosen; i++)
    {
        ans.Add(ind);
    }

    int temp = maxIndChosen;
    int sum = maxIndChosen * A[ind];

    // Try to replace the first element in ans by i,
    // making the order lexicographically smaller
    for (int i = 0; i < ind; i++)
    {

        // If no further replacement possible return
        if (sum - X == 0 || temp == 0)
            break;

        // If found an index smaller than ind and sum
        // not exceeding X then remove index of smallest
        // value from ans and then add index i to ans
        while ((sum - A[ind] + A[i]) <= X && temp != 0)
        {
            ans.RemoveAt(0);
            ans.Add(i);
            temp--;
            sum += (A[i] - A[ind]);
        }
    }

    ans.Sort();

    return ans;
}

// Driver code
public static void Main(String []args)
{
    int []arr = { 5, 6, 4, 8 };
    List<int> A = new List<int>(arr);
    int X = 18;

    List<int> ans = solve(X, A);

    // Print the chosen indices
    for (int i = 0; i < ans.Count; i++)
        Console.Write(ans[i] + " ");
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the chosen indices
function solve(X,A)
{
    let min = Number.MAX_VALUE;
    let ind = -1;

    for (let i = 0; i < A.length; i++)
    {
        if (A[i] < min)
        {
            min = A[i];
            ind = i;
        }
    }

    // Maximum indices chosen
    let maxIndChosen = Math.floor(X / min);

    let ans = [];

    if (maxIndChosen == 0)
    {
        return ans;
    }

    for (let i = 0; i < maxIndChosen; i++)
    {
        ans.push(ind);
    }

    let temp = maxIndChosen;
    let sum = maxIndChosen * A[ind];

    // Try to replace the first element in ans by i,
    // making the order lexicographically smaller
    for (let i = 0; i < ind; i++) {

        // If no further replacement possible return
        if (sum - X == 0 || temp == 0)
            break;

        // If found an index smaller than ind and sum
        // not exceeding X then remove index of smallest
        // value from ans and then add index i to ans
        while ((sum - A[ind] + A[i]) <= X && temp != 0)
        {
            ans.shift();
            ans.push(i);
            temp--;
            sum += (A[i] - A[ind]);
        }
    }

    ans.sort(function(a,b){return a-b;});

    return ans;
}

// Driver code
let A = [5, 6, 4, 8];
let X = 18;
let ans = solve(X, A);

// Print the chosen indices
for (let i = 0; i < ans.length; i++)
    document.write(ans[i]+" ");

// This code is contributed by rag2127
</script>
```

**Output:** 

```
0 0 2 2
```

**时间复杂度:** O(NLog(N))