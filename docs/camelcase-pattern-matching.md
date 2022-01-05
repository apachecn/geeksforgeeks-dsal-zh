# 山茶花图案匹配

> 原文:[https://www.geeksforgeeks.org/camelcase-pattern-matching/](https://www.geeksforgeeks.org/camelcase-pattern-matching/)

给定一个单词列表，其中每个单词都遵循 CamelCase 符号，任务是打印字典中与给定的仅由大写字符组成的模式匹配的所有单词。

**示例**

> **输入:**arr[]=[“welcome geek”“welcome ogeeksforgeks”“geeks forgeeks”]，pattern = "WTG"
> **输出:**welcome ogeeksforgeks
> **解释:**
> 给定模式只有一个缩写，即 welcome ogeeksforgeks。
> 
> **输入:**arr[]=[“Hi”、“Hello”、“HelloWorld”、“HiTech”、“HiGeek”、“HiTechWorld”、“HiTechCity”、“HiTechLab”]，pattern = "HA"
> **输出:**未找到匹配项
> **解释:**
> 给定的模式没有这样的缩写。

**进场:**
1。遍历每个单词，用给定字符串中的每个大写字母对该单词进行哈希处理(T3)。
例如:

```
For string = "GeeksForGeeks"
then the hashing after every uppercase letter found is:
map {
     {G, GeeksForGeeks},
     {GF, GeeksForGeeks},
     {GFG, GeeksForGeeks}
} 
```

2 .为[列表](https://www.geeksforgeeks.org/list-cpp-stl/)中的所有字符串创建哈希后。在[地图](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中搜索给定的图案，并打印所有映射到该图案的字符串。

下面是上述方法的实现:

## C++

```
// C++ to find CamelCase Pattern
// matching
#include "bits/stdc++.h"
using namespace std;

// Function that prints the camel
// case pattern matching
void CamelCase(vector<string>& words,
               string pattern)
{

    // Map to store the hashing
    // of each words with every
    // uppercase letter found
    map<string, vector<string> > map;

    // Traverse the words array
    // that contains all the
    // string
    for (int i = 0; i < words.size(); i++) {

        // Initialise str as
        // empty
        string str = "";

        // length of string words[i]
        int l = words[i].length();
        for (int j = 0; j < l; j++) {

            // For every uppercase
            // letter found map
            // that uppercase to
            // original words
            if (words[i][j] >= 'A'
                && words[i][j] <= 'Z') {
                str += words[i][j];
                map[str].push_back(words[i]);
            }
        }
    }

    bool wordFound = false;

    // Traverse the map for pattern
    // matching
    for (auto& it : map) {

        // If pattern matches then
        // print the corresponding
        // mapped words
        if (it.first == pattern) {
            wordFound = true;
            for (auto& itt : it.second) {
                cout << itt << endl;
            }
        }
    }

    // If word not found print
    // "No match found"
    if (!wordFound) {
        cout << "No match found";
    }
}

// Driver's Code
int main()
{
    vector<string> words = {
        "Hi", "Hello", "HelloWorld",
        "HiTech", "HiGeek", "HiTechWorld",
        "HiTechCity", "HiTechLab"
    };

    // Pattern to be found
    string pattern = "HT";

    // Function call to find the
    // words that match to the
    // given pattern
    CamelCase(words, pattern);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java to find CamelCase Pattern
// matching
import java.util.*;

class GFG{

// Function that prints the camel
// case pattern matching
static void CamelCase(ArrayList<String> words,
               String pattern)
{

    // Map to store the hashing
    // of each words with every
    // uppercase letter found
    Map<String, List<String>> map = new HashMap<String, List<String>>();

    // Traverse the words array
    // that contains all the
    // String
    for (int i = 0; i < words.size(); i++) {

        // Initialise str as
        // empty
        String str = "";

        // length of String words[i]
        int l = words.get(i).length();
        for (int j = 0; j < l; j++) {

            // For every uppercase
            // letter found map
            // that uppercase to
            // original words
            if (words.get(i).charAt(j) >= 'A'
                && words.get(i).charAt(j) <= 'Z') {
                str += words.get(i).charAt(j);
                map.put(str,list(map.get(str),words.get(i)));
            }
        }
    }

    boolean wordFound = false;

    // Traverse the map for pattern
    // matching
    for (Map.Entry<String,List<String>> it : map.entrySet()) {

        // If pattern matches then
        // print the corresponding
        // mapped words
        if (it.getKey().equals(pattern)) {
            wordFound = true;
            for(String s : it.getValue())
            System.out.print(s +"\n");

        }
    }

    // If word not found print
    // "No match found"
    if (!wordFound) {
        System.out.print("No match found");
    }
}

private static List<String> list(List<String> list, String str) {
    List<String> temp = new ArrayList<String>();
    if(list != null)
        temp.addAll(list);
    temp.add(str);
    return temp;
}

// Driver's Code
public static void main(String[] args)
{
    String arr[] = {"Hi", "Hello", "HelloWorld",
            "HiTech", "HiGeek", "HiTechWorld",
            "HiTechCity", "HiTechLab"
        };

    ArrayList<String> words = new ArrayList<String>(Arrays.asList(arr));

    // Pattern to be found
    String pattern = "HT";

    // Function call to find the
    // words that match to the
    // given pattern
    CamelCase(words, pattern);

}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 to find CamelCase Pattern
# matching

# Function that prints the camel
# case pattern matching
def CamelCase(words, pattern) :

    # Map to store the hashing
    # of each words with every
    # uppercase letter found
    map = dict.fromkeys(words,None);

    # Traverse the words array
    # that contains all the
    # string
    for i in range(len(words)) :

        # Initialise str as
        # empty
        string = "";

        # length of string words[i]
        l = len(words[i]);
        for j in range(l) :

            # For every uppercase
            # letter found map
            # that uppercase to
            # original words
            if (words[i][j] >= 'A' and words[i][j] <= 'Z') :
                string += words[i][j];

                if string not in map :
                    map[string] = [words[i]]

                elif map[string] is None :
                    map[string] = [words[i]]

                else :
                    map[string].append(words[i]);

    wordFound = False;

    # Traverse the map for pattern
    # matching
    for key,value in map.items() :

        # If pattern matches then
        # print the corresponding
        # mapped words
        if (key == pattern) :
            wordFound = True;
            for itt in value :
                print(itt);

    # If word not found print
    # "No match found"
    if (not wordFound) :
        print("No match found");

# Driver's Code
if __name__ == "__main__" :

    words = [
        "Hi", "Hello", "HelloWorld",
        "HiTech", "HiGeek", "HiTechWorld",
        "HiTechCity", "HiTechLab"
    ];

    # Pattern to be found
    pattern = "HT";

    # Function call to find the
    # words that match to the
    # given pattern
    CamelCase(words, pattern);

# This code is contributed by AnkitRai01
```

## C#

```
// C# to find CamelCase Pattern
// matching
using System;
using System.Collections.Generic;

class GFG{

// Function that prints the camel
// case pattern matching
static void CamelCase(List<String> words,
               String pattern)
{

    // Map to store the hashing
    // of each words with every
    // uppercase letter found
    Dictionary<String, List<String>> map = new Dictionary<String, List<String>>();

    // Traverse the words array
    // that contains all the
    // String
    for (int i = 0; i < words.Count; i++) {

        // Initialise str as
        // empty
        String str = "";

        // length of String words[i]
        int l = words[i].Length;
        for (int j = 0; j < l; j++) {

            // For every uppercase
            // letter found map
            // that uppercase to
            // original words
            if (words[i][j] >= 'A'
                && words[i][j] <= 'Z') {
                str += words[i][j];
                if(map.ContainsKey(str))
                    map[str] = list(map[str],words[i]);
                else
                    map.Add(str,list(null,words[i]));
            }
        }
    }

    bool wordFound = false;

    // Traverse the map for pattern
    // matching
    foreach (KeyValuePair<String,List<String>> it in map) {
        // If pattern matches then
        // print the corresponding
        // mapped words
        if (it.Key.Equals(pattern)) {
            wordFound = true;
            foreach(String s in it.Value)
            Console.Write(s +"\n");

        }
    }

    // If word not found print
    // "No match found"
    if (!wordFound) {
        Console.Write("No match found");
    }
}

private static List<String> list(List<String> list, String str) {
    List<String> temp = new List<String>();
    if(list != null)
        temp.AddRange(list);
    temp.Add(str);
    return temp;
}

// Driver's Code
public static void Main(String[] args)
{
    String []arr = {"Hi", "Hello", "HelloWorld",
            "HiTech", "HiGeek", "HiTechWorld",
            "HiTechCity", "HiTechLab"
        };

    List<String> words = new List<String>(arr);

    // Pattern to be found
    String pattern = "HT";

    // Function call to find the
    // words that match to the
    // given pattern
    CamelCase(words, pattern);

}
}

// This code is contributed by Rajput-Ji
```

**Output**

```
HiTech
HiTechWorld
HiTechCity
HiTechLab
```

**时间复杂度:** O(N*M)，其中 N 是包含字符串的列表的长度，M 是最长字符串的长度。

**有效方法:**

1.  通过串联所有数组元素来准备一个字符串&在每个数组元素后使用分号作为分隔符。
2.  遍历串联字符串，查找大写字符或分隔符。
3.  保留一个包含所有大写字符的临时字符串，直到遍历中出现分隔符。将此临时字符串作为关键字(如果关键字不存在)添加到字典中，或者如果关键字已经存在，则追加该单词。
4.  一旦到达分隔符，重置临时变量。

下面是上述方法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;

void PrintMatchingCamelCase(vector<string> arr,
                            string pattern)
{

  // Concatenating all array elements
  // using Aggregate function of LINQ
  // putting semicolon as delimiter after each element
  string cctdString = "";
  for (int i = 0; i < arr.size(); i++) {
    cctdString += arr[i];
    if (i != arr.size() - 1)
      cctdString.push_back(';');
  }

  // Map to store the hashing
  // of each words with every
  // uppercase letter found
  unordered_map<string, vector<string> > maps;

  // temporary Variables
  int charPos = 0;
  int wordPos = 0;
  string strr = "";

  // Traversing through concatenated String
  for (; charPos < cctdString.length(); charPos++) {

    // Identifying if the current Character is
    // CamelCase If so, then adding to map
    // accordingly
    if (cctdString[charPos] >= 'A'
        && cctdString[charPos] <= 'Z') {
      strr += cctdString[charPos];

      // If pattern matches then
      // print the corresponding
      // mapped words
      if (maps.find(strr) != maps.end()) {
        vector<string> temp;
        temp.insert(temp.end(), maps[strr].begin(),
                    maps[strr].end());
        temp.push_back(arr[wordPos]);
        maps[strr] = temp;
      }
      else {
        vector<string> vec = { arr[wordPos] };
        maps[strr] = vec;
      }
    }

    // If delimiter has reached then reseting
    // temporary string also incrementing word
    // position value
    else if (cctdString[charPos] == ';') {
      wordPos++;
      strr = "";
    }
  }

  // If pattern matches then
  // print the corresponding
  // mapped words
  if (maps.find(pattern) != maps.end()) {
    for (int i = 0; i < maps[pattern].size(); i++) {
      cout << maps[pattern][i] << endl;
    }
  }
  else {
    cout << "No Match Found" << endl;
  }
}

// Driver code
int main()
{

  // Array of words
  vector<string> arr
    = { "Hi",         "Hello",    "HelloWorld",
       "HiTech",     "HiGeek",   "HiTechWorld",
       "HiTechCity", "HiTechLab" };

  // Pattern to be found
  string pattern = "HT";

  // Function call to find the
  // words that match to the
  // given pattern
  PrintMatchingCamelCase(arr, pattern);
}

// This code is contributed by parthmanchanda81
```

## C#

```
using System;
using System.Collections.Generic;
using System.Linq;

public class GFG {
    public static void
    PrintMatchingCamelCase(String[] arr, String pattern)
    {
        // Concatenating all array elements
        // using Aggregate function of LINQ
        // putting semicolon as delimiter after each element
        String cctdString
            = arr.Aggregate((i, j) = > i + ';' + j);
        // Map to store the hashing
        // of each words with every
        // uppercase letter found
        Dictionary<String, List<String> > map
            = new Dictionary<string, List<string> >();
        // temporary Variables
        int charPos = 0;
        int wordPos = 0;
        string strr = string.Empty;

        // Traversing through concatenated String
        for (; charPos < cctdString.Length; charPos++) {
            // Identifying if the current Character is
            // CamelCase If so, then adding to map
            // accordingly
            if (cctdString[charPos] >= 'A'
                && cctdString[charPos] <= 'Z') {
                strr += cctdString[charPos];
                if (map.ContainsKey(strr)) {
                    List<String> temp = new List<string>();
                    temp.AddRange(map[strr]);
                    temp.Add(arr[wordPos]);
                    map[strr] = temp;
                }
                else {
                    map.Add(strr, new List<string>{
                                      arr[wordPos] });
                }
            }
            // If delimiter has reached then reseting
            // temporary string also incrementing word
            // position value
            else if (cctdString[charPos] == ';') {
                wordPos++;
                strr = string.Empty;
            }
        }
        // If pattern matches then
        // print the corresponding
        // mapped words
        if (map.ContainsKey(pattern)) {
            foreach(String word in map[pattern])
            {
                Console.WriteLine(word);
            }
        }
        else {
            Console.WriteLine("No Match Found");
        }
    }

    // Driver's Code
    public static void Main(String[] args)
    {
        // Array of Words
        String[] arr
            = { "Hi",         "Hello",    "HelloWorld",
                "HiTech",     "HiGeek",   "HiTechWorld",
                "HiTechCity", "HiTechLab" };

        // Pattern to be found
        String pattern = "HT";

        // Function call to find the
        // words that match to the
        // given pattern
        PrintMatchingCamelCase(arr, pattern);
    }

    // This code is contributed by Rishabh Singh
}
```

## 蟒蛇 3

```
def PrintMatchingCamelCase(arr, pattern):

    # Concatenating all array elements
    # using Aggregate function of LINQ
    # putting semicolon as delimiter after each element
    cctdString = ';'.join(arr)

    # Map to store the hashing
    # of each words with every
    # uppercase letter found
    maps = dict()

    # temporary Variables
    wordPos = 0
    strr = ""

    # Traversing through concatenated String
    for charPos in range(len(cctdString)):

        # Identifying if the current Character is
        # CamelCase If so, then adding to map
        # accordingly
        if (cctdString[charPos] >= 'A'
                and cctdString[charPos] <= 'Z'):
            strr += cctdString[charPos]

            # If pattern matches then
            # print the corresponding
            # mapped words
            if strr in maps:
                temp = []
                temp.extend(maps[strr])
                temp.append(arr[wordPos])
                maps[strr] = temp

            else:
                vec = [arr[wordPos], ]
                maps[strr] = vec

        # If delimiter has reached then reseting
        # temporary string also incrementing word
        # position value
        elif (cctdString[charPos] == ';'):
            wordPos += 1
            strr = ""

    # If pattern matches then
    # print the corresponding
    # mapped words
    if (pattern in maps):
        for i in range(len(maps[pattern])):
            print(maps[pattern][i])

    else:
        print("No Match Found")

# Driver code
if __name__ == '__main__':

    # Array of words
    arr = ["Hi",         "Hello",    "HelloWorld",
           "HiTech",     "HiGeek",   "HiTechWorld",
           "HiTechCity", "HiTechLab"]

    # Pattern to be found
    pattern = "HT"

    # Function call to find the
    # words that match to the
    # given pattern
    PrintMatchingCamelCase(arr, pattern)

# This code is contributed by Amartya Ghosh
```

**Output**

```
HiTech
HiTechWorld
HiTechCity
HiTechLab
```

**时间复杂度:**O(N)
T3】辅助空间 : O(N)