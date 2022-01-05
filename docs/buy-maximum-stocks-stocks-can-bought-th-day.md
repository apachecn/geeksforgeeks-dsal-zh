# 如果我的股票可以在第一天买入

买入最大股票

> 原文:[https://www . geesforgeks . org/buy-max-stocks-stocks-can-buy-th-day/](https://www.geeksforgeeks.org/buy-maximum-stocks-stocks-can-bought-th-day/)

在股票市场上，有一种产品的股票是无限的。股票价格是在第 **N** 天给出的，其中 arr【I】表示股票在第<sup>天的价格。有一条规定，客户最多只能在 i <sup>日</sup>购买 I 股票。如果客户最初有一笔 **k** 金额，找出客户可以购买的最大股票数量。</sup>

例如，对于 3 天，股票的价格是 7，10，4。你可以在第一天买 1 只价值 7 卢比的股票，在第二天买 2 只价值 10 卢比的股票，在第三天买 3 只价值 4 卢比的股票。

示例:

```
Input : price[] = { 10, 7, 19 }, 
              k = 45.
Output : 4
A customer purchases 1 stock on day 1, 
2 stocks on day 2 and 1 stock on day 3 for 
10, 7 * 2 = 14 and 19 respectively. Hence, 
total amount is 10 + 14 + 19 = 43 and number 
of stocks purchased is 4.

Input  : price[] = { 7, 10, 4 }, 
               k = 100.
Output : 6
```

这个想法是用贪婪的方法，我们应该从股价最低的那一天开始购买产品，以此类推。
所以，我们将根据股价对两个值即{股价、日}对进行排序，如果股价相同，那么我们就根据日进行排序。
现在，我们将遍历排序后的配对列表，开始购买如下:
假设我们到目前为止还有 R rs，并且这一天的产品成本是 C，那么我们可以在这一天购买 atmost L 产品，
这一天的总购买量(P) = min(L，R/C)
现在，将这个值添加到答案中。
当天总购买量(P) = min(L，R/C)
现在，把这个值加到答案
total_purchase = Total _ purchase+P，其中 P =min(L，R/C)
现在，用剩余的钱减去购买 P 个物品的成本，R = R–P * C .
我们能购买的产品总数等于 Total _ purchase。

下面是该方法的实现:

## C++

```
// C++ program to find maximum number of stocks that
// can be bought with given constraints.
#include <bits/stdc++.h>
using namespace std;

// Return the maximum stocks
int buyMaximumProducts(int n, int k, int price[])
{
    vector<pair<int, int> > v;

    // Making pair of product cost and number
    // of day..
    for (int i = 0; i < n; ++i)
        v.push_back(make_pair(price[i], i + 1));   

    // Sorting the vector pair.
    sort(v.begin(), v.end());   

    // Calculating the maximum number of stock
    // count.
    int ans = 0;
    for (int i = 0; i < n; ++i) {
        ans += min(v[i].second, k / v[i].first);
        k -= v[i].first * min(v[i].second,
                               (k / v[i].first));
    }

    return ans;
}

// Driven Program
int main()
{
    int price[] = { 10, 7, 19 };
    int n = sizeof(price)/sizeof(price[0]);
    int k = 45;

    cout << buyMaximumProducts(n, k, price) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum number of stocks that
// can be bought with given constraints.
import java.util.*;

// Helper class
class Pair {
    int first, second;
    Pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// For Sorting using Pair.first value
class SortPair implements Comparator<Pair> {
    public int compare(Pair a, Pair b)
    {
        return a.first - b.first;
    }
}

public class GFG {

    // Return the maximum stocks
    static int buyMaximumProducts(int[] price, int K, int n)
    {
        Pair[] arr = new Pair[n];

        // Making pair of product cost and number of day..
        for (int i = 0; i < n; i++)
            arr[i] = new Pair(price[i], i + 1);

        // Sorting the pair array.
        Arrays.sort(arr, new SortPair());
        // Calculating the maximum number of stock
        // count.
        int ans = 0;
        for (int i = 0; i < n; i++) {
            ans += Math.min(arr[i].second,
                            K / arr[i].first);
            K -= arr[i].first
                 * Math.min(arr[i].second,
                            K / arr[i].first);
        }
        return ans;
    }

  // Driver code
    public static void main(String[] args)
    {
        int[] price = { 10, 7, 19 };
        int K = 45;

        // int []price = { 7, 10, 4 };
        // int K = 100;
        System.out.println(
            buyMaximumProducts(price, K, price.length));
    }
}

// This code is contributed by Aakash Choudhary
```

## 蟒蛇 3

```
# Python3 program to find maximum number of stocks
# that can be bought with given constraints.

# Returns the maximum stocks
def buyMaximumProducts(n, k, price):

    # Making pair of stock cost and day number
    arr = []

    for i in range(n):
        arr.append([i + 1, price[i]])

    # Sort based on the price of stock
    arr.sort(key = lambda x: x[1])

    # Calculating the max stocks purchased
    total_purchase = 0
    for i in range(n):
        P = min(arr[i][0], k//arr[i][1])
        total_purchase += P
        k -= (P * arr[i][1])

    return total_purchase

# Driver code
price = [ 10, 7, 19 ]
n = len(price)
k = 45

print(buyMaximumProducts(n, k, price))

# This code is contributed by Tharun Reddy
```

**输出:**

```
4
```

**时间复杂度:** O(nlogn)。

本文由 **Anuj Chauhan** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。