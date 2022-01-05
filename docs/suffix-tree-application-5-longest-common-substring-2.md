# 后缀树应用 5–最长公共子串

> 原文:[https://www . geesforgeks . org/后缀-树-应用-5-最长-公共-子串-2/](https://www.geeksforgeeks.org/suffix-tree-application-5-longest-common-substring-2/)

给定两个字符串 X 和 Y，找到 X 和 Y 的[最长公共子串](https://en.wikipedia.org/wiki/Longest_common_substring_problem)
幼稚【O(N*M)<sup>2</sup>】和动态规划【O(N * M)】方法已经在[这里](https://www.geeksforgeeks.org/longest-common-substring/)讨论过了。
在本文中，我们将讨论使用后缀树寻找 LCS 的线性时间方法(第 5 <sup>次</sup>后缀树应用)。
这里我们将为两个字符串 X 和 Y 构建通用后缀树，正如已经在:
[通用后缀树 1](https://www.geeksforgeeks.org/generalized-suffix-tree-1/)
中讨论的那样。让我们举一个与我们在[通用后缀树 1](https://www.geeksforgeeks.org/generalized-suffix-tree-1/) 中看到的相同的例子(X = xabxa，Y = babxba)。
我们在那里为 X 和 Y 建立了以下后缀树:

![Longest Common Substring](img/03d7219a95cbe3c2c161b9940bc4a43e.png)

这是 xabxa#babxba{content}#xA0 的通用后缀树；
上图中，后缀索引在[0，4]的叶子是字符串 xabxa 的后缀，后缀索引在[6，11]的叶子是字符串 babxa 的后缀。为什么呢？？
因为在串联字符串 xabxa#babxba$，字符串 xabxa 的索引是 0，长度是 5，所以它的后缀的索引是 0，1，2，3 和 4。类似地，字符串 babxba 的索引是 6，它的长度是 6，所以它的后缀的索引是 6，7，8，9，10 和 11。
由此我们可以看到，在上面的广义后缀树图中，有一些内部节点从
开始有叶子在下面

*   字符串 X 和 Y(即至少有一个叶的后缀索引在[0，4]中，一个叶的后缀索引在[6，11]中)
*   仅字符串 X(即所有叶节点的后缀索引都在[0，4]中)
*   仅字符串 Y(即所有叶节点在[6，11]中都有后缀索引)

下图显示了标记为“XY”、“X”或“Y”的内部节点，这取决于叶子所属的字符串，即它们自身下面的字符串。

![Longest Common Substring](img/42fcc1c54307940232107ab8691553fb.png)

这些“XY”、“X”或“Y”标记是什么意思？
从根到内部节点的路径标签给出了一个 X 或 Y 的子串，或者两者都有。
对于标记为 XY 的节点，从根到该节点的子串同时属于字符串 X 和 y。
对于标记为 X 的节点，从根到该节点的子串只属于字符串 X。
对于标记为 Y 的节点，从根到该节点的子串只属于字符串 Y。
看上图，能看出如何得到 X 和 Y 的 LCS 吗？
到现在应该清楚了，如何至少得到 X 和 Y 的公共子串。
如果我们遍历从根到标记为 XY 的节点的路径，我们将获得 X 和 y 的公共子串。
现在我们需要在所有这些公共子串中找到最长的一个。
你能想到现在怎么去 LCS 吗？回想一下，我们是如何使用后缀树在给定的字符串中获得[最长重复子串](https://www.geeksforgeeks.org/suffix-tree-application-3-longest-repeated-substring/)的。
从根到标记为 XY 的最深节点的路径标签将给出 X 和 y 的 LCS，最深节点在上图中突出显示，从根到该节点的路径标签“abx”是 X 和 y 的 LCS。

## C

```
// A C program to implement Ukkonen's Suffix Tree Construction
// Here we build generalized suffix tree for two strings
// And then we find longest common substring of the two input strings
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
     connect two nodes,  one parent and one child, and
     (start, end) interval of a given edge  will be stored
     in the child node. Lets say there are two nods A and B
     connected by an edge with indices (5, 8) then this
     indices (5, 8) will be stored in node B. */
    int start;
    int *end;

    /*for leaf nodes, it stores the index of suffix for
      the path  from root to leaf*/
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
int size1 = 0; //Size of 1st string

Node *newNode(int start, int *end)
{
    Node *node =(Node*) malloc(sizeof(Node));
    int i;
    for (i = 0; i < MAX_CHAR; i++)
          node->children[i] = NULL;

    /*For root node, suffixLink will be set to NULL
    For internal nodes, suffixLink will be set to root
    by default in  current extension and may change in
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
    if(n == root)
        return 0;
    return *(n->end) - (n->start) + 1;
}

int walkDown(Node *currNode)
{
    /*activePoint change for walk down (APCFWD) using
     Skip/Count Trick  (Trick 1). If activeLength is greater
     than current edge length, set next  internal node as
     activeNode and adjust activeEdge and activeLength
     accordingly to represent same activePoint*/
    if (activeLength >= edgeLength(currNode))
    {
        activeEdge += edgeLength(currNode);
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

        if (activeLength == 0)
            activeEdge = pos; //APCFALZ

        // There is no outgoing edge starting with
        // activeEdge from activeNode
        if (activeNode->children] == NULL)
        {
            //Extension Rule 2 (A new leaf edge gets created)
            activeNode->children] =
                                          newNode(pos, &leafEnd);

            /*A new leaf edge is created in above line starting
             from  an existing node (the current activeNode), and
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
            Node *next = activeNode->children];
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
              being processed is not  on the edge (we fall off
              the tree). In this case, we add a new internal node
              and a new leaf edge going out of that new node. This
              is Extension Rule 2, where a new leaf edge and a new
            internal node get created*/
            splitEnd = (int*) malloc(sizeof(int));
            *splitEnd = next->start + activeLength - 1;

            //New internal node
            Node *split = newNode(next->start, splitEnd);
            activeNode->children] = split;

            //New leaf coming out of new internal node
            split->children] = newNode(pos, &leafEnd);
            next->start += activeLength;
            split->children] = next;

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
            activeEdge = pos - remainingSuffixCount + 1;
        }
        else if (activeNode != root) //APCFER2C2
        {
            activeNode = activeNode->suffixLink;
        }
    }
}

void print(int i, int j)
{
    int k;
    for (k=i; k<=j && text[k] != '#'; k++)
        printf("%c", text[k]);
    if(k<=j)
        printf("#");
}

//Print the suffix tree as well along with setting suffix index
//So tree will be printed in DFS manner
//Each edge along with it's suffix index will be printed
void setSuffixIndexByDFS(Node *n, int labelHeight)
{
    if (n == NULL)  return;

    if (n->start != -1) //A non-root node
    {
        //Print the label on edge from parent to current node
        //Uncomment below line to print suffix tree
        //print(n->start, *(n->end));
    }
    int leaf = 1;
    int i;
    for (i = 0; i < MAX_CHAR; i++)
    {
        if (n->children[i] != NULL)
        {
            //Uncomment below two lines to print suffix index
         //   if (leaf == 1 && n->start != -1)
           //     printf(" [%d]\n", n->suffixIndex);

            //Current node is not a leaf as it has outgoing
            //edges from it.
            leaf = 0;
            setSuffixIndexByDFS(n->children[i], labelHeight +
                                  edgeLength(n->children[i]));
        }
    }
    if (leaf == 1)
    {
        for(i= n->start; i<= *(n->end); i++)
        {
            if(text[i] == '#')
            {
                n->end = (int*) malloc(sizeof(int));
                *(n->end) = i;
            }
        }
        n->suffixIndex = size - labelHeight;
        //Uncomment below line to print suffix index
       // printf(" [%d]\n", n->suffixIndex);
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
}

int doTraversal(Node *n, int labelHeight, int* maxHeight,
int* substringStartIndex)
{
    if(n == NULL)
    {
        return;
    }
    int i=0;
    int ret = -1;
    if(n->suffixIndex < 0) //If it is internal node
    {
        for (i = 0; i < MAX_CHAR; i++)
        {
            if(n->children[i] != NULL)
            {
                ret = doTraversal(n->children[i], labelHeight +
                    edgeLength(n->children[i]),
                    maxHeight, substringStartIndex);

                if(n->suffixIndex == -1)
                    n->suffixIndex = ret;
                else if((n->suffixIndex == -2 && ret == -3) ||
                    (n->suffixIndex == -3 && ret == -2) ||
                    n->suffixIndex == -4)
                {
                    n->suffixIndex = -4;//Mark node as XY
                    //Keep track of deepest node
                    if(*maxHeight < labelHeight)
                    {
                        *maxHeight = labelHeight;
                        *substringStartIndex = *(n->end) -
                            labelHeight + 1;
                    }
                }
            }
        }
    }
    else if(n->suffixIndex > -1 && n->suffixIndex < size1)//suffix of X
        return -2;//Mark node as X
    else if(n->suffixIndex >= size1)//suffix of Y
        return -3;//Mark node as Y
    return n->suffixIndex;
}

void getLongestCommonSubstring()
{
    int maxHeight = 0;
    int substringStartIndex = 0;
    doTraversal(root, 0, &maxHeight, &substringStartIndex);

    int k;
    for (k=0; k<maxHeight; k++)
        printf("%c", text[k + substringStartIndex]);
    if(k == 0)
        printf("No common substring");
    else
        printf(", of length: %d",maxHeight);
    printf("\n");
}

// driver program to test above functions
int main(int argc, char *argv[])
{
    size1 = 7;
    printf("Longest Common Substring in xabxac and abcabxabcd is: ");
    strcpy(text, "xabxac#abcabxabcd{content}quot;); buildSuffixTree();
    getLongestCommonSubstring();
    //Free the dynamically allocated memory
    freeSuffixTreeByPostOrder(root);

    size1 = 10;
    printf("Longest Common Substring in xabxaabxa and babxba is: ");
    strcpy(text, "xabxaabxa#babxba{content}quot;); buildSuffixTree();
    getLongestCommonSubstring();
    //Free the dynamically allocated memory
    freeSuffixTreeByPostOrder(root);

    size1 = 14;
    printf("Longest Common Substring in GeeksforGeeks and GeeksQuiz is: ");
    strcpy(text, "GeeksforGeeks#GeeksQuiz{content}quot;); buildSuffixTree();
    getLongestCommonSubstring();
    //Free the dynamically allocated memory
    freeSuffixTreeByPostOrder(root);

    size1 = 26;
    printf("Longest Common Substring in OldSite:GeeksforGeeks.org");
    printf(" and NewSite:GeeksQuiz.com is: ");
    strcpy(text, "OldSite:GeeksforGeeks.org#NewSite:GeeksQuiz.com{content}quot;);
    buildSuffixTree();
    getLongestCommonSubstring();
    //Free the dynamically allocated memory
    freeSuffixTreeByPostOrder(root);

    size1 = 6;
    printf("Longest Common Substring in abcde and fghie is: ");
    strcpy(text, "abcde#fghie{content}quot;); buildSuffixTree();
    getLongestCommonSubstring();
    //Free the dynamically allocated memory
    freeSuffixTreeByPostOrder(root);

    size1 = 6;
    printf("Longest Common Substring in pqrst and uvwxyz is: ");
    strcpy(text, "pqrst#uvwxyz{content}quot;); buildSuffixTree();
    getLongestCommonSubstring();
    //Free the dynamically allocated memory
    freeSuffixTreeByPostOrder(root);

    return 0;
}
```

**输出:**

```
Longest Common Substring in xabxac and abcabxabcd is: abxa, of length: 4
Longest Common Substring in xabxaabxa and babxba is: abx, of length: 3
Longest Common Substring in GeeksforGeeks and GeeksQuiz is: Geeks, of length: 5
Longest Common Substring in OldSite:GeeksforGeeks.org and 
NewSite:GeeksQuiz.com is: Site:Geeks, of length: 10
Longest Common Substring in abcde and fghie is: e, of length: 1
Longest Common Substring in pqrst and uvwxyz is: No common substring
```

如果两个字符串的大小是 M 和 N，那么广义后缀树的构造采用 O(M+N)，LCS 发现是树上的 DFS，它也是 O(M+N)。
所以整体复杂度在时间和空间上是线性的。
**后续:**

1.  给定一个模式，检查它是 X 的子串还是 Y 的子串，或者两者都是。如果它是一个子字符串，查找它的所有出现以及它属于哪个字符串(X 或 Y 或两者)。

2.  扩展实现以找到两个以上字符串的 LCS
3.  解决两个以上字符串的问题 1
4.  给定一个字符串，找到它的[最长回文子串](https://en.wikipedia.org/wiki/Longest_palindromic_substring)

我们发表了以下更多关于后缀树应用的文章:

*   [后缀树应用 1–子串检查](https://www.geeksforgeeks.org/suffix-tree-application-1-substring-check/)

*   [后缀树应用 2–搜索所有模式](https://www.geeksforgeeks.org/suffix-tree-application-2-searching-all-patterns/)

*   [后缀树应用 3–最长重复子串](https://www.geeksforgeeks.org/suffix-tree-application-3-longest-repeated-substring/)

*   [后缀树应用 4–构建线性时间后缀数组](https://www.geeksforgeeks.org/suffix-tree-application-4-build-linear-time-suffix-array/)

*   [后缀树应用 6–最长回文子串](https://www.geeksforgeeks.org/suffix-tree-application-6-longest-palindromic-substring/)

*   [广义后缀树 1](https://www.geeksforgeeks.org/generalized-suffix-tree-1/)

本文由**阿努拉格·辛格**供稿。如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论