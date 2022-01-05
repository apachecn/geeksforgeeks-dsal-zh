# 将第 I 个索引处的元素向右移动 I 步，对作为数组给出的数字行进行排序

> 原文:[https://www . geeksforgeeks . org/sort-number-line-给定为数组-通过向右移动 I 步索引一个元素/](https://www.geeksforgeeks.org/sort-number-line-given-as-array-by-moving-an-element-at-ith-index-by-i-steps-to-right/)

给定一个由 **N 个**整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是通过在单次移动中将位于 **i <sup>th</sup>** 索引处的元素向右移动 **i** 步，找到[按升序](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)排列数组所需的最小移动次数。

> **注意:**在一个步骤中，两个数字可以位于同一位置。

**示例:**

> ***输入:** N = 4，arr[] = {1，2，7，4}*
> ***输出:** 1*
> ***解释:**将索引 3 处的元素向右移动 2 步，在 1 次移动中按升序对数组进行排序。因此，打印 1。*
> 
> ***输入:** N = 5，arr[] = {2，5，8，1，9}*
> ***输出:** 12*
> ***解释:***
> *排列数组的最佳方式是:arr[] = {-，-，-，-，1，-，-，-，2，-，-，-，-，-，-，-，5，-，-，-，-，-，-，-，-*
> 
> 1.  *首先 arr[0]跳转到索引 2，然后跳转到索引 4，然后跳转到索引 7。因此，移动 arr[0]将需要 3 次移动才能到达索引 7。*
> 2.  *首先 arr[1]跳到索引 3，然后跳到索引 7，然后跳到索引 15。因此，移动 arr[1]将需要 3 次移动才能到达索引 15。*
> 3.  *首先 arr[2]跳到索引 6，然后跳到索引 12，然后跳到索引 24。因此，移动 arr[2]将需要 3 次移动才能到达索引 23。*
> 4.  *首先 arr[4]跳到索引 9，然后跳到索引 19，然后跳到索引 39。因此，移动 arr[4]也需要 3 次移动才能到达索引 39。*
> 
> *所以总共需要(3 + 3 + 3 + 3) = 12 招。*

**方法:**给定的问题可以通过使用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)来解决，该方法基于这样的观察，即首先将最小的数放置在其适当的位置，然后相应地放置较大的元素总是最优的。按照以下步骤解决问题:

*   初始化一个[图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)比如 **M** ，该图将数组元素及其索引存储在给定的数组 **arr[]** 中。
*   [使用变量 **i** 遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，并将地图**M【arr[I]】**更新为**M【arr[I]】=(I+1)**。
*   初始化一个变量，比如说**和**为 **0** ，它存储了所需的最小总移动次数。
*   [遍历地图](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/) **M** ，执行以下步骤:
    *   将当前迭代器和前一个迭代器的位置存储在变量中，比如 **i** 和 **j** 。
    *   迭代直到 **i- >秒**小于或等于 **j- >秒**并将 **ans** 的值增加 **1** 并将 **i- >秒**的值增加 **i- >秒**。
*   完成上述步骤后，打印作为最小移动结果的**和**的值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number
// of moves required to sort the numbers
int MinimumMoves(int arr[], int N)
{
    // Stores value of number and the
    // position of the number
    map<int, int> mp;

    for (int i = 0; i < N; i++) {

        // Update mp[arr[i]]
        mp[arr[i]] = (i + 1);
    }

    // Stores the iterator pointing at
      // the beginning of the map
    auto it = mp.begin();
    it++;

    // Stores the minimum count of moves
    int ans = 0;

    // Traverse the map mp
    for (auto i = it; i != mp.end(); i++) {

        // Stores previous iterator
        auto j = i;
        j--;

        // Iterate while i->second is less
          // than or equal to j->second
        while (i->second <= j->second) {

            // Update the i->second
            i->second += i->second;

            // Increment ans by 1
            ans++;
        }
    }

    // Return the resultant minimum moves
    return ans;
}

// Driver Code
int main()
{
    int arr[] = { 2, 5, 8, 1, 9 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << MinimumMoves(arr, N);

      return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG {

    // Function to find the minimum number
    // of moves required to sort the numbers
    static int MinimumMoves(int arr[], int N)
    {

        // Stores value of number and the
        // position of the number
        Map<Integer, Integer> mp
            = new HashMap<Integer, Integer>();

        for (int i = 0; i < N; i++) {

            // Update mp[arr[i]]
            if (mp.containsKey(arr[i])) {

                mp.put(arr[i], mp.get(arr[i]) + (i + 1));
            }
            else {

                mp.put(arr[i], (i + 1));
            }
        }

        // Stores the iterator pointing at
        // the beginning of the map
        Iterator<Map.Entry<Integer, Integer> > it
            = mp.entrySet().iterator();

        Map.Entry<Integer, Integer> i = it.next();

        // Stores the minimum count of moves
        int ans = 0;

        // Traverse the map mp
        while (it.hasNext()) {

            // Stores previous iterator
            Map.Entry<Integer, Integer> j = i;
            i = it.next();

            // Iterate while i->second is less
            // than or equal to j->second
            while (i.getValue() <= j.getValue()) {

                // Update the i->second
                i.setValue(i.getValue() + i.getValue());

                // Increment ans by 1
                ans++;
            }
        }

        // Return the resultant minimum moves
        return ans;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 2, 5, 8, 1, 9 };
        int N = arr.length;
        System.out.println(MinimumMoves(arr, N));
    }
}

// This code is contributed by Dharanendra L V.
```

**Output**

```
12
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*