# TCS nqt 2020 |火车

> 原文:[https://www.geeksforgeeks.org/tcs-nqt-2020-trains/](https://www.geeksforgeeks.org/tcs-nqt-2020-trains/)

**问题:**

一次通过**列车 A** 可以在**T【0】**时间从始发站出发，在每个车站停留 **h** 时间单位，直到在**T【N–1】**到达最后一个车站，其中 **N** 是代表车站总数的正整数。

给定，**列车 A 在每个时间单位的**时刻为 **T[] = {10.00，10.04，10.09，10.15，10.19，10.22}** 。

现在，假设铁路管理局想增加更多的列车来增加频率。因此，启动其他**列车 B** ，与**列车 A**的车站相同。如果**B**次列车在 **t** 时刻发车，他们想知道**B**次列车的时间。程序应该像**列车 A** 一样，从第一站到最后一站，在每个车站为**列车 B** 返回一个字符串数组 **S** (时间戳(在[浮动](https://www.geeksforgeeks.org/difference-float-double-c-cpp/)中)。

**注:**

*   时间以 24 小时制表示。
*   开始时间应在**【0，23】**范围内。
*   开始分钟应该在**【0，59】**范围内。
*   输入开始时间(24 小时)

**示例:**

> **输入:** t = 11.00
> **输出:**11.00 11.04 11.09 11.15 11.19 11.22
> **说明:**B 列车的发车时间为 11.00，B 列车的站间时差与 a 列车相同
> 
> **输入:**t =-26.15
> T3】输出:无效输入
> T6】说明:不存在-26.15 这样的时间。因此，打印“无效输入”。

**方法:**思路是根据给定的 a 列车时刻计算各站之间的时差，按照以下步骤解决问题:

*   从给定的[数组](https://www.geeksforgeeks.org/array-data-structure/) **T[]** 中，生成一个数组 **train_B[]** ，其中 **train_B[i]** 是 **T[i]** 和**T[I–1]**之间的时间差，其中 **train_B[0] = 0.00** 和 **1 ≤ i ≤ 5。**
*   因此， **train_B[] = {0.00，0.04，0.05，0.06，0.04，0.03}** 。
*   如果 **t** 的整数部分不在**【0，24】**范围内，或者 **t** 的小数部分不在**【0，60】**范围内，则打印**“无效输入”**，因为整数部分代表小时，小数部分代表分钟。
*   否则，遍历**【0，5】**范围，打印 **t +列车 _B[i]** 表示**列车 B** 到达**I**站的时间。然后更新 t 为 **t = t + train_B[i]** 。

下面是上述方法的实现:

## C

```
// C program for the above approach

#include <stdio.h>
#include <string.h>

// Function to find the timings for
// train B having same time difference
// as train_A
void findTime(float train_A[], int N,
              float t)
{
    float x;

    // Stores the time for train_B
    float train_B[N];
    train_B[0] = 0.00;

    for (int i = 1; i < N; i++) {
        train_B[i] = train_A[i]
                     - train_A[i - 1];
    }

    // Variables for typecasting
    int it, ix;
    it = (int)t;

    // Check if t is valid
    if (t >= 0.0 && t <= 24.0
        && (t - it) <= 60.0) {

        // Traverse from 0 to 5
        for (int i = 0; i < 6; i++) {

            // Update t
            x = t + train_B[i];
            ix = (int)x;

            if (x - ix >= 0.60)
                x = x + 0.40;
            if (x > 24.00)
                x = x - 24.0;

            // Print the current time
            printf("%.2f ", x);
            t = x;
        }
    }

    // If no answer exist
    else {
        printf("Invalid Input");
    }
}

// Driver Code
int main()
{
    // Given timings of train A
    // at each station
    float train_A[]
        = { 10.00, 10.04, 10.09,
            10.15, 10.19, 10.22 };

    int N = sizeof(train_A)
            / sizeof(train_A[0]);

    // Given start time t
    float t = 11.00;

    // Function Call
    findTime(train_A, N, t);
    return 0;
}
```

**Output:**

```
11.00 11.04 11.09 11.15 11.19 11.22

```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)