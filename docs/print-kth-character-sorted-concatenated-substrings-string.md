# 打印字符串的排序串联子串中的第 Kth 个字符

> 原文:[https://www . geeksforgeeks . org/print-kth-character-sorted-串接-substrings-string/](https://www.geeksforgeeks.org/print-kth-character-sorted-concatenated-substrings-string/)

给定一串较低的字母字符，当以排序形式连接时，在由(给定字符串的)子字符串构成的字符串中找到第 K 个字符。

**示例:**

```
Input : str = “banana”
          K = 10
Output : n
All substring in sorted form are,
"a", "an", "ana", "anan", "anana", 
"b", "ba", "ban", "bana", "banan", 
"banana", "n", "na", "nan", "nana"
Concatenated string = “aananaanana
nanabbabanbanabananbananannanannana”
We can see a 10th character in the 
above concatenated string is ‘n’ 
which is our final answer.
```

一个**简单的解决方案**是生成一个给定字符串的所有子串，并将它们存储在一个数组中。生成子字符串后，对它们进行排序，并在排序后进行连接。最后打印串联字符串中的第 K 个字符。

一个有效的解决方案是基于使用后缀数组对字符串中不同的子串进行计数的 T2 算法。同样的方法也被用于解决这个问题。在获得后缀数组和 lcp 数组之后，我们循环所有的 lcp 值，对于每个这样的值，我们计算要跳过的字符。我们不断从我们的 K 中减去这许多字符，当要跳过的字符变得大于 K 时，我们停止并循环对应于当前 lcp[i]的子字符串，其中我们从 lcp[i]循环直到字符串的最大长度，然后打印第 Kth 个字符。

## C++

```
// C++ program to print Kth character
// in sorted concatenated substrings
#include <bits/stdc++.h>
using namespace std;

// Structure to store information of a suffix
struct suffix
{
    int index;  // To store original index
    int rank[2]; // To store ranks and next
                 // rank pair
};

// A comparison function used by sort() to compare
// two suffixes. Compares two pairs, returns 1 if
// first pair is smaller
int cmp(struct suffix a, struct suffix b)
{
    return (a.rank[0] == b.rank[0])?
           (a.rank[1] < b.rank[1] ?1: 0):
           (a.rank[0] < b.rank[0] ?1: 0);
}

// This is the main function that takes a string
// 'txt' of size n as an argument, builds and return
// the suffix array for the given string
vector<int> buildSuffixArray(string txt, int n)
{
    // A structure to store suffixes and their indexes
    struct suffix suffixes[n];

    // Store suffixes and their indexes in an array
    // of structures. The structure is needed to sort
    // the suffixes alphabetically and maintain their
    // old indexes while sorting
    for (int i = 0; i < n; i++)
    {
        suffixes[i].index = i;
        suffixes[i].rank[0] = txt[i] - 'a';
        suffixes[i].rank[1] = ((i+1) < n)?
                              (txt[i + 1] - 'a'): -1;
    }

    // Sort the suffixes using the comparison function
    // defined above.
    sort(suffixes, suffixes+n, cmp);

    // At his point, all suffixes are sorted according
    // to first 2 characters.  Let us sort suffixes
    // according to first 4 characters, then first
    // 8 and so on
    int ind[n];  // This array is needed to get the
                 // index in suffixes[] from original
                 // index. This mapping is needed to get
                 // next suffix.

    for (int k = 4; k < 2*n; k = k*2)
    {
        // Assigning rank and index values to first suffix
        int rank = 0;
        int prev_rank = suffixes[0].rank[0];
        suffixes[0].rank[0] = rank;
        ind[suffixes[0].index] = 0;

        // Assigning rank to suffixes
        for (int i = 1; i < n; i++)
        {
            // If first rank and next ranks are same as
            // that of previous suffix in array, assign
            // the same new rank to this suffix
            if (suffixes[i].rank[0] == prev_rank &&
               suffixes[i].rank[1] == suffixes[i-1].rank[1])
            {
                prev_rank = suffixes[i].rank[0];
                suffixes[i].rank[0] = rank;
            }

            else // Otherwise increment rank and assign
            {
                prev_rank = suffixes[i].rank[0];
                suffixes[i].rank[0] = ++rank;
            }
            ind[suffixes[i].index] = i;
        }

        // Assign next rank to every suffix
        for (int i = 0; i < n; i++)
        {
            int nextindex = suffixes[i].index + k/2;
            suffixes[i].rank[1] = (nextindex < n)?
                      suffixes[ind[nextindex]].rank[0]: -1;
        }

        // Sort the suffixes according to first k characters
        sort(suffixes, suffixes+n, cmp);
    }

    // Store indexes of all sorted suffixes in the suffix
    // array
    vector<int>suffixArr;
    for (int i = 0; i < n; i++)
        suffixArr.push_back(suffixes[i].index);

    // Return the suffix array
    return  suffixArr;
}

/* To construct and return LCP */
vector<int> kasai(string txt, vector<int> suffixArr)
{
    int n = suffixArr.size();

    // To store LCP array
    vector<int> lcp(n, 0);

    // An auxiliary array to store inverse of suffix array
    // elements. For example if suffixArr[0] is 5, the
    // invSuff[5] would store 0.  This is used to get next
    // suffix string from suffix array.
    vector<int> invSuff(n, 0);

    // Fill values in invSuff[]
    for (int i=0; i < n; i++)
        invSuff[suffixArr[i]] = i;

    // Initialize length of previous LCP
    int k = 0;

    // Process all suffixes one by one starting from
    // first suffix in txt[]
    for (int i=0; i<n; i++)
    {
        /* If the current suffix is at n-1, then we don’t
           have next substring to consider. So lcp is not
           defined for this substring, we put zero. */
        if (invSuff[i] == n-1)
        {
            k = 0;
            continue;
        }

        /* j contains index of the next substring to
           be considered  to compare with the present
           substring, i.e., next string in suffix array */
        int j = suffixArr[invSuff[i]+1];

        // Directly start matching from k'th index as
        // at-least k-1 characters will match
        while (i+k<n && j+k<n && txt[i+k]==txt[j+k])
            k++;

        lcp[invSuff[i]] = k; // lcp for the present suffix.

        // Deleting the starting character from the string.
        if (k>0)
            k--;
    }

    // return the constructed lcp array
    return lcp;
}

//    Utility method to get sum of first N numbers
int sumOfFirstN(int N)
{
    return (N * (N + 1)) / 2;
}

// Returns Kth character in sorted concatenated
// substrings of str
char printKthCharInConcatSubstring(string str, int K)
{
    int n = str.length();
    //  calculating suffix array and lcp array
    vector<int> suffixArr = buildSuffixArray(str, n);
    vector<int> lcp = kasai(str, suffixArr);

    for (int i = 0; i < lcp.size(); i++)
     {
         //    skipping characters common to substring
         //    (n - suffixArr[i]) is length of current
         //  maximum substring lcp[i] will length of
         // common substring
        int charToSkip = sumOfFirstN(n - suffixArr[i]) -
                         sumOfFirstN(lcp[i]);

        /*    if characters are more than K, that means
            Kth character belongs to substring
            corresponding to current lcp[i]*/
        if (K <= charToSkip)
        {
            // loop from current lcp value to current
            // string length
            for (int j = lcp[i] + 1; j <= (n-suffixArr[i]); j++)
            {
                int curSubstringLen = j;

                /* Again reduce K by current substring's
                   length one by one and when it becomes less,
                    print Kth character of current substring */
                if (K <= curSubstringLen)
                    return str[(suffixArr[i] + K - 1)];
                else
                    K -= curSubstringLen;

            }
            break;
        }
        else
            K -= charToSkip;
     }
}

//    Driver code to test above methods
int main()
{
    string str = "banana";
    int K = 10;
    cout << printKthCharInConcatSubstring(str, K);
    return 0;
}
```

## 蟒蛇 3

```
# Python3 program to print Kth character
# in sorted concatenated substrings

# Structure to store information of a suffix
class suffix:

    def __init__(self):

        self.index = 0

        # To store original index
        self.rank = [0] * 2

        # To store ranks and next
        # rank pair

# This is the main function that takes a string
# 'txt' of size n as an argument, builds and return
# the suffix array for the given string
def buildSuffixArray(txt: str, n: int) -> list:

    # A structure to store suffixes
    # and their indexes
    suffixes = [0] * n
    for i in range(n):
        suffixes[i] = suffix()

    # Store suffixes and their indexes in an array
    # of structures. The structure is needed to sort
    # the suffixes alphabetically and maintain their
    # old indexes while sorting
    for i in range(n):
        suffixes[i].index = i
        suffixes[i].rank[0] = ord(txt[i]) - ord('a')
        suffixes[i].rank[1] = (ord(txt[i + 1]) -
                        ord('a')) if ((i + 1) < n) else -1

    # Sort the suffixes using the comparison function
    # defined above.
    suffixes.sort(key = lambda a: a.rank)

    # At his point, all suffixes are sorted according
    # to first 2 characters.  Let us sort suffixes
    # according to first 4 characters, then first
    # 8 and so on
    ind = [0] * n

    # This array is needed to get the
    # index in suffixes[] from original
    # index. This mapping is needed to get
    # next suffix.
    k = 4
    while k < 2 * n:
        k *= 2

        # for k in range(4, 2 * n, k * 2):

        # Assigning rank and index values
        # to first suffix
        rank = 0
        prev_rank = suffixes[0].rank[0]
        suffixes[0].rank[0] = rank
        ind[suffixes[0].index] = 0

        # Assigning rank to suffixes
        for i in range(1, n):

            # If first rank and next ranks are same as
            # that of previous suffix in array, assign
            # the same new rank to this suffix
            if (suffixes[i].rank[0] == prev_rank and
                suffixes[i].rank[1] == suffixes[i - 1].rank[1]):
                prev_rank = suffixes[i].rank[0]
                suffixes[i].rank[0] = rank

            # Otherwise increment rank and assign
            else: 
                prev_rank = suffixes[i].rank[0]
                rank += 1
                suffixes[i].rank[0] = rank

            ind[suffixes[i].index] = i

        # Assign next rank to every suffix
        for i in range(n):
            nextindex = suffixes[i].index + k // 2
            suffixes[i].rank[1] = suffixes[ind[nextindex]].rank[0] if (
                nextindex < n) else -1

        # Sort the suffixes according to first k characters
        suffixes.sort(key = lambda a : a.rank)

    # Store indexes of all sorted suffixes
    # in the suffix array
    suffixArr = []
    for i in range(n):
        suffixArr.append(suffixes[i].index)

    # Return the suffix array
    return suffixArr

# To construct and return LCP */
def kasai(txt: str, suffixArr: list) -> list:

    n = len(suffixArr)

    # To store LCP array
    lcp = [0] * n

    # An auxiliary array to store inverse of
    # suffix array elements. For example if
    # suffixArr[0] is 5, the invSuff[5] would
    # store 0.  This is used to get next
    # suffix string from suffix array.
    invSuff = [0] * n

    # Fill values in invSuff[]
    for i in range(n):
        invSuff[suffixArr[i]] = i

    # Initialize length of previous LCP
    k = 0

    # Process all suffixes one by one
    # starting from first suffix in txt[]
    for i in range(n):

        # If the current suffix is at n-1, then
        # we don’t have next substring to
        # consider. So lcp is not defined for
        # this substring, we put zero.
        if (invSuff[i] == n - 1):
            k = 0
            continue

        # j contains index of the next substring to
        # be considered  to compare with the present
        # substring, i.e., next string in suffix array
        j = suffixArr[invSuff[i] + 1]

        # Directly start matching from k'th index as
        # at-least k-1 characters will match
        while (i + k < n and j + k < n and
           txt[i + k] == txt[j + k]):
            k += 1

        lcp[invSuff[i]] = k
        # lcp for the present suffix.

        # Deleting the starting character
        # from the string.
        if (k > 0):
            k -= 1

    # Return the constructed lcp array
    return lcp

# Utility method to get sum of first N numbers
def sumOfFirstN(N: int) -> int:

    return (N * (N + 1)) // 2

# Returns Kth character in sorted concatenated
# substrings of str
def printKthCharInConcatSubstring(string: str,
                               K: int) -> str:

    n = len(string)

    # Calculating suffix array and lcp array
    suffixArr = buildSuffixArray(string, n)
    lcp = kasai(string, suffixArr)

    for i in range(len(lcp)):

        # Skipping characters common to substring
        # (n - suffixArr[i]) is length of current
        # maximum substring lcp[i] will length of
        # common substring
        charToSkip = (sumOfFirstN(n - suffixArr[i]) -
                                sumOfFirstN(lcp[i]))

        # If characters are more than K, that means
        # Kth character belongs to substring
        # corresponding to current lcp[i]
        if (K <= charToSkip):

            # Loop from current lcp value to current
            # string length
            for j in range(lcp[i] + 1,
               (n - suffixArr[i]) + 1):
                curSubstringLen = j

                # Again reduce K by current substring's
                # length one by one and when it becomes less,
                # print Kth character of current substring
                if (K <= curSubstringLen):
                    return string[(suffixArr[i] + K - 1)]
                else:
                    K -= curSubstringLen

            break

        else:
            K -= charToSkip

# Driver code
if __name__ == "__main__":

    string = "banana"
    K = 10

    print(printKthCharInConcatSubstring(string, K))

# This code is contributed by sanjeev2552
```

**输出:**

```
n
```

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。