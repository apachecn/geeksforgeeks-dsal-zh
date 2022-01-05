# 找到串(S)中子串的起始索引，串(S)是通过连接列表(L)中的所有单词而形成的

> 原文:[https://www . geesforgeks . org/find-start-indexs-substrings-string-s-maked-concating-words-listl/](https://www.geeksforgeeks.org/find-starting-indices-substrings-string-s-made-concatenating-words-listl/)

给你一个字符串 *S* ，一个单词列表 *L* 即字符串的数组/向量(列表 L 中的单词都是一样长的)。找到字符串 S 中子字符串的起始索引，它包含列表 l 中的所有单词。

列表 L 的单词出现在字符串 S 内部的顺序无关紧要，即如果字符串 S 是“barfooapplefoobar”，而单词列表(L)是[“foo”、“bar”]，那么我们必须在字符串 S 中寻找子字符串“foobar”、“barfoo”

注意:**列表 L 里面的单词可以重复。**

**示例:**

```
Input : S: "barfoothefoobarman" 
        L: ["foo", "bar"]                     
Output : 0 9
Explanation : 
// at index 0 : barfoo
// at index 9 : foobar 

Input : S: "catbatatecatatebat"
        L: ["cat", "ate", "bat"] 
Output : 0 3 9
Explanation : 
// at index 0 : catbatate
// at index 3 : batatecat
// at index 9 : catatebat    

Input : S : "abcdababcd"
        L : ["ab", "ab", "cd"]
Output : 0 2 4 
Explanation :
// at index 0 : abcdab
// at index 2 : cdabab
// at index 4 : ababcd

Input : S : "abcdababcd"
        L : ["ab", "ab"]
Output : 4
```

**方法:**
我们可以使用哈希技术来解决上述问题。让我们看看步骤:

1.  声明一个映射( **hash_map** )，该映射存储列表 L 中所有与它们在列表 L 中的出现相对应的单词
2.  遍历字符串 S 中所有可能的子字符串，这些子字符串等于 size_L(如果列表 L 中的所有单词连接在一起，则产生的字符总数)。
3.  为每个可能的子串创建一个临时映射( **temp_hash_map** )并用原始映射( **hash_map** )初始化它。
4.  从子串中提取单词，如果单词出现在 temp_hash_map 中，我们就减少它的相应计数，如果它不出现在 temp_hash_map 中，我们就简单地中断。
5.  在遍历子串之后，我们遍历 temp_hash_map 并寻找其计数大于 0 的任何键。如果我们没有找到这样的关键字，这意味着列表 L 中的所有单词都是在子串中找到的，并且存储子串的给定起始索引，如果我们找到一个其计数> 0 的关键字，这意味着我们没有遍历整个子串，因为我们遇到了一个不在 temp_hash_map 中的单词。

以下是上述方法的实现:

## C++

```
// CPP program to calculate the starting indices
// of substrings inside S which contains all the
// words present in List L.
#include <bits/stdc++.h>
using namespace std;

// Returns an integer vector consisting of starting
// indices of substrings present inside the string S
vector<int> findSubstringIndices(string S, 
                            const vector<string>& L)
{

    // Number of a characters of a word in list L.
    int size_word = L[0].size();

    // Number of words present inside list L.
    int word_count = L.size();

    // Total characters present in list L.
    int size_L = size_word * word_count;

    // Resultant vector which stores indices.
    vector<int> res;

    // If the total number of characters in list L
    // is more than length of string S itself.
    if (size_L > S.size())
        return res;

    // Map stores the words present in list L
    // against it's occurrences inside list L
    unordered_map<string, int> hash_map;

    for (int i = 0; i < word_count; i++) 
        hash_map[L[i]]++;    

    for (int i = 0; i <= S.size() - size_L; i++) {
        unordered_map<string, int> temp_hash_map(hash_map);

        int j = i,count=word_count;

        // Traverse the substring
        while (j < i + size_L) {

            // Extract the word
            string word = S.substr(j, size_word);

            // If word not found or if frequency of current word is more than required simply break.
            if (hash_map.find(word) == hash_map.end()||temp_hash_map[word]==0)
                break;

            // Else decrement the count of word from hash_map
            else
               { temp_hash_map[word]--;count--;} 

            j += size_word;
        }

        // Store the starting index of that substring when all the words in the list are in substring
        if (count == 0)
            res.push_back(i);
    }

    return res;
}

// Driver Code
int main()
{
    string S = "barfoothefoobarman";
    vector<string> L = { "foo", "bar" };
    vector<int> indices = findSubstringIndices(S, L);
    for (int i = 0; i < indices.size(); i++)
        cout << indices[i] << " ";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate the starting indices
// of substrings inside S which contains all the
// words present in List L.
import java.util.ArrayList;
import java.util.Arrays;
import java.util.HashMap;
import java.util.List;

class GFG 
{
    public static ArrayList<Integer> 
    findSubstring(String A, final List<String> B) 
    {

        // Number of a characters of a word in list L.
        int size_word = B.get(0).length();

        // Number of words present inside list L. 
        int word_count = B.size();

        // Total characters present in list L.
        int size_l = size_word * word_count;

        // Resultant vector which stores indices.
        ArrayList<Integer> res = new ArrayList<Integer>();
        int n = A.length();

        // If the total number of characters in list L 
        // is more than length of string S itself.
        if (size_l > n) 
        {
            return res;
        }

        // Map stores the words present in list L 
        // against it's occurrences inside list L 
        HashMap<String, Integer> hashMap = 
            new HashMap<String, Integer>();

        for (String word : B) 
        {
            hashMap.put(word, hashMap.getOrDefault(word, 0) + 1);
        }

        for (int i = 0; i <= n - size_l; i++) 
        {
            HashMap<String, Integer> tempMap = 
            (HashMap<String, Integer>) hashMap.clone();
            int j = i, count = word_count;

            // Traverse the substring 
            while (j < i + size_l) 
            {
                // Extract the word
                String word = A.substring(j, j + size_word);

                // If word not found or if frequency 
                // of current word is more than required simply break. 
                if (!hashMap.containsKey(word) || tempMap.get(word) == 0) 
                {
                    break;
                } 

                // Else decrement the count of word from hash_map
                else 
                {
                    tempMap.put(word, tempMap.get(word) - 1);
                    count--;
                }
                j += size_word;
            }

            // Store the starting index of that
            // substring when all the words in 
            // the list are in substring 
            if (count == 0)
            {
                res.add(i);
            }

        }
        return res;
    }

    // Driver code
    public static void main(String[] args) 
    {
        String S = "barfoothefoobarman";
        ArrayList<String> L = 
        new ArrayList<>(Arrays.asList("foo", "bar"));
        ArrayList<Integer> indices = findSubstring(S, L);
        for (Integer i : indices)
        {
            System.out.println(i);
        }
    }
}

// This code is contributed by Manish Sakariya
```

## 蟒蛇 3

```
# Python3 program to calculate the starting indices
# of substrings inside S which contains all the
# words present in List L.

# Returns an integer vector consisting of starting
# indices of substrings present inside the string S
def findSubStringIndices(s, L):

    # Number of a characters of a word in list L.
    size_word = len(L[0])

    # Number of words present inside list L.
    word_count = len(L)

    # Total characters present in list L.
    size_L = size_word * word_count

    # Resultant vector which stores indices.
    res = []

    # If the total number of characters in list L
    # is more than length of string S itself.
    if size_L > len(s):
        return res

    # Map stores the words present in list L
    # against it's occurrences inside list L
    hash_map = dict()

    for i in range(word_count):
        if L[i] in hash_map:
            hash_map[L[i]] += 1
        else:
            hash_map[L[i]] = 1

    for i in range(0, len(s) - size_L + 1, 1):
        temp_hash_map = hash_map.copy()
        j = i
        count = word_count

        # Traverse the substring
        while j < i + size_L:

            # Extract the word
            word = s[j:j + size_word]

            # If word not found or if frequency of 
            # current word is more than required simply break.
            if (word not in hash_map or 
                temp_hash_map[word] == 0):
                break

            # Else decrement the count of word
            # from hash_map
            else:
                temp_hash_map[word] -= 1
                count -= 1
            j += size_word

        # Store the starting index of that substring
        # when all the words in the list are in substring
        if count == 0:
            res.append(i)
    return res

# Driver Code
if __name__ == "__main__":
    s = "barfoothefoobarman"
    L = ["foo", "bar"]
    indices = findSubStringIndices(s, L)

    print(*indices)

# This code is contributed by
# sanjeev2552
```

**Output:**

```
0 9
```

时间复杂度:**O(N–K)* K**
N:字符串的长度 S.
K:如果所有单词都连接在一起，列表 L 的总长度。如果 L : ["ab "，" cd"]那么 K = 4。