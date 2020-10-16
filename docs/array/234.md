# 合并 3 个排序的数组

> 原文： [https://www.geeksforgeeks.org/merge-3-sorted-arrays/](https://www.geeksforgeeks.org/merge-3-sorted-arrays/)

给定 3 个按升序排列的数组`A, B, C`，我们需要将它们按升序合并在一起并输出数组`D`。

例子：

```
Input : A = [1, 2, 3, 4, 5] 
        B = [2, 3, 4]
        C = [4, 5, 6, 7]
Output : D = [1, 2, 2, 3, 3, 4, 4, 4, 5, 5, 6, 7]

Input : A = [1, 2, 3, 5]
        B = [6, 7, 8, 9 ]
        C = [10, 11, 12]
Output: D = [1, 2, 3, 5, 6, 7, 8, 9\. 10, 11, 12]

```

**方法 1（一次两个数组）**：

我们讨论了[合并 2 个排序的数组](https://www.geeksforgeeks.org/merge-two-sorted-arrays/)。 因此，我们可以首先合并两个数组，然后将结果与第三个数组合并。 合并两个数组`O(m + n)`的时间复杂度。 因此，对于合并第三个数组，时间复杂度将变为`O(m + n + o)`。 请注意，这确实是可以解决此问题的最佳时间复杂度。

**空间复杂度**：由于我们一次合并两个数组，因此我们需要另一个数组来存储第一次合并的结果。 这将空间复杂度提高到`O(m + n)`。 注意，在计算复杂度时，保留 3 个数组的结果所需的空间将被忽略。

算法：

```
function merge(A, B)
    Let m and n be the sizes of A and B
    Let D be the array to store result

    // Merge by taking smaller element from A and B
    while i < m and j < n
        if A[i] <= B[j]
            Add A[i] to D and increment i by 1
        else Add B[j] to D and increment j by 1

    // If array A has exhausted, put elements from B
    while j < n
        Add B[j] to D and increment j by 1

    // If array B has exhausted, put elements from A
    while i < n
        Add A[j] to D and increment i by 1

    Return D

function merge_three(A, B, C)
    T = merge(A, B)
    return merge(T, C)

```

具体实现如下：

## CPP

```

// C++ program to merge three sorted arrays 
// by merging two at a time. 
#include <iostream> 
#include <vector> 
using namespace std; 

using Vector = vector<int>; 

void printVector(const Vector& a) 
{ 
    cout << "["; 
    for (auto e : a) 
        cout << e << " "; 
    cout << "]" << endl; 
} 

Vector mergeTwo(Vector& A, Vector& B) 
{ 
    // Get sizes of vectors 
    int m = A.size(); 
    int n = B.size(); 

    // Vector for storing Result 
    Vector D; 
    D.reserve(m + n); 

    int i = 0, j = 0; 
    while (i < m && j < n) { 

        if (A[i] <= B[j]) 
            D.push_back(A[i++]); 
        else
            D.push_back(B[j++]); 
    } 

    // B has exhausted 
    while (i < m) 
        D.push_back(A[i++]); 

    // A has exhausted 
    while (j < n) 
        D.push_back(B[j++]); 

    return D; 
} 

int main() 
{ 
    Vector A = { 1, 2, 3, 5 }; 
    Vector B = { 6, 7, 8, 9 }; 
    Vector C = { 10, 11, 12 }; 

    // First Merge A and B 
    Vector T = mergeTwo(A, B); 

    // Print Result after merging T with C 
    printVector(mergeTwo(T, C)); 
    return 0; 
} 

```

## Java

```java

import java.util.*; 
// Java program to merge three sorted arrays 
// by merging two at a time. 
class GFG { 

    static ArrayList<Integer> mergeTwo(List<Integer> A, 
                                       List<Integer> B) 
    { 
        // Get sizes of vectors 
        int m = A.size(); 
        int n = B.size(); 

        // ArrayList for storing Result 
        ArrayList<Integer> D = new ArrayList<Integer>(m + n); 

        int i = 0, j = 0; 
        while (i < m && j < n) { 

            if (A.get(i) <= B.get(j)) 
                D.add(A.get(i++)); 
            else
                D.add(B.get(i++)); 
        } 

        // B has exhausted 
        while (i < m) 
            D.add(A.get(i++)); 

        // A has exhausted 
        while (j < n) 
            D.add(B.get(j++)); 

        return D; 
    } 

    // Driver code 
    public static void main(String[] args) 
    { 
        Integer[] a = { 1, 2, 3, 5 }; 
        Integer[] b = { 6, 7, 8, 9 }; 
        Integer[] c = { 10, 11, 12 }; 
        List<Integer> A = Arrays.asList(a); 
        List<Integer> B = Arrays.asList(b); 
        List<Integer> C = Arrays.asList(c); 

        // First Merge A and B 
        ArrayList<Integer> T = mergeTwo(A, B); 

        // Print Result after merging T with C 
        System.out.println(mergeTwo(T, C)); 
    } 
} 

/* This code contributed by PrinciRaj1992 */

```

## Python

```

# Python program to merge three sorted arrays 
# by merging two at a time. 

def merge_two(a, b): 
    (m, n) = (len(a), len(b)) 
    i = j = 0

    # Destination Array 
    d = [] 

    # Merge from a and b together 
    while i < m and j < n: 
        if a[i] <= b[j]: 
            d.append(a[i]) 
            i += 1
        else: 
            d.append(b[j]) 
            j += 1

    # Merge from a if b has run out 
    while i < m: 
        d.append(a[i]) 
        i += 1

    # Merge from b if a has run out 
    while j < n: 
        d.append(b[j]) 
        j += 1

    return d 

def merge(a, b, c): 
    t = merge_two(a, b) 
    return merge_two(t, c) 

if __name__ == "__main__": 
    A = [1, 2, 3, 5] 
    B = [6, 7, 8, 9] 
    C = [10, 11, 12] 
    print(merge(A, B, C)) 

```

**输出**：

```
[1, 2, 3, 5, 6, 7, 8, 9, 10, 11, 12]

```

**方法 2（一次三个数组）**：

通过将三个数组合并在一起，可以提高方法 1 的空间复杂度。

```
function merge-three(A, B, C)
    Let m, n, o be size of A, B, and C
    Let D be the array to store the result

    // Merge three arrays at the same time
    while i < m and j < n and k < o
        Get minimum of A[i], B[j], C[i]
        if the minimum is from A, add it to 
           D and advance i
        else if the minimum is from B add it 
                to D and advance j
        else if the minimum is from C add it 
                to D and advance k

   // After above step at least 1 array has 
   // exhausted. Only C has exhausted
   while i < m and j < n
       put minimum of A[i] and B[j] into D
       Advance i if minimum is from A else advance j 

   // Only B has exhausted
   while i < m and k < o
       Put minimum of A[i] and C[k] into D
       Advance i if minimum is from A else advance k

   // Only A has exhausted
   while j < n and k < o
       Put minimum of B[j] and C[k] into D
       Advance j if minimum is from B else advance k

   // After above steps at least 2 arrays have 
   // exhausted
   if A and B have exhausted take elements from C
   if B and C have exhausted take elements from A
   if A and C have exhausted take elements from B

   return D

```

**复杂度**：时间复杂度为`O(m + n + o)`，因为我们一次处理了三个数组中的每个元素。 我们只需要一个数组来存储合并的结果，因此忽略此数组，空间复杂度为`O(1)`。

该算法的 C++ 和 Python 实现如下所示：

## C++ 

```cpp

// C++ program to merger three sorted arrays 
// by merging three simultaneously. 
#include <iostream> 
#include <vector> 
using namespace std; 

using Vector = vector<int>; 

void printVector(const Vector& a) 
{ 
    cout << "["; 
    for (auto e : a) { 
        cout << e << " "; 
    } 
    cout << "]" << endl; 
} 

Vector mergeThree(Vector& A, Vector& B, 
                  Vector& C) 
{ 
    int m, n, o, i, j, k; 
    // Get Sizes of three vectors 
    m = A.size(); 
    n = B.size(); 
    o = C.size(); 

    // Vector for storing output 
    Vector D; 
    D.reserve(m + n + o); 

    i = j = k = 0; 

    while (i < m && j < n && k < o) { 

        // Get minimum of a, b, c 
        int m = min(min(A[i], B[j]), C[k]); 

        // Put m in D 
        D.push_back(m); 

        // Increment i, j, k 
        if (m == A[i]) 
            i++; 
        else if (m == B[j]) 
            j++; 
        else
            k++; 
    } 

    // C has exhausted 
    while (i < m && j < n) { 
        if (A[i] <= B[j]) { 
            D.push_back(A[i]); 
            i++; 
        } 
        else { 
            D.push_back(B[j]); 
            j++; 
        } 
    } 

    // B has exhausted 
    while (i < m && k < 0) { 
        if (A[i] <= C[j]) { 
            D.push_back(A[i]); 
            i++; 
        } 
        else { 
            D.push_back(C[j]); 
            k++; 
        } 
    } 

    // A has exhausted 
    while (j < n && k < 0) { 
        if (B[j] <= C[k]) { 
            D.push_back(B[j]); 
            j++; 
        } 
        else { 
            D.push_back(C[j]); 
            k++; 
        } 
    } 

    // A and B have exhausted 
    while (k < o) 
        D.push_back(C[k++]); 

    // B and C have exhausted 
    while (i < m) 
        D.push_back(A[i++]); 

    // A and C have exhausted 
    while (j < n) 
        D.push_back(B[j++]); 

    return D; 
} 

int main() 
{ 
    Vector A = { 1, 2, 41, 52, 84 }; 
    Vector B = { 1, 2, 41, 52, 67 }; 
    Vector C = { 1, 2, 41, 52, 67, 85 }; 

    // Print Result 
    printVector(mergeThree(A, B, C)); 
    return 0; 
} 

```

## Python

```

# Python program to merge three sorted arrays 
# simultaneously.  

def merge_three(a, b, c): 
    (m, n, o) = (len(a), len(b), len(c)) 
    i = j = k = 0

    # Destination array 
    d = [] 

    while i < m and j < n and k < o: 

        # Get Minimum element 
        m = min(a[i], b[j], c[k]) 

        # Add m to D 
        d.append(m) 

        # Increment the source pointer which 
        # gives m 
        if a[i] == m: 
            i += 1
        elif b[j] == m: 
            j += 1
        elif c[k] == m: 
            k += 1

    # Merge a and b in c has exhausted 
    while i < m and j < n: 
        if a[i] <= b[k]: 
            d.append(a[i]) 
            i += 1
        else: 
            d.append(b[j]) 
            j += 1

    # Merge b and c if a has exhausted 
    while j < n and k < o: 
        if b[j] <= c[k]: 
            d.append(b[j]) 
            j += 1
        else: 
            d.append(c[k]) 
            k += 1

    # Merge a and c if b has exhausted 
    while i < m and k < o: 
        if a[i] <= c[k]: 
            d.append(a[i]) 
            i += 1
        else: 
            d.append(c[k]) 
            k += 1

    # Take elements from a if b and c 
    # have exhausted 
    while i < m: 
        d.append(a[i]) 
        i += 1

    # Take elements from b if a and c  
    # have exhausted 
    while j < n: 
        d.append(b[j]) 
        j += 1

    # Take elements from c if a and  
    # b have exhausted 
    while k < o: 
        d.append(c[k]) 
        k += 1

    return d 

if __name__ == "__main__": 
    a = [1, 2, 41, 52, 84] 
    b = [1, 2, 41, 52, 67] 
    c = [1, 2, 41, 52, 67, 85] 

    print(merge_three(a, b, c)) 

```

## Java

```java

import java.util.*; 
import java.io.*; 
import java.lang.*; 
class Sorting { 
    public static void main(String[] args) 
    { 
        int A[] = { 1, 2, 41, 52, 84 }; 
        int B[] = { 1, 2, 41, 52, 67 }; 
        int C[] = { 1, 2, 41, 52, 67, 85 }; 

        // call the function to sort and print the sorted numbers 
        merge3sorted(A, B, C); 
    } 

    // Function to merge three sorted arrays 
    // A[], B[], C[]: input arrays 
    static void merge3sorted(int A[], int B[], int C[]) 
    { 
        // creating an empty list to store sorted numbers 
        ArrayList<Integer> list = new ArrayList<Integer>(); 
        int i = 0, j = 0, k = 0; 

        // using merge concept and trying to find 
        // smallest of three while all three arrays 
        // contains at least one element 
        while (i < A.length && j < B.length && k < C.length) { 
            int a = A[i]; 
            int b = B[j]; 
            int c = C[k]; 
            if (a <= b && a <= c) { 
                list.add(a); 
                i++; 
            } 
            else if (b <= a && b <= c) { 
                list.add(b); 
                j++; 
            } 
            else { 
                list.add(c); 
                k++; 
            } 
        } 
        // next three while loop is to sort two 
        // of arrays if one of the three gets exhausted 
        while (i < A.length && j < B.length) { 
            if (A[i] < B[j]) { 
                list.add(A[i]); 
                i++; 
            } 
            else { 
                list.add(B[j]); 
                j++; 
            } 
        } 
        while (j < B.length && k < C.length) { 
            if (B[j] < C[k]) { 
                list.add(B[j]); 
                j++; 
            } 
            else { 
                list.add(C[k]); 
                k++; 
            } 
        } 
        while (i < A.length && k < C.length) { 
            if (A[i] < C[k]) { 
                list.add(A[i]); 
                i++; 
            } 
            else { 
                list.add(C[k]); 
                k++; 
            } 
        } 

        // if one of the array are left then 
        // simply appending them as there will 
        // be only largest element left 
        while (i < A.length) { 
            list.add(A[i]); 
            i++; 
        } 
        while (j < B.length) { 
            list.add(B[j]); 
            j++; 
        } 
        while (k < C.length) { 
            list.add(C[k]); 
            k++; 
        } 
        // finally print the list 
        for (Integer x : list) 
            System.out.print(x + " "); 
    } // merge3sorted closing braces 
} 

```

Output

```
[1, 1, 1, 2, 2, 2, 41, 41, 41, 52, 52, 52, 67, 67, 84, 85]

```

**注意**：虽然实现直接过程来合并两个或三个数组比较容易，但是如果我们要合并 4 个或更多数组，则过程变得很麻烦。 在这种情况下，我们应遵循[合并`K`个排序数组](https://www.geeksforgeeks.org/merge-k-sorted-arrays/)中所示的过程。



* * *

* * *



