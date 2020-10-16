# 对排序向量中的二分搜索

> 原文： [https://www.geeksforgeeks.org/binary-search-sorted-vector-pairs/](https://www.geeksforgeeks.org/binary-search-sorted-vector-pairs/)

给定向量按其第一个值（关键字）排序的情况下，如何将 STL [`binary_search`](https://www.geeksforgeeks.org/binary-search-algorithms-the-c-standard-template-library-stl/)应用于（键，值）对的[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)

代码中的**结构比较**包含两个函数，将键（搜索元素）与向量中的第一个元素进行比较。

```

/* C++ code to demonstrate how Binary Search 
   can be applied on a vector of pairs */
#include <bits/stdc++.h> 
using namespace std; 

struct compare { 
    bool operator()(const pair<int, int>& value,  
                                const int& key) 
    { 
        return (value.first < key); 
    } 
    bool operator()(const int& key,  
                    const pair<int, int>& value) 
    { 
        return (key < value.first); 
    } 
}; 

int main() 
{ 
    // initializing the vector of pairs 
    vector<pair<int, int> > vect; 

    // insertion of pairs (key, value) in vector vect 
    vect.push_back(make_pair(1, 20)); 
    vect.push_back(make_pair(3, 42)); 
    vect.push_back(make_pair(4, 36)); 
    vect.push_back(make_pair(2, 80)); 
    vect.push_back(make_pair(7, 50)); 
    vect.push_back(make_pair(9, 20)); 
    vect.push_back(make_pair(3, 29)); 

    // sorting the vector according to key 
    sort(vect.begin(), vect.end()); 

    // printing the sorted vector 
    cout << "KEY" << '\t' << "ELEMENT" << endl; 
    for (pair<int, int>& x : vect) 
        cout << x.first << '\t' << x.second << endl; 

    // searching for the key element 3 
    cout << "search for key 3 in vector" << endl; 
    if (binary_search(vect.begin(), vect.end(), 
                                  3, compare())) 
        cout << "Element found"; 
    else
        cout << "Element not found"; 

    return 0; 
} 

```

**输出**：

```
KEY    ELEMENT
1    20
2    80
3    29
3    42
4    36
7    50
9    20
search for key 3 in vector
Element found

```

上面的`binary_search`操作具有时间复杂度`O(lg n)`。



* * *

* * *



