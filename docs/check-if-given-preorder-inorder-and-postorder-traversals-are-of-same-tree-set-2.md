# 检查给定的前序、中序和后序遍历是否属于同一棵树|集合 2

> 原文:[https://www . geesforgeks . org/check-if-given-preorder-in order-and-post-traversals-同树同集-2/](https://www.geeksforgeeks.org/check-if-given-preorder-inorder-and-postorder-traversals-are-of-same-tree-set-2/)

给定某棵树的前序、中序和后序遍历。任务是检查它们是否都属于同一棵树。
**例:**

```
Input : Inorder -> 4 2 5 1 3
        Preorder -> 1 2 4 5 3
        Postorder -> 4 5 2 3 1
Output : Yes
Exaplanation : All of the above three traversals are of 
the same tree.             1
                         /   \
                        2     3
                      /   \
                     4     5

Input : Inorder -> 4 2 5 1 3
        Preorder -> 1 5 4 2 3
        Postorder -> 4 1 2 3 5
Output : No
```

在[之前的文章](https://www.geeksforgeeks.org/check-if-given-preorder-inorder-and-postorder-traversals-are-of-same-tree/)中，我们已经讨论了通过使用任意两个遍历来构建树来解决上述问题的方法。
本文讨论了一种不使用任何额外空间的方法。
**进场**:

1.  在 order 数组中搜索 preorder 数组的第一个元素，并将其索引存储为 idx，如果它不存在，则返回 False。另外，检查该元素是否出现在后置数组中。如果不是，则返回假。
2.  从长度 idx 的前序的第 0 个索引到后序的第 1 个索引的所有内容都成为前序数组的第一个元素的左子树。
3.  从位置 idx+1 开始的有序和前序以及从 idx 开始的长度后序( *length-idx-1* )的所有内容都成为前序数组第一个元素的右子树。
4.  递归地重复步骤 1 到 3，直到数组的长度变成 0(在这种情况下，我们
    返回真)或 1(在这种情况下，只有当所有三个数组相等时，我们才返回真，否则返回假)。

下面是上述方法的实现:

## C++

```
// C++ program to check if the given
// three traversals are of the same
// tree or not

#include <bits/stdc++.h>
using namespace std;

// Function to check if traversals are
// of the same tree
int checktree(int preorder[], int inorder[],
              int postorder[], int len)
{

    // if the array lengths are 0,
    // then all of them are obviously equal
    if (len == 0)
        return 1;

    // if array lengths are 1,
    // then check if all of them are equal
    if (len == 1)
        return (preorder[0] == inorder[0])
               && (inorder[0] == postorder[0]);

    // search for first element of preorder
    // in inorder array
    int idx = -1, f = 0;
    for (int i = 0; i < len; ++i)
        if (inorder[i] == preorder[0]) {
            idx = i;
            break;
        }

    if(idx != -1){
      for(int i = 0; i < len; i++)
        if(preorder[0] == postorder[i]){f = 1; break;}
    }

    if (idx == -1 || f == 0)
        return 0;

    // check for the left subtree
    int ret1
        = checktree(preorder + 1, inorder, postorder, idx);

    // check for the right subtree
    int ret2
        = checktree(preorder + idx + 1, inorder + idx + 1,
                    postorder + idx, len - idx - 1);

    // return 1 only if both of them are
    // correct else 0
    return (ret1 && ret2);
}

// Driver Code
int main()
{
    // Traversal Arrays
    int inorder[] = { 4, 2, 5, 1, 3 };
    int preorder[] = { 1, 2, 4, 5, 3 };
    int postorder[] = { 4, 5, 2, 3, 1 };
    int len1 = sizeof(inorder) / sizeof(inorder[0]);
    int len2 = sizeof(preorder) / sizeof(preorder[0]);
    int len3 = sizeof(postorder) / sizeof(postorder[0]);

    // Check if all the array lengths are equal
    if ((len1 == len2) && (len2 == len3)) {

        bool res
            = checktree(preorder, inorder, postorder, len1);

        (res) ? cout << "Yes" : cout << "No";
    }
    else
        cout << "No\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if the given
// three traversals are of the same
// tree or not
class GFG {

    // Function to check if traversals are
    // of the same tree
    static boolean checktree(int preorder[], int s,
                             int inorder[], int s1,
                             int postorder[], int s2,
                             int len)
    {

        // if the array lengths are 0,
        // then all of them are obviously equal
        if (len == 0)
            return true;

        // if array lengths are 1,
        // then check if all of them are equal
        if (len == 1)
            return ((preorder[s] == inorder[s1])
                    && (inorder[s1] == postorder[s2]));

        // search for first element of preorder
        // in inorder array
        int idx = -1;
        for (int i = s1; i < s1 + len; ++i)
            if (inorder[i] == preorder[s]) {
                idx = i;
                break;
            }

        if (idx == -1)
            return false;
        idx = idx - s1;

        // check for the left subtree
        boolean ret1 = checktree(preorder, s + 1, inorder,
                                 s1, postorder, s2, idx);

        // check for the right subtree
        boolean ret2 = checktree(
            preorder, s + idx + 1, inorder, s1 + idx + 1,
            postorder, s2 + idx, len - idx - 1);

        // return 1 only if both of them are
        // correct else 0
        return (ret1 && ret2);
    }

    // Driver Code
    public static void main(String args[])
    {
        // Traversal Arrays
        int inorder[] = { 4, 2, 5, 1, 3 };
        int preorder[] = { 1, 2, 4, 5, 3 };
        int postorder[] = { 4, 5, 2, 3, 1 };
        int len1 = inorder.length;
        int len2 = preorder.length;
        int len3 = postorder.length;

        // Check if all the array lengths are equal
        if ((len1 == len2) && (len2 == len3)) {

            boolean res = checktree(preorder, 0, inorder, 0,
                                    postorder, 0, len1);

            System.out.print(((res) ? "Yes" : "No"));
        }
        else
            System.out.print("No\n");
    }
}

// This code is contributed by Arnab Kundu
```

## 计算机编程语言

```
# Python program to check if the given
# three traversals are of the same
# tree or not

# Function to check if all three traversals
# are of the same tree

def checktree(preorder, inorder, postorder, length):

    # if the array lengths are 0,
    # then all of them are obviously equal
    if length == 0:
        return 1

    # if array lengths are 1,
    # then check if all of them are equal
    if length == 1:
        return (preorder[0] == inorder[0]) and
               (inorder[0] == postorder[0])

    # search for first element of preorder
    # in inorder array
    idx = -1

    for i in range(length):
        if inorder[i] == preorder[0]:
            idx = i
            break

    if idx == -1:
        return 0

    # check for the left subtree
    ret1 = checktree(preorder[1:], inorder, postorder, idx)

    # check for the right subtree
    ret2 = checktree(preorder[idx + 1:], inorder[idx + 1:],
                     postorder[idx:], length-idx-1)

    # return 1 only if both of them are correct else 0
    return (ret1 and ret2)

# Driver Code
if __name__ == "__main__":
    inorder = [4, 2, 5, 1, 3]
    preorder = [1, 2, 4, 5, 3]
    postorder = [4, 5, 2, 3, 1]
    len1 = len(inorder)
    len2 = len(preorder)
    len3 = len(postorder)

    # check if all the array lengths are equal
    if (len1 == len2) and (len2 == len3):
        correct = checktree(preorder, inorder,
                            postorder, len1)
        if (correct):
            print("Yes")
        else:
            print("No")
    else:
        print("No")
```

## C#

```
// C# program to check if the given
// three traversals are of the same
// tree or not
using System;

class GFG {

    // Function to check if traversals are
    // of the same tree
    static bool checktree(int[] preorder, int s,
                          int[] inorder, int s1,
                          int[] postorder, int s2, int len)
    {

        // if the array lengths are 0,
        // then all of them are obviously equal
        if (len == 0)
            return true;

        // if array lengths are 1,
        // then check if all of them are equal
        if (len == 1)
            return ((preorder[s] == inorder[s1])
                    && (inorder[s1] == postorder[s2]));

        // search for first element of preorder
        // in inorder array
        int idx = -1;
        for (int i = s1; i < len; ++i)
            if (inorder[i] == preorder[s]) {
                idx = i;
                break;
            }

        if (idx == -1)
            return false;

        // check for the left subtree
        bool ret1 = checktree(preorder, s + 1, inorder, s1,
                              postorder, s2, idx);

        // check for the right subtree
        bool ret2 = checktree(
            preorder, s + idx + 1, inorder, s1 + idx + 1,
            postorder, s2 + idx, len - idx - 1);

        // return 1 only if both of them are
        // correct else 0
        return (ret1 && ret2);
    }

    // Driver Code
    static public void Main()
    {
        // Traversal Arrays
        int[] inorder = { 4, 2, 5, 1, 3 };
        int[] preorder = { 1, 2, 4, 5, 3 };
        int[] postorder = { 4, 5, 2, 3, 1 };
        int len1 = inorder.Length;
        int len2 = preorder.Length;
        int len3 = postorder.Length;

        // Check if all the array lengths are equal
        if ((len1 == len2) && (len2 == len3)) {

            bool res = checktree(preorder, 0, inorder, 0,
                                 postorder, 0, len1);

            Console.Write(((res) ? "Yes" : "No"));
        }
        else
            Console.Write("No\n");
    }
}

// This code is contributed by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if the given
// three traversals are of the same
// tree or not

// Function to check if traversals are
// of the same tree
function checktree($preorder, $inorder,
                $postorder, $len)
{

    // if the array lengths are 0,
    // then all of them are obviously equal
    if ($len == 0)
        return 1;

    // if array lengths are 1,
    // then check if all of them are equal
    if ($len == 1)
        return ($preorder[0] == $inorder[0])
            && ($inorder[0] == $postorder[0]);

    // search for first element of preorder
    // in inorder array
    $idx = -1;
    for ($i = 0; $i < $len; ++$i)
        if ($inorder[$i] == $preorder[0])
        {
            $idx = $i;
            break;
        }

    if ($idx == -1)
        return 0;

    // check for the left subtree
    $ret1 = checktree(array_slice($preorder,1), $inorder,
                        $postorder, $idx);

    // check for the right subtree
    $ret2 = checktree(array_slice($preorder,$idx + 1),
                        array_slice($inorder,$idx + 1),
                        array_slice($postorder,$idx), $len - $idx - 1);

    // return 1 only if both of them are
    // correct else 0
    return ($ret1 && $ret2);
}

    // Driver Code

    // Traversal Arrays
    $inorder = array( 4, 2, 5, 1, 3 );
    $preorder = array( 1, 2, 4, 5, 3 );
    $postorder = array( 4, 5, 2, 3, 1 );
    $len1 = count($inorder) ;
    $len2 = count($preorder) ;
    $len3 = count($postorder) ;

    // Check if all the array lengths are equal
    if (($len1 == $len2) && ($len2 == $len3))
    {

        $res = checktree($preorder, $inorder,
                            $postorder, $len1);

        if($res)
            echo "Yes";
        else
            echo "No";
    }
    else
        echo "No\n";

    // This code is contributed by AnkitRai01
?>
```

## java 描述语言

```
<script>
    // Javascript program to check if the given
    // three traversals are of the same
    // tree or not

    // Function to check if traversals are
    // of the same tree
    function checktree(preorder, s, inorder, s1, postorder, s2, len)
    {

        // if the array lengths are 0,
        // then all of them are obviously equal
        if (len == 0)
            return true;

        // if array lengths are 1,
        // then check if all of them are equal
        if (len == 1)
            return ((preorder[s] == inorder[s1])
                    && (inorder[s1] == postorder[s2]));

        // search for first element of preorder
        // in inorder array
        let idx = -1;
        for (let i = s1; i < len; ++i)
            if (inorder[i] == preorder[s]) {
                idx = i;
                break;
            }

        if (idx == -1)
            return false;

        // check for the left subtree
        let ret1 = checktree(preorder, s + 1, inorder, s1,
                              postorder, s2, idx);

        // check for the right subtree
        let ret2 = checktree(
            preorder, s + idx + 1, inorder, s1 + idx + 1,
            postorder, s2 + idx, len - idx - 1);

        // return 1 only if both of them are
        // correct else 0
        return (ret1 && ret2);
    }

    // Traversal Arrays
    let inorder = [ 4, 2, 5, 1, 3 ];
    let preorder = [ 1, 2, 4, 5, 3 ];
    let postorder = [ 4, 5, 2, 3, 1 ];
    let len1 = inorder.length;
    let len2 = preorder.length;
    let len3 = postorder.length;

    // Check if all the array lengths are equal
    if ((len1 == len2) && (len2 == len3)) {

      let res = checktree(preorder, 0, inorder, 0,
                           postorder, 0, len1);

      document.write(((res) ? "Yes" : "No"));
    }
    else
      document.write("No");

</script>
```

**Output:** 

```
Yes
```