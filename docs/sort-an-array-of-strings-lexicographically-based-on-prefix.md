# 根据前缀

按照字典顺序对字符串数组进行排序

> 原文:[https://www . geeksforgeeks . org/sort-字符串数组-基于前缀的词典编纂/](https://www.geeksforgeeks.org/sort-an-array-of-strings-lexicographically-based-on-prefix/)

给定一个大小为 **N** 的字符串数组**arr【】**，任务是[按照字典顺序](https://www.geeksforgeeks.org/sort-words-lexicographical-order-python/)对字符串数组进行排序，如果在对任意两个字符串 **A** 和字符串 **B** 进行排序时，如果字符串 **A** 是字符串 **B** 的前缀，那么字符串 **B** 应该按照排序顺序出现。

**示例:**

> **输入:** arr[] = {“太阳”、“月亮”、“模拟”}
> **输出:**
> 模拟
> 月亮
> 太阳
> **解释:**
> 辞书排序为模拟、月亮、太阳。
> 
> **输入:**arr[]= {“geeks”、“geeksfor”、“geeks forgeeks”}
> **输出:**
> 【geeks forgeeks】
> 
> geeks

**方法:**想法是使用内置的[排序](https://www.geeksforgeeks.org/sort-c-stl/)函数使用下面的比较器函数对给定的字符串数组进行排序。用于[的比较器函数使用 C++中的](https://www.geeksforgeeks.org/check-string-substring-another/) [compare()函数检查是否有任何字符串作为子字符串出现在另一个字符串](https://www.geeksforgeeks.org/stdstringcompare-in-c/)中，然后，它应该按照长度的降序排列它们。

## C++

```
bool my_compare(string a, string b)
{
    // If any string is a substring then
    // return the size with greater length
    if (a.compare(0, b.size(), b) == 0
        || b.compare(0, a.size(), a) == 0)
        return a.size() & gt;
    b.size();

    // Else return lexicographically
    // smallest string
    else return a & lt;
    b;
}
```

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to print the vector
void Print(vector<string> v)
{
    for (auto i : v)
        cout << i << endl;
}

// Comparator function to sort the
// array of string wrt given conditions
bool my_compare(string a, string b)
{
    // Check if a string is present as
    // prefix in another string, then
    // compare the size of the string
    // and return the larger size
    if (a.compare(0, b.size(), b) == 0
        || b.compare(0, a.size(), a) == 0)

        return a.size() > b.size();

    // Else return lexicographically
    // smallest string
    else
        return a < b;
}

// Driver Code
int main()
{
    // GIven vector of strings
    vector<string> v = { "batman", "bat", "apple" };

    // Calling Sort STL with my_compare
    // function passed as third parameter
    sort(v.begin(), v.end(), my_compare);

    // Function call to print the vector
    Print(v);
    return 0;
}
```

**Output:** 

```
apple
batman
bat
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(1)*