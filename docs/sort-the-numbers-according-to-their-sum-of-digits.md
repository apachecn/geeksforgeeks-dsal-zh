# 根据数字的总和对数字进行排序

> 原文:[https://www . geesforgeks . org/根据数字总和对数字进行排序/](https://www.geeksforgeeks.org/sort-the-numbers-according-to-their-sum-of-digits/)

给定一个非负整数 **N** 的数组 **arr[]** ，任务是根据这些整数的位数之和对它们进行排序。

**示例:**

> **输入:** arr[] = {12，10，102，31，15}
> **输出:**10 12 102 31 15
> 10 =>1+0 = 1
> 12 =>1+2 = 3
> 102 =>1+0+2 = 3
> 31 =>3+1 = 4
> 15 =>1+1
> 
> **输入:** arr[] = {14，1101，10，35，0 }
> T3】输出: 0 10 1101 14 35

**方法:**思想是将每个元素及其数字和存储在一个向量对中，然后根据存储的数字和对向量的所有元素进行排序。最后，按顺序打印元素。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the sum
// of the digits of n
int sumOfDigit(int n)
{
    int sum = 0;
    while (n > 0) {
        sum += n % 10;
        n = n / 10;
    }
    return sum;
}

// Function to sort the array according to
// the sum of the digits of elements
void sortArr(int arr[], int n)
{
    // Vector to store digit sum with respective element
    vector<pair<int, int> > vp;

    // Inserting digit sum with element in the vector pair
    for (int i = 0; i < n; i++) {
        vp.push_back(make_pair(sumOfDigit(arr[i]), arr[i]));
    }

    // Quick sort the vector, this will sort the pair
    // according to sum of the digits of elements
    sort(vp.begin(), vp.end());

    // Print the sorted vector content
    for (int i = 0; i < vp.size(); i++)
        cout << vp[i].second << " ";
}

// Driver code
int main()
{
    int arr[] = { 14, 1101, 10, 35, 0 };
    int n = sizeof(arr) / sizeof(arr[0]);
    sortArr(arr, n);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach 

# Function to return the sum 
# of the digits of n 
def sumOfDigit(n) : 

    sum = 0; 
    while (n > 0) :

        sum += n % 10; 
        n = n // 10; 

    return sum; 

# Function to sort the array according to 
# the sum of the digits of elements 
def sortArr(arr, n) :

    # Vector to store digit sum with 
    # respective element 
    vp = []; 

    # Inserting digit sum with element
    # in the vector pair 
    for i in range(n) :
        vp.append([sumOfDigit(arr[i]), arr[i]]); 

    # Quick sort the vector, this will 
    # sort the pair according to sum 
    # of the digits of elements 
    vp.sort()

    # Print the sorted vector content 
    for i in range(len(vp)) :
        print(vp[i][1], end = " "); 

# Driver code 
if __name__ == "__main__" : 

    arr = [14, 1101, 10, 35, 0]; 
    n = len(arr);
    sortArr(arr, n); 

# This code is contributed by Ryuga
```

**Output:**

```
0 10 1101 14 35

```