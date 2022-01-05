# 按照另一个数组定义的顺序打印一个数组的元素|集合 2

> 原文:[https://www . geesforgeks . org/print-elements-of-a-array-按另一个数组集定义的顺序-2/](https://www.geeksforgeeks.org/print-elements-of-an-array-according-to-the-order-defined-by-another-array-set-2/)

给定两个数组 a1[]和 a2[]，以这样一种方式打印 a1 的元素，即元素之间的相对顺序与 a2 中的顺序相同。也就是说，数组 a2[]中位于前面的元素首先从数组 a1[]中打印这些元素。对于 a2 中没有的元素，最后按排序顺序打印出来。
还给出 a2[]中的元素个数小于或等于 a1[]中的元素个数，a2[]具有所有不同的元素。
**例:**

> **输入:** a1[] = {2，1，2，5，7，1，9，3，6，8，8}
> a2[] = {2，1，8，3 }
> T4】输出:2 1 8 8 3 5 6 7 9
> T7】输入: a1[] = {2，1，2，5，7，1，9，3，6，8，8}
> a2[] = {1，10，11}

**简单方法:**我们创建一个临时数组和一个访问数组，其中临时数组用于将 a1[]的内容复制到其中，访问数组用于标记临时数组中复制到 a1[]的那些元素。然后对临时数组进行排序，并对 a1[]中 a2[]的每个元素进行二分搜索法运算。你可以在这里找到解决方案[。
**高效途径:**我们可以在 O(mlog(n))时间内使用 c++中的**映射，按照 a2[]定义的顺序打印 a1[]的元素。我们遍历 a1[]并将每个数字的频率存储在地图中。然后我们遍历 a2[]，检查地图中是否有这个数字。如果数字存在，那么打印很多次，并从地图上删除该数字。将地图中剩余的数字按顺序打印出来，因为数字是按排序顺序存储在地图中的。
以下是上述方法的实施:**](https://www.geeksforgeeks.org/sort-array-according-order-defined-another-array/) 

## C++

```
// A C++ program to print an array according
// to the order defined by another array
#include <bits/stdc++.h>
using namespace std;

// Function to print an array according
// to the order defined by another array
void print_in_order(int a1[], int a2[], int n, int m)
{
    // Declaring map and iterator
    map<int, int> mp;
    map<int, int>::iterator itr;

    // Store the frequency of each
    // number of a1[] int the map
    for (int i = 0; i < n; i++)
        mp[a1[i]]++;

    // Traverse through a2[]
    for (int i = 0; i < m; i++) {
        // Check whether number
        // is present in map or not

        if (mp.find(a2[i]) != mp.end()) {
            itr = mp.find(a2[i]);

            // Print that number that
            // many times of its frequency
            for (int j = 0; j < itr->second; j++)
                cout << itr->first << " ";
            mp.erase(a2[i]);
        }
    }

    // Print those numbers that are not
    // present in a2[]
    for (itr = mp.begin(); itr != mp.end(); itr++) {
        for (int j = 0; j < itr->second; j++)
            cout << itr->first << " ";
    }

    cout << endl;
}

// Driver code
int main()
{
    int a1[] = { 2, 1, 2, 5, 7, 1, 9, 3, 6, 8, 8 };
    int a2[] = { 2, 1, 8, 3 };
    int n = sizeof(a1) / sizeof(a1[0]);
    int m = sizeof(a2) / sizeof(a2[0]);

    print_in_order(a1, a2, n, m);

    return 0;
}
```

## 蟒蛇 3

```
# A Python3 program to print an array according
# to the order defined by another array

# Function to print an array according
# to the order defined by another array
def print_in_order(a1, a2, n, m) :

    # Declaring map and iterator
    mp = dict.fromkeys(a1,0);

    # Store the frequency of each
    # number of a1[] int the map
    for i in range(n) :
        mp[a1[i]] += 1;

    # Traverse through a2[]
    for i in range(m) :
        # Check whether number
        # is present in map or not

        if a2[i] in mp.keys() :

            # Print that number that
            # many times of its frequency
            for j in range(mp[a2[i]]) :
                print(a2[i],end=" ");

            del(mp[a2[i]]);

    # Print those numbers that are not
    # present in a2[]
    for key,value in mp.items() :
        for j in range(value) :
            print(key,end=" ");

    print();

# Driver code
if __name__ == "__main__" :

    a1 = [ 2, 1, 2, 5, 7, 1, 9, 3, 6, 8, 8 ];
    a2 = [ 2, 1, 8, 3 ];
    n =len(a1);
    m = len(a2);

    print_in_order(a1, a2, n, m);

    # This code is contributed by AnkitRai01
```

**Output:** 

```
2 2 1 1 8 8 3 5 6 7 9
```