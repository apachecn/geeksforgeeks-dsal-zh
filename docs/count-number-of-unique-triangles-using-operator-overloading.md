# 使用运算符重载计算唯一三角形的数量

> 原文:[https://www . geeksforgeeks . org/count-唯一三角形的数量-使用运算符-重载/](https://www.geeksforgeeks.org/count-number-of-unique-triangles-using-operator-overloading/)

给定 **N 个**三角形及其三条边的长度为 **a、b 和 c** 。任务是计算这些给定三角形中唯一三角形的数量 **N** 。如果两个三角形至少有一条边不同，那么它们就是不同的。

**示例:**

> **输入:** arr[] = {{3，1，2}，{2，1，4}，{4，5，6}，{6，5，4}，{4，5，6}，{5，4，6 } }；
> T3】输出: 3
> 
> **输入:** arr[] = {{4，5，6}，{6，5，4}，{1，2，2}，{8，9，12 } }；
> T3】输出: 3

这个问题已经在[之前的帖子](https://www.geeksforgeeks.org/count-number-of-unique-triangles-using-stl/)中使用[有序集 STL](https://www.geeksforgeeks.org/ordered-set-gnu-c-pbds/) 解决了。

**方法:**我们将讨论基于[运算符重载](https://www.geeksforgeeks.org/operator-overloading-c/)的方法来解决这个问题，我们将重载我们类的关系运算符 **(==)** 。

*   因为三角形的任意两组边，比如说{4，5，6}，{6，5，4}，如果一组中的每个元素对应于另一组中的元素，则被认为是相等的。因此，我们将检查一个集合的每个元素与另一个集合的元素，并对其进行计数。如果计数相同，这两组可以简单地认为是相等的。现在，我们已经简单地使用关系运算符比较了集合，以找到集合的唯一数量。
*   为了获得唯一集合的数量，我们可以采用一种方法，将当前集合的唯一性与其前面的集合进行比较。所以，如果有相同类型的 **k** 套，只有最后一套被认为是唯一的。

下面是上述方法的 C++实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Structure to represent a Triangle
// with three sides as a, b, c
struct Triangle {
    int a, b, c;

public:
    bool operator==(const Triangle& t) const;
};

// Function to overload relational
// operator (==)
bool Triangle::operator==(const Triangle& t) const
{
    int cnt = 0;
    if ((this->a == t.a)
        || (this->a == t.b)
        || (this->a == t.c)) {
        cnt++;
    }
    if ((this->b == t.a)
        || (this->b == t.b)
        || (this->b == t.c)) {
        cnt++;
    }
    if ((this->c == t.a)
        || (this->c == t.b)
        || (this->c == t.c)) {
        cnt++;
    }

    // If all the three elements a, b, c
    // are same, triangle is not unique
    if (cnt == 3) {
        return false;
    }

    // For unique triangle return true
    return true;
}

// Function returns the number
// of unique Triangles
int countUniqueTriangles(struct Triangle arr[],
                         int n)
{

    // Unique sets
    int uni = 0;

    for (int i = 0; i < n - 1; i++) {

        // Check on uniqueness for a
        // particular set w.r.t others
        int cnt = 0;

        for (int j = i; j < n - 1; j++) {

            // Checks if two triangles
            // are different
            if (arr[i] == arr[j + 1])
                cnt++;
        }

        // If count of unique triangles
        // is same as the number of remaining
        // triangles then, increment count
        if (cnt == n - 1 - i)
            uni++;
    }

    // Since last element that
    // remains will be unique only
    return uni + 1;
}

// Driver Code
int main()
{
    // An array of structure to
    // store sides of Triangles
    struct Triangle arr[] = {
        { 3, 2, 2 }, { 3, 4, 5 }, { 1, 2, 2 },
        { 2, 2, 3 }, { 5, 4, 3 }, { 6, 4, 5 }
    };

    int n = sizeof(arr) / sizeof(Triangle);

    // Function Call
    cout << countUniqueTriangles(arr, n);
    return 0;
}
```

**Output:**

```
4

```

**时间复杂度:***O(N)*
T5】辅助空间: *O(1)*