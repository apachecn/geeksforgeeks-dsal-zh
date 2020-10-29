# 如何检查两个给定的集合是否不相交？

> 原文：[https://www.geeksforgeeks.org/check-two-given-sets-disjoint/](https://www.geeksforgeeks.org/check-two-given-sets-disjoint/)

给定两个数组表示的两个集合，如何检查给定的两个集合是否不相交？ 可以假定给定的数组没有重复项。

```
Input: set1[] = {12, 34, 11, 9, 3}
       set2[] = {2, 1, 3, 5}
Output: Not Disjoint
3 is common in two sets.

Input: set1[] = {12, 34, 11, 9, 3}
       set2[] = {7, 2, 1, 5}
Output: Yes, Disjoint
There is no common element in two sets.

```

有很多方法可以解决此问题，这是检查您能猜出多少解决方案的好方法。

**方法 1（简单）**

遍历第一个集合的每个元素，然后在另一个集合中搜索，如果找到任何元素，则返回 false。 如果未找到任何元素，则返回树。 该方法的时间复杂度为 O（mn）。

以下是上述想法的实现。

## C++

```cpp

// A Simple C++ program to check if two sets are disjoint 
#include<bits/stdc++.h> 
using namespace std; 

// Returns true if set1[] and set2[] are disjoint, else false 
bool areDisjoint(int set1[], int set2[], int m, int n) 
{ 
    // Take every element of set1[] and search it in set2 
    for (int i=0; i<m; i++) 
      for (int j=0; j<n; j++) 
         if (set1[i] == set2[j]) 
            return false; 

    // If no element of set1 is present in set2 
    return true; 
} 

// Driver program to test above function 
int main() 
{ 
    int set1[] = {12, 34, 11, 9, 3}; 
    int set2[] = {7, 2, 1, 5}; 
    int m = sizeof(set1)/sizeof(set1[0]); 
    int n = sizeof(set2)/sizeof(set2[0]); 
    areDisjoint(set1, set2, m, n)? cout << "Yes" : cout << " No"; 
    return 0; 
} 

```

## Java

```java

// Java program to check if two sets are disjoint 

public class disjoint1  
{ 
    // Returns true if set1[] and set2[] are  
    // disjoint, else false 
    boolean aredisjoint(int set1[], int set2[])  
    { 
         // Take every element of set1[] and  
         // search it in set2 
        for (int i = 0; i < set1.length; i++)  
        { 
            for (int j = 0; j < set2.length; j++)  
            { 
                if (set1[i] == set2[j]) 
                    return false; 
            } 
        } 
        // If no element of set1 is present in set2 
        return true; 
    } 

    // Driver program to test above function 
    public static void main(String[] args)  
    { 
        disjoint1 dis = new disjoint1(); 
        int set1[] = { 12, 34, 11, 9, 3 }; 
        int set2[] = { 7, 2, 1, 5 }; 

        boolean result = dis.aredisjoint(set1, set2); 
        if (result) 
            System.out.println("Yes"); 
        else
            System.out.println("No"); 
    } 
} 

// This code is contributed by Rishabh Mahrsee 

```

## 蟒蛇

```

# A Simple python 3 program to check 
# if two sets are disjoint 

# Returns true if set1[] and set2[] are disjoint, else false 
def areDisjoint(set1, set2, m, n): 
    # Take every element of set1[] and search it in set2 
    for i in range(0, m): 
        for j in range(0, n): 
            if (set1[i] == set2[j]): 
                return False

    # If no element of set1 is present in set2 
    return True

# Driver program 
set1 = [12, 34, 11, 9, 3] 
set2 = [7, 2, 1, 5] 
m = len(set1) 
n = len(set2) 
print("yes") if areDisjoint(set1, set2, m, n) else(" No") 

# This code ia contributed by Smitha Dinesh Semwal 

```

## C#

```cs

// C# program to check if two  
// sets are disjoint  
using System; 

class GFG 
{ 
// Returns true if set1[] and set2[]  
// are disjoint, else false  
public virtual bool aredisjoint(int[] set1,  
                                int[] set2) 
{ 
    // Take every element of set1[]  
    // and search it in set2  
    for (int i = 0; i < set1.Length; i++) 
    { 
        for (int j = 0;  
                 j < set2.Length; j++) 
        { 
            if (set1[i] == set2[j]) 
            { 
                return false; 
            } 
        } 
    } 

    // If no element of set1 is  
    // present in set2  
    return true; 
} 

// Driver Code 
public static void Main(string[] args) 
{ 
    GFG dis = new GFG(); 
    int[] set1 = new int[] {12, 34, 11, 9, 3}; 
    int[] set2 = new int[] {7, 2, 1, 5}; 

    bool result = dis.aredisjoint(set1, set2); 
    if (result) 
    { 
        Console.WriteLine("Yes"); 
    } 
    else
    { 
        Console.WriteLine("No"); 
    } 
} 
} 

// This code is contributed by Shrikant13 

```

## PHP

```php

<?php 
// A Simple PHP program to check  
// if two sets are disjoint 

// Returns true if set1[] and set2[]  
// are disjoint, else false 
function areDisjoint($set1, $set2, $m, $n) 
{ 
    // Take every element of set1[] 
    // and search it in set2 
    for ($i = 0; $i < $m; $i++) 
    for ($j = 0; $j < $n; $j++) 
        if ($set1[$i] == $set2[$j]) 
            return false; 

    // If no element of set1 is  
    // present in set2 
    return true; 
} 

// Driver Code 
$set1 = array(12, 34, 11, 9, 3); 
$set2 = array(7, 2, 1, 5); 
$m = sizeof($set1); 
$n = sizeof($set2); 
if(areDisjoint($set1, $set2, 
               $m, $n) == true) 
    echo "Yes"; 
else
    echo " No"; 

// This code is contributed 
// by Akanksha Rai 
?> 

```

**输出**：

```
Yes

```

**方法 2（使用排序和合并）**，

1.  对第一和第二组进行排序。

2.  使用合并等过程来比较元素。

以下是上述想法的实现。

## C++

```cpp

// A Simple C++ program to check if two sets are disjoint 
#include<bits/stdc++.h> 
using namespace std; 

// Returns true if set1[] and set2[] are disjoint, else false 
bool areDisjoint(int set1[], int set2[], int m, int n) 
{ 
    // Sort the given two sets 
    sort(set1, set1+m); 
    sort(set2, set2+n); 

    // Check for same elements using merge like process 
    int i = 0, j = 0; 
    while (i < m && j < n) 
    { 
        if (set1[i] < set2[j]) 
            i++; 
        else if (set2[j] < set1[i]) 
            j++; 
        else /* if set1[i] == set2[j] */
            return false; 
    } 

    return true; 
} 

// Driver program to test above function 
int main() 
{ 
    int set1[] = {12, 34, 11, 9, 3}; 
    int set2[] = {7, 2, 1, 5}; 
    int m = sizeof(set1)/sizeof(set1[0]); 
    int n = sizeof(set2)/sizeof(set2[0]); 
    areDisjoint(set1, set2, m, n)? cout << "Yes" : cout << " No"; 
    return 0; 
} 

```

## Java

```java

// Java program to check if two sets are disjoint 

import java.util.Arrays; 

public class disjoint1  
{ 
    // Returns true if set1[] and set2[] are  
    // disjoint, else false 
    boolean aredisjoint(int set1[], int set2[])  
    { 
        int i=0,j=0; 

        // Sort the given two sets 
        Arrays.sort(set1); 
        Arrays.sort(set2); 

        // Check for same elements using  
        // merge like process 
        while(i<set1.length && j<set2.length) 
        { 
            if(set1[i]<set2[j]) 
                i++; 
            else if(set1[i]>set2[j]) 
                j++; 
            else 
                return false; 

        } 
        return true; 
    } 

    // Driver program to test above function 
    public static void main(String[] args)  
    { 
        disjoint1 dis = new disjoint1(); 
        int set1[] = { 12, 34, 11, 9, 3 }; 
        int set2[] = { 7, 2, 1, 5 }; 

        boolean result = dis.aredisjoint(set1, set2); 
        if (result) 
            System.out.println("YES"); 
        else
            System.out.println("NO"); 
    } 
} 

// This code is contributed by Rishabh Mahrsee 

```

## 蟒蛇

```

# A Simple Python 3 program to check 
# if two sets are disjoint 

# Returns true if set1[] and set2[] 
# are disjoint, else false 
def areDisjoint(set1, set2, m, n): 
    # Sort the given two sets 
    set1.sort() 
    set2.sort() 

    # Check for same elements   
    # using merge like process 
    i = 0; j = 0
    while (i < m and j < n): 

        if (set1[i] < set2[j]): 
            i += 1
        elif (set2[j] < set1[i]): 
            j += 1
        else: # if set1[i] == set2[j]  
            return False
    return True

# Driver Code 
set1 = [12, 34, 11, 9, 3] 
set2 = [7, 2, 1, 5] 
m = len(set1) 
n = len(set2) 

print("Yes") if areDisjoint(set1, set2, m, n) else print("No") 

# This code is contributed by Smitha Dinesh Semwal 

```

## C#

```cs

// C# program to check if two sets are disjoint 
using System; 

public class disjoint1  
{ 
    // Returns true if set1[] and set2[] are  
    // disjoint, else false 
    Boolean aredisjoint(int []set1, int []set2)  
    { 
        int i = 0, j = 0; 

        // Sort the given two sets 
        Array.Sort(set1); 
        Array.Sort(set2); 

        // Check for same elements using  
        // merge like process 
        while(i < set1.Length && j < set2.Length) 
        { 
            if(set1[i] < set2[j]) 
                i++; 
            else if(set1[i] > set2[j]) 
                j++; 
            else
                return false; 

        } 
        return true; 
    } 

    // Driver code 
    public static void Main(String[] args)  
    { 
        disjoint1 dis = new disjoint1(); 
        int []set1 = { 12, 34, 11, 9, 3 }; 
        int []set2 = { 7, 2, 1, 5 }; 

        Boolean result = dis.aredisjoint(set1, set2); 
        if (result) 
            Console.WriteLine("YES"); 
        else
            Console.WriteLine("NO"); 
    } 
} 

// This code contributed by Rajput-Ji 

```

**输出**：

```
Yes

```

上述解决方案的时间复杂度为 O（mLogm + nLogn）。

上面的解决方案首先对两个集合进行排序，然后花费 O（m + n）的时间找到交点。 如果我们给输入集排序，那么这种方法是最好的。

**方法 3（使用排序和二进制搜索）**

与方法 1 相似。我们使用[二进制搜索](http://geeksquiz.com/binary-search/)代替线性搜索。

1.  排序第一组。

2.  遍历第二组的每个元素，并使用二进制搜索来搜索第一组的每个元素。 如果找到一个元素，则将其返回。

此方法的时间复杂度为 O（mLogm + nLogm）

**方法 4（使用二进制搜索树）**。

1.  创建自平衡二进制搜索树（ [第一组中所有元素的红色黑色](https://www.geeksforgeeks.org/red-black-tree-set-1-introduction-2/)， [AVL](https://www.geeksforgeeks.org/avl-tree-set-1-insertion/) ， [Splay](https://www.geeksforgeeks.org/splay-tree-set-1-insert/) 等）。

2.  遍历第二组的所有元素，并在上述构造的二进制搜索树中搜索每个元素。 如果找到该元素，则返回 false。

3.  如果所有元素都不存在，则返回 true。

此方法的时间复杂度为 O（mLogm + nLogm）。

**方法 5（使用散列）**

1.  创建一个空散列表。

2.  遍历第一组并将每个元素存储在哈希表中。

3.  遍历第二组并检查哈希表中是否存在任何元素。 如果存在，则返回 false，否则忽略该元素。

4.  如果哈希表中不存在第二组的所有元素，则返回 true。

以下是此方法的实现。

## C / C++

```cpp

/* C++ program to check if two sets are distinct or not */
#include<bits/stdc++.h> 
using namespace std; 

// This function prints all distinct elements 
bool areDisjoint(int set1[], int set2[], int n1, int n2) 
{ 
    // Creates an empty hashset 
    set<int> myset; 

    // Traverse the first set and store its elements in hash 
    for (int i = 0; i < n1; i++) 
        myset.insert(set1[i]); 

    // Traverse the second set and check if any element of it 
    // is already in hash or not. 
    for (int i = 0; i < n2; i++) 
        if (myset.find(set2[i]) != myset.end()) 
            return false; 

    return true; 
} 

// Driver method to test above method 
int main() 
{ 
    int set1[] = {10, 5, 3, 4, 6}; 
    int set2[] = {8, 7, 9, 3}; 

    int n1 = sizeof(set1) / sizeof(set1[0]); 
    int n2 = sizeof(set2) / sizeof(set2[0]); 
    if (areDisjoint(set1, set2, n1, n2)) 
        cout << "Yes"; 
    else
        cout << "No"; 
} 
//This article is contributed by Chhavi 

```

## Java

```java

/* Java program to check if two sets are distinct or not */
import java.util.*; 

class Main 
{ 
    // This function prints all distinct elements 
    static boolean areDisjoint(int set1[], int set2[]) 
    { 
        // Creates an empty hashset 
        HashSet<Integer> set = new HashSet<>(); 

        // Traverse the first set and store its elements in hash 
        for (int i=0; i<set1.length; i++) 
            set.add(set1[i]); 

        // Traverse the second set and check if any element of it 
        // is already in hash or not. 
        for (int i=0; i<set2.length; i++) 
            if (set.contains(set2[i])) 
                return false; 

        return true; 
    } 

    // Driver method to test above method 
    public static void main (String[] args) 
    { 
        int set1[] = {10, 5, 3, 4, 6}; 
        int set2[] = {8, 7, 9, 3}; 
        if (areDisjoint(set1, set2)) 
            System.out.println("Yes"); 
        else
            System.out.println("No"); 
    } 
} 

```

## Python3

```py

# Python3 program to  
# check if two sets are  
# distinct or not  
# This function prints  
# all distinct elements 
def areDisjoint(set1, set2,  
                n1, n2): 

  # Creates an empty hashset 
  myset = set([]) 

  # Traverse the first set  
  # and store its elements in hash 
  for i in range (n1): 
    myset.add(set1[i]) 

  # Traverse the second set  
  # and check if any element of it 
  # is already in hash or not. 
  for i in range (n2): 
    if (set2[i] in myset): 
      return False
  return True

# Driver method to test above method 
if __name__ == "__main__": 

  set1 = [10, 5, 3, 4, 6] 
  set2 = [8, 7, 9, 3] 

  n1 = len(set1) 
  n2 = len(set2) 

  if (areDisjoint(set1, set2, 
                  n1, n2)): 
    print ("Yes") 
  else: 
    print("No") 

# This code is contributed by Chitranayal

```

## C#

```cs

using System; 
using System.Collections.Generic; 

/* C# program to check if two sets are distinct or not */

public class GFG 
{ 
    // This function prints all distinct elements  
    public static bool areDisjoint(int[] set1, int[] set2) 
    { 
        // Creates an empty hashset  
        HashSet<int> set = new HashSet<int>(); 

        // Traverse the first set and store its elements in hash  
        for (int i = 0; i < set1.Length; i++) 
        { 
            set.Add(set1[i]); 
        } 

        // Traverse the second set and check if any element of it  
        // is already in hash or not.  
        for (int i = 0; i < set2.Length; i++) 
        { 
            if (set.Contains(set2[i])) 
            { 
                return false; 
            } 
        } 

        return true; 
    } 

    // Driver method to test above method  
    public static void Main(string[] args) 
    { 
        int[] set1 = new int[] {10, 5, 3, 4, 6}; 
        int[] set2 = new int[] {8, 7, 9, 3}; 
        if (areDisjoint(set1, set2)) 
        { 
            Console.WriteLine("Yes"); 
        } 
        else
        { 
            Console.WriteLine("No"); 
        } 
    } 
} 
//This code is contributed by Shrikant13 

```

**输出**：

```
No

```

在假设像 add（）和 contains（）这样的哈希集操作在`O(1)`时间内工作的情况下，上述实现的时间复杂度为 O（m + n）。

本文由 **Rajeev** 提供。 如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请写评论

