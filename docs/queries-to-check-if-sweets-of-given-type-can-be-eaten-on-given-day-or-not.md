# 查询给定类型的糖果在给定的一天是否可以吃

> 原文:[https://www . geeksforgeeks . org/query-to-check-如果给定日期可以吃或不可以吃给定类型的糖果/](https://www.geeksforgeeks.org/queries-to-check-if-sweets-of-given-type-can-be-eaten-on-given-day-or-not/)

给定两个由 **N** 整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**A【】**和**B【】**，其中**A<sub>I</sub>T11】表示 i <sup>第</sup>类型的甜食数量，**B<sub>I</sub>T17】表示 **i <sup>第</sup>T21】甜食的优先级(*值越高优先级越大【T22 优先级较低的甜食不能在优先级较高的甜食之前吃，一天只能吃一种类型的甜食。给定一个表示形式为 **{Q[i][0]、Q[i][1] }** 的查询的数组 **Q[][]** ，每个查询的任务是找出在第天 **Q[i][1]** <sup>是否可以吃到类型为 **Q[i][0]** 的甜味。如有可能，打印“**是**”。否则，打印“**否**”。</sup>*******

**示例:**

> **输入:** A[] = { 6，3，7，5，2 }，B[] = { 1，2，3，4，5 }，K = 3，Q[][] = { {4，4}，{3，16}，{2，7} }
> **输出:**是否是
> **解释:**
> 查询 1:按以下顺序吃甜食，第四天可以吃第四种类型的甜食。
> 第 1 天:第 5 类- > 2 个单位
> 第 2 天:第 4 类- > 2 个单位
> 第 3 天:第 4 类- > 2 个单位
> 第 4 天:第 4 类- > 1 个单位
> 查询 2:第 5、4、3 类甜食合计= 2 + 5 + 7 = 14。因此，即使每天吃一颗糖，也不会在第 16 天留下任何 3 型糖。
> 查询 3:按以下顺序吃甜食，第 7 天可以吃第 2 类甜食。
> 第 1 天:5 型- > 2 台。
> 第 2 天:4 型- > 3 个单位。
> 第 3 天:4 型- > 2 台。
> 第 4 天:3 型- > 3 个单位。
> 第 5 天:3 型- > 2 台。
> 第 6 天:3 型- > 2 台。
> 第 7 天:2 型->2 台。
> 
> **输入:** A[] = { 5，2，6，4，1 }，B[] = { 2，1，3，5，4 }，K = 4，Q[][] = { {2，17}，{ 5，6} }
> **输出:**是否

**方法:**解决这个问题的思路是为每一种甜型维持一个窗口。该窗口将基本包含天数的[下限](https://www.geeksforgeeks.org/lower_bound-in-cpp/)和[上限](https://www.geeksforgeeks.org/upper_bound-in-cpp/)，在此范围内，可以使用以下条件食用该类型的甜食:

*   对于窗口的**下限，考虑完成所有优先级较高的甜食所需的最少天数，即从每天的一种甜食中减去**最小值(K，剩余量)**。**
*   对于窗口的**上限，考虑完成所有高优先级糖果的最大天数，即所有高优先级糖果总数的总和。**

为每种类型准备好窗口后，只需检查每个查询给定的日期是否在窗口内。按照以下步骤解决问题:

步骤:

*   维护一个容器，说出一个[对](https://www.geeksforgeeks.org/pair-in-cpp-stl/) **v** 的[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)来存储每个甜味类型的**优先级**和**数量**。
*   [按照优先级递减的顺序对向量对进行排序](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-2-sort-in-descending-order-by-first-and-second/)。
*   初始化两个变量，比如**下限**和**上限**，来存储每个甜味类型的窗口限制。
*   [遍历向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **v** ，执行以下步骤:
    *   计算第 i <sup>个</sup>类型的吃甜食所需的最大和最小天数为**最大天数= A【I】**和**最小天数=上限(A【I】/K)。**
    *   更新**上限+=最大天数**。
    *   存储当前甜型的窗口 **{ lowerbound，upperbound}** 。
    *   更新**下限+= min_days** 。
*   一旦完成以上步骤，遍历数组 **Q[][]** ，对于每个查询，检查给定甜蜜类型的给定日期是否落在该甜蜜类型的窗口 **{ lowerbound，upperbound}** 内。如果发现是真的，打印**“是”**。否则，打印**“否”**。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find queries to check
// if a sweet of given type can be
// eaten on a given day or not
void sweetTypeOnGivenDay(int a[], int b[],
                         int n, int k,
                         vector<pair<int, int> >& q)
{
    // Stores pairs {priority, quantity}
    // of each sweet-type
    vector<pair<int, pair<int, int> > > v;
    for (int i = 0; i < n; i++)
        v.push_back({ b[i], { a[i], i + 1 } });

    // Sorting the order of sweets in
    // decreasing order of their priority
    sort(v.begin(), v.end(),
         greater<pair<int, pair<int, int> > >());

    // Stores the window {min_days, max_days}
    // for each sweet-type
    map<int, pair<int, int> > mp;

    // Variables to calculate the windows
    int lowerbound = 0, upperbound = 0;

    // Traverse the array
    for (int i = 0; i < n; i++) {

        // Calculating maximum and minimum
        // number of days required to complete
        // the sweets of the current type
        int maxi_days = v[i].second.first;
        int mini_days = v[i].second.first / k;

        if (v[i].second.first % k != 0)
            mini_days++;

        // Creating the window and storing it
        upperbound += maxi_days;
        mp[v[i].second.second]
            = { lowerbound, upperbound };

        lowerbound += mini_days;
    }

    // Traversing the queries
    for (int i = 0; i < q.size(); i++) {

        // x: Type of sweet, y: Day
        int x = q[i].first, y = q[i].second;

        // Find the window for the
        // sweet of type x
        int e = mp[x].first;
        int f = mp[x].second;

        // If the given day lies
        // within the window
        if (y >= e && y <= f)
            cout << "Yes"
                 << " ";
        else
            cout << "No"
                 << " ";
    }
}

// Driver Code
int main()
{
    // Quantites of sweets of each type
    int A[] = { 6, 3, 7, 5, 2 };

    // Priorites of each type sweet
    int B[] = { 1, 2, 3, 4, 5 };

    // Maximum sweet of one type
    // that can be eaten on a day
    int K = 3;

    // Queries
    vector<pair<int, int> > Queries
        = { { 4, 4 }, { 3, 16 }, { 2, 7 } };

    // Calculating number of types
    int n = sizeof(A) / sizeof(A[0]);

    sweetTypeOnGivenDay(A, B, n, K, Queries);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.ArrayList;
import java.util.Arrays;
import java.util.Collections;
import java.util.Comparator;
import java.util.HashMap;
import java.util.Map;
class GFG
{
    static class Pair<K, V>
    {
        K first;
        V second;
        public Pair(K first, V second)
        {
            this.first = first;
            this.second = second;
        }
        public static <K, V> Pair<K, V> of(K first, V second)
        {
            return new Pair<>(first, second);
        }
    }

    // Function to find queries to check
    // if a sweet of given type can be
    // eaten on a given day or not
    static void sweetTypeOnGivenDay(int a[], int b[],
                                    int n, int k,
                                    ArrayList<Pair<Integer, Integer>> q)
    {

        // Stores pairs {priority, quantity}
        // of each sweet-type
        ArrayList<Pair<Integer, Pair<Integer, Integer>>> v = new ArrayList<>();
        for (int i = 0; i < n; i++)
            v.add(Pair.of(b[i], Pair.of(a[i], i + 1)));

        // Sorting the order of sweets in
        // decreasing order of their priority
        Collections.sort(v, new Comparator<Pair<Integer, Pair<Integer, Integer>>>() {
            @Override
            public int compare(Pair<Integer, Pair<Integer, Integer>> a, Pair<Integer, Pair<Integer, Integer>> b) {
                if (a.first == b.first) {
                    if (a.second.first == b.second.first) {
                        return b.second.second - a.second.second;
                    }
                    return b.second.first - a.second.first;
                }
                return b.first - a.first;
            }
        });

        // Stores the window {min_days, max_days}
        // for each sweet-type
        Map<Integer, Pair<Integer, Integer>> mp = new HashMap<>();

        // Variables to calculate the windows
        int lowerbound = 0, upperbound = 0;

        // Traverse the array
        for (int i = 0; i < n; i++) {

            // Calculating maximum and minimum
            // number of days required to complete
            // the sweets of the current type
            int maxi_days = v.get(i).second.first;
            int mini_days = v.get(i).second.first / k;

            if (v.get(i).second.first % k != 0)
                mini_days++;

            // Creating the window and storing it
            upperbound += maxi_days;
            mp.put(v.get(i).second.second, Pair.of(lowerbound, upperbound));
            lowerbound += mini_days;
        }

        // Traversing the queries
        for (int i = 0; i < q.size(); i++)
        {

            // x: Type of sweet, y: Day
            int x = q.get(i).first, y = q.get(i).second;

            // Find the window for the
            // sweet of type x
            int e = mp.get(x).first;
            int f = mp.get(x).second;

            // If the given day lies
            // within the window
            if (y >= e && y <= f)
                System.out.println("Yes ");
            else
                System.out.println("No ");
        }
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Quantites of sweets of each type
        int A[] = { 6, 3, 7, 5, 2 };

        // Priorites of each type sweet
        int B[] = { 1, 2, 3, 4, 5 };

        // Maximum sweet of one type
        // that can be eaten on a day
        int K = 3;

        // Queries
        ArrayList<Pair<Integer, Integer>> Queries = new ArrayList<>(
                Arrays.asList(Pair.of(4, 4), Pair.of(3, 16), Pair.of(2, 7)));

        // Calculating number of types
        int n = A.length;
        sweetTypeOnGivenDay(A, B, n, K, Queries);
    }
}

    // This code is contributed by sanjeev2552
```

**Output:** 

```
Yes No Yes
```

***时间复杂度:** O(N logN)*
***辅助空间:** O(N)*