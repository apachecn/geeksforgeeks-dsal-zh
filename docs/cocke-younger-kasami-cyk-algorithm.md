# Cocke–Younger–Kasami(CYK)算法

> 原文:[https://www . geeksforgeeks . org/cocke-younger-kasami-cyk-algorithm/](https://www.geeksforgeeks.org/cocke-younger-kasami-cyk-algorithm/)

[语法](https://www.geeksforgeeks.org/relationship-between-grammar-and-language-in-theory-of-computation/)表示自然语言中会话的句法规则。但是在形式语言理论中，语法被定义为一组可以生成字符串的规则。可以从语法中生成的所有字符串的集合称为语法语言。

**上下文无关语法:**
给我们一个[上下文无关语法](https://www.geeksforgeeks.org/classification-of-context-free-grammars/) G = (V，X，R，S)和一个字符串 w，其中:

*   *V* 是变量或非终结符号的有限集合，
*   *X* 是一组有限的终端符号，
*   *R* 是一组有限的规则，
*   *S* 是起始符号，是 *V* 的独特元素，并且
*   *V* 和 *X* 假设为不相交的集合。

**隶属问题**定义为:语法 G 生成语言 L(G)。给定的字符串是 L(G)的成员吗？

**乔姆斯基范式:**
如果 *G* 的每个规则的形式为:

*   *A–>**BC*【RHS 上最多有两个非终端符号】
*   *A*–>*A*，或【右侧一个终端符号】
*   *s*–>零字串*，*【零字串】

**Cocke-Younger-Kasami 算法**
它用于使用[动态规划](http://www.geeksforgeeks.org/dynamic-programming/)方法解决成员资格问题。该算法基于问题*【I，j】*的解可以从子问题*【I，k】*的解和子问题*【k，j】的解构造的原理。*算法要求语法 *G* 为乔姆斯基范式(CNF)。请注意，任何上下文无关语法都可以系统地[转换为 CNF](https://www.geeksforgeeks.org/converting-context-free-grammar-chomsky-normal-form/) 。采用这种限制是为了使每个问题只能分成两个子问题，而不是更多子问题——以限制时间复杂度。

**CYK 算法是如何工作的？**

对于长度为 **N** 的字符串，构建一个大小为 **N x N** 的表 **T** 。表中的每个单元格 **T[i，j]** 是能够产生从位置 I 到 j 的子串的所有组成部分的集合。该过程包括用自下而上解析过程中遇到的子问题的解决方案填充表。因此，单元格将从左到右、从下到上填充。

<figure class="table">

|   | 

one

 | 

Two

 | 

three

 | 

**4**

 | 

**5**

 |
| --- | --- | --- | --- | --- | --- |
| one | [1, 1] | [1, 2] | [1, 3] | [1, 4] | [1, 5] |
| Two |   | [2, 2] | [2, 3] | [2, 4] | [2, 5] |
| three |   |   | [3, 3] | [3, 4] | [3, 5] |
| four |   |   |   | [4, 4] | [4, 5] |
| five |   |   |   |   | [5, 5] |

在 T[i，j]中，行号 *i* 表示开始索引，列号 *j* 表示结束索引。

![A \in T[i, j] \text{ if and only if } B \in T[i, k], C \in T[k, j] \text{ and } A \rightarrow BC \text{ is a rule of G} ](img/4c9308539ef1e65eebee84b58dfe5f16.png "Rendered by QuickLaTeX.com")

该算法考虑了[字母的每个可能的子序列](https://www.geeksforgeeks.org/generating-all-possible-subsequences-using-recursion/)，如果从 *i* 到 *j* 的字母序列可以从非端 *K* 生成，则将 **K** 加到*T【I，j】*上。对于长度为 2 或更长的子序列，它会考虑将子序列分成两部分的每种可能，并检查是否存在 *A* 形式的规则？ *BC* 中的语法，其中 B 和 C 可以根据 *T* 中已经存在的条目分别生成这两个部分。只有当整个字符串与起始符号匹配时，即 *S* 是 *T[1，n]的成员时，句子才能由语法产生。*

考虑乔姆斯基范式中的一个示例语法:

```
*NP   -->  Det | Nom*
*Nom  -->  AP | Nom*
*AP  -->  Adv | A*
*Det  -->  a | an*
*Adv  -->  very | extremely*
*AP   -->  heavy | orange | tall*
*A   -->  heavy | orange | tall | muscular*
*Nom -->  book | orange | man*
```

现在考虑短语“**一本非常重的橙色书**”:

```
a(1) very(2) heavy (3) orange(4) book(5)
```

让我们开始根据上面描述的规则，从左到右、从下到上填充表格:

<figure class="table">

|   | 

1
a

 | 

2
非常

 | 

3
重

 | 

4
橙色

 | 

5
书

 |
| --- | --- | --- | --- | --- | --- |
| 

1
a

 | 方阵函数 | – | – | 公证人 | 公证人 |
| 

2
非常

 |   | 副词 | 美国联合通讯社(Associated Press) | Nom | Nom |
| 

3
重

 |   |   | 美联社 | Nom | Nom |
| 

4
橙色

 |   |   |   | 名称，a，AP | Nom |
| 

5
书

 |   |   |   |   | Nom |

表格按以下方式填写:

1.  T[1，1]= { Det } as Det –> a 是语法规则之一。
2.  T[2，2]= { Adv } as Adv–>非常是语法规则之一。
3.  T[1，2] = {}，因为没有观察到匹配规则。
4.  T[3，3] = {A，AP } as A–>非常和 AP –>非常是语法规则。
5.  T[2，3]= { AP } as AP–> Adv(T[2，2]) A (T[3，3])是语法规则。
6.  T[1，3] = {}，因为没有观察到匹配规则。
7.  T[4，4] = {Nom，A，AP}作为 Nom –> orange 和 A –> orange 和 AP –> orange 是语法规则。
8.  T[3，4]= { Nom } as Nom –> AP(T[3，3]) Nom (T[3，4])是语法规则。
9.  T[2，4]= { Nom } as Nom –> AP(T[2，3]) Nom (T[4，4])是语法规则。
10.  T[1，4]= { NP } as NP–> Det(T[1，1]) Nom (T[2，4])是语法规则。
11.  T[5，5] = {Nom}作为 Nom –>书是语法规则。
12.  T[4，5]= { Nom } as Nom–> AP(T[4，4]) Nom (T[5，5])是语法规则。
13.  T[3，5]= { Nom } as Nom –> AP(T[3，3]) Nom (T[4，5])是语法规则。
14.  T[2，5]= { Nom } as Nom –> AP(T[2，3]) Nom (T[4，5])是语法规则。
15.  T[1，5]= { NP } as NP–> Det(T[1，1]) Nom (T[2，5])是语法规则。

我们看到 T[1][5]有 **NP** ，开始符号，这意味着这个短语是语法 *G* 语言的一个成员。

这个短语的解析树如下所示:

![](img/7f342f65c102eb4737142ac6268ef681.png)

让我们看另一个例子短语，“**一个非常高的极度肌肉发达的男人”:**

```
a(1) very(2) tall(3) extremely(4) muscular(5) man(6)
```

我们现在将使用 CYK 算法来查找这个字符串是否是语法 *G:* 的成员

<figure class="table">

|   | 

1
a

 | 

2
非常

 | 

3
高

 | 

4
极

 | 

5
肌肉发达

 | 

6
男人

 |
| --- | --- | --- | --- | --- | --- | --- |
| 

1
a

 | 方阵函数 | – | – | – | – | 公证人 |
| 

2
非常

 |   | 副词 | 美国联合通讯社(Associated Press) | – | – | Nom |
| 

3
高

 |   |   | 美联社，阿 | – | –

 | Nom |
| 

4
极

 |   |   |   | 副词 | 美国联合通讯社(Associated Press) | Nom |
| 

5
肌肉发达

 |   |   |   |   | A | – |
| 

6
男人

 |   |   |   |   |   | Nom |

我们看到 T[1][6]有 **NP** ，开始符号，这意味着这个短语是语法 g 语言的一员。

以下是上述算法的实现:

## C++

```
// C++ implementation for the
// CYK Algorithm

#include<bits/stdc++.h>
using namespace std;

// Non-terminals symbols
vector<string> terminals,non_terminals;

// Rules of the grammar
unordered_map<string,vector<vector<string>>> R;

// function to perform the CYK Algorithm
void cykParse(vector<string> w)
{
  int n = (int)w.size();

  // Initialize the table
  map<int,map<int,set<string>>> T;

  // Filling in the table
  for(int j=0;j<n;j++)
  {

    // Iterate over the rules
    for(auto x:R)
    {
      string lhs = x.first;
      vector<vector<string>> rule = x.second;

      for(auto rhs:rule)
      {

        // If a terminal is found
        if(rhs.size() == 1 && rhs[0] == w[j])
          T[j][j].insert(lhs);
      }

    }
    for(int i=j;i>=0;i--)
    {

      // Iterate over the range from i to j
      for(int k = i;k<=j;k++)
      {

        // Iterate over the rules
        for(auto x:R)
        {
          string lhs = x.first;
          vector<vector<string>> rule = x.second;

          for(auto rhs:rule)
          {
          // If a terminal is found
            if(rhs.size()==2 && T[i][k].find(rhs[0])!=T[i][k].end() && T[k+1][j].find(rhs[1])!=T[k+1][j].end())
              T[i][j].insert(lhs);
          }

        }
      }
    }
  }

  // If word can be formed by rules
  // of given grammar
  if(T[0][n-1].size()!=0)
    cout << "True\n";
  else
    cout << "False\n";
}

// Driver Code
int main()
{
  // terminal symbols
  terminals = {"book", "orange", "man",
             "tall", "heavy",
             "very", "muscular"};

  // non terminal symbols
  non_terminals = {"NP", "Nom", "Det", "AP",
                  "Adv", "A"};

  // Rules
  R["NP"]={{"Det", "Nom"}};
  R["Nom"]= {{"AP", "Nom"}, {"book"},
             {"orange"}, {"man"}};
  R["AP"] = {{"Adv", "A"}, {"heavy"},
            {"orange"}, {"tall"}};
  R["Det"] = {{"a"}};
  R["Adv"] = {{"very"}, {"extremely"}};
  R["A"] = {{"heavy"}, {"orange"}, {"tall"},
           {"muscular"}};

  // Given String
  vector<string> w = {"a", "very", "heavy", "orange", "book"};

  // Function Call
  cykParse(w);

  return 0;
}
```

## 蟒蛇 3

```
# Python implementation for the
# CYK Algorithm

# Non-terminal symbols
non_terminals = ["NP", "Nom", "Det", "AP",
                  "Adv", "A"]
terminals = ["book", "orange", "man",
             "tall", "heavy",
             "very", "muscular"]

# Rules of the grammar
R = {
     "NP": [["Det", "Nom"]],
     "Nom": [["AP", "Nom"], ["book"],
             ["orange"], ["man"]],
     "AP": [["Adv", "A"], ["heavy"],
            ["orange"], ["tall"]],
     "Det": [["a"]],
     "Adv": [["very"], ["extremely"]],
     "A": [["heavy"], ["orange"], ["tall"],
           ["muscular"]]
    }

# Function to perform the CYK Algorithm
def cykParse(w):
    n = len(w)

    # Initialize the table
    T = [[set([]) for j in range(n)] for i in range(n)]

    # Filling in the table
    for j in range(0, n):

        # Iterate over the rules
        for lhs, rule in R.items():
            for rhs in rule:

                # If a terminal is found
                if len(rhs) == 1 and \
                rhs[0] == w[j]:
                    T[j][j].add(lhs)

        for i in range(j, -1, -1):  

            # Iterate over the range i to j + 1  
            for k in range(i, j + 1):    

                # Iterate over the rules
                for lhs, rule in R.items():
                    for rhs in rule:

                        # If a terminal is found
                        if len(rhs) == 2 and \
                        rhs[0] in T[i][k] and \
                        rhs[1] in T[k + 1][j]:
                            T[i][j].add(lhs)

    # If word can be formed by rules
    # of given grammar
    if len(T[0][n-1]) != 0:
        print("True")
    else:
        print("False")

# Driver Code

# Given string
w = "a very heavy orange book".split()

# Function Call
cykParse(w)
```

**Output:** 

```
True
```

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(N <sup>2</sup> )*

</figure>

</figure>

</figure>