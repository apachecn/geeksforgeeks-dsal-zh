# 来自另一个数组的每个数组元素的最接近的较大元素

> 原文： [https://www.geeksforgeeks.org/closest-greater-element-every-array-element-another-array/](https://www.geeksforgeeks.org/closest-greater-element-every-array-element-another-array/)

给定两个数组`a[]`和`b[]`，我们需要构建一个数组`c[]`，使得`c[]`的每个元素`c[i]`都包含`a[]`中的一个值，该值大于`b[i]`并且最接近`b[i]`。 如果`a[]`的元素不大于`b[i]`，则`c[i]`的值为 -1。 所有数组的大小相同。

**示例**：

```
Input : a[] = [ 2, 6, 5, 7, 0]  
        b[] = [1, 3, 2, 5, 8]
Output : c[] = [2, 5, 5, 7, -1]

Input : a[] = [ 2, 6, 5, 7, 0]   
        b[] = [0, 2, 3, 5, 1]
Output : c[] = [2, 5, 5, 6, 2]

```



**朴素的方法**：对于`b[]`中的每个元素，我们遍历整个`a[]`并尝试查找最接近的较大元素，并保存每次搜索的结果。 这将花费`O(n ^ 2)`的时间复杂度。

**有效方法**：对数组`a[]`进行排序，并对每个`b[i]`在排序后的数组`a[]`中应用[二分搜索](https://www.geeksforgeeks.org/binary-search/)。 对于这种方法，我们的时间复杂度将为`O(nLogn)`。

**注意**：对于最接近的较大元素，我们可以使用[`upper_bound()`](https://www.geeksforgeeks.org/stdupper_bound-in-cpp/)。

下面是实现。

## C++ 

```cpp

// CPP to find result from target array 
// for closest element 
#include <bits/stdc++.h> 
using namespace std; 

// Function for printing resultant array 
void closestResult(int a[], int b[], int n) 
{ 
    // change arr[] to vector 
    vector<int> vect(a, a + n); 

    // sort vector for ease 
    sort(vect.begin(), vect.end()); 

    // iterator for upper_bound 
    vector<int>::iterator up; 

    // vector for result 
    vector<int> c; 

    // calculate resultant array 
    for (int i = 0; i < n; i++) { 

        // check upper bound element 
        up = upper_bound(vect.begin(), vect.end(), b[i]); 

        // if no element found push -1 
        if (up == vect.end()) 
            c.push_back(-1); 

        // Else push the element 
        else
            c.push_back(*up); // add to resultant 
    } 

    cout << "Result = "; 
    for (auto it = c.begin(); it != c.end(); it++) 
        cout << *it << " "; 
} 

// driver program 
int main() 
{ 
    int a[] = { 2, 5, 6, 1, 8, 9 }; 
    int b[] = { 2, 1, 0, 5, 4, 9 }; 
    int n = sizeof(a) / sizeof(a[0]); 
    closestResult(a, b, n); 
    return 0; 
} 

```

## Java

```java

// Java to find result from target array  
// for closest element 
import java.util.*; 

class GFG  
{ 

    // Function for printing resultant array 
    static void closestResult(Integer[] a,  
                              int[] b, int n)  
    { 

        // change arr[] to Set 
        TreeSet<Integer> vect = new TreeSet<>(Arrays.asList(a)); 

        // vector for result 
        Vector<Integer> c = new Vector<>(); 

        // calculate resultant array 
        for (int i = 0; i < n; i++)  
        { 

            // check upper bound element 
            Integer up = vect.higher(b[i]); 

            // if no element found push -1 
            if (up == null) 
                c.add(-1); 

            // Else push the element 
            else
                c.add(up); // add to resultant 
        } 

        System.out.print("Result = "); 
        for (int i : c) 
            System.out.print(i + " "); 
    } 

    // Driver Code 
    public static void main(String[] args)  
    { 
        Integer[] a = { 2, 5, 6, 1, 8, 9 }; 
        int[] b = { 2, 1, 0, 5, 4, 9 }; 
        int n = a.length; 

        closestResult(a, b, n); 
    } 
} 

// This code is contributed by 
// sanjeev2552 

```

## Python3

```py

# Python implementation to find result 
# from target array for closest element 

import bisect 

# Function for printing resultant array 
def closestResult(a, b, n): 

    # sort list for ease 
    a.sort() 

    # list for result 
    c = [] 

    # calculate resultant array 
    for i in range(n): 

        # check location of upper bound element 
        up = bisect.bisect_right(a, b[i]) 

        # if no element found push -1 
        if up == n: 
            c.append(-1) 

        # else puch the element 
        else: 
            c.append(a[up]) # add to resultant 

    print("Result = ", end = "") 
    for i in c: 
        print(i, end = " ") 

# Driver code 
if __name__ == "__main__": 
    a = [2,5,6,1,8,9] 
    b = [2,1,0,5,4,9] 
    n = len(a) 
    closestResult(a, b, n) 

# This code is contributed by 
# sanjeev2552 

```

**输出**：

```
Result = 5 2 1 6 5 -1

```



* * *

* * *



