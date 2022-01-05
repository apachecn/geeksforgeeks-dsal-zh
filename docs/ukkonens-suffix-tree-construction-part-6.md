# Ukkonen 的后缀树构造–第 6 部分

> 原文:[https://www . geeksforgeeks . org/ukkonens-后缀-树-构造-part-6/](https://www.geeksforgeeks.org/ukkonens-suffix-tree-construction-part-6/)

本文是以下五篇文章的续篇:
[Ukkonen 的后缀树构建–第一部分](https://www.geeksforgeeks.org/ukkonens-suffix-tree-construction-part-1/)
[Ukkonen 的后缀树构建–第二部分](https://www.geeksforgeeks.org/ukkonens-suffix-tree-construction-part-2/)
[Ukkonen 的后缀树构建–第三部分](https://www.geeksforgeeks.org/ukkonens-suffix-tree-construction-part-3/)
[Ukkonen 的后缀树构建–第四部分](https://www.geeksforgeeks.org/ukkonens-suffix-tree-construction-part-4/)
[Ukkonen 的后缀树构建–第五部分](https://www.geeksforgeeks.org/ukkonens-suffix-tree-construction-part-5/)
请浏览[第一部分](https://www.geeksforgeeks.org/ukkonens-suffix-tree-construction-part-1/)、 [](https://www.geeksforgeeks.org/ukkonens-suffix-tree-construction-part-5/) [第 4 部分](https://www.geeksforgeeks.org/ukkonens-suffix-tree-construction-part-4/)和[第 5 部分](https://www.geeksforgeeks.org/ukkonens-suffix-tree-construction-part-5/)在看当前文章之前，我们已经看到了一些关于后缀树的基础知识，高级 ukkonen 的算法，后缀链接和三个实现技巧和活动点，以及一个示例字符串“abcabxabcd ”,在这里我们经历了构建后缀树的所有阶段。
在这里，我们将看到用于表示后缀树的数据结构和代码实现。
在[第 5 部分](https://www.geeksforgeeks.org/ukkonens-suffix-tree-construction-part-5/)文章末尾，我们已经讨论了在构建后缀树时以及稍后在不同应用程序中使用后缀树时将要执行的一些操作。
我们可能会想到不同的数据结构来满足需求，其中一些数据结构在某些操作上可能很慢，而另一些则很快。这里，我们将在实现中使用以下内容:

我们将使用后缀树节点结构来表示树中的每个节点。后缀树节点结构将有以下成员:

*   **孩子**–这将是一个字母表大小的数组。这会将当前节点的所有子节点存储在以不同字符开始的不同边上。
*   **后缀链接**–这将通过后缀链接指向当前节点应该指向的其他节点。
*   **开始，结束**–这两个将存储从父节点到当前节点的边标签细节。(start，end) interval 指定边，节点通过该边连接到其父节点。每个边将连接两个节点，一个父节点和一个子节点，给定边的(开始，结束)间隔将存储在子节点中。假设有两个节点 A(父节点)和 B(子节点)通过带有索引(5，8)的边连接，那么这个索引(5，8)将存储在节点 B 中
*   **后缀索引**–这对于叶子来说是非负的，并将给出从根到这个叶子的路径的后缀索引。对于非叶节点，它将是-1。

该数据结构将快速回答所需的查询，如下所示:

*   如何检查节点是否是根节点？—根是一个特殊的节点，没有父节点，因此它的开始和结束将为-1，对于所有其他节点，开始和结束索引将为非负。
*   如何检查节点是内部节点还是叶节点？— suffixIndex 将在此提供帮助。内部节点为-1，叶节点为非负。
*   某条边上路径标签的长度是多少？—每条边都有开始和结束索引，路径标签的长度为结束-开始+1
*   某条边上的路径标签是什么？—如果字符串是 S，则路径标签将是从开始索引到结束索引(包括开始、结束)的 S 的子字符串。
*   如何从节点 A 检查给定字符 c 是否有输出边？—如果 A->子级不为空，则有路径，如果为空，则没有路径。
*   距离节点 A 一定距离 d 的边上的字符值是多少？—距离节点 A 距离为 d 的字符将是 S[A->start + d]，其中 S 是字符串。
*   内部节点通过后缀链接指向哪里？—节点 A 将指向 A->后缀链接
*   从根到叶的路径上的后缀索引是什么？—如果路径上的叶节点是 A，则该路径上的后缀索引将是 A->后缀索引

以下是 Ukkonen 后缀树构造的 C 实现。代码可能看起来有点长，可能是因为注释太多。

## C

```
// A C program to implement Ukkonen's Suffix Tree Construction
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#define MAX_CHAR 256

struct SuffixTreeNode {
    struct SuffixTreeNode *children[MAX_CHAR];

    //pointer to other node via suffix link
    struct SuffixTreeNode *suffixLink;

    /*(start, end) interval specifies the edge, by which the
    node is connected to its parent node. Each edge will
    connect two nodes, one parent and one child, and
    (start, end) interval of a given edge will be stored
    in the child node. Lets say there are two nods A and B
    connected by an edge with indices (5, 8) then this
    indices (5, 8) will be stored in node B. */
    int start;
    int *end;

    /*for leaf nodes, it stores the index of suffix for
    the path from root to leaf*/
    int suffixIndex;
};

typedef struct SuffixTreeNode Node;

char text[100]; //Input string
Node *root = NULL; //Pointer to root node

/*lastNewNode will point to newly created internal node,
waiting for it's suffix link to be set, which might get
a new suffix link (other than root) in next extension of
same phase. lastNewNode will be set to NULL when last
newly created internal node (if there is any) got it's
suffix link reset to new internal node created in next
extension of same phase. */
Node *lastNewNode = NULL;
Node *activeNode = NULL;
int count=0;

/*activeEdge is represented as input string character
index (not the character itself)*/
int activeEdge = -1;
int activeLength = 0;

// remainingSuffixCount tells how many suffixes yet to
// be added in tree
int remainingSuffixCount = 0;
int leafEnd = -1;
int *rootEnd = NULL;
int *splitEnd = NULL;
int size = -1; //Length of input string

Node *newNode(int start, int *end)
{
    count++;
    Node *node =(Node*) malloc(sizeof(Node));
    int i;
    for (i = 0; i < MAX_CHAR; i++)
        node->children[i] = NULL;

    /*For root node, suffixLink will be set to NULL
    For internal nodes, suffixLink will be set to root
    by default in current extension and may change in
    next extension*/
    node->suffixLink = root;
    node->start = start;
    node->end = end;

    /*suffixIndex will be set to -1 by default and
    actual suffix index will be set later for leaves
    at the end of all phases*/
    node->suffixIndex = -1;
    return node;
}

int edgeLength(Node *n) {
    return *(n->end) - (n->start) + 1;
}

int walkDown(Node *currNode)
{
    /*activePoint change for walk down (APCFWD) using
    Skip/Count Trick (Trick 1). If activeLength is greater
    than current edge length, set next internal node as
    activeNode and adjust activeEdge and activeLength
    accordingly to represent same activePoint*/
    if (activeLength >= edgeLength(currNode))
    {
        activeEdge =
         (int)text[activeEdge+edgeLength(currNode)]-(int)' ';
        activeLength -= edgeLength(currNode);
        activeNode = currNode;
        return 1;
    }
    return 0;
}

void extendSuffixTree(int pos)
{
    /*Extension Rule 1, this takes care of extending all
    leaves created so far in tree*/
    leafEnd = pos;

    /*Increment remainingSuffixCount indicating that a
    new suffix added to the list of suffixes yet to be
    added in tree*/
    remainingSuffixCount++;

    /*set lastNewNode to NULL while starting a new phase,
    indicating there is no internal node waiting for
    it's suffix link reset in current phase*/
    lastNewNode = NULL;

    //Add all suffixes (yet to be added) one by one in tree
    while(remainingSuffixCount > 0) {

        if (activeLength == 0) {
            //APCFALZ
            activeEdge = (int)text[pos]-(int)' ';
        }
        // There is no outgoing edge starting with
        // activeEdge from activeNode
        if (activeNode->children[activeEdge] == NULL)
        {
            //Extension Rule 2 (A new leaf edge gets created)
            activeNode->children[activeEdge] =
                                  newNode(pos, &leafEnd);

            /*A new leaf edge is created in above line starting
            from an existing node (the current activeNode), and
            if there is any internal node waiting for it's suffix
            link get reset, point the suffix link from that last
            internal node to current activeNode. Then set lastNewNode
            to NULL indicating no more node waiting for suffix link
            reset.*/
            if (lastNewNode != NULL)
            {
                lastNewNode->suffixLink = activeNode;
                lastNewNode = NULL;
            }
        }
        // There is an outgoing edge starting with activeEdge
        // from activeNode
        else
        {
            // Get the next node at the end of edge starting
            // with activeEdge
            Node *next = activeNode->children[activeEdge];
            if (walkDown(next))//Do walkdown
            {
                //Start from next node (the new activeNode)
                continue;
            }
            /*Extension Rule 3 (current character being processed
            is already on the edge)*/
            if (text[next->start + activeLength] == text[pos])
            {
                //If a newly created node waiting for it's
                //suffix link to be set, then set suffix link
                //of that waiting node to current active node
                if(lastNewNode != NULL && activeNode != root)
                {
                    lastNewNode->suffixLink = activeNode;
                    lastNewNode = NULL;
                }

                //APCFER3
                activeLength++;
                /*STOP all further processing in this phase
                and move on to next phase*/
                break;
            }

            /*We will be here when activePoint is in middle of
            the edge being traversed and current character
            being processed is not on the edge (we fall off
            the tree). In this case, we add a new internal node
            and a new leaf edge going out of that new node. This
            is Extension Rule 2, where a new leaf edge and a new
            internal node get created*/
            splitEnd = (int*) malloc(sizeof(int));
            *splitEnd = next->start + activeLength - 1;

            //New internal node
            Node *split = newNode(next->start, splitEnd);
            activeNode->children[activeEdge] = split;

            //New leaf coming out of new internal node
            split->children[(int)text[pos]-(int)' '] =
                                      newNode(pos, &leafEnd);
            next->start += activeLength;
            split->children[activeEdge] = next;

            /*We got a new internal node here. If there is any
            internal node created in last extensions of same
            phase which is still waiting for it's suffix link
            reset, do it now.*/
            if (lastNewNode != NULL)
            {
            /*suffixLink of lastNewNode points to current newly
            created internal node*/
                lastNewNode->suffixLink = split;
            }

            /*Make the current newly created internal node waiting
            for it's suffix link reset (which is pointing to root
            at present). If we come across any other internal node
            (existing or newly created) in next extension of same
            phase, when a new leaf edge gets added (i.e. when
            Extension Rule 2 applies is any of the next extension
            of same phase) at that point, suffixLink of this node
            will point to that internal node.*/
            lastNewNode = split;
        }

        /* One suffix got added in tree, decrement the count of
        suffixes yet to be added.*/
        remainingSuffixCount--;
        if (activeNode == root && activeLength > 0) //APCFER2C1
        {
            activeLength--;
            activeEdge = (int)text[pos -
                            remainingSuffixCount + 1]-(int)' ';
        }

        //APCFER2C2
        else if (activeNode != root)
        {
            activeNode = activeNode->suffixLink;
        }
    }
}

void print(int i, int j)
{
    int k;
    for (k=i; k<=j; k++)
        printf("%c", text[k]);
}

//Print the suffix tree as well along with setting suffix index
//So tree will be printed in DFS manner
//Each edge along with it's suffix index will be printed
void setSuffixIndexByDFS(Node *n, int labelHeight)
{
    if (n == NULL) return;

    if (n->start != -1) //A non-root node
    {
        //Print the label on edge from parent to current node
        print(n->start, *(n->end));
    }
    int leaf = 1;
    int i;
    for (i = 0; i < MAX_CHAR; i++)
    {
        if (n->children[i] != NULL)
        {
            if (leaf == 1 && n->start != -1)
                printf(" [%d]\n", n->suffixIndex);

            //Current node is not a leaf as it has outgoing
            //edges from it.
            leaf = 0;
            setSuffixIndexByDFS(n->children[i],
                  labelHeight + edgeLength(n->children[i]));
        }
    }
    if (leaf == 1)
    {
        n->suffixIndex = size - labelHeight;
        printf(" [%d]\n", n->suffixIndex);
    }
}

void freeSuffixTreeByPostOrder(Node *n)
{
    if (n == NULL)
        return;
    int i;
    for (i = 0; i < MAX_CHAR; i++)
    {
        if (n->children[i] != NULL)
        {
            freeSuffixTreeByPostOrder(n->children[i]);
        }
    }
    if (n->suffixIndex == -1)
        free(n->end);
    free(n);
}

/*Build the suffix tree and print the edge labels along with
suffixIndex. suffixIndex for leaf edges will be >= 0 and
for non-leaf edges will be -1*/
void buildSuffixTree()
{
    size = strlen(text);
    int i;
    rootEnd = (int*) malloc(sizeof(int));
    *rootEnd = - 1;

    /*Root is a special node with start and end indices as -1,
    as it has no parent from where an edge comes to root*/
    root = newNode(-1, rootEnd);

    activeNode = root; //First activeNode will be root
    for (i=0; i<size; i++)
        extendSuffixTree(i);
    int labelHeight = 0;
    setSuffixIndexByDFS(root, labelHeight);

    //Free the dynamically allocated memory
    freeSuffixTreeByPostOrder(root);
}

// driver program to test above functions
int main(int argc, char *argv[])
{
    strcpy(text, "abbc"); buildSuffixTree();
    printf("Number of nodes in suffix tree are %d\n",count);
    return 0;
}
```

输出(树的每条边，以及边上子节点的后缀索引，以 DFS 顺序打印。为了更好地理解输出，将其与上一篇[第 5 部分](https://www.geeksforgeeks.org/ukkonens-suffix-tree-construction-part-5/)文章中的最后一个数字 43 相匹配:

```
abbc [0]
b [-1]
bc [1]
c [2]
c [3]
Number of nodes in suffix tee are 6
```

现在我们能够在线性时间内构建后缀树，我们可以用有效的方式解决许多字符串问题:

*   检查给定的模式 P 是否是文本 T 的子串(当文本固定且模式改变时有用，否则为 [KMP](https://www.geeksforgeeks.org/searching-for-patterns-set-2-kmp-algorithm/)
*   查找文本中出现的给定模式 P 的所有出现
*   查找最长的重复子串
*   [线性时间后缀数组创建](http://en.wikipedia.org/wiki/Suffix_array#Correspondence_to_suffix_trees)

上述基本问题可以通过后缀树上的 DFS 遍历来解决。
我们很快会发布关于上述问题的文章，以及类似以下的其他文章:

*   构建[通用后缀树](https://www.geeksforgeeks.org/searching-for-patterns-set-2-kmp-algorithm/)
*   线性时间[最长公共子串问题](http://en.wikipedia.org/wiki/Longest_common_substring_problem)
*   线性时间[最长回文子串](http://en.wikipedia.org/wiki/Longest_palindromic_substring)

还有[更](http://en.wikipedia.org/wiki/Suffix_tree#Functionality)。
T3】考验你的理解力？

1.  为字符串“AABAACAADAABAAABAA { content }”绘制后缀树(带有适当的后缀链接、后缀索引)；在纸上，看看是否与代码输出相匹配。
2.  每个扩展都必须遵循三个规则之一:规则 1、规则 2 和规则 3。
    以下是在某些阶段 i (i > 5)中连续五次延期时适用的规则，哪些规则有效:
    A)规则 1、规则 2、规则 2、规则 3、规则 3
    B)规则 1、规则 2、规则 2、规则 3、规则 2
    C)规则 2、规则 1、规则 1、规则 3、规则 3
    D)规则 1、规则 1、规则 1、规则 1、规则 1
    E)规则 2、规则 2、规则 2、规则 2、规则 2 【T6
3.  以上第 5 阶段的有效顺序是什么
4.  每个内部节点必须将其后缀链接设置到另一个节点(内部或根)。新创建的节点能否指向已经存在的内部节点？在扩展 j 中创建的新节点可能不会在下一个扩展 j+1 中获得正确的后缀链接，而在以后的扩展如 j+2、j+3 等中获得正确的后缀链接，这种情况会发生吗？
5.  试着解决上面讨论的基本问题。

我们发表了以下关于后缀树应用的文章:

*   [后缀树应用 1–子串检查](https://www.geeksforgeeks.org/suffix-tree-application-1-substring-check/)
*   [后缀树应用 2–搜索所有模式](https://www.geeksforgeeks.org/suffix-tree-application-2-searching-all-patterns/)
*   [后缀树应用 3–最长重复子串](https://www.geeksforgeeks.org/suffix-tree-application-3-longest-repeated-substring/)
*   [后缀树应用 4–构建线性时间后缀数组](https://www.geeksforgeeks.org/suffix-tree-application-4-build-linear-time-suffix-array/)
*   [广义后缀树 1](https://www.geeksforgeeks.org/generalized-suffix-tree-1/)
*   [后缀树应用 5–最长公共子串](https://www.geeksforgeeks.org/suffix-tree-application-5-longest-common-substring-2/)
*   [后缀树应用 6–最长回文子串](https://www.geeksforgeeks.org/suffix-tree-application-6-longest-palindromic-substring/)

**参考文献**:
[http://web.stanford.edu/~mjkay/gusfield.pdf](http://web.stanford.edu/~mjkay/gusfield.pdf)
[Ukkonen 的后缀树算法通俗易懂](http://stackoverflow.com/questions/9452701/ukkonens-suffix-tree-algorithm-in-plain-english)
本文由 **Anurag Singh** 供稿。如果您发现任何不正确的地方，请写评论，或者您想分享更多关于上面讨论的主题的信息