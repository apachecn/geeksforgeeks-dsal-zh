# 电视机| TCS MockVita 2020

> 原文:[https://www . geesforgeks . org/TV-sets-TCS-mock vita-2020/](https://www.geeksforgeeks.org/television-sets-tcs-mockvita-2020/)

**问题描述**

毗湿奴医生正在一个小镇上开设一家新的世界级医院，旨在成为该市患者的首选。医院有带电视和不带电视两种类型的 **N** 房间，每日房价分别为**【R1】****R2**。然而，从他的经验来看，毗湿奴医生知道病人的数量不是全年不变的，而是遵循一种模式。一年中任何一天的患者人数由以下公式给出:

> **每日患者=(6–M)<sup>2</sup>+| D–15 |**
> 其中，
> **M:** 月数从 1 日开始至 12 日
> **D:** 日从 1 日开始至 31 日结束

所有患者都喜欢没有电视的房间，因为它们更便宜，但只有在没有电视的房间不可用的情况下，才会选择有电视的房间。医院有运营第一年的收入目标。给定这个目标以及 **N** 、 **R1** 和 **R2** 的值，你需要确定医院应该购买的电视数量，以便达到收入目标。假设医院在 1 月 1 日开业，并且这一年是非闰年。

**示例:**

> **输入:** N = 20，R1 = 1500，R2 = 1000，目标= 7000000
> **输出:** 14
> **解释:**
> 使用公式:
> 1 月 1 日患者人数为 39 人，1 月 2 日为 38 人，以此类推。
> 考虑到只有 20 个房间，两种房间的价格分别为 1500 和 1000。
> 因此需要 14 台电视机才能以 13 台电视机获得 711.95 万的收入。
> 总营收将低于 7000000。
> 
> **输入:** N = 10，R1 = 1000，R2 = 1500，目标= 1000000
> **输出:** 10
> **说明:**
> 在上面的例子中，即使给所有房间都装上电视，目标也不会实现。
> 因此，答案是 10，即医院的房间总数。

**方法:**思路是遍历全年，每天产生收益。找出第一年每一个可能有电视的房间的收入。按照以下步骤解决问题:

1.  假设有电视的房间总数为**台电视**，其中 **0 ≤电视≤ N** 。
2.  对于每一个数字的电视，第一年的收入可以通过每天的遍历找到。
3.  上面的公式可以用来计算每天的病人数量。假设 **np** 为当前患者数。
4.  当前患者人数 **np** 可以有今天患者人数的值，也可以有房间总数的值，以最小者为准。
5.  如果病人数量少于没有电视的房间数量，那么今天的总收入就是 **np*R2** 因为便宜。
6.  否则，如果病人数量大于没有电视的房间，那么今天的总收入由下式给出:

    > **(N-电视)* R2+(NP –( N-电视))*R1**

7.  在目标值中添加每天的收入，并在检查所有可能的组合后打印生成的最大目标值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function that returns number of
// patient for a day in a month
int getPatients(int M, int D)
{
    return ((6 - M) * (6 - M))
           + abs(D - 15);
}

// Function that count the TVs with
// given amount of revenue target
void countTVs(long long n, long long r1,
              long long r2, long long target)
{
    long long np, tvs, current_target;

    // Days in each month
    vector<int> days = { 0, 31, 28, 31,
                         30, 31, 30, 31,
                         31, 30, 31, 30,
                         31 };

    // Check all possible combinations
    for (tvs = 0; tvs <= n; tvs++) {

        // Stores the current target
        current_target = 0;

        for (int m = 1; m <= 12; m++) {

            for (int d = 1;
                 d <= days[m]; d++) {

                // Number of patients
                // on day d of month m
                np = getPatients(m, d);

                // Patients cannot be
                // exceed number of rooms
                np = min(np, n);

                // If the number of patient is
                // <= count of rooms without tv
                if (np <= n - tvs) {

                    // All patients will opt
                    // for rooms without tv
                    current_target += np * r2;
                }

                // Otherwise
                else {

                    // Some will opt for
                    // rooms with tv and
                    // others without tv
                    current_target
                        += ((n - tvs) * r2
                            + ((np - (n - tvs))
                               * r1));
                }
            }
        }

        // If current target meets
        // the required target
        if (current_target >= target) {
            break;
        }
    }

    // Print the count of TVs
    cout << min(tvs, n);
}

// Driver Code
int main()
{
    long long N = 20, R1 = 1500;
    long long R2 = 1000;
    long long target = 7000000;

    // Function Call
    countTVs(N, R1, R2, target);

    return 0;
}
```

**Output:**

```
14

```

***时间复杂度:** O(N*365)，其中 N 为给定房间数。*
***辅助空间:** O(1)*