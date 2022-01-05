# 在 C++ STL 中使用 binary_search()函数搜索字符串

> 原文:[https://www . geesforgeks . org/search-string-use-binary _ search-function-in-CPP-STL/](https://www.geeksforgeeks.org/search-string-using-binary_search-function-in-cpp-stl/)

用于搜索给定字符串的内置 [STL 库函数](https://www.geeksforgeeks.org/the-c-standard-template-library-stl/)[**binary _ search()**](https://www.geeksforgeeks.org/binary-search-functions-in-c-stl-binary_search-lower_bound-and-upper_bound/)在给定字符串数组中存在或不存在。二分搜索法是一个分裂和征服的方法。[二分搜索法算法](https://www.geeksforgeeks.org/binary-search/)背后的思想是继续将数组分成两半，直到找到元素，或者所有元素都用完。将数组的中间项与目标值(即需要搜索的值)进行比较，如果匹配，则返回 true 否则，如果中间项大于目标值，则在左子数组中执行搜索。如果中间项目小于目标，则在右侧子阵列中执行搜索。

**示例:**

```
Input: arr[] = {“Geeks”, “For”, “GeeksForGeek”}
Search “Geeks”
Output: String Founded in array
```

**语法:**

```
binary_search(starting_address, ending_address, value_of_string)
```

下面是上述方法的实现:

## C++14

```
// C++ program to implement Binary
// Search in Standard Template Library (STL)
#include <algorithm>
#include <iostream>
using namespace std;

void show_array(string arr[], int arraysize)
{
    for (int i = 0; i < arraysize; i++)
        cout << arr[i] << ", ";
}

void binarySearch(string arr[], int size)
{
    cout << "\nThe array is : \n";
    show_array(arr, size);

    // Sort string array a for binary search as prerequisite
    sort(arr, arr + size);

    // Finding for "Geeks"
    cout << "\n\nSearching Result for \"Geeks\"";
    if (binary_search(arr, arr + size, "Geeks"))
        cout << "\nString Founded in array\n";
    else
        cout << "\nString not Founded in array\n";

    // Finding for string str
    string str = "Best";
    cout << "\nSearching Result for \"Best\"";
    if (binary_search(arr, arr + size, str))
        cout << "\nString Found in array";
    else
        cout << "\nString not Found in array";
}

// Driver code
int main()
{
    // Initialising string array a
    string arr[] = { "Geeks", "For", "GeeksForGeek" };

    // Find size of array arr
    int size = sizeof(arr) / sizeof(arr[0]);

    // Function call
    binarySearch(arr, size);

    return 0;
}
```

**Output:** 

```
The array is : 
Geeks, For, GeeksForGeek, 

Searching Result for "Geeks"
String Founded in array

Searching Result for "Best"
String not Found in array
```

```
***Time Complexity: O(N*log N)***
***Auxiliary Space: O(1)***
```