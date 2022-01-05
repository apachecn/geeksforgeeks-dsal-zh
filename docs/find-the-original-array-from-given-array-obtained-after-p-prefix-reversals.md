# 从 P 前缀反转后得到的给定数组中找到原始数组

> 原文:[https://www . geeksforgeeks . org/find-the-original-array-from-给定-array-after-p-prefix-reverses/](https://www.geeksforgeeks.org/find-the-original-array-from-given-array-obtained-after-p-prefix-reversals/)

给定大小为 **N** 的数组**arr【】**和整数 **P** (P < N)，任务是从通过 **P 前缀反转**获得的数组中找到原始数组，其中在**和**反转中，包含范围为**【0，I-1】**的索引的数组的大小为 I**前缀被反转。**

**示例:**

> **输入:** arr[] = {4，2，1，3，5，6}，P = 4。
> **输出:** 1 2 3 4 5 6
> **解释:** {1，2，3，4，5，6}在前缀反转 P = 1 时转换为{1，2，3，4，5，6}。
> {1，2，3，4，5，6}在前缀反转 P = 2 时转换为{2，1，3，4，5，6}。
> {2，1，3，4，5，6}在前缀反转 P = 3 时转换为{3，1，2，4，5，6}
> {3，1，2，4，5，6}在前缀反转 P = 4 时转换为{4，2，1，3，5，6}
> 所以答案是{1，2，3，4，5，6}
> 
> **输入:** arr[] = {10，9，8，3，5，6}，P = 3
> T3】输出: 9 8 10 3 5 6

**天真方法:**解决问题从 **P** 大小的前缀开始，在范围**【1，P】**内为 **i** 每一步反向大小的前缀 **i** ，然后逐渐递减大小。

***时间复杂度:***O(N<sup>2</sup>)
***辅助空间:*** O(1)

**高效进场:**该方案基于[双指针进场](https://www.geeksforgeeks.org/two-pointers-technique/)。由于只有 **P** 前缀反转，数组的第一个 **P** 元素只受到影响，其余保持不变。因此，在 **P** 前缀反转后，可以观察到原始数组和数组的模式。只需修改第一个 **P** 元素。按照以下步骤解决上述问题:

*   初始化两个变量 **l = 0** 和 **r = P-1**
*   初始化向量 **res** 以存储修改的前缀和**索引= 0** 以跟踪奇数和偶数索引处的元素。
*   使用 while 循环遍历 **arr[]的前缀。**
    *   如果指数为偶数，将**arr【l】**推入向量 res 并增加 **l** 。
    *   否则将**arr【r】**推入向量 **res** 并递减 **r** 。
    *   也增加**索引**。
*   现在反转 **res** 并将修改后的前缀分配给 arr 的长度为 p 的前缀。
*   打印原始数组。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

void find_original_array(int arr[], int n, int p)
{
    // Initialize the r and l
    int r = p - 1;
    int l = 0;

    // Initialize index = 0
    // to track elements at
    // odd and even positions
    int index = 0;
    vector<int> res;

    while (l <= r) {

        // If index is even
        if (index % 2 == 0) {
            res.push_back(arr[l++]);
        }

        // If index is odd
        else {
            res.push_back(arr[r--]);
        }

        // Increment index
        index = index + 1;
    }

    // Reverse the res
    reverse(res.begin(), res.end());

    // Assign the modified prefix to arr
    for (int i = 0; i < res.size(); i++) {
        arr[i] = res[i];
    }

    // Print the array arr
    // which is the original array
    // modified from the
    // prefix reversed array
    for (int i = 0; i < n; i++) {
        cout << arr[i] << " ";
    }
}

// Driver code
int main()
{

    int arr[] = { 4, 2, 1, 3, 5, 6 }, P = 4;
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call
    find_original_array(arr, n, P);

    return 0;
}
```

**Output**

```
1 2 3 4 5 6 
```

***时间复杂度:*** O(N)，其中 N 为数组长度。
***辅助空间:*** O(N)