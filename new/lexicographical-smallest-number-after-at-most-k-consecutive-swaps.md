# 最多 K 次连续互换后的词典最小数字

> 原文：[https://www.geeksforgeeks.org/lexicographical-smallest-number-after-at-most-k-consecutive-swaps/](https://www.geeksforgeeks.org/lexicographical-smallest-number-after-at-most-k-consecutive-swaps/)

给定字符串 **str** 形式的数字和整数 **K** 的形式，任务是找到执行最多 **K** 次连续交换后可以形成的最小整数 。

> **连续交换**表示一次交换就可以将索引 **i** 的字符与索引 **i – 1** 或 **i + 1** 的字符交换。 。

**示例**：

> **输入**：str =“ 76921”，K = 3
> **输出**：27691
> **说明**：
> 27691 是词典上可能的最小数字 。
> 
> **输入**：str =“ 9438957234785635408”，K = 23
> **输出**：0345989723478563548
> **说明**：
> 0345989723478563548 是字典上最小的数字 。

**朴素的方法**：最简单的想法是[生成给定字符串](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/)的所有可能排列，并检查哪个词典上最小的字符串最多满足 **K** 交换的条件。 打印该字符串。

**时间复杂度**：*O（N！），其中 N 是给定字符串的*长度。

**辅助空间**：*`O(1)`*

**更好的方法**：更好的方法是使用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)。 步骤如下：

1.  如果给定数字中存在前导零，则将其删除。

2.  当 **K** 较小时，从字符串 str [考虑 **str [k]** 中选择最小的元素，否则 **N** ]。

3.  将所有这些元素右移 1 个位置后，将最小的元素放置在**第 0 个**位置。

4.  在上述步骤中，从 **K** 减去交换的数量。

5.  如果仍然剩下 **K > 0** ，那么我们从下一个起始位置开始应用相同的程序，即 **str [2，…N]，**，然后 将其放置在**第一**位置。

6.  因此，我们继续应用相同的过程，直到 **K 变为 0** 为止。

**时间复杂度**：*O（N <sup>2</sup> ），其中 N 是给定字符串的*长度。

**辅助空间**：*`O(1)`*

**有效方法**：的想法是使用 [**细分树**](http://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/) 和 [**散列**](http://www.geeksforgeeks.org/hashing-data-structure/) 。 步骤如下：

1.  如果给定数字中存在前导零，则将其删除。

2.  将数字的原始位置存储在[映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中，并找到最适合每个移位小于 **K** 的索引的数字。

3.  使用地图查找数字的原始位置。

4.  找到当前位置正对的数字位数，为此，在段树中标记其位置从 **[0…N-1]** 移位。

5.  段树的每个节点都包含已移位的位置数。 现在的任务是查找在 **[current_index，N-1]** 范围内移动了多少个位置，因为这只会影响原始位置。

6.  要移动的新位置将为**（原始位置** **+ number_of_right – element_shifted – i），即**，即元素的原始位置被添加到刚移动的段树中。

下面是上述方法的程序：

## C++

```cpp

// C++ program for the above approach 
#include <bits/stdc++.h> 
using namespace std; 

// Function to mark the pos as 1 that 
// are shifted in string in Segtree node 
void segAdd(vector<int>& seg, int start, 
            int end, int pos, int curr) 
{ 

    // Out of Range 
    if (pos < start or pos > end) 
        return; 

    // Check if we reach the positon 
    if (start == end) { 
        seg[curr] = 1; 
        return; 
    } 

    // Initialize the mid 
    int mid = (start + end) / 2; 

    // Recursion call 
    segAdd(seg, start, mid, pos, 
           2 * curr + 1); 

    segAdd(seg, mid + 1, end, pos, 
           2 * curr + 2); 

    // Every node contains no of 
    // marked postion that are 
    // shifted in a range 
    seg[curr] = seg[2 * curr + 1] 
                + seg[2 * curr + 2]; 

    return; 
} 

// Function to find the number of 
// elements which got shifted 
int segFind( 
    vector<int>& seg, int pos_start, 
    int pos_end, int start, int end, 
    int curr) 
{ 
    // Return 0 is the end position is 
    // less than start or the start 
    // position is greater than end 
    if (pos_end < start 
        or pos_start > end) 
        return 0; 

    if (pos_start <= start 
        and pos_end >= end) 
        return seg[curr]; 

    // Initialize the mid 
    int mid = (start + end) / 2; 

    // Recursion call 
    int left = segFind( 
        seg, pos_start, pos_end, 
        start, mid, 2 * curr + 1); 

    int rigt = segFind( 
        seg, pos_start, pos_end, 
        mid + 1, end, 2 * curr + 2); 

    // Return the result 
    return left + rigt; 
} 

// Function to remove leading zeros 
// from the given string str 
string removeLeadingZeros(string str) 
{ 

    int i = 0; 

    // To store the resultant string 
    string ans = ""; 

    for (; i < str[i]; i++) { 

        // If Initial character is 0, 
        // then remove it 
        if (str[i] == '0') { 
            i++; 
        } 

        // Else break 
        else { 
            break; 
        } 
    } 

    ans = str.substr(i - 1, 
                     str.length()); 

    // Return the updated string 
    return ans; 
} 

// Function to find the lexiographically 
// smallest integer 
string findMinimumInteger( 
    string arr, int k) 
{ 

    // To remove leading zeros 
    arr = removeLeadingZeros(arr); 

    int n = arr.size(); 

    // Segment tree vector 
    vector<int> seg( 
        (2 * (int)pow( 
                 2, 
                 (int)(ceil(log2(n)))) 
         - 1), 
        0); 

    // Hash to find the original 
    // position of the digit 
    unordered_map<int, list<int> > m; 

    for (int i = 0; i < n; i++) { 
        m[arr[i] - '0'].push_back(i); 
    } 

    // Resultant string variable 
    string res = ""; 

    for (int i = 0; i < n; i++) { 

        // Place a digit from 
        // 0-9 which fit best 
        for (int digit = 0; 
             digit <= 9; digit++) { 

            if (m[digit].size() != 0) { 
                int original_pos 
                    = m[digit].front(); 

                // Find the number of 
                // right elements that 
                // are shifted from 
                // current element 
                int shift 
                    = segFind( 
                        seg, original_pos, 
                        n - 1, 0, n - 1, 0); 

                // Mark the new position 
                int new_pos = original_pos 
                              + shift 
                              - i; 

                if (new_pos <= k) { 
                    k -= new_pos; 

                    // Add the original postion of 
                    // the element which got shifted 
                    segAdd(seg, 0, n - 1, 
                           original_pos, 0); 

                    res.push_back('0' + digit); 
                    m[digit].pop_front(); 
                    break; 
                } 
            } 
        } 
    } 

    // Return the result 
    return res; 
} 

// Driver Code 
int main() 
{ 
    // Given string 
    string s = "9438957234785635408"; 

    // Given K swaps 
    int k = 23; 

    // Function Call 
    cout << findMinimumInteger(s, k) 
         << endl; 
} 

```

**Output:**

```
0345989723478563548

```

**时间复杂度**：O（N * log N），其中 N 是字符串的长度。

**辅助空间**：`O(n)`

[![competitive-programming-img](img/5211864e7e7a28eeeb039fa5d6073a24.png)](https://practice.geeksforgeeks.org/courses/competitive-programming-live?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_cp)

* * *

* * *



