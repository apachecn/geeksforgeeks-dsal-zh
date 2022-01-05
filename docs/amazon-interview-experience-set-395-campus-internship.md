# 亚马逊面试体验|集 395(校内实习)

> 原文:[https://www . geesforgeks . org/Amazon-面试-体验-设置-395-校园-实习/](https://www.geeksforgeeks.org/amazon-interview-experience-set-395-campus-internship/)

**第一轮:**共有 300 名学生参与了入选亚马逊做实习生的想法。
第一轮有 20 个 mcq 和 2 个问题。

1.  Given a range [L,R] find the count of numbers having prime number of set bits in their binary representation. [This hint was included in O/P section. Only even numbers should be checked within the L,R range]
    [GeeksforGeeks Link](https://practice.geeksforgeeks.org/problems/prime-number-of-set-bits/0)

    **示例**:

    ```
    Input : 6 10 
    Output :2
    6 -> 110 (2 set bits, 2 is prime)
    10->1010 (2 set bits , 2 is prime)
    So 6,10 are even numbers having prime number of set bits
    (Use the optimized way to check prime by creating a array 
    of prime numbers and trying to divide the setbit count
    to check if it is prime or not).

    ```

2.  Given n lines a land can be split into many areas of different measure(say b). You are provided with a constant K . You have to find whether it is possible to use K areas from the B areas

    ```
    Input : 2 4
    Output : True
    Think of a circle whenever a circle is split by 
    a n line the total number of areas is given by n*2 
    so the answer will be if(n*2>=k||n+1==k) return True.

    ```

    共有 30 名学生进入下一轮。

**第 2 回合:**
果然是一群飞来飞去的回合。我和我的朋友坐在同一个房间里，被要求编写以下代码:

1.  [重新排列一个字符串中的字符，这样相邻的字符就不会相同](https://practice.geeksforgeeks.org/problems/rearrange-characters/0)
    但是我使用了一个堆栈，我使用了 hashmap 来查找字符的出现。创建了一个用迭代器遍历地图的字符数组。用奇数位置的元素填充字符数组，然后在填充所有奇数位置后，我填充偶数位置。使用验证函数检查新生成的字符串是否没有重复的相邻字符。如果打印为假，则不能形成字符串，否则返回字符串。
2.  Given a tree and a element K . Find the root-leaf path with a sum equalling K and delete the path.[GeeksforGeeks Link](https://practice.geeksforgeeks.org/problems/root-to-leaf-path-sum/1)

    共有 10 人入围。

    接下来是最后一轮。是 F2F 轮。

    **第 3 轮:**
    面试官让我简单介绍一下我。
    然后他继续向我射击编码问题。

    1.  Find the intersection elements in 2 unsorted arrays. [GeeksforGeeks Link](https://practice.geeksforgeeks.org/problems/intersection-of-two-arrays/0)

        ```
        Input: 5 4 1 3 2
               12 3 15 1 7
        Output: 3 1

        ```

        蛮力:O(n^2)
        所以他让我用优化的方式编码。
        给了我三个约束
        大小的 arr1，arr2 是 m，n
        当 m<T8】n(可以忽略不计)，n<T10】m，m 近似 eq 到 n 时怎么办？
        我说当 m 或 n 值可以忽略不计时，我们可以对较小大小的数组进行排序，并制作一个二分搜索法
        排序采用 O(nlogn)和二分搜索法采用 O(logn)，但是由于数组大小可以忽略不计，排序不会花费太多。
        当它们相等(或近似)时，将所有元素推到一个集合，然后搜索(O(logn))，这里我们不使用排序，因为数组大小大致相同，我们使用更多的空间，从而降低时间复杂度，无论如何搜索时间是相同的。

    2.  This was an interesting question . Given Air tickets to different cities in the form of a pair of cities where one denotes the source and another tells the destination.Our job is to return a linkedlist indicating the way the travelling should travel in order to cover all the cities.(Linkedlist wasnt mentioned by the interviewer).

        ```
        Input: (Chennai,Bombay) (Bangalore,Goa) (Agra,Chennai) (Bombay,Bangalore)
        Output Agra->Chennai->Bombay->Bangalore->Goa

        ```

        **解决方法**:放在一个散列表中。现在找出所有城市的出现。在这种情况下，我们可以注意到源和目的地在票证中只出现一次。与原始配对列表交叉检查，找出哪个是源，哪个是目的地。然后在一个单独的比较器函数的帮助下，将这些对推入一个新的散列表中，这样一个对的源一定是前一个对的目的地)。然后遍历新的 hashmap 来创建一个链表，然后返回它。

        如果你要求任何方法，面试官也会帮助你(但不要向他们寻求更多帮助。)但是，如果面试官有意给出一个线索，那么就按照他的意愿编码，因为这是他们测试你是否能适应任何方法和代码的一种方式。

        结果出来了，8 人得到了实习。
        幸好我也在其中。
        我个人的建议:要自信，保持高沟通能力，使用 geeksforgeeks 网站学习链表、Trees、STL 和 DP，然后解决所有公司特有的问题。

        本文由**斯里尼瓦斯**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

        如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。