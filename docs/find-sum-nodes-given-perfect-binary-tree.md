# 求给定完美二叉树所有节点的和

> 原文:[https://www . geesforgeks . org/find-sum-nodes-given-perfect-二叉树/](https://www.geeksforgeeks.org/find-sum-nodes-given-perfect-binary-tree/)

给定一个正整数 L，它代表完美二叉树的层数。假设这个完美二叉树中的叶节点从 1 到 n 开始编号，其中 n 是叶节点的数量。父节点是两个子节点的总和。我们的任务是编写一个程序来打印这个完美二叉树所有节点的总和。
**例:**

```
Input : L = 3
Output : 30
Explanation : Tree will be - 10
                            /   \
                           3     7
                          /  \  /  \
                         1   2  3   4

Input : L = 2
Output : 6
Explanation : Tree will be -  3
                            /   \
                           1     2
```

**天真法**:最简单的解决方法是先生成完美二叉树所有节点的值，然后计算所有节点的和。我们可以首先生成所有的叶节点，然后以自下而上的方式生成其余的节点。我们知道，在一棵完美的二叉树中，叶节点的数量可以由 2 <sup>L-1</sup> 给出，其中 L 是层数。当我们从底部向上移动时，完美二叉树中的节点数量将减少一半。
以下是以上想法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;

// function to find sum of all of the nodes
// of given perfect binary tree
int sumNodes(int l)
{
    // no of leaf nodes
    int leafNodeCount = pow(2, l - 1);

    // list of vector to store nodes of
    // all of the levels
    vector<int> vec[l];

    // store the nodes of last level
    // i.e., the leaf nodes
    for (int i = 1; i <= leafNodeCount; i++)
        vec[l - 1].push_back(i);

    // store nodes of rest of the level
    // by moving in bottom-up manner
    for (int i = l - 2; i >= 0; i--) {
        int k = 0;

        // loop to calculate values of parent nodes
        // from the children nodes of lower level
        while (k < vec[i + 1].size() - 1) {

            // store the value of parent node as
            // sum of children nodes
            vec[i].push_back(vec[i + 1][k] +
                             vec[i + 1][k + 1]);
            k += 2;
        }
    }

    int sum = 0;

    // traverse the list of vector
    // and calculate the sum
    for (int i = 0; i < l; i++) {
        for (int j = 0; j < vec[i].size(); j++)
            sum += vec[i][j];
    }

    return sum;
}

// Driver Code
int main()
{
    int l = 3;

    cout << sumNodes(l);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG
{

// function to find sum of
// all of the nodes of given
// perfect binary tree
static int sumNodes(int l)
{
    // no of leaf nodes
    int leafNodeCount = (int)Math.pow(2, l - 1);

    // list of vector to store
    // nodes of all of the levels
    Vector<Vector
          <Integer>> vec = new Vector<Vector
                                     <Integer>>();

    //initialize
    for (int i = 1; i <= l; i++)
    vec.add(new Vector<Integer>());

    // store the nodes of last level
    // i.e., the leaf nodes
    for (int i = 1;
             i <= leafNodeCount; i++)
        vec.get(l - 1).add(i);

    // store nodes of rest of
    // the level by moving in
    // bottom-up manner
    for (int i = l - 2; i >= 0; i--)
    {
        int k = 0;

        // loop to calculate values
        // of parent nodes from the
        // children nodes of lower level
        while (k < vec.get(i + 1).size() - 1)
        {

            // store the value of parent
            // node as sum of children nodes
            vec.get(i).add(vec.get(i + 1).get(k) +
                           vec.get(i + 1).get(k + 1));
            k += 2;
        }
    }

    int sum = 0;

    // traverse the list of vector
    // and calculate the sum
    for (int i = 0; i < l; i++)
    {
        for (int j = 0;
                 j < vec.get(i).size(); j++)
            sum += vec.get(i).get(j);
    }

    return sum;
}

// Driver Code
public static void main(String args[])
{
    int l = 3;

    System.out.println(sumNodes(l));
}
}

// This code is contributed
// by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to implement the
# above approach

# function to find Sum of all of the
# nodes of given perfect binary tree
def SumNodes(l):

    # no of leaf nodes
    leafNodeCount = pow(2, l - 1)

    # list of vector to store nodes of
    # all of the levels
    vec = [[] for i in range(l)]

    # store the nodes of last level
    # i.e., the leaf nodes
    for i in range(1, leafNodeCount + 1):
        vec[l - 1].append(i)

    # store nodes of rest of the level
    # by moving in bottom-up manner
    for i in range(l - 2, -1, -1):
        k = 0

        # loop to calculate values of parent nodes
        # from the children nodes of lower level
        while (k < len(vec[i + 1]) - 1):

            # store the value of parent node as
            # Sum of children nodes
            vec[i].append(vec[i + 1][k] +
                          vec[i + 1][k + 1])
            k += 2

    Sum = 0

    # traverse the list of vector
    # and calculate the Sum
    for i in range(l):
        for j in range(len(vec[i])):
            Sum += vec[i][j]

    return Sum

# Driver Code
if __name__ == '__main__':
    l = 3

    print(SumNodes(l))

# This code is contributed by PranchalK
```

## C#

```
using System;
using System.Collections.Generic;

// C# program to implement 
// the above approach
public class GFG
{

// function to find sum of 
// all of the nodes of given
// perfect binary tree 
public static int sumNodes(int l)
{
    // no of leaf nodes 
    int leafNodeCount = (int)Math.Pow(2, l - 1);

    // list of vector to store 
    // nodes of all of the levels 
    List<List<int>> vec = new List<List<int>>();

    //initialize
    for (int i = 1; i <= l; i++)
    {
    vec.Add(new List<int>());
    }

    // store the nodes of last level 
    // i.e., the leaf nodes 
    for (int i = 1; i <= leafNodeCount; i++)
    {
        vec[l - 1].Add(i);
    }

    // store nodes of rest of 
    // the level by moving in 
    // bottom-up manner 
    for (int i = l - 2; i >= 0; i--)
    {
        int k = 0;

        // loop to calculate values 
        // of parent nodes from the
        // children nodes of lower level 
        while (k < vec[i + 1].Count - 1)
        {

            // store the value of parent
            // node as sum of children nodes 
            vec[i].Add(vec[i + 1][k] + vec[i + 1][k + 1]);
            k += 2;
        }
    }

    int sum = 0;

    // traverse the list of vector 
    // and calculate the sum 
    for (int i = 0; i < l; i++)
    {
        for (int j = 0; j < vec[i].Count; j++)
        {
            sum += vec[i][j];
        }
    }

    return sum;
}

// Driver Code 
public static void Main(string[] args)
{
    int l = 3;

    Console.WriteLine(sumNodes(l));
}
}

  // This code is contributed by Shrikant13
```

## java 描述语言

```
<script>
    // Javascript program to implement the above approach

    // function to find sum of
    // all of the nodes of given
    // perfect binary tree
    function sumNodes(l)
    {
        // no of leaf nodes
        let leafNodeCount = Math.pow(2, l - 1);

        // list of vector to store
        // nodes of all of the levels
        let vec = [];

        //initialize
        for (let i = 1; i <= l; i++)
        {
            vec.push([]);
        }

        // store the nodes of last level
        // i.e., the leaf nodes
        for (let i = 1; i <= leafNodeCount; i++)
        {
            vec[l - 1].push(i);
        }

        // store nodes of rest of
        // the level by moving in
        // bottom-up manner
        for (let i = l - 2; i >= 0; i--)
        {
            let k = 0;

            // loop to calculate values
            // of parent nodes from the
            // children nodes of lower level
            while (k < vec[i + 1].length - 1)
            {

                // store the value of parent
                // node as sum of children nodes
                vec[i].push(vec[i + 1][k] + vec[i + 1][k + 1]);
                k += 2;
            }
        }

        let sum = 0;

        // traverse the list of vector
        // and calculate the sum
        for (let i = 0; i < l; i++)
        {
            for (let j = 0; j < vec[i].length; j++)
            {
                sum += vec[i][j];
            }
        }

        return sum;
    }

    let l = 3;

    document.write(sumNodes(l));

    // This code is contributed by mukesh07.
</script>
```

**输出:**

```
30
```

**时间复杂度** : O(n)，其中 n 为完美二叉树中的节点总数。
**高效方法**:高效方法是观察我们只需要找到所有节点的和。利用前 n 个自然数之和的公式，我们可以很容易地得到最后一层所有节点的和。此外，可以看到，由于它是一个完美的二叉树，父节点将是子节点的总和，因此所有级别的节点总和将是相同的。因此，我们只需要找到最后一层节点的总和，然后乘以总层数。
以下是上述思路的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;

// function to find sum of all of the nodes
// of given perfect binary tree
int sumNodes(int l)
{
    // no of leaf nodes
    int leafNodeCount = pow(2, l - 1);

    int sumLastLevel = 0;

    // sum of nodes at last level
    sumLastLevel = (leafNodeCount * (leafNodeCount + 1)) / 2;

    // sum of all nodes
    int sum = sumLastLevel * l;

    return sum;
}

// Driver Code
int main()
{
    int l = 3;
    cout << sumNodes(l);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find sum of all nodes
// of the given perfect binary tree
import java.io.*;
import java.lang.Math;

class GFG {

    // function to find sum of
    // all of the nodes of given
    // perfect binary tree
    static double sumNodes(int l)
    {

        // no of leaf nodes
        double leafNodeCount = Math.pow(2, l - 1);

        double sumLastLevel = 0;

        // sum of nodes at last level
        sumLastLevel = (leafNodeCount *
            (leafNodeCount + 1)) / 2;

        // sum of all nodes
        double sum = sumLastLevel * l;

        return sum;
    }

    // Driver Code
    public static void main (String[] args) {

        int l = 3;
        System.out.println(sumNodes(l));
    }
}

// This code is contributed by
// Anuj_{AJ_67}
```

## 蟒蛇 3

```
# function to find sum of all of the nodes
# of given perfect binary tree
import math

def sumNodes(l):

    # no of leaf nodes
    leafNodeCount = math.pow(2, l - 1);

    sumLastLevel = 0;

    # sum of nodes at last level
    sumLastLevel = ((leafNodeCount *
                  (leafNodeCount + 1)) / 2);

    # sum of all nodes
    sum = sumLastLevel * l;

    return int(sum);

# Driver Code
l = 3;
print (sumNodes(l));

# This code is contributed by manishshaw
```

## C#

```
// C# code to find sum of all nodes
// of the given perfect binary tree
using System;
using System.Collections.Generic;

class GFG {

    // function to find sum of
    // all of the nodes of given
    // perfect binary tree
    static double sumNodes(int l)
    {

        // no of leaf nodes
        double leafNodeCount = Math.Pow(2, l - 1);

        double sumLastLevel = 0;

        // sum of nodes at last level
        sumLastLevel = (leafNodeCount *
               (leafNodeCount + 1)) / 2;

        // sum of all nodes
        double sum = sumLastLevel * l;

        return sum;
    }

    // Driver Code
    public static void Main()
    {
        int l = 3;
        Console.Write(sumNodes(l));
    }
}

// This code is contributed by
// Manish Shaw (manishshaw1)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to find sum of all nodes
// of the given perfect binary tree

// function to find sum of
// all of the nodes of given
// perfect binary tree
function sumNodes($l)
{

    // no of leaf nodes
    $leafNodeCount = ($l - 1) *
                     ($l - 1);

    $sumLastLevel = 0;

    // sum of nodes at last level
    $sumLastLevel = ($leafNodeCount *
            ($leafNodeCount + 1)) / 2;

    // sum of all nodes
    $sum = $sumLastLevel * $l;

    return $sum;
}

// Driver Code
$l = 3;
echo (sumNodes($l));

// This code is contributed by
// Manish Shaw (manishshaw1)
?>
```

## java 描述语言

```
<script>
    // Javascript code to find sum of all nodes
    // of the given perfect binary tree

    // function to find sum of
    // all of the nodes of given
    // perfect binary tree
    function sumNodes(l)
    {

        // no of leaf nodes
        let leafNodeCount = Math.pow(2, l - 1);

        let sumLastLevel = 0;

        // sum of nodes at last level
        sumLastLevel = (leafNodeCount * (leafNodeCount + 1)) / 2;

        // sum of all nodes
        let sum = sumLastLevel * l;

        return sum;
    }

    let l = 3;
      document.write(sumNodes(l));

    // This code is contributed by divyeshrabadiya07.
</script>
```

输出:

```
30
```

**时间复杂度** : O(1)