# 在给定的 N 数组树中寻找最大独立集大小的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-program-to-find-size-of-the-size-the-the-size-the-the-size-of-the-a-n-array-tree/](https://www.geeksforgeeks.org/java-program-to-find-size-of-the-largest-independent-setlis-in-a-given-an-n-array-tree/)

基本上，一个 N[-数组树](https://www.geeksforgeeks.org/generic-treesn-array-trees/)就是这样一个树结构，其中每个节点最多可以有“N”个子节点。[最大独立集](https://www.geeksforgeeks.org/largest-independent-set-problem-dp-26/)是一组顶点，其中没有两个顶点彼此相邻。所以基本上在这个程序中，我们必须看到，我们如何在 N 数组树中找到这样一个最大集合的大小。这里我们使用 java 中的一个向量来实现树，并使用了图论中邻接表的思想。

**算法如下:**

我们主要要做的是，我们将创建一个 LIS(int a)方法，当前节点的编号被传递给这个方法。这是一个递归方法。在这种方法中，我们将首先检查基础条件。在讨论基础条件之前，我们必须先看看方法的其余部分。

所以在代码中，对于每个节点，我们主要看是否包含那个节点插图给出了更大的集合。如果没有，那么那个特定的节点不包括在内，但是因为这个节点不包括在内，所以我们必须对它的子节点重复同样的过程。但是如果包含了节点，那么我们就不能包含它的子节点，所以我们必须检查它的子节点，就像对父节点所做的一样，这样我们就可以知道是否包含这个节点。

现在来看基本案例:

1.  如果该节点为空，这意味着该节点不存在，那么我们不能包含任何内容。
2.  如果节点是叶子，那么我们必须包含它。

> 当调用方法时，为什么总是包括那些叶节点？
> 
> 这里要考虑的主要部分是，只有当某个节点的父节点不包含在集合中(根节点除外)时，该节点才可以被传递给这个方法。所以如果父节点不在集合中，并且这个节点是叶节点，那么我们应该将这个节点包含在集合中。这基本上是一种贪婪的方法。

我们还将对我们的代码做一个小的修改，以打印集合元素。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to Find Size of the Largest Independent
// Set(LIS) in a Given an N-array Tree
import java.io.*;
import java.util.*;

// save the file named as GFG2.java
public class GFG2 {

    // declaring static list of vector.
    public static Vector<Vector<Integer> > v
        = new Vector<Vector<Integer> >();

    // 7 nodes initially
    public static int n = 7;
    public static void main(String[] args)
    {
        System.out.println("Initializing an n array tree");

        Vector<Integer> v0 = new Vector<Integer>();
        v0.add(1);
        v0.add(2);
        v.add(v0);
        Vector<Integer> v1 = new Vector<Integer>();
        v1.add(3);
        v1.add(4);
        v.add(v1);
        Vector<Integer> v2 = new Vector<Integer>();
        v2.add(5);
        v.add(v2);
        Vector<Integer> v3 = new Vector<Integer>();
        v3.add(6);
        v.add(v3);
        Vector<Integer> v4 = new Vector<Integer>();
        v.add(v4);
        v.add(v4);
        v.add(v4);

        /*
        the tree looks like
                                                0
                                        /        \
                                        1        2
                                         /\       /
                                         3  4      5
                                        /
                                        6
        so initially the vector looks like
        v = {
                {1,2},
                {3,4},
                {5},
                {6},
                {},
                {},
                {},
        }
        */

        System.out.println(
            "Finding the elements to be included in the set");

        // calling the function with the first node.
        int x = LIS(0);
        System.out.println("process finished and size is "
                           + x);
    }

    public static int LIS(int a)
    {
        // if no node is there with labelling a
        if (a >= n)
            return 0;

        // if it is leaf node
        if (v.get(a).size() == 0) {
            System.out.println(a);
            return 1;
        }
        // if not considering that node
        int ifno = 0;

        // if considering that node.
        int ifyes = 1;

        // since not considering this node
        // so we should call the same function
        // on the children of this node
        for (int i = 0; i < v.get(a).size(); ++i)
            ifno += LIS(v.get(a).get(i));

        // if including this node
        // then call the same function recursively on the
        // grand children of this node.
        for (int i = 0; i < v.get(a).size(); ++i) {
            int k = v.get(v.get(a).get(i)).size();
            --k;
            while (k >= 0) {
                ifyes += LIS(v.get(v.get(a).get(i)).get(k));
                --k;
            }
        }

        // if found that including this node is beneficial
        if (ifyes > ifno)
            System.out.println(a);
        return Math.max(ifyes, ifno);
    }
}
```

**Output**

```
Initializing an n array tree
Finding the elements to be included in the set
6
4
6
5
4
6
5
0
process finished and size is 4
```

> 由于输出不止一次地显示集合的元素，所以我们必须基本上实现一个映射或集合数据类型来唯一地获取元素。
> 
> 第二件要注意的是，这种方法是递归方法，因此这可能导致指数时间复杂度。使用动态规划方法可以增强这种方法。我们可以通过地图数据结构实现记忆。