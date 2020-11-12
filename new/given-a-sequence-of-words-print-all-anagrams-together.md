# 给定一个单词序列，一起打印所有异序词 | 系列 1

> 原文：[https://www.geeksforgeeks.org/given-a-sequence-of-words-print-all-anagrams-together/](https://www.geeksforgeeks.org/given-a-sequence-of-words-print-all-anagrams-together/)

给定一组单词，将所有异序词一起打印。 例如，如果给定的数组是`{"cat", "dog", "tac", "god", "act"}`，则输出可能是`"cat tac act dog god"`。

**简单方法**是创建哈希表。 以所有异序词都具有相同哈希值的方式计算每个单词的哈希值。 用这些哈希值填充哈希表。 最后，将这些单词与相同的哈希值一起打印。 一个简单的哈希机制可以是所有字符的模和。 使用模和，两个非异序词单词可能具有相同的哈希值。 这可以通过匹配单个字符来处理。

以下是**另一种将所有异序词一起打印的方法**。 取两个辅助数组，索引数组和字数组。 用给定的单词序列填充单词数组。 对单词数组中的每个单词排序。 最后，对单词数组排序并跟踪相应的索引。 排序后，所有的异序词聚在一起。 使用索引数组可打印原始字符串数组中的字符串。

让我们了解以下输入单词序列的步骤：

```
"cat", "dog", "tac", "god", "act"

```

1.  创建两个辅助数组`index[]`和`word[]`。 将所有给定的单词复制到`words[]`并将原始索引存储在`index[]`中。

```
index[]:  0   1   2   3   4
words[]: cat dog tac god act

```

2.  对单词中的单个单词排序[]。 索引数组不变。

```
index[]:   0    1    2    3    4
words[]:  act  dgo  act  dgo  act

```

3.  对单词数组排序。 使用`strcmp()`比较单个单词排序。

```
index:     0    2    4    1    3
words[]:  act  act  act  dgo  dgo

```

4.  所有的异序词组合在一起。 但是单词会在单词数组中更改。 要打印原始单词，请从索引数组中获取索引并在原始数组中使用它。 我们得到：

```
"cat tac act dog god"

```

以下是上述算法的实现。 在下面的程序中，结构`Word`的数组用于存储索引和单词数组。 `DupArray`是另一个存储结构`Word`的数组的结构。

## C++

```cpp

// A C++ program to print all anagarms together
#include <bits/stdc++.h>
#include <string.h>
using namespace std;

// structure for each word of duplicate array
class Word {
public:
    char* str; // to store word itself
    int index; // index of the word in the original array
};

// structure to represent duplicate array.
class DupArray {
public:
    Word* array; // Array of words
    int size; // Size of array
};

// Create a DupArray object that contains an array of Words
DupArray* createDupArray(char* str[], int size)
{
    // Allocate memory for dupArray and all members of it
    DupArray* dupArray = new DupArray();
    dupArray->size = size;
    dupArray->array = new Word[(dupArray->size * sizeof(Word))];

    // One by one copy words from the given wordArray to dupArray
    int i;
    for (i = 0; i < size; ++i) {
        dupArray->array[i].index = i;
        dupArray->array[i].str = new char[(strlen(str[i]) + 1)];
        strcpy(dupArray->array[i].str, str[i]);
    }

    return dupArray;
}

// Compare two characters. Used in qsort() for
// sorting an array of characters (Word)
int compChar(const void* a, const void* b)
{
    return *(char*)a - *(char*)b;
}

// Compare two words. Used in qsort()
// for sorting an array of words
int compStr(const void* a, const void* b)
{
    Word* a1 = (Word*)a;
    Word* b1 = (Word*)b;
    return strcmp(a1->str, b1->str);
}

// Given a list of words in wordArr[],
void printAnagramsTogether(char* wordArr[], int size)
{
    // Step 1: Create a copy of all words present in given wordArr.
    // The copy will also have original indexes of words
    DupArray* dupArray = createDupArray(wordArr, size);

    // Step 2: Iterate through all words in dupArray and sort
    // individual words.
    int i;
    for (i = 0; i < size; ++i)
        qsort(dupArray->array[i].str,
              strlen(dupArray->array[i].str), sizeof(char), compChar);

    // Step 3: Now sort the array of words in dupArray
    qsort(dupArray->array, size, sizeof(dupArray->array[0]), compStr);

    // Step 4: Now all words in dupArray are together, but these
    // words are changed. Use the index member of word struct to
    // get the corresponding original word
    for (i = 0; i < size; ++i)
        cout << wordArr[dupArray->array[i].index] << " ";
}

// Driver program to test above functions
int main()
{
    char* wordArr[] = { "cat", "dog", "tac", "god", "act" };
    int size = sizeof(wordArr) / sizeof(wordArr[0]);
    printAnagramsTogether(wordArr, size);
    return 0;
}

// This is code is contributed by rathbhupendra

```

## C

```c

// A C program to print all anagarms together
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// structure for each word of duplicate array
struct Word {
    char* str; // to store word itself
    int index; // index of the word in the original array
};

// structure to represent duplicate array.
struct DupArray {
    struct Word* array; // Array of words
    int size; // Size of array
};

// Create a DupArray object that contains an array of Words
struct DupArray* createDupArray(char* str[], int size)
{
    // Allocate memory for dupArray and all members of it
    struct DupArray* dupArray = (struct DupArray*)malloc(sizeof(struct DupArray));
    dupArray->size = size;
    dupArray->array = (struct Word*)malloc(dupArray->size * sizeof(struct Word));

    // One by one copy words from the given wordArray to dupArray
    int i;
    for (i = 0; i < size; ++i) {
        dupArray->array[i].index = i;
        dupArray->array[i].str = (char*)malloc(strlen(str[i]) + 1);
        strcpy(dupArray->array[i].str, str[i]);
    }

    return dupArray;
}

// Compare two characters. Used in qsort() for sorting an array of
// characters (Word)
int compChar(const void* a, const void* b)
{
    return *(char*)a - *(char*)b;
}

// Compare two words. Used in qsort() for sorting an array of words
int compStr(const void* a, const void* b)
{
    struct Word* a1 = (struct Word*)a;
    struct Word* b1 = (struct Word*)b;
    return strcmp(a1->str, b1->str);
}

// Given a list of words in wordArr[],
void printAnagramsTogether(char* wordArr[], int size)
{
    // Step 1: Create a copy of all words present in given wordArr.
    // The copy will also have original indexes of words
    struct DupArray* dupArray = createDupArray(wordArr, size);

    // Step 2: Iterate through all words in dupArray and sort
    // individual words.
    int i;
    for (i = 0; i < size; ++i)
        qsort(dupArray->array[i].str,
              strlen(dupArray->array[i].str), sizeof(char), compChar);

    // Step 3: Now sort the array of words in dupArray
    qsort(dupArray->array, size, sizeof(dupArray->array[0]), compStr);

    // Step 4: Now all words in dupArray are together, but these
    // words are changed. Use the index member of word struct to
    // get the corresponding original word
    for (i = 0; i < size; ++i)
        printf("%s ", wordArr[dupArray->array[i].index]);
}

// Driver program to test above functions
int main()
{
    char* wordArr[] = { "cat", "dog", "tac", "god", "act" };
    int size = sizeof(wordArr) / sizeof(wordArr[0]);
    printAnagramsTogether(wordArr, size);
    return 0;
}

```

## Java

```java

// A Java program to print all anagrams together
import java.util.Arrays;
import java.util.Comparator;
public class GFG {
    // class for each word of duplicate array
    static class Word {
        String str; // to store word itself
        int index; // index of the word in the
        // original array

        // constructor
        Word(String str, int index)
        {
            this.str = str;
            this.index = index;
        }
    }

    // class to represent duplicate array.
    static class DupArray {
        Word[] array; // Array of words
        int size; // Size of array

        // constructor
        public DupArray(String str[], int size)
        {
            this.size = size;
            array = new Word[size];

            // One by one copy words from the
            // given wordArray to dupArray
            int i;
            for (i = 0; i < size; ++i) {
                // create a word Object with the
                // str[i] as str and index as i
                array[i] = new Word(str[i], i);
            }
        }
    }

    // Compare two words. Used in Arrays.sort() for
    // sorting an array of words
    static class compStr implements Comparator<Word> {
        public int compare(Word a, Word b)
        {
            return a.str.compareTo(b.str);
        }
    }

    // Given a list of words in wordArr[],
    static void printAnagramsTogether(String wordArr[],
                                      int size)
    {
        // Step 1: Create a copy of all words present
        // in given wordArr. The copy will also have
        // original indexes of words
        DupArray dupArray = new DupArray(wordArr, size);

        // Step 2: Iterate through all words in
        // dupArray and sort individual words.
        int i;
        for (i = 0; i < size; ++i) {
            char[] char_arr = dupArray.array[i].str.toCharArray();
            Arrays.sort(char_arr);
            dupArray.array[i].str = new String(char_arr);
        }

        // Step 3: Now sort the array of words in
        // dupArray
        Arrays.sort(dupArray.array, new compStr());

        // Step 4: Now all words in dupArray are together,
        // but these words are changed. Use the index
        // member of word struct to get the corresponding
        // original word
        for (i = 0; i < size; ++i)
            System.out.print(wordArr[dupArray.array[i].index] + " ");
    }

    // Driver program to test above functions
    public static void main(String args[])
    {
        String wordArr[] = { "cat", "dog", "tac", "god", "act" };
        int size = wordArr.length;
        printAnagramsTogether(wordArr, size);
    }
}
// This code is contributed by Sumit Ghosh

```

## Python

```py

# A Python program to print all anagarms together

# structure for each word of duplicate array
class Word(object):
    def __init__(self, string, index):
        self.string = string
        self.index = index

# Create a DupArray object that contains an array
# of Words
def createDupArray(string, size):
    dupArray = []

    # One by one copy words from the given wordArray
    # to dupArray
    for i in xrange(size):
        dupArray.append(Word(string[i], i))

    return dupArray

# Given a list of words in wordArr[]
def printAnagramsTogether(wordArr, size):
    # Step 1: Create a copy of all words present in
    # given wordArr.
    # The copy will also have original indexes of words
    dupArray = createDupArray(wordArr, size)

    # Step 2: Iterate through all words in dupArray and sort
    # individual words.
    for i in xrange(size):
        dupArray[i].string = ''.join(sorted(dupArray[i].string))

    # Step 3: Now sort the array of words in dupArray
    dupArray = sorted(dupArray, key = lambda k: k.string)

    # Step 4: Now all words in dupArray are together, but
    # these words are changed. Use the index member of word
    # struct to get the corresponding original word
    for word in dupArray:
        print wordArr[word.index],

# Driver program
wordArr = ["cat", "dog", "tac", "god", "act"]
size = len(wordArr)
printAnagramsTogether(wordArr, size)

# This code is contributed by BHAVYA JAIN

```

**输出**：

```
cat tac act dog god 

```

**时间复杂度**：假设有`N`个单词，每个单词最多包含`M`个字符。 上限为`O(NMLogM + MNLogN)`。

步骤 2 需要`O(NMLogM)`时间。 排序单词最多需要 `O(MLogM)`时间。 因此，对`N`个单词排序需要`O(NMLogM)`时间。 步骤 3 使用`O(MNLogN)`单词排序数组进行`NLogN`比较。 比较可能需要最多`O(M)`时间。 因此，对单词数组排序的时间为`O(MNLogN)`。

**使用哈希映射**

在这里，我们首先对每个单词排序，将排序后的单词用作键，然后将原始单词放入映射中。 映射的值将是一个列表，其中包含排序后具有相同单词的所有单词。

最后，我们将打印哈希映射中所有值大于 1 的值。

## Java

```java

// Java program to print anagrams
// together using dictionary
import java.util.*;

public class FindAnagrams {

    private static void printAnagrams(String arr[])
    {
        HashMap<String, List<String> > map = new HashMap<>();

        // loop over all words
        for (int i = 0; i < arr.length; i++) {

            // convert to char array, sort and
            // then re-convert to string
            String word = arr[i];
            char[] letters = word.toCharArray();
            Arrays.sort(letters);
            String newWord = new String(letters);

            // calculate hashcode of string
            // after sorting
            if (map.containsKey(newWord)) {

                map.get(newWord).add(word);
            }
            else {

                // This is the first time we are
                // adding a word for a specific
                // hashcode
                List<String> words = new ArrayList<>();
                words.add(word);
                map.put(newWord, words);
            }
        }

        // print all the values where size is > 1
        // If you want to print non-anagrams,
        // just print the values having size = 1
        for (String s : map.keySet()) {
            List<String> values = map.get(s);
            if (values.size() > 1) {
                System.out.print(values);
            }
        }
    }

    public static void main(String[] args)
    {

        // Driver program
        String arr[] = { "cat", "dog", "tac", "god", "act" };
        printAnagrams(arr);
    }
}

```

## Python3

```py

from collections import defaultdict 

def printAnagramsTogether(words):
    groupedWords = defaultdict(list)

    # Put all anagram words together in a dictionary 
    # where key is sorted word
    for word in words:
        groupedWords["".join(sorted(word))].append(word)

    # Print all anagrams together
    for group in groupedWords.values():
        print(" ".join(group))      

if __name__ == "__main__":   
    arr =  ["cat", "dog", "tac", "god", "act"]  
    printAnagramsTogether(arr)     

```

## C#

```cs

// C# program to print anagrams
// together using dictionary
using System;
using System.Collections.Generic;

class GFG {
    private static void printAnagrams(String[] arr)
    {
        Dictionary<String,
                   List<String> >
            map = new Dictionary<String,
                                 List<String> >();

        // loop over all words
        for (int i = 0; i < arr.Length; i++) {

            // convert to char array, sort and
            // then re-convert to string
            String word = arr[i];
            char[] letters = word.ToCharArray();
            Array.Sort(letters);
            String newWord = new String(letters);

            // calculate hashcode of string
            // after sorting
            if (map.ContainsKey(newWord)) {
                map[newWord].Add(word);
            }
            else {

                // This is the first time we are
                // adding a word for a specific
                // hashcode
                List<String> words = new List<String>();
                words.Add(word);
                map.Add(newWord, words);
            }
        }

        // print all the values where size is > 1
        // If you want to print non-anagrams,
        // just print the values having size = 1
        List<String> value = new List<String>();
        foreach(KeyValuePair<String,
                             List<String> >
                    entry in map)
        {
            value.Add(entry.Key);
        }
        int k = 0;
        foreach(KeyValuePair<String,
                             List<String> >
                    entry in map)
        {
            List<String> values = map[value[k++]];
            if (values.Count > 1) {
                Console.Write("[");
                int len = 1;
                foreach(String s in values)
                {
                    Console.Write(s);
                    if (len++ < values.Count)
                        Console.Write(", ");
                }
                Console.Write("]");
            }
        }
    }

    // Driver Code
    public static void Main(String[] args)
    {
        String[] arr = { "cat", "dog", "tac",
                         "god", "act" };
        printAnagrams(arr);
    }
}

// This code is contributed by Princi Singh

```

**输出**：

```
[cat, tac, act][dog, god]

```

**使用`HashMap`的`O(NM)`解决方案**

在先前的方法中，我们对每个字符串排序以维护相似的键，但是这种方法花费额外的时间将利用另一个哈希映射来 保持字符的频率，将为具有相同字符频率的不同字符串生成相同的哈希函数。

在这里，我们将使用`HashMap<HashMap, ArrayList>`，内部的`hashmap`将计算每个字符串的字符的频率，外部的`HashMap`将检查该`hashmap`是否存在（如果存在），然后它将 将该字符串添加到相应的列表中。

## C++

```cpp

// C++ code to print all anagrams together 
#include <bits/stdc++.h>
using namespace std;

void solver(vector<string> my_list)
{

    // Inner hashmap counts frequency
    // of characters in a string.
    // Outer hashmap for if same
    // frequency characters are present in
    // in a string then it will add it to
    // the vector.
    map<map<char, int>, vector<string>> my_map;

    // Loop over all words
    for(string str : my_list)
    {

        // Counting the frequency of the
        // characters present in a string
        map<char, int> temp_map;
        vector<string> temp_my_list;
        for(int i = 0; i < str.length(); ++i) 
        {
            ++temp_map[str[i]];
        }

        // If the same frequency of chanracters
        // are alraedy present then add that
        // string into that arraylist otherwise
        // created a new arraylist and add that
        // string
        auto it = my_map.find(temp_map);
        if (it != my_map.end())
        {
            it->second.push_back(str);
        }
        else
        {
            temp_my_list.push_back(str);
            my_map.insert({ temp_map, temp_my_list });
        }
    }

    // Stores the result in a vector
    vector<vector<string>> result;

    for(auto it = my_map.begin();
             it != my_map.end(); ++it)
    {
        result.push_back(it->second);
    }

    for(int i = 0; i < result.size(); ++i) 
    {
          cout << "[";
        for(int j = 0; j < result[i].size(); ++j) 
        {
            cout << result[i][j] << ", ";
        }
          cout << "]";
    }
}

// Driver code
int main()
{
    vector<string> my_list = { "cat", "dog", "ogd",
                               "god", "atc" };
    solver(my_list);
    return 0;
}

// This code is contributed by 
// Apurba Kumar Gorai(coolapurba05)

```

## Java

```java

// Java code tp print all anagrams together
import java.util.ArrayList;
import java.util.HashMap;

public class FindAnagrams {

    private static ArrayList<ArrayList<String> >
    solver(
        ArrayList<String> list)
    {

        // Inner hashmap counts frequency
        // of characters in a string.
        // Outer hashmap for if same
        // frequency characters are present in
        // in a string then it will add it to
        // the arraylist.
        HashMap<HashMap<Character, Integer>,
                ArrayList<String> >
            map = new HashMap<HashMap<Character, Integer>,
                              ArrayList<String> >();
        for (String str : list) {
            HashMap<Character, Integer>
                tempMap = new HashMap<Character, Integer>();

            // Counting the frequency of the
            // characters present in a string
            for (int i = 0; i < str.length(); i++) {
                if (tempMap.containsKey(str.charAt(i))) {
                    int x = tempMap.get(str.charAt(i));
                    tempMap.put(str.charAt(i), ++x);
                }
                else {
                    tempMap.put(str.charAt(i), 1);
                }
            }

            // If the same frequency of chanracters
            // are alraedy present then add that
            // string into that arraylist otherwise
            // created a new arraylist and add that string
            if (map.containsKey(tempMap))
                map.get(tempMap).add(str);
            else {
                ArrayList<String>
                    tempList = new ArrayList<String>();
                tempList.add(str);
                map.put(tempMap, tempList);
            }
        }

        // Stores the result in a arraylist
        ArrayList<ArrayList<String> >
            result = new ArrayList<>();
        for (HashMap<Character, Integer>
                 temp : map.keySet())
            result.add(map.get(temp));
        return result;
    }

    // Drivers Method
    public static void main(String[] args)
    {
        ArrayList<String> list = new ArrayList<>();
        list.add("cat");
        list.add("dog");
        list.add("ogd");
        list.add("god");
        list.add("atc");

        System.out.println(solver(list));
    }
}

// This code is contributed by Arijit Basu(ArijitXfx)

```

**输出**：

```
[[cat, atc], [dog, ogd, god]]

```

**时间复杂度**：假设有`N`个单词，每个单词最多包含`M`个字符。 上限为`O(NM)`。

**空间复杂度**：假设有`N`个单词，每个单词最多包含`M`个字符。 上限为`O(N + M)`。

[**给定一个单词序列，一起打印所有异序词 | 系列 2**](https://www.geeksforgeeks.org/given-a-sequence-of-words-print-all-anagrams-together-set-2/)

如果发现不正确的内容，或者想共享有关上述主题的更多信息，请写评论。

