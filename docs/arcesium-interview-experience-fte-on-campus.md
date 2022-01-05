# Arcesium 面试体验(FTE 校内)

> 原文:[https://www . geesforgeks . org/arcesium-面试-体验-fte-在校园内/](https://www.geeksforgeeks.org/arcesium-interview-experience-fte-on-campus/)

整个过程都是在线的。

所有的面试都是通过我们 TPC 办公室的黑客银行代码对平台帮助的，因为他们没有访问校园。

**线上回合:**

共有 32 个问题，分为:

第 1-15 节 MAT/逻辑推理问题。(MCQs)

第 2- 15 节技术问题(同样是 MCQs，但主要是确定输出)

第 3- 2 节编码问题。

第一个问题:https://stackoverflow . com/questions/21077763/数组中数字和不能构成的最小数字

我不记得第二个问题了。

解决一个编码问题并在另外两个部分做得很好(每个部分都有自己的截止点)就足以进行技术面试了。

**第一轮:**

1.从我的简历中问了一点。没有详细说明。

2.检查二叉树是否是 BST

*   First, tell him that we can check whether the ordered traversal is incremental (assuming that all elements are unique), and we can easily distinguish it. But since I will use arrays, it will add extra space complexity. So I suggest another method.
*   Tell him to approach the shooting range. He was satisfied, but asked me if I could improve the space complexity in the Inorder method. I said that we can actually store only the previous elements and keep a condition in the Inorder code. He was satisfied and asked me to code the function.
*   I was asked to make some changes to the code.

3.OOPS

*   The main concepts of are told to all four with examples. Let me demonstrate runtime polymorphism with sample code.

**第二轮:**

1.问我知道哪些技术。我提到了姜戈和其他一些人。要求简单解释一下什么是 Django。

2.让我们假设我们有一个图书馆，里面的书没有在书架上分类。您必须设计一个库软件，以便:

你可以用多个关键词搜索(后来我问是否所有关键词都要包含在书名里)

你必须输出加权结果。例如:如果你的关键词是“汤姆”，有一本书名字中包含“汤姆”3 次，其余的书只有一次，那么它应该先输出包含 3 个“汤姆”的书名，然后输出其余的书名。

*   The first method: suppose we have an array of strings, where the string is the name of the book. For each keyword, we take it as a pattern, perform KMP operation on each string, and calculate the number of times it is repeated. Then, we will have a refined list, and we can iteratively check each keyword in a similar way in the refined list. Then he asked the weight part. I said that we can make an evaluation function accordingly, and maybe we can keep the sum of the occurrences of each keyword as the weight evaluation function. Then he asked me about my shortcomings. (Time complexity is obvious)
*   The second method: use trie. He asked me how Terry looked. Explain him with gestures, because it looks more like a linked list on the screen. He asked me a few questions about how we can use Trie to realize it and what benefits it will bring. I don't think the traditional Trie is the best, so we may need to make some changes to the traditional Trie. He asked me to show these changes by writing its nodes and how I would use it. I didn't think he was convinced enough, so he changed the question.

3.void 指针和 int 指针的区别。以下操作会发生什么。++在 void poiter 上，++在 int 指针上(我想这两个部分我都答错了)。

4.如果我们可以类型化一个空指针，为什么我们需要 int 指针等等。告诉他一些事情，但我不太确定。

5.涉及使用 group by 和 limit 的联接的 SQL 查询。

6.什么是操作系统中的虚拟化？

**第三轮:**

1.A = { 1，4，6，8，9，}(任何随机数，也可以是 10^6)。有一个数字 B = 2 ^ A[0] + 2 ^ A[1] + …

我们需要知道在 B 的二进制表示中，在什么位置会有设置位？(可以是 n 位，而不是 32 /64 )

*   The concept that 2 m equals 1 < < m is used. Therefore, when the numbers in the array are duplicated, the problem is simplified to processing multiple set bits in the same position.

2.什么是抽象类。它有什么用？

3.为什么我们不能做抽象类的对象(答不上来)

4.什么是虚拟化？我们应该为每个进程使用什么样的页面大小？

**小时轮:**

两个候选人(包括我)入围了人力资源轮。我们都被邀请参加了同一个在线视频会议，人力资源告诉我们他们为我们俩提供了机会，并解释了公司的情况。

**干杯！**