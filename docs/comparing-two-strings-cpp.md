# 在 C++中比较两个字符串

> 原文:[https://www.geeksforgeeks.org/comparing-two-strings-cpp/](https://www.geeksforgeeks.org/comparing-two-strings-cpp/)

给定两个字符串，如何检查两个字符串是否相等。
**例:**

```
Input  : ABCD, XYZ
Output : ABCD is not equal to XYZ
         XYZ is greater than ABCD

Input  : Geeks, forGeeks
Output : Geeks is not equal to forGeeks
         forGeeks is greater than Geeks
```

这个问题可以使用以下两种方法中的任何一种来解决

*   **C++关系运算符**

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP code to implement relational
// operators on string objects
#include <iostream>
using namespace std;

void relationalOperation(string s1, string s2)
{

    if (s1 != s2)
    {
        cout << s1 << " is not equal to " << s2 << endl;
        if (s1 > s2)
            cout << s1 << " is greater than " << s2 << endl;
        else
            cout << s2 << " is greater than " << s1 << endl;
    }
    else
        cout << s1 << " is equal to " << s2 << endl;
}

// Driver code
int main()
{
    string s1("Geeks");
    string s2("forGeeks");
    relationalOperation(s1, s2);
    string s3("Geeks");
    string s4("Geeks");
    relationalOperation(s3, s4);
    return 0;
}
```

**Output**

```
Geeks is not equal to forGeeks
forGeeks is greater than Geeks
Geeks is equal to Geeks
```

*   **标准::比较()**

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP code perform relational
// operation using compare function
#include <iostream>

using namespace std;

void compareFunction(string s1, string s2)
{
    // comparing both using inbuilt function
    int x = s1.compare(s2);

    if (x != 0) {
        cout << s1
             << " is not equal to "
             << s2 << endl;
        if (x > 0)
            cout << s1
                 << " is greater than "
                 << s2 << endl;
        else
            cout << s2
                 << " is greater than "
                 << s1 << endl;
    }
    else
        cout << s1 << " is equal to " << s2 << endl;
}

// Driver Code
int main()
{
    string s1("Geeks");
    string s2("forGeeks");
    compareFunction(s1, s2);
    string s3("Geeks");
    string s4("Geeks");
    compareFunction(s3, s4);
    return 0;
}
```

**Output**

```
Geeks is not equal to forGeeks
forGeeks is greater than Geeks
Geeks is equal to Geeks
```