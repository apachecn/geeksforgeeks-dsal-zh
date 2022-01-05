# 使用记忆的水壶问题

> 原文:[https://www . geesforgeks . org/water-jug-problem-use-memoimation/](https://www.geeksforgeeks.org/water-jug-problem-using-memoization/)

分别给定最大容量为 **m** 和 **n** 升的两个壶。壶上没有标记，可以帮助我们测量更少的量。任务是用这两个壶来测量水的体积。因此，我们的目标是从初始状态(m，n)到达最终状态(0，d)或(d，0)。

**示例:**

> **输入:**4 3 2
> T3】输出: (0，0)–>(4，0)–>(4，3)–>(0，3)–>(3，0)–>(3，3)–>(4，2)–>(0，2)
> 
> **输入:**5 2 4
> T3】输出: (0，0)–>(5，0)–>(5，2)–>(0，2)–>(2，0)–>(2，2)–>(4，0)

**进场:**使用 [BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 的进场已经在之前的[帖子](https://www.geeksforgeeks.org/water-jug-problem-using-bfs/)中讨论过。在这篇文章中，已经讨论了使用[记忆](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)和[递归](https://www.geeksforgeeks.org/recursion/)的方法。在任何时候，总共有六种可能性:

*   把第一罐完全倒空
*   将第二个罐子完全倒空
*   装满第一个罐子
*   装满第二个罐子
*   将第二壶中的水注入第一壶，直到第一壶满了或者第二壶没有水了
*   将第一个壶中的水注入第二个壶中，直到第二个壶满了或者第一个壶没有水了

**接近**:使用[递归](https://www.geeksforgeeks.org/recursion/)，逐个访问所有六个可能的招式，直到其中一个返回 True。由于可以重复相同的递归调用，因此使用[记忆](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)存储每个返回值，以避免再次调用递归函数并返回存储的值。

下面是上述方法的实现:

```
# This function is used to initialize the 
# dictionary elements with a default value.
from collections import defaultdict

# jug1 and jug2 contain the value 
# for max capacity in respective jugs 
# and aim is the amount of water to be measured. 
jug1, jug2, aim = 4, 3, 2

# Initialize dictionary with 
# default value as false.
visited = defaultdict(lambda: False)

# Recursive function which prints the 
# intermediate steps to reach the final 
# solution and return boolean value 
# (True if solution is possible, otherwise False).
# amt1 and amt2 are the amount of water present 
# in both jugs at a certain point of time.
def waterJugSolver(amt1, amt2): 

    # Checks for our goal and 
    # returns true if achieved.
    if (amt1 == aim and amt2 == 0) or (amt2 == aim and amt1 == 0):
        print(amt1, amt2)
        return True

    # Checks if we have already visited the
    # combination or not. If not, then it proceeds further.
    if visited[(amt1, amt2)] == False:
        print(amt1, amt2)

        # Changes the boolean value of
        # the combination as it is visited. 
        visited[(amt1, amt2)] = True

        # Check for all the 6 possibilities and 
        # see if a solution is found in any one of them.
        return (waterJugSolver(0, amt2) or
                waterJugSolver(amt1, 0) or
                waterJugSolver(jug1, amt2) or
                waterJugSolver(amt1, jug2) or
                waterJugSolver(amt1 + min(amt2, (jug1-amt1)),
                amt2 - min(amt2, (jug1-amt1))) or
                waterJugSolver(amt1 - min(amt1, (jug2-amt2)),
                amt2 + min(amt1, (jug2-amt2))))

    # Return False if the combination is 
    # already visited to avoid repetition otherwise
    # recursion will enter an infinite loop.
    else:
        return False

print("Steps: ")

# Call the function and pass the
# initial amount of water present in both jugs.
waterJugSolver(0, 0)
```

**Output:**

```
Steps: 
0 0
4 0
4 3
0 3
3 0
3 3
4 2
0 2

```

**时间复杂度**:O(M * N)
T3】辅助空间 : O(M * N)