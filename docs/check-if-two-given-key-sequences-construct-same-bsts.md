# 检查两个给定的键序列是否构建了相同的 BSTs

> 原文:[https://www . geesforgeks . org/check-if-two-给定-key-sequence-construct-same-bsts/](https://www.geeksforgeeks.org/check-if-two-given-key-sequences-construct-same-bsts/)

给定两个数组，表示用于创建 BSt 的两个键序列。假设我们用每个数组做一个二叉查找树。我们需要在不实际构建树的情况下判断两个 BST 是否相同。

示例:

```
Let the input arrays be a[] and b[]

Example 1:
a[] = {2, 4, 1, 3} will construct following tree.
   2
 /  \
1    4
    /
   3
b[] = {2, 4, 3, 1} will also also construct the same tree.
   2
 /  \
1    4
    /
   3 
So the output is "True"

Example 2:
a[] = {8, 3, 6, 1, 4, 7, 10, 14, 13}
b[] = {8, 10, 14, 3, 6, 4, 1, 7, 13}

They both construct the same following BST, so output is "True"
            8
         /    \
       3       10
     /  \        \
    1     6       14
        /   \     /
       4     7   13  
```

1)比较两个数组的大小。如果不一样，返回 false。
2)比较两个数组的第一个值。如果不一样，返回 false。
3)从每个给定的数组创建两个列表，使得第一个列表包含的值小于对应数组的第一项。第二个列表包含更大的值。
4)递归检查第一个数组的第一个列表和第二个数组的第一个列表，对于第二个列表同样如此。

## C++

```
// C++ program to check if given two arrays represent
// same BST.

#include <bits/stdc++.h>
using namespace std;
bool sameBSTs(vector<int> aL1,
                            vector<int> aL2)
{
    // Base cases
    if (aL1.size() != aL2.size())
        return false;
    if (aL1.size() == 0)
        return true;
    if (aL1[0] != aL2[0])
        return false;

    // Construct two lists from each input array. The first
    // list contains values smaller than first value, i.e.,
    // left subtree. And second list contains right subtree.
    vector<int> aLLeft1 ;
    vector<int> aLRight1 ;
    vector<int> aLLeft2 ;
    vector<int> aLRight2 ;
    for (int i = 1; i < aL1.size(); i++)
    {
        if (aL1[i] < aL1[0])
            aLLeft1.push_back(aL1[i]);
        else
            aLRight1.push_back(aL1[i]);

        if (aL2[i] < aL2[0])
            aLLeft2.push_back(aL2[i]);
        else
            aLRight2.push_back(aL2[i]);
    }

    // Recursively compare left and right
    // subtrees.
    return sameBSTs(aLLeft1, aLLeft2) &&
        sameBSTs(aLRight1, aLRight2);
}

// Driver code
int main()
{
    vector<int> aL1;
    vector<int> aL2;
    aL1.push_back(3);
    aL1.push_back(5);
    aL1.push_back(4);
    aL1.push_back(6);
    aL1.push_back(1);
    aL1.push_back(0);
    aL1.push_back(2);

    aL2.push_back(3);
    aL2.push_back(1);
    aL2.push_back(5);
    aL2.push_back(2);
    aL2.push_back(4);
    aL2.push_back(6);
    aL2.push_back(0);

    cout << ((sameBSTs(aL1, aL2))?"true":"false")<<"\n";
    return 0;
}

// This code is contributed by Arnab Kundu
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if given two arrays represent
// same BST.
import java.util.ArrayList;
import java.util.Arrays;

public class SameBST {
    static boolean sameBSTs(ArrayList<Integer> aL1,
                            ArrayList<Integer> aL2)
    {
        // Base cases
        if (aL1.size() != aL2.size())
            return false;
        if (aL1.size() == 0)
            return true;
        if (aL1.get(0) != aL2.get(0))
            return false;

        // Construct two lists from each input array. The first
        // list contains values smaller than first value, i.e.,
        // left subtree. And second list contains right subtree.
        ArrayList<Integer> aLLeft1 = new ArrayList<Integer>();
        ArrayList<Integer> aLRight1 = new ArrayList<Integer>();
        ArrayList<Integer> aLLeft2 = new ArrayList<Integer>();
        ArrayList<Integer> aLRight2 = new ArrayList<Integer>();
        for (int i = 1; i < aL1.size(); i++) {
            if (aL1.get(i) < aL1.get(0))
                aLLeft1.add(aL1.get(i));
            else
                aLRight1.add(aL1.get(i));

            if (aL2.get(i) < aL2.get(0))
                aLLeft2.add(aL2.get(i));
            else
                aLRight2.add(aL2.get(i));
        }

        // Recursively compare left and right
        // subtrees.
        return sameBSTs(aLLeft1, aLLeft2) &&
               sameBSTs(aLRight1, aLRight2);
    }

    // Driver code
    public static void main(String[] args)
    {
        ArrayList<Integer> aL1 =
                         new ArrayList<Integer>(Arrays.
                           asList(3, 5, 4, 6, 1, 0, 2));
        ArrayList<Integer> aL2 =
                         new ArrayList<Integer>(Arrays.
                          asList(3, 1, 5, 2, 4, 6, 0));

        System.out.println(sameBSTs(aL1, aL2));
    }
}
```

## 蟒蛇 3

```
# Python3 program to check if given two arrays represent
# same BST.
def sameBSTs(aL1, aL2):

    # Base cases
    if (len(aL1) != len(aL2)):
        return False
    if (len(aL1) == 0):
        return True
    if (aL1[0] != aL2[0]):
        return False

    # Construct two lists from each input array. The first
    # list contains values smaller than first value, i.e.,
    # left subtree. And second list contains right subtree.
    aLLeft1 = []
    aLRight1 = []
    aLLeft2 = []
    aLRight2 = []
    for i in range(1, len(aL1)):
        if (aL1[i] < aL1[0]):
            aLLeft1.append(aL1[i])
        else:
            aLRight1.append(aL1[i])

        if (aL2[i] < aL2[0]):
            aLLeft2.append(aL2[i])
        else:
            aLRight2.append(aL2[i])

    # Recursively compare left and right
    # subtrees.
    return sameBSTs(aLLeft1, aLLeft2) and sameBSTs(aLRight1, aLRight2)

# Driver code
aL1 = []
aL2 = []
aL1.append(3)
aL1.append(5)
aL1.append(4)
aL1.append(6)
aL1.append(1)
aL1.append(0)
aL1.append(2)

aL2.append(3)
aL2.append(1)
aL2.append(5)
aL2.append(2)
aL2.append(4)
aL2.append(6)
aL2.append(0)

if (sameBSTs(aL1, aL2)):
    print("true")
else:
    print("false")

# This code is contributed by shubhamsingh10
```

## C#

```
// C# program to check if given
// two arrays represent same BST.
using System;
using System.Linq;
using System.Collections.Generic;

public class SameBST
{
    static bool sameBSTs(List<int> aL1,
                            List<int> aL2)
    {
        // Base cases
        if (aL1.Count != aL2.Count)
            return false;
        if (aL1.Count == 0)
            return true;
        if (aL1[0] != aL2[0])
            return false;

        // Construct two lists from each
        // input array. The first list contains
        // values smaller than first value, i.e.,
        // left subtree. And second list contains right subtree.
        List<int> aLLeft1 = new List<int>();
        List<int> aLRight1 = new List<int>();
        List<int> aLLeft2 = new List<int>();
        List<int> aLRight2 = new List<int>();
        for (int i = 1; i < aL1.Count; i++)
        {
            if (aL1[i] < aL1[0])
                aLLeft1.Add(aL1[i]);
            else
                aLRight1.Add(aL1[i]);

            if (aL2[i] < aL2[0])
                aLLeft2.Add(aL2[i]);
            else
                aLRight2.Add(aL2[i]);
        }

        // Recursively compare left and right
        // subtrees.
        return sameBSTs(aLLeft1, aLLeft2) &&
            sameBSTs(aLRight1, aLRight2);
    }

    // Driver code
    public static void Main()
    {
        int []arr1 = {3, 5, 4, 6, 1, 0, 2};
        List<int> aL1 = arr1.ToList();
        int []arr2 = {3, 1, 5, 2, 4, 6, 0};
        List<int> aL2 = arr2.ToList();

        Console.WriteLine(sameBSTs(aL1, aL2));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// javascript program to check if given two arrays represent
// same BST.

function sameBSTs(aL1, aL2)
{
    // Base cases
    if (aL1.length != aL2.length)
        return false;
    if (aL1.length == 0)
        return true;
    if (aL1[0] !== aL2[0])
        return false;

    // Construct two lists from each input array. The first
    // list contains values smaller than first value, i.e.,
    // left subtree. And second list contains right subtree.
    var aLLeft1 = [];
    var aLRight1 =[] ;
    var aLLeft2 =[];
    var aLRight2 =[];
    for (var i = 1; i < aL1.length; i++)
    {
        if (aL1[i] < aL1[0])
            aLLeft1.push(aL1[i]);
        else
            aLRight1.push(aL1[i]);

        if (aL2[i] < aL2[0])
            aLLeft2.push(aL2[i]);
        else
            aLRight2.push(aL2[i]);
    }

    // Recursively compare left and right
    // subtrees.
    if(sameBSTs(aLLeft1, aLLeft2) && sameBSTs(aLRight1, aLRight2))
    {
            return true;
    }
    return false;
}

// Driver code
var aL1 =[3, 5, 4, 6, 1, 0, 2] ;
var aL2 =[3, 1, 5, 2, 4, 6, 0];

document.write( ((sameBSTs(aL1, aL2))?"true":"false")+"<br>");

</script>
```

**Output:** 

```
true
```

**时间复杂度:** O(n * n)
请参考下方帖子获取 O(n)解决方案
[在不建树的情况下检查相同的 BST](https://www.geeksforgeeks.org/check-for-identical-bsts-without-building-the-trees/)