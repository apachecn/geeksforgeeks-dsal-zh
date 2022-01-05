# 位屏蔽和动态编程|设置 1(为每个人分配唯一上限的计数方式)

> 原文:[https://www . geesforgeks . org/bit masking-and-dynamic-programming-set-1-count-way-assign-unique-cap-to-ever-person/](https://www.geeksforgeeks.org/bitmasking-and-dynamic-programming-set-1-count-ways-to-assign-unique-cap-to-every-person/)

考虑下面的问题陈述。

有 100 种不同类型的瓶盖，每个瓶盖都有一个从 1 到 100 的唯一 id。此外，还有“n”个人，每个人都有不同数量的帽子。有一天，所有这些人都决定戴着一顶帽子去参加聚会，但为了显得独特，他们决定他们中没有人会戴同样类型的帽子。所以，数一数排列或方式的总数，这样就不会有人戴着同样类型的帽子。

约束:1 <= n <="10 "示例:

```
The first line contains the value of n, next n lines contain collections 
of all the n persons.
Input: 
3
5 100 1     // Collection of the first person.
2           // Collection of the second person.
5 100       // Collection of the third person.

Output:
4
Explanation: All valid possible ways are (5, 2, 100),  (100, 2, 5),
            (1, 2, 5) and  (1, 2, 100)
因为路的数量可能很大，所以输出模 1000000007**我们强烈建议你尽量减少浏览器，先自己试试这个。** 
 A **简单的解决方法**就是尝试所有可能的组合。首先从第一个集合中选取第一个元素，将其标记为已访问，并对其余集合重复出现。它基本上是一个基于回溯的解决方案。

一个**更好的解决方案是使用位屏蔽和 DP** 。让我们首先介绍一下位屏蔽。**什么是位屏蔽？** 
假设我们有一个从 1 到 N 编号的元素集合。如果我们想表示这个集合的一个子集，那么它可以由一个 N 位序列编码(我们通常称这个序列为“掩码”)。在我们选择的子集中，当且仅当掩码的第 I 位被设置，即它等于 1 时，第 I 个元素才属于它。例如，掩码 10000101 意味着集合[1… 8]的子集由元素 1、3 和 8 组成。我们知道，对于一组 N 个元素，总共有 2 个 <sup>N</sup> 子集，因此 2 个 <sup>N</sup> 掩码是可能的，每个子集代表一个掩码。事实上，每个掩码都是用二进制表示法写的整数。我们的主要方法是为每个掩码(以及每个子集)分配一个值，从而使用已经计算的掩码值来计算新掩码的值。通常我们的主要目标是计算整个集合的值/解，即掩码 11111111。通常，为了找到子集 X 的值，我们以各种可能的方式移除一个元素，并使用获得的子集 X’<sub>1</sub>、X’<sub>2</sub>…、X’<sub>k</sub>的值来计算 X 的值/解。这意味着 X’<sub>I</sub>的值必须已经计算过了，因此我们需要建立一个考虑掩码的顺序。很容易看出，自然排序就行了:按照相应数字的递增顺序遍历掩码。同样，我们有时，从空子集 X 开始，我们以各种可能的方式添加元素，并使用获得的子集 X’<sub>1</sub>、X’<sub>2</sub>…、X’<sub>k</sub>的值来计算 X 的值/解我们在掩码上主要使用以下符号/操作:
位(I，mask)–掩码的第 I 位
计数(掩码)–掩码中非零位的数量
第一位(掩码)–掩码中最低非零位的数量
设置(I，mask)–设置掩码中的第 ith 位
检查(I，mask)–检查掩码中的第 ith 位**使用位屏蔽+ DP 如何解决这个问题？** 
这个想法是利用最多有 10 个人的事实。因此，我们可以使用一个整数变量作为位掩码来存储哪个人戴着帽子，哪个人没有。

```
Let i be the current cap number (caps from 1 to i-1 are already 
processed). Let integer variable mask indicates that the persons w
earing and not wearing caps.  If i'th bit is set in mask, then 
i'th person is wearing a cap, else not.

             // consider the case when ith cap is not included 
                     // in the arrangement
countWays(mask, i) = countWays(mask, i+1) +             

                    // when ith cap is included in the arrangement
                    // so, assign this cap to all possible persons 
                    // one by one and recur for remaining persons.
                    ∑ countWays(mask | (1 << j), i+1)
                       for every person j that can wear cap i 

Note that the expression "mask | (1 << j)" sets j'th bit in mask.
And a person can wear cap i if it is there in the person's cap list
provided as input.

```

如果画出完整的递归树，可以观察到很多子问题一次又一次地被解决。所以我们使用动态编程。使用表 dp[][]使得在每个条目 dp[i][j]中，I 是掩码，j 是帽号。因为我们想访问所有能戴给定帽子的人，所以我们使用一组向量，capList[101]。capList[i]值表示可以佩戴 cap i 的人员列表。以下是上述想法的实现。

## C/C++

```
// C++ program to find number of ways to wear hats
#include<bits/stdc++.h>
#define MOD 1000000007
using namespace std;

// capList[i]'th vector contains the list of persons having a cap with id i
// id is between 1 to 100 so we declared an array of 101 vectors as indexing
// starts from 0.
vector<int> capList[101];

// dp[2^10][101] .. in dp[i][j], i denotes the mask i.e., it tells that
// how many and which persons are wearing cap. j denotes the first j caps
// used. So, dp[i][j] tells the number ways we assign j caps to mask i
// such that none of them wears the same cap
int dp[1025][101];

// This is used for base case, it has all the N bits set
// so, it tells whether all N persons are wearing a cap.
int allmask;

// Mask is the set of persons, i is cap-id (OR the 
// number of caps processed starting from first cap).
long long int countWaysUtil(int mask, int i)
{
    // If all persons are wearing a cap so we
    // are done and this is one way so return 1
    if (mask == allmask) return 1;

    // If not everyone is wearing a cap and also there are no more
    // caps left to process, so there is no way, thus return 0;
    if (i > 100) return 0;

    // If we already have solved this subproblem, return the answer.
    if (dp[mask][i] != -1) return dp[mask][i];

    // Ways, when we don't include this cap in our arrangement
    // or solution set.
    long long int ways = countWaysUtil(mask, i+1);

    // size is the total number of persons having cap with id i.
    int size = capList[i].size();

    // So, assign one by one ith cap to all the possible persons
    // and recur for remaining caps.
    for (int j = 0; j < size; j++)
    {
        // if person capList[i][j] is already wearing a cap so continue as
        // we cannot assign him this cap
        if (mask & (1 << capList[i][j])) continue;

        // Else assign him this cap and recur for remaining caps with
        // new updated mask vector
        else ways += countWaysUtil(mask | (1 << capList[i][j]), i+1);
        ways %= MOD;
    }

    // Save the result and return it.
    return dp[mask][i] = ways;
}

// Reads n lines from standard input for current test case
void countWays(int n)
{
    //----------- READ INPUT --------------------------
    string temp, str;
    int x;
    getline(cin, str);  // to get rid of newline character
    for (int i=0; i<n; i++)
    {
        getline(cin, str);
        stringstream ss(str);

        // while there are words in the streamobject ss
        while (ss >> temp)
        {
            stringstream s;
            s << temp;
            s >> x;

            // add the ith person in the list of cap if with id x
            capList[x].push_back(i);
        }
    }
    //----------------------------------------------------

    // All mask is used to check whether all persons
    // are included or not, set all n bits as 1
    allmask = (1 << n) - 1;

    // Initialize all entries in dp as -1
    memset(dp, -1, sizeof dp);

    // Call recursive function count ways
    cout << countWaysUtil(0, 1) << endl;
}

// Driver Program
int main()
{ 
     int n;   // number of persons in every test case
     cin >> n;
     countWays(n);
     return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number of ways to wear hats

import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.Vector;

class Test
{
    static final int MOD = 1000000007;

    // for input
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

    // capList[i]'th vector contains the list of persons having a cap with id i
    // id is between 1 to 100 so we declared an array of 101 vectors as indexing
    // starts from 0.
    static Vector<Integer> capList[] = new Vector[101];

    // dp[2^10][101] .. in dp[i][j], i denotes the mask i.e., it tells that
    // how many and which persons are wearing cap. j denotes the first j caps
    // used. So, dp[i][j] tells the number ways we assign j caps to mask i
    // such that none of them wears the same cap
    static int dp[][] = new int[1025][101];

    // This is used for base case, it has all the N bits set
    // so, it tells whether all N persons are wearing a cap.
    static int allmask;

    // Mask is the set of persons, i is cap-id (OR the 
    // number of caps processed starting from first cap).
    static long countWaysUtil(int mask, int i)
    {
        // If all persons are wearing a cap so we
        // are done and this is one way so return 1
        if (mask == allmask) return 1;

        // If not everyone is wearing a cap and also there are no more
        // caps left to process, so there is no way, thus return 0;
        if (i > 100) return 0;

        // If we already have solved this subproblem, return the answer.
        if (dp[mask][i] != -1) return dp[mask][i];

        // Ways, when we don't include this cap in our arrangement
        // or solution set.
        long ways = countWaysUtil(mask, i+1);

        // size is the total number of persons having cap with id i.
        int size = capList[i].size();

        // So, assign one by one ith cap to all the possible persons
        // and recur for remaining caps.
        for (int j = 0; j < size; j++)
        {
            // if person capList[i][j] is already wearing a cap so continue as
            // we cannot assign him this cap
            if ((mask & (1 << capList[i].get(j))) != 0) continue;

            // Else assign him this cap and recur for remaining caps with
            // new updated mask vector
            else ways += countWaysUtil(mask | (1 << capList[i].get(j)), i+1);
            ways %= MOD;
        }

        // Save the result and return it.
        return dp[mask][i] = (int) ways;
    }

    // Reads n lines from standard input for current test case
    static void countWays(int n) throws Exception
    {
        //----------- READ INPUT --------------------------
        String str;
        String split[];
        int x;

        for (int i=0; i<n; i++)
        {
            str = br.readLine();
            split = str.split(" ");

            // while there are words in the split[]
            for (int j = 0; j < split.length; j++) {
                 // add the ith person in the list of cap if with id x
                x = Integer.parseInt(split[j]);
                capList[x].add(i);
            }

        }
        //----------------------------------------------------

        // All mask is used to check of all persons
        // are included or not, set all n bits as 1
        allmask = (1 << n) - 1;

        // Initialize all entries in dp as -1
        for (int[] is : dp) {
            for (int i = 0; i < is.length; i++) {
                is[i] = -1;
            }
        }

        // Call recursive function count ways
        System.out.println(countWaysUtil(0, 1));
    }

    // Driver method
    public static void main(String args[]) throws Exception
    {
        int n;   // number of persons in every test case

        // initializing vector array
        for (int i = 0; i < capList.length; i++)
            capList[i] = new Vector<>();

        n = Integer.parseInt(br.readLine());
        countWays(n);
    }
}
// This code is contributed by Gaurav Miglani
```

## 计算机编程语言

```
#Python program to find number of ways to wear hats
from collections import defaultdict

class AssignCap:

    # Initialize variables
    def __init__(self):

            self.allmask = 0

            self.total_caps = 100

            self.caps = defaultdict(list)

    #  Mask is the set of persons, i is the current cap number.
    def countWaysUtil(self,dp, mask, cap_no):

        # If all persons are wearing a cap so we
        # are done and this is one way so return 1
        if mask == self.allmask:
            return 1

        # If not everyone is wearing a cap and also there are no more
        # caps left to process, so there is no way, thus return 0;
        if cap_no > self.total_caps:
            return 0

        # If we have already solved this subproblem, return the answer.
        if dp[mask][cap_no]!= -1 :
            return dp[mask][cap_no]

        # Ways, when we don't include this cap in our arrangement
        # or solution set
        ways = self.countWaysUtil(dp, mask, cap_no + 1)

        # assign ith cap one by one  to all the possible persons
        # and recur for remaining caps.
        if cap_no in self.caps:

            for ppl in self.caps[cap_no]:

                # if person 'ppl' is already wearing a cap then continue
                if mask & (1 << ppl) : continue

                # Else assign him this cap and recur for remaining caps with
                # new updated mask vector
                ways += self.countWaysUtil(dp, mask | (1 << ppl), cap_no + 1) 

                ways = ways % (10**9 + 7)

        # Save the result and return it
        dp[mask][cap_no] = ways

        return dp[mask][cap_no]

    def countWays(self,N):

        # Reads n lines from standard input for current test case
        # create dictionary for cap. cap[i] = list of person having
        # cap no i
        for ppl in range(N):

            cap_possessed_by_person = map(int, raw_input().strip().split())

            for i in cap_possessed_by_person:

                self.caps[i].append(ppl)

        # allmask is used to check if all persons
        # are included or not, set all n bits as 1
        self.allmask = (1 << N) -1

        # Initialize all entries in dp as -1
        dp = [[-1 for j in range(self.total_caps + 1)] for i in range(2 ** N)]

        # Call recursive function countWaysUtil
        # result will be in dp[0][1]
        print self.countWaysUtil(dp, 0, 1,)

#Driver Program
def main():
    No_of_people = input() # number of persons in every test case

    AssignCap().countWays(No_of_people)

if __name__ == '__main__':
    main()

# This code is contributed by Neelam Yadav
```

Input:

```
3               
5 100 1         
2               
5 100
```

输出:

```
4
```

本文由 Gaurav Ahirwar 供稿。如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论

=>

```