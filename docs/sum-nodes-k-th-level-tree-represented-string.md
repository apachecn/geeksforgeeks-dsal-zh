# 表示为字符串的树中第 k 级节点的总和

> 原文:[https://www . geesforgeks . org/sum-nodes-k-th-level-tree-presented-string/](https://www.geeksforgeeks.org/sum-nodes-k-th-level-tree-represented-string/)

给定一个整数“K”和一个字符串格式的二叉树。树的每个节点的值都在 0 到 9 之间。我们需要从根开始寻找 K 级元素的和。根在 0 级。
树以如下形式给出:(节点值(左子树)(右子树))

**示例:**

```
Input : tree = "(0(5(6()())(4()(9()())))(7(1()())(3()())))" 
        k = 2
Output : 14
Its tree representation is shown below
```

![](img/bc5787ff546f5ba45c98826fc412bbd6.png)

```
Elements at level k = 2 are 6, 4, 1, 3
sum of the digits of these elements = 6+4+1+3 = 14 

Input : tree = "(8(3(2()())(6(5()())()))(5(10()())(7(13()())())))" 
        k = 3
Output : 9
Elements at level k = 3 are 5, 1 and 3
sum of digits of these elements = 5+1+3 = 9
```

```
1\. Input 'tree' in string format and level k
2\. Initialize level = -1 and sum = 0
3\. for each character 'ch' in 'tree'
   3.1  if ch == '(' then
        --> level++
   3.2  else if ch == ')' then
        --> level--
   3.3  else
        if level == k then
           sum = sum + (ch-'0')
4\. Print sum
```

## C++

```
// C++ implementation to find sum of
// digits of elements at k-th level
#include <bits/stdc++.h>
using namespace std;

// Function to find sum of digits
// of elements at k-th level
int sumAtKthLevel(string tree, int k)
{
    int level = -1;
    int sum = 0;  // Initialize result
    int n = tree.length();

    for (int i=0; i<n; i++)
    {
        // increasing level number
        if (tree[i] == '(')
            level++;

        // decreasing level number
        else if (tree[i] == ')')
            level--;

        else
        {
            // check if current level is
            // the desired level or not
            if (level == k)
                sum += (tree[i]-'0');
        }
    }

    // required sum
    return sum;
}

// Driver program to test above
int main()
{
    string tree = "(0(5(6()())(4()(9()())))(7(1()())(3()())))";
    int k = 2;
    cout << sumAtKthLevel(tree, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find sum of
// digits of elements at k-th level
class GfG {

// Function to find sum of digits
// of elements at k-th level
static int sumAtKthLevel(String tree, int k)
{
    int level = -1;
    int sum = 0; // Initialize result
    int n = tree.length();

    for (int i=0; i<n; i++)
    {
        // increasing level number
        if (tree.charAt(i) == '(')
            level++;

        // decreasing level number
        else if (tree.charAt(i) == ')')
            level--;

        else
        {
            // check if current level is
            // the desired level or not
            if (level == k)
                sum += (tree.charAt(i)-'0');
        }
    }

    // required sum
    return sum;
}

// Driver program to test above
public static void main(String[] args)
{
    String tree = "(0(5(6()())(4()(9()())))(7(1()())(3()())))";
    int k = 2;
    System.out.println(sumAtKthLevel(tree, k));
}
}
```

## 蟒蛇 3

```
# Python3 implementation to find sum of
# digits of elements at k-th level

# Function to find sum of digits
# of elements at k-th level
def sumAtKthLevel(tree, k) :

    level = -1
    sum = 0 # Initialize result
    n = len(tree)

    for i in range(n):

        # increasing level number
        if (tree[i] == '(') :
            level += 1

        # decreasing level number
        elif (tree[i] == ')'):
            level -= 1

        else:

            # check if current level is
            # the desired level or not
            if (level == k) :
                sum += (ord(tree[i]) - ord('0'))

    # required sum
    return sum

# Driver Code
if __name__ == '__main__':
    tree = "(0(5(6()())(4()(9()())))(7(1()())(3()())))"
    k = 2
    print(sumAtKthLevel(tree, k))

# This code is contributed by
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
// C# implementation to find sum of
// digits of elements at k-th level

using System;
class GfG {

// Function to find sum of digits
// of elements at k-th level
static int sumAtKthLevel(string tree, int k)
{
    int level = -1;
    int sum = 0; // Initialize result
    int n = tree.Length;

    for (int i = 0; i < n; i++)
    {
        // increasing level number
        if (tree[i] == '(')
            level++;

        // decreasing level number
        else if (tree[i] == ')')
            level--;

        else
        {
            // check if current level is
            // the desired level or not
            if (level == k)
                sum += (tree[i]-'0');
        }
    }

    // required sum
    return sum;
}

// Driver code
public static void Main()
{
    string tree = "(0(5(6()())(4()(9()())))(7(1()())(3()())))";
    int k = 2;
    Console.Write(sumAtKthLevel(tree, k));
}
}

// This code is contributed by Ita_c
```

## java 描述语言

```
<script>

// Javascript implementation to find sum of
// digits of elements at k-th level

// Function to find sum of digits
// of elements at k-th level
function sumAtKthLevel(tree, k)
{
    let level = -1;

    // Initialize result
    let sum = 0;
    let n = tree.length;

    for(let i = 0; i < n; i++)
    {

        // Increasing level number
        if (tree[i] == '(')
            level++;

        // Decreasing level number
        else if (tree[i] == ')')
            level--;

        else
        {

            // Check if current level is
            // the desired level or not
            if (level == k)
                sum += (tree[i] - '0');
        }
    }

    // Required sum
    return sum;
}

// Driver code
let tree = "(0(5(6()())(4()(9()())))(7(1()())(3()())))";
let k = 2;

document.write(sumAtKthLevel(tree, k));

// This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
14
```

**时间复杂度:** O(n)

**递归方法:**思想是将字符串视为树，而不实际创建一个树，简单地以 Postorder 方式递归遍历字符串，并考虑仅在 k 级的节点。

以下是相同的实现:

## C++

```
// C++ implementation to find sum of
// digits of elements at k-th level
#include <bits/stdc++.h>
using namespace std;

// Recursive Function to find sum of digits
// of elements at k-th level
int sumAtKthLevel(string tree, int k,int &i,int level)
{

    if(tree[i++]=='(')
    {

      // if subtree is null, just like if root == NULL
      if(tree[i] == ')')
           return 0;           

      int sum=0;

      // Consider only level k node to be part of the sum
      if(level == k)
        sum = tree[i]-'0';

      // Recur for Left Subtree
      int leftsum = sumAtKthLevel(tree,k,++i,level+1);

      // Recur for Right Subtree
      int rightsum = sumAtKthLevel(tree,k,++i,level+1);

      // Taking care of ')' after left and right subtree
      ++i;
      return sum+leftsum+rightsum;       
    }
}

// Driver program to test above
int main()
{
    string tree = "(0(5(6()())(4()(9()())))(7(1()())(3()())))";
    int k = 2;
        int i=0;
    cout << sumAtKthLevel(tree, k,i,0);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find sum of
// digits of elements at k-th level
class GFG
{
    static int i;

    // Recursive Function to find sum of digits
    // of elements at k-th level
    static int sumAtKthLevel(String tree, int k, int level)
    {

        if (tree.charAt(i++) == '(')
        {

            // if subtree is null, just like if root == null
            if (tree.charAt(i) == ')')
                return 0;

            int sum = 0;

            // Consider only level k node to be part of the sum
            if (level == k)
                sum = tree.charAt(i) - '0';

            // Recur for Left Subtree
            ++i;
            int leftsum = sumAtKthLevel(tree, k, level + 1);

            // Recur for Right Subtree
            ++i;
            int rightsum = sumAtKthLevel(tree, k, level + 1);

            // Taking care of ')' after left and right subtree
            ++i;
            return sum + leftsum + rightsum;
        }
        return Integer.MIN_VALUE;
    }

    // Driver code
    public static void main(String[] args)
    {
        String tree = "(0(5(6()())(4()(9()())))(7(1()())(3()())))";
        int k = 2;
        i = 0;
        System.out.print(sumAtKthLevel(tree, k, 0));
    }
}

// This code is contributed by 29AjayKumar
```

## 计算机编程语言

```
# Python implementation to find sum of
# digits of elements at k-th level

# Recursive Function to find sum of digits
# of elements at k-th level
def sumAtKthLevel(tree, k, i, level):

    if(tree[i[0]] == '('):
        i[0] += 1

        # if subtree is null, just like if root == NULL
        if(tree[i[0]] == ')'):
            return 0           

        sum = 0

        # Consider only level k node to be part of the sum
        if(level == k):
            sum = int(tree[i[0]])

        # Recur for Left Subtree
        i[0] += 1
        leftsum = sumAtKthLevel(tree, k, i, level + 1)

        # Recur for Right Subtree
        i[0] += 1
        rightsum = sumAtKthLevel(tree, k, i, level + 1)

        # Taking care of ')' after left and right subtree
        i[0] += 1
        return sum + leftsum + rightsum    

# Driver program to test above
tree = "(0(5(6()())(4()(9()())))(7(1()())(3()())))"
k = 2
i = [0]
print(sumAtKthLevel(tree, k, i, 0))

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
// C# implementation to find sum of
// digits of elements at k-th level
using System;

class GFG
{
    static int i;

    // Recursive Function to find sum of digits
    // of elements at k-th level
    static int sumAtKthLevel(String tree, int k, int level)
    {

        if (tree[i++] == '(')
        {

            // if subtree is null, just like if root == null
            if (tree[i] == ')')
                return 0;

            int sum = 0;

            // Consider only level k node to be part of the sum
            if (level == k)
                sum = tree[i] - '0';

            // Recur for Left Subtree
            ++i;
            int leftsum = sumAtKthLevel(tree, k, level + 1);

            // Recur for Right Subtree
            ++i;
            int rightsum = sumAtKthLevel(tree, k, level + 1);

            // Taking care of ')' after left and right subtree
            ++i;
            return sum + leftsum + rightsum;
        }
        return int.MinValue;
    }

    // Driver code
    public static void Main(String[] args)
    {
        String tree = "(0(5(6()())(4()(9()())))(7(1()())(3()())))";
        int k = 2;
        i = 0;
        Console.Write(sumAtKthLevel(tree, k, 0));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript implementation to find sum of
// digits of elements at k-th level

    // Recursive Function to find sum of digits
    // of elements at k-th level
    function sumAtKthLevel(tree,k,level)
    {
        if (tree[i++] == '(')
        {

            // if subtree is null, just like if root == null
            if (tree[i] == ')')
                return 0;

            let sum = 0;

            // Consider only level k node to be part of the sum
            if (level == k)
                sum = tree[i] - '0';

            // Recur for Left Subtree
            ++i;
            let leftsum = sumAtKthLevel(tree, k, level + 1);

            // Recur for Right Subtree
            ++i;
            let rightsum = sumAtKthLevel(tree, k, level + 1);

            // Taking care of ')' after left and right subtree
            ++i;
            return sum + leftsum + rightsum;
        }
        return Number.MIN_VALUE;
    }

     // Driver code
    let tree = "(0(5(6()())(4()(9()())))(7(1()())(3()())))";
    let k = 2;
    let i = 0;
    document.write(sumAtKthLevel(tree, k, 0));

    // This code is contributed by rag2127
</script>
```

**输出:**

```
14
```

**时间复杂度:** O(n)

本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。