# 在图中寻找良好反馈顶点集的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-program-to-find-good-feedback-顶点集在图中/](https://www.geeksforgeeks.org/java-program-to-find-a-good-feedback-vertex-set-in-a-graph/)

图的反馈顶点集是一组顶点，去掉这些顶点后，图没有循环。下图成为有向无环图。

**示例:**

```
Input:
Enter the number of vertices:  
4
Enter the number of edges:  
5
Enter the graph: <Start> <end>
1 2
2 3
3 4
4 1
1 3
Output:
The Graph is:
1-> 2-> 3
2-> 3
3-> 4
4-> 1
The set of edges in FeedBack arc set: 2 - 3
4 - 1

Input:
Enter the number of vertices:  
5
Enter the number of edges:  
5
Enter the graph: <Start> <end>
1 2
2 4
5 3
5 1
4 3.
Output:
The Graph is:
1-> 2
2-> 4
4-> 3
5-> 3-> 1
The set of edges in FeedBack arc set: None
```

**进场:**

*   我们将声明所有需要的变量，像计数，边，开始，结束和顶点
*   现在我们将调用图形函数:我们将取值并存储在一个相邻的列表中，该列表将被声明为类的变量。
*   然后保持 while 条件不变，我们将获取图中构造函数的所有起点和终点的输入。
*   现在调用 set edge 函数:我们检查相邻列表是否为空，如果不是，我们将在其中存储它的值。
*   然后我们调用 printGraph()函数——这个方法将基本上打印图形，其中我们迭代循环并打印元素，并将其存储在列表中
*   然后我们调用类的对象并调用检查函数——每个迭代器检查我们是否只取了一次值。如果值重复，我们就移除它
*   然后我们设置反馈顶点并调用该函数——我们现在将检查我们是否访问了所有节点，如果访问了，我们将对其进行计数，如果没有访问，我们将保持它等于 1。现在使用所有这些，我们会发现哪个节点可以删除。

**代码:**

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to Find a Good Feedback Vertex Set in a
// Graph

import java.util.HashMap;
import java.util.Iterator;
import java.util.LinkedList;
import java.util.List;
import java.util.Map;
import java.util.Scanner;

// Let us declare a class
class Edge

{

    // We have declared a Map with Integer as its parameters
    // Named adjacentList

    private Map<Integer, List<Integer> > adjacentList;

    // Now lets us declare a function called "Graph"
    public Edge(int vertices)
    {
        // Now taking the new List as a HashMap
        adjacentList
            = new HashMap<Integer, List<Integer> >();

        // Iterating i from 1 till vertices
        for (int i = 1; i <= vertices; i++) {
            // Adding them to a new LinkedList
            adjacentList.put(i, new LinkedList<Integer>());
        }
    }

    // We are now declaring  a class edge
    // It has two parameters start and end
    public void set_Edge(int end, int start)
    {
        // We will write the condition for checking
        // If the the vertices are empty
        if (end > adjacentList.size()
            || start > adjacentList.size())

            System.out.println("There are no vertices");

        // Now if the input isn't zero
        // We will add them to a new list
        List<Integer> fls = adjacentList.get(start);

        fls.add(end);
    }

    // We created a list function called get edge
    // Help us to return the edges of a Graph
    public List<Integer> get_Edge(int end)
    {

        // Returning the edges back
        return adjacentList.get(end);
    }

    // Now let us check
    public Edge check()
    {

        // Now let us keep the count as 0
        Integer count = 0;

        // Let us iterator for easy function
        Iterator<Integer> iterator
            = this.adjacentList.keySet().iterator();

        // Let us take a size variable of adjacent List
        Integer size = this.adjacentList.size() - 1;

        // Iterating it till the end of the loop
        while (iterator.hasNext()) {

            // Now taking the variable which is an iterator
            Integer i = iterator.next();

            // Declaring a new list adjlist
            List<Integer> adjList
                = this.adjacentList.get(i);

            // checking for equal size we would return the
            // same
            if (count == size) {
                return this;
            }

            // Now keeping the condition adjList==0
            if (adjList.size() == 0) {

                // Every time we run the if
                // we increase the count
                count++;

                // Now taking an iterator Right
                Iterator<Integer> iteratorR
                    = this.adjacentList.keySet().iterator();

                // Again iterating completely over the new
                // Iterator
                while (iteratorR.hasNext()) {

                    // Having the new R , help us to iterate
                    // the new Iterator
                    Integer R = iteratorR.next();

                    // New List is taken

                    List<Integer> lit
                        = this.adjacentList.get(R);

                    // This if condition will help not to
                    // have

                    // Any duplicate values inside the new
                    // List
                    if (lit.contains(i)) {
                        // If we have one we would remove it

                        lit.remove(i);
                    }
                }

                // The below line would help us to remove
                // the values

                // Of the adjacent List as we move on to
                // make the vertices

                // The other values are simultaneously
                // removed.
                this.adjacentList.remove(i);

                iterator
                    = this.adjacentList.keySet().iterator();
            }
        }

        return this;
    }

    // This function helps us to print a graph
    public void printGraph()

    {

        System.out.println("The Graph is:");

        // Now let us taken an iterator and try to print it

        // This iterator contains the values of the new
        // graph
        Iterator<Integer> iterator
            = this.adjacentList.keySet().iterator();

        // Now  iterating the values
        while (iterator.hasNext())

        {

            // taking the variable i to be the next Iterator
            Integer i = iterator.next();

            // Taking a list which will help us have the
            // side edges.
            List<Integer> edgeList = this.get_Edge(i);

            // Now checking the edge list if it is not zero
            if (edgeList.size() != 0)

            {

                // print them out
                System.out.print(i);

                // now iterating it till edgelist
                for (int j = 0; j < edgeList.size(); j++)

                {

                    // Now printing the graph in its pattern
                    System.out.print("-> "
                                     + edgeList.get(j));
                }

                System.out.println();
            }
        }
    }

    // Closing the function

    // Now finding the FeedbackArc set
    public boolean getFeedbackArcSet(int vertices)

    {

        // Taking boolean flag false
        boolean flag = false;

        // Now taking visited array
        // This array length is vertices+1
        int[] visited = new int[vertices + 1];

        // This iterator has values of adjacent list
        Iterator<Integer> iterator
            = this.adjacentList.keySet().iterator();

        // Now let us see the feedback arc
        System.out.print(
            "The set of edges in FeedBack arc set: ");

        // Now it has iterator which is next
        while (iterator.hasNext())

        {

            // Now taking i which will be iterating next
            Integer i = iterator.next();

            // Now taking a list of values adjacent list
            List<Integer> list = this.adjacentList.get(i);

            // Visited array to be after i
            visited[i] = 1;

            // Now taking if the list size not equal to 0
            if (list.size() != 0)

            {

                // We iterate till list sie
                for (int j = 0; j < list.size(); j++)

                {

                    // If we have visited the list
                    // e will flag it to be true
                    if (visited[list.get(j)] == 1)

                    {

                        flag = true;

                        // Now taking the output of feedback
                        // arc
                        System.out.println(i + " - "
                                           + list.get(j));
                    }

                    else

                    {

                        // Now if we dint visit
                        // We will be iterating it to 1
                        visited[list.get(j)] = 1;
                    }
                }
            }
        }

        // Return the flag
        return flag;
    }
}

// Now let us declare the class GFG

class GFG {

    public static void main(String[] args)
    {

        // Now let us declare and initialize all the
        // variables
        int vertices = 4, e = 5, count = 1;
        int[] start = { 1, 2, 3, 4, 1 };
        int[] end = { 2, 3, 4, 1, 3 };

        // Now let us see  the object of the class
        Edge ist;

        // Now let us try the exception.
        try

        {

            // printing both the values
            System.out.println("Number of vertices: "
                               + vertices);

            System.out.println("Number of edges: " + e);

            // Now calling the function
            ist = new Edge(vertices);

            // calling the function by iterating the loop
            for (int i = 0; i < e; i++)

            {

                // Now calling the function set_edge
                ist.set_Edge(end[i], start[i]);
            }

            // Now we are calling the print Graph Function
            ist.printGraph();

            // Now we will call the object of class
            // and then we called the function check
            Edge modified = ist.check();

            // If we dont get the flag to be true
            // We can print the output to be None or empty
            if (modified.getFeedbackArcSet(vertices)
                == false)

            {

                System.out.println("None");
            }
        }

        // Try for catch
        // We print empty nodes
        catch (Exception E)

        {

            System.out.println("Empty Nodes");
        }
    }
}
```

**Output**

```
Number of vertices: 4
Number of edges: 5
The Graph is:
1-> 2-> 3
2-> 3
3-> 4
4-> 1
The set of edges in FeedBack arc set: 2 - 3
4 - 1
```