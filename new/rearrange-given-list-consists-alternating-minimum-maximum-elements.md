# 重新排列给定列表，使其包含交替的最小最大元素

给定一个整数列表，请重新排列该列表，使其仅使用列表操作由交替的最小最大元素**组成。 在列表中存在的所有元素中，列表的第一个元素应为最小值，第二个元素应为最大值。 同样，第三个元素将是下一个最小元素，第四个元素是下一个最大元素，依此类推。 不允许使用多余的空间。**

例子：

```
Input:  [1 3 8 2 7 5 6 4]
Output: [1 8 2 7 3 6 4 5]

Input:  [1 2 3 4 5 6 7]
Output: [1 7 2 6 3 5 4]

Input:  [1 6 2 5 3 4]
Output: [1 6 2 5 3 4]

```

想法是先按升序对列表进行排序。 然后，我们从列表末尾开始弹出元素，然后将其插入列表中的正确位置。

以下是上述想法的实现–

## C / C++

```cpp

// C++ program to rearrange a given list such that it 
// consists of alternating minimum maximum elements 
#include <bits/stdc++.h> 
using namespace std; 

// Function to rearrange a given list such that it 
// consists of alternating minimum maximum elements 
void alternateSort(list<int>& inp) 
{ 
    // sort the list in ascending order 
    inp.sort(); 

    // get iterator to first element of the list 
    list<int>::iterator it = inp.begin(); 
    it++; 

    for (int i=1; i<(inp.size() + 1)/2; i++) 
    { 
        // pop last element (next greatest) 
        int val = inp.back(); 
        inp.pop_back(); 

        // insert it after next minimum element 
        inp.insert(it, val); 

        // increment the pointer for next pair 
        ++it; 
    } 
} 

// Driver code 
int main() 
{ 
    // input list 
    list<int> inp({ 1, 3, 8, 2, 7, 5, 6, 4 }); 

    // rearrange the given list 
    alternateSort(inp); 

    // print the modified list 
    for (int i : inp) 
        cout << i << " "; 

    return 0; 
} 

```

## Java

```java

// Java program to rearrange a given list such that it 
// consists of alternating minimum maximum elements 
import java.util.*; 

class AlternateSort 
{ 
    // Function to rearrange a given list such that it 
    // consists of alternating minimum maximum elements 
    // using LinkedList 
    public static void alternateSort(LinkedList<Integer> ll)  
    { 
        Collections.sort(ll); 

        for (int i = 1; i < (ll.size() + 1)/2; i++) 
        { 
            Integer x = ll.getLast(); 
            ll.removeLast(); 
            ll.add(2*i - 1, x); 
        } 

        System.out.println(ll); 
    } 

    public static void main (String[] args) throws java.lang.Exception 
    { 
        // input list 
        Integer arr[] = {1, 3, 8, 2, 7, 5, 6, 4}; 

        // convert array to LinkedList 
        LinkedList<Integer> ll = new LinkedList<Integer>(Arrays.asList(arr)); 

        // rearrange the given list 
        alternateSort(ll); 
    } 
} 

```

## Python

```py

# Python program to rearrange a given list such that it 
# consists of alternating minimum maximum elements 
inp = [] 

# Function to rearrange a given list such that it 
# consists of alternating minimum maximum elements 
def alternateSort(): 

    global inp 

    # sort the list in ascending order 
    inp.sort() 

    # get index to first element of the list 
    it = 0
    it = it + 1

    i = 1

    while ( i < (len(inp) + 1)/2 ): 

        i = i + 1

        # pop last element (next greatest) 
        val = inp[-1] 
        inp.pop() 

        # insert it after next minimum element 
        inp.insert(it, val) 

        # increment the pointer for next pair 
        it = it + 2

# Driver code 

# input list 
inp=[ 1, 3, 8, 2, 7, 5, 6, 4 ] 

# rearrange the given list 
alternateSort() 

# print the modified list 
print (inp)  

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# program to rearrange a given list such that it 
// consists of alternating minimum maximum elements  
using System;  
using System.Collections.Generic; 

class GFG 
{ 
    // Function to rearrange a given list such that it 
    // consists of alternating minimum maximum elements 
    // using List 
    public static void alternateSort(List<int> ll)  
    { 
        ll.Sort(); 

        for (int i = 1; i < (ll.Count + 1)/2; i++) 
        { 
            int x = ll[ll.Count-1]; 
            ll.RemoveAt(ll.Count-1); 
            ll.Insert(2*i - 1, x); 
        } 
        foreach(int a in ll) 
        { 
            Console.Write(a+" "); 
        } 

    } 

    // Driver code 
    public static void Main (String[] args) 
    { 
        // input list 
        int []arr = {1, 3, 8, 2, 7, 5, 6, 4}; 

        // convert array to List 
        List<int> ll = new List<int>(arr); 

        // rearrange the given list 
        alternateSort(ll); 
    } 
} 

/* This code contributed by PrinciRaj1992 */

```

**Output:**

```
1 8 2 7 3 6 4 5

```

本文由 **Aditya Goel** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

