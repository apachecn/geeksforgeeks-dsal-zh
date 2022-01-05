# 将非负整数数组划分为两个子集，使得两个子集的平均值相等

> 原文:[https://www . geesforgeks . org/将非负整数数组划分为两个子集，使得两个子集的平均值相等/](https://www.geeksforgeeks.org/partition-an-array-of-non-negative-integers-into-two-subsets-such-that-average-of-both-the-subsets-is-equal/)

给定大小为 **N** 的数组。任务是将给定的数组划分为两个子集，使得两个子集中所有元素的平均值相等。如果不存在这样的分区，打印-1。否则，打印分区。如果存在多个解决方案，打印第一个子集长度最小的解决方案。如果仍有平局，则打印第一个子集按字典顺序最小的分区。

**示例:**

```
Input : vec[] = {1, 7, 15, 29, 11, 9}
Output : [9, 15] [1, 7, 11, 29]
Explanation : Average of the both the subsets is 12

Input : vec[] = {1, 2, 3, 4, 5, 6}
Output : [1, 6] [2, 3, 4, 5]. 
Explanation : Another possible solution is [3, 4] [1, 2, 5, 6], 
but print the  solution whose first subset is lexicographically 
smallest.

```

**观察:**
如果我们直接计算某个子集的平均值，并与另一个子集的平均值进行比较，由于编译器的精度问题，会出现意想不到的结果。例如，5/3 = 1.66666..而 166/100 = 1.66。一些编译器可能会将它们视为相同的，而另一些则不会。
设所考虑的两个子集之和为 sub1 和 sub2，大小为 s1 和 s2。如果它们的平均值相等，sub1/s1 = sub2/s2。这意味着 sub1*s2 = sub2*s1。
同样，上述两个子集的总和= sub1+sub2，s2=总大小–S1。
关于简化上述内容，我们得到

> (sub1/s1) = (sub1+sub2)/ (s1+s2) =(总和)/(总大小)。

现在这个问题简化为这样一个事实，如果我们能选择一个特定大小的子集
，它的和等于当前子集的和，我们就完成了。

**方法:**
让我们定义函数分区(ind，curr_sum，curr_size)，如果可以使用索引等于 ind 且大小等于 curr_size 且总和等于 curr_sum 的元素构造子集，则返回 true。
这个递归关系可以定义为:

> 分区(ind，curr_sum，curr_size) =分区(ind+1，curr_sum，curr_size) ||分区(ind+1，curr _ sum–val[ind]，curr_size-1)。

上述等式右侧的两个部分表示我们是否包括索引**处的元素。
这是对经典[子集和问题](https://www.geeksforgeeks.org/dynamic-programming-subset-sum-problem/)的偏离，在经典[子集和问题中，子问题被一次又一次地评估。因此我们记住子问题，并将其转化为](https://www.geeksforgeeks.org/dynamic-programming-subset-sum-problem/)[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解。**

## C++14

```
// C++ program to Partition an array of
// non-negative integers into two subsets
// such that average of both the subsets are equal
#include <bits/stdc++.h>
using namespace std;

vector<vector<vector<bool> > > dp;
vector<int> res;
vector<int> original;
int total_size;

// Function that returns true if it is possible to
// use elements with index = ind to construct a set of s
// ize = curr_size whose sum is curr_sum.
bool possible(int index, int curr_sum, int curr_size)
{
    // base cases
    if (curr_size == 0)
        return (curr_sum == 0);
    if (index >= total_size)
        return false;

    // Which means curr_sum cant be found for curr_size
    if (dp[index][curr_sum][curr_size] == false)
        return false;

    if (curr_sum >= original[index]) {
        res.push_back(original[index]);
        // Checks if taking this element at
        // index i leads to a solution
        if (possible(index + 1, curr_sum -
        original[index],
                     curr_size - 1))
            return true;

        res.pop_back();
    }
    // Checks if not taking this element at
    // index i leads to a solution
    if (possible(index + 1, curr_sum, curr_size))
        return true;

    // If no solution has been found
    return dp[index][curr_sum][curr_size] = false;
}

// Function to find two Partitions having equal average
vector<vector<int> > partition(vector<int>& Vec)
{
    // Sort the vector
    sort(Vec.begin(), Vec.end());
    original.clear();
    original = Vec;
    dp.clear();
    res.clear();

    int total_sum = 0;
    total_size = Vec.size();

    for (int i = 0; i < total_size; ++i)
        total_sum += Vec[i];
    // building the memoization table
    dp.resize(original.size(), vector<vector<bool> >
(total_sum + 1, vector<bool>(total_size, true)));

    for (int i = 1; i < total_size; i++) {
        // Sum_of_Set1 has to be an integer
        if ((total_sum * i) % total_size != 0)
            continue;
        int Sum_of_Set1 = (total_sum * i) / total_size;

        // We build our solution vector if its possible
        // to find subsets that match our criteria
        // using a recursive function
        if (possible(0, Sum_of_Set1, i)) {

            // Find out the elements in Vec, not in
            // res and return the result.
            int ptr1 = 0, ptr2 = 0;
            vector<int> res1 = res;
            vector<int> res2;
            while (ptr1 < Vec.size() || ptr2 < res.size())
            {
                if (ptr2 < res.size() &&
                        res[ptr2] == Vec[ptr1])
                {
                    ptr1++;
                    ptr2++;
                    continue;
                }
                res2.push_back(Vec[ptr1]);
                ptr1++;
            }

            vector<vector<int> > ans;
            ans.push_back(res1);
            ans.push_back(res2);
            return ans;
        }
    }
    // If we havent found any such subset.
    vector<vector<int> > ans;
    return ans;
}

// Function to print partitions
void Print_Partition(vector<vector<int> > sol)
{
    // Print two partitions
    for (int i = 0; i < sol.size(); i++) {
        cout << "[";
        for (int j = 0; j < sol[i].size(); j++) {
            cout << sol[i][j];
            if (j != sol[i].size() - 1)
                cout << " ";
        }
        cout << "] ";
    }
}

// Driver code
int main()
{
    vector<int> Vec = { 1, 7, 15, 29, 11, 9 };

    vector<vector<int> > sol = partition(Vec);

    // If partition possible
    if (sol.size())
        Print_Partition(sol);
    else
        cout << -1;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Partition an array of
// non-negative integers into two subsets
// such that average of both the subsets are equal
import java.io.*;
import java.util.*;

class GFG
{

    static boolean[][][] dp;
    static Vector<Integer> res = new Vector<>();
    static int[] original;
    static int total_size;

    // Function that returns true if it is possible to
    // use elements with index = ind to construct a set of s
    // ize = curr_size whose sum is curr_sum.
    static boolean possible(int index, int curr_sum,
                                        int curr_size)
    {

        // base cases
        if (curr_size == 0)
            return (curr_sum == 0);
        if (index >= total_size)
            return false;

        // Which means curr_sum cant be found for curr_size
        if (dp[index][curr_sum][curr_size] == false)
            return false;

        if (curr_sum >= original[index])
        {
            res.add(original[index]);

            // Checks if taking this element at
            // index i leads to a solution
            if (possible(index + 1, curr_sum - original[index],
                                                curr_size - 1))
                return true;

            res.remove(res.size() - 1);
        }

        // Checks if not taking this element at
        // index i leads to a solution
        if (possible(index + 1, curr_sum, curr_size))
            return true;

        // If no solution has been found
        return dp[index][curr_sum][curr_size] = false;
    }

    // Function to find two Partitions having equal average
    static Vector<Vector<Integer>> partition(int[] Vec)
    {

        // Sort the vector
        Arrays.sort(Vec);
        original = Vec;
        res.clear();

        int total_sum = 0;
        total_size = Vec.length;

        for (int i = 0; i < total_size; ++i)
            total_sum += Vec[i];

        // building the memoization table
        dp = new boolean[original.length][total_sum + 1][total_size];

        for (int i = 0; i < original.length; i++)
            for (int j = 0; j < total_sum + 1; j++)
                for (int k = 0; k < total_size; k++)
                    dp[i][j][k] = true;

        for (int i = 1; i < total_size; i++)
        {

            // Sum_of_Set1 has to be an integer
            if ((total_sum * i) % total_size != 0)
                continue;
            int Sum_of_Set1 = (total_sum * i) / total_size;

            // We build our solution vector if its possible
            // to find subsets that match our criteria
            // using a recursive function
            if (possible(0, Sum_of_Set1, i))
            {

                // Find out the elements in Vec, not in
                // res and return the result.
                int ptr1 = 0, ptr2 = 0;
                Vector<Integer> res1 = res;
                Vector<Integer> res2 = new Vector<>();
                while (ptr1 < Vec.length || ptr2 < res.size())
                {
                    if (ptr2 < res.size() &&
                        res.elementAt(ptr2) == Vec[ptr1])
                    {
                        ptr1++;
                        ptr2++;
                        continue;
                    }
                    res2.add(Vec[ptr1]);
                    ptr1++;
                }

                Vector<Vector<Integer>> ans = new Vector<>();
                ans.add(res1);
                ans.add(res2);
                return ans;
            }
        }

        // If we havent found any such subset.
        Vector<Vector<Integer>> ans = new Vector<>();
        return ans;
    }

    // Function to print partitions
    static void Print_Partition(Vector<Vector<Integer>> sol)
    {

        // Print two partitions
        for (int i = 0; i < sol.size(); i++)
        {
            System.out.print("[");
            for (int j = 0; j < sol.elementAt(i).size(); j++)
            {
                System.out.print(sol.elementAt(i).elementAt(j));
                if (j != sol.elementAt(i).size() - 1)
                    System.out.print(" ");
            }
            System.out.print("]");
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] Vec = { 1, 7, 15, 29, 11, 9 };
        Vector<Vector<Integer>> sol = partition(Vec);

        // If partition possible
        if (sol.size() > 0)
            Print_Partition(sol);
        else
            System.out.println("-1");
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 program to partition an array of
# non-negative integers into two subsets
# such that average of both the subsets are equal
dp = []
res = []
original = []
total_size = int(0)

# Function that returns true if it is possible
# to use elements with index = ind to construct
# a set of s ize = curr_size whose sum is curr_sum.
def possible(index, curr_sum, curr_size):

    index = int(index)
    curr_sum = int(curr_sum)
    curr_size = int(curr_size)

    global dp, res

    # Base cases
    if curr_size == 0:
        return (curr_sum == 0)
    if index >= total_size:
        return False

    # Which means curr_sum cant be
    # found for curr_size
    if dp[index][curr_sum][curr_size] == False:
        return False

    if curr_sum >= original[index]:
        res.append(original[index])

        # Checks if taking this element
        # at index i leads to a solution
        if possible(index + 1,
                    curr_sum - original[index],
                    curr_size - 1):
            return True

        res.pop()

    # Checks if not taking this element at
    # index i leads to a solution
    if possible(index + 1, curr_sum, curr_size):
        return True

    # If no solution has been found
    dp[index][curr_sum][curr_size] = False
    return False

# Function to find two partitions
# having equal average
def partition(Vec):

    global dp, original, res, total_size

    # Sort the vector
    Vec.sort()

    if len(original) > 0:
        original.clear()

    original = Vec

    if len(dp) > 0:
        dp.clear()
    if len(res) > 0:
        res.clear()

    total_sum = 0
    total_size = len(Vec)

    for i in range(total_size):
        total_sum += Vec[i]

    # Building the memoization table
    dp = [[[True for _ in range(total_size)]
                 for _ in range(total_sum + 1)]
                 for _ in range(len(original))]

    for i in range(1, total_size):

        # Sum_of_Set1 has to be an integer
        if (total_sum * i) % total_size != 0:
            continue

        Sum_of_Set1 = (total_sum * i) / total_size

        # We build our solution vector if its possible
        # to find subsets that match our criteria
        # using a recursive function
        if possible(0, Sum_of_Set1, i):

            # Find out the elements in Vec,
            # not in res and return the result.
            ptr1 = 0
            ptr2 = 0
            res1 = res
            res2 = []

            while ptr1 < len(Vec) or ptr2 < len(res):
                if (ptr2 < len(res) and
                    res[ptr2] == Vec[ptr1]):
                    ptr1 += 1
                    ptr2 += 1
                    continue

                res2.append(Vec[ptr1])
                ptr1 += 1

            ans = []
            ans.append(res1)
            ans.append(res2)

            return ans

    # If we havent found any such subset.
    ans = []
    return ans

# Driver code
Vec = [ 1, 7, 15, 29, 11, 9 ]

sol = partition(Vec)

if len(sol) > 0:
    print(sol)
else:
    print("-1")

# This code is contributed by saishashank1
```

## C#

```
// C# program to Partition an array of 
// non-negative integers into two subsets 
// such that average of both the subsets are equal 
using System;
using System.Collections; 

class GFG{

static bool[,,] dp;
static ArrayList res = new ArrayList();
static int[] original;
static int total_size;

// Function that returns true if it is possible to
// use elements with index = ind to construct a set of s
// ize = curr_size whose sum is curr_sum.
static bool possible(int index, int curr_sum, 
                                int curr_size) 
{

    // base cases
    if (curr_size == 0)
        return (curr_sum == 0);
    if (index >= total_size)
        return false;

    // Which means curr_sum cant be
    // found for curr_size
    if (dp[index, curr_sum, curr_size] == false)
        return false;

    if (curr_sum >= original[index])
    {
        res.Add(original[index]);

        // Checks if taking this element at
        // index i leads to a solution
        if (possible(index + 1, curr_sum -
                     original[index], curr_size - 1))
            return true;

        res.Remove(res[res.Count - 1]);
    }

    // Checks if not taking this element at
    // index i leads to a solution
    if (possible(index + 1, curr_sum, curr_size))
        return true;

    dp[index, curr_sum, curr_size] = false;

    // If no solution has been found
    return dp[index, curr_sum, curr_size];
}

// Function to find two Partitions
// having equal average
static ArrayList partition(int[] Vec)
{

    // Sort the vector
    Array.Sort(Vec);
    original = Vec;
    res.Clear();

    int total_sum = 0;
    total_size = Vec.Length;

    for(int i = 0; i < total_size; ++i)
        total_sum += Vec[i];

    // Building the memoization table
    dp = new bool[original.Length,
                  total_sum + 1,
                  total_size];

    for(int i = 0; i < original.Length; i++)
        for(int j = 0; j < total_sum + 1; j++)
            for(int k = 0; k < total_size; k++)
                dp[i, j, k] = true;

    for(int i = 1; i < total_size; i++) 
    {

        // Sum_of_Set1 has to be an integer
        if ((total_sum * i) % total_size != 0)
            continue;

        int Sum_of_Set1 = (total_sum * i) / total_size;

        // We build our solution vector if its possible
        // to find subsets that match our criteria
        // using a recursive function
        if (possible(0, Sum_of_Set1, i)) 
        {

            // Find out the elements in Vec, not in
            // res and return the result.
            int ptr1 = 0, ptr2 = 0;

            ArrayList res1 = new ArrayList(res);
            ArrayList res2 = new ArrayList();

            while (ptr1 < Vec.Length || ptr2 < res.Count)
            {
                if (ptr2 < res.Count && 
                   (int)res[ptr2] == Vec[ptr1])
                {
                    ptr1++;
                    ptr2++;
                    continue;
                }
                res2.Add(Vec[ptr1]);
                ptr1++;
            }

            ArrayList ans = new ArrayList();
            ans.Add(res1);
            ans.Add(res2);
            return ans;
        }
    }

    // If we havent found any such subset.
    ArrayList ans2 = new ArrayList();
    return ans2;
}

// Function to print partitions
static void Print_Partition(ArrayList sol) 
{

    // Print two partitions
    for(int i = 0; i < sol.Count; i++) 
    {
        Console.Write("[");
        for(int j = 0; j < ((ArrayList)sol[i]).Count; j++) 
        {
            Console.Write((int)((ArrayList)sol[i])[j]);
            if (j != ((ArrayList)sol[i]).Count - 1)
                Console.Write(" ");
        }
        Console.Write("] ");
    }
}

// Driver Code
public static void Main(string[] args)
{
    int[] Vec = { 1, 7, 15, 29, 11, 9 };
    ArrayList sol = partition(Vec);

    // If partition possible
    if (sol.Count > 0)
        Print_Partition(sol);
    else
        Console.Write("-1");
}
}

// This code is contributed by rutvik_56
```

**Output:** 

```
[9 15] [1 7 11 29]

```