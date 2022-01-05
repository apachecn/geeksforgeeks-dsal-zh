# 反转布伦斯-惠勒变换

> 原文:[https://www . geeksforgeeks . org/inventing-burrows-wheeler-transform/](https://www.geeksforgeeks.org/inverting-burrows-wheeler-transform/)

**先决条件:** [布伦斯-惠勒数据转换算法](https://www.geeksforgeeks.org/burrows-wheeler-data-transform-algorithm/)

**为什么反 BWT？背后的主要思想:**

1.BWT 算法的显著之处在于，这种特殊的变换是可逆的，并且数据开销最小。

2.计算 BWT 逆就是撤销 BWT 并恢复原始字符串。实现这个算法的天真方法可以从 [**这里**](https://en.wikipedia.org/wiki/Burrows%E2%80%93Wheeler_transform) 开始研究。简单的方法是速度和内存密集型的，需要我们存储|文本|字符串的循环旋转|文本|。

3.让我们讨论一个更快的算法，其中我们只有两件事:
i. **bwt_arr[]** ，这是排序旋转列表的最后一列**，给出为**“annb $ aa”**。
二。**‘x’**这是我们的原始字符串**“香蕉{content}”所在的行索引。**出现在排序的循环列表中。我们可以看到**‘x’在下面的例子中是 4** 。**

```
 Row Index    Original Rotations    Sorted Rotations
 ~~~~~~~~~    ~~~~~~~~~~~~~~~~~~    ~~~~~~~~~~~~~~~~
    0             banana$               $banana
    1             anana$b               a$banan
    2             nana$ba               ana$ban
    3             ana$ban               anana$b
   *4             na$bana               banana$
    5             a$banan               na$bana
    6             $banana               nana$ba

```

4.**一个重要的观察:**如果第 JT 个原始旋转(也就是向左移动了 j 个字符的原始旋转)是排序顺序中的第 I 行，那么 **l_shift[i]** 按照排序顺序记录第(j+1)个原始旋转出现的位置。例如，第 0 个原始旋转**“香蕉{内容} ”;**是排序顺序的第 4 行，由于 l_shift[4]是 3，下一个原始旋转**“anana $ b”**是排序顺序的第 3 行。

```
Row Index  Original Rotations  Sorted Rotations l_shift 
~~~~~~~~~ ~~~~~~~~~~~~~~~~~~  ~~~~~~~~~~~~~~~~  ~~~~~~~
   0           banana$         $banana           4
   1           anana$b         a$banan           0
   2           nana$ba         ana$ban           5
   3           ana$ban         anana$b           6
  *4           na$bana         banana$           3
   5           a$banan         na$bana           1
   6           $banana         nana$ba           2

```

5.我们的工作是从我们可获得的信息中推导出 **l_shift[]** ，即 **bwt_arr[]** 和 **'x'** ，并在它的帮助下计算出 bwt 的倒数。

**如何计算 l_shift[]？**
1。我们知道 BWT 是“T4”。这意味着我们知道原始字符串的所有字符，即使它们是以错误的顺序排列的。

2.通过排序 **bwt_arr[]** ，我们可以重构排序旋转列表的第一列，我们称之为**排序 _bwt[]** 。

```
 Row Index    Sorted Rotations   bwt_arr    l_shift  
 ~~~~~~~~~    ~~~~~~~~~~~~~~~~~~~~~~~~~~    ~~~~~~~   
     0         $  ?  ?  ?  ?  ?  a             4
     1         a  ?  ?  ?  ?  ?  n
     2         a  ?  ?  ?  ?  ?  n
     3         a  ?  ?  ?  ?  ?  b
    *4         b  ?  ?  ?  ?  ?  $             3
     5         n  ?  ?  ?  ?  ?  a
     6         n  ?  ?  ?  ?  ?  a

```

3.自 **'{content} '起；**在字符串 **'sorted_bwt[]'** 中只出现一次，旋转是使用循环环绕形成的，我们可以推导出 **l_shift[0] = 4。**同样，**‘b’**出现一次，所以我们可以推导出 **l_shift[4] = 3。**

4.但是，因为**‘n’**出现了两次，所以 l_shift[5] = 1 和 l_shift[6] = 2 还是 l_shift[5] = 2 和 l_shift[6] = 1 就显得模糊了**。**

5.解决这个歧义的规则是**如果行 I 和 j 都以相同的字母 I 和 i < j 开始，那么 l_shift[i] < l_shift[j]** 。这意味着 l_shift[5] = 1，l_shift[6] =2。以类似的方式继续， **l_shift[]** 计算如下。

```
 Row Index    Sorted Rotations   bwt_arr    l_shift  
 ~~~~~~~~~    ~~~~~~~~~~~~~~~~~~~~~~~~~~    ~~~~~~~   
     0         $  ?  ?  ?  ?  ?  a             4
     1         a  ?  ?  ?  ?  ?  n             0
     2         a  ?  ?  ?  ?  ?  n             5
     3         a  ?  ?  ?  ?  ?  b             6
    *4         b  ?  ?  ?  ?  ?  $             3
     5         n  ?  ?  ?  ?  ?  a             1
     6         n  ?  ?  ?  ?  ?  a             2

```

**歧义消解规则为什么有效？**

1.旋转以这样的方式排序，即第 5 行在字典上小于第 6 行。

2.因此，第 5 行中的五个未知字符必须少于第 6 行中的五个未知字符(因为两者都以**‘n’**开头)。

3.我们还知道，两行之间比以**‘n’**结尾，第 1 行比第 2 行低。

4.但是，第 5 行和第 6 行中的五个未知字符恰恰是第 1 行和第 2 行中的前五个字符，否则这将与循环排序的事实相矛盾。

5.因此， **l_shift[5] = 1** 和 **l_shift[6] = 2。**

**实施方式:**

1.**BWT 排序:**使用 **qsort()** ，我们将 **bwt_arr[]** 的字符按排序顺序排列，并存储在 **sorted_arr[]** 中。

2.**计算 l_shift[]:**
i .我们取一个指针数组 **struct node *arr[]** ，每个指针都指向一个链表。

二.使 **bwt_arr[]** 的每个不同字符成为链表的头节点，我们将节点附加到链表，链表的数据部分包含该字符在 **bwt_arr[]** 中出现的索引。

```
   i        *arr[128]           Linked Lists
~~~~~~~~~    ~~~~~~~~~      ~~~~~~~~~~~~~~~~~~~~~~  
   37          $     ----->    4 ->  NULL
   97          a     ----->    0 -> 5 -> 6 -> NULL
   110         n     ----->    1 -> 2 -> NULL
   98          b     ----->    3 -> NULL

```

三.将**排序后的 _ bwt【】**头做成不同的字符，遍历链表，得到相应的**l _ shift【】**值。

```
     int[] l_shift = { 4, 0, 5, 6, 3, 1, 2 };

```

3.迭代字符串长度次，我们用 **x = l_shift[x]** 解码 BWT，并输出 **bwt_arr[x]。**

```
     x = l_shift[4] 
     x = 3
     bwt_arr[3] = 'b'

     x = l_shift[3] 
     x = 6
     bwt_arr[6] = 'a'

```

示例:

```
Input : annb$aa // Burrows - Wheeler Transform
        4 // Row index at which original message 
          // appears in sorted rotations list 
Output : banana$

Input : ard$rcaaaabb
        3
Output : abracadabra$

```

下面是上面解释的实现方式的 C 代码:

```
// C program to find inverse of Burrows
// Wheeler transform
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// Structure to store info of a node of
// linked list
struct node {
    int data;
    struct node* next;
};

// Compares the characters of bwt_arr[]
// and sorts them alphabetically
int cmpfunc(const void* a, const void* b)
{
    const char* ia = (const char*)a;
    const char* ib = (const char*)b;
    return strcmp(ia, ib);
}

// Creates the new node
struct node* getNode(int i)
{
    struct node* nn = 
        (struct node*)malloc(sizeof(struct node));
    nn->data = i;
    nn->next = NULL;
    return nn;
}

// Does insertion at end in the linked list
void addAtLast(struct node** head, struct node* nn)
{
    if (*head == NULL) {
        *head = nn;
        return;
    }
    struct node* temp = *head;
    while (temp->next != NULL)
        temp = temp->next;
    temp->next = nn;
}

// Computes l_shift[]
void* computeLShift(struct node** head, int index,
                    int* l_shift)
{
    l_shift[index] = (*head)->data;
    (*head) = (*head)->next;
}

void invert(char bwt_arr[])
{
    int i,len_bwt = strlen(bwt_arr);
    char* sorted_bwt = (char*)malloc(len_bwt * sizeof(char));
    strcpy(sorted_bwt, bwt_arr);
    int* l_shift = (int*)malloc(len_bwt * sizeof(int));

    // Index at which original string appears
    // in the sorted rotations list
    int x = 4;

    // Sorts the characters of bwt_arr[] alphabetically
    qsort(sorted_bwt, len_bwt, sizeof(char), cmpfunc);

    // Array of pointers that act as head nodes
    // to linked lists created to compute l_shift[]
    struct node* arr[128] = { NULL };

    // Takes each distinct character of bwt_arr[] as head
    // of a linked list and appends to it the new node
    // whose data part contains index at which
    // character occurs in bwt_arr[]
    for (i = 0; i < len_bwt; i++) {
        struct node* nn = getNode(i);
        addAtLast(&arr[bwt_arr[i]], nn);
    }

    // Takes each distinct character of sorted_arr[] as head
    // of a linked list and finds l_shift[]
    for (i = 0; i < len_bwt; i++)
        computeLShift(&arr[sorted_bwt[i]], i, l_shift);

    printf("Burrows - Wheeler Transform: %s\n", bwt_arr);
    printf("Inverse of Burrows - Wheeler Transform: ");
    // Decodes the bwt
    for (i = 0; i < len_bwt; i++) {
        x = l_shift[x];
        printf("%c", bwt_arr[x]);
    }
}

// Driver program to test functions above
int  main()
{
    char bwt_arr[] = "annb$aa";
    invert(bwt_arr);
    return 0;
}
```

输出:

```

Burrows - Wheeler Transform: annb$aa
Inverse of Burrows - Wheeler Transform: banana$

```

**时间复杂度:** O(nLogn)作为 qsort()占用 O(nLogn)时间。

**练习:**在 O(n)时间内实现 Burrows-Wheeler 变换的逆变换。

**来源:**
[http://www . cs . Princeton . edu/courses/archive/fall 07/cos226/assignments/burrows . html](http://www.cs.princeton.edu/courses/archive/fall07/cos226/assignments/burrows.html)

本文由 [**阿努里特考尔**](https://www.quora.com/profile/Anureet-Kaur-30) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。