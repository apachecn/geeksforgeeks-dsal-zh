# 在一个字符串中分别对数字组和字符组进行排序

> 原文:[https://www . geeksforgeeks . org/sort-一组数字和字符-字符串中单独列出/](https://www.geeksforgeeks.org/sort-groups-of-numbers-and-characters-separately-in-a-string/)

给定字母数字字符的字符串 **str** ，任务是分别对相似的连续字符组进行排序，并打印修改后的字符串，即所有连续的数字组和字母字符组将分别排序。
**例:**

> **输入:** str = "121geeks21"
> **输出:**112 eegks12
> “121”“geeks”“21”为有效组
> ，将分别排序。
> **输入:** str = "cba321ab"
> **输出:** abc123ab

**方法:**创建一个向量来存储给定字符串中所有有效组的起始索引。现在，逐个字符遍历字符串，如果当前字符与前一个字符来自不同的组，则将当前索引推送到向量。在字符串完全遍历后，使用之前更新的向量对给定字符串的所有单个子字符串组进行排序。最后，打印修改后的字符串。
以下是上述办法的实施情况:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the modified string
string get_string(string str, int n)
{

    // To store the previous character
    char prev = str[0];

    // To store the starting indices
    // of all the groups
    vector<int> result;

    // Starting index of the first group
    result.push_back(0);

    for (int i = 1; i < n; i++) {

        // If the current character and the
        // previous character differ
        if (isdigit(str[i]) != isdigit(prev)) {

            // Push the starting index
            // of the new group
            result.push_back(i);
        }

        // The current character now becomes previous
        prev = str[i];
    }

    // Sort the first group
    sort(str.begin(), str.begin() + result[0]);

    // Sort all the remaining groups
    for (int i = 0; i < result.size() - 1; i++) {
        sort(str.begin() + result[i],
             str.begin() + result[i + 1]);

    }
    //cout<<str<<endl;
    // Sort the last group
    sort(str.begin() + result[result.size() - 1],
         str.end());

    // Return the modified string
    return str;
}

// Driver code
int main()
{
    string str = "121geeks21";
    int n = str.length();

    cout << get_string(str, n);

    return 0;
}
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return the modified string
def get_string(st, n):

    # To store the previous character
    prev = st[0]

    # To store the starting indices
    # of all the groups
    result = []

    # Starting index of the first group
    result.append(0)

    for i in range(1, n):

        # If the current character and the
        # previous character differ
        if (st[i].isdigit() != prev.isdigit()):

            # Push the starting index
            # of the new group
            result.append(i)

        # The current character now becomes previous
        prev = st[i]

    # Sort the first group
    st = list(st)
    st[:result[0]].sort()
    p = st.copy()

    # Sort all the remaining groups
    for i in range(len(result)-1):
        p[result[i]:result[i+1]] = sorted(st[result[i]:result[i+1]])

    # print(''.join(st))

    # Sort the last group
    p[len(p)-2:] = sorted(st[result[-1]:])

    # Return the modified string
    return ''.join(p)

# Driver code
if __name__ == "__main__":

    st = "121geeks21"
    n = len(st)

    print(get_string(st, n))

    # This code is contributed by ukasp.
```

**Output:** 

```
112eegks12
```