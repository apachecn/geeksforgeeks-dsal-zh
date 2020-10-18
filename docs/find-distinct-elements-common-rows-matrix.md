# 查找矩阵所有行共有的不同元素

> 原文： [https://www.geeksforgeeks.org/find-distinct-elements-common-rows-matrix/](https://www.geeksforgeeks.org/find-distinct-elements-common-rows-matrix/)

给定一个`n x n`矩阵。 问题是要找到矩阵所有行共有的所有不同元素。 元素可以按任何顺序打印。

**示例**：

```
Input : mat[][] = {  {2, 1, 4, 3},
                     {1, 2, 3, 2},  
                     {3, 6, 2, 3},  
                     {5, 2, 5, 3}  }
Output : 2 3

Input : mat[][] = {  {12, 1, 14, 3, 16},
                     {14, 2, 1, 3, 35},  
                     {14, 1, 14, 3, 11},  
                     {14, 25, 3, 2, 1},
                     {1, 18, 3, 21, 14}  }
Output : 1 3 14

```



**方法 1**：使用三个嵌套循环。 检查第一行的元素是否存在于所有后续行中。 `O(n ^ 3)`的时间复杂度。 可能需要额外的空间来处理重复的元素。

**方法 2**：按升序分别对矩阵的所有行进行排序。 然后对[在 3 个排序的数组中查找公共元素](https://www.geeksforgeeks.org/find-common-elements-three-sorted-arrays/)的问题应用改进的方法。 下面给出了相同的实现。

## C++

```
// C++ implementation to find distinct elements 
// common to all rows of a matrix 
#include <bits/stdc++.h> 
using namespace std; 
const int MAX = 100; 
  
// function to individually sort 
// each row in increasing order 
void sortRows(int mat[][MAX], int n) 
{ 
    for (int i=0; i<n; i++) 
        sort(mat[i], mat[i] + n); 
} 
  
// function to find all the common elements 
void findAndPrintCommonElements(int mat[][MAX], int n) 
{ 
    // sort rows individually 
    sortRows(mat, n); 
  
    // current column index of each row is stored 
    // from where the element is being searched in 
    // that row 
    int curr_index[n]; 
    memset(curr_index, 0, sizeof(curr_index)); 
    int f = 0; 
  
    for (; curr_index[0]<n; curr_index[0]++) 
    { 
        // value present at the current column index 
        // of 1st row 
        int value = mat[0][curr_index[0]]; 
  
        bool present = true; 
  
        // 'value' is being searched in all the 
        // subsequent rows 
        for (int i=1; i<n; i++) 
        { 
            // iterate through all the elements of 
            // the row from its current column index 
            // till an element greater than the 'value' 
            // is found or the end of the row is 
            // encountered 
            while (curr_index[i] < n && 
                   mat[i][curr_index[i]] <= value) 
                curr_index[i]++; 
  
            // if the element was not present at the column 
            // before to the 'curr_index' of the row 
            if (mat[i][curr_index[i]-1] != value) 
                present = false; 
  
            // if all elements of the row have 
            // been traversed 
            if (curr_index[i] == n) 
            { 
                f = 1; 
                break; 
            } 
        } 
  
        // if the 'value' is common to all the rows 
        if (present) 
            cout << value << " "; 
  
        // if any row have been completely traversed 
        // then no more common elements can be found 
        if (f == 1) 
            break; 
    } 
} 
  
// Driver program to test above 
int main() 
{ 
    int mat[][MAX] = {  {12, 1, 14, 3, 16}, 
        {14, 2, 1, 3, 35}, 
        {14, 1, 14, 3, 11}, 
        {14, 25, 3, 2, 1}, 
        {1, 18, 3, 21, 14} 
    }; 
  
    int n = 5; 
    findAndPrintCommonElements(mat, n); 
    return 0; 
}
```

## Java

```
// JAVA Code to find distinct elements 
// common to all rows of a matrix 
import java.util.*; 
  
class GFG { 
      
    // function to individually sort 
    // each row in increasing order 
    public static void sortRows(int mat[][], int n) 
    { 
        for (int i=0; i<n; i++) 
            Arrays.sort(mat[i]); 
    } 
       
    // function to find all the common elements 
    public static void findAndPrintCommonElements(int mat[][], 
                                                     int n) 
    { 
        // sort rows individually 
        sortRows(mat, n); 
       
        // current column index of each row is stored 
        // from where the element is being searched in 
        // that row 
        int curr_index[] = new int[n]; 
          
        int f = 0; 
       
        for (; curr_index[0]<n; curr_index[0]++) 
        { 
            // value present at the current column index 
            // of 1st row 
            int value = mat[0][curr_index[0]]; 
       
            boolean present = true; 
       
            // 'value' is being searched in all the 
            // subsequent rows 
            for (int i=1; i<n; i++) 
            { 
                // iterate through all the elements of 
                // the row from its current column index 
                // till an element greater than the 'value' 
                // is found or the end of the row is 
                // encountered 
                while (curr_index[i] < n && 
                       mat[i][curr_index[i]] <= value) 
                    curr_index[i]++; 
       
                // if the element was not present at the  
                // column before to the 'curr_index' of the  
               // row 
                if (mat[i][curr_index[i]-1] != value) 
                    present = false; 
       
                // if all elements of the row have 
                // been traversed 
                if (curr_index[i] == n) 
                { 
                    f = 1; 
                    break; 
                } 
            } 
       
            // if the 'value' is common to all the rows 
            if (present) 
               System.out.print(value+" "); 
       
            // if any row have been completely traversed 
            // then no more common elements can be found 
            if (f == 1) 
                break; 
        } 
    } 
      
    /* Driver program to test above function */
    public static void main(String[] args)  
    { 
        int mat[][] = {  {12, 1, 14, 3, 16}, 
                         {14, 2, 1, 3, 35}, 
                         {14, 1, 14, 3, 11}, 
                         {14, 25, 3, 2, 1}, 
                         {1, 18, 3, 21, 14} 
                                            }; 
           
            int n = 5; 
            findAndPrintCommonElements(mat, n); 
    } 
  } 
// This code is contributed by Arnav Kr. Mandal.
```

## Python3

```
# Python3 implementation to find distinct  
# elements common to all rows of a matrix 
MAX = 100
  
# function to individually sort 
# each row in increasing order 
def sortRows(mat, n): 
  
    for i in range(0, n): 
        mat[i].sort(); 
  
# function to find all the common elements 
def findAndPrintCommonElements(mat, n): 
  
    # sort rows individually 
    sortRows(mat, n) 
  
    # current column index of each row is  
    # stored from where the element is being  
    # searched in that row 
      
    curr_index = [0] * n 
    for i in range (0, n): 
        curr_index[i] = 0
          
    f = 0
  
    while(curr_index[0] < n): 
      
        # value present at the current  
        # column index of 1st row 
        value = mat[0][curr_index[0]] 
  
        present = True
  
        # 'value' is being searched in  
        # all the subsequent rows 
        for i in range (1, n): 
          
            # iterate through all the elements  
            # of the row from its current column  
            # index till an element greater than  
            # the 'value' is found or the end of  
            # the row is encountered 
            while (curr_index[i] < n and
                   mat[i][curr_index[i]] <= value): 
                curr_index[i] = curr_index[i] + 1
                  
            # if the element was not present at  
            # the column before to the 'curr_index'  
            # of the row 
            if (mat[i][curr_index[i] - 1] != value): 
                present = False
  
            # if all elements of the row have 
            # been traversed) 
            if (curr_index[i] == n): 
              
                f = 1
                break
              
        # if the 'value' is common to all the rows 
        if (present): 
            print(value, end = " ") 
  
        # if any row have been completely traversed 
        # then no more common elements can be found 
        if (f == 1): 
            break
      
        curr_index[0] = curr_index[0] + 1
  
# Driver Code 
mat = [[12, 1, 14, 3, 16], 
       [14, 2, 1, 3, 35], 
       [14, 1, 14, 3, 11], 
       [14, 25, 3, 2, 1], 
       [1, 18, 3, 21, 14]] 
  
n = 5
findAndPrintCommonElements(mat, n) 
  
# This code is contributed by iAyushRaj
```

## C#

```
// C# Code to find distinct elements  
// common to all rows of a matrix  
using System; 
  
class GFG 
{ 
  
// function to individually sort  
// each row in increasing order  
public static void sortRows(int[][] mat, int n) 
{ 
    for (int i = 0; i < n; i++) 
    { 
        Array.Sort(mat[i]); 
    } 
} 
  
// function to find all the common elements  
public static void findAndPrintCommonElements(int[][] mat,  
                                              int n) 
{ 
    // sort rows individually  
    sortRows(mat, n); 
  
    // current column index of each row is stored  
    // from where the element is being searched in  
    // that row  
    int[] curr_index = new int[n]; 
  
    int f = 0; 
  
    for (; curr_index[0] < n; curr_index[0]++) 
    { 
        // value present at the current column index  
        // of 1st row  
        int value = mat[0][curr_index[0]]; 
  
        bool present = true; 
  
        // 'value' is being searched in all the  
        // subsequent rows  
        for (int i = 1; i < n; i++) 
        { 
            // iterate through all the elements of  
            // the row from its current column index  
            // till an element greater than the 'value'  
            // is found or the end of the row is  
            // encountered  
            while (curr_index[i] < n &&  
                   mat[i][curr_index[i]] <= value) 
            { 
                curr_index[i]++; 
            } 
  
            // if the element was not present at the column  
            // before to the 'curr_index' of the row  
            if (mat[i][curr_index[i] - 1] != value) 
            { 
                present = false; 
            } 
  
            // if all elements of the row have  
            // been traversed  
            if (curr_index[i] == n) 
            { 
                f = 1; 
                break; 
            } 
        } 
  
        // if the 'value' is common to all the rows  
        if (present) 
        { 
            Console.Write(value + " "); 
        } 
  
        // if any row have been completely traversed  
        // then no more common elements can be found  
        if (f == 1) 
        { 
            break; 
        } 
    } 
} 
  
// Driver Code 
public static void Main(string[] args) 
{ 
    int[][] mat = new int[][] 
    { 
        new int[] {12, 1, 14, 3, 16}, 
        new int[] {14, 2, 1, 3, 35}, 
        new int[] {14, 1, 14, 3, 11}, 
        new int[] {14, 25, 3, 2, 1}, 
        new int[] {1, 18, 3, 21, 14} 
    }; 
  
    int n = 5; 
    findAndPrintCommonElements(mat, n); 
} 
} 
  
// This code is contributed by Shrikant13
```

输出：

```
1 3 14
```

时间复杂度：`O(n ^ 2 log n)`，大小为`n`的每一行都需要`O(n logn)`进行排序，总共有`n`行。

辅助空间：`O(n)`存储每行的当前列索引。

 

方法 3：它使用哈希的概念。 以下步骤是：

+   将第一行的元素映射到哈希表中。 让它成为哈希。
+   对于`row = 2`到`n`：
+   将当前行的每个元素映射到一个临时哈希表中。 让它成为临时的。
+   遍历哈希的元素，并检查哈希中的元素是否以临时形式存在。 如果不存在，则从哈希中删除那些元素。
+   当以这种方式处理所有行时，哈希中剩下的元素就是必需的公共元素。

## C++

```
// C++ program to find distinct elements 
// common to all rows of a matrix 
#include <bits/stdc++.h> 
using namespace std; 
  
const int MAX = 100; 
  
// function to individually sort 
// each row in increasing order 
void findAndPrintCommonElements(int mat[][MAX], int n) 
{ 
    unordered_set<int> us; 
  
    // map elements of first row 
    // into 'us' 
    for (int i=0; i<n; i++) 
        us.insert(mat[0][i]); 
  
    for (int i=1; i<n; i++) 
    { 
        unordered_set<int> temp; 
        // mapping elements of current row 
        // in 'temp' 
        for (int j=0; j<n; j++) 
            temp.insert(mat[i][j]); 
  
        unordered_set<int>:: iterator itr; 
  
        // iterate through all the elements 
        // of 'us' 
        for (itr=us.begin(); itr!=us.end(); itr++) 
  
            // if an element of 'us' is not present 
            // into 'temp', then erase that element 
            // from 'us' 
            if (temp.find(*itr) == temp.end()) 
                us.erase(*itr); 
  
        // if size of 'us' becomes 0, 
        // then there are no common elements 
        if (us.size() == 0) 
            break; 
    } 
  
    // print the common elements 
    unordered_set<int>:: iterator itr; 
    for (itr=us.begin(); itr!=us.end(); itr++) 
        cout << *itr << " "; 
} 
  
// Driver program to test above 
int main() 
{ 
    int mat[][MAX] = { {2, 1, 4, 3}, 
                       {1, 2, 3, 2}, 
                       {3, 6, 2, 3}, 
                       {5, 2, 5, 3}  }; 
    int n = 4; 
    findAndPrintCommonElements(mat, n); 
    return 0; 
}
```

## Python3

```
# Python3 program to find distinct elements 
# common to all rows of a matrix 
MAX = 100
  
# function to individually sort 
# each row in increasing order 
def findAndPrintCommonElements(mat, n): 
    us = dict() 
  
    # map elements of first row 
    # into 'us' 
    for i in range(n): 
        us[mat[0][i]] = 1
  
    for i in range(1, n): 
        temp = dict() 
          
        # mapping elements of current row 
        # in 'temp' 
        for j in range(n): 
            temp[mat[i][j]] = 1
  
        # iterate through all the elements 
        # of 'us' 
        for itr in list(us): 
  
            # if an element of 'us' is not present 
            # into 'temp', then erase that element 
            # from 'us' 
            if itr not in temp: 
                del us[itr] 
  
        # if size of 'us' becomes 0, 
        # then there are no common elements 
        if (len(us) == 0): 
            break
  
    # prthe common elements 
    for itr in list(us)[::-1]: 
        print(itr, end = " ") 
  
# Driver Code 
mat = [[2, 1, 4, 3], 
       [1, 2, 3, 2], 
       [3, 6, 2, 3], 
       [5, 2, 5, 3]] 
n = 4
findAndPrintCommonElements(mat, n) 
  
# This code is contributed by Mohit Kumar
```

输出：

```
3 2
```

时间复杂度：`O(n ^ 2)`。

空间复杂度：`O(n)`。