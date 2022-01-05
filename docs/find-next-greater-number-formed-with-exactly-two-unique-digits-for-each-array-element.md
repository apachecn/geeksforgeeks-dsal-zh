# 查找下一个更大的数字，该数字由每个数组元素的两个唯一数字组成

> 原文:[https://www . geeksforgeeks . org/find-next-better-number-formed-每个数组元素有两个唯一的数字/](https://www.geeksforgeeks.org/find-next-greater-number-formed-with-exactly-two-unique-digits-for-each-array-element/)

给定一个具有 **N** 个整数的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是为范围**【0，N】**中的每个 **i** 找到下一个更大的数 **X** ，即**X>= arr【I】**，使得 **X** 中唯一数字的计数正好为 **2** 。

**示例:**

> **输入:** arr[] = {123，234}
> **输出:** 131 242
> **解释:**对于给定数组，131 是大于 123 的最小数字，正好有 2 个唯一数字。类似地，242 是大于 234 的最小数字，正好有 2 个唯一的数字。
> 
> **输入:**arr[]= { 35466666 }
> T3】输出:355333333

**天真方法:**对于范围**【0，N】**中的每个 **i** 迭代所有大于**arr【I】**的整数，并跟踪第一个整数，使得整数中唯一数字的[计数正好为 2，就可以解决给定的问题。](https://www.geeksforgeeks.org/count-of-unique-digits-in-a-given-number-n/)

***时间复杂度:** O(N * M)，其中 M 代表 arr[]中的最大元素。*
***辅助空间:** O(log N)*

**高效方法:**上述方法可以使用[位屏蔽](https://www.geeksforgeeks.org/bitmasking-and-dynamic-programming-set-1-count-ways-to-assign-unique-cap-to-every-person/)进行优化。可以观察到，在给定范围内具有两位数的所有整数都可以通过迭代所有可能的两个唯一数字对并生成由它们形成的所有数字来计算。这可以通过[这篇](https://www.geeksforgeeks.org/print-all-numbers-less-than-n-with-at-most-2-unique-digits/)文章中讨论的算法来实现。之后，可以使用[集合数据结构](https://www.geeksforgeeks.org/set-in-cpp-stl/)来存储所有的整数，对于 **arr[i]** 的每个值，可以使用[下界](https://www.geeksforgeeks.org/upper_bound-and-lower_bound-for-vector-in-cpp-stl/)函数使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)找到大于 **arr[i]** 的最小整数。

下面是上述方法的实现:

## C++

```
// C++ program of the above approach
#include <bits/stdc++.h>
using namespace std;

#define int long long

// Stores the set of integers with 2 unique digits
set<int> helper;
vector<int> nums;

// Function to find the value of a^b
int power(int a, int b)
{

    // Stores the value
    int ans = 1;
    while (b > 0) {
        if (b & 1) {
            ans = ans * a;
        }
        b = b >> 1;
        a = a * a;
    }

    // Return Answer
    return ans;
}

void nextGreaterEle(int arr[], int N)
{

    // Loop to iterate the given array
    for (int i = 0; i < N; i++) {

        // For each array element, find next
        // greater element in the vector nums
        // of integers using lower_bound
        cout << *lower_bound(nums.begin(), nums.end(),
                             arr[i])
             << " ";
    }
}

// Function to calculate the digits having
// exactly two unique digits
void preProcess()
{
    // Loop to iterate over all possible
    // pairs of digits from 0 to 9
    for (int i = 0; i <= 9; i++) {
        for (int j = 0; j <= 9; j++) {

            // Stores the maximum length of integer
            int len = 10;
            for (int k = 0; k <= (1 << len); k++) {
                int temp = k;
                int number = 0;
                int curLen = 0;
                while (temp > 0) {
                    if (temp & 1) {

                        // Include numbers with the
                        // next digit as i
                        number = i * power(10, curLen)
                                 + number;
                    }
                    else {

                        // Include numbers with the next
                        // next digit as j
                        number = j * power(10, curLen)
                                 + number;
                    }

                    // Update temp
                    temp = (temp >> 1);
                    curLen++;
                }

                // Insert the current number into the set
                helper.insert(number);
                while (curLen <= len) {
                    number = j * power(10, curLen) + number;
                    helper.insert(number);
                    curLen++;
                }
            }
        }
    }

    // Loop to insert all the integers into
    // a vector from the set if the unique digits
    // in the integer is exactly two.
    for (auto cur : helper) {

        // Stores the unique digits
        set<int> count;
        int orz = cur;
        while (cur > 0) {
            count.insert(cur % 10);
            cur = cur / 10;
        }

        // If count of exactly two
        if (count.size() == 2) {
            nums.push_back(orz);
        }
    }
}

// Driver Code
signed main()
{
    int arr[] = { 123, 234 };
    int N = sizeof(arr) / sizeof(arr[0]);

    preProcess();
    nextGreaterEle(arr, N);

    return 0;
}
```

**Output**

```
131 242 
```

***时间复杂度:**O(10<sup>6</sup>+N * log N)= O(N * log N)*
***辅助空间:** O(10 <sup>6</sup> ) = O(1)*