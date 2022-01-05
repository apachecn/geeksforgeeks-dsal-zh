# 图形的基本属性

> 原文:[https://www.geeksforgeeks.org/basic-properties-of-a-graph/](https://www.geeksforgeeks.org/basic-properties-of-a-graph/)

图是由节点和边组成的非线性数据结构。节点有时也称为顶点，边是连接图中任意两个节点的直线或圆弧。

根据图的结构，图的性质基本上用于描述图的特征。我们用属于图论领域的特定术语定义了这些性质。在本文中，我们将讨论图的一些性质，如下所示:

1.  **Distance between two Vertices**
    It is basically the number of edges that are available in the shortest path between vertex A and vertex B.If there is more than one edge which is used two connect two vertices then we basically considered the shortest path as the distance between these two vertices.

    ```
    Notation used :
    d(A, B)
    here function d is basically showing the distance between vertex A and vertex B.

    ```

    让我们用一个例子来理解这一点:
    ![](img/08dbc601e31f48522d98a3988b67e3f2.png)
    在上图中，让我们试着找出顶点 b 和 d 之间的距离。

    ```
    d(b, c)
    We can go from vertex b to vertex d in different ways such as
    1.ba, af, fe, ed here the d(b, c) will be 4.
    2.ba, af, fc, cd here the d(b, c) will be 4.
    3.bc, cf, fe, ed here the d(b, c) will be 4.
    4.bc, cd here the d(b, c) will be 2.
    hence the minimum distance between vertex b and vertex d is 2.

    ```

2.  **Eccentricity of a Vertex**
    Maximum distance from a vertex to all other vertices is considered as the Eccentricity of that vertex.

    ```
    Notation used:
    e(V)
    here e(v) determines the eccentricity of vertex V.

    ```

    让我们试着用下面的例子来理解这一点。
    ![](img/08dbc601e31f48522d98a3988b67e3f2.png)

    ```
    From the above diagram lets try to find the eccentricity of vertex b.
    e(b)
    d(b, a)=1
    d(b, c)=1
    d(b, d)=2
    d(b, e)=3
    d(b, f)=2
    d(b, g)=2
    Hence the eccentricity of vertex b is 3

    ```

3.  **Radius of a Connected Graph**
    The minimum value of eccentricity from all vertices is basically considered as the radius of connected graph.

    ```
    Notation used:
    r(G)
    here G is the connected graph.

    ```

    让我们试着用下面的例子来理解这一点。
    ![](img/08dbc601e31f48522d98a3988b67e3f2.png)

    ```
    From the above diagram:
    r(G) is 2.
    Because the minimum value of eccentricity from all vertices is 2.

    ```

4.  **Diameter of A Connected Graph**
    Unlike the radius of the connected graph here we basically used the maximum value of eccentricity from all vertices to determine the diameter of the graph.

    ```
    Notation used:
    d(G)
    where G is the connected graph.

    ```

    让我们试着用下面的例子来理解这一点。
    ![](img/08dbc601e31f48522d98a3988b67e3f2.png)

    ```
    From the above diagram:
    d(G) is 3.
    Because the maximum value of eccentricity from all vertices is 3.

    ```

5.  **Central Point and Centre**
    The vertex having minimum eccentricity is considered as the central point of the graph.And the sets of all central point is considered as the centre of Graph.

    ```
    if
    e(V)=r(G)
    then v is the central point.

    ```

    让我们试着用下面的例子来理解这一点。
    ![](img/08dbc601e31f48522d98a3988b67e3f2.png)

    ```
    In the above diagram the central point will be f.
    because 
    e(f)=r(G)=2
    hence f is considered as the central point of graph.
    Hence f is also the centre of the graph.

    ```