# 使范围不重叠所需的最小清除量

> 原文:[https://www . geesforgeks . org/minimum-removes-需要制作范围-不重叠/](https://www.geeksforgeeks.org/minimum-removals-required-to-make-ranges-non-overlapping/)

给定一个带有起始值和结束值的范围列表，任务是找到需要移除的最小范围数，以使剩余范围不重叠。

**示例:**

> **输入:**输入= {{1，2}，{4，7}，{3，8}}
> **输出:** 1
> **解释:**移除{3，8}使{{1，2}和{4，7}}不重叠。
> 
> **输入:**输入= {{ 10，20 }、{ 10，20 }、{ 10，20 }}
> **输出:** 2
> **说明:**去掉【10，20】使剩余范围不重叠。
> 
> **输入:**输入= {{1，2}、{5，10}、{18，35}、{40，45}}
> **输出:** 0
> **说明:**所有范围已经不重叠。

**进场:**

*   按起始值对范围进行排序。
*   遍历范围，检查是否有任何范围的起点小于上一个范围的终点(即。存在重叠)。
*   Remove the range with greater ending point.

    下面的代码是上述方法的实现:

    ## C++

    ```
    #include <bits/stdc++.h>
    using namespace std;

    int minRemovals(vector<vector<int> >& ranges)
    {

        int size = ranges.size(), rem = 0;

        if (size <= 1)
            return 0;

        // Sort by minimum starting point
        sort(ranges.begin(), ranges.end(), 
            [](const vector<int>& a, const vector<int>& b) 
                        { return a[0] < b[0]; });

        int end = ranges[0][1];
        for (int i = 1; i < ranges.size(); i++) {

            // If the current starting point is less than
            // the previous interval's ending point 
            // (ie. there is an overlap)
            if (ranges[i][0] < end) {
                // increase rem
                rem++;
                // Remove the interval
                // with the higher ending point
                end = min(ranges[i][1], end);
            }
            else
                end = ranges[i][1];
        }

        return rem;
    }

    // Driver code
    int main()
    {
        vector<vector<int> > input = { { 19, 25 }, 
                            { 10, 20 }, { 16, 20 } };
        cout << minRemovals(input) << endl;
    }
    ```

    ## 蟒蛇 3

    ```
    def minRemovels (ranges):

        size = len(ranges)
        rem = 0

        # Sort by minimum starting point
        ranges.sort()

        end = ranges[0][1]
        for i in range(1, size):

            # If the current starting point is less
            # than the previous interval's ending
            # point (ie. there is an overlap)
            if (ranges[i][0] < end):

                # Increase rem
                rem += 1

                # Remove the interval
                # with the higher ending point
                end = min(ranges[i][1], end)

            else:
                end = ranges[i][1]

        return rem

    # Driver Code
    if __name__ == '__main__':

        Input = [ [ 19, 25 ],
                  [ 10, 20 ],
                  [ 16, 20 ] ]

        print(minRemovels(Input))

    # This code is contributed by himanshu77
    ```

    **Output:**

    ```
    2

    ```

    **时间复杂度:** O(n log n)