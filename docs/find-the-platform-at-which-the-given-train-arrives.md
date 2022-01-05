# 找到给定列车到达的站台

> 原文:[https://www . geesforgeks . org/find-给定列车到达的平台/](https://www.geeksforgeeks.org/find-the-platform-at-which-the-given-train-arrives/)

给定一个由 **N** 列车信息组成的 2D [数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】【3】**，其中**arr【I】【0】**为车次号，**arr【I】【1】**为到达时间，**arr【I】【2】**为停运时长。给定另一个代表车次的整数 **F** ，任务是按照以下规则找到车次为 **F** 的列车到达的站台号:

*   平台编号从 **1** 开始，平台数量无限。
*   较早释放的站台被分配给下一趟列车。
*   如果两个或多个站台同时空闲，则列车到达站台号最低的站台。
*   如果两辆或多辆列车同时到达，则先分配车次较少的列车。

**示例:**

> **输入:** arr[] = {{112567，1，2}，{112563，3，3}，{112569，4，7}，{112560，9，3}}，F = 112569
> T3】输出:1
> T6】说明:T8】以下为列车到站顺序:
> 列车站台发车时间
> 112567 1
> 
> 因此，112569 次列车到达 1 号站台。
> 
> **输入:** arr[] = {{112567，2，1}，{112563，5，5}，{112569，7，3}，{112560，3，7}}，F = 112569
> T3】输出: 3

**方法:**使用[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)可以解决给定的问题。按照以下步骤解决此问题:

*   [根据列车到达时间对 **N** 列车的给定数组**arr【】**T3】进行排序。](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)
*   初始化一个[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)，比如说 **PQ** 对 **{PlatformNumber，time}** ，按照最少出发时间执行[分堆](https://www.geeksforgeeks.org/binary-heap/)。在[优先级队列中插入**{平台号，时间}** ，即 **{1，0}** 。](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)
*   初始化一个 [HashMap](https://www.geeksforgeeks.org/java-util-hashmap-in-java/) ，比如说 **M** ，存储任何一列火车到达的站台号。
*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，并执行以下步骤:
    *   [弹出 **PQ**](https://www.geeksforgeeks.org/priority_queuepush-priority_queuepop-c-stl/) 的顶部平台，存放在 **free_platform[]** 。
    *   如果当前列车的到达时间至少是弹出站台的发车时间，那么将弹出站台的发车时间更新为**(到达和停运时间之和+ 1)** ，在 **PQ** 中插入站台的当前状态，在 HashMap **M** 中插入当前列车的当前站台号。
    *   否则，将新的站台条目添加到 **PQ** 中，并在 HashMap **M** 中添加当前列车的当前站台号。
*   完成上述步骤后，在散列表 **M** 中打印与车次 **F** 关联的站台号。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;

// Stores the information for each
// train as Objects
class Train {
    // Stores the train number
    String train_num;

    // Stores the arrival time
    int arrival_time;

    // Stores the stoppage time
    int stoppage_time;

    // Constructor
    Train(String train_num,
        int arrival_time,
        int stoppage_time)
    {
        this.train_num = train_num;
        this.arrival_time = arrival_time;
        this.stoppage_time = stoppage_time;
    }
}

public class GFG {
    // Function to find the platform
    // on which train F arrives
    static int findPlatformOf(
        ArrayList<Train> trains, int n,
        String F)
    {
        // Sort the array arr[] according
        // to the arrival time
        Collections.sort(
            trains,
            (a, b) -> a.arrival_time==b.arrival_time ? Integer.parseInt(a.train_num)-Integer.parseInt(b.train_num) : a.arrival_time - b.arrival_time);

        // Stores the platforms that
        // is in currently in use
        PriorityQueue<int[]> pq
            = new PriorityQueue<>(
                (a, b)
                    -> a[1] == b[1] ? a[0] - b[0]
                                    : a[1] - b[1]);

        // Insert the platform number 1
        // with departure time as 0
        pq.add(new int[] { 1, 0 });

        // Store the platform number
        // on which train arrived
        HashMap<String, Integer> schedule
            = new HashMap<>();

        // Traverse the given array
        for (Train t : trains) {

            // Pop the top platform of
            // the priority queue
            int[] free_platform = pq.poll();

            // If arrival time of the train
            // >= freeing time of the platform
            if (t.arrival_time >= free_platform[1]) {
                // Update the train status
                free_platform[1]
                    = t.arrival_time + t.stoppage_time + 1;

                // Add the current platform
                // to the pq
                pq.add(free_platform);

                // Add the platform
                // number to the HashMap
                schedule.put(t.train_num,
                            free_platform[0]);
            }

            // Otherwise, add a new platform
            // for the current train
            else {

                // Update the priority queue
                pq.add(free_platform);

                // Get the platform number
                int platform_num = pq.size() + 1;

                // Add the platform to
                // the priority queue
                pq.add(new int[] {
                    platform_num,
                    t.arrival_time
                        + t.stoppage_time + 1 });

                // Add the platform
                // number to the HashMap
                schedule.put(t.train_num,
                            platform_num);
            }
        }

        // Return the platform on
        // which F train arrived
        return schedule.get(F);
    }

    // Driver Code
    public static void main(String[] args)
    {
        ArrayList<Train> trains
            = new ArrayList<>();

        trains.add(new Train(

            "112567", 2, 1));
        trains.add(new Train(
            "112569", 5, 5));
        trains.add(new Train(
            "112563", 5, 3));
        trains.add(new Train(
            "112560", 3, 7));
        String F = "112563";

        System.out.println(
            findPlatformOf(
                trains, trains.size(), F));
    }
}
```

**Output:** 

```
3
```

***时间复杂度:** O(N * log N)*
***辅助空间:** O(N)*