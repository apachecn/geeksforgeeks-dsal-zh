# 使用给定的数字组形成的 N 的最小倍数

> 原文:[https://www . geeksforgeeks . org/最小 n 倍数使用给定的数字组/](https://www.geeksforgeeks.org/smallest-multiple-of-n-formed-using-the-given-set-of-digits/)

给定一组数字 **S** 和一个整数 **N** ，任务是找到最小的正整数(如果存在)，它只包含来自 **S** 的数字，并且是 **N** 的倍数。**注意**集合中的数字可以多次使用。

**示例:**

> **输入:** S[] = {5，2，3}，N = 12
> **输出:** 252
> 我们可以观察到 252 是用{2，5}形成的，是 12 的倍数
> 
> **输入:** S[] = {1，3，5，7，9}，N = 2
> **输出:**-1
> 2 的倍数总是偶数，但是从给定的一组数字中不能形成偶数。

一种**简单的方法**是对这组数字进行排序，然后从最小的数字移动到使用给定数字形成的最大的数字。我们检查每个数字是否满足给定的条件。以这种方式实现它将导致指数级的时间复杂度。

更好的方法是使用模运算。因此，我们维护了一个队列，在这个队列中，我们将存储使用给定数字 **N** 的数字集形成的模数。最初在队列中，会有(一位数)% N，但是我们可以通过使用计算(两位数)% N，

> New_mod = (Old_mod * 10 +数字)% N

通过使用上面的表达式，我们可以计算多个数字的模数值。这是动态编程的一个应用，因为我们正在构建从较小状态到较大状态的解决方案。我们维护另一个向量，以确保要插入队列的元素已经存在于队列中。它使用哈希来确保 O(1)时间复杂度。我们使用了另一个向量对，它也使用哈希来存储值，它的结构是

> 结果[new _ mod]= { current _ element _ of _ queue，数字}

该向量将用于构建解决方案:

1.  对这组数字进行排序。
2.  初始化两个向量 dp 和 result，分别用 INT_MAX 和{-1，0}初始化。
3.  初始化队列并插入数字% N
4.  队列不为空时执行。
5.  从队列中删除前值，对于集合中的每个数字，使用上面写的表达式找到(形成的数字)% N。
6.  如果在队列为空之前我们没有得到 0 作为模值，那么最小的正数不存在，否则从第 0 个索引开始跟踪结果向量，直到我们在任何索引处得到-1。
7.  将所有这些值放在另一个向量中，并反转它。
8.  这是我们需要的解决方案。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the required number
int findSmallestNumber(vector<int>& arr, int n)
{

    // Initialize both vectors with their initial values
    vector<int> dp(n, numeric_limits<int>::max() - 5);
    vector<pair<int, int> > result(n, make_pair(-1, 0));

    // Sort the vector of digits
    sort(arr.begin(), arr.end());

    // Initialize the queue
    queue<int> q;
    for (auto i : arr) {
        if (i != 0) {

            // If modulus value is not present
            // in the queue
            if (dp[i % n] > 1e9) {

                // Compute digits modulus given number and
                // update the queue and vectors
                q.push(i % n);
                dp[i % n] = 1;
                result[i % n] = { -1, i };
            }
        }
    }

    // While queue is not empty
    while (!q.empty()) {

        // Remove the first element of the queue
        int u = q.front();
        q.pop();
        for (auto i : arr) {

            // Compute new modulus values by using old queue
            // values and each digit of the set
            int v = (u * 10 + i) % n;

            // If value is not present in the queue
            if (dp[u] + 1 < dp[v]) {
                dp[v] = dp[u] + 1;
                q.push(v);
                result[v] = { u, i };
            }
        }
    }

    // If required condition can't be satisfied
    if (dp[0] > 1e9)
        return -1;
    else {

        // Initialize new vector
        vector<int> ans;
        int u = 0;
        while (u != -1) {

            // Constructing the solution by backtracking
            ans.push_back(result[u].second);
            u = result[u].first;
        }

        // Reverse the vector
        reverse(ans.begin(), ans.end());
        for (auto i : ans) {

            // Return the required number
            return i;
        }
    }
}

// Driver code
int main()
{
    vector<int> arr = { 5, 2, 3 };
    int n = 12;

    cout << findSmallestNumber(arr, n);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach 

# Function to return the required number 
def findSmallestNumber(arr, n): 

    # Initialize both vectors with their initial values 
    dp = [float('inf')] * n 
    result = [(-1, 0)] * n 

    # Sort the vector of digits 
    arr.sort() 

    # Initialize the queue 
    q = [] 
    for i in arr:  
        if i != 0:  

            # If modulus value is not 
            # present in the queue 
            if dp[i % n] > 10 ** 9:  

                # Compute digits modulus given number 
                # and update the queue and vectors 
                q.append(i % n) 
                dp[i % n] = 1 
                result[i % n] = -1, i  

    # While queue is not empty 
    while len(q) > 0:

        # Remove the first element of the queue 
        u = q.pop(0) 
        for i in arr:  

            # Compute new modulus values by using old 
            # queue values and each digit of the set 
            v = (u * 10 + i) % n 

            # If value is not present in the queue 
            if dp[u] + 1 < dp[v]:  
                dp[v] = dp[u] + 1 
                q.append(v) 
                result[v] = u, i  

    # If required condition can't be satisfied 
    if dp[0] > 10 ** 9:
        return -1 
    else:  

        # Initialize new vector 
        ans = [] 
        u = 0 
        while u != -1:  

            # Constructing the solution by backtracking 
            ans.append(result[u][1]) 
            u = result[u][0] 

        # Reverse the vector 
        ans = ans[::-1] 
        for i in ans:  

            # Return the required number 
            return i 

# Driver code 
if __name__ == "__main__": 

    arr = [5, 2, 3]  
    n = 12 

    print(findSmallestNumber(arr, n)) 

# This code is contributed by Rituraj Jain
```

**Output:**

```
2

```