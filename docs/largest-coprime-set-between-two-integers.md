# 两个整数之间的最大互质集

> 原文:[https://www . geesforgeks . org/maximum-互素-两个整数之间的集合/](https://www.geeksforgeeks.org/largest-coprime-set-between-two-integers/)

给定表示一个范围的两个整数 **L** 和 **R** ，任务是找到范围 L 到 R 的最大的同素整数集
**示例:**

> **输入:** L = 10，R = 25
> **输出:** 10 11 13 17 19 21 23
> **输入:** L = 45，R = 57
> **输出:** 45 46 47 49 53

**方法:**思想是从 L 迭代到 R，并尝试将整数放在一个集合中，使得该集合的最大公约数保持为 1。这可以通过存储集合的 LCM 来完成，并且每次在将元素添加到集合中之前，检查具有集合 LCM 的编号的 GCD 是否保持为 1。最后，找到最大的整数集合。
**例如:**

```
Let L = 10, R = 14

Element 10:
// Co-prime Sets 
S = {{10}},
LCM of Co-prime sets
A = {10}

Element 11:
// Element 11 can be added to
// the first set
S = {{10, 11}}
A = {110}

Element 12:
S = {{10, 11}, {12}}
A = {110, 12}

Element 13:
S = {{10, 11, 13}, {12}}
A = {1430, 12}

Element 14:
S = {{10, 11, 13}, {12}, {14}}
A = {1430, 12, 14}
```

## C++

```
// C++ implementation to find
// the largest co-prime set in a
// given range
#include <bits/stdc++.h>
using namespace std;

// Function to find the largest
// co-prime set of the integers
void findCoPrime(int n, int m)
{
    // Initialize sets
    // with starting integers
    vector<int> a = { n };
    vector<vector<int> > b = { a };

    // Iterate over all the possible
    // values of the integers
    for (int i = n + 1; i <= m; i++) {

        // lcm of each set in array
        // 'b' stored in set 'a'
        // so go through set 'a'
        for (int j = 0; j < a.size(); j++) {
            // if there gcd is 1 then
            // element add in that
            // array corresponding to b
            if (__gcd(i, a[j]) == 1) {

                // update the new lcm value
                int q = (i * a[j]) / __gcd(i, a[j]);

                b[j].push_back(i);
                a[j] = q;
            }
        }
        a.push_back(i);
        b.push_back({ i });
    }
    vector<int> maxi = {};
    for (int i = 0; i < b.size(); i++) {
        if (b[i].size() > maxi.size()) {
            maxi = b[i];
        }
    }
    for (auto i = maxi.begin(); i != maxi.end(); i++) {
        cout << *i << " ";
    }
    cout << endl;
}

// Driver Code
int main()
{
    int n = 10;
    int m = 14;
    findCoPrime(n, m);
    return 0;
}

// This code is contributed by rj13to.
```

## 计算机编程语言

```
# Python implementation to find
# the largest co-prime set in a
# given range

import math

# Function to find the largest
# co-prime set of the integers
def findCoPrime(n, m):
    # Initialize sets
    # with starting integers
    a =[n]
    b =[[n]]

    # Iterate over all the possible
    # values of the integers
    for i in range(n + 1, m + 1):

        # lcm of each list in array
        # 'b' stored in list 'a'
        # so go through list 'a'
        for j in range(len(a)):

            # if there gcd is 1 then
            # element add in that
            # list corresponding to b
            if math.gcd(i, a[j])== 1:

                # update the new lcm value
                q =(i * a[j])//math.gcd(i, a[j])
                r = b[j]
                r.append(i)
                b[j]= r
                a[j]= q
        else:
            a.append(i)
            b.append([i])
    maxi = []
    for i in b:
        if len(i) > len(maxi):
            maxi = i
    print(*maxi)

# Driver Code
if __name__ == "__main__":
    n = 10
    m = 14
    findCoPrime(n, m)
```

**Output:** 

```
10 11 13
```