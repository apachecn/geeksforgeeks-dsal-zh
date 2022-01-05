# 按照第一次出现的顺序对数组元素的多次出现进行分组

> 原文:[https://www . geesforgeks . org/group-数组元素的多次出现-按首次出现排序/](https://www.geeksforgeeks.org/group-multiple-occurrence-of-array-elements-ordered-by-first-occurrence/)

给定一个重复的未排序数组，任务是将多个出现的单个元素分组。分组的方式应保持所有元素首次出现的顺序。
**例:**

```
Input: arr[] = {5, 3, 5, 1, 3, 3}
Output:        {5, 5, 3, 3, 3, 1}

Input: arr[] = {4, 6, 9, 2, 3, 4, 9, 6, 10, 4}
Output:        {4, 4, 4, 6, 6, 9, 9, 2, 3, 10}
```

**简单的解决方法**就是使用嵌套循环。外部循环逐个遍历数组元素。内部循环检查这是否是第一次出现，如果是，则内部循环打印它和所有其他出现。

## C++

```
// A simple C++ program to group multiple occurrences of individual
// array elements
#include<bits/stdc++.h>
using namespace std;

// A simple method to group all occurrences of individual elements
void groupElements(int arr[], int n)
{
    // Initialize all elements as not visited
    bool *visited = new bool[n];
    for (int i=0; i<n; i++)
        visited[i] = false;

    // Traverse all elements
    for (int i=0; i<n; i++)
    {
        // Check if this is first occurrence
        if (!visited[i])
        {
            // If yes, print it and all subsequent occurrences
            cout << arr[i] << " ";
            for (int j=i+1; j<n; j++)
            {
                if (arr[i] == arr[j])
                {
                    cout << arr[i] << " ";
                    visited[j] = true;
                }
            }
        }
    }

    delete [] visited; 
}

/* Driver program to test above function */
int main()
{
    int arr[] = {4, 6, 9, 2, 3, 4, 9, 6, 10, 4};
    int n = sizeof(arr)/sizeof(arr[0]);
    groupElements(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A simple Java program to group
// multiple occurrences of individual
// array elements

class GFG
{

    // A simple method to group all occurrences
    // of individual elements
    static void groupElements(int arr[], int n)
    {

        // Initialize all elements as not visited
        boolean visited[] = new boolean[n];
        for (int i = 0; i < n; i++)
        {
            visited[i] = false;
        }

        // Traverse all elements
        for (int i = 0; i < n; i++)
        {

            // Check if this is first occurrence
            if (!visited[i])
            {

                // If yes, print it and all
                // subsequent occurrences
                System.out.print(arr[i] + " ");
                for (int j = i + 1; j < n; j++)
                {
                    if (arr[i] == arr[j])
                    {
                        System.out.print(arr[i] + " ");
                        visited[j] = true;
                    }
                }
            }
        }
    }

    /* Driver code */
    public static void main(String[] args)
    {
        int arr[] = {4, 6, 9, 2, 3, 4,
                        9, 6, 10, 4};
        int n = arr.length;
        groupElements(arr, n);
    }
}

// This code is contributed by Rajput-JI
```

## 蟒蛇 3

```
# A simple Python 3 program to
# group multiple occurrences of
# individual array elements

# A simple method to group all
# occurrences of individual elements
def groupElements(arr, n):

    # Initialize all elements
    # as not visited
    visited = [False] * n
    for i in range(0, n):
        visited[i] = False

    # Traverse all elements
    for i in range(0, n):

        # Check if this is
        # first occurrence
        if (visited[i] == False):

            # If yes, print it and
            # all subsequent occurrences
            print(arr[i], end = " ")
            for j in range(i + 1, n):

                if (arr[i] == arr[j]):

                    print(arr[i], end = " ")
                    visited[j] = True

# Driver Code
arr = [4, 6, 9, 2, 3,
       4, 9, 6, 10, 4]
n = len(arr)
groupElements(arr, n)

# This code is contributed
# by Smitha
```

## C#

```
// A simple C# program to group
// multiple occurrences of individual
// array elements
using System;

class GFG
{

    // A simple method to group all occurrences
    // of individual elements
    static void groupElements(int []arr, int n)
    {

        // Initialize all elements as not visited
        bool []visited = new bool[n];
        for (int i = 0; i < n; i++)
        {
            visited[i] = false;
        }

        // Traverse all elements
        for (int i = 0; i < n; i++)
        {

            // Check if this is first occurrence
            if (!visited[i])
            {

                // If yes, print it and all
                // subsequent occurrences
                Console.Write(arr[i] + " ");
                for (int j = i + 1; j < n; j++)
                {
                    if (arr[i] == arr[j])
                    {
                        Console.Write(arr[i] + " ");
                        visited[j] = true;
                    }
                }
            }
        }
    }

    /* Driver code */
    public static void Main(String[] args)
    {
        int []arr = {4, 6, 9, 2, 3, 4,
                        9, 6, 10, 4};
        int n = arr.Length;
        groupElements(arr, n);
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program to group
// multiple occurrences of individual
// array elements

    // A simple method to group all occurrences
    // of individual elements
    function groupElements(arr, n)
    {

        // Initialize all elements as not visited
        let visited = Array(n).fill(0);
        for (let i = 0; i < n; i++)
        {
            visited[i] = false;
        }

        // Traverse all elements
        for (let i = 0; i < n; i++)
        {

            // Check if this is first occurrence
            if (!visited[i])
            {

                // If yes, prlet it and all
                // subsequent occurrences
                document.write(arr[i] + " ");
                for (let j = i + 1; j < n; j++)
                {
                    if (arr[i] == arr[j])
                    {
                        document.write(arr[i] + " ");
                        visited[j] = true;
                    }
                }
            }
        }
    }

// Driver program

      let arr = [ 4, 6, 9, 2, 3, 4,
                        9, 6, 10, 4];
        let n = arr.length;
        groupElements(arr, n);

</script>
```

**输出:**

```
4 4 4 6 6 9 9 2 3 10
```

上述方法的时间复杂度为 O(n <sup>2</sup> )。
**基于二叉查找树的方法:**使用像[红黑树](https://www.geeksforgeeks.org/red-black-tree-set-1-introduction-2/)或 [AVL 树](https://www.geeksforgeeks.org/avl-tree-set-1-insertion/)这样的自平衡二叉查找树，时间复杂度可以提高到 0(nLogn)。下面是完整的算法。
1)创建一个空的二叉查找树(BST)。每个 BST 节点都将包含一个数组元素及其计数。
2)遍历输入数组，并对每个元素执行以下操作。
……..a)如果元素不在 BST 中，则插入它，计数为 0。
……..b)如果元素存在，则递增相应 BST 节点中的计数。
3)再次遍历数组，并对每个元素执行以下操作。
……..如果元素存在于 BST 中，则执行以下操作
……。a)获取其计数并打印元素“计数”次数。
……。b)从 BST 中删除该元素。
上述解决方案的时间复杂度为 O(nLogn)。
**基于哈希的方法:**我们也可以使用哈希。这个想法是用上述算法中的哈希映射来代替二叉查找树。
下面是基于哈希的解决方案的实现。

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Java program to group multiple occurrences of individual array elements */
import java.util.HashMap;

class Main
{
    // A hashing based method to group all occurrences of individual elements
    static void orderedGroup(int arr[])
    {
        // Creates an empty hashmap
        HashMap<Integer, Integer> hM = new HashMap<Integer, Integer>();

        // Traverse the array elements, and store count for every element
        // in HashMap
        for (int i=0; i<arr.length; i++)
        {
           // Check if element is already in HashMap
           Integer prevCount = hM.get(arr[i]);
           if (prevCount == null)
                prevCount = 0;

           // Increment count of element element in HashMap
           hM.put(arr[i], prevCount + 1);
        }

        // Traverse array again
        for (int i=0; i<arr.length; i++)
        {
            // Check if this is first occurrence
            Integer count =  hM.get(arr[i]);    
            if (count != null)
            {
                // If yes, then print the element 'count' times
                for (int j=0; j<count; j++)
                   System.out.print(arr[i] + " ");

                // And remove the element from HashMap.
                hM.remove(arr[i]);
            }
        }
    }

    // Driver method to test above method
    public static void main (String[] args)
    {
        int arr[] = {10, 5, 3, 10, 10, 4, 1, 3};
        orderedGroup(arr);
    }
}
```

## 蟒蛇 3

```
# Python3 program to group multiple
# occurrences of individual array elements

# A hashing based method to group
# all occurrences of individual elements
def orderedGroup(arr):

    # Creates an empty hashmap
    hM = {}

    # Traverse the array elements, and store
    # count for every element in HashMap
    for i in range(0, len(arr)):

        # Increment count of elements
        # in HashMap
        hM[arr[i]] = hM.get(arr[i], 0) + 1

    # Traverse array again
    for i in range(0, len(arr)):

        # Check if this is first occurrence
        count = hM.get(arr[i], None)    
        if count != None:

            # If yes, then print
            # the element 'count' times
            for j in range(0, count):
                print(arr[i], end = " ")

            # And remove the element from HashMap.
            del hM[arr[i]]

# Driver Code
if __name__ == "__main__":

    arr = [10, 5, 3, 10, 10, 4, 1, 3]
    orderedGroup(arr)

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to group multiple occurrences
// of individual array elements
using System;
using System.Collections.Generic;

class GFG
{

// A hashing based method to group
// all occurrences of individual elements
static void orderedGroup(int []arr)
{
    // Creates an empty hashmap
    Dictionary<int,
               int> hM = new Dictionary<int,
                                        int>();

    // Traverse the array elements,
    // and store count for every element in HashMap
    for (int i = 0; i < arr.Length; i++)
    {
        // Check if element is already in HashMap
        int prevCount = 0;
        if (hM.ContainsKey(arr[i]))
                prevCount = hM[arr[i]];

        // Increment count of element element in HashMap
        if (hM.ContainsKey(arr[i]))
            hM[arr[i]] = prevCount + 1;
        else
            hM.Add(arr[i], prevCount + 1);
    }

    // Traverse array again
    for (int i = 0; i < arr.Length; i++)
    {
        // Check if this is first occurrence
        int count = 0;
        if (hM.ContainsKey(arr[i]))
            count = hM[arr[i]];
        if (count != 0)
        {
            // If yes, then print the
            // element 'count' times
            for (int j = 0; j < count; j++)
            Console.Write(arr[i] + " ");

            // And remove the element from HashMap.
            hM.Remove(arr[i]);
        }
    }
}

// Driver Code
public static void Main (String[] args)
{
    int []arr = {10, 5, 3, 10, 10, 4, 1, 3};
    orderedGroup(arr);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

      // JavaScript program to group multiple occurrences
      // of individual array elements
      // A hashing based method to group
      // all occurrences of individual elements
      function orderedGroup(arr) {
        // Creates an empty hashmap
        var hM = {};

        // Traverse the array elements,
        // and store count for every element in HashMap
        for (var i = 0; i < arr.length; i++) {
          // Check if element is already in HashMap
          var prevCount = 0;
          if (hM.hasOwnProperty(arr[i])) prevCount = hM[arr[i]];

          // Increment count of element element in HashMap
          if (hM.hasOwnProperty(arr[i])) hM[arr[i]] = prevCount + 1;
          else hM[arr[i]] = prevCount + 1;
        }

        // Traverse array again
        for (var i = 0; i < arr.length; i++) {
          // Check if this is first occurrence
          var count = 0;
          if (hM.hasOwnProperty(arr[i])) count = hM[arr[i]];
          if (count !== 0) {
            // If yes, then print the
            // element 'count' times
            for (var j = 0; j < count; j++)
            document.write(arr[i] + " ");

            // And remove the element from HashMap.
            delete hM[arr[i]];
          }
        }
      }

      // Driver Code
      var arr = [10, 5, 3, 10, 10, 4, 1, 3];
      orderedGroup(arr);

</script>
```

**输出:**

```
10 10 10 5 3 3 4 1 
```

假设 HashMap 上的插入、搜索和删除操作花费 O(1)个时间，上述基于散列的解决方案的时间复杂度为θ(n)。
下面是字符串的相关问题。
[根据第一次出现](https://www.geeksforgeeks.org/group-occurrences-characters-according-first-appearance/)
对所有出现的人物进行分组本文由**希曼舒·古普塔**供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。