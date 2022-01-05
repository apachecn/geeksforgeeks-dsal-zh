# 用补数求图中最大独立集的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-program-to-find-最大独立集-在图中按补数/](https://www.geeksforgeeks.org/java-program-to-find-the-largest-independent-set-in-a-graph-by-complements/)

在有 V 个顶点和 E 条边的图中， **LIS(最大独立集)**是图中所有没有通过 E 条边相互连接的顶点的集合。

**进场:**

*   我们创建一个 HashMap，它有一对整数和一个整数作为参数。
*   这对表示两个顶点，整数表示这两个顶点之间的边。
*   我们遍历所有顶点，检查两个特定顶点之间是否存在边。如果不满足这个条件，我们将这些顶点附加到我们的结果 HashSet 独立集上。
*   这样，所有独立集的集合都被添加到 HashSet 中，在最后一步中，我们找出其中最大的一个。

**解决方案:**

以顶点数和边数为输入，可以计算出图中最大的独立集。

我们还需要在这里定义一个用户定义的配对类，检查两个顶点之间是否存在边。

## Java 语言(一种计算机语言，尤用于创建网站)

```
static class pair {
    int first, second;
    pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
    @Override public String toString()
    {
        return "(" + first + "," + second + ")";
    }
}
```

*   为了找到图中最大的独立集，我们可以先找出图中所有的独立集，然后分离出最大长度的集合作为我们的答案。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to Find the Largest Independent Set in a
// Graph by Complements

import java.util.*;
class GFG {
    static ArrayList<Integer> vertices = new ArrayList<>();
    static HashMap<pair, Integer> edges = new HashMap<>();

    static HashSet<ArrayList<Integer> > independentSets = new HashSet<>();

    public static void main(String args[])
    {
        int numOfVertices = 4, numOfEdges = 0;
        for (int i = 1; i <= numOfVertices; i++)
            vertices.add(i);

        HashSet<Integer> SolnSet = new HashSet<>();

        // this function call adds all sets to the global
        // solution set
        findAllIndependentSets(1, numOfVertices, SolnSet);

        // to find the largest result set
        ArrayList<Integer> Max = new ArrayList<>();

        for (ArrayList<Integer> i : independentSets) {
            System.out.println(i);

            // comparing lengths of all
            // independent sets
            if (i.size() > Max.size()) 
                Max = i;
        }

        System.out.println("Maximal Independent Set = "
                           + Max);
    }

    // this function finds all independent sets and
    // adds them to the solution object
    static void findAllIndependentSets(int currentVertice, int setSize,
                           HashSet<Integer> SolnSet)
    {
        for (int i = currentVertice; i <= setSize; i++) 
        {
            // checking if vertex is independent
            if (checkSafety(vertices.get(i - 1), SolnSet)) {

                // adding to the temporary solution set
                SolnSet.add(vertices.get(i - 1));

                findAllIndependentSets(i + 1, setSize,
                                       SolnSet);

                // removing previous set
                SolnSet.remove(vertices.get(i - 1));
            }
        }

        // appending the temporary solution set to the
        // solution object
        independentSets.add(new ArrayList<Integer>(SolnSet));
    }

    // this function checks if there exists an edge between
    // 2 vertices
    static boolean checkSafety(int vertex,
                               HashSet<Integer> SolnSet)
    {
        for (int i : SolnSet) {
            if (edges.containsKey(new pair(i, vertex)))

                // if there is an edge, return false
                return false;
        }

        // if vertex is independent , return true
        return true;
    }

    // user-define pair class
    static class pair {
        int first, second;
        pair(int first, int second)
        {
            this.first = first;
            this.second = second;
        }
        @Override public String toString()
        {
            return "(" + first + "," + second + ")";
        }
    }
}
```

**Output**

```
[1]
[1, 2, 3]
[1, 3, 4]
[2]
[]
[1, 2, 4]
[1, 2]
[2, 3, 4]
[2, 3]
[3, 4]
[3]
[1, 3]
[2, 4]
[4]
[1, 4]
[1, 2, 3, 4]
Maximal Independent Set = [1, 2, 3, 4]
```