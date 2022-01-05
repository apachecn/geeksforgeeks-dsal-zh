# 后缀数组|集合 2 (nLogn 算法)

> 原文:[https://www . geesforgeks . org/后缀-数组-集合-2-a-nlognlogn-算法/](https://www.geeksforgeeks.org/suffix-array-set-2-a-nlognlogn-algorithm/)

**后缀数组是给定字符串的所有后缀的排序数组。**的定义类似于[后缀树](https://www.geeksforgeeks.org/pattern-searching-set-8-suffix-tree-introduction/)，它是给定文本所有后缀的压缩三元组。

```
Let the given string be "banana".

0 banana                          5 a
1 anana     Sort the Suffixes     3 ana
2 nana      ---------------->     1 anana  
3 ana        alphabetically       0 banana  
4 na                              4 na   
5 a                               2 nana

The suffix array for "banana" is {5, 3, 1, 0, 4, 2}
```

我们已经讨论了构造后缀数组的 [**朴素算法**。朴素算法是考虑所有后缀，使用 O(nLogn)排序算法对它们进行排序，并且在排序时，保持原始索引。朴素算法的时间复杂度是 O(n <sup>2</sup> Logn)，其中 n 是输入字符串中的字符数。](https://www.geeksforgeeks.org/suffix-array-set-1-introduction/)

在这篇文章中，讨论了一种用于后缀数组构造的 **O(nLogn)算法**。为了简单起见，让我们首先讨论一个 O(n * Logn * Logn)算法。其思想是利用要排序的字符串是单个字符串的后缀这一事实。
我们首先根据第一个字符对所有后缀进行排序，然后根据前 2 个字符，然后是前 4 个字符，以此类推，同时要考虑的字符数小于 2n。重要的一点是，如果我们已经根据前 2 个 <sup>i</sup> 字符对后缀进行了排序，那么我们可以使用像 Merge Sort 这样的 nLogn 排序算法，在 O(nLogn)时间内根据前 2 个 <sup>i+1</sup> 字符对后缀进行排序。这是可能的，因为两个后缀可以在 O(1)时间内进行比较(我们只需要比较两个值，参见下面的示例和代码)。

排序函数被称为 0(Logn)次(注意，我们增加了要考虑的字符数的 2 次方)。因此，总的时间复杂度变成了 0(nLognLogn)。详见[http://www.stanford.edu/class/cs97si/suffix-array.pdf](http://www.stanford.edu/class/cs97si/suffix-array.pdf)。

让我们使用上面的算法来构建示例字符串“香蕉”的后缀数组。

**根据前两个字符排序**使用第一个字符的 ASCII 值为所有后缀指定一个等级。分配等级的一个简单方法是对 strp[]的后缀做“str[I]–‘a””

```
Index     Suffix            Rank
 0        banana             1   
 1        anana              0 
 2        nana               13 
 3        ana                0
 4        na                 13
 5        a                  0
```

对于每个字符，我们还存储下一个相邻字符的等级，即 str[i + 1]处的字符等级(这是根据前 2 个字符对后缀进行排序所需要的)。如果一个字符是最后一个字符，我们存储下一个等级为-1

```
Index    Suffix            Rank          Next Rank 
 0       banana             1              0
 1       anana              0              13    
 2       nana               13             0
 3       ana                0              13
 4       na                 13             0 
 5       a                  0             -1
```

根据等级和相邻等级对所有后缀进行排序。等级被视为第一位数字或 MSD，相邻的等级被视为第二位数字。

```
Index    Suffix            Rank          Next Rank 
 5        a                  0              -1
 1        anana              0               13    
 3        ana                0               13
 0        banana             1               0
 2        nana               13              0
 4        na                 13              0
```

**按照前四个字符**
排序，给所有后缀分配新的等级。为了分配新的等级，我们逐个考虑排序后的后缀。将 0 指定为第一个后缀的新等级。为了给剩余的后缀分配等级，我们考虑当前后缀前面的后缀的等级对。如果一个后缀的前一个等级对与其前一个后缀的前一个等级相同，那么给它分配相同的等级。否则，指定前一个后缀加 1 的等级。

```
Index       Suffix          Rank       
  5          a               0     [Assign 0 to first]        
  1          anana           1     (0, 13) is different from previous
  3          ana             1     (0, 13) is same as previous     
  0          banana          2     (1, 0) is different from previous      
  2          nana            3     (13, 0) is different from previous      
  4          na              3     (13, 0) is same as previous
```

对于每个后缀串[i]，也在串[i + 2]中存储下一个后缀的等级。如果在 i + 2 没有下一个后缀，我们将下一个等级存储为-1

```
Index       Suffix          Rank        Next Rank
  5          a               0             -1
  1          anana           1              1      
  3          ana             1              0 
  0          banana          2              3
  2          nana            3              3 
  4          na              3              -1
```

根据排名和下一个排名对所有后缀进行排序。

```
Index       Suffix          Rank        Next Rank
  5          a               0             -1
  3          ana             1              0 
  1          anana           1              1      
  0          banana          2              3
  4          na              3             -1
  2          nana            3              3
```

## C++

```
// C++ program for building suffix array of a given text
#include <iostream>
#include <cstring>
#include <algorithm>
using namespace std;

// Structure to store information of a suffix
struct suffix
{
    int index; // To store original index
    int rank[2]; // To store ranks and next rank pair
};

// A comparison function used by sort() to compare two suffixes
// Compares two pairs, returns 1 if first pair is smaller
int cmp(struct suffix a, struct suffix b)
{
    return (a.rank[0] == b.rank[0])? (a.rank[1] < b.rank[1] ?1: 0):
               (a.rank[0] < b.rank[0] ?1: 0);
}

// This is the main function that takes a string 'txt' of size n as an
// argument, builds and return the suffix array for the given string
int *buildSuffixArray(char *txt, int n)
{
    // A structure to store suffixes and their indexes
    struct suffix suffixes[n];

    // Store suffixes and their indexes in an array of structures.
    // The structure is needed to sort the suffixes alphabetically
    // and maintain their old indexes while sorting
    for (int i = 0; i < n; i++)
    {
        suffixes[i].index = i;
        suffixes[i].rank[0] = txt[i] - 'a';
        suffixes[i].rank[1] = ((i+1) < n)? (txt[i + 1] - 'a'): -1;
    }

    // Sort the suffixes using the comparison function
    // defined above.
    sort(suffixes, suffixes+n, cmp);

    // At this point, all suffixes are sorted according to first
    // 2 characters.  Let us sort suffixes according to first 4
    // characters, then first 8 and so on
    int ind[n];  // This array is needed to get the index in suffixes[]
                 // from original index.  This mapping is needed to get
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
            // If first rank and next ranks are same as that of previous
            // suffix in array, assign the same new rank to this suffix
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

    // Store indexes of all sorted suffixes in the suffix array
    int *suffixArr = new int[n];
    for (int i = 0; i < n; i++)
        suffixArr[i] = suffixes[i].index;

    // Return the suffix array
    return  suffixArr;
}

// A utility function to print an array of given size
void printArr(int arr[], int n)
{
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
    cout << endl;
}

// Driver program to test above functions
int main()
{
    char txt[] = "banana";
    int n = strlen(txt);
    int *suffixArr = buildSuffixArray(txt,  n);
    cout << "Following is suffix array for " << txt << endl;
    printArr(suffixArr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for building suffix array of a given text
import java.util.*;
class GFG
{
    // Class to store information of a suffix
    public static class Suffix implements Comparable<Suffix>
    {
        int index;
        int rank;
        int next;

        public Suffix(int ind, int r, int nr)
        {
            index = ind;
            rank = r;
            next = nr;
        }

        // A comparison function used by sort()
        // to compare two suffixes.
        // Compares two pairs, returns 1
        // if first pair is smaller
        public int compareTo(Suffix s)
        {
            if (rank != s.rank) return Integer.compare(rank, s.rank);
            return Integer.compare(next, s.next);
        }
    }

    // This is the main function that takes a string 'txt'
    // of size n as an argument, builds and return the
    // suffix array for the given string
    public static int[] suffixArray(String s)
    {
        int n = s.length();
        Suffix[] su = new Suffix[n];

        // Store suffixes and their indexes in
        // an array of classes. The class is needed
        // to sort the suffixes alphabetically and
        // maintain their old indexes while sorting
        for (int i = 0; i < n; i++)
        {
            su[i] = new Suffix(i, s.charAt(i) - '{content}apos;, 0);
        }
        for (int i = 0; i < n; i++)
            su[i].next = (i + 1 < n ? su[i + 1].rank : -1);

        // Sort the suffixes using the comparison function
        // defined above.
        Arrays.sort(su);

        // At this point, all suffixes are sorted
        // according to first 2 characters.
        // Let us sort suffixes according to first 4
        // characters, then first 8 and so on
        int[] ind = new int[n];

        // This array is needed to get the index in suffixes[]
        // from original index. This mapping is needed to get
        // next suffix.
        for (int length = 4; length < 2 * n; length <<= 1)
        {

            // Assigning rank and index values to first suffix
            int rank = 0, prev = su[0].rank;
            su[0].rank = rank;
            ind[su[0].index] = 0;
            for (int i = 1; i < n; i++)
            {
                // If first rank and next ranks are same as
                // that of previous suffix in array,
                // assign the same new rank to this suffix
                if (su[i].rank == prev &&
                    su[i].next == su[i - 1].next)
                {
                    prev = su[i].rank;
                    su[i].rank = rank;
                }
                else
                {
                    // Otherwise increment rank and assign
                    prev = su[i].rank;
                    su[i].rank = ++rank;
                }
                ind[su[i].index] = i;
            }

            // Assign next rank to every suffix
            for (int i = 0; i < n; i++)
            {
                int nextP = su[i].index + length / 2;
                su[i].next = nextP < n ?
                   su[ind[nextP]].rank : -1;
            }

            // Sort the suffixes according
            // to first k characters
            Arrays.sort(su);
        }

        // Store indexes of all sorted
        // suffixes in the suffix array
        int[] suf = new int[n];

        for (int i = 0; i < n; i++)
            suf[i] = su[i].index;

        // Return the suffix array
        return suf;
    }   

    static void printArr(int arr[], int n)
    {
        for (int i = 0; i < n; i++)
            System.out.print(arr[i] + " ");
        System.out.println();
    }

    // Driver Code
    public static void main(String[] args)
    {
        String txt = "banana";
        int n = txt.length();
        int[] suff_arr = suffixArray(txt);
        System.out.println("Following is suffix array for banana:");
        printArr(suff_arr, n);
    }
}

// This code is contributed by AmanKumarSingh
```

## 蟒蛇 3

```
# Python3 program for building suffix
# array of a given text

# Class to store information of a suffix
class suffix:

    def __init__(self):

        self.index = 0
        self.rank = [0, 0]

# This is the main function that takes a
# string 'txt' of size n as an argument,
# builds and return the suffix array for
# the given string
def buildSuffixArray(txt, n):

    # A structure to store suffixes
    # and their indexes
    suffixes = [suffix() for _ in range(n)]

    # Store suffixes and their indexes in
    # an array of structures. The structure
    # is needed to sort the suffixes alphabetically
    # and maintain their old indexes while sorting
    for i in range(n):
        suffixes[i].index = i
        suffixes[i].rank[0] = (ord(txt[i]) -
                               ord("a"))
        suffixes[i].rank[1] = (ord(txt[i + 1]) -
                        ord("a")) if ((i + 1) < n) else -1

    # Sort the suffixes according to the rank
    # and next rank
    suffixes = sorted(
        suffixes, key = lambda x: (
            x.rank[0], x.rank[1]))

    # At this point, all suffixes are sorted
    # according to first 2 characters.  Let
    # us sort suffixes according to first 4
    # characters, then first 8 and so on
    ind = [0] * n  # This array is needed to get the
                   # index in suffixes[] from original
                   # index.This mapping is needed to get
                   # next suffix.
    k = 4
    while (k < 2 * n):

        # Assigning rank and index
        # values to first suffix
        rank = 0
        prev_rank = suffixes[0].rank[0]
        suffixes[0].rank[0] = rank
        ind[suffixes[0].index] = 0

        # Assigning rank to suffixes
        for i in range(1, n):

            # If first rank and next ranks are
            # same as that of previous suffix in
            # array, assign the same new rank to
            # this suffix
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
            suffixes[i].rank[1] = suffixes[ind[nextindex]].rank[0] \
                if (nextindex < n) else -1

        # Sort the suffixes according to
        # first k characters
        suffixes = sorted(
            suffixes, key = lambda x: (
                x.rank[0], x.rank[1]))

        k *= 2

    # Store indexes of all sorted
    # suffixes in the suffix array
    suffixArr = [0] * n

    for i in range(n):
        suffixArr[i] = suffixes[i].index

    # Return the suffix array
    return suffixArr

# A utility function to print an array
# of given size
def printArr(arr, n):

    for i in range(n):
        print(arr[i], end = " ")

    print()

# Driver code
if __name__ == "__main__":

    txt = "banana"
    n = len(txt)

    suffixArr = buildSuffixArray(txt, n)

    print("Following is suffix array for", txt)

    printArr(suffixArr, n)

# This code is contributed by debrc
```

## java 描述语言

```
<script>
// Javascript program for building suffix array of a given text

// Class to store information of a suffix
class Suffix
{
    constructor(ind,r,nr)
    {
        this.index = ind;
        this.rank = r;
        this.next = nr;
    }

}

// This is the main function that takes a string 'txt'
    // of size n as an argument, builds and return the
    // suffix array for the given string
function suffixArray(s)
{
    let n = s.length;
        let su = new Array(n);

        // Store suffixes and their indexes in
        // an array of classes. The class is needed
        // to sort the suffixes alphabetically and
        // maintain their old indexes while sorting
        for (let i = 0; i < n; i++)
        {
            su[i] = new Suffix(i, s[i].charCodeAt(0) - '{content}apos;.charCodeAt(0), 0);
        }
        for (let i = 0; i < n; i++)
            su[i].next = (i + 1 < n ? su[i + 1].rank : -1);

        // Sort the suffixes using the comparison function
        // defined above.
        su.sort(function(a,b){
            if(a.rank!=b.rank)
                return a.rank-b.rank;
            else
                return a.next-b.next;
        });

        // At this point, all suffixes are sorted
        // according to first 2 characters.
        // Let us sort suffixes according to first 4
        // characters, then first 8 and so on
        let ind = new Array(n);

        // This array is needed to get the index in suffixes[]
        // from original index. This mapping is needed to get
        // next suffix.
        for (let length = 4; length < 2 * n; length <<= 1)
        {

            // Assigning rank and index values to first suffix
            let rank = 0, prev = su[0].rank;
            su[0].rank = rank;
            ind[su[0].index] = 0;
            for (let i = 1; i < n; i++)
            {
                // If first rank and next ranks are same as
                // that of previous suffix in array,
                // assign the same new rank to this suffix
                if (su[i].rank == prev &&
                    su[i].next == su[i - 1].next)
                {
                    prev = su[i].rank;
                    su[i].rank = rank;
                }
                else
                {
                    // Otherwise increment rank and assign
                    prev = su[i].rank;
                    su[i].rank = ++rank;
                }
                ind[su[i].index] = i;
            }

            // Assign next rank to every suffix
            for (let i = 0; i < n; i++)
            {
                let nextP = su[i].index + length / 2;
                su[i].next = nextP < n ?
                   su[ind[nextP]].rank : -1;
            }

            // Sort the suffixes according
            // to first k characters
            su.sort(function(a,b){
            if(a.rank!=b.rank)
                return a.rank-b.rank;
            else
                return a.next-b.next;
        });
        }

        // Store indexes of all sorted
        // suffixes in the suffix array
        let suf = new Array(n);

        for (let i = 0; i < n; i++)
            suf[i] = su[i].index;

        // Return the suffix array
        return suf;
}

function printArr(arr,n)
{
    for (let i = 0; i < n; i++)
            document.write(arr[i] + " ");
        document.write();
}

// Driver Code
let txt = "banana";
let n = txt.length;
let suff_arr = suffixArray(txt);
document.write("Following is suffix array for banana:<br>");
printArr(suff_arr, n);

// This code is contributed by patel2127
</script>
```

**Output**

```
Following is suffix array for banana
5 3 1 0 4 2 
```