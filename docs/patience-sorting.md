# 耐心整理

> 原文:[https://www.geeksforgeeks.org/patience-sorting/](https://www.geeksforgeeks.org/patience-sorting/)

**耐心排序**是基于卡牌游戏[耐心](https://en.wikipedia.org/wiki/Patience_(game))的排序算法。在这个排序算法中，耐心游戏规则用于根据元素的值对元素列表进行排序。
**耐心游戏规则:**

*   价值较低的卡片可以放在卡片上。
*   如果卡没有可能的位置，则可以创建一个新的堆。
*   目标是形成尽可能少的桩。

下面是游戏的可视化如下:

<video class="wp-video-shortcode" id="video-406280-1" width="640" height="360" preload="metadata" controls=""><source type="video/mp4" src="https://media.geeksforgeeks.org/wp-content/cdn-uploads/20200906151051/ezgif.com-gif-to-mp41.mp4?_=1">[https://media.geeksforgeeks.org/wp-content/cdn-uploads/20200906151051/ezgif.com-gif-to-mp41.mp4](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20200906151051/ezgif.com-gif-to-mp41.mp4)</video>

就像上面的可视化一样，很明显，只有当牌的价值低于牌堆中最高的牌时，才会放置牌。否则，如果没有这样的桩，则创建一个新桩。
**耐心排序:**耐心排序一般有两个步骤，即创建堆和合并堆。以下是步骤说明:

*   初始化一个 2D 数组来存储桩。
*   遍历给定的数组并执行以下操作:
    1.  遍历所有的堆，检查每个堆的顶部是否小于当前元素。如果发现为真，则将当前元素推到堆栈顶部。
    2.  否则，创建一个新的堆栈，将当前元素作为该堆栈的顶部。
*   **合并桩:**想法是执行 **p** 桩的 **k** 路合并，每个桩都在内部排序。当堆中元素的计数大于或等于 **0** 时，迭代所有堆，从每个堆的顶部找到最小的元素，并将其推入排序的数组中。

下面是排序步骤的可视化:

<video class="wp-video-shortcode" id="video-406280-2" width="640" height="360" preload="metadata" controls=""><source type="video/mp4" src="https://media.geeksforgeeks.org/wp-content/cdn-uploads/20200906151444/Patience_Sorting.mp4?_=2">[https://media.geeksforgeeks.org/wp-content/cdn-uploads/20200906151444/Patience_Sorting.mp4](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20200906151444/Patience_Sorting.mp4)</video>

以下是上述方法的实现:

## C++

```
// C++ program of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to merge piles in a sorted order
vector<int> merge_piles(vector<vector<int> >& v)
{

    // Store minimum element from
    // the top of stack
    vector<int> ans;

    // In every iteration find the smallest element
    // of top of pile and remove it from the piles
    // and store into the final array
    while (1) {

        // Stores the smallest element
        // of the top of the piles
        int minu = INT_MAX;

        // Stores index of the smallest element
        // of the top of the piles
        int index = -1;

        // Calculate the smallest element
        // of the top of the every stack
        for (int i = 0; i < v.size(); i++) {

            // If minu is greater than
            // the top of the current stack
            if (minu > v[i][v[i].size() - 1]) {

                // Update minu
                minu = v[i][v[i].size() - 1];

                // Update index
                index = i;
            }
        }

        // Insert the smallest element
        // of the top of the stack
        ans.push_back(minu);

        // Remove the top element from
        // the current pile
        v[index].pop_back();

        // If current pile is empty
        if (v[index].empty()) {

            // Remove current pile
            // from all piles
            v.erase(v.begin() + index);
        }

        // If all the piles are empty
        if (v.size() == 0)
            break;
    }
    return ans;
}

// Function to sort the given array
// using the patience sorting
vector<int> patienceSorting(vector<int> arr)
{

    // Store all the created piles
    vector<vector<int> > piles;

    // Traverse the array
    for (int i = 0; i < arr.size(); i++) {

        // If no piles are created
        if (piles.empty()) {

            // Initialize a new pile
            vector<int> temp;

            // Insert current element
            // into the pile
            temp.push_back(arr[i]);

            // Insert current pile into
            // all the piles
            piles.push_back(temp);
        }
        else {

            // Check if top element of each pile
            // is less than or equal to
            // current element or not
            int flag = 1;

            // Traverse all the piles
            for (int j = 0; j < piles.size(); j++) {

                // Check if the element to be
                // inserted is less than
                // current pile's top
                if (arr[i] < piles[j][piles[j].size() - 1]) {
                    piles[j].push_back(arr[i]);

                    // Update flag
                    flag = 0;
                    break;
                }
            }

            // If flag is true
            if (flag) {

                // Create a new pile
                vector<int> temp;

                // Insert current element
                // into temp
                temp.push_back(arr[i]);

                // Insert current pile
                // into all the piles
                piles.push_back(temp);
            }
        }
    }

    // Store the sorted sequence
    // of the given array
    vector<int> ans;

    // Sort the given array
    ans = merge_piles(piles);

    // Traverse the array, ans[]
    for (int i = 0; i < ans.size(); i++)
        cout << ans[i] << " ";

    return ans;
}

// Driver Code
int main()
{
    vector<int> arr = { 6, 12, 2, 8, 3, 7 };

    // Function Call
    patienceSorting(arr);
}
```

## java 描述语言

```
<script>
// Javascript program of the above approach

// Function to merge piles in a sorted order
function merge_piles(v) {

    // Store minimum element from
    // the top of stack
    let ans = [];

    // In every iteration find the smallest element
    // of top of pile and remove it from the piles
    // and store into the final array
    while (1) {

        // Stores the smallest element
        // of the top of the piles
        let minu = Number.MAX_SAFE_INTEGER;

        // Stores index of the smallest element
        // of the top of the piles
        let index = -1;

        // Calculate the smallest element
        // of the top of the every stack
        for (let i = 0; i < v.length; i++) {

            // If minu is greater than
            // the top of the current stack
            if (minu > v[i][v[i].length - 1]) {

                // Update minu
                minu = v[i][v[i].length - 1];

                // Update index
                index = i;
            }
        }

        // Insert the smallest element
        // of the top of the stack
        ans.push(minu);

        // Remove the top element from
        // the current pile
        v[index].pop();

        // If current pile is empty
        if (v[index].length == 0) {

            // Remove current pile
            // from all piles
            v.splice(index, 1);
        }

        // If all the piles are empty
        if (v.length == 0)
            break;
    }
    return ans;
}

// Function to sort the given array
// using the patience sorting
function patienceSorting(arr) {

    // Store all the created piles
    let piles = [];

    // Traverse the array
    for (let i = 0; i < arr.length; i++) {

        // If no piles are created
        if (piles.length == 0) {

            // Initialize a new pile
            let temp = [];

            // Insert current element
            // into the pile
            temp.push(arr[i]);

            // Insert current pile into
            // all the piles
            piles.push(temp);
        }
        else {

            // Check if top element of each pile
            // is less than or equal to
            // current element or not
            let flag = 1;

            // Traverse all the piles
            for (let j = 0; j < piles.length; j++) {

                // Check if the element to be
                // inserted is less than
                // current pile's top
                if (arr[i] < piles[j][piles[j].length - 1]) {
                    piles[j].push(arr[i]);

                    // Update flag
                    flag = 0;
                    break;
                }
            }

            // If flag is true
            if (flag) {

                // Create a new pile
                let temp = [];

                // Insert current element
                // into temp
                temp.push(arr[i]);

                // Insert current pile
                // into all the piles
                piles.push(temp);
            }
        }
    }

    // Store the sorted sequence
    // of the given array
    let ans = [];

    // Sort the given array
    ans = merge_piles(piles);

    // Traverse the array, ans[]
    for (let i = 0; i < ans.length; i++)
        document.write(ans[i] + " ");

    return ans;
}

// Driver Code

let arr = [6, 12, 2, 8, 3, 7];

// Function Call
patienceSorting(arr);

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output:** 

```
2 3 6 7 8 12
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

**注意:**上述方法可以通过使用[优先级队列](https://www.geeksforgeeks.org/priority-queue-in-cpp-stl/)合并桩来优化。
***时间复杂度:**O(N * log(N))*
***辅助空间:** O(N)*

函数 playGif(){var gif = document . getelementbyid(' gif ')；if(gif . src = = " https://media . geesforgeeks . org/WP-content/uploads/20200501171647/Perience . gif "){gif . src = " https://media . geesforgeeks . org/WP-content/uploads/20200501175532/base 2 . jpg "；} else {gif . src = " https://media . geeksforgeeks . org/WP-content/uploads/20200501171647/Perience . gif "； } } 函数 playsortingif(){var gif 1 = document . getelementbyid('排序')；var gif 2 = document . getelementbyid(' sorting _ gif 1 ')；gif 1 . style . display = " none "；gif 2 . style . display = " block "； } 函数 pauseortinggif(){var gif 1 = document . getelementbyid('排序')；var gif 2 = document . getelementbyid(' sorting _ gif 1 ')；gif 1 . style . display = " block "；gif 2 . style . display = " none "； }