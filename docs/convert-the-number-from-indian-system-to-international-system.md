# 将印度系统的号码转换为国际系统

> 原文:[https://www . geesforgeks . org/convert-the-number-from-Indian-system-to-international-system/](https://www.geeksforgeeks.org/convert-the-number-from-indian-system-to-international-system/)

在印度数字系统中，给定由数字和分隔符(，)组成的输入字符串 **N** ，任务是根据国际数字系统在放置分隔符(，)后打印字符串。

**示例:**

> **输入:** N = "12，34，56，789 "
> T3】输出: 123，456，789
> 
> **输入:**N =“90，05，00，00，000”
> T3】输出: 90，050，000，000

**进场:**

1.  从字符串中移除所有分隔符(，)。
2.  从字符串末尾开始迭代，并在每三个数字后放置一个分隔符(，)。
3.  打印结果。

以下是上述方法的实现:

## C++

```
// C++ Program to convert
// the number from Indian system
// to International system

#include <bits/stdc++.h>
using namespace std;

// Function to convert Indian Numeric
// System to International Numeric System
string convert(string input)
{
    // Length of the input string
    int len = input.length();

    // Removing all the separators(, )
    // From the input string
    for (int i = 0; i < len; i++) {
        if (input[i] == ',') {
            input.erase(input.begin() + i);
            len--;
            i--;
        }
    }

    // Initialize output string
    string output = "";
    int ctr = 0;

    // Process the input string
    for (int i = len - 1; i >= 0; i--) {

        ctr++;
        output = input[i] + output;

        // Add a separator(, ) after
        // every third digit
        if (ctr % 3 == 0 && ctr < len) {
            output = ',' + output;
        }
    }

    // Return the output string back
    // to the main function
    return output;
}

// Driver Code
int main()
{
    string input1 = "12,34,56,789";
    string input2 = "90,05,00,00,000";

    cout << convert(input1) << endl;
    cout << convert(input2) << endl;
}
```

**Output:**

```
123,456,789
90,050,000,000

```

**相关文章:** [将数字从国际系统转换为印度系统](https://www.geeksforgeeks.org/convert-the-number-from-international-system-to-indian-system/)