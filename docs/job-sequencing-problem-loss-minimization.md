# 作业排序问题–损失最小化

> 原文:[https://www . geesforgeks . org/job-sequence-problem-loss-minimum/](https://www.geeksforgeeks.org/job-sequencing-problem-loss-minimization/)

我们被给予编号为 1 到 N 的 N 个作业。对于每个活动，让 Ti 表示完成该作业所需的天数。第一项工作每拖延一天，李就会损失一天。
我们需要找到一个顺序来完成工作，以便将整体损失降至最低。我们一次只能做一项工作。

如果多个这样的解是可能的，那么我们需要给出字典序最小排列(即字典顺序中最早的排列)。

示例:

```
Input : L = {3, 1, 2, 4} and 
        T = {4, 1000, 2, 5}
Output : 3, 4, 1, 2
Explanation: We should first complete 
job 3, then jobs 4, 1, 2 respectively.

Input : L = {1, 2, 3, 5, 6} 
        T = {2, 4, 1, 3, 2}
Output : 3, 5, 4, 1, 2 
Explanation: We should complete jobs 
3, 5, 4, 1 and then 2 in this order.

```

让我们考虑两种极端情况，我们将从中推导出一般情况下的解。

1.  所有的工作都需要相同的时间来完成，也就是说 Ti = k 代表所有的 I。因为所有的工作都需要相同的时间来完成，所以我们应该首先选择损失较大的工作(李)。我们应该选择损失最大的工作，并尽早完成。
    由此可见这是一个贪婪算法。仅基于李按降序对作业进行排序。
2.  所有的工作都有相同的惩罚。因为所有的工作都有相同的惩罚，我们会先做那些需要较少时间完成的工作。这将最大限度地减少总延迟，从而也减少总损失。
    这也是一个贪婪算法。基于 Ti 按升序对作业进行排序。或者我们也可以按照 1/Ti 的降序排序。

    从上面的案例中，我们很容易看出，我们不应该仅仅根据李或钛来排序工作。取而代之的是，我们应该按照 Li/Ti 的比例，按照降序对作业进行排序。

    如果我们对作业执行[稳定排序](https://www.geeksforgeeks.org/stability-in-sorting-algorithms/)，就可以得到字典上最小的作业排列。稳定排序的一个例子是[合并排序](https://www.geeksforgeeks.org/merge-sort/)。

    为了得到最准确的结果，避免用 Ti 除 Li。相反，像分数一样比较这两个比率。要比较 a/b 和 c/d，请比较 ad 和 bc。

    ```
    // CPP program to minimize loss using stable sort.
    #include <iostream>
    #include <algorithm>
    #include <vector>
    using namespace std;

    #define all(c) c.begin(), c.end()

    // Each job is represented as a pair of int and pair.
    // This is done to provide implementation simplicity
    // so that we can use functions provided by algorithm
    // header
    typedef pair<int, pair<int, int> > job;

    // compare function is given so that we can specify
    // how to compare a pair of jobs
    bool cmp_pair(job a, job b)
    {
        int a_Li, a_Ti, b_Li, b_Ti;
        a_Li = a.second.first;
        a_Ti = a.second.second;
        b_Li = b.second.first;
        b_Ti = b.second.second;

        // To compare a/b and c/d, compare ad and bc
        return (a_Li * b_Ti) > (b_Li * a_Ti);
    }

    void printOptimal(int L[], int T[], int N)
    {
        vector<job> list; // (Job Index, Si, Ti)

        for (int i = 0; i < N; i++) {
            int t = T[i];
            int l = L[i];

            // Each element is: (Job Index, (Li, Ti) )
            list.push_back(make_pair(i + 1, make_pair(l, t)));
        }

        stable_sort(all(list), cmp_pair);

        // traverse the list and print job numbers
        cout << "Job numbers in optimal sequence are\n";
        for (int i = 0; i < N; i++) 
            cout << list[i].first << " ";   

    }

    // Driver code
    int main()
    {
        int L[] = { 1, 2, 3, 5, 6 };
        int T[] = { 2, 4, 1, 3, 2 };
        int N = sizeof(L) / sizeof(L[0]);
        printOptimal(L, T, N);
        return 0;
    }
    ```

    输出:

    ```
    Job numbers in optimal sequence are
    3 5 4 1 2 

    ```

    时间复杂度:O(N log N)
    空间复杂度:O(N)

    本文由 [**萨彦·马哈帕特拉**](https://auth.geeksforgeeks.org/profile.php?user=Sayan Mahapatra) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

    如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。