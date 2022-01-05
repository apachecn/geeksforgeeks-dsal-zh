# 组合和

> 原文:[https://www.geeksforgeeks.org/combinational-sum/](https://www.geeksforgeeks.org/combinational-sum/)

给定一组正整数 **arr[]** 和一个和 **x** ，在 arr[]中找到所有唯一的组合，其中和等于 x。相同的重复数可以从 arr[]中无限次选择。组合(a1，a2，…，ak)中的元素必须以非降序打印。(即 a1 < = a2 < = … < = ak)。
组合本身必须按升序排序，即首先打印第一个元素最小的组合。如果没有可能的组合，打印“空”(不带引号)。

**示例:**

```
Input : arr[] = 2, 4, 6, 8 
            x = 8
Output : [2, 2, 2, 2]
         [2, 2, 4]
         [2, 6]
         [4, 4]
         [8]
```

由于问题是得到所有可能的结果，而不是最好的或结果的数量，因此我们不需要考虑 DP(动态规划)，需要递归来处理它。

我们应该使用以下算法。

```
1\. Sort the array(non-decreasing).
2\. First remove all the duplicates from array.
3\. Then use recursion and backtracking to solve 
   the problem.
   (A) If at any time sub-problem sum == 0 then 
       add that array to the result (vector of 
       vectors).
   (B) Else if sum is negative then ignore that 
       sub-problem.
   (C) Else insert the present index in that 
       array to the current vector and call 
       the function with sum = sum-ar[index] and
       index = index, then pop that element from 
       current index (backtrack) and call the 
       function with sum = sum and index = index+1
```

下面是上述步骤的 C++实现。

## C++

```
// C++ program to find all combinations that
// sum to a given value
#include <bits/stdc++.h>
using namespace std;

// Print all members of ar[] that have given
void findNumbers(vector<int>& ar, int sum,
                 vector<vector<int> >& res, vector<int>& r,
                 int i)
{
    // if we get exact answer
    if (sum == 0) {
        res.push_back(r);
        return;
    }

    // Recur for all remaining elements that
    // have value smaller than sum.
    while (i < ar.size() && sum - ar[i] >= 0) {

        // Till every element in the array starting
        // from i which can contribute to the sum
        r.push_back(ar[i]); // add them to list

        // recur for next numbers
        findNumbers(ar, sum - ar[i], res, r, i);
        i++;

        // Remove number from list (backtracking)
        r.pop_back();
    }
}

// Returns all combinations
// of ar[] that have given
// sum.
vector<vector<int> > combinationSum(vector<int>& ar,
                                    int sum)
{
    // sort input array
    sort(ar.begin(), ar.end());

    // remove duplicates
    ar.erase(unique(ar.begin(), ar.end()), ar.end());

    vector<int> r;
    vector<vector<int> > res;
    findNumbers(ar, sum, res, r, 0);

    return res;
}

// Driver code
int main()
{
    vector<int> ar;
    ar.push_back(2);
    ar.push_back(4);
    ar.push_back(6);
    ar.push_back(8);
    int n = ar.size();

    int sum = 8; // set value of sum
    vector<vector<int> > res = combinationSum(ar, sum);

    // If result is empty, then
    if (res.size() == 0) {
        cout << "Emptyn";
        return 0;
    }

    // Print all combinations stored in res.
    for (int i = 0; i < res.size(); i++) {
        if (res[i].size() > 0) {
            cout << " ( ";
            for (int j = 0; j < res[i].size(); j++)
                cout << res[i][j] << " ";
            cout << ")";
        }
    }
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find all combinations that
// sum to a given value
import java.io.*;
import java.util.*;

class GFG {

    static ArrayList<ArrayList<Integer> >
    combinationSum(ArrayList<Integer> arr, int sum)
    {
        ArrayList<ArrayList<Integer> > ans
            = new ArrayList<>();
        ArrayList<Integer> temp = new ArrayList<>();

        // first do hashing since hashset does not always
        // sort
        //  removing the duplicates using HashSet and
        // Sorting the arrayList

        Set<Integer> set = new HashSet<>(arr);
        arr.clear();
        arr.addAll(set);
        Collections.sort(arr);

        findNumbers(ans, arr, sum, 0, temp);
        return ans;
    }

    static void
    findNumbers(ArrayList<ArrayList<Integer> > ans,
                ArrayList<Integer> arr, int sum, int index,
                ArrayList<Integer> temp)
    {

        if (sum == 0) {

            // Adding deep copy of list to ans

            ans.add(new ArrayList<>(temp));
            return;
        }

        for (int i = index; i < arr.size(); i++) {

            // checking that sum does not become negative

            if ((sum - arr.get(i)) >= 0) {

                // adding element which can contribute to
                // sum

                temp.add(arr.get(i));

                findNumbers(ans, arr, sum - arr.get(i), i,
                            temp);

                // removing element from list (backtracking)
                temp.remove(arr.get(i));
            }
        }
    }

    // Driver Code

    public static void main(String[] args)
    {
        ArrayList<Integer> arr = new ArrayList<>();

        arr.add(2);
        arr.add(4);
        arr.add(6);
        arr.add(8);

        int sum = 8;

        ArrayList<ArrayList<Integer> > ans
            = combinationSum(arr, sum);

        // If result is empty, then
        if (ans.size() == 0) {
            System.out.println("Empty");
            return;
        }

        // print all combinations stored in ans

        for (int i = 0; i < ans.size(); i++) {

            System.out.print("(");
            for (int j = 0; j < ans.get(i).size(); j++) {
                System.out.print(ans.get(i).get(j) + " ");
            }
            System.out.print(") ");
        }
    }
}
```

## 蟒蛇 3

```
# Python3 program to find all combinations that
# sum to a given value

def combinationSum(arr, sum):
    ans = []
    temp = []

    # first do hashing nothing but set{}
    # since set does not always sort
    # removing the duplicates using Set and
    # Sorting the List
    arr = sorted(list(set(arr)))
    findNumbers(ans, arr, temp, sum, 0)
    return ans

def findNumbers(ans, arr, temp, sum, index):

    if(sum == 0):

        # Adding deep copy of list to ans
        ans.append(list(temp))
        return

    # Iterate from index to len(arr) - 1
    for i in range(index, len(arr)):

        # checking that sum does not become negative
        if(sum - arr[i]) >= 0:

            # adding element which can contribute to
            # sum
            temp.append(arr[i])
            findNumbers(ans, arr, temp, sum-arr[i], i)

            # removing element from list (backtracking)
            temp.remove(arr[i])

# Driver Code
arr = [2, 4, 6, 8]
sum = 8
ans = combinationSum(arr, sum)

# If result is empty, then
if len(ans) <= 0:
    print("empty")

# print all combinations stored in ans
for i in range(len(ans)):

    print("(", end=' ')
    for j in range(len(ans[i])):
        print(str(ans[i][j])+" ", end=' ')
    print(")", end=' ')

# This Code Is Contributed by Rakesh(vijayarigela09)
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
using System.Collections;

class GFG {

    static List<List<int> >
    combinationSum(List<int> arr, int sum)
    {
        List<List<int> > ans
            = new List<List<int> >();
        List<int> temp = new List<int>();

        // first do hashing since hashset does not always
        // sort
        //  removing the duplicates using HashSet and
        // Sorting the List

        HashSet<int> set = new HashSet<int>(arr);
        arr.Clear();
        arr.AddRange(set);
        arr.Sort();

        findNumbers(ans, arr, sum, 0, temp);
        return ans;
    }

    static void
    findNumbers(List<List<int> > ans,
                List<int> arr, int sum, int index,
                List<int> temp)
    {

        if (sum == 0) {

            // Adding deep copy of list to ans

            ans.Add(new List<int>(temp));
            return;
        }

        for (int i = index; i < arr.Count; i++) {

            // checking that sum does not become negative

            if ((sum - arr[i]) >= 0) {

                // Adding element which can contribute to
                // sum

                temp.Add(arr[i]);

                findNumbers(ans, arr, sum - arr[i], i,
                            temp);

                // removing element from list (backtracking)
                temp.Remove(arr[i]);
            }
        }
    }

    // Driver Code

    public static void Main()
    {
        List<int> arr = new List<int>();

        arr.Add(2);
        arr.Add(4);
        arr.Add(6);
        arr.Add(8);

        int sum = 8;

        List<List<int> > ans
            = combinationSum(arr, sum);

        // If result is empty, then
        if (ans.Count == 0) {
            Console.WriteLine("Empty");
            return;
        }

        // print all combinations stored in ans

        for (int i = 0; i < ans.Count; i++) {

            Console.Write("(");
            for (int j = 0; j < ans[i].Count; j++) {
                Console.Write(ans[i][j] + " ");
            }
            Console.Write(") ");
        }
    }
}

// This code is contributed by ShubhamSingh10
```

**Output**

```
 ( 2 2 2 2 ) ( 2 2 4 ) ( 2 6 ) ( 4 4 ) ( 8 )
```

本文由**阿迪蒂亚·尼哈尔·库马尔·辛格**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。