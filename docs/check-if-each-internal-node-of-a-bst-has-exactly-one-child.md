# 检查一个 BST 的每个内部节点是否正好有一个子节点

> 原文:[https://www . geesforgeks . org/check-如果每个 bst 的内部节点都有一个子节点/](https://www.geeksforgeeks.org/check-if-each-internal-node-of-a-bst-has-exactly-one-child/)

给定 BST 的 Preorder 遍历，检查每个非叶节点是否只有一个子节点。假设 BST 包含唯一的条目。

**示例**

```
Input: pre[] = {20, 10, 11, 13, 12}
Output: Yes
The given array represents following BST. In the following BST, every internal
node has exactly 1 child. Therefore, the output is true.
        20
       /
      10
       \
        11
          \
           13
           /
         12
```

在 Preorder 遍历中，每个节点的后代(或 Preorder 后继)出现在该节点之后。在上面的例子中，20 是前序中的第一个节点，20 的所有后代都出现在它之后。20 的后代都比它小。对于 10 来说，所有后代都大于它。一般来说，我们可以说，如果所有内部节点在一个 BST 中只有一个子节点，那么每个节点的所有后代要么比该节点小，要么比该节点大。原因很简单，因为树是 BST，每个节点只有一个子节点，所以一个节点的所有后代要么在左侧，要么在右侧，这意味着所有后代要么更小，要么更大。

**方法 1(幼稚)**
这种方法简单地遵循了上面的想法，即右侧的所有值要么更小，要么更大。使用两个循环，外部循环从最左边的元素开始，逐个选取一个元素。内部循环检查拾取元素右侧的所有元素是更小还是更大。这种方法的时间复杂度将是 O(n^2).

**方法 2**
因为一个节点的所有后代必须大于或小于该节点。我们可以对循环中的每个节点执行以下操作。
1。查找节点的下一个前序后继(或后代)。
2。查找节点的最后一个前序后继(pre[])元素。
3。如果两个后续节点都小于当前节点，或者两个后续节点都大于当前节点，则继续。否则，返回 false。

## C++

```
#include<bits/stdc++.h>
using namespace std;

bool hasOnlyOneChild(int pre[], int size)
{
    int nextDiff, lastDiff;

    for (int i=0; i<size-1; i++)
    {
        nextDiff = pre[i] - pre[i+1];
        lastDiff = pre[i] - pre[size-1];
        if (nextDiff*lastDiff < 0)
            return false;;
    }
    return true;
}

// driver program to test above function
int main()
{
    int pre[] = {8, 3, 5, 7, 6};
    int size = sizeof(pre)/sizeof(pre[0]);
    if (hasOnlyOneChild(pre, size) == true )
        cout<<"Yes";
    else
        cout<<"No";
    return 0;
}

// This code is contributed by rrrtnx.
```

## C

```
#include <stdio.h>

bool hasOnlyOneChild(int pre[], int size)
{
    int nextDiff, lastDiff;

    for (int i=0; i<size-1; i++)
    {
        nextDiff = pre[i] - pre[i+1];
        lastDiff = pre[i] - pre[size-1];
        if (nextDiff*lastDiff < 0)
            return false;;
    }
    return true;
}

// driver program to test above function
int main()
{
    int pre[] = {8, 3, 5, 7, 6};
    int size = sizeof(pre)/sizeof(pre[0]);
    if (hasOnlyOneChild(pre, size) == true )
        printf("Yes");
    else
        printf("No");
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Check if each internal node of BST has only one child

class BinaryTree {

    boolean hasOnlyOneChild(int pre[], int size) {
        int nextDiff, lastDiff;

        for (int i = 0; i < size - 1; i++) {
            nextDiff = pre[i] - pre[i + 1];
            lastDiff = pre[i] - pre[size - 1];
            if (nextDiff * lastDiff < 0) {
                return false;
            };
        }
        return true;
    }

    public static void main(String[] args) {
        BinaryTree tree = new BinaryTree();
        int pre[] = new int[]{8, 3, 5, 7, 6};
        int size = pre.length;
        if (tree.hasOnlyOneChild(pre, size) == true) {
            System.out.println("Yes");
        } else {
            System.out.println("No");
        }
    }
}

// This code has been contributed by Mayank Jaiswal
```

## 蟒蛇 3

```
# Check if each internal
# node of BST has only one child

def hasOnlyOneChild (pre, size):
    nextDiff=0; lastDiff=0

    for i in range(size-1):
        nextDiff = pre[i] - pre[i+1]
        lastDiff = pre[i] - pre[size-1]
        if nextDiff*lastDiff < 0:
            return False
    return True

# driver program to
# test above function
if __name__ == "__main__":

    pre = [8, 3, 5, 7, 6]
    size= len(pre)

    if (hasOnlyOneChild(pre,size) == True):
        print("Yes")
    else:
        print("No")

# This code is contributed by
# Harshit Saini
```

## C#

```
// Check if each internal node of BST has only one child
using System;
public class BinaryTree
{

  bool hasOnlyOneChild(int[] pre, int size)
  {
    int nextDiff, lastDiff;
    for (int i = 0; i < size - 1; i++)
    {
      nextDiff = pre[i] - pre[i + 1];
      lastDiff = pre[i] - pre[size - 1];
      if (nextDiff * lastDiff < 0)
      {
        return false;
      };
    }
    return true;
  }

  // Driver code
  public static void Main(String[] args)
  {
    BinaryTree tree = new BinaryTree();
    int []pre = new int[]{8, 3, 5, 7, 6};
    int size = pre.Length;
    if (tree.hasOnlyOneChild(pre, size) == true)
    {
      Console.WriteLine("Yes");
    }
    else
    {
      Console.WriteLine("No");
    }
  }
}

// This code is contributed by aashish1995
```

## java 描述语言

```
<script>

// Check if each internal node of BST has only one child
function hasOnlyOneChild(pre, size)
{
  var nextDiff, lastDiff;
  for (var i = 0; i < size - 1; i++)
  {
    nextDiff = pre[i] - pre[i + 1];
    lastDiff = pre[i] - pre[size - 1];
    if (nextDiff * lastDiff < 0)
    {
      return false;
    };
  }
  return true;
}

// Driver code
var pre = [8, 3, 5, 7, 6];
var size = pre.length;
if (hasOnlyOneChild(pre, size) == true)
{
  document.write("Yes");
}
else
{
  document.write("No");
}

// This code is contributed by itsok.
</script>
```

**输出:**

```
 Yes 
```

**进场 3**
1。扫描预订单的最后两个节点&标记为最小&最大。
2。扫描预排序数组中的每个节点。每个节点必须小于最小节点或大于最大节点。相应地更新最小值&最大值。

## C++

```
#include <bits/stdc++.h>
using namespace std;

int hasOnlyOneChild(int pre[], int size)
{

    // Initialize min and max using last two elements
    int min, max;
    if (pre[size - 1] > pre[size - 2])
    {
        max = pre[size - 1];
        min = pre[size - 2];
    }
    else
    {
        max = pre[size - 2];
        min = pre[size - 1];
    }

    // Every element must be either smaller
    // than min or greater than max
    for(int i = size - 3; i >= 0; i--)
    {
        if (pre[i] < min)
            min = pre[i];
        else if (pre[i] > max)
            max = pre[i];
        else
            return false;
    }
    return true;
}

// Driver code
int main()
{
    int pre[] = { 8, 3, 5, 7, 6 };
    int size = sizeof(pre) / sizeof(pre[0]);

    if (hasOnlyOneChild(pre,size))
        cout <<"Yes";
    else
        cout <<"No";

    return 0;
}

// This code is contributed by shivanisinghss2110
```

## C

```
#include <stdio.h>

int hasOnlyOneChild(int pre[], int size)
{
    // Initialize min and max using last two elements
    int min, max;
    if (pre[size-1] > pre[size-2])
    {
        max = pre[size-1];
        min = pre[size-2];
    }
    else
    {
        max = pre[size-2];
        min = pre[size-1];
    }

    // Every element must be either smaller than min or
    // greater than max
    for (int i=size-3; i>=0; i--)
    {
        if (pre[i] < min)
            min = pre[i];
        else if (pre[i] > max)
            max = pre[i];
        else
            return false;
    }
    return true;
}

// Driver program to test above function
int main()
{
    int pre[] = {8, 3, 5, 7, 6};
    int size = sizeof(pre)/sizeof(pre[0]);
    if (hasOnlyOneChild(pre,size))
        printf("Yes");
    else
        printf("No");
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Check if each internal node of BST has only one child

class BinaryTree {

    boolean hasOnlyOneChild(int pre[], int size) {
        // Initialize min and max using last two elements
        int min, max;
        if (pre[size - 1] > pre[size - 2]) {
            max = pre[size - 1];
            min = pre[size - 2];
        } else {
            max = pre[size - 2];
            min = pre[size - 1];
        }

        // Every element must be either smaller than min or
        // greater than max
        for (int i = size - 3; i >= 0; i--) {
            if (pre[i] < min) {
                min = pre[i];
            } else if (pre[i] > max) {
                max = pre[i];
            } else {
                return false;
            }
        }
        return true;
    }

    public static void main(String[] args) {
        BinaryTree tree = new BinaryTree();
        int pre[] = new int[]{8, 3, 5, 7, 6};
        int size = pre.length;
        if (tree.hasOnlyOneChild(pre, size) == true) {
            System.out.println("Yes");
        } else {
            System.out.println("No");
        }
    }
}

// This code has been contributed by Mayank Jaiswal
```

## 蟒蛇 3

```
# Check if each internal
# node of BST has only one child
# approach 2

def hasOnlyOneChild(pre,size):

    # Initialize min and max
    # using last two elements
    min=0; max=0

    if pre[size-1] > pre[size-2] :
        max = pre[size-1]
        min = pre[size-2]
    else :
        max = pre[size-2]
        min = pre[size-1]

    # Every element must be
    # either smaller than min or
    # greater than max
    for i in range(size-3, 0, -1):
        if pre[i] < min:
            min = pre[i]
        elif pre[i] > max:
            max = pre[i]
        else:
            return False
    return True

# Driver program to
# test above function
if __name__ == "__main__":

    pre = [8, 3, 5, 7, 6]

    size = len(pre)
    if (hasOnlyOneChild(pre, size)):
        print("Yes")
    else:
        print("No")

# This code is contributed by
# Harshit Saini
```

## C#

```
// Check if each internal node of BST has only one child
using System;
public class BinaryTree
{

  bool hasOnlyOneChild(int []pre, int size)
  {

    // Initialize min and max using last two elements
    int min, max;
    if (pre[size - 1] > pre[size - 2]) {
      max = pre[size - 1];
      min = pre[size - 2];
    } else {
      max = pre[size - 2];
      min = pre[size - 1];
    }

    // Every element must be either smaller than min or
    // greater than max
    for (int i = size - 3; i >= 0; i--) {
      if (pre[i] < min) {
        min = pre[i];
      } else if (pre[i] > max) {
        max = pre[i];
      } else {
        return false;
      }
    }
    return true;
  }

  // Driver code
  public static void Main(String[] args)
  {
    BinaryTree tree = new BinaryTree();
    int []pre = new int[]{8, 3, 5, 7, 6};
    int size = pre.Length;
    if (tree.hasOnlyOneChild(pre, size) == true)
    {
      Console.WriteLine("Yes");
    }
    else
    {
      Console.WriteLine("No");
    }
  }
}

// This code is contributed by aashish1995
```

## java 描述语言

```
<script>

      // Check if each internal node of BST
      // has only one child
      class BinaryTree {
        hasOnlyOneChild(pre, size) {
          // Initialize min and max using
          // last two elements
          var min, max;
          if (pre[size - 1] > pre[size - 2]) {
            max = pre[size - 1];
            min = pre[size - 2];
          } else {
            max = pre[size - 2];
            min = pre[size - 1];
          }

          // Every element must be either
          // smaller than min or
          // greater than max
          for (var i = size - 3; i >= 0; i--) {
            if (pre[i] < min) {
              min = pre[i];
            } else if (pre[i] > max) {
              max = pre[i];
            } else {
              return false;
            }
          }
          return true;
        }
      }
      // Driver code
      var tree = new BinaryTree();
      var pre = [8, 3, 5, 7, 6];
      var size = pre.length;
      if (tree.hasOnlyOneChild(pre, size) == true) {
        document.write("Yes");
      } else {
        document.write("No");
      }

</script>
```

**输出:**

```
Yes
```

如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息