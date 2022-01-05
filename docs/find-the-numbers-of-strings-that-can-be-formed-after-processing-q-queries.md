# 查找 Q 查询处理后可以形成的字符串个数

> 原文:[https://www . geeksforgeeks . org/find-the-numbers-of-the-string-of-the-numbers-of-the-the-numbers-of-the-of-the-numbers-of-the-of-the-the-the-numbers-of-the-the-the-the-the-numbers](https://www.geeksforgeeks.org/find-the-numbers-of-strings-that-can-be-formed-after-processing-q-queries/)

给定一个数字 **N** (1 < =N < =2000)。，任务是通过处理给定的 **q** (1 < =q < =200000)查询，找到使用从“a”到“z”的字符后可以获得的大小为 N 的数字串。

对于每个给定两个整数 L，R (0<=L<=R<=N)的查询，生成的大小为 N 的字符串的子串[L，R]必须是回文。任务是处理所有查询并生成一个大小为 N 的字符串，这样由所有查询定义的该字符串的子字符串都是回文。

答案可能非常大。所以，输出答案模 1000000007。

**注**:字符串考虑基于 1 的索引。

**示例:**

```
Input : N = 3
query 1: (1, 2)
query 2: (2, 3)
Output : 26
Explanation : Substring 1 to 2 should be 
palindrome and substring 2 to 3 should be palindrome. so, all 
three characters should be same. so, we can obtain 26 such strings.

Input : N = 4
query 1: (1, 3)
query 2: (2, 4)
Output : 676
Explanation : substring 1 to 3 should be 
palindrome and substring 2 to 4 should be a palindrome. 
So, a first and third character should be the same and 
second and the fourth should be the same. So, we can 
obtain 26*26 such strings.

```

**逼近**:一个有效的解决方案是使用[联合查找](https://www.geeksforgeeks.org/union-find-algorithm-set-2-union-by-rank/)算法。

*   找到每个范围的中点(查询)，如果有许多查询具有相同的中点，则只保留长度最大的查询，即(其中 r–l 最大)。
*   由于长度为 N 的字符串中有 2*N 个中间点，这将使查询数量最多减少到 2*N
*   现在，对于每个查询，执行元素 l 与 r 的并集，(l + 1)与(r–1)、(l + 2)与(r–2)的并集，以此类推。我们这样做是因为放在索引 l 上的字符将与放在索引 r 上的字符相同。将这个逻辑扩展到所有查询，我们需要维护[不相交集数据结构](https://www.geeksforgeeks.org/union-find/)。所以基本上不相交集的一个分量的所有元素都应该有相同的字母。
*   After processing all the queries, let the number of disjoint-set components be x, then the answer is 26^x

    。

    以下是上述方法的实现:

    ## C++

    ```
    // C++ program to implement above approach

    #include <bits/stdc++.h>
    using namespace std;
    #define N 2005
    #define mod (int)(1e9 + 7)

    // To store the size of string and
    // number of queries
    int n, q;

    // To store parent and rank of ith place
    int par[N], Rank[N];

    // To store maximum interval
    map<int, int> m;

    // Function for initialization
    void initialize()
    {
        for (int i = 0; i <= n; i++) {
            par[i] = i;
            Rank[i] = 0;
        }
    }

    // Function to find parent
    int find(int x)
    {
        if (par[x] != x)
            par[x] = find(par[x]);

        return par[x];
    }

    // Function to make union
    void Union(int x, int y)
    {
        int xpar = find(x);
        int ypar = find(y);

        if (Rank[xpar] < Rank[ypar])
            par[xpar] = ypar;
        else if (Rank[xpar] > Rank[ypar])
            par[ypar] = xpar;
        else {
            par[ypar] = xpar;
            Rank[xpar]++;
        }
    }

    // Power function to calculate a raised to m1
    // under modulo 10000007
    int power(long long a, long long m1)
    {
        if (m1 == 0)
            return 1;
        else if (m1 == 1)
            return a;
        else if (m1 == 2)
            return (1LL * a * a) % mod;
        else if (m1 & 1)
            return (1LL * a * power(power(a, m1 / 2), 2)) % mod;
        else
            return power(power(a, m1 / 2), 2) % mod;
    }

    // Function to take maxmium interval
    void query(int l, int r)
    {
        m[l + r] = max(m[l + r], r);
    }

    // Function to find different possible strings
    int possiblestrings()
    {
        initialize();

        for (auto i = m.begin(); i != m.end(); i++) {
            int x = i->first - i->second;
            int y = i->second;

            // make union of all chracters which
            // are meant to be same
            while (x < y) {
                Union(x, y);
                x++;
                y--;
            }
        }

        // find number of different sets formed
        int ans = 0;
        for (int i = 1; i <= n; i++)
            if (par[i] == i)
                ans++;

        // return the required answer
        return power(26, ans) % mod;
    }

    // Driver Code
    int main()
    {
        n = 4;

        // queries
        query(1, 3);
        query(2, 4);

        cout << possiblestrings();

        return 0;
    }
    ```

    ## Java 语言(一种计算机语言，尤用于创建网站)

    ```
    // Java program to implement above approach
    import java.util.*;

    class GFG 
    {
        static final int N = 2005;
        static final int mod = 1000000007;

        // To store the size of string and
        // number of queries
        static int n, q;

        // To store parent and rank of ith place
        static int[] par = new int[N], Rank = new int[N];

        // To store maximum interval
        static HashMap<Integer,
                       Integer> m = new HashMap<>();

        // Function for initialization
        static void initialize()
        {
            for (int i = 0; i <= n; i++)
            {
                par[i] = i;
                Rank[i] = 0;
            }
        }

        // Function to find parent
        static int find(int x)
        {
            if (par[x] != x)
                par[x] = find(par[x]);

            return par[x];
        }

        // Function to make union
        static void Union(int x, int y) 
        {
            int xpar = find(x);
            int ypar = find(y);

            if (Rank[xpar] < Rank[ypar])
                par[xpar] = ypar;
            else if (Rank[xpar] > Rank[ypar])
                par[ypar] = xpar;
            else 
            {
                par[ypar] = xpar;
                Rank[xpar]++;
            }
        }

        // Power function to calculate a raised to m1
        // under modulo 10000007
        static long power(long a, long m1) 
        {
            if (m1 == 0)
                return 1;
            else if (m1 == 1)
                return a;
            else if (m1 == 2)
                return (1L * a * a) % mod;
            else if (m1 % 2 == 1)
                return (1L * a * power(power(a, m1 / 2), 2)) % mod;
            else
                return power(power(a, m1 / 2), 2) % mod;
        }

        // Function to take maxmium interval
        static void query(int l, int r)
        {
            if (m.containsKey(l + r))
                m.put(l + r, Math.max(m.get(l + r), r));
            else
                m.put(l + r, r);
        }

        // Function to find different possible strings
        static long possiblestrings() 
        {
            initialize();

            for (Integer i : m.keySet())
            {
                int x = i - m.get(i);
                int y = m.get(i);

                // make union of all chracters which
                // are meant to be same
                while (x < y) 
                {
                    Union(x, y);
                    x++;
                    y--;
                }
            }

            // find number of different sets formed
            int ans = 0;
            for (int i = 1; i <= n; i++)
                if (par[i] == i)
                    ans++;

            // return the required answer
            return power(26, ans) % mod;
        }

        // Driver Code
        public static void main(String[] args) 
        {
            n = 4;

            // queries
            query(1, 3);
            query(2, 4);

            System.out.println(possiblestrings());
        }
    }

    // This code is contributed by
    // sanjeev2552
    ```

    ## 蟒蛇 3

    ```
    # Python3 program to implement above approach
    N = 2005
    mod = 10**9 + 7

    # To store the size of string and
    # number of queries
    n, q = 0, 0

    # To store parent and rank of ith place
    par = [0 for i in range(N)]
    Rank = [0 for i in range(N)]

    # To store maximum interval
    m = dict()

    # Function for initialization
    def initialize():

        for i in range(n + 1):
            Rank[i], par[i] = 0, i

    # Function to find parent
    def find(x):
        if (par[x] != x):
            par[x] = find(par[x])

        return par[x]

    # Function to make union
    def Union(x, y):

        xpar = find(x)
        ypar = find(y)

        if (Rank[xpar] < Rank[ypar]):
            par[xpar] = ypar
        elif (Rank[xpar] > Rank[ypar]):
            par[ypar] = xpar
        else:
            par[ypar] = xpar
            Rank[xpar] += 1

    # Power function to calculate a raised to m1
    # under modulo 10000007
    def power(a, m1):

        if (m1 == 0):
            return 1
        elif (m1 == 1):
            return a
        elif (m1 == 2):
            return (a * a) % mod
        elif (m1 & 1):
            return (a * power(power(a, m1 // 2), 2)) % mod
        else:
            return power(power(a, m1 // 2), 2) % mod

    # Function to take maxmium interval
    def query(l, r):
        if l + r in m.keys():
            m[l + r] = max(m[l + r], r)
        else:
            m[l + r] = max(0, r)

    # Function to find different possible strings
    def possiblestrings():
        initialize()

        for i in m:
            x = i - m[i]
            y = m[i]

            # make union of all chracters which
            # are meant to be same
            while (x < y):
                Union(x, y)
                x += 1
                y -= 1

        # find number of different sets formed
        ans = 0
        for i in range(1, n + 1):
            if (par[i] == i):
                ans += 1

        # return the required answer
        return power(26, ans) % mod

    # Driver Code
    n = 4

    # queries
    query(1, 3)
    query(2, 4)

    print(possiblestrings())

    # This code is contributed by Mohit Kumar
    ```

    ## C#

    ```
    // C# program to implement above approach
    using System;
    using System.Collections.Generic; 

    class GFG{

    const int N = 2005;
    const int mod = 1000000007;

    // To store the size of string and
    // number of queries
    static int n;
    //static int q;

    // To store parent and rank of ith place
    static int[]par = new int[N];
    static int[]Rank = new int[N];

    // To store maximum interval
    static Dictionary<int,
                      int> m = new Dictionary<int,
                                              int>();

    // Function for initialization
    static void initialize()
    {
        for(int i = 0; i <= n; i++)
        {
            par[i] = i;
            Rank[i] = 0;
        }
    }

    // Function to find parent
    static int find(int x)
    {
        if (par[x] != x)
            par[x] = find(par[x]);

        return par[x];
    }

    // Function to make union
    static void Union(int x, int y) 
    {
        int xpar = find(x); 
        int ypar = find(y); 

        if (Rank[xpar] < Rank[ypar]) 
            par[xpar] = ypar; 
        else if (Rank[xpar] > Rank[ypar]) 
            par[ypar] = xpar; 
        else
        { 
            par[ypar] = xpar; 
            Rank[xpar]++; 
        } 
    }

    // Power function to calculate a raised to m1
    // under modulo 10000007
    static long power(long a, long m1) 
    {
        if (m1 == 0)
            return 1;
        else if (m1 == 1)
            return a;
        else if (m1 == 2)
            return (1L * a * a) % mod;
        else if (m1 % 2 == 1)
            return (1L * a * power(
                   power(a, m1 / 2), 2)) % mod;
        else
            return power(power(a, m1 / 2), 2) % mod;
    }

    // Function to take maxmium interval
    static void query(int l, int r)
    {
        if (m.ContainsKey(l + r))
            m[l + r] = Math.Max(m[l + r], r);
        else
            m[l + r] = r;
    }

    // Function to find different possible strings
    static long possiblestrings() 
    {
        initialize();

        foreach(KeyValuePair<int, int> i in m)
        {
            int x = i.Key - m[i.Key];
            int y = m[i.Key];

            // Make union of all chracters 
            // which are meant to be same
            while (x < y) 
            {
                Union(x, y);
                x++;
                y--;
            }
        }

        // Find number of different sets formed
        int ans = 0;
        for(int i = 1; i <= n; i++)
            if (par[i] == i)
                ans++;

        // Return the required answer
        return power(26, ans) % mod;
    }

    // Driver Code
    public static void Main(string[] args) 
    {
        n = 4;

        // Queries
        query(1, 3);
        query(2, 4);

        Console.Write(possiblestrings());
    }
    }

    // This code is contributed by rutvik_56
    ```

    **Output:**

    ```
    676

    ```