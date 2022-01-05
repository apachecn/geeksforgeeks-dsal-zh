# 找到与其他数组元素频率不同的元素

> 原文:[https://www . geeksforgeeks . org/find-具有不同于其他数组元素的频率的元素/](https://www.geeksforgeeks.org/find-the-element-having-different-frequency-than-other-array-elements/)

给定一个 N 个整数的数组。除了一个元素之外，数组中的每个元素出现的次数相同。任务是找到这个元素。

**示例:**

```
Input : arr[] = {1, 1, 2, 2, 3}
Output : 3

Input : arr[] = {0, 1, 2, 4, 4}
Output : 4

```

这个想法是使用散列表 **freq** 来存储给定元素的频率。一旦哈希表中有了频率，我们就可以遍历这个表，找到唯一不同于其他表的值。

以下是上述思路的实现:

## C++

```
// C++ program to find the element having
// different frequency than other array
// elements having same frequency
#include <bits/stdc++.h>
using namespace std;

// Function to find the element having
// different frequency from other array
// elements with same frequency
int findElement(int arr[], int n)
{
    // Store frequencies of elements
    unordered_map<int, int> freq;
    for (int i = 0; i < n; i++) {

        // increase the value by 1 for every
        // time the element occurs in an array
        freq[arr[i]]++;
    }

    // Below code is used find the only different
    // value in freq. 
    auto it = freq.begin();
    int fst_fre = it->second, fst_ele = it->first;
    if (freq.size() <= 2)
        return fst_fre;
    it++;
    int sec_fre = it->second, sec_ele = it->first;
    it++;
    int trd_fre = it->second, trd_ele = it->first;
    if (sec_fre == fst_fre && sec_fre != trd_fre)
        return trd_ele;
    if (sec_fre == trd_fre && sec_fre != fst_fre)
        return fst_ele;
    if (fst_fre == trd_fre && sec_fre != fst_fre)
        return sec_ele;

    // We reach here when first three frequencies are same
    it++;
    for (; it != freq.end(); it++) {
        if (it->second != fst_fre)
            return it->first;
    }

    return -1;
}

// Driver code
int main()
{
    int arr[] = { 0, 1, 2, 4, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << findElement(arr, n) << endl;
    return 0;
}
```

## 蟒蛇 3

```
# Python program to find the element having 
# different frequency than other array 
# elements having same frequency 

# Function for above implementation
def findElement(arr, n) :

    # Empty dictionary to hold the values
    freq = {}

    # Initialization of frequencies of each 
    # element to 0
    for i in range(0, n) :

        freq[arr[i]] = 0

    # Count of frequencies of elements
    for i in range(0, n) :

        freq[arr[i]] = freq[arr[i]] + 1

    # Storing the first value of dictionary
    trd_ele = freq[0]

    # Variable to hold the final result
    position = -1

    # Following loop iterates through the dictionary
    # and checks if frequencies are different 
    # from the frequency of the first element
    for i in freq :

        flag = freq[i]

        if trd_ele != flag :

            # Difference has been detected
            position = i
            break

    # Following lines of code checks if the first
    # element is itself the required anomaly by 
    # comparing the frequencies of first 3 elements
    fst_ele = freq[1]
    sec_ele = freq[2]

    if trd_ele != fst_ele :

        if trd_ele != sec_ele :

            for i in freq :

                # First element is the desired result
                position = i
                break

    # Final result is returned
    return position

# Driver code
arr = [ 0, 1, 2, 4, 4 ]
# Variable to store length of array
n = len(arr)
print (findElement(arr, n))

# This code is contributed by Pratik Basu 
```

**Output:**

```
4

```

时间复杂度:O(n)
辅助空间:O(n)