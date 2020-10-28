# 查找出现在第一个数组而不是第二个数组中的元素

给定两个数组，任务是我们找到第一个数组中存在但第二个数组中不存在的数字。

**范例**：

```
Input : a[] = {1, 2, 3, 4, 5, 10};
    b[] = {2, 3, 1, 0, 5};
Output : 4 10    
4 and 10 are present in first array, but
not in second array.

Input : a[] = {4, 3, 5, 9, 11};
        b[] = {4, 9, 3, 11, 10};
Output : 5  

```

**方法 1（简单）**

天真的方法是使用两个循环和检查第二个数组中不存在的元素。

## C++

```cpp

// C++ simple program to  
// find elements which are  
// not present in second array 
#include<bits/stdc++.h> 
using namespace std; 

// Function for finding  
// elements which are there  
// in a[]  but not in b[]. 
void findMissing(int a[], int b[],  
                 int n, int m) 
{ 
    for (int i = 0; i < n; i++) 
    { 
        int j; 
        for (j = 0; j < m; j++) 
            if (a[i] == b[j]) 
                break; 

        if (j == m) 
            cout << a[i] << " "; 
    } 
} 

// Driver code 
int main() 
{ 
    int a[] = { 1, 2, 6, 3, 4, 5 }; 
    int b[] = { 2, 4, 3, 1, 0 }; 
    int n = sizeof(a) / sizeof(a[0]); 
    int m = sizeof(b) / sizeof(b[1]); 
    findMissing(a, b, n, m); 
    return 0; 
} 

```

## Java

```java

// Java simple program to  
// find elements which are  
// not present in second array 
class GFG  
{ 

    // Function for finding elements  
    // which are there in a[] but not 
    // in b[]. 
    static void findMissing(int a[], int b[],  
                            int n, int m) 
    { 
        for (int i = 0; i < n; i++) 
        { 
            int j; 

            for (j = 0; j < m; j++) 
                if (a[i] == b[j]) 
                    break; 

            if (j == m) 
                System.out.print(a[i] + " "); 
        } 
    } 

    // Driver Code 
    public static void main(String[] args) 
    { 
        int a[] = { 1, 2, 6, 3, 4, 5 }; 
        int b[] = { 2, 4, 3, 1, 0 }; 

        int n = a.length; 
        int m = b.length; 

        findMissing(a, b, n, m); 
    } 
} 

// This code is contributed 
// by Anant Agarwal. 

```

## Python 3

```

# Python 3 simple program to find elements  
# which are not present in second array 

# Function for finding elements which  
# are there in a[] but not in b[]. 
def findMissing(a, b, n, m): 

    for i in range(n): 
        for j in range(m): 
            if (a[i] == b[j]): 
                break

        if (j == m - 1): 
            print(a[i], end = " ") 

# Driver code 
if __name__ == "__main__": 

    a = [ 1, 2, 6, 3, 4, 5 ] 
    b = [ 2, 4, 3, 1, 0 ] 
    n = len(a) 
    m = len(b) 
    findMissing(a, b, n, m) 

# This code is contributed  
# by ChitraNayal 

```

## C#

```cs

// C# simple program to find elements 
// which are not present in second array 
using System; 

class GFG { 

    // Function for finding elements  
    // which are there in a[] but not 
    // in b[]. 
    static void findMissing(int []a, int []b,  
                            int n, int m) 
    { 
        for (int i = 0; i < n; i++) 
        { 
            int j; 

            for (j = 0; j < m; j++) 
                if (a[i] == b[j]) 
                    break; 

            if (j == m) 
                Console.Write(a[i] + " "); 
        } 
    } 

    // Driver code 
    public static void Main() 
    { 
        int []a = {1, 2, 6, 3, 4, 5}; 
        int []b = {2, 4, 3, 1, 0}; 

        int n = a.Length; 
        int m = b.Length; 

        findMissing(a, b, n, m); 
    } 
} 

// This code is contributed by vt_m. 

```

## PHP

```php

<?php 
// PHP simple program to find  
// elements which are not  
// present in second array 

// Function for finding  
// elements which are there 
// in a[] but not in b[]. 
function findMissing( $a, $b, $n, $m) 
{ 
    for ( $i = 0; $i < $n; $i++) 
    { 
        $j; 
        for ($j = 0; $j < $m; $j++) 
            if ($a[$i] == $b[$j]) 
                break; 

        if ($j == $m) 
            echo $a[$i] , " "; 
    } 
} 

// Driver code 
$a = array( 1, 2, 6, 3, 4, 5 ); 
$b = array( 2, 4, 3, 1, 0 ); 
$n = count($a); 
$m = count($b); 
findMissing($a, $b, $n, $m); 

// This code is contributed by anuj_67\. 
?>  

```

**Output :**

```
6 5

```

**方法 2（使用哈希）**

在此方法中，我们将第二个数组的所有元素存储在哈希表中（ [unordered_set](https://www.geeksforgeeks.org/unorderd_set-stl-uses/) ）。 逐一检查第一个数组的所有元素，并打印散列表中不存在的所有那些元素。

## C++

```cpp

// C++ efficient program to  
// find elements which are not 
// present in second array 
#include<bits/stdc++.h> 
using namespace std; 

// Function for finding  
// elements which are there  
// in a[] but not in b[]. 
void findMissing(int a[], int b[],  
                 int n, int m) 
{ 
    // Store all elements of  
    // second array in a hash table 
    unordered_set <int> s; 
    for (int i = 0; i < m; i++) 
        s.insert(b[i]); 

    // Print all elements of  
    // first array that are not 
    // present in hash table 
    for (int i = 0; i < n; i++) 
        if (s.find(a[i]) == s.end()) 
            cout << a[i] << " "; 
} 

// Driver code 
int main() 
{ 
    int a[] = { 1, 2, 6, 3, 4, 5 }; 
    int b[] = { 2, 4, 3, 1, 0 }; 
    int n = sizeof(a) / sizeof(a[0]); 
    int m = sizeof(b) / sizeof(b[1]); 
    findMissing(a, b, n, m); 
    return 0; 
}  

```

## Java

```java

// Java efficient program to find elements  
// which are not present in second array  
import java.util.HashSet; 
import java.util.Set; 

public class GfG{ 

    // Function for finding elements which   
    // are there in a[] but not in b[].  
    static void findMissing(int a[], int b[],   
                     int n, int m)  
    {  
        // Store all elements of   
        // second array in a hash table  
        HashSet<Integer> s = new HashSet<>();  
        for (int i = 0; i < m; i++)  
            s.add(b[i]);  

        // Print all elements of first array  
        // that are not present in hash table  
        for (int i = 0; i < n; i++)  
            if (!s.contains(a[i])) 
                System.out.print(a[i] + " ");  
    }  

     public static void main(String []args){ 

        int a[] = { 1, 2, 6, 3, 4, 5 };  
        int b[] = { 2, 4, 3, 1, 0 };  
        int n = a.length;  
        int m = b.length;  
        findMissing(a, b, n, m); 
     } 
} 

// This code is contributed by Rituraj Jain  

```

## Python3

```py

# Python3 efficient program to find elements  
# which are not present in second array 

# Function for finding elements which  
# are there in a[] but not in b[]. 
def findMissing(a, b, n, m): 

    # Store all elements of second  
    # array in a hash table 
    s = dict() 
    for i in range(m): 
        s[b[i]] = 1

    # Print all elements of first array  
    # that are not present in hash table 
    for i in range(n): 
        if a[i] not in s.keys(): 
            print(a[i], end = " ") 

# Driver code 
a = [ 1, 2, 6, 3, 4, 5 ] 
b = [ 2, 4, 3, 1, 0 ] 
n = len(a) 
m = len(b) 
findMissing(a, b, n, m) 

# This code is contributed by mohit kumar 

```

## C#

```cs

// C# efficient program to find elements  
// which are not present in second array  
using System;  
using System.Collections.Generic; 

class GfG 
{ 

    // Function for finding elements which  
    // are there in a[] but not in b[].  
    static void findMissing(int []a, int []b,  
                    int n, int m)  
    {  
        // Store all elements of  
        // second array in a hash table  
        HashSet<int> s = new HashSet<int>();  
        for (int i = 0; i < m; i++)  
            s.Add(b[i]);  

        // Print all elements of first array  
        // that are not present in hash table  
        for (int i = 0; i < n; i++)  
            if (!s.Contains(a[i])) 
                Console.Write(a[i] + " ");  
    }  

    // Driver code 
    public static void Main(String []args) 
    { 
        int []a = { 1, 2, 6, 3, 4, 5 };  
        int []b = { 2, 4, 3, 1, 0 };  
        int n = a.Length;  
        int m = b.Length;  
        findMissing(a, b, n, m); 
    } 
} 

/* This code contributed by PrinciRaj1992 */

```

**Output :**

```
6 5

```

**时间复杂度**：O（n）

**辅助空间**：O（n）

本文由 **DANISH_RAZA** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

