# 检查是否可以通过追加字符串 S1 的子序列获得字符串 S2

> 原文:[https://www . geesforgeks . org/check-if-string-S2-可通过追加字符串子序列-s1/](https://www.geeksforgeeks.org/check-if-string-s2-can-be-obtained-by-appending-subsequences-of-string-s1/) 获得

给定两个[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/)**【S1】**和 **S2** ，任务是通过将 **S1** 的[子序列](https://www.geeksforgeeks.org/print-subsequences-string/)重复追加到最初为空的字符串的末尾来检查是否有可能生成字符串 **S2** 。如果可能，打印“**是**”和所需的最小操作次数。否则，打印“**否**”。

**示例:**

> **输入:**S1 =“acbcd”，S2 =“acbcd”
> **输出:**
> YES
> 2
> **说明:**追加子序列“acbc”后加“d”得到 S2。
> 
> **输入:**S1 =“aceasd”，S2 =“asdxds”
> T3】输出: NO
> **说明:**由于 S1 不存在字符**‘x’**，无法获取 S2。

**方法:**按照以下步骤解决问题:

*   [迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)**【S1】**中的字符，并将每个字符在 **S1** 中的[频率存储在一个数组 **freq[]** 中。](https://www.geeksforgeeks.org/python-frequency-of-each-character-in-string/)
*   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)**【S2】**[检查 S2 是否有 S1](https://www.geeksforgeeks.org/check-if-there-is-any-common-character-in-two-given-strings/) 没有的字符。如果发现任何这样的字符，打印“否”。
*   否则，迭代 **S1** 中的字符，并更新[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)中每个字符的索引
*   遍历字符串 **S2** ，对于每个字符，检查它是否可以包含在可以追加的 **S1** 的当前子序列中。
*   如果发现为真，则将当前字符的索引设置为附加的最后一个字符的索引。否则，增加子序列的数量，并将当前字符的索引设置为附加的最后一个字符的索引。继续下一个字符。
*   最后，打印“ **YES** ”和该子序列的计数作为所需答案。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include "bits/stdc++.h"
using namespace std;

// Function for finding minimum
// number of operations
int findMinimumOperations(string s,
                          string s1)
{

    // Stores the length of strings
    int n = s.length(), m = s1.length();

    // Stores frequency of
    // characters in string s
    int frequency[26] = { 0 };

    // Update  frequencies of
    // character in s
    for (int i = 0; i < n; i++)
        frequency[s[i] - 'a']++;

    // Traverse string s1
    for (int i = 0; i < m; i++) {

        // If any character in s1
        // is not present in s
        if (frequency[s1[i] - 'a']
            == 0) {
            return -1;
        }
    }

    // Stores the indices of
    // each character in s
    set<int> indices[26];

    // Traverse string s
    for (int i = 0; i < n; i++) {

        // Store indices of characters
        indices[s[i] - 'a'].insert(i);
    }

    int ans = 1;

    // Stores index of last
    // appended character
    int last = (*indices[s1[0]
                      - 'a']
                     .begin());

    // Traverse string s1
    for (int i = 1; i < m; i++) {

        int ch = s1[i] - 'a';

        // Find the index of next
        // character that can be appended
        auto it = indices[ch].upper_bound(
            last);

        // Check if the current
        // character be included
        // in the current subsequence
        if (it != indices[ch].end()) {
            last = (*it);
        }

        // Otherwise
        else {

            // Start a new subsequence
            ans++;

            // Update index of last
            // character appended
            last = (*indices[ch].begin());
        }
    }
    return ans;
}

// Driver Code
int main()
{

    string S1 = "acebcd", S2 = "acbcde";
    int ans = findMinimumOperations(
        S1, S2);

    // If S2 cannot be obtained
    // from subsequences of S1
    if (ans == -1) {
        cout << "NO\n";
    }
    // Otherwise
    else {
        cout << "YES\n"
             << ans;
    }

    return 0;
}
```

## 蟒蛇 3

```
# Python3 Program to implement
# the above approach
from bisect import bisect ,bisect_left,bisect_right

# Function for finding minimum
# number of operations
def findMinimumOperations(s,s1):

    #Stores the length of strings
    n = len(s)
    m = len(s1)

    # Stores frequency of
    # characters in string s
    frequency = [0]*26

    # Update  frequencies of
    # character in s
    for i in range(n):
        frequency[ord(s[i]) - ord('a')] += 1

    # Traverse string s1
    for i in range(m):

        # If any character in s1
        # is not present in s
        if (frequency[ord(s1[i]) - ord('a')] == 0):
            return -1

    # Stores the indices of
    # each character in s
    indices = [[] for i in range(26)]

    # Traverse string s
    for i in range(n):

        # Store indices of characters
        indices[ord(s[i]) - ord('a')].append(i)

    ans = 2

    # Stores index of last
    # appended character
    last =len(indices[ord(s1[0])- ord('a')]) - 1

    # Traverse string s1
    for i in range(1,m):

        ch = ord(s1[i]) - ord('a')

        # Find the index of next
        # character that can be appended
        it = bisect_right(indices[ch],last)
        # print(it)

        # Check if the current
        # character be included
        # in the current subsequence
        if (it != len(indices[ch])):
            last = it
        # Otherwise
        else:

            # Start a new subsequence
            ans += 1

            # Update index of last
            # character appended
            last = len(indices[ch])
    return ans

# Driver Code
if __name__ == '__main__':

    S1 = "acebcd"
    S2 = "acbcde"
    ans = findMinimumOperations(S1, S2)

    # If S2 cannot be obtained
    # from subsequences of S1
    if (ans == -1):
        print("NO")
    # Otherwise
    else:
        print("YES")
        print(ans)

# This code is contributed by mohit kumar 29
```

**Output:** 

```
YES
2
```

***时间复杂度:** O(Mlog(N))*
***辅助空间:** O(N)*