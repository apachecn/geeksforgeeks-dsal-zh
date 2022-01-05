# 在给定约束条件下交替移动称重秤

> 原文:[https://www . geesforgeks . org/move-weighting-scale-alternate-given-constraints/](https://www.geeksforgeeks.org/move-weighting-scale-alternate-given-constraints/)

给定一个权重和一组不同的正权重，每个权重有无限的供给。我们的任务是将砝码一个接一个地放在秤盘的左侧和右侧，这样秤盘就会移动到放置砝码的一侧，也就是说，每次秤盘都会移动到交替的一侧。

*   我们得到了另一个整数“步长”，执行这个操作所需的时间。
*   Another constraint is that we can’t put same weight consecutively i.e. if weight w is taken then in next step while putting the weight on opposite pan we can’t take w again.

    **示例:**

    ```
    Let weight array is [7, 11]  and steps = 3 
    then 7, 11, 7 is the sequence in which 
    weights should be kept in order to move
    scale alternatively.

    Let another weight array is [2, 3, 5, 6] 
    and steps = 10 then, 3, 2, 3, 5, 6, 5, 3, 
    2, 3 is the sequence in which weights should
    be kept in order to move scale alternatively.

    ```

    这个问题可以通过在刻度状态之间做 [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 来解决。

    1.  我们遍历该解决方案的各种离散傅立叶变换状态，其中每个离散傅立叶变换状态对应于左右平移和当前步数之间的实际差值。
    2.  不是存储两个锅的重量，我们只是存储差值的剩余值，每次选择的重量值应该大于这个差值，不应该等于之前选择的重量值。
    3.  如果是，那么我们用新的差值和多一步递归调用 DFS 方法。

    为了更好的理解，请参见下面的代码，

    ## C++

    ```
    // C++ program to print weights for alternating
    // the weighting scale
    #include <bits/stdc++.h>
    using namespace std;

    // DFS method to traverse among states of weighting scales
    bool dfs(int residue, int curStep, int wt[], int arr[],
             int N, int steps)
    {
        // If we reach to more than required steps,
        // return true
        if (curStep > steps)
            return true;

        // Try all possible weights and choose one which
        // returns 1 afterwards
        for (int i = 0; i < N; i++)
        {
            /* Try this weight only if it is greater than
               current residueand not same as previous chosen
               weight */
            if (arr[i] > residue && arr[i] != wt[curStep - 1])
            {
                // assign this weight to array and recur for
                // next state
                wt[curStep] = arr[i];
                if (dfs(arr[i] - residue, curStep + 1, wt,
                        arr, N, steps))
                    return true;
            }
        }

        //    if any weight is not possible, return false
        return false;
    }

    // method prints weights for alternating scale and if
    // not possible prints 'not possible'
    void printWeightsOnScale(int arr[], int N, int steps)
    {
        int wt[steps];

        // call dfs with current residue as 0 and current
        // steps as 0
        if (dfs(0, 0, wt, arr, N, steps))
        {
            for (int i = 0; i < steps; i++)
                cout << wt[i] << " ";
            cout << endl;
        }
        else
            cout << "Not possible\n";
    }

    //    Driver code to test above methods
    int main()
    {
        int arr[] = {2, 3, 5, 6};
        int N = sizeof(arr) / sizeof(int);

        int steps = 10;
        printWeightsOnScale(arr, N, steps);
        return 0;
    }
    ```

    ## Java 语言(一种计算机语言，尤用于创建网站)

    ```
    // Java program to print weights for alternating 
    // the weighting scale
    class GFG 
    {

        // DFS method to traverse among 
        // states of weighting scales
        static boolean dfs(int residue, int curStep, 
                           int[] wt, int[] arr,
                           int N, int steps) 
        {

            // If we reach to more than required steps,
            // return true
            if (curStep >= steps)
                return true;

            // Try all possible weights and 
            // choose one which returns 1 afterwards
            for (int i = 0; i < N; i++) 
            {

                /*
                * Try this weight only if it is 
                * greater than current residue 
                * and not same as previous chosen weight
                */
                if (curStep - 1 < 0 || 
                   (arr[i] > residue &&
                    arr[i] != wt[curStep - 1]))
                {

                    // assign this weight to array and 
                    // recur for next state
                    wt[curStep] = arr[i];
                    if (dfs(arr[i] - residue, curStep + 1,
                                       wt, arr, N, steps))
                        return true;
                }
            }

            // if any weight is not possible,
            // return false
            return false;
        }

        // method prints weights for alternating scale 
        // and if not possible prints 'not possible'
        static void printWeightOnScale(int[] arr, 
                                       int N, int steps) 
        {
            int[] wt = new int[steps];

            // call dfs with current residue as 0 
            // and current steps as 0
            if (dfs(0, 0, wt, arr, N, steps)) 
            {
                for (int i = 0; i < steps; i++)
                    System.out.print(wt[i] + " ");
                System.out.println();
            } 
            else
                System.out.println("Not Possible");
        }

        // Driver Code
        public static void main(String[] args)
        {
            int[] arr = { 2, 3, 5, 6 };
            int N = arr.length;
            int steps = 10;
            printWeightOnScale(arr, N, steps);
        }
    }

    // This code is contributed by
    // sanjeev2552
    ```

    ## 蟒蛇 3

    ```
    # Python3 program to print weights for  
    # alternating the weighting scale 

    # DFS method to traverse among states 
    # of weighting scales 
    def dfs(residue, curStep, wt, arr, N, steps):

        # If we reach to more than required 
        # steps, return true 
        if (curStep >= steps): 
            return True

        # Try all possible weights and choose 
        # one which returns 1 afterwards
        for i in range(N):

            # Try this weight only if it is greater 
            # than current residueand not same as 
            # previous chosen weight 
            if (arr[i] > residue and 
                arr[i] != wt[curStep - 1]):

                # assign this weight to array and 
                # recur for next state 
                wt[curStep] = arr[i] 
                if (dfs(arr[i] - residue, curStep + 1,
                                  wt, arr, N, steps)): 
                    return True

        # if any weight is not possible,
        # return false 
        return False

    # method prints weights for alternating scale 
    # and if not possible prints 'not possible' 
    def printWeightsOnScale(arr, N, steps):
        wt = [0] * (steps) 

        # call dfs with current residue as 0 
        # and current steps as 0 
        if (dfs(0, 0, wt, arr, N, steps)):
            for i in range(steps):
                print(wt[i], end = " ")
        else:
            print("Not possible")

    # Driver Code
    if __name__ == '__main__':

        arr = [2, 3, 5, 6] 
        N = len(arr)

        steps = 10
        printWeightsOnScale(arr, N, steps)

    # This code is contributed by PranchalK
    ```

    **Output:**

    ```
    2 3 2 3 5 6 5 3 2 3

    ```

    本文由 **[乌卡什·特里维迪](https://in.linkedin.com/in/utkarsh-trivedi-253069a7)** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

    如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。