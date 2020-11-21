# 链表

> 原文：[https://www.geeksforgeeks.org/sum-of-all-subset-sums-of-a-linked-list/](https://www.geeksforgeeks.org/sum-of-all-subset-sums-of-a-linked-list/)

的所有子集总和

给定一个链表，任务是找到链表所有子集的总和。

**示例**：

> **输入**：2-> 3->空
> **输出**：10
> **说明**：
> 所有非空子集 是{2}，{3}和{2，3}
> 总和= 2 + 3 +（2 + 3）= 10
> 
> **输入**：2-> 1-> 5-> 6->空
> **输出**：112

**方法**：考虑所有可能的子集，我们可以观察到每个节点出现 **2 <sup>（N – 1）</sup>** 次。 因此，所有节点与 2 <sup>（N – 1）</sup>之和的乘积给出了最终答案。

下面是上述方法的实现：

## C++

```cpp

<div id="highlighter_918399" class="syntaxhighlighter nogutter  "><table border="0" cellpadding="0" cellspacing="0"><tbody><tr><td class="code"><div class="container"><div class="line number1 index0 alt2"><code class="comments">// C++ implementation to find the </code></div><div class="line number2 index1 alt1"><code class="comments">// sum of values of all subsets of linked list. </code></div><div class="line number3 index2 alt2"><code class="preprocessor">#include <bits/stdc++.h> </code></div><div class="line number4 index3 alt1"><code class="keyword bold">using</code> <code class="keyword bold">namespace</code> <code class="plain">std; </code></div><div class="line number5 index4 alt2"><code class="undefined spaces"> </code> </div><div class="line number6 index5 alt1"><code class="comments">/* A Linked list node */</code></div><div class="line number7 index6 alt2"><code class="keyword bold">struct</code> <code class="plain">Node { </code></div><div class="line number8 index7 alt1"><code class="undefined spaces">    </code><code class="color1 bold">int</code> <code class="plain">data; </code></div><div class="line number9 index8 alt2"><code class="undefined spaces">    </code><code class="keyword bold">struct</code> <code class="plain">Node* next; </code></div><div class="line number10 index9 alt1"><code class="plain">}; </code></div><div class="line number11 index10 alt2"><code class="undefined spaces"> </code> </div><div class="line number12 index11 alt1"><code class="comments">// function to insert a node at the </code></div><div class="line number13 index12 alt2"><code class="comments">// beginning of the linked list </code></div><div class="line number14 index13 alt1"><code class="keyword bold">void</code> <code class="plain">push(</code><code class="keyword bold">struct</code> <code class="plain">Node** head_ref, </code><code class="color1 bold">int</code> <code class="plain">new_data) </code></div><div class="line number15 index14 alt2"><code class="plain">{ </code></div><div class="line number16 index15 alt1"><code class="undefined spaces">    </code><code class="comments">/* allocate node */</code></div><div class="line number17 index16 alt2"><code class="undefined spaces">    </code><code class="keyword bold">struct</code> <code class="plain">Node* new_node = </code><code class="keyword bold">new</code> <code class="plain">Node; </code></div><div class="line number18 index17 alt1"><code class="undefined spaces"> </code> </div><div class="line number19 index18 alt2"><code class="undefined spaces">    </code><code class="comments">/* put in the data */</code></div><div class="line number20 index19 alt1"><code class="undefined spaces">    </code><code class="plain">new_node->data = new_data; </code></div><div class="line number21 index20 alt2"><code class="undefined spaces"> </code> </div><div class="line number22 index21 alt1"><code class="undefined spaces">    </code><code class="comments">/* link the old list to the new node */</code></div><div class="line number23 index22 alt2"><code class="undefined spaces">    </code><code class="plain">new_node->next = (*head_ref); </code></div><div class="line number24 index23 alt1"><code class="undefined spaces"> </code> </div><div class="line number25 index24 alt2"><code class="undefined spaces">    </code><code class="comments">/* move the head to point to the new node */</code></div><div class="line number26 index25 alt1"><code class="undefined spaces">    </code><code class="plain">(*head_ref) = new_node; </code></div><div class="line number27 index26 alt2"><code class="plain">} </code></div><div class="line number28 index27 alt1"><code class="undefined spaces"> </code> </div><div class="line number29 index28 alt2"><code class="comments">// function to find the </code></div><div class="line number30 index29 alt1"><code class="comments">// sum of values of all subsets of linked list. </code></div><div class="line number31 index30 alt2"><code class="color1 bold">int</code> <code class="plain">sumOfNodes(</code><code class="keyword bold">struct</code> <code class="plain">Node* head) </code></div><div class="line number32 index31 alt1"><code class="plain">{ </code></div><div class="line number33 index32 alt2"><code class="undefined spaces">    </code><code class="keyword bold">struct</code> <code class="plain">Node* ptr = head; </code></div><div class="line number34 index33 alt1"><code class="undefined spaces">    </code><code class="color1 bold">int</code> <code class="plain">sum = 0; </code></div><div class="line number35 index34 alt2"><code class="undefined spaces">    </code><code class="color1 bold">int</code> <code class="plain">n = 0; </code><code class="comments">// size of linked list </code></div><div class="line number36 index35 alt1"><code class="undefined spaces">    </code><code class="keyword bold">while</code> <code class="plain">(ptr != NULL) { </code></div><div class="line number37 index36 alt2"><code class="undefined spaces"> </code> </div><div class="line number38 index37 alt1"><code class="undefined spaces">        </code><code class="plain">sum += ptr->data; </code></div><div class="line number39 index38 alt2"><code class="undefined spaces">        </code><code class="plain">ptr = ptr->next; </code></div><div class="line number40 index39 alt1"><code class="undefined spaces">        </code><code class="plain">n++; </code></div><div class="line number41 index40 alt2"><code class="undefined spaces">    </code><code class="plain">} </code></div><div class="line number42 index41 alt1"><code class="undefined spaces"> </code> </div><div class="line number43 index42 alt2"><code class="undefined spaces">    </code><code class="comments">// Every element appears 2^(n-1) times </code></div><div class="line number44 index43 alt1"><code class="undefined spaces">    </code><code class="plain">sum = sum * </code><code class="functions bold">pow</code><code class="plain">(2, n - 1); </code></div><div class="line number45 index44 alt2"><code class="undefined spaces">    </code><code class="keyword bold">return</code> <code class="plain">sum; </code></div><div class="line number46 index45 alt1"><code class="plain">} </code></div><div class="line number47 index46 alt2"><code class="undefined spaces"> </code> </div><div class="line number48 index47 alt1"><code class="comments">// Driver program to test above </code></div><div class="line number49 index48 alt2"><code class="color1 bold">int</code> <code class="plain">main() </code></div><div class="line number50 index49 alt1"><code class="plain">{ </code></div><div class="line number51 index50 alt2"><code class="undefined spaces">    </code><code class="keyword bold">struct</code> <code class="plain">Node* head = NULL; </code></div><div class="line number52 index51 alt1"><code class="undefined spaces"> </code> </div><div class="line number53 index52 alt2"><code class="undefined spaces">    </code><code class="comments">// create linked list 2->1->5->6 </code></div><div class="line number54 index53 alt1"><code class="undefined spaces">    </code><code class="plain">push(&head, 2); </code></div><div class="line number55 index54 alt2"><code class="undefined spaces">    </code><code class="plain">push(&head, 1); </code></div><div class="line number56 index55 alt1"><code class="undefined spaces">    </code><code class="plain">push(&head, 5); </code></div><div class="line number57 index56 alt2"><code class="undefined spaces">    </code><code class="plain">push(&head, 6); </code></div><div class="line number58 index57 alt1"><code class="undefined spaces"> </code> </div><div class="line number59 index58 alt2"><code class="undefined spaces">    </code><code class="plain">cout << sumOfNodes(head); </code></div><div class="line number60 index59 alt1"><code class="undefined spaces">    </code><code class="keyword bold">return</code> <code class="plain">0; </code></div><div class="line number61 index60 alt2"><code class="plain">} </code></div></div></td></tr></tbody></table></div>

```

## Java

```java
Python3

```py

C#

```cs

```

**输出**：

```
112

```

**时间复杂度**：`O(n)`



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。