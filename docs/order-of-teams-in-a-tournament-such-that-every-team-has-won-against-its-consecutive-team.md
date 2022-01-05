# 锦标赛中各队的顺序，每个队都战胜了其连续的队

> 原文:[https://www . geeksforgeeks . org/锦标赛中的团队顺序，这样每个团队都可以战胜其连续团队/](https://www.geeksforgeeks.org/order-of-teams-in-a-tournament-such-that-every-team-has-won-against-its-consecutive-team/)

给定 **N** 支队伍和[循环赛](https://www.geeksforgeeks.org/program-round-robin-scheduling-set-1/)的结果，其中没有比赛结果是平局或平局。任务是找到球队的顺序，这样每支球队都可以战胜连续的球队。

**示例:**

> **输入:** N = 4
> 结果[] = {{1，4}、{4，3}、{2，3}、{1，2}、{2，1}、{3，1}、{2，4 } }
> T4】输出:2 4 3 1
> T7】说明:T9】2 队在最后一场比赛中战胜了 4 队。
> 3 队在 **2 <sup>第二场</sup>** 比赛中输给了 4 队，
> 3 队在倒数第二场比赛中战胜了 1 队。
> 所以，每支队伍都有赢过旁边队伍的。
> 
> **输入:** N = 5
> 结果[] = {{1，4}，{4，3}，{2，3}，{1，2}，{2，1}，
> {3，1}，{4，2}，{2，5}，{5，3}，{4，5}，{5，1}}
> **输出:** 4 2 5 3 1

**方法:**想法是为每个队维护一个散列图，其中存储了该队在循环锦标赛中获胜的队。这可以通过对结果的元素进行迭代来完成，对于每个获胜者，将它附加到该团队的哈希映射对象列表中。

```
The hashtable for an example is as follows:

Key          Value

Team-1 => [Team-4, Team-2]
Team-2 => [Team-3, Team-1, Team-4]
Team-3 => [Team-1]
Team-4 => [Team-3]

```

最后，递归地计算团队的顺序。下面是递归函数的图示:

*   **基本情况:**当队伍当前长度为 1 时，返回队伍。
*   **递归案例:**计算 N-1 个团队的顺序，在计算团队后，迭代团队的顺序，找到当前团队相对于其前一个团队失败的位置。如果没有这样的位置，将团队追加到最后一个位置。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// order of the teams in a round
// robin tournament such that every
// team has won against to its next team

import java.util.*;
import java.lang.*;

// A class to represent result
// of a match of a tournament.
class Result {
    int winner;
    int loser;

    Result(int winner, int loser)
    {
        this.winner = winner;
        this.loser = loser;
    }
}

public class TeamOrdering {

    // Function to arrange the teams of
    // the round-robin tournament
    static void arrangeTeams(int[] teams,
                             Result[] results)
    {
        HashMap<Integer,
                List<Integer> >
            map = new HashMap<>();
        int winner = 0;

        // Creating a hashmap of teams
        // and the opponents against
        // which they have won, using
        // the results of the tournament
        for (int i = 0; i < results.length; i++) {
            winner = results[i].winner;
            if (map.containsKey(winner)) {
                map.get(winner).add(
                    results[i].loser);
            }
            else {
                List<Integer> list
                    = new ArrayList<Integer>();
                list.add(results[i].loser);
                map.put(winner, list);
            }
        }
        List<Integer> output = new ArrayList<>();

        // Arrange the teams in required order
        setInOrder(teams, map, teams.length, output);
        Iterator<Integer> it = output.iterator();

        // Displaying the final output
        while (it.hasNext()) {
            System.out.print(it.next());
            System.out.print(" ");
        }
    }

    // Function to determine
    // the order of teams
    static void setInOrder(
        int[] teams,
        HashMap<Integer, List<Integer> > map,
        int n, List<Integer> output)
    {
        // Base Cases
        if (n < 1) {
            return;
        }
        // If there is only 1 team,
        // add it to the output
        else if (n == 1) {
            output.add(teams[n - 1]);
            return;
        }

        // Recursive call to generate
        // output for N-1 teams
        setInOrder(teams, map, n - 1, output);
        int key = teams[n - 1];
        int i;

        // Finding the position for the
        // current team in the output list.
        for (i = 0; i < output.size(); i++) {

            // Obtain the team at current
            // index in the list
            int team = output.get(i);

            // Check if it has lost against
            // current team
            List<Integer> losers = map.get(key);
            if (losers.indexOf(team) != -1)
                break;
        }
        // Add the current team
        // to its final position
        output.add(i, key);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] teams = { 1, 2, 3, 4 };
        Result[] results = {
            new Result(1, 4),
            new Result(4, 3),
            new Result(2, 3),
            new Result(1, 2),
            new Result(2, 1),
            new Result(3, 1),
            new Result(2, 4)
        };

        // Function Call
        arrangeTeams(teams, results);
    }
}
```

**Output:**

```
2 4 3 1

```

**性能分析:**

*   **时间复杂度:** O(N <sup>2</sup> )
*   **辅助空间:** O(N)