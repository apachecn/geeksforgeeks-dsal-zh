# 稳定婚姻问题

> 原文： [https://www.geeksforgeeks.org/stable-marriage-problem/](https://www.geeksforgeeks.org/stable-marriage-problem/)

稳定婚姻问题指出，给定 N 个男人和 N 个女人（每个人都按偏好对所有异性进行排名），将这些男人和女人结婚在一起，这样就不会有两个异性会 双方宁愿彼此之间，而不是当前的伙伴。 如果没有这样的人，那么所有婚姻都是“稳定的”（来源 [Wiki](http://en.wikipedia.org/wiki/Stable_marriage_problem) ）。

考虑以下示例。

假设有两个男人 m1 和 m2 ，两个女人 w1 和 w2 。
令 m1 的偏好列表为{ w1 ， w2 }
令 m2 的偏好列表 设为{ w1 ， w2 }
令 w1 的首选项列表为{ m1 ， m2 }
令 w2 的首选项列表为{ m1 ， m2 }

匹配{{ m1 ， w2 }，{ w1 ， m2 }}不稳定，因为 m1 和 w1 会比彼此分配的伙伴更喜欢对方。 {{HTG12] m1 ， w1 }和{ m2 ， w2 }的匹配是稳定的，因为没有两个异性会 彼此更喜欢彼此分配的伙伴。

始终可以从偏好列表中形成稳定的婚姻（请参阅参考资料以获取证明）。 以下是 **Gale-Shapley 算法**，用于找到稳定的匹配项：
的想法是在所有自由人可用的情况下迭代所有自由人。 每个自由男人都会按照顺序去选择其偏好列表中的所有女人。 对于他去的每个女人，他都会检查这个女人是否有空，如果有，他们都会订婚。 如果该妇女不是自由的，则该妇女选择对他说不，或根据她的偏好列表放弃当前的婚约。 因此，如果女人有更好的选择，一次就无法进行订婚。 Gale-Shapley 算法的时间复杂度为 O（n <sup>2</sup> ）。
以下是 [Wiki](http://en.wikipedia.org/wiki/Stable_marriage_problem) 中的完整算法

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

**输入&输出：**输入是大小为（2 * N）* N 的 2D 矩阵，其中 N 为男女人数。 从 0 到 N-1 的行代表男性的偏好列表，从 N 到 2 * N – 1 的行代表女性的偏好列表。 因此，男性的编号从 0 到 N-1，女性的编号从 N 到 2 * N –1。输出是已婚夫妇的列表。

以下是上述算法的实现。

## C ++

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
        // If m1 comes before m in lisr of w, then w prefers her 
        // cirrent engagement, don't do anything 
        if (prefer[w][i] == m1) 
            return true; 

        // If m cmes before m1 in w's list, then free her current 
        // engagement and engage her with m 
        if (prefer[w][i] == m) 
           return false; 
    } 
} 

// Prints stable matching for N boys and N girls. Boys are numbered as 0 to 
// N-1\. Girls are numbereed as N to 2N-1\. 
void stableMarriage(int prefer[2*N][N]) 
{ 
    // Stores partner of women. This is our output array that 
    // stores paing information.  The value of wPartner[i] 
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