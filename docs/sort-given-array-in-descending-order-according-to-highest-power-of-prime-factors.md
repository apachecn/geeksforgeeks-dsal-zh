# 按照质因数的最高幂次对给定数组进行降序排序

> 原文:[https://www . geesforgeks . org/按质因数的最高幂降序排列给定数组/](https://www.geeksforgeeks.org/sort-given-array-in-descending-order-according-to-highest-power-of-prime-factors/)

给定一个大小为 **N** 的数组 **arr[]** 。任务是根据**最高表达度**对**arr【】**中的元素进行降序排序。一个数的最大度被定义为它可以用其因子的幂来表示的最大值。

**注:**

*   如果数字具有相同的表达程度，则在原始数组中排在第一位的元素将在排序数组中排在第一位。
*   如果两个数字具有相同的最高学位，则应使用先到先得的方法。

**示例:**

> **输入** : arr[] = {81，25，27，32，51}
> **输出**:【32，81，27，25，51】
> **说明:**经过素分解后
> 81 可以表示为 81 <sup>1</sup> ，9 <sup>2</sup> ，或者 3 <sup>4</sup> 。表达程度最高的选择(3) <sup>4</sup> ，因为 4 大于 2 和 1。
> 25 可以表示为 5 <sup>2。</sup>
> 27 可以表示为 3 <sup>3</sup> 。
> 32 可以改为 2 <sup>5</sup> 。
> 51 可以表示为 51 <sup>1</sup> 。
> 现在，根据他们的力量按降序排列。
> 所以 32 排第一，因为 2 <sup>5</sup> 的功率最高，其次是 81、27、25，最后是 51，功率为 1。
> 
> **输入** : arr[] = {23，6}
> **输出**:【23，6】
> **解释**:由于 23 和 6 的幂相同(1)，所以我们打印 23，先有 23，后有 6。

**逼近**:这个问题可以用[素分解](https://www.geeksforgeeks.org/prime-factorization-using-sieve-olog-n-multiple-queries/)解决。按照以下步骤解决给定的问题。

*   一个数的最高幂可以通过把它分解成它的素因子的乘积来获得。
*   在这些因素中选择权力最大的因素。
*   将一个数的最高幂与该数一起存储在一对中，并根据其因子的最高幂对该对进行排序。
*   **使用埃拉托斯特尼方法的[筛，预先计算](http://www.geeksforgeeks.org/sieve-of-eratosthenes/)**到 10^5 的所有素数。
*   对于数组中的每个数字，找出该数字的所有因子，并将其因子的最高幂与该数字一起存储在一对整数的向量中。
*   根据第二个元素(表达式的最高顺序)对该对进行降序排序。

下面是上述方法的实现。

## C++

```
// C++ code to implement the above approach
#include <bits/stdc++.h>
#include <iostream>
using namespace std;

bitset<500001> Primes;
vector<int> Factors;

// Function to compute Sieve of Eratosthenes
void SieveOfEratosthenes(int n)
{
    Primes[0] = 1;
    for (int i = 3; i <= n; i += 2) {
        if (Primes[i / 2] == 0) {
            for (int j = 3 * i; j <= n; j += 2 * i)
                Primes[j / 2] = 1;
        }
    }

    for (int i = 2; i <= 500001; i++) {
        if (!Primes[i])
            Factors.push_back(i);
    }
}

// Compare function for sorting
bool compare(const pair<int, int>& a,
             const pair<int, int>& b)
{
    return a.second > b.second;
}

// Function to find any log(a) base b
int log_a_to_base_b(int a, int b)
{
    return log(a) / log(b);
}

// Function to find the Highest Power
// of K which divides N
int HighestPower(int N, int K)
{
    int start = 0, end = log_a_to_base_b(N, K);
    int ans = 0;
    while (start <= end) {

        int mid = start + (end - start) / 2;
        int temp = (int)(pow(K, mid));

        if (N % temp == 0) {
            ans = mid;
            start = mid + 1;
        }
        else {
            end = mid - 1;
        }
    }
    return ans;
}

// Function to display N numbers
// on the basis of their Highest Order
// of Expression in descending order
void displayHighestOrder(int arr[], int N)
{
    vector<pair<int, int> > Nums;

    for (int i = 0; i < N; i++) {

        // The least power of a number
        // will always be 1 because
        // that number raised to
        // the power 1 is it itself
        int temp = 1;
        for (auto& Prime : Factors) {

            // The factor of a number greater than
            // its square root is the number itself
            // which is considered in temp
            if (Prime * Prime > arr[i])
                break;
            else if (arr[i] % Prime == 0)
                temp = max(
                    temp,
                    HighestPower(arr[i], Prime));
        }
        Nums.push_back(make_pair(arr[i], temp));
    }

    sort(Nums.begin(), Nums.end(), compare);

    for (int i = 0; i < N; i++) {
        cout << Nums[i].first << " ";
    }
    cout << endl;
}

// Driver Code
int main()
{

    SieveOfEratosthenes(500000);

    int arr[] = { 81, 25, 27, 32, 51 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    displayHighestOrder(arr, N);

    return 0;
}
```

**Output**

```
32 81 27 25 51 

```

***时间复杂度:**T3】O(N<sup>1.5</sup>* log(K))，其中 K 是数组中最大的元素。
***辅助空间** :* O(1)*