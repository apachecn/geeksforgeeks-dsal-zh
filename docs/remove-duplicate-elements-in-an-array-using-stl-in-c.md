# 在 C++中使用 STL 移除数组中的重复元素

> 原文:[https://www . geesforgeks . org/remove-replicate-elements-in-a-array-use-STL-in-c/](https://www.geeksforgeeks.org/remove-duplicate-elements-in-an-array-using-stl-in-c/)

给定一个数组，任务是使用 C++中的 STL 从数组中移除重复的元素

**示例:**

```
Input: arr[] = {2, 2, 2, 2, 2}
Output: arr[] = {2}

Input: arr[] = {1, 2, 2, 3, 4, 4, 4, 5, 5}
Output: arr[] = {1, 2, 3, 4, 5}

```

**进场:**

这可以使用标准模板库中设置的来完成。[在](https://www.geeksforgeeks.org/set-in-cpp-stl/) [STL](https://www.geeksforgeeks.org/the-c-standard-template-library-stl/) 中设置类型变量，当我们在其中存储元素时，自动移除复制元素。

下面是上述方法的实现:

```
// C++ program to remove the
// duplicate elements from the array
// using STL in C++

#include <bits/stdc++.h>
using namespace std;

// Function to remove duplicate elements
void removeDuplicates(int arr[], int n)
{

    int i;

    // Initialise a set
    // to store the array values
    set<int> s;

    // Insert the array elements
    // into the set
    for (i = 0; i < n; i++) {

        // insert into set
        s.insert(arr[i]);
    }

    set<int>::iterator it;

    // Print the array with duplicates removed
    cout << "\nAfter removing duplicates:\n";
    for (it = s.begin(); it != s.end(); ++it)
        cout << *it << ", ";
    cout << '\n';
}

// Driver code
int main()
{
    int arr[] = { 4, 2, 3, 3, 2, 4 };

    int n = sizeof(arr) / sizeof(arr[0]);

    // Print array
    cout << "\nBefore removing duplicates:\n";
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";

    // call removeDuplicates()
    removeDuplicates(arr, n);

    return 0;
}
```

**Output:**

```
Before removing duplicates:
4 2 3 3 2 4 
After removing duplicates:
2, 3, 4,

```