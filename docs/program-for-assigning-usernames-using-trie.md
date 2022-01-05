# 使用 Trie 分配用户名的程序

> 原文:[https://www . geesforgeks . org/program-for-assignment-used-trie/](https://www.geeksforgeeks.org/program-for-assigning-usernames-using-trie/)

假设有 n 个用户的队列，您的任务是为他们分配一个用户名。该系统的工作方式如下。每个用户都喜欢以字符串形式登录，该字符串仅由小写字母和数字组成。用户名按以下顺序分配:s，s0，s1，S2…S11…意味着首先检查 s 是否可用如果 s 已经被占用请分配它检查 s0 是否空闲请分配它或者如果它被占用请检查 s1 等等…如果一个用户名被分配给一个用户，它将被队列中他之后的其他用户占用。
**例** :

> **输入**:name[]= { ABC，bcd }
> T3】输出:user _ name[]= { ABC BCD }
> **输入**:name[]= { ABC，BCD，abc}
> **输出**:user _ name[]= { ABC BCD ABC 0 }
> **输入**:name[]= { geek，geek0，geek1， geek }
> **Output**:user _ name【】= { geek0 geek1 geek2 }
> 对于第一个用户 geek 是免费的，所以对第二个和第三个用户分配给他类似，但是对于第四个用户 geek 不是免费的，所以我们会检查 geek 0，但它也不是免费的，然后我们会检查 geek 1，但它也不是免费的，然后我们会检查 geek 2，它是免费的，所以它被分配给他。

我们使用 [Trie](https://www.geeksforgeeks.org/trie-insert-and-search/) 来解决这个问题。我们不使用通常的有 26 个子节点的 Trie，而是节点有 36 个子节点的 Trie 26 个字母(a-z)和 10 个数字(0-9)。除此之外，Trie 的每个节点都有 bool 变量，当插入以该节点结束的字符串时，该变量将变为 true，还有一个 int 变量，让我们称之为 add，它最初为-1，假设字符串是 geek，这个 int 变量等于-1，这意味着我们将直接返回 geek，因为这是第一次被要求，但假设它是 12，这意味着字符串 geek，geek0…..极客 12 已经出现在 Trie 中。
步骤
步骤 1:保持如上所述的 Trie。
第二步:对于每个名字， 检查用户给出的字符串是否不在 Trie 中，然后返回相同的字符串，否则从 i=add+1 开始(add 在上面讨论过) 并开始检查我们是否将 I 与输入字符串连接在一起是否存在于 Trie 中如果它不存在，则返回它并设置 add=i 以及将其插入 Trie 中否则递增 i
假设字符串是 geek 和 i=5 检查 geek5 是否在 Trie 中如果它不存在则返回 geek5 为 geek 设置 add = 5 在 Trie 中插入 geek5 否则如果它不存在，对 geek6 执行相同的步骤，直到您找到不存在于 Trie 中的字符串。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to assign usernames to users
#include <bits/stdc++.h>
using namespace std;

#define MAX_CHAR 26

struct additional {

    // is checks if the current node is
    // leaf node or not
    bool is;

    // add counts number of concatenations
    // of string are present in Trie
    int add;
};

// represents Trie node
struct Trie {

    // MAX_CHAR character children
    Trie* character[MAX_CHAR];

    // 10 numbers (from 0 to 9)
    Trie* number[10];

    // one additional struct children
    additional a;
};

// function to get new node
Trie* getnew()
{
    // initialising the Trie node
    Trie* node = new Trie;
    node->a.is = false;
    node->a.add = -1;
    for (int i = 0; i < MAX_CHAR; i++)
        node->character[i] = NULL;
    for (int i = 0; i < 10; i++)
        node->number[i] = NULL;
    return node;
}

// inserting a string into Trie
void insert(Trie*& head, string s)
{
    Trie* curr = head;
    for (int i = 0; i < s.length(); i++) {
        if (s[i] - 'a' < 0) {
            if (curr->number[s[i] - '0'] == NULL) {
                curr->number[s[i] - '0'] = getnew();
            }
            curr = curr->number[s[i] - '0'];
        }
        else {
            if (curr->character[s[i] - 'a'] == NULL)
                curr->character[s[i] - 'a'] = getnew();
            curr = curr->character[s[i] - 'a'];
        }
    }
    curr->a.is = true;
}

// returns the structure additional
additional search(Trie* head, string s)
{
    additional x;
    x.is = false;
    x.add = -1;

    // if head is null directly return additional x
    if (head == NULL)
        return x;
    Trie* curr = head;

    // checking if string is present or not and
    // accordingly returning x
    for (int i = 0; i < s.size(); i++) {
        if (s[i] - 'a' < 0) {
            curr = curr->number[s[i] - '0'];
        }
        else
            curr = curr->character[s[i] - 'a'];
        if (curr == NULL)
            return x;
    }
    x.is = curr->a.is;
    x.add = curr->a.add;
    return x;
}

// special function to update add variable to z
void update(Trie* head, string s, int z)
{
    Trie* curr = head;
    for (int i = 0; i < s.size(); i++) {
        if (s[i] - 'a' < 0)
            curr = curr->number[s[i] - '0'];
        else
            curr = curr->character[s[i] - 'a'];
    }
    curr->a.add = z;
}

void printUsernames(string username[], int n)
{
    // Initialing a Trie root
    Trie* head = getnew();

    // Assigning usernames one by one
    for (int i = 0; i < n; i++) {
        string s = username[i];
        additional x = search(head, s);

        // if string is not present directly return it
        if (x.is == false) {
            cout << s << endl;
            insert(head, s);
        }

        // to_string(x) converts integer x into string
        else if (x.is == true) {

            // start from x.add+1
            int y = x.add + 1;
            string x = s;

            // continuing searching the string
            // until a free username is found
            while (1 < 2) {

                // if free username is found
                if (search(head, x + to_string(y)).is == false) {

                    // print it insert it and update add
                    cout << x << y << endl;
                    insert(head, x + to_string(y));
                    update(head, s, y);
                    break;
                }
                // else increment y
                else if (search(head, x + to_string(y)).is == true)
                    y++;
            }
        }
    }
}

// driver function
int main()
{
    string name[] = { "geek", "geek0", "geek1", "geek" };
    int n = sizeof(name) / sizeof(name[0]);
    printUsernames(name, n);
    return 0;
}
```

**Output:** 

```
geek
geek0
geek1
geek2
```