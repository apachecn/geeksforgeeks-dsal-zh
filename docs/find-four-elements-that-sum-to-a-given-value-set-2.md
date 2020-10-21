# 找到四个总和为给定值的元素 | 系列 2

> 原文： [https://www.geeksforgeeks.org/find-four-elements-that-sum-to-a-given-value-set-2/](https://www.geeksforgeeks.org/find-four-elements-that-sum-to-a-given-value-set-2/)

给定一个整数数组，请找到该数组中四个元素的总和等于给定值`X`的任意组合。

**例如**：

```
Input: array = {10, 2, 3, 4, 5, 9, 7, 8} 
       X = 23 
Output: 3 5 7 8
Sum of output is equal to 23, 
i.e. 3 + 5 + 7 + 8 = 23.

Input: array = {1, 2, 3, 4, 5, 9, 7, 8}
       X = 16 
Output: 1 3 5 7
Sum of output is equal to 16, 
i.e. 1 + 3 + 5 + 7 = 16.

```



在此主题的[先前文章](https://www.geeksforgeeks.org/find-four-numbers-with-sum-equal-to-given-sum/)中，我们讨论了`O(n ^ 3)`算法。 借助辅助空间，可以在`O(n ^ 2Logn)`时间内解决该问题。

**感谢它的建议方法。 以下是详细的过程。**

**方法 1 - 两个指针算法**：

**方法**：令输入数组为`A[]`。

1.  创建一个辅助数组`aux[]`并将所有可能的对的和存储在`aux[]`中。 `aux[]`的大小将为`n *(n-1) / 2`，其中`n`是`A[]`的大小。

2.  排序辅助数组`aux[]`。

3.  现在问题减少了，在`aux[]`中找到两个元素，它们的总和等于`X`。我们可以使用本文的方法 1 来高效地找到两个元素。 但是，需要注意以下重要点：

    `aux[]`的元素表示来自`A[]`的一对。 在从`aux[]`中选择两个元素时，我们必须检查两个元素是否具有共同的`A[]`元素。 例如，如果第一个元素的总和为`A[1]`和`A[2]`，第二个元素的总和为 `A[2]`和`A[4]`，则`aux[]`的这两个元素不代表输入数组`A[]`的四个不同元素。

下面是上述方法的实现：

## C++ 

```cpp

#include <bits/stdc++.h> 
using namespace std; 

// The following structure is needed 
// to store pair sums in aux[] 
class pairSum { 
public: 
    // index (int A[]) of first element in pair 
    int first; 

    // index of second element in pair 
    int sec; 

    // sum of the pair 
    int sum; 
}; 

// Following function is needed 
// for library function qsort() 
int compare(const void* a, const void* b) 
{ 
    return ( 
        (*(pairSum*)a).sum 
        - (*(pairSum*)b).sum); 
} 

// Function to check if two given pairs 
// have any common element or not 
bool noCommon(pairSum a, pairSum b) 
{ 
    if (a.first == b.first 
        || a.first == b.sec 
        || a.sec == b.first 
        || a.sec == b.sec) 
        return false; 
    return true; 
} 

// The function finds four 
// elements with given sum X 
void findFourElements( 
    int arr[], int n, int X) 
{ 
    int i, j; 

    // Create an auxiliary array 
    // to store all pair sums 
    int size = (n * (n - 1)) / 2; 
    pairSum aux[size]; 

    /* Generate all possible pairs  
from A[] and store sums  
    of all possible pairs in aux[] */
    int k = 0; 
    for (i = 0; i < n - 1; i++) { 
        for (j = i + 1; j < n; j++) { 
            aux[k].sum = arr[i] + arr[j]; 
            aux[k].first = i; 
            aux[k].sec = j; 
            k++; 
        } 
    } 

    // Sort the aux[] array using 
    // library function for sorting 
    qsort(aux, size, sizeof(aux[0]), compare); 

    // Now start two index variables 
    // from two corners of array 
    // and move them toward each other. 
    i = 0; 
    j = size - 1; 
    while (i < size && j >= 0) { 
        if ( 
            (aux[i].sum + aux[j].sum == X) 
            && noCommon(aux[i], aux[j])) { 
            cout << arr[aux[i].first] 
                 << ", " << arr[aux[i].sec] 
                 << ", " << arr[aux[j].first] 
                 << ", " << arr[aux[j].sec] 
                 << endl; 
            return; 
        } 
        else if (aux[i].sum + aux[j].sum < X) 
            i++; 
        else
            j--; 
    } 
} 

// Driver code 
int main() 
{ 
    int arr[] = { 10, 20, 30, 40, 1, 2 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    int X = 91; 
    findFourElements(arr, n, X); 
    return 0; 
} 

// This is code is contributed by rathbhupendra 

```

## C

```
// C++ program to find 4 elements
// with given sum
#include <stdio.h>
#include <stdlib.h>
 
// The following structure is
// needed to store pair sums in aux[]
struct pairSum {
 
    // index (int A[]) of first element in pair
    int first;
 
    // index of second element in pair
    int sec;
 
    // sum of the pair
    int sum;
};
 
// Following function is needed
// for library function qsort()
int compare(const void* a, const void* b)
{
    return ((*(pairSum*)a).sum - (*(pairSum*)b).sum);
}
 
// Function to check if two given
// pairs have any common element or not
bool noCommon(struct pairSum a, struct pairSum b)
{
    if (a.first == b.first || a.first == b.sec
        || a.sec == b.first || a.sec == b.sec)
        return false;
    return true;
}
 
// The function finds four
// elements with given sum X
void findFourElements(int arr[], int n, int X)
{
    int i, j;
 
    // Create an auxiliary array
    // to store all pair sums
    int size = (n * (n - 1)) / 2;
    struct pairSum aux[size];
 
    // Generate all possible pairs
    // from A[] and store sums
    // of all possible pairs in aux[]
    int k = 0;
    for (i = 0; i < n - 1; i++) {
        for (j = i + 1; j < n; j++) {
            aux[k].sum = arr[i] + arr[j];
            aux[k].first = i;
            aux[k].sec = j;
            k++;
        }
    }
 
    // Sort the aux[] array using
    // library function for sorting
    qsort(aux, size, sizeof(aux[0]), compare);
 
    // Now start two index variables
    // from two corners of array
    // and move them toward each other.
    i = 0;
    j = size - 1;
    while (i < size && j >= 0) {
        if ((aux[i].sum + aux[j].sum == X)
            && noCommon(aux[i], aux[j])) {
            printf("%d, %d, %d, %d\n", arr[aux[i].first],
                   arr[aux[i].sec], arr[aux[j].first],
                   arr[aux[j].sec]);
            return;
        }
        else if (aux[i].sum + aux[j].sum < X)
            i++;
        else
            j--;
    }
}
 
// Driver code
int main()
{
    int arr[] = { 10, 20, 30, 40, 1, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int X = 91;
    
    // Function call
    findFourElements(arr, n, X);
    return 0;
}
```

输出：

```
20, 1, 30, 40
```

请注意，以上代码仅打印四元组。 如果我们删除`return`语句并添加`i ++; j--;`，然后将四元组打印五次。 该代码可以修改为仅打印所有四元组一次。 保持这种方式以使其简单。

复杂度分析：

+   时间复杂度：`O(n ^ 2 Logn)`。
    
    步骤 1 花费`O(n ^ 2)`时间。 第二步是对大小为`O(n ^ 2)`的数组进行排序。 可以使用合并排序或堆排序或任何其他`O(nLogn)`算法在`O(n ^ 2Logn)`时间内完成排序。 第三步花费`O(n ^ 2)`时间。 因此，总体复杂度为`O(n ^ 2Logn)`。
+   辅助空间：`O(n ^ 2)`。
    
    辅助数组的大小为`O(n ^ 2)`。 辅助阵列的大尺寸可能是此方法中的一个问题。

方法 2 - 基于哈希的解决方案`O(n ^ 2)`：

方法：

+   将所有对的总和存储在哈希表中。
+   再次遍历所有对，并在哈希表中搜索`X`减当前对和。
+   如果找到具有所需总和的一对，则确保所有元素都是不同的数组元素，并且一个元素不应被视为多次。


下图是上述方法的模拟：

![](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20190702113336/FourElementsThatSumToAGivenValue1.png)

下面是上述方法的实现：

## C++

```
// A hashing based  CPP program
// to find if there are
// four elements with given sum.
#include <bits/stdc++.h>
using namespace std;
 
// The function finds four
// elements with given sum X
void findFourElements(int arr[], int n, int X)
{
    // Store sums of all pairs
    // in a hash table
    unordered_map<int, pair<int, int> > mp;
    for (int i = 0; i < n - 1; i++)
        for (int j = i + 1; j < n; j++)
            mp[arr[i] + arr[j]] = { i, j };
 
    // Traverse through all pairs and search
    // for X - (current pair sum).
    for (int i = 0; i < n - 1; i++) {
        for (int j = i + 1; j < n; j++) {
            int sum = arr[i] + arr[j];
 
            // If X - sum is present in hash table,
            if (mp.find(X - sum) != mp.end()) {
 
                // Making sure that all elements are
                // distinct array elements and an element
                // is not considered more than once.
                pair<int, int> p = mp[X - sum];
                if (p.first != i && p.first != j
                    && p.second != i && p.second != j) {
                    cout << arr[i] << ", " << arr[j] << ", "
                         << arr[p.first] << ", "
                         << arr[p.second];
                    return;
                }
            }
        }
    }
}
 
// Driver code
int main()
{
    int arr[] = { 10, 20, 30, 40, 1, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int X = 91;
    
    // Function call
    findFourElements(arr, n, X);
    return 0;
}
```

## Java

```
// A hashing based Java program to find
// if there are four elements with given sum.
import java.util.HashMap;
class GFG {
    static class pair {
        int first, second;
        public pair(int first, int second)
        {
            this.first = first;
            this.second = second;
        }
    }
 
    // The function finds four elements
    // with given sum X
    static void findFourElements(int arr[], int n, int X)
    {
        // Store sums of all pairs in a hash table
        HashMap<Integer, pair> mp
            = new HashMap<Integer, pair>();
        for (int i = 0; i < n - 1; i++)
            for (int j = i + 1; j < n; j++)
                mp.put(arr[i] + arr[j], new pair(i, j));
 
        // Traverse through all pairs and search
        // for X - (current pair sum).
        for (int i = 0; i < n - 1; i++) {
            for (int j = i + 1; j < n; j++) {
                int sum = arr[i] + arr[j];
 
                // If X - sum is present in hash table,
                if (mp.containsKey(X - sum)) {
 
                    // Making sure that all elements are
                    // distinct array elements and an
                    // element is not considered more than
                    // once.
                    pair p = mp.get(X - sum);
                    if (p.first != i && p.first != j
                        && p.second != i && p.second != j) {
                        System.out.print(
                            arr[i] + ", " + arr[j] + ", "
                            + arr[p.first] + ", "
                            + arr[p.second]);
                        return;
                    }
                }
            }
        }
    }
 
    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 10, 20, 30, 40, 1, 2 };
        int n = arr.length;
        int X = 91;
       
        // Function call
        findFourElements(arr, n, X);
    }
}
 
// This code is contributed by Princi Singh
```

## Python3

```
# A hashing based Python program to find if there are
# four elements with given summ.
 
# The function finds four elements with given summ X
 
 
def findFourElements(arr, n, X):
 
    # Store summs of all pairs in a hash table
    mp = {}
    for i in range(n - 1):
        for j in range(i + 1, n):
            mp[arr[i] + arr[j]] = [i, j]
 
    # Traverse through all pairs and search
    # for X - (current pair summ).
    for i in range(n - 1):
        for j in range(i + 1, n):
            summ = arr[i] + arr[j]
 
            # If X - summ is present in hash table,
            if (X - summ) in mp:
 
                # Making sure that all elements are
                # distinct array elements and an element
                # is not considered more than once.
                p = mp[X - summ]
                if (p[0] != i and p[0] != j and p[1] != i and p[1] != j):
                    print(arr[i], ", ", arr[j], ", ",
                          arr[p[0]], ", ", arr[p[1]], sep="")
                    return
 
 
# Driver code
arr = [10, 20, 30, 40, 1, 2]
n = len(arr)
X = 91
 
# Function call
findFourElements(arr, n, X)
 
# This is code is contributed by shubhamsingh10
```

## C#

```
// A hashing based C# program to find
// if there are four elements with given sum.
using System;
using System.Collections.Generic;
 
class GFG {
    public class pair {
        public int first, second;
        public pair(int first, int second)
        {
            this.first = first;
            this.second = second;
        }
    }
 
    // The function finds four elements
    // with given sum X
    static void findFourElements(int[] arr, int n, int X)
    {
        // Store sums of all pairs in a hash table
        Dictionary<int, pair> mp
            = new Dictionary<int, pair>();
        for (int i = 0; i < n - 1; i++)
            for (int j = i + 1; j < n; j++)
                if (mp.ContainsKey(arr[i] + arr[j]))
                    mp[arr[i] + arr[j]] = new pair(i, j);
                else
                    mp.Add(arr[i] + arr[j], new pair(i, j));
 
        // Traverse through all pairs and search
        // for X - (current pair sum).
        for (int i = 0; i < n - 1; i++) {
            for (int j = i + 1; j < n; j++) {
                int sum = arr[i] + arr[j];
 
                // If X - sum is present in hash table,
                if (mp.ContainsKey(X - sum)) {
 
                    // Making sure that all elements are
                    // distinct array elements and an
                    // element is not considered more than
                    // once.
                    pair p = mp[X - sum];
                    if (p.first != i && p.first != j
                        && p.second != i && p.second != j) {
                        Console.Write(arr[i] + ", " + arr[j]
                                      + ", " + arr[p.first]
                                      + ", "
                                      + arr[p.second]);
                        return;
                    }
                }
            }
        }
    }
 
    // Driver Code
    public static void Main(String[] args)
    {
        int[] arr = { 10, 20, 30, 40, 1, 2 };
        int n = arr.Length;
        int X = 91;
       
        // Function call
        findFourElements(arr, n, X);
    }
}
 
// This code is contributed by 29AjayKumar
```

输出：

```
20, 30, 40, 1
```

复杂度分析：

时间复杂度：`O(n ^ 2)`。

需要嵌套遍历以将所有对存储在哈希图中。

辅助空间：`O(n ^ 2)`。

所有`n * (n-1)`对都存储在哈希映射中，因此所需空间为`O(n ^ 2)`。

如果您发现上述任何代码/算法不正确，或者找到其他解决相同问题的方法，请发表评论。

方法 3 - 没有重复元素的解决方案：

方法：

+   将所有对的总和存储在哈希表中
+   再次遍历所有对，并在哈希表中搜索`X`减当前对和。
+   考虑一个最初以零存储的临时数组。 当我们得到 4 个元素的总和达到所需值时，它将变为 1。
+   如果找到具有所需总和的一对，则确保所有元素都是不同的数组元素，并检查`temp`数组中的值是否为 0，以便不考虑重复项。

下面是代码的实现：

## Java

```
// Java prgram to find four 
// elements with the given sum
import java.util.*;
 
class fourElementWithSum {
 
    // Function to find 4 elements that add up to
    // given sum
    public static void fourSum(int X, int[] arr,
                               Map<Integer, pair> map)
    {
        int[] temp = new int[arr.length];
 
        // Iterate from 0 to temp.length
        for (int i = 0; i < temp.length; i++)
            temp[i] = 0;
 
        // Iterate from 0 to arr.length
        for (int i = 0; i < arr.length - 1; i++) {
 
            // Iterate from i + 1 to arr.length
            for (int j = i + 1; j < arr.length; j++) {
 
                // Store curr_sum = arr[i] + arr[j]
                int curr_sum = arr[i] + arr[j];
 
                // Check if X - curr_sum if present
                // in map
                if (map.containsKey(X - curr_sum)) {
 
                    // Store pair having map value
                    // X - curr_sum
                    pair p = map.get(X - curr_sum);
 
                    if (p.first != i && p.sec != i
                        && p.first != j && p.sec != j
                        && temp[p.first] == 0
                        && temp[p.sec] == 0 && temp[i] == 0
                        && temp[j] == 0) {
 
                        // Print the output
                        System.out.printf(
                            "%d,%d,%d,%d", arr[i], arr[j],
                            arr[p.first], arr[p.sec]);
                        temp[p.sec] = 1;
                        temp[i] = 1;
                        temp[j] = 1;
                        break;
                    }
                }
            }
        }
    }
 
    // Program for two Sum
    public static Map<Integer, pair> twoSum(int[] nums)
    {
        Map<Integer, pair> map = new HashMap<>();
        for (int i = 0; i < nums.length - 1; i++) {
            for (int j = i + 1; j < nums.length; j++) {
                map.put(nums[i] + nums[j], new pair(i, j));
            }
        }
        return map;
    }
 
    // to store indices of two sum pair
    public static class pair {
        int first, sec;
 
        public pair(int first, int sec)
        {
            this.first = first;
            this.sec = sec;
        }
    }
 
    // Driver Code
    public static void main(String args[])
    {
        int[] arr = { 10, 20, 30, 40, 1, 2 };
        int n = arr.length;
        int X = 91;
        Map<Integer, pair> map = twoSum(arr);
       
        // Function call
        fourSum(X, arr, map);
    }
}
 
// This code is contributed by Likhita avl.
```

输出：

```
20,30,40,1
```

复杂度分析：

时间复杂度：`O(n ^ 2)`。

需要嵌套遍历以将所有对存储在哈希图中。

辅助空间：`O(n ^ 2)`。

所有`n * (n-1)`对都存储在哈希映射中，因此所需空间为`O(n ^ 2)`，临时数组采用`O(n)`，因此空间为`O(n ^ 2)`。