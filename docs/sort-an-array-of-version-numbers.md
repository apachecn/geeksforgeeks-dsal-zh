# 对版本号数组进行排序

> 原文:[https://www . geesforgeks . org/sort-a-array-of-version-numbers/](https://www.geeksforgeeks.org/sort-an-array-of-version-numbers/)

给定一个字符串数组 **arr[]** ，由 **N** 个字符串组成，每个字符串以软件版本的形式表示点分隔的数字。

> **输入:**arr[]= {“1 . 1 . 2”“0 . 9 . 1”“1 . 1 . 0”}
> **输出:**“0 . 9 . 1”“1 . 1 . 0”“1 . 1 . 2”
> 
> **输入:**arr[]= {“1.2”、“0.8.1”、“1.0”}
> **输出:**“0 . 8 . 1”“1.0”“1.2”

**方法:**按照以下步骤解决问题:

*   创建一个函数来比较两个字符串。
*   将字符串存储到一个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)中。
*   为了比较两个**点分隔的字符串****【S1】**和 **S2** ，迭代至长度 **min(S1，S2) + 1** ，并比较字符串的每个数字部分并进行相应排序。
*   Repeat the above steps for each pair of string and sort the array accordingly.

    以下是上述想法的实现:

    ## C++

    ```
    // C++ Program to implement
    // the above approach
    #include <bits/stdc++.h>
    using namespace std;

    // Compares two strings
    int check(const string& a, const string& b)
    {

        int al = a.length();
        int bl = b.length();

        int i = 0, j = 0;
        while (i < al && j < bl) {
            if (a[i] == b[j]) {
                ++i;
                ++j;
            }
            else if (a[i] > b[j]) {
                return 1;
            }
            else
                return -1;
        }

        if (i == al && j == bl)
            return 0;
        if (i == al)
            return -1;
        return 1;
    }

    // Function to split strings based on dots
    vector<string> getTokens(const string& a)
    {
        vector<string> v;
        string s;

        // Stringstream is used here for
        // tokenising the string based
        // on "." delimiter which might
        // contain unequal number of "."[dots]
        stringstream ss(a);
        while (getline(ss, s, '.')) {
            v.push_back(s);
        }
        return v;
    }

    // Comparator to sort the array of strings
    bool comp(const string& a, const string& b)
    {

        // Stores the numerical substrings
        vector<string> va, vb;
        va = getTokens(a);
        vb = getTokens(b);

        // Iterate up to length of minimum
        // of the two strings
        for (int i = 0; i < min(va.size(), vb.size());
             i++) {

            // Compare each numerical substring
            // of the two strings
            int countCheck = check(va[i], vb[i]);

            if (countCheck == -1)
                return true;

            else if (countCheck == 1)
                return false;
        }

        if (va.size() < vb.size())
            return true;

        return false;
    }

    // Driver Code
    int main()
    {

        vector<string> s;
        s.push_back("1.1.0");
        s.push_back("1.2.1");
        s.push_back("0.9.1");
        s.push_back("1.3.4");
        s.push_back("1.1.2");
        s.push_back("1.1.2.2.3");
        s.push_back("9.3");

        // Sort the strings using comparator
        sort(s.begin(), s.end(), comp);

        // Display the sorted order
        for (int i = 0; i < s.size(); i++) {
            cout << s[i] << endl;
        }
        cout << endl;
        return 0;
    }
    ```

    **Output:**

    ```
    0.9.1
    1.1.0
    1.1.2
    1.1.2.2.3
    1.2.1
    1.3.4
    9.3

    ```

    ***时间复杂度:** O(N*L*logN)，其中 N 是版本字符串的总数，L 是这些字符串中最大的长度。
    **辅助空间:** O(N * L)*