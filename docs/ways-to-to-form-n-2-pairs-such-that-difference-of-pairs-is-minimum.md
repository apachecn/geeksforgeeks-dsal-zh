# 形成 n/2 对的方式，使得对的差异最小

> 原文:[https://www . geesforgeks . org/形成 n-2 对的方法-这样对的差异最小/](https://www.geeksforgeeks.org/ways-to-to-form-n-2-pairs-such-that-difference-of-pairs-is-minimum/)

给定一个由 *N* 个整数组成的数组 *arr* ，任务是将数组的元素分成 *N/2* 对(每对有 2 个元素)，使得任意一对中两个元素之间的绝对差尽可能小。
**注:** *N* 永远是偶数。

**示例:**

> **输入:** arr[] = {1，7，3，8}
> **输出:** 1
> 只有一种方法可以和
> 最小差，(7，8)和(1，3)成对。
> 
> **输入:** arr[] = {1，1，1，1，2，2，2}
> **输出:** 9
> 这里所有值为 2 的元素将在它们之间配对(3 种可能的方式)，所有值为 1 的元素将在它们之间配对(3 种可能的方式)
> 因此，路数= 3 * 3 = 9
> 
> **输入:** arr[] = {2，3，2，2 }
> T3】输出: 3

**做法:**这个问题涉及到计数的基本原理和对排列组合的一些基本理解。

在继续之前，让我们计算数组= [3，3]
答案= 1 的路数，因为只有 1 个组合是可能的。
现在，让我们将数组修改为[3，3，3，3]。如上例所述，实现这一点的方法是:

> (1、2)、(3、4)
> (1、3)、(2、4)
> (1、4)、(2、3)
> 答案= 3 路。

进一步将数组修改为[3，3，3，3，3，3]

> (1、2)、(3、4)、(5、6)
> (1、2)、(3、5)、(4、6)
> (1、2)、(3、6)、(4、5)
> (1、3)、(2、4)、(5、6)
> (1、3)、(2、5)、(4、6)
> (1、3)、(2、6)、(4、5)
> (1、4)、(2、3)、(5、6)
> (1、4)、(2、5)、(3、6)【6】 (3、4)
> (1、6)、(2、3)、(4、5)
> (1、6)、(2、4)、(3、5)
> (1、6)、(2、5)、(3、4)
> 答案= 15 路。

这里我们通过简单的观察得到了一个广义的结果。如果数组中有 *K* 个元素具有相同的值，并且 K 是**偶数**，那么在它们之间形成对的方式的数量是:

> 对于尺寸 2，计数= 1 (1)
> 对于尺寸 4，计数= 3 (1 * 3)
> 对于尺寸 6，计数= 15 (1 * 3 * 5)
> 以此类推。
> 因此，形成大小为 K 的配对的方法有很多，其中 K 是偶数= 1 * 3 * 5 *……。* (K-1)

我们可以如下预计算这个结果。让 way[]成为数组，以便 way[I]存储大小为“I”的路的数量。

> way[2]= 1；
> 为(I = 4；一<1e 5+1；i += 2)
> 路[i] =路[I–2]*(I–1)；
> 
> 例如，我们考虑数组[3，3，3，3，3]
> 为了计算路的数量，我们用剩余的 5 个中的任何一个来固定第一个元素。
> 所以我们组成一对。现在还剩 4 个元素可以通过**方式【4】**方式配对。
> 所以路数为 **5 *路【4】**。

现在，计数可能不必总是偶数。因此，如果需要为一个通用数组解决这个问题，我们需要做两件事。

1.  按升序对数组进行排序。
2.  分析每组具有相同值的计数。

让我们的**数组= [2，3，3，3，3，4，4，4，4，4]** 。此数组已排序。

*   考虑值为 4 的元素。由于有 5 个元素，4 个元素将以**方式【4】**方式配对。可以通过 5 种方式选择遗漏元素。左边的元素必须与值为 3 的元素配对。这以 **4 种方式**发生，因为有 4 个元素的值为 3。因此，将保留一个值为 3 的元素与一个值为 4 的元素配对。所以剩下 3 个值为 3 的元素。2 将通过**方式【2】**方式配对，1 将通过 1 方式与值为 2 的元素配对。同样，将通过 3 种方式选择单独的元素。
*   因此从第 1 点开始，途径数将为:

    > 路[4] * 5 * 4 *路[2] * 3 * 1 = 180

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>

#define mp make_pair
#define pb push_back
#define S second
#define ll long long

using namespace std;

// Using mod because the number
// of ways might be very large
const int mod = 1000000007;

const int MAX = 100000;

// ways is serving the same
// purpose as discussed
ll ways[MAX + 1];

void preCompute()
{
    // pairing up zero people
    // requires one way.
    ways[0] = 1LL;
    ways[2] = 1LL;
    for (int i = 4; i <= MAX; i += 2) {
        ways[i] = (1LL * (i - 1) * ways[i - 2]) % mod;
    }
}

void countWays(int* arr, int n)
{

    // map count stores count of s.
    map<int, int> count;
    for (int i = 0; i < n; i++)
        count[arr[i]]++;

    vector<pair<int, int> > count_vector;
    map<int, int>::iterator it;
    for (it = count.begin(); it != count.end(); it++) {
        count_vector.pb(mp(it->first, it->second));
    }

    // vector count_vector stores a
    // pair < value, count of value>

    // sort according to value
    sort(count_vector.begin(), count_vector.end());

    ll ans = 1;

    // Iterating backwards.
    for (int i = count_vector.size() - 1; i > 0; i--) {

        int current_count = count_vector[i].S;
        int prev_count = count_vector[i - 1].S;

        // Checking if current count is odd.
        if (current_count & 1) {

            // if current count = 5, multiply ans by ways[4].
            ans = (ans * ways[current_count - 1]) % mod;

            // left out person will be selected
            // in current_count ways
            ans = (ans * current_count) % mod;

            // left out person will pair with previous
            //  person in previous_count ways
            ans = (ans * prev_count) % mod;

            /* if previous count is odd,
             * then multiply answer by ways[prev_count-1].
             * since one has already been reserved,
             * remaining will be even.
             * reduce prev_count = 0, since we don't need it now.*/
            if (prev_count & 1) {
                ans = (ans * ways[prev_count - 1]) % mod;
                count_vector[i - 1].S = 0;
            }
            else {

                /* if prev count is even, one will be reserved,
                 * therefore decrement by 1.
                 * In the next iteration, prev_count will become odd
                 * and it will be handled in the same way.*/
                count_vector[i - 1].S--;
            }
        }
        else {

            /* if current count is even,
             * then simply multiply ways[current_count]
             * to answer.*/
            ans = (ans * ways[current_count]) % mod;
        }
    }

    /* multiply answer by ways[first__count] since
       that is left out, after iterating the array.*/
    ans = (ans * ways[count_vector[0].S]) % mod;
    cout << ans << "\n";
}

// Driver code
int main()
{
    preCompute();
    int arr[] = { 2, 3, 3, 3, 3, 4, 4, 4, 4, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);
    countWays(arr, n);
    return 0;
}
```

## 蟒蛇 3

```
# Python3 implementation of the 
# above approach 
from collections import defaultdict

# Using mod because the number 
# of ways might be very large 
mod = 1000000007
MAX = 100000

# ways is serving the same 
# purpose as discussed 
ways = [None] * (MAX + 1) 

def preCompute(): 

    # pairing up zero people 
    # requires one way. 
    ways[0] = 1
    ways[2] = 1
    for i in range(4, MAX + 1, 2): 
        ways[i] = ((1 * (i - 1) * 
                    ways[i - 2]) % mod)

def countWays(arr, n): 

    # map count stores count of s. 
    count = defaultdict(lambda:0)
    for i in range(0, n): 
        count[arr[i]] += 1

    count_vector = [] 
    for key in count: 
        count_vector.append([key, count[key]]) 

    # vector count_vector stores a 
    # pair < value, count of value> 

    # sort according to value 
    count_vector.sort() 
    ans = 1

    # Iterating backwards. 
    for i in range(len(count_vector) - 1, -1, -1): 

        current_count = count_vector[i][1] 
        prev_count = count_vector[i - 1][1] 

        # Checking if current count is odd. 
        if current_count & 1: 

            # if current count = 5, multiply
            # ans by ways[4]. 
            ans = (ans * ways[current_count - 1]) % mod 

            # left out person will be selected 
            # in current_count ways 
            ans = (ans * current_count) % mod 

            # left out person will pair with previous 
            # person in previous_count ways 
            ans = (ans * prev_count) % mod 

            # if previous count is odd, 
            # then multiply answer by ways[prev_count-1]. 
            # since one has already been reserved, 
            # remaining will be even. 
            # reduce prev_count = 0, since we
            # don't need it now.
            if prev_count & 1:
                ans = (ans * ways[prev_count - 1]) % mod 
                count_vector[i - 1][1] = 0

            else:

                # if prev count is even, one will be 
                # reserved, therefore decrement by 1. 
                # In the next iteration, prev_count 
                # will become odd and it will be 
                # handled in the same way.
                count_vector[i - 1][1] -= 1

        else:

            # if current count is even, then simply
            # multiply ways[current_count] to answer.
            ans = (ans * ways[current_count]) % mod 

    # multiply answer by ways[first__count] since 
    # that is left out, after iterating the array.
    ans = (ans * ways[count_vector[0][1]]) % mod 
    print(ans) 

# Driver code 
if __name__ == "__main__":

    preCompute() 
    arr = [2, 3, 3, 3, 3, 4, 4, 4, 4, 4] 
    n = len(arr)
    countWays(arr, n) 

# This code is contributed by Rituraj Jain
```

**Output:**

```
180

```