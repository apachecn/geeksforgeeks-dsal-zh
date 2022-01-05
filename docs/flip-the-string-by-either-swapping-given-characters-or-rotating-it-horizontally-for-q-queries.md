# 通过交换给定的字符或水平旋转字符串来翻转字符串进行 Q 查询

> 原文:[https://www . geeksforgeeks . org/通过交换给定字符或水平旋转来翻转字符串以进行 q 查询/](https://www.geeksforgeeks.org/flip-the-string-by-either-swapping-given-characters-or-rotating-it-horizontally-for-q-queries/)

给定一个长度为 **2N** 和**的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，Q 查询**包含三个整数 **T** 、 **A** 和 **B** ，其中查询可以是以下两种类型:

*   T=1:交换 **S.** 中的 **Ath** 和 **Bth** 字符(在基于 1 的索引中)
*   T=2:将第一个 **N** 字符与最后一个 **N** 字符交换，即“ABCD”变成“CDAB”

任务是在对其应用 **Q 查询**后找到最终字符串。

**示例:**

> **输入:**S =【ABCD】，N=2，Q={{2，0，0}，{1，1，3}，{2，0，0}}
> **输出:**
> CBAD
> T7】解释:
> 第 1 次查询后:S =【CDAB】
> 第 2 次查询后:S =【ADCB】
> 第 3 次查询后:S =【CBAD】
> 
> **输入:** S="GEEK "，N=2，Q={{2，0，0}，{1，1，2}，{1，2，3}，{1，3，4}，{2，0，0 } }
> T3】输出:T5】EEKG

**天真方法:**按照以下步骤解决问题:

1.  遍历**查询**数组，对于每个当前索引 **i** ，执行以下操作:
    1.  提取 **T** 、 **A** 和 **B** 为 **T=Q[i][0]，A=Q[i][1]** 和 **B=Q[i][2]。**
    2.  递减 **A** 和 **B** 使它们都被 0 索引。
    3.  如果 **T** 等于 **1** ，[分别交换](https://www.geeksforgeeks.org/vectorat-vectorswap-c-stl/)索引 **A** 和 **B** 处的字符。
    4.  否则，从 **0** 到 **N-1** 遍历字符串，并用**A【j+N】交换每个**A【j】**。**
2.  [打印字符串](https://www.geeksforgeeks.org/strings-in-c-2/) **S**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find final string
// after applying all Queries on it
void solve(string S, int N,
           vector<vector<int> > Queries,
           int Q)
{
    // Traverse the Queries array
    for (int i = 0; i < Q; i++) {
        int T = Queries[i][0], A = Queries[i][1],
            B = Queries[i][2];
        // convert A, B to zero indexing
        A--;
        B--;
        // Query of 1st type
        if (T == 1) {
            // swap ath and bth characters
            swap(S[A], S[B]);
        }
        // Query of 2nd type
        else {
            // swap first N characters
            // with last N characters
            for (int j = 0; j < N; j++) {
                swap(S[j], S[j + N]);
            }
        }
    }
    // Print answer
    cout << S << endl;
}
// Driver code
int main()
{
    // Input
    string S = "ABCD";
    int N = S.length() / 2;
    vector<vector<int> > Queries
        = { { 2, 0, 0 }, { 1, 1, 3 }, { 2, 0, 0 } };
    int Q = Queries.size();

    // Function call
    solve(S, N, Queries, Q);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find final string
# after applying all Queries on it
def solve(S, N, Queries, Q):

    # Traverse the Queries array
    S = list(S)
    for i in range(Q):
        T = Queries[i][0]
        A = Queries[i][1]
        B = Queries[i][2]

        # Convert A, B to zero indexing
        A -= 1
        B -= 1

        # Query of 1st type
        if (T == 1):

            # Swap ath and bth characters
            temp = S[A]
            S[A] = S[B]
            S[B] = temp

        # Query of 2nd type
        else:

            # Swap first N characters
            # with last N characters
            for j in range(N):
                temp = S[j]
                S[j] = S[j + N]
                S[j + N] = temp

    S = ''.join(S)

    # Print answer
    print(S)

# Driver code
if __name__ == '__main__':

    # Input
    S = "ABCD"
    N = len(S) // 2
    Queries = [ [ 2, 0, 0 ],
                [ 1, 1, 3 ],
                [ 2, 0, 0 ] ]
    Q = len(Queries)

    # Function call
    solve(S, N, Queries, Q)

# This code is contributed by ipg2016107
```

**Output**

```
CBAD
```

***时间复杂度:** O(N*Q)*
***辅助空间:** O(1)*

**高效方法:**对于类型 2 的每个查询，不需要实际上用最后一个**字符替换第一个 **N** 字符。通过在一个单独的变量中记录完成的次数，可以在最后完成一次。按照以下步骤解决问题:**

1.  初始化一个变量**将**翻转到 **0** ，它会记录在 **S** 上执行类型 2 查询的次数。
2.  遍历**查询**数组，对于每个当前索引 **i** ，执行以下操作:
    1.  提取 **T** 、 **A** 和 **B** 为 **T=Q[i][0]，A=Q[i][1]** 和 **B=Q[i][2]。**
    2.  递减 **A** 和 **B** 使它们都被 0 索引。
    3.  如果 **T** 等于 **1** ，请执行以下操作:
        1.  检查**翻转**是否均匀。如果是，只需[将 **S** 中的 **Ath** 和 **Bth** 字符互换即可](https://www.geeksforgeeks.org/vectorat-vectorswap-c-stl/)
        2.  否则，相应地更新 **A** 和 **B** 的值(当琴弦翻转时)，方法是将 **N** 加到它们上面，然后用 **2N** 取它们的模量。然后[交换 **S** 中的 **Ath** 和 **Bth** 字符。](https://www.geeksforgeeks.org/vectorat-vectorswap-c-stl/)
    4.  否则，增加**翻转**
3.  检查**翻转**是否均匀。如果是，按原样打印 **S** 。
4.  否则 **S** 翻转，先打印 **S** 的最后 **N** 字符，再打印 **S** 的第一个 **N** 字符。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find final string
// after applying all Queries on it
void solve(string S, int N,
           vector<vector<int> > Queries,
           int Q)
{
    int flip = 0;
    // Traverse the Queries array
    for (int i = 0; i < Q; i++) {
        int T = Queries[i][0], A = Queries[i][1],
            B = Queries[i][2];
        // convert A, B to zero indexing
        A--;
        B--;
        // Query of 1st type
        if (T == 1) {
            // simply swap the character at
            // Ath and Bth index
            if (flip % 2 == 0)
                swap(S[A], S[B]);
            else {
                // add N to A, B as string starts at nth
                // index(0 indexing) and take mod with size
                // of string (2*N) and swap the character at
                // Ath and Bth index calculated.
                A = (A + N) % (2 * N);
                B = (B + N) % (2 * N);
                swap(S[A], S[B]);
            }
        }
        // Query of 2nd type
        else {
            // increment flip
            flip++;
        }
    }
    // Print answer
    if (flip % 2 == 0)
        cout << S << endl;
    else {
        // string starts at Nth index;
        for (int i = N; i < 2 * N; i++)
            cout << S[i];
        for (int i = 0; i < N; i++)
            cout << S[i];
        cout << endl;
    }
}
// Driver code
int main()
{
    // Input
    string S = "ABCD";
    int N = S.length() / 2;
    vector<vector<int> > Queries
        = { { 2, 0, 0 }, { 1, 1, 3 }, { 2, 0, 0 } };
    int Q = Queries.size();

    // Function call
    solve(S, N, Queries, Q);

    return 0;
}
```

**Output**

```
CBAD
```

***时间复杂度:** O(N+Q)*
***辅助空间:** O(1)*