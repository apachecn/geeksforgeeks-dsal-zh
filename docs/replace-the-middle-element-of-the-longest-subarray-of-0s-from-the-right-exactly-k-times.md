# 从右边恰好 K 次开始替换最长的 0 子阵列的中间元素

> 原文:[https://www . geeksforgeeks . org/从正好 k 次中替换最长的 0 子数组中的中间元素/](https://www.geeksforgeeks.org/replace-the-middle-element-of-the-longest-subarray-of-0s-from-the-right-exactly-k-times/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，最初由 **0** s 和正整数 **K** 组成，任务是通过精确执行以下操作 **K** 次来打印数组元素。

*   对于每一次**I**操作，选择最右边最长的[子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)由所有 **0** s 组成，并用 **i** 替换子阵列的中间元件。
*   如果存在两个中间元素，则[检查 **i** 是否为偶数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)。如果发现是真的，那么用 **i** 替换最右边的中间元素。
*   Otherwise, replace the leftmost middle element with **i**.

    **示例:**

    > **输入:** arr[] = { 0，0，0，0，0}，K = 3
    > **输出:** 3 0 1 0 2
    > **解释:**
    > 在第一次操作中选择子阵列{ arr[0]，…，arr[4]}并用 1 替换 arr[2]将 arr[]修改为{ 0，0，1，0，0}
    > 在第二次操作中选择子阵列{ arr[3]，…，arr[4]}并替换 arr[4] 2}
    > 在第三次操作中，选择子阵列{ arr[0]，…，arr[1]}并用 3 替换 arr[1]将 arr[]修改为{ 0，3，1，0，2}
    > 因此，所需的输出为 3 0 1 0 2。
    > 
    > **输入:** arr[] = { 0，0，0，0，0，0，0 }，K = 7
    > **输出:** 7 3 6 1 5 2 4

    **方法:**使用[贪婪手法](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决问题。想法是使用[优先队列](https://www.geeksforgeeks.org/priority-queue-of-vectors-in-c-stl-with-examples/)选择最右边最长的[子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)全 0。按照以下步骤解决问题:

    *   初始化一个[优先级队列](https://www.geeksforgeeks.org/priority-queue-of-vectors-in-c-stl-with-examples/)，比如 **pq** ，以存储形式 **{ X，Y}** 的子阵列，其中 **X** 表示子阵列的长度， **Y** 表示[子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)的起始索引。
    *   所有 **0** s 的子阵初始最大长度为 **N** ，子阵起始指数为 **0** 。因此，将 **{ N，0 }** 插入 **pq** 。
    *   使用变量 **i** 迭代范围**【1，K】**。每次 **i <sup>第</sup>** 次操作，从 **pq** 弹出[顶元素，检查弹出元素的长度是否为](https://www.geeksforgeeks.org/priority_queuetop-c-stl/)[奇数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)。如果发现是真的，则用 **i** 替换子阵列的中间元件。
    *   否则，[如果 **i** 是偶数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)，则用 **i** 替换子阵最右边的中间元素。否则，用 **i** 替换子阵列最左边的中间元件。
    *   用 **i** 替换中间元件后，将包含所有 **0** s 的子阵列的左半部分和右半部分插入 **pq** 中。
    *   最后，打印数组元素。

    下面是上述方法的实现:

    ## C++

    ```
    // C++ program to implement
    // the above approach

    #include <bits/stdc++.h>
    using namespace std;

    // Function to print array by replacing the mid
    // of the righmost longest subarray with count
    // of operations performed on the array 
    void ReplaceArray(int arr[], int N, int K)
    {

        // Stores subarray of the form { X, Y },
        // where X is the length and Y is start
        // index of the subarray
        priority_queue<vector<int> > pq;

        // Insert the array arr[] 
        pq.push({ N, 0 });

        // Stores index of mid 
        // element of the subarray
        int mid;

        // Iterate over the range [1, N]
        for (int i = 1; i <= K; i++) {

            // Stores top element of pq
            vector<int> sub = pq.top();

            // Pop top element of pq
            pq.pop();

            // If length of the subarray
            // is an odd number
            if (sub[0] % 2 == 1) {

                // Update mid
                mid = sub[1] + sub[0] / 2;

                // Replacing arr[mid] with i
                arr[mid] = i;

                // Insert left half of
                // the subarray into pq
                pq.push({ sub[0] / 2,
                             sub[1] });

                // Insert right half of
                // the subarray into pq
                pq.push({ sub[0] / 2, 
                               (mid + 1) });
            }

            // If length of the current 
            // subarray is an even number
            else {

                // If i is 
                // an odd number
                if (i % 2 == 1) {

                    // Update mid
                    mid = sub[1] + sub[0] / 2;

                    // Replacing mid element
                    // with i
                    arr[mid - 1] = i;

                    // Insert left half of
                    // the subarray into pq
                    pq.push({ sub[0] / 2 - 1, 
                                   sub[1] });

                    // Insert right half of
                    // the subarray into pq
                    pq.push({ sub[0] / 2, mid });
                }

                // If i is an even number
                else {

                    // Update mid
                    mid = sub[1] + sub[0] / 2;

                    // Replacing mid element
                    // with i
                    arr[mid - 1] = i;

                    // Insert left half of
                    // the subarray into pq
                    pq.push({ sub[0] / 2,
                                sub[1] });

                    // Insert right half of
                    // the subarray into pq
                    pq.push({ sub[0] / 2 - 1,
                               (mid + 1) });
                }
            }
        }

        // Print array elements
        for (int i = 0; i < N; i++)
            cout << arr[i] << " ";
    }

    // Driver Code
    int main()
    {

        int arr[] = { 0, 0, 0, 0, 0 };
        int N = sizeof(arr) / sizeof(arr[0]);
        int K = 3;
        ReplaceArray(arr, N, K);
    }
    ```

    **Output:**

    ```
    3 0 1 2 0

    ```

    ***时间复杂度:** O(K * log(N))*
    ***辅助空间:** O(N)*