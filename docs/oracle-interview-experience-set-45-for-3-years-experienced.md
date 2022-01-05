# 甲骨文面试经验|第 45 集(3 年经验)

> 原文:[https://www . geesforgeks . org/Oracle-面试-经验-设置-3 年 45-经验/](https://www.geeksforgeeks.org/oracle-interview-experience-set-45-for-3-years-experienced/)

甲骨文 3 年 Java 经验丰富的加尔各答位置。我参加了两轮。

**第 1 轮**

1.  List the prime factorization of numbers from 1 to 10000
2.  List Armstrong numbers from 1 to 500.
3.  Write 5 features from 5 classes of the collection framework.
4.  Find the missing number from the given pattern. It's easy, but now I can't remember the exact pattern.

**第 2 轮**

1.  The Find Middle element in the LinkedList only traverses once and contains millions of pieces of data, and no extra memory space is used.

    ```
    public E getMidElement() {
        E header = null;
        Iterator<E> increementIterator = linkedList.iterator();
        Iterator<E> headerIterator = linkedList.iterator();
        int counter = 0;
        header = null;
        while (increementIterator.hasNext()) {
            counter++;
            if (counter % 2 == 0)
                header = headerIterator.next();
            increementIterator.next();
        }
        if (counter % 2 != 0) {
            header = headerIterator.next();
        }
        return header;
    }
    ```

2.  List the consecutive elements with the largest sum in the array containing signed integers.
3.  Print odd numbers in one thread and even numbers in another thread, but the final printing will be in normal order, such as 1 2 3 4 5 ...

    如果您喜欢 GeeksforGeeks 并想投稿，您也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或将您的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

    发现有不正确的地方请写评论，或者想分享更多以上讨论话题的信息。

    ## 相关练习题

    [阿姆斯特朗数字](https://practice.geeksforgeeks.org/problems/armstrong-numbers/0)[卡丹算法](https://practice.geeksforgeeks.org/problems/kadanes-algorithm/0)