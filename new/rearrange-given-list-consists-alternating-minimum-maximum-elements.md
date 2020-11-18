# 重新排列给定列表，使其包含交替的最小最大元素

给定一个整数列表，请重新排列该列表，使其仅使用列表操作由交替的最小最大元素**组成。 在列表中存在的所有元素中，列表的第一个元素应为最小值，第二个元素应为最大值。 同样，第三个元素将是下一个最小元素，第四个元素是下一个最大元素，依此类推。 不允许使用多余的空间。**

例子：

```
Input:  [1 3 8 2 7 5 6 4]
Output: [1 8 2 7 3 6 4 5]

Input:  [1 2 3 4 5 6 7]
Output: [1 7 2 6 3 5 4]

Input:  [1 6 2 5 3 4]
Output: [1 6 2 5 3 4]

```

想法是先按升序对列表进行排序。 然后，我们从列表末尾开始弹出元素，然后将其插入列表中的正确位置。

以下是上述想法的实现–

## C / C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to rearrange a given list such that it``// consists of alternating minimum maximum elements``#include <bits/stdc++.h>``using` `namespace` `std;` [`// Function to rearrange a given list such that it``// consists of alternating minimum maximum elements``void` `alternateSort(list<` `int` `>& inp)``{` `// sort the list in ascending order` `inp.sort();` `// get iterator to first element of the list` `list<` `int` `>::iterator it = inp.begin();` `it++;` `for` `(` `int` `i=1; i<(inp.size() + 1)/2; i++)` `{` `// pop last element (next greatest)` `int` `val = inp.back();` `inp.pop_back();` `// insert it after next minimum element` `inp.insert(it, val);`  `// increment the pointer for next pair` `++it;` `}``}``// Driver code``int` `main()``{` `// input list` `list<` `int` `> inp({ 1, 3, 8, 2, 7, 5, 6, 4 });` `// rearrange the given list` `alternateSort(inp);` `// print the modified list` `for` `(` `int` `i : inp)` `cout << i <<` `" "` `;` `return` `0;``}` |

*chevron_right**filter_none*