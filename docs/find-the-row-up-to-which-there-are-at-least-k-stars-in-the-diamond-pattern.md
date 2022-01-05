# 找出菱形图案中至少有 K 颗星的行

> 原文:[https://www . geeksforgeeks . org/find-the-row-up-to-the-at-the-at-k-star-in-the-diamond-pattern/](https://www.geeksforgeeks.org/find-the-row-up-to-which-there-are-at-least-k-stars-in-the-diamond-pattern/)

给定两个整数 **N** 和 **K** ，其中 N 代表一个带有( **2 * N) -1** 行的[菱形图案](https://www.geeksforgeeks.org/c-program-print-diamond-shape/)，任务是找到第一行的**索引**，直到在一个**菱形**图案中有至少 K 颗**星。**

请注意，K 的值永远会有一个确定的答案。

**示例**:

> **输入** : N = 3，K = 8
> **输出** : 4
> **说明**:前 4 行共包含 8 颗星。
> *
> 
> * *
> 
> * * *
> 
> * *
> 
> *
> **输入** : N = 5，K = 5
> **输出** : 3

**天真方法:**给定的问题可以通过简单地[迭代每行](https://www.geeksforgeeks.org/row-wise-vs-column-wise-traversal-matrix/)并保持每行星星数量的计数来解决。打印星星数超过 k 的前两个。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the index of
// required row
void get(int N, int K)
{
    // Stores the count of stars
    // till ith row
    int sum = 0, ans;

    // Iterating over the rows
    for (int i = 1; i <= 2 * N - 1; i++) {

        // Upper half
        if (i <= N) {
            sum += i;
        }

        // Lower half
        else {
            sum += 2 * N - i;
        }

        // Atleast K stars are found
        if (sum >= K) {
            ans = i;
            break;
        }
    }

    // Print Answer
    cout << ans << endl;
}

// Driver Code
int main()
{
    int N = 3, K = 8;
    get(N, K);
    return 0;
}
```

**Output**

```
4
```

***时间复杂度*****:**O(N)
***辅助空间*** **:** O(1)

**高效方法:**上述方法可以使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)对来自**【0，2 * n-1】**的行数值进行优化。按照以下步骤解决问题:

*   初始化变量**开始** = 0，**结束**=**(2 * N)–1**和， **ans** = 0。
*   当**开始**的值小于**T3**结束**的值时，请遵循以下步骤。**
    *   计算**中间**，等于**(开始+结束)/ 2**
    *   数星星的数量直到**中间**。
    *   如果到 mid 为止的星数**大于或等于 K，s** 将 mid 撕入变量并向 mid 左侧移动**结束= mid 1**
    *   否则，通过**开始=中间+1** 移动到中间右侧
*   返回所需值**和**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the number of rows
int count_rows(int n, int k)
{

    // A diamond pattern contains
    // 2*n-1 rows so end = 2*n-1
    int start = 1, end = 2 * n - 1, ans = 0;

    // Loop for the binary search
    while (start <= end) {
        int mid = start - (start - end) / 2;

        int stars_till_mid = 0;

        if (mid > n) {

            // l_stars is no of rows in
            // lower triangle of diamond
            int l_stars = 2 * n - 1 - mid;
            int till_half = (n * (n + 1)) / 2;

            stars_till_mid
                = till_half + ((n - 1) * (n)) / 2
                  - ((l_stars) * (l_stars + 1)) / 2;
        }
        else {

            // No of stars till mid th row
            stars_till_mid = mid * (mid + 1) / 2;
        }

        // Check if k > starts_till_mid
        if (k <= stars_till_mid) {
            ans = mid;
            end = mid - 1;
        }
        else
            start = mid + 1;
    }

    // Return Answer
    return ans;
}

// Driver function
int main()
{
    int N = 3, K = 8;

    // Call the function
    // and print the answer
    cout << count_rows(N, K);
}
```

## 蟒蛇 3

```
# python3 program for the above approach

# Function to count the number of rows
def count_rows(n, k):

        # A diamond pattern contains
        # 2*n-1 rows so end = 2*n-1
    start = 1
    end = 2 * n - 1
    ans = 0

    # Loop for the binary search
    while (start <= end):
        mid = start - (start - end) // 2

        stars_till_mid = 0

        if (mid > n):

            # l_stars is no of rows in
            # lower triangle of diamond
            l_stars = 2 * n - 1 - mid
            till_half = (n * (n + 1)) / 2

            stars_till_mid = till_half + \
                ((n - 1) * (n)) / 2 - ((l_stars) * (l_stars + 1)) / 2

        else:

            # No of stars till mid th row
            stars_till_mid = mid * (mid + 1) / 2

            # Check if k > starts_till_mid
        if (k <= stars_till_mid):
            ans = mid
            end = mid - 1
        else:
            start = mid + 1

        # Return Answer
    return ans

# Driver function
if __name__ == "__main__":

    N = 3
    K = 8

    # Call the function
    # and print the answer
    print(count_rows(N, K))

    # This code is contributed by rakeshsahni
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to count the number of rows
const count_rows = (n, k) => {

    // A diamond pattern contains
    // 2*n-1 rows so end = 2*n-1
    let start = 1, end = 2 * n - 1, ans = 0;

    // Loop for the binary search
    while (start <= end)
    {
        let mid = start - parseInt((start - end) / 2);
        let stars_till_mid = 0;

        if (mid > n)
        {

            // l_stars is no of rows in
            // lower triangle of diamond
            let l_stars = 2 * n - 1 - mid;
            let till_half = (n * (n + 1)) / 2;

            stars_till_mid = till_half + ((n - 1) * (n)) / 2 -
                            ((l_stars) * (l_stars + 1)) / 2;
        }
        else
        {

            // No of stars till mid th row
            stars_till_mid = mid * (mid + 1) / 2;
        }

        // Check if k > starts_till_mid
        if (k <= stars_till_mid)
        {
            ans = mid;
            end = mid - 1;
        }
        else
            start = mid + 1;
    }

    // Return Answer
    return ans;
}

// Driver code
let N = 3, K = 8;

// Call the function
// and print the answer
document.write(count_rows(N, K));

// This code is contributed by rakeshsahni

</script>
```

**Output**

```
4
```

***时间复杂度:** O(log N)*
***辅助空间:** O(1)*