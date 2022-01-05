# 检查给定的数组是否可以从给定的子序列集合中唯一地构造出来

> 原文:[https://www . geeksforgeeks . org/check-如果给定的数组能够从给定的子序列集中唯一地构造出来/](https://www.geeksforgeeks.org/check-if-the-given-array-can-be-constructed-uniquely-from-the-given-set-of-subsequences/)

给定不同元素的数组 **arr** 和数组的子序列列表 **seqs** ，任务是检查给定的数组是否可以从给定的子序列集合中唯一构造。
**例:**

> **输入:** arr[] = {1，2，3，4}，seqs[][] = {{1，2}，{2，3}，{3，4}}
> **输出:** Yes
> **解释:**序列[1，2]，[2，3]和[3，4]可以唯一地重构
> 原始数组{1，2，3，4}。
> **输入:** arr[] = {1，2，3，4}，seqs[][] = {{1，2}，{2，3}，{2，4}}
> **输出:** No
> **解释:**序列[1，2]，[2，3]和[2，4]不能唯一重构
> {1，2，3，4}。有两种可能的序列可以由给定的序列构建:
> 1) {1，2，3，4}
> 2) {1，2，4，3}

**方法:**
为了解决这个问题，我们需要找到所有数组元素的[拓扑排序](https://www.geeksforgeeks.org/topological-sorting/)，并检查元素是否只存在一个拓扑排序，这可以通过在找到元素拓扑排序的同时，每一瞬间只存在单个源来确认。
以下是上述方法的实施:

## C++

```
// C++ program to Check if 
// the given array can be constructed
// uniquely from the given set of subsequences

#include <bits/stdc++.h>
using namespace std;

bool canConstruct(vector<int> originalSeq,
                vector<vector<int> > sequences)
{
    vector<int> sortedOrder;
    if (originalSeq.size() <= 0) {
        return false;
    }

    // Count of incoming edges for every vertex
    unordered_map<int, int> inDegree;

    // Adjacency list graph
    unordered_map<int, vector<int> > graph;
    for (auto seq : sequences) {
        for (int i = 0; i < seq.size(); i++) {
            inDegree[seq[i]] = 0;
            graph[seq[i]] = vector<int>();
        }
    }

    // Build the graph
    for (auto seq : sequences) {
        for (int i = 1; i < seq.size(); i++) {
            int parent = seq[i - 1], child = seq[i];
            graph[parent].push_back(child);
            inDegree[child]++;
        }
    }

    // if ordering rules for all the numbers
    // are not present
    if (inDegree.size() != originalSeq.size()) {
        return false;
    }

    // Find all sources i.e., all vertices
    // with 0 in-degrees
    queue<int> sources;
    for (auto entry : inDegree) {
        if (entry.second == 0) {
            sources.push(entry.first);
        }
    }

    // For each source, add it to the sortedOrder
    // and subtract one from all of in-degrees
    // if a child's in-degree becomes zero
    // add it to the sources queue
    while (!sources.empty()) {

        // If there are more than one source
        if (sources.size() > 1) {

            // Multiple sequences exist
            return false;
        }

        // If the next source is different from the origin
        if (originalSeq[sortedOrder.size()] !=
                                sources.front()) {
            return false;
        }
        int vertex = sources.front();
        sources.pop();
        sortedOrder.push_back(vertex);
        vector<int> children = graph[vertex];
        for (auto child : children) {

            // Decrement the node's in-degree
            inDegree[child]--;
            if (inDegree[child] == 0) {
                sources.push(child);
            }
        }
    }

    // Compare the sizes of sortedOrder
    // and the original sequence
    return sortedOrder.size() == originalSeq.size();
}

int main(int argc, char* argv[])
{
    vector<int> arr = { 1, 2, 6, 7, 3, 5, 4 };
    vector<vector<int> > seqs = { { 1, 2, 3 },
                                { 7, 3, 5 },
                                { 1, 6, 3, 4 },
                                { 2, 6, 5, 4 } };
    bool result = canConstruct(arr, seqs);
    if (result)
        cout << "Yes" << endl;
    else
        cout << "No" << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Check if
// the given array can be constructed
// uniquely from the given set of subsequences
import java.io.*;
import java.util.*;

class GFG {

    static boolean canConstruct(int[] originalSeq,
                                int[][] sequences)
    {
        List<Integer> sortedOrder
            = new ArrayList<Integer>();
        if (originalSeq.length <= 0) {
            return false;
        }

        // Count of incoming edges for every vertex
        Map<Integer, Integer> inDegree
            = new HashMap<Integer, Integer>();

        // Adjacency list graph
        Map<Integer, ArrayList<Integer> > graph
            = new HashMap<Integer, ArrayList<Integer> >();
        for (int[] seq : sequences)
        {
            for (int i = 0; i < seq.length; i++)
            {
                inDegree.put(seq[i], 0);
                graph.put(seq[i], new ArrayList<Integer>());
            }
        }

        // Build the graph
        for (int[] seq : sequences)
        {
            for (int i = 1; i < seq.length; i++)
            {
                int parent = seq[i - 1], child = seq[i];
                graph.get(parent).add(child);
                inDegree.put(child,
                             inDegree.get(child) + 1);
            }
        }

        // if ordering rules for all the numbers
        // are not present
        if (inDegree.size() != originalSeq.length)
        {
            return false;
        }

        // Find all sources i.e., all vertices
        // with 0 in-degrees
        List<Integer> sources = new ArrayList<Integer>();
        for (Map.Entry<Integer, Integer> entry :
             inDegree.entrySet())
        {
            if (entry.getValue() == 0)
            {
                sources.add(entry.getKey());
            }
        }

        // For each source, add it to the sortedOrder
        // and subtract one from all of in-degrees
        // if a child's in-degree becomes zero
        // add it to the sources queue
        while (!sources.isEmpty())
        {

            // If there are more than one source
            if (sources.size() > 1)
            {

                // Multiple sequences exist
                return false;
            }

            // If the next source is different from the
            // origin
            if (originalSeq[sortedOrder.size()]
                != sources.get(0))
            {
                return false;
            }
            int vertex = sources.get(0);
            sources.remove(0);
            sortedOrder.add(vertex);
            List<Integer> children = graph.get(vertex);
            for (int child : children)
            {

                // Decrement the node's in-degree
                inDegree.put(child,
                             inDegree.get(child) - 1);
                if (inDegree.get(child) == 0)
                {
                    sources.add(child);
                }
            }
        }

        // Compare the sizes of sortedOrder
        // and the original sequence
        return sortedOrder.size() == originalSeq.length;
    }

    // Driver code
    public static void main(String[] args)
    {
        int[] arr = { 1, 2, 6, 7, 3, 5, 4 };
        int[][] seqs = { { 1, 2, 3 },
                         { 7, 3, 5 },
                         { 1, 6, 3, 4 },
                         { 2, 6, 5, 4 } };
        boolean result = canConstruct(arr, seqs);
        if (result)
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by jitin
```

## 蟒蛇 3

```
# Python 3 program to Check if
# the given array can be constructed
# uniquely from the given set of subsequences

def canConstruct(originalSeq, sequences):
    sortedOrder = []
    if (len(originalSeq) <= 0):
        return False

    # Count of incoming edges for every vertex
    inDegree = {i : 0 for i in range(100)}

    # Adjacency list graph
    graph = {i : [] for i in range(100)}
    for seq in sequences:
        for i in range(len(seq)):
            inDegree[seq[i]] = 0
            graph[seq[i]] = []

    # Build the graph
    for seq in sequences:
        for i in range(1, len(seq)):
            parent = seq[i - 1]
            child = seq[i]
            graph[parent].append(child)
            inDegree[child] += 1

    # If ordering rules for all the numbers
    # are not present
    if (len(inDegree) != len(originalSeq)):
        return False

    # Find all sources i.e., all vertices
    # with 0 in-degrees
    sources = []
    for entry in inDegree:
        if (entry[1] == 0):
            sources.append(entry[0])

    # For each source, add it to the sortedOrder
    # and subtract one from all of in-degrees
    # if a child's in-degree becomes zero
    # add it to the sources queue
    while (len(sources) > 0):

        # If there are more than one source
        if (len(sources)  > 1):

            # Multiple sequences exist
            return False

        # If the next source is different from the origin
        if (originalSeq[len(sortedOrder)] != sources[0]):
            return False
        vertex = sources[0]
        sources.remove(sources[0])
        sortedOrder.append(vertex)
        children = graph[vertex]
        for child in children:

            # Decrement the node's in-degree
            inDegree[child] -= 1
            if (inDegree[child] == 0):
                sources.append(child)

    # Compare the sizes of sortedOrder
    # and the original sequence
    return len(sortedOrder) == len(originalSeq)

if __name__ == '__main__':
    arr = [ 1, 2, 6, 7, 3, 5, 4 ]
    seqs = [[ 1, 2, 3 ],
            [ 7, 3, 5 ],
            [ 1, 6, 3, 4 ],
            [ 2, 6, 5, 4 ]]
    result = canConstruct(arr, seqs)
    if (result):
        print("Yes")
    else:
        print("No")

# This code is contributed by Bhupendra_Singh
```

**Output:** 

```
No
```

**时间复杂度:**
上述算法的时间复杂度将为 O(N+E)，其中‘N’为元素个数，‘E’为规则总数。因为，最多每对数字可以给我们一个规则，我们可以得出结论，规则的上限是 O(M)，其中‘M’是所有序列中数字的计数。因此，我们可以说我们的算法的时间复杂度是 O(N + M)。
**辅助空间:** O(N+ M)，因为我们正在为每个元素存储所有可能的规则。