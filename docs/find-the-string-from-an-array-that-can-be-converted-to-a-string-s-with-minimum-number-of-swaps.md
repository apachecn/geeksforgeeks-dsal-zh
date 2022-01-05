# 从一个数组中找出可以转换成交换次数最少的字符串 S 的字符串

> 原文:[https://www . geesforgeks . org/find-the-string-from-a-a-array-the-string-s-a-a-a-a-s-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a](https://www.geeksforgeeks.org/find-the-string-from-an-array-that-can-be-converted-to-a-string-s-with-minimum-number-of-swaps/)

给定一个长度分别为 **N** 和 **M** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** 和[字符串数组](https://www.geeksforgeeks.org/array-strings-c-3-different-ways-create/) **arr[]** ，任务是通过交换最少数量的字符从给定数组中找到字符串到字符串 **S** 。如果没有字符串可以转换为 **S** ，则打印 **-1。**

**示例:**

> **输入:**S =“abc”，arr[]= {“acb”，“XYZ”}
> **输出:** acb
> **解释:**
> 字符串“ACB”可以通过交换 1 对字符“a**CB**”->a**BC**转换为“ABC”。
> 字符串“xyz”不能转换为“abc”。
> 
> **输入:**S =“ABC”，arr[]= {“ab”，“xy”，“CB”}
> T3】输出: -1

**方法:**这个问题可以通过[从给定的字符串数组](https://www.geeksforgeeks.org/check-whether-two-strings-are-anagram-of-each-other/)中搜索 **S** 的字谜来解决，然后，对于每个这样的字符串，找到将字符串转换为 **S** 所需的最少字符互换次数。

按照以下步骤解决问题:

*   [遍历字符串数组](https://www.geeksforgeeks.org/iterating-arrays-java/)，对于数组中的每个字符串，[检查它是否是](https://www.geeksforgeeks.org/check-whether-two-strings-are-anagram-of-each-other/) **S** 的字谜。
*   如果没有找到这样的字符串，则打印 **-1** 。
*   否则，通过[迭代当前字符串的字符](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)，比如 **S1** ，找到将当前字符串转换为 **S，**所需的最小交换次数。
*   将 **S1** 中的字符位置存储在 **26** 列表中。对于 **S1** 中的每个字符，将其索引附加到其对应的列表中，即**列表 0** 存储字符**‘a’**的所有位置。同样的，**列表 1** 存储**【b】**等所有位置。
*   在完成字符串**的遍历后，S1** 、[反过来遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)、T4 的字符，对于每个字符，说**S【j】**，从给定的列表数组中获取其各自的索引，说 **temp** 。
*   现在，最佳的移动是将 **temp** 中最后一个索引处的字符移动到索引 **j** 处。这是最佳选择，因为:
    *   每个动作都在移动角色。因此，没有任何举措被浪费。
    *   由于字符串是反向迭代的，因此 **temp** 中的最后一个索引将比其他索引更接近 **j** 。
    *   为了优化，可以使用[分威克树](https://www.geeksforgeeks.org/binary-indexed-tree-or-fenwick-tree-2/)来确定字符在 **S1** 中的修改位置，以防任何互换。

插图:

> 假设，**S =“abca”，S1 =“cbaa”**
> 下面是为 S1 生成的列表:
> 列表为“a”= { 2，3}
> 列表为“b”= { 1 }
> 列表为“c”= { 0 }
> 通过用 **0 初始化**最小移动**来反过来迭代 **S** 的字符。**
> 
> 1.  **S = "abc <u>a"</u> ，i = 3**
>     从对应于**‘a’**的列表中删除最后一个索引，即 3。
>     搜索**分支树**查看分支树中该索引左侧是否有索引。
>     既然树现在是空的，就不用转移这个指标了。
>     给**芬威克树**增加索引 3。
>     最小移动+=(I–索引)=(3–3)。因此，最小运动= 0
> 2.  **S = "ab <u>c</u> a "，i = 2**
>     从列表中删除**【c】**对应的最后一个索引，即 0。
>     搜索**分支树**查看分支树中该索引左侧是否有索引。
>     由于树中唯一的索引是 3，并且在 0 的右边，所以不需要移动这个索引。
>     给**芬威克树**添加索引 0。
>     最小移动+=(I–索引)=(2–0)。因此，最小运动= 2
> 3.  **S = "a <u>b</u> ca "，i = 1**
>     从对应于**【b】**的列表中删除最后一个索引，即 1。
>     搜索**分支树**查看分支树中该索引左侧是否有索引。
>     获得的计数是 1，即索引 1 的左边有一个字符，现在是它的右边。
>     给**芬威克树**增加索引 1。
>     新索引= 1–left shit = 1–1 = 0
>     最小移动+=(I–新索引)= 1–0 = 3
> 4.  **S =<u>a</u>BCA，i= 0**
>     从对应于**‘a’**的列表中删除最后一个索引，即 2。
>     搜索**分威克树**查看分威克树中该索引左侧是否有索引。
>     获得的计数是 2，即在索引 2 的左边有两个字符，现在在它的右边。
>     给**芬威克树**添加索引 2。
>     新索引= 2–left shit = 2–2 = 0
>     最小移动+=(I-新索引)= 0–0 = 3

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check is two
// strings are anagrams
bool checkIsAnagram(vector<int> charCountS,
                    vector<int> charCountS1)
{
    for(int i = 0; i < 26; i++)
    {
        if (charCountS[i] != charCountS1[i])
            return false;
    }
    return true;
}

// Function to return the frequency of
// characters in the array of strings
vector<int> getCharCount(string S)
{
    vector<int> charCount(26, 0);

    for(char i:S)
        charCount[i - 'a']++;

    return charCount;
}

// Function to return the count of
// indices to the left of this index
int get(vector<int> &fenwickTree, int index)
{
    int leftShift = 0;
    leftShift += fenwickTree[index];

    while (index > 0)
    {
        index -= (-index) & index;
        leftShift += fenwickTree[index];
    }
    return leftShift;
}

// Update function of Fenwick Tree
void update(vector<int> &fenwickTree,
                   int index)
{
    while (index < fenwickTree.size())
    {
        fenwickTree[index]++;
        index += (-index) & index;
    }
}

// Function to get all positions of
// characters present in the string S1
vector<vector<int>> getPositions(string S)
{

    //@SuppressWarnings("unchecked")
    vector<vector<int>> charPositions(26);

    for(int i = 0; i < S.size(); i++)
        charPositions[i - 'a'].push_back(i);

    return charPositions;
}

// Function to return the minimum number
// of swaps required to convert S1 to S
int findMinMoves(string S, string S1)
{

    // cout<<"run\n";
    // Stores number of swaps
    int minMoves = 0;

    // Initialize Fenwick Tree
    vector<int> fenwickTree(S.size() + 1);

    // Get all positions of characters
    // present in the string S1
    vector<int> charPositions[26];
    int j = 0;
    for(char i:S1)
    {
        charPositions[i-'a'].push_back(j);
        j++;
    }

    // cout<<charPositions[2].size()<<endl;

    // Traverse the given string in reverse
    for(int i = S.size() - 1; i >= 0; i--)
    {

        // Get the list corresponding
        // to character S[i]
        vector<int> temp = charPositions[S[i] - 'a'];

        // Size of the list
        int size = temp.size() - 1;

        // Get and remove last
        // indices from the list
        int index = temp[size] + 1;
        charPositions[S[i] - 'a'].pop_back();

        //temp.pop_back();

        // Count of indices to
        // the left of this index
        int leftShift = get(fenwickTree, index);

        // Update Fenwick T ree
        update(fenwickTree, index);

        // Shift the index to it's left
        index -= leftShift;

        // Update moves
        minMoves += abs(i - index + 1);
    }

    // Return moves
    return minMoves;
}

// Function to find anagram of S
// requiring minimum number of swaps
string getBeststring(string S, vector<string> group)
{

    // Initialize variables
    bool isAnagram = false;
    string beststring ="";
    int minMoves = INT_MAX;

    // Count frequency of characters in S
    vector<int> charCountS = getCharCount(S);

    // Traverse the array of strings
    for(string S1 : group)
    {

        // Count frequency of characters in S1
        vector<int> charCountS1 = getCharCount(S1);

        // cout<<S1<<endl;
        // Check if S1 is anagram of S
        bool anagram = checkIsAnagram(charCountS,
                                      charCountS1);
        //cout<<anagram<<endl;

        // If not an anagram of S
        if (anagram == 0)
            continue;

        isAnagram = true;

        // Count swaps required
        // to convert S to S1
        int moves = findMinMoves(S, S1);
        //cout<<moves<<endl;

        // Count minimum number of swaps
        if (moves < minMoves)
        {
            minMoves = moves;
            beststring = S1;
        }
    }

    // If no anagram is found, print -1
    return (isAnagram) ? beststring : "-1";
}

// Driver Code
int main()
{
    // Given string
    string S = "abcdac";

    // Given array of strings
    vector<string> arr = { "cbdaca",
                           "abcacd",
                           "abcdef" };

    string beststring = getBeststring(S, arr);

    // Print answer
    cout << (beststring) << endl;
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.util.*;

class GFG {

    // Function to find anagram of S
    // requiring minimum number of swaps
    static String getBestString(String S,
                                List<String> group)
    {
        // Initialize variables
        boolean isAnagram = false;
        String bestString = null;
        int minMoves = Integer.MAX_VALUE;

        // Count frequency of characters in S
        int[] charCountS = getCharCount(S);

        // Traverse the array of strings
        for (String S1 : group) {

            // Count frequency of characters in S1
            int[] charCountS1 = getCharCount(S1);

            // Check if S1 is anagram of S
            boolean anagram
                = checkIsAnagram(charCountS,
                                 charCountS1);

            // If not an anagram of S
            if (!anagram)
                continue;

            isAnagram = true;

            // Count swaps required
            // to convert S to S1
            int moves = findMinMoves(S, S1);

            // Count minimum number of swaps
            if (moves < minMoves) {
                minMoves = moves;
                bestString = S1;
            }
        }

        // If no anagram is found, print -1
        return (isAnagram) ? bestString : "-1";
    }

    // Function to return the minimum number
    // of swaps required to convert S1 to S
    static int findMinMoves(String S, String S1)
    {

        // Stores number of swaps
        int minMoves = 0;

        // Initialize Fenwick Tree
        int[] fenwickTree = new int[S.length() + 1];

        // Get all positions of characters
        // present in the string S1
        List<List<Integer> > charPositions
            = getPositions(S1);

        // Traverse the given string in reverse
        for (int i = S.length() - 1; i >= 0; i--) {

            // Get the list corresponding
            // to character S[i]
            List<Integer> temp
                = charPositions.get(
                    S.charAt(i) - 'a');

            // Size of the list
            int size = temp.size() - 1;

            // Get and remove last
            // indices from the list
            int index = temp.remove(size) + 1;

            // Count of indices to
            // the left of this index
            int leftShift = get(
                fenwickTree, index);

            // Update Fenwick T ree
            update(fenwickTree, index);

            // Shift the index to it's left
            index -= leftShift;

            // Update moves
            minMoves += Math.abs(i - index + 1);
        }

        // Return moves
        return minMoves;
    }

    // Function to get all positions of
    // characters present in the string S1
    static List<List<Integer> > getPositions(
        String S)
    {
        @SuppressWarnings("unchecked")
        List<List<Integer> > charPositions
            = new ArrayList();

        for (int i = 0; i < 26; i++)
            charPositions.add(
                new ArrayList<Integer>());

        for (int i = 0; i < S.length(); i++)
            charPositions.get(
                             S.charAt(i) - 'a')
                .add(i);

        return charPositions;
    }

    // Update function of Fenwick Tree
    static void update(int[] fenwickTree,
                       int index)
    {
        while (index < fenwickTree.length) {
            fenwickTree[index]++;
            index += (-index) & index;
        }
    }

    // Function to return the count of
    // indices to the left of this index
    static int get(int[] fenwickTree, int index)
    {
        int leftShift = 0;
        leftShift += fenwickTree[index];

        while (index > 0) {
            index -= (-index) & index;
            leftShift += fenwickTree[index];
        }
        return leftShift;
    }

    // Function to return the frequency of
    // characters in the array of strings
    static int[] getCharCount(String S)
    {
        int[] charCount = new int[26];

        for (int i = 0; i < S.length(); i++)
            charCount[S.charAt(i) - 'a']++;

        return charCount;
    }

    // Function to check is two
    // strings are anagrams
    static boolean checkIsAnagram(
        int[] charCountS,
        int[] charCountS1)
    {

        for (int i = 0; i < 26; i++) {
            if (charCountS[i] != charCountS1[i])
                return false;
        }

        return true;
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Given string
        String S = "abcdac";

        // Given array of strings
        String arr[] = { "cbdaca",
                         "abcacd",
                         "abcdef" };

        String bestString
            = getBestString(S, Arrays.asList(arr));

        // Print answer
        System.out.println(bestString);
    }
}
```

**Output:** 

```
abcacd
```

***时间复杂度:**O(M * N * logN)*
T5**辅助空间:** O(N)