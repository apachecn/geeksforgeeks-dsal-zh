# 在给定的 N 个范围内找到从 1 到 M 的缺失元素

> 原文:[https://www . geesforgeks . org/find-the-missing-elements-从-1 到-m-in-给定-n-ranges/](https://www.geeksforgeeks.org/find-the-missing-elements-from-1-to-m-in-given-n-ranges/)

给定作为范围[L，R]的 *N* 段，其中范围是不相交和不重叠的。任务是找出 1 到 *M* 之间不属于任何给定范围的所有数字。

**示例** :

```
Input : N = 2, M = 6
        Ranges:
        [1, 2]
        [4, 5]
Output : 3, 6
Explanation: Only 3 and 6 are missing from
the above ranges.

Input : N = 1, M = 5
        Ranges:
        [2, 4]
Output : 1, 5
```

**方法:**假设我们有 *N* 个范围，它们不重叠也不相交。首先，根据起始值对所有段进行排序。排序后，从每个片段中迭代，找出缺失的数字。

下面是上述方法的实现:

## c++

```
// C++ program to find missing elements
// from given Ranges

#include <bits/stdc++.h>
using namespace std;

// Function to find missing elements
// from given Ranges
void findMissingNumber(vector<pair<int, int> > ranges, int m)
{
    // First of all sort all the given ranges
    sort(ranges.begin(), ranges.end());

    // store ans in a different vector
    vector<int> ans;

    // prev is use to store end of
    // last range
    int prev = 0;

    // j is used as a counter for ranges
    for (int j = 0; j < ranges.size(); j++) {
        int start = ranges[j].first;
        int end = ranges[j].second;

        for (int i = prev + 1; i < start; i++)
            ans.push_back(i);

        prev = end;
    }

    // for last segment
    for (int i = prev + 1; i <= m; i++)
        ans.push_back(i);

    // finally print all answer
    for (int i = 0; i < ans.size(); i++) {
        if (ans[i] <= m)
            cout << ans[i] << " ";
    }
}

// Driver code
int main()
{
    int N = 2, M = 6;

    // Store ranges in vector of pair
    vector<pair<int, int> > ranges;
    ranges.push_back({ 1, 2 });
    ranges.push_back({ 4, 5 });

    findMissingNumber(ranges, M);

    return 0;
}
```

## Java

```
// Java program to find missing elements
// from given Ranges
import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;

class GFG{

static class Pair
{
    int first, second;

    public Pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to find missing elements
// from given Ranges
static void findMissingNumber(ArrayList<Pair> ranges,
                              int m)
{

    // First of all sort all the given ranges
    Collections.sort(ranges, new Comparator<Pair>()
    {
        public int compare(Pair first, Pair second)
        {
            if (first.first == second.first)
            {
                return first.second - second.second;
            }
            return first.first - second.first;
        }
    });

    // Store ans in a different vector
    ArrayList<Integer> ans = new ArrayList<>();

    // prev is use to store end of
    // last range
    int prev = 0;

    // j is used as a counter for ranges
    for(int j = 0; j < ranges.size(); j++)
    {
        int start = ranges.get(j).first;
        int end = ranges.get(j).second;

        for(int i = prev + 1; i < start; i++)
            ans.add(i);

        prev = end;
    }

    // For last segment
    for(int i = prev + 1; i <= m; i++)
        ans.add(i);

    // Finally print all answer
    for(int i = 0; i < ans.size(); i++)
    {
        if (ans.get(i) <= m)
            System.out.print(ans.get(i) + " ");
    }
}

// Driver code
public static void main(String[] args)
{
    int N = 2, M = 6;

    // Store ranges in vector of pair
    ArrayList<Pair> ranges = new ArrayList<>();
    ranges.add(new Pair(1, 2));
    ranges.add(new Pair(4, 5));

    findMissingNumber(ranges, M);
}
}

// This code is contributed by sanjeev2552
```

## python 3

```
# Python3 program to find missing
# elements from given Ranges

# Function to find missing elements
# from given Ranges
def findMissingNumber(ranges, m):

    # First of all sort all the
    # given ranges
    ranges.sort()

    # store ans in a different vector
    ans = []

    # prev is use to store end
    # of last range
    prev = 0

    # j is used as a counter for ranges
    for j in range(len(ranges)):
        start = ranges[j][0]
        end = ranges[j][1]

        for i in range(prev + 1, start):
            ans.append(i)

        prev = end

    # for last segment
    for i in range(prev + 1, m + 1):
        ans.append(i)

    # finally print all answer
    for i in range(len(ans)):
        if ans[i] <= m:
            print(ans[i], end = " ")

# Driver Code
if __name__ == "__main__":

    N, M = 2, 6

    # Store ranges in vector of pair
    ranges = []
    ranges.append([1, 2])
    ranges.append([4, 5])

    findMissingNumber(ranges, M)

# This code is contributed
# by Rituraj Jain
```

T18】c#

```
// C# program to find missing elements
// from given Ranges
using System;
using System.Collections;
using System.Collections.Generic;

class GFG{

class sortHelper : IComparer
{
   int IComparer.Compare(object a, object b)
   {
      Pair first = (Pair)a;
      Pair second = (Pair)b;
      if (first.first == second.first)
      {
        return first.second - second.second;
      }

      return first.first - second.first;
   }
}

public class Pair
{
    public int first, second;

    public Pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to find missing elements
// from given Ranges
static void findMissingNumber(ArrayList ranges, int m)
{
    IComparer myComparer = new sortHelper();
    ranges.Sort(myComparer);

    // Store ans in a different vector
    ArrayList ans = new ArrayList();

    // prev is use to store end of
    // last range
    int prev = 0;

    // j is used as a counter for ranges
    for(int j = 0; j < ranges.Count; j++)
    {
        int start = ((Pair)ranges[j]).first;
        int end = ((Pair)ranges[j]).second;

        for(int i = prev + 1; i < start; i++)
            ans.Add(i);

        prev = end;
    }

    // For last segment
    for(int i = prev + 1; i <= m; i++)
        ans.Add(i);

    // Finally print all answer
    for(int i = 0; i < ans.Count; i++)
    {
        if ((int)ans[i] <= m)
            Console.Write(ans[i] + " ");
    }
}

// Driver code
public static void Main(string[] args)
{
    int  M = 6;

    // Store ranges in vector of pair
    ArrayList ranges = new ArrayList();
    ranges.Add(new Pair(1, 2));
    ranges.Add(new Pair(4, 5));

    findMissingNumber(ranges, M);
}
}

// This code is contributed by rutvik_56
```

T21

## PHP

T4

***时间复杂度:** O(n * log(n))，其中 n 为*的长度*向量*

***辅助空间:** O(n)*