# 使用 BFS 的水壶问题

> 原文:[https://www.geeksforgeeks.org/water-jug-problem-using-bfs/](https://www.geeksforgeeks.org/water-jug-problem-using-bfs/)

给你一个 m 升的罐子和一个 n 升的罐子。两个壶最初都是空的。壶没有标记，无法测量较小的量。你必须用壶来测量 d 升水，其中 d 小于 n。

(X，Y)对应于这样一种状态，其中 X 指的是 Jug1 中的水量，Y 指的是 Jug2 中的水量
确定从初始状态(xi，yi)到最终状态(xf，yf)的路径，其中(xi，yi)是(0，0)，表示两个 Jug 最初都是空的，而(xf，yf)表示可能是(0，d)或(d，0)的状态。

您可以执行的操作有:

1.  清空壶，(X，Y)->(0，Y)清空壶 1
2.  装满一个罐子，(0，0)->(X，0)装满罐子 1
3.  将水从一个壶倒入另一个壶，直到其中一个壶是空的或满的，(X，Y) -> (X-d，Y+d)

**示例:**

```
Input : 4 3 2
Output : {(0, 0), (0, 3), (3, 0), (3, 3), (4, 2), (0, 2)}
```

我们已经在[两个水罐难题](https://www.geeksforgeeks.org/two-water-jug-puzzle/)
中讨论了一个解决方案，在这篇文章中讨论了一个基于 [BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 的解决方案。

我们在状态上运行广度优先搜索，这些状态将在应用允许的操作后创建，我们还使用访问过的成对地图来跟踪在搜索中应该只访问一次的状态。这个解决方案也可以使用深度优先搜索来实现。

## C++

```
#include <bits/stdc++.h>
using namespace std;
typedef pair<int,int> pii;
void printpath(map<pii,pii>mp ,pii u)
{
  if(u.first==0 &&u.second==0)
    {
      cout<<0<<" "<<0<<endl;
      return ;
    }
  printpath(mp,mp[u]);
    cout<<u.first<<" "<<u.second<<endl;
}
void BFS(int a ,int b, int target)
{
  map<pii, int>m;
  bool isSolvable =false;
  vector<tuple<int ,int ,int>>path;
  map<pii, pii>mp;

  queue<pii>q;

  q.push(make_pair(0,0));
  while(!q.empty())
  {

        auto u =q.front();
      // cout<<u.first<<" "<<u.second<<endl;
      q.pop();
      if(m[u]==1)
        continue;

      if ((u.first > a || u.second > b || u.first < 0 || u.second < 0))
        continue;
      // cout<<u.first<<" "<<u.second<<endl;

      m[{u.first,u.second}]=1;

      if(u.first == target || u.second==target)
      {
        isSolvable = true;

          printpath(mp,u);
            if (u.first == target) {
              if (u.second != 0)
                  cout<<u.first<<" "<<0<<endl;
          }
          else {
              if (u.first != 0)
                  cout<<0<<" "<<u.second<<endl;
          }
              return;
      }
      // completely fill the jug 2
      if(m[{u.first,b}]!=1)
      {q.push({u.first,b});
      mp[{u.first,b}]=u;}

      // completely fill the jug 1
      if(m[{a,u.second}]!=1)
     { q.push({a,u.second});
      mp[{a,u.second}]=u;}

    //transfer jug 1 -> jug 2
      int d = b - u.second;
      if(u.first >= d)
      {
        int c = u.first - d;
        if(m[{c,b}]!=1)
          {q.push({c,b});
          mp[{c,b}]=u;}
      }
      else
      {
        int c = u.first + u.second;
        if(m[{0,c}]!=1)
          {q.push({0,c});
          mp[{0,c}]=u;}
      }
      //transfer jug 2 -> jug 1
      d = a - u.first;
      if(u.second >= d)
      {
        int c = u.second - d;
        if(m[{a,c}]!=1)
          {q.push({a,c});
          mp[{a,c}]=u;}
      }
      else
      {
        int c = u.first + u.second;
        if(m[{c,0}]!=1)
          {q.push({c,0});
          mp[{c,0}]=u;}
      }

      // empty the jug 2
      if(m[{u.first,0}]!=1)
        { q.push({u.first,0});
          mp[{u.first,0}]=u;}

      // empty the jug 1
      if(m[{0,u.second}]!=1)
        {q.push({0,u.second});
        mp[{0,u.second}]=u;}

  }
  if (!isSolvable)
        cout << "No solution";
}

int main()
{
    int Jug1 = 5, Jug2 = 7, target = 3;
    cout << "Path from initial state "
            "to solution state ::\n";
    BFS(Jug1, Jug2, target);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;

public class GFG{

    class Pair{
        int first, second;

        Pair(int f, int s){
            first = f;
            second = s;
        }
    }

    void BFS(int a, int b, int target)
    {
        // This 2d array is used as a hashmap
        // to keep track of already visited
        // values and avoid repetition
        int m[][] = new int[1000][1000];
        for(int[] i : m){
            Arrays.fill(i, -1);
        }

        boolean isSolvable = false;
        Vector<Pair> path = new Vector<Pair>();

        Queue<Pair> q = new LinkedList<Pair>(); // queue to maintain states
        q.add(new Pair( 0, 0 )); // Initialing with initial state

        while (!q.isEmpty()) {

            Pair u = q.peek(); // current state

            q.poll(); // pop off used state

            // doesn't met jug constraints
            if ((u.first > a || u.second > b ||
                u.first < 0 || u.second < 0))
                continue;

            // if this state is already visited
            if (m[u.first][u.second] > -1)
                continue;

            // filling the vector for constructing
            // the solution path
            path.add(new Pair( u.first, u.second ));

            // marking current state as visited

            m[u.first][u.second] = 1;

            // System.out.println(m.get(new Pair(u.first, u.second)));

            // if we reach solution state, put ans=1
            if (u.first == target || u.second == target) {
                isSolvable = true;
                if (u.first == target) {
                    if (u.second != 0)

                        // fill final state
                        path.add(new Pair(u.first, 0 ));
                }
                else {
                    if (u.first != 0)

                        // fill final state
                        path.add(new Pair( 0, u.second ));
                }

                // print the solution path
                int sz = path.size();
                for (int i = 0; i < sz; i++)
                    System.out.println("(" + path.get(i).first
                        + ", " + path.get(i).second + ")");
                break;
            }

            // if we have not reached final state
            // then, start developing intermediate
            // states to reach solution state
            q.add(new Pair( u.first, b )); // fill Jug2
            q.add(new Pair( a, u.second )); // fill Jug1

            for (int ap = 0; ap <= Math.max(a, b); ap++) {

                // pour amount ap from Jug2 to Jug1
                int c = u.first + ap;
                int d = u.second - ap;

                // check if this state is possible or not
                if (c == a || (d == 0 && d >= 0))
                    q.add(new Pair( c, d ));

                // Pour amount ap from Jug 1 to Jug2
                c = u.first - ap;
                d = u.second + ap;

                // check if this state is possible or not
                if ((c == 0 && c >= 0) || d == b)
                    q.add(new Pair( c, d ));
            }

            q.add(new Pair( a, 0 )); // Empty Jug2
            q.add(new Pair( 0, b )); // Empty Jug1
        }

        // No, solution exists if ans=0
        if (!isSolvable)
            System.out.print("No solution");
    }

    // Driver code
    public static void main(String args[])
    {
        int Jug1 = 4, Jug2 = 3, target = 2;

        System.out.println("Path from initial state " +
                "to solution state ::");

        GFG object = new GFG();

        object.BFS(Jug1, Jug2, target);

    }
}

// This code is contributed by aditypande88.
```

## 蟒蛇 3

```
from collections import deque

def BFS(a, b, target):

    # Map is used to store the states, every
    # state is hashed to binary value to
    # indicate either that state is visited
    # before or not
    m = {}
    isSolvable = False
    path = []

    # Queue to maintain states
    q = deque()

    # Initialing with initial state
    q.append((0, 0))

    while (len(q) > 0):

        # Current state
        u = q.popleft()

        #q.pop() #pop off used state

        # If this state is already visited
        if ((u[0], u[1]) in m):
            continue

        # Doesn't met jug constraints
        if ((u[0] > a or u[1] > b or
             u[0] < 0 or u[1] < 0)):
            continue

        # Filling the vector for constructing
        # the solution path
        path.append([u[0], u[1]])

        # Marking current state as visited
        m[(u[0], u[1])] = 1

        # If we reach solution state, put ans=1
        if (u[0] == target or u[1] == target):
            isSolvable = True

            if (u[0] == target):
                if (u[1] != 0):

                    # Fill final state
                    path.append([u[0], 0])
            else:
                if (u[0] != 0):

                    # Fill final state
                    path.append([0, u[1]])

            # Print the solution path
            sz = len(path)
            for i in range(sz):
                print("(", path[i][0], ",",
                           path[i][1], ")")
            break

        # If we have not reached final state
        # then, start developing intermediate
        # states to reach solution state
        q.append([u[0], b]) # Fill Jug2
        q.append([a, u[1]]) # Fill Jug1

        for ap in range(max(a, b) + 1):

            # Pour amount ap from Jug2 to Jug1
            c = u[0] + ap
            d = u[1] - ap

            # Check if this state is possible or not
            if (c == a or (d == 0 and d >= 0)):
                q.append([c, d])

            # Pour amount ap from Jug 1 to Jug2
            c = u[0] - ap
            d = u[1] + ap

            # Check if this state is possible or not
            if ((c == 0 and c >= 0) or d == b):
                q.append([c, d])

        # Empty Jug2
        q.append([a, 0])

        # Empty Jug1
        q.append([0, b])

    # No, solution exists if ans=0
    if (not isSolvable):
        print ("No solution")

# Driver code
if __name__ == '__main__':

    Jug1, Jug2, target = 4, 3, 2
    print("Path from initial state "
          "to solution state ::")

    BFS(Jug1, Jug2, target)

# This code is contributed by mohit kumar 29
```

## C#

```
using System;
using System.Collections.Generic;

class GFG{

static void BFS(int a, int b, int target)
{

    // Map is used to store the states, every
    // state is hashed to binary value to
    // indicate either that state is visited
    // before or not
    Dictionary<Tuple<int,
                     int>, int> m = new Dictionary<Tuple<int,
                                                         int> ,int>(); 
    bool isSolvable = false;
    List<Tuple<int,
               int>> path = new List<Tuple<int,
                                           int>>();
    // Queue to maintain states
    List<Tuple<int,
               int>> q = new List<Tuple<int,
                                        int>>();

    // Initializing with initial state
    q.Add(new Tuple<int,int>(0, 0));

    while (q.Count > 0)
    {

        // Current state
        Tuple<int, int> u = q[0];

        // Pop off used state
        q.RemoveAt(0);

        // If this state is already visited
        if (m.ContainsKey(u) && m[u] == 1)
            continue;

        // Doesn't met jug constraints
        if ((u.Item1 > a || u.Item2 > b ||
            u.Item1 < 0 || u.Item2 < 0))
            continue;

        // Filling the vector for constructing
        // the solution path
        path.Add(u);

        // Marking current state as visited
        m[u] = 1;

        // If we reach solution state, put ans=1
        if (u.Item1 == target || u.Item2 == target)
        {
            isSolvable = true;

            if (u.Item1 == target)
            {
                if (u.Item2 != 0)

                    // Fill final state
                    path.Add(new Tuple<int, int>(u.Item1, 0));
            }
            else
            {
                if (u.Item1 != 0)

                    // Fill final state
                    path.Add(new Tuple<int, int>(0, u.Item2));
            }

            // Print the solution path
            int sz = path.Count;
            for(int i = 0; i < sz; i++)
                Console.WriteLine("(" + path[i].Item1 +
                                 ", " + path[i].Item2 + ")");
            break;
        }

        // If we have not reached final state
        // then, start developing intermediate
        // states to reach solution state
        // Fill Jug2
        q.Add(new Tuple<int, int>(u.Item1, b));

        // Fill Jug1
        q.Add(new Tuple<int, int>(a, u.Item2));

        for(int ap = 0; ap <= Math.Max(a, b); ap++)
        {

            // Pour amount ap from Jug2 to Jug1
            int c = u.Item1 + ap;
            int d = u.Item2 - ap;

            // Check if this state is possible or not
            if (c == a || (d == 0 && d >= 0))
                q.Add(new Tuple<int, int>(c, d));

            // Pour amount ap from Jug 1 to Jug2
            c = u.Item1 - ap;
            d = u.Item2 + ap;

            // Check if this state is possible or not
            if ((c == 0 && c >= 0) || d == b)
                q.Add(new Tuple<int, int>(c, d));
        }

        // Empty Jug2
        q.Add(new Tuple<int, int>(a, 0));

        // Empty Jug1
        q.Add(new Tuple<int, int>(0, b));
    }

    // No, solution exists if ans=0
    if (!isSolvable)
        Console.WriteLine("No solution");
}

// Driver code
static void Main()
{
    int Jug1 = 4, Jug2 = 3, target = 2;
    Console.WriteLine("Path from initial state " +
                      "to solution state ::");

    BFS(Jug1, Jug2, target);
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

    function BFS(a,b,target)
    {
        // This 2d array is used as a hashmap
        // to keep track of already visited
        // values and avoid repetition
        let m = new Array(1000);
        for(let i=0;i<1000;i++){
            m[i]=new Array(1000);
            for(let j=0;j<1000;j++)
            {
                m[i][j]=-1;
            }
        }

        let isSolvable = false;
        let path = [];

        let q = []; // queue to maintain states
        q.push([0,0]); // Initialing with initial state

        while (q.length!=0) {

            let u = q[0]; // current state

            q.shift(); // pop off used state

            // doesn't met jug constraints
            if ((u[0] > a || u[1] > b ||
                u[0] < 0 || u[1] < 0))
                continue;

            // if this state is already visited
            if (m[u[0]][u[1]] > -1)
                continue;

            // filling the vector for constructing
            // the solution path
            path.push([u[0],u[1]]);

            // marking current state as visited

            m[u[0]][u[1]] = 1;

            // System.out.println(m.get(new Pair(u.first, u.second)));

            // if we reach solution state, put ans=1
            if (u[0] == target || u[1] == target) {
                isSolvable = true;
                if (u[0] == target) {
                    if (u[1] != 0)

                        // fill final state
                        path.push([u[0],0]);
                }
                else {
                    if (u[0] != 0)

                        // fill final state
                        path.push([0,u[1]]);
                }

                // print the solution path
                let sz = path.length;
                for (let i = 0; i < sz; i++)
                    document.write("(" + path[i][0]
                        + ", " + path[i][1] + ")<br>");
                break;
            }

            // if we have not reached final state
            // then, start developing intermediate
            // states to reach solution state
            q.push([u[0],b]); // fill Jug2
            q.push([a,u[1]]); // fill Jug1

            for (let ap = 0; ap <= Math.max(a, b); ap++) {

                // pour amount ap from Jug2 to Jug1
                let c = u[0] + ap;
                let d = u[1] - ap;

                // check if this state is possible or not
                if (c == a || (d == 0 && d >= 0))
                    q.push([c,d]);

                // Pour amount ap from Jug 1 to Jug2
                c = u[0] - ap;
                d = u[1] + ap;

                // check if this state is possible or not
                if ((c == 0 && c >= 0) || d == b)
                    q.push([c,d]);
            }

            q.push([a,0]); // Empty Jug2
            q.push([0,b]); // Empty Jug1
        }

        // No, solution exists if ans=0
        if (!isSolvable)
            document.write("No solution");
    }

    // Driver code
    let Jug1 = 4, Jug2 = 3, target = 2;
    document.write("Path from initial state " +
                "to solution state ::<br>");
    BFS(Jug1, Jug2, target);

// This code is contributed by unknown2108
</script>
```

**Output**

```
Path from initial state to solution state ::
0 0
5 0
0 5
5 5
3 7
3 0
```