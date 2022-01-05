# 稳定婚姻问题

> 原文:[https://www.geeksforgeeks.org/stable-marriage-problem/](https://www.geeksforgeeks.org/stable-marriage-problem/)

《稳定婚姻问题》指出，给定 N 名男性和 N 名女性，其中每个人都按照偏好的顺序排列了所有异性，将男性和女性结合在一起，这样就不会有两个异性都宁愿拥有对方而不是他们现在的伴侣。如果没有这样的人，所有的婚姻都是“稳定”的(来源 [Wiki](http://en.wikipedia.org/wiki/Stable_marriage_problem) )。

考虑下面的例子。
让两个男的 m1 和 m2 和两个女的 w1 和 w2 。
让 m1 的首选项列表为{ w1 、 w2 }
让 m2 的首选项列表为{ w1 、 w2 }
让 w1 的首选项列表为{ m1 、 m2 } m2 }
匹配的{ { m1 、 w2 }、{ w1 、 m2 } }并不稳定，因为 m1 和 w1 会更喜欢对方而不是他们指定的伴侣。 匹配的{ m1 、 w1 }和{ m2 、 w2 }是稳定的，因为没有两个异性会比他们指定的伴侣更喜欢对方。

从偏好列表中形成稳定的婚姻总是可能的(见参考文献的证明)。下面是**盖尔-沙普利算法**来寻找一个稳定的匹配:
这个想法是在有任何自由人可用的时候遍历所有自由人。每个自由的男人都会按照顺序去找他偏爱的所有女人。对于他去找的每个女人，他都会检查这个女人是否有空，如果有，他们就会订婚。如果女方没有空，那么女方选择要么拒绝他，要么根据自己的偏好清单放弃目前的婚约。所以，如果一个女人有更好的选择，一次订婚就可能被打破。盖尔-沙普利算法的时间复杂度为 O(n <sup>2</sup> )。

以下是[维基](http://en.wikipedia.org/wiki/Stable_marriage_problem)的完整算法

```
Initialize all men and women to free
while there exist a free man m who still has a woman w to propose to 
{
    w = m's highest ranked such woman to whom he has not yet proposed
    if w is free
       (m, w) become engaged
    else some pair (m', w) already exists
       if w prefers m to m'
          (m, w) become engaged
           m' becomes free
       else
          (m', w) remain engaged    
}
```

**输入&输出:**输入是一个大小为(2*N)*N 的 2D 矩阵，其中 N 是女性或男性的数量。从 0 到 N-1 的行代表男性偏好列表，从 N 到 2 * N-1 的行代表女性偏好列表。所以男人从 0 到 N-1，女人从 N 到 2 * N-1。输出是已婚夫妇列表。

下面是上述算法的实现。

## C++

```
// C++ program for stable marriage problem
#include <iostream>
#include <string.h>
#include <stdio.h>
using namespace std;

// Number of Men or Women
#define N  4

// This function returns true if woman 'w' prefers man 'm1' over man 'm'
bool wPrefersM1OverM(int prefer[2*N][N], int w, int m, int m1)
{
    // Check if w prefers m over her current engagment m1
    for (int i = 0; i < N; i++)
    {
        // If m1 comes before m in list of w, then w prefers her
        // current engagement, don't do anything
        if (prefer[w][i] == m1)
            return true;

        // If m comes before m1 in w's list, then free her current
        // engagement and engage her with m
        if (prefer[w][i] == m)
           return false;
    }
}

// Prints stable matching for N boys and N girls. Boys are numbered as 0 to
// N-1\. Girls are numbered as N to 2N-1.
void stableMarriage(int prefer[2*N][N])
{
    // Stores partner of women. This is our output array that
    // stores passing information.  The value of wPartner[i]
    // indicates the partner assigned to woman N+i.  Note that
    // the woman numbers between N and 2*N-1\. The value -1
    // indicates that (N+i)'th woman is free
    int wPartner[N];

    // An array to store availability of men.  If mFree[i] is
    // false, then man 'i' is free, otherwise engaged.
    bool mFree[N];

    // Initialize all men and women as free
    memset(wPartner, -1, sizeof(wPartner));
    memset(mFree, false, sizeof(mFree));
    int freeCount = N;

    // While there are free men
    while (freeCount > 0)
    {
        // Pick the first free man (we could pick any)
        int m;
        for (m = 0; m < N; m++)
            if (mFree[m] == false)
                break;

        // One by one go to all women according to m's preferences.
        // Here m is the picked free man
        for (int i = 0; i < N && mFree[m] == false; i++)
        {
            int w = prefer[m][i];

            // The woman of preference is free, w and m become
            // partners (Note that the partnership maybe changed
            // later). So we can say they are engaged not married
            if (wPartner[w-N] == -1)
            {
                wPartner[w-N] = m;
                mFree[m] = true;
                freeCount--;
            }

            else  // If w is not free
            {
                // Find current engagement of w
                int m1 = wPartner[w-N];

                // If w prefers m over her current engagement m1,
                // then break the engagement between w and m1 and
                // engage m with w.
                if (wPrefersM1OverM(prefer, w, m, m1) == false)
                {
                    wPartner[w-N] = m;
                    mFree[m] = true;
                    mFree[m1] = false;
                }
            } // End of Else
        } // End of the for loop that goes to all women in m's list
    } // End of main while loop

    // Print the solution
    cout << "Woman   Man" << endl;
    for (int i = 0; i < N; i++)
       cout << " " << i+N << "\t" << wPartner[i] << endl;
}

// Driver program to test above functions
int main()
{
    int prefer[2*N][N] = { {7, 5, 6, 4},
        {5, 4, 6, 7},
        {4, 5, 6, 7},
        {4, 5, 6, 7},
        {0, 1, 2, 3},
        {0, 1, 2, 3},
        {0, 1, 2, 3},
        {0, 1, 2, 3},
    };
    stableMarriage(prefer);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for stable marriage problem
import java.util.*;

class GFG
{

// Number of Men or Women
static int N = 4;

// This function returns true if woman
// 'w' prefers man 'm1' over man 'm'
static boolean wPrefersM1OverM(int prefer[][], int w,
                               int m, int m1)
{
    // Check if w prefers m over
    // her current engagment m1
    for (int i = 0; i < N; i++)
    {
        // If m1 comes before m in list of w,
        // then w prefers her current engagement,
        // don't do anything
        if (prefer[w][i] == m1)
            return true;

        // If m comes before m1 in w's list,
        // then free her current engagement
        // and engage her with m
        if (prefer[w][i] == m)
        return false;
    }
    return false;
}

// Prints stable matching for N boys and
// N girls. Boys are numbered as 0 to
// N-1\. Girls are numbered as N to 2N-1.
static void stableMarriage(int prefer[][])
{
    // Stores partner of women. This is our
    // output array that stores passing information.
    // The value of wPartner[i] indicates the partner
    // assigned to woman N+i. Note that the woman
    // numbers between N and 2*N-1\. The value -1
    // indicates that (N+i)'th woman is free
    int wPartner[] = new int[N];

    // An array to store availability of men.
    // If mFree[i] is false, then man 'i' is
    // free, otherwise engaged.
    boolean mFree[] = new boolean[N];

    // Initialize all men and women as free
    Arrays.fill(wPartner, -1);
    int freeCount = N;

    // While there are free men
    while (freeCount > 0)
    {
        // Pick the first free man
        // (we could pick any)
        int m;
        for (m = 0; m < N; m++)
            if (mFree[m] == false)
                break;

        // One by one go to all women
        // according to m's preferences.
        // Here m is the picked free man
        for (int i = 0; i < N &&
                        mFree[m] == false; i++)
        {
            int w = prefer[m][i];

            // The woman of preference is free,
            // w and m become partners (Note that
            // the partnership maybe changed later).
            // So we can say they are engaged not married
            if (wPartner[w - N] == -1)
            {
                wPartner[w - N] = m;
                mFree[m] = true;
                freeCount--;
            }

            else // If w is not free
            {
                // Find current engagement of w
                int m1 = wPartner[w - N];

                // If w prefers m over her current engagement m1,
                // then break the engagement between w and m1 and
                // engage m with w.
                if (wPrefersM1OverM(prefer, w, m, m1) == false)
                {
                    wPartner[w - N] = m;
                    mFree[m] = true;
                    mFree[m1] = false;
                }
            } // End of Else
        } // End of the for loop that goes
          // to all women in m's list
    } // End of main while loop

// Print the solution
System.out.println("Woman Man");
for (int i = 0; i < N; i++)
{
    System.out.print(" ");
    System.out.println(i + N + "     " +
                           wPartner[i]);
}
}

// Driver Code
public static void main(String[] args)
{
    int prefer[][] = new int[][]{{7, 5, 6, 4},
                                 {5, 4, 6, 7},
                                 {4, 5, 6, 7},
                                 {4, 5, 6, 7},
                                 {0, 1, 2, 3},
                                 {0, 1, 2, 3},
                                 {0, 1, 2, 3},
                                 {0, 1, 2, 3}};
    stableMarriage(prefer);
}
}

// This code is contributed by Prerna Saini
```

## 蟒蛇 3

```
# Python3 program for stable marriage problem

# Number of Men or Women
N = 4

# This function returns true if
# woman 'w' prefers man 'm1' over man 'm'
def wPrefersM1OverM(prefer, w, m, m1):

    # Check if w prefers m over her
    # current engagment m1
    for i in range(N):

        # If m1 comes before m in list of w,
        # then w prefers her current engagement,
        # don't do anything
        if (prefer[w][i] == m1):
            return True

        # If m comes before m1 in w's list,
        # then free her current engagement
        # and engage her with m
        if (prefer[w][i] == m):
            return False

# Prints stable matching for N boys and N girls.
# Boys are numbered as 0 to N-1.
# Girls are numbered as N to 2N-1.
def stableMarriage(prefer):

    # Stores partner of women. This is our output
    # array that stores passing information.
    # The value of wPartner[i] indicates the partner
    # assigned to woman N+i. Note that the woman numbers
    # between N and 2*N-1\. The value -1 indicates
    # that (N+i)'th woman is free
    wPartner = [-1 for i in range(N)]

    # An array to store availability of men.
    # If mFree[i] is false, then man 'i' is free,
    # otherwise engaged.
    mFree = [False for i in range(N)]

    freeCount = N

    # While there are free men
    while (freeCount > 0):

        # Pick the first free man (we could pick any)
        m = 0
        while (m < N):
            if (mFree[m] == False):
                break
            m += 1

        # One by one go to all women according to
        # m's preferences. Here m is the picked free man
        i = 0
        while i < N and mFree[m] == False:
            w = prefer[m][i]

            # The woman of preference is free,
            # w and m become partners (Note that
            # the partnership maybe changed later).
            # So we can say they are engaged not married
            if (wPartner[w - N] == -1):
                wPartner[w - N] = m
                mFree[m] = True
                freeCount -= 1

            else:

                # If w is not free
                # Find current engagement of w
                m1 = wPartner[w - N]

                # If w prefers m over her current engagement m1,
                # then break the engagement between w and m1 and
                # engage m with w.
                if (wPrefersM1OverM(prefer, w, m, m1) == False):
                    wPartner[w - N] = m
                    mFree[m] = True
                    mFree[m1] = False
            i += 1

            # End of Else
        # End of the for loop that goes
        # to all women in m's list
    # End of main while loop

    # Print solution
    print("Woman ", " Man")
    for i in range(N):
        print(i + N, "\t", wPartner[i])

# Driver Code
prefer = [[7, 5, 6, 4], [5, 4, 6, 7],
          [4, 5, 6, 7], [4, 5, 6, 7],
          [0, 1, 2, 3], [0, 1, 2, 3],
          [0, 1, 2, 3], [0, 1, 2, 3]]

stableMarriage(prefer)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program for stable marriage problem
using System;
using System.Collections.Generic;

class GFG
{

// Number of Men or Women
static int N = 4;

// This function returns true if woman
// 'w' prefers man 'm1' over man 'm'
static bool wPrefersM1OverM(int [,]prefer, int w,
                            int m, int m1)
{
    // Check if w prefers m over
    // her current engagment m1
    for (int i = 0; i < N; i++)
    {
        // If m1 comes before m in list of w,
        // then w prefers her current engagement,
        // don't do anything
        if (prefer[w, i] == m1)
            return true;

        // If m comes before m1 in w's list,
        // then free her current engagement
        // and engage her with m
        if (prefer[w, i] == m)
        return false;
    }
    return false;
}

// Prints stable matching for N boys and
// N girls. Boys are numbered as 0 to
// N-1\. Girls are numbered as N to 2N-1.
static void stableMarriage(int [,]prefer)
{
    // Stores partner of women. This is our
    // output array that stores passing information.
    // The value of wPartner[i] indicates the partner
    // assigned to woman N+i. Note that the woman
    // numbers between N and 2*N-1\. The value -1
    // indicates that (N+i)'th woman is free
    int []wPartner = new int[N];

    // An array to store availability of men.
    // If mFree[i] is false, then man 'i' is
    // free, otherwise engaged.
    bool []mFree = new bool[N];

    // Initialize all men and women as free
    for (int i = 0; i < N; i++)
        wPartner[i] = -1;
    int freeCount = N;

    // While there are free men
    while (freeCount > 0)
    {
        // Pick the first free man
        // (we could pick any)
        int m;
        for (m = 0; m < N; m++)
            if (mFree[m] == false)
                break;

        // One by one go to all women
        // according to m's preferences.
        // Here m is the picked free man
        for (int i = 0; i < N &&
                        mFree[m] == false; i++)
        {
            int w = prefer[m,i];

            // The woman of preference is free,
            // w and m become partners (Note that
            // the partnership maybe changed later).
            // So we can say they are engaged not married
            if (wPartner[w - N] == -1)
            {
                wPartner[w - N] = m;
                mFree[m] = true;
                freeCount--;
            }

            else // If w is not free
            {
                // Find current engagement of w
                int m1 = wPartner[w - N];

                // If w prefers m over her current engagement m1,
                // then break the engagement between w and m1 and
                // engage m with w.
                if (wPrefersM1OverM(prefer, w, m, m1) == false)
                {
                    wPartner[w - N] = m;
                    mFree[m] = true;
                    mFree[m1] = false;
                }
            } // End of Else
        } // End of the for loop that goes
         // to all women in m's list
    } // End of main while loop

    // Print the solution
    Console.WriteLine("Woman Man");
    for (int i = 0; i < N; i++)
    {
        Console.Write(" ");
        Console.WriteLine(i + N + "     " +
                              wPartner[i]);
    }
}

// Driver Code
public static void Main(String[] args)
{
    int [,]prefer = new int[,]{{7, 5, 6, 4},
                               {5, 4, 6, 7},
                               {4, 5, 6, 7},
                               {4, 5, 6, 7},
                               {0, 1, 2, 3},
                               {0, 1, 2, 3},
                               {0, 1, 2, 3},
                               {0, 1, 2, 3}};
    stableMarriage(prefer);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript program for stable marriage problem

// Number of Men or Women
N = 4;

// This function returns true if woman 'w' prefers man 'm1' over man 'm'
function wPrefersM1OverM( prefer,  w,  m,  m1)
{

    // Check if w prefers m over her current engagment m1
    for (var i = 0; i < N; i++)
    {

        // If m1 comes before m in list of w, then w prefers her
        // current engagement, don't do anything
        if (prefer[w][i] == m1)
            return true;

        // If m comes before m1 in w's list, then free her current
        // engagement and engage her with m
        if (prefer[w][i] == m)
           return false;
    }
}

// Prints stable matching for N boys and N girls. Boys are numbered as 0 to
// N-1\. Girls are numbered as N to 2N-1.
function stableMarriage( prefer)
{

    // Stores partner of women. This is our output array that
    // stores passing information.  The value of wPartner[i]
    // indicates the partner assigned to woman N+i.  Note that
    // the woman numbers between N and 2*N-1\. The value -1
    // indicates that (N+i)'th woman is free
    var wPartner = new Array(N);

    // An array to store availability of men.  If mFree[i] is
    // false, then man 'i' is free, otherwise engaged.
     mFree = new Array(N);

    // Initialize all men and women as free
    wPartner.fill(-1);
    mFree.fill(false);
    var freeCount = N;

    // While there are free men
    while (freeCount > 0)
    {
        // Pick the first free man (we could pick any)
        var m;
        for (m = 0; m < N; m++)
            if (mFree[m] == false)
                break;

        // One by one go to all women according to m's preferences.
        // Here m is the picked free man
        for (var i = 0; i < N && mFree[m] == false; i++)
        {
            var w = prefer[m][i];

            // The woman of preference is free, w and m become
            // partners (Note that the partnership maybe changed
            // later). So we can say they are engaged not married
            if (wPartner[w-N] == -1)
            {
                wPartner[w-N] = m;
                mFree[m] = true;
                freeCount--;
            }

            else  // If w is not free
            {

                // Find current engagement of w
                var m1 = wPartner[w-N];

                // If w prefers m over her current engagement m1,
                // then break the engagement between w and m1 and
                // engage m with w.
                if (wPrefersM1OverM(prefer, w, m, m1) == false)
                {
                    wPartner[w-N] = m;
                    mFree[m] = true;
                    mFree[m1] = false;
                }
            } // End of Else
        } // End of the for loop that goes to all women in m's list
    } // End of main while loop

    // Print the solution
     document.write("Woman      Man" +"<br>");
    for (var i = 0; i < N; i++)
      document.write(" " + (i+N) + "     " + wPartner[i] +"<br>");
}

var prefer  = [ [7, 5, 6, 4],
        [5, 4, 6, 7],
        [4, 5, 6, 7],
        [4, 5, 6, 7],
        [0, 1, 2, 3],
        [0, 1, 2, 3],
        [0, 1, 2, 3],
        [0, 1, 2, 3],
    ];
    stableMarriage(prefer);

// This code is contributed by SoumikMondal
</script>
```

**输出:**

```
Woman   Man
 4      2
 5      1
 6      3
 7      0

```

**参考文献:**
[http://www . csee . wvu . edu/~ ksmani/courses/fa01/random/lecnotes/讲师 5 . pdf](http://www.csee.wvu.edu/~ksmani/courses/fa01/random/lecnotes/lecture5.pdf)
[http://www.youtube.com/watch?v=5RSMLgy06Ew#t=11m4s](http://www.youtube.com/watch?v=5RSMLgy06Ew#t=11m4s)
如发现有不正确的地方，请写评论，或者想分享更多以上讨论话题的信息