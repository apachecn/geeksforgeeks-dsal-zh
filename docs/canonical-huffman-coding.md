# 规范霍夫曼编码

> 原文:[https://www.geeksforgeeks.org/canonical-huffman-coding/](https://www.geeksforgeeks.org/canonical-huffman-coding/)

> [霍夫曼编码](https://www.geeksforgeeks.org/huffman-coding-greedy-algo-3/)是一种无损数据压缩算法，其中数据中的每个字符都被分配一个可变长度的前缀码。最不频繁的字符得到最大的代码，最频繁的字符得到最小的代码。使用这种技术对数据进行编码非常简单有效。然而，解码使用该技术生成的比特流是低效的。解码器(或解压缩器)需要所用编码机制的知识，以便将编码数据解码回原始字符。因此，关于编码过程的信息需要与编码数据一起作为字符表和它们相应的代码传递给解码器。在大数据的常规霍夫曼编码中，该表占用大量存储空间，并且如果数据中存在大量唯一字符，则由于码本的存在，压缩(或编码)的数据大小增加。因此，为了使解码过程在计算上高效并保持良好的压缩比，引入了规范霍夫曼码。

> 在规范霍夫曼编码中，使用为每个符号生成的标准霍夫曼码的比特长度。这些符号首先按照它们的比特长度以非递减的顺序排序，然后对于每个比特长度，它们按照字典顺序排序。第一个符号获得一个包含全零的代码，其长度与原始位长度相同。对于随后的符号，如果符号的位长度等于前一个符号的位长度，则前一个符号的代码**增加 1**，并分配给当前符号。否则，如果该符号的位长度大于前一符号的位长度，则在**递增**后，前一符号的代码为**零被追加，直到该长度等于当前符号的位长度**，然后该代码被分配给当前符号。
> 对于其余符号，此过程继续。

**以下示例说明了该过程:**

**考虑以下数据:**

<figure class="table">

| 性格；角色；字母 | 频率 |
| --- | --- |
| a | Ten |
| b | one |
| c | Fifteen |
| d | seven |

</figure>

**标准霍夫曼码生成位长:**

<figure class="table">

| 性格；角色；字母 | 霍夫曼码 | 位长度 |
| --- | --- | --- |
| a | Eleven | Two |
| b | One hundred | three |
| c | Zero | one |
| d | One hundred and one | three |

**步骤 1:** 根据位长度对数据进行排序，然后针对每个位长度对符号进行字典式排序。

<figure class="table">

| 性格；角色；字母 | 位长度 |
| --- | --- |
| c | one |
| a | Two |
| b | three |
| d | three |

**步骤 2:** 为第一个符号的代码分配与位长相同数量的“0”。
代码为“c”:0
下一个符号“a”的位长为 2 >上一个符号“c”的位长为 1。将前一个符号的代码增加 1，并附加(2-1)=1 个零，然后将代码赋给“a”。
代码为“a”:10
下一个符号“b”的位长为 3 >上一个符号“a”的位长为 2。将前一个符号的代码增加 1，并附加(3-2)=1 个零，并将代码赋给“b”。
b 的代码:110
下一个符号“d”的位长为 3 =前一个符号“b”的位长为 3。将前一个符号的代码增加 1，并将其赋给“d”。
代码为“d”:111

**第三步:**最终结果。

<figure class="table">

| 性格；角色；字母 | 规范霍夫曼码 |
| --- | --- |
| c | Zero |
| a | Ten |
| b | One hundred and ten |
| d | One hundred and eleven |

这种方法的基本优点是传递给解码器的编码信息可以变得更加紧凑和高效。例如，可以简单地将字符或符号的比特长度传递给解码器。规范码可以很容易地从长度中产生，因为它们是连续的。
使用哈夫曼树生成哈夫曼码请参考这里的。

**方法:**一种简单有效的方法是为数据生成霍夫曼树，并使用类似于 java 中 TreeMap 的数据结构来存储符号和位长，以便信息始终保持排序。然后，可以使用递增和按位左移操作来获得规范代码。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for Canonical Huffman Encoding

import java.io.*;
import java.util.*;

// Nodes of Huffman tree
class Node {

    int data;
    char c;

    Node left;
    Node right;
}

// comparator class helps to compare the node
// on the basis of one of its attribute.
// Here we will be compared
// on the basis of data values of the nodes.
class Pq_compare implements Comparator<Node> {
    public int compare(Node a, Node b)
    {

        return a.data - b.data;
    }
}

class Canonical_Huffman {

    // Treemap to store the
    // code lengths(sorted) as keys
    // and corresponding(sorted)
    // set of characters as values
    static TreeMap<Integer, TreeSet<Character> > data;

    // Constructor to initialize the Treemap
    public Canonical_Huffman()
    {
        data = new TreeMap<Integer, TreeSet<Character> >();
    }

    // Recursive function
    // to generate code lengths
    // from regular Huffman codes
    static void code_gen(Node root, int code_length)
    {
        if (root == null)
            return;

        // base case; if the left and right are null
        // then its a leaf node.
        if (root.left == null && root.right == null) {

            // check if key is present or not.
            // If not present add a new treeset
            // as value along with the key
            data.putIfAbsent(code_length, new TreeSet<Character>());

            // c is the character in the node
            data.get(code_length).add(root.c);
            return;
        }

        // Add 1 when on going left or right.
        code_gen(root.left, code_length + 1);
        code_gen(root.right, code_length + 1);
    }

    static void testCanonicalHC(int n, char chararr[], int freq[])
    {

        // min-priority queue(min-heap).
        PriorityQueue<Node> q
            = new PriorityQueue<Node>(n, new Pq_compare());

        for (int i = 0; i < n; i++) {

            // creating a node object
            // and adding it to the priority-queue.
            Node node = new Node();

            node.c = chararr[i];
            node.data = freq[i];

            node.left = null;
            node.right = null;

            // add functions adds
            // the node to the queue.
            q.add(node);
        }

        // create a root node
        Node root = null;

        // extract the two minimum value
        // from the heap each time until
        // its size reduces to 1, extract until
        // all the nodes are extracted.
        while (q.size() > 1) {

            // first min extract.
            Node x = q.peek();
            q.poll();

            // second min extract.
            Node y = q.peek();
            q.poll();

            // new node f which is equal
            Node nodeobj = new Node();

            // to the sum of the frequency of the two nodes
            // assigning values to the f node.
            nodeobj.data = x.data + y.data;
            nodeobj.c = '-';

            // first extracted node as left child.
            nodeobj.left = x;

            // second extracted node as the right child.
            nodeobj.right = y;

            // marking the f node as the root node.
            root = nodeobj;

            // add this node to the priority-queue.
            q.add(nodeobj);
        }

        // Creating a canonical Huffman object
        Canonical_Huffman obj = new Canonical_Huffman();

        // generate code lengths by traversing the tree
        code_gen(root, 0);

        // Object array to store the keys
        Object[] arr = data.keySet().toArray();

        // Set initial canonical code=0
        int c_code = 0, curr_len = 0, next_len = 0;

        for (int i = 0; i < arr.length; i++) {
            Iterator it = data.get(arr[i]).iterator();

            // code length of current character
            curr_len = (int)arr[i];

            while (it.hasNext()) {

                // Display the canonical codes
                System.out.println(it.next() + ":"
                                   + Integer.toBinaryString(c_code));

                // if values set is not
                // completed or if it is
                // the last set set code length
                // of next character as current
                // code length
                if (it.hasNext() || i == arr.length - 1)
                    next_len = curr_len;
                else
                    next_len = (int)arr[i + 1];

                // Generate canonical code
                // for next character using
                // regular code length of next
                // character
                c_code = (c_code + 1) << (next_len - curr_len);
            }
        }
    }

    // Driver code
    public static void main(String args[]) throws IOException
    {
        int n = 4;
        char[] chararr = { 'a', 'b', 'c', 'd' };
        int[] freq = { 10, 1, 15, 7 };
        testCanonicalHC(n, chararr, freq);
    }
}
```

**Output:** 

```
c:0
a:10
b:110
d:111
```

</figure>

</figure>

</figure>