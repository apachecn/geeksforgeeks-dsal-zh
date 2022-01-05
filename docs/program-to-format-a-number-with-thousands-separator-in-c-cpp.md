# 在 C/C++中用千位分隔符格式化数字的程序

> 原文:[https://www . geesforgeks . org/program-to-format-一个带千位分隔符的数字-in-c-cpp/](https://www.geeksforgeeks.org/program-to-format-a-number-with-thousands-separator-in-c-cpp/)

给定一个整数 **N** ，任务是以国际位置值格式打印给定整数的输出，并在合适的位置放置逗号，从右边开始。

**示例**

> **输入:**N = 47634
> T3】输出: 47，634
> 
> **输入:**N = 1000000
> T3】输出:1000000

**方法:**按照以下步骤解决问题:

1.  [将给定的整数 **N** 转换为其等价的字符串](https://www.geeksforgeeks.org/converting-string-to-number-and-vice-versa-in-c/)。
2.  [从右向左迭代给定字符串的字符](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)。
3.  每遍历 3 个字符后，插入一个'，'分隔符。

下面是上述方法的实现:

## C++

```
// C++ program to implement the
// above approach

#include <bits/stdc++.h>
using namespace std;

// Function to put thousands
// separators in the given integer
string thousandSeparator(int n)
{
    string ans = "";

    // Convert the given integer
    // to equivalent string
    string num = to_string(n);

    // Initialise count
    int count = 0;

    // Traverse the string in reverse
    for (int i = num.size() - 1;
         i >= 0; i--) {
        count++;
        ans.push_back(num[i]);

        // If three characters
        // are traversed
        if (count == 3) {
            ans.push_back(',');
            count = 0;
        }
    }

    // Reverse the string to get
    // the desired output
    reverse(ans.begin(), ans.end());

    // If the given string is
    // less than 1000
    if (ans.size() % 4 == 0) {

        // Remove ','
        ans.erase(ans.begin());
    }

    return ans;
}

// Driver Code
int main()
{
    int N = 47634;
    string s = thousandSeparator(N);
    cout << s << endl;
}
```

**Output:**

```
47,634

```

***时间复杂度:** O(log <sub>10</sub> N)
**辅助空间:** O(1)*