# 模拟退火

> 原文:[https://www.geeksforgeeks.org/simulated-annealing/](https://www.geeksforgeeks.org/simulated-annealing/)

**问题:**给定一个成本函数*f:r^n–>r*，找到一个 *n* 元组，该元组最小化 *f* 的值。请注意，最小化函数值在算法上等同于最大化(因为我们可以将成本函数重新定义为 1-f)。
很多有微积分/分析背景的人可能都熟悉单变量函数的简单优化。例如，函数 *f(x) = x^2 + 2x* 可以通过将一阶导数设置为零来优化，从而获得产生最小值 *f(-1) = -1* 的解 *x = -1* 。这种技术适用于变量很少的简单函数。然而，通常情况下，研究人员对优化几个变量的函数感兴趣，在这种情况下，只能通过计算获得解。

一个困难的优化任务的极好例子是芯片平面规划问题。假设你在英特尔工作，你的任务是设计集成电路的布局。您有一组不同形状/大小的模块，以及可以放置模块的固定区域。你想要达到的目标有很多:最大化导线连接元件的能力，最小化净面积，最小化芯片成本，等等。考虑到这些，您创建了一个成本函数，取所有，比如说， *1000* 个变量配置，并返回一个代表输入配置“成本”的实数值。我们称之为目标函数，因为目标是最小化它的值。
一个简单的算法是完全的空间搜索——我们搜索所有可能的配置，直到找到最小值。这对于变量很少的函数来说可能就足够了，但是我们想到的问题需要这样一个强力算法来玩 *O(n！)*。

由于这类问题和其他 NP 难问题的计算困难，许多优化试探法已经被开发出来，试图产生一个好的，尽管可能是次优的值。在我们的例子中，我们不一定需要找到一个严格的最优值——找到一个接近最优的值将满足我们的目标。一种广泛使用的技术是模拟退火，通过它我们引入了一定程度的随机性，有可能从一个更好的解转移到一个更差的解，试图逃离局部极小值并收敛到一个更接近全局最优的值。

模拟退火是基于冶金实践，通过这种实践，材料被加热到高温并冷却。在高温下，原子可能会不可预测地移动，通常会随着材料冷却成纯晶体而消除杂质。这是通过模拟退火优化算法复制的，能量状态对应于当前解。
在这个算法中，我们定义了一个初始温度和一个最低温度，初始温度通常设置为 1，最低温度的数量级为 10^-4.当前温度乘以某个分数α，然后降低，直到达到最低温度。对于每个不同的温度值，我们运行核心优化例程的次数是固定的。优化程序包括找到一个相邻解并以概率*e^(f(c–f(n)】*接受它，其中 *c* 是当前解而 *n* 是相邻解。通过对当前解施加微小的扰动来找到相邻解。这种随机性有助于避开优化启发式算法的常见陷阱——陷入局部极小值。通过潜在地接受一个比我们目前拥有的更差的最优解，并以与成本增加相反的概率接受它，算法更有可能收敛到全局最优。设计一个邻居函数是相当棘手的，必须在个案的基础上完成，但以下是在位置优化问题中寻找邻居的一些想法。

*   在随机方向上将所有点移动 0 或 1 个单位
*   随机移动输入元素
*   交换输入序列中的随机元素
*   置换输入序列
*   将输入序列分成随机数量的段和置换段

一个警告是，我们需要提供一个初始解决方案，以便算法知道从哪里开始。这可以通过两种方式来实现:(1)使用关于问题的先验知识来输入良好的起点，以及(2)生成随机解。尽管生成随机解更糟糕，有时会抑制算法的成功，但对于我们对环境一无所知的问题，这是唯一的选择。

还有许多其他优化技术，尽管模拟退火是一种有用的随机优化启发式方法，适用于大型离散搜索空间，在这些空间中，随着时间的推移，最优性是优先的。下面，我包含了一个基于位置的模拟退火的基本框架(可能是模拟退火最适用的优化风格)。当然，成本函数、候选生成函数和邻居函数必须根据手头的具体问题来定义，尽管核心优化例程已经实现。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement Simulated Annealing
import java.util.*;

public class SimulatedAnnealing {

    // Initial and final temperature
    public static double T = 1;

    // Simulated Annealing parameters

    // Temperature at which iteration terminates
    static final double Tmin = .0001;

    // Decrease in temperature
    static final double alpha = 0.9;

    // Number of iterations of annealing
    // before decreasing temperature
    static final int numIterations = 100;

    // Locational parameters

    // Target array is discretized as M*N grid
    static final int M = 5, N = 5;

    // Number of objects desired
    static final int k = 5;

    public static void main(String[] args) {

        // Problem: place k objects in an MxN target
        // plane yielding minimal cost according to
        // defined objective function

        // Set of all possible candidate locations
        String[][] sourceArray = new String[M][N];

        // Global minimum
        Solution min = new Solution(Double.MAX_VALUE, null);

        // Generates random initial candidate solution
        // before annealing process
        Solution currentSol = genRandSol();

        // Continues annealing until reaching minimum
        // temperature
        while (T > Tmin) {
            for (int i=0;i<numIterations;i++){

                // Reassigns global minimum accordingly
                if (currentSol.CVRMSE < min.CVRMSE){
                    min = currentSol;
                }

                Solution newSol = neighbor(currentSol);
                double ap = Math.pow(Math.E,
                     (currentSol.CVRMSE - newSol.CVRMSE)/T);
                if (ap > Math.random())
                    currentSol = newSol;
            }

            T *= alpha; // Decreases T, cooling phase
        }

        //Returns minimum value based on optimization
        System.out.println(min.CVRMSE+"\n\n");

        for(String[] row:sourceArray) Arrays.fill(row, "X");

        // Displays
        for (int object:min.config) {
            int[] coord = indexToPoints(object);
            sourceArray[coord[0]][coord[1]] = "-";
        }

        // Displays optimal location
        for (String[] row:sourceArray)
            System.out.println(Arrays.toString(row));

    }

    // Given current configuration, returns "neighboring"
    // configuration (i.e. very similar)
    // integer of k points each in range [0, n)
    /* Different neighbor selection strategies:
        * Move all points 0 or 1 units in a random direction
        * Shift input elements randomly
        * Swap random elements in input sequence
        * Permute input sequence
        * Partition input sequence into a random number
          of segments and permute segments   */
    public static Solution neighbor(Solution currentSol){

        // Slight perturbation to the current solution
        // to avoid getting stuck in local minimas

        // Returning for the sake of compilation
        return currentSol;

    }

    // Generates random solution via modified Fisher-Yates
    // shuffle for first k elements
    // Pseudorandomly selects k integers from the interval
    // [0, n-1]
    public static Solution genRandSol(){

        // Instantiating for the sake of compilation
        int[] a = {1, 2, 3, 4, 5};

        // Returning for the sake of compilation
        return new Solution(-1, a);
    }

    // Complexity is O(M*N*k), asymptotically tight
    public static double cost(int[] inputConfiguration){

        // Given specific configuration, return object
        // solution with assigned cost
        return -1; //Returning for the sake of compilation
    }

    // Mapping from [0, M*N] --> [0,M]x[0,N]
    public static int[] indexToPoints(int index){
        int[] points = {index%M, index/M};
        return points;
    }

    // Class solution, bundling configuration with error
    static class Solution {

        // function value of instance of solution;
        // using coefficient of variance root mean
        // squared error
        public double CVRMSE;

        public int[] config; // Configuration array
        public Solution(double CVRMSE, int[] configuration) {
            this.CVRMSE = CVRMSE;
            config = configuration;
        }
    }
}
```

输出:

```
-1.0

[X, -, X, X, X]
[-, X, X, X, X]
[-, X, X, X, X]
[-, X, X, X, X]
[-, X, X, X, X]
```

本文由**乔尔·亚伯拉罕**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。