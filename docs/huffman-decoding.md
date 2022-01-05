# 霍夫曼解码

> 原文:[https://www.geeksforgeeks.org/huffman-decoding/](https://www.geeksforgeeks.org/huffman-decoding/)

我们在之前的文章中讨论过[霍夫曼编码](https://www.geeksforgeeks.org/greedy-algorithms-set-3-huffman-coding/)。本文讨论后解码。

示例:

```
Input Data : AAAAAABCCCCCCDDEEEEE
Frequencies : A: 6, B: 1, C: 6, D: 2, E: 5
Encoded Data : 
0000000000001100101010101011111111010101010
Huffman Tree: '#' is the special character used
              for internal nodes as character field
              is not needed for internal nodes. 
               #(20)
             /       \
        #(12)         #(8)
     /      \        /     \
    A(6)     C(6) E(5)     #(3)
                         /     \
                       B(1)    D(2)  
Code of 'A' is '00', code of 'C' is '01', ..
Decoded Data : AAAAAABCCCCCCDDEEEEE

Input Data : GeeksforGeeks
Character With there Frequencies
e 10, f 1100, g 011, k 00, o 010, r 1101, s 111
Encoded Huffman data :
01110100011111000101101011101000111
Decoded Huffman Data
geeksforgeeks

```

为了解码编码数据，我们需要霍夫曼树。我们遍历二进制编码的数据。要查找对应于当前位的字符，我们使用以下简单步骤。

1.  我们从根开始，一直到找到一片叶子。
2.  如果当前位为 0，我们移动到树的左节点。
3.  如果该位为 1，我们移动到树的右节点。
4.  如果在遍历过程中，我们遇到一个叶节点，我们打印该特定叶节点的字符，然后从步骤 1 开始再次继续编码数据的迭代。

下面的代码将一个字符串作为输入，对其进行编码并保存在变量 encodedString 中。然后它解码并打印原始字符串。

下面的代码执行给定输入数据的完全霍夫曼编码和解码。

```
// C++ program to encode and decode a string using
// Huffman Coding.
#include <bits/stdc++.h>
#define MAX_TREE_HT 256
using namespace std;

// to map each character its huffman value
map<char, string> codes;

// to store the frequency of character of the input data
map<char, int> freq;

// A Huffman tree node
struct MinHeapNode
{
    char data;             // One of the input characters
    int freq;             // Frequency of the character
    MinHeapNode *left, *right; // Left and right child

    MinHeapNode(char data, int freq)
    {
        left = right = NULL;
        this->data = data;
        this->freq = freq;
    }
};

// utility function for the priority queue
struct compare
{
    bool operator()(MinHeapNode* l, MinHeapNode* r)
    {
        return (l->freq > r->freq);
    }
};

// utility function to print characters along with
// there huffman value
void printCodes(struct MinHeapNode* root, string str)
{
    if (!root)
        return;
    if (root->data != '{content}apos;)
        cout << root->data << ": " << str << "\n";
    printCodes(root->left, str + "0");
    printCodes(root->right, str + "1");
}

// utility function to store characters along with
// there huffman value in a hash table, here we
// have C++ STL map
void storeCodes(struct MinHeapNode* root, string str)
{
    if (root==NULL)
        return;
    if (root->data != '{content}apos;)
        codes[root->data]=str;
    storeCodes(root->left, str + "0");
    storeCodes(root->right, str + "1");
}

// STL priority queue to store heap tree, with respect
// to their heap root node value
priority_queue<MinHeapNode*, vector<MinHeapNode*>, compare> minHeap;

// function to build the Huffman tree and store it
// in minHeap
void HuffmanCodes(int size)
{
    struct MinHeapNode *left, *right, *top;
    for (map<char, int>::iterator v=freq.begin(); v!=freq.end(); v++)
        minHeap.push(new MinHeapNode(v->first, v->second));
    while (minHeap.size() != 1)
    {
        left = minHeap.top();
        minHeap.pop();
        right = minHeap.top();
        minHeap.pop();
        top = new MinHeapNode('{content}apos;, left->freq + right->freq);
        top->left = left;
        top->right = right;
        minHeap.push(top);
    }
    storeCodes(minHeap.top(), "");
}

// utility function to store map each character with its
// frequency in input string
void calcFreq(string str, int n)
{
    for (int i=0; i<str.size(); i++)
        freq[str[i]]++;
}

// function iterates through the encoded string s
// if s[i]=='1' then move to node->right
// if s[i]=='0' then move to node->left
// if leaf node append the node->data to our output string
string decode_file(struct MinHeapNode* root, string s)
{
    string ans = "";
    struct MinHeapNode* curr = root;
    for (int i=0;i<s.size();i++)
    {
        if (s[i] == '0')
           curr = curr->left;
        else
           curr = curr->right;

        // reached leaf node
        if (curr->left==NULL and curr->right==NULL)
        {
            ans += curr->data;
            curr = root;
        }
    }
    // cout<<ans<<endl;
    return ans+'\0';
}

// Driver program to test above functions
int main()
{
    string str = "geeksforgeeks";
    string encodedString, decodedString;
    calcFreq(str, str.length());
    HuffmanCodes(str.length());
    cout << "Character With there Frequencies:\n";
    for (auto v=codes.begin(); v!=codes.end(); v++)
        cout << v->first <<' ' << v->second << endl;

    for (auto i: str)
        encodedString+=codes[i];

    cout << "\nEncoded Huffman data:\n" << encodedString << endl;

    decodedString = decode_file(minHeap.top(), encodedString);
    cout << "\nDecoded Huffman Data:\n" << decodedString << endl;
    return 0;
}
```

输出:

```
Character With there Frequencies
e 10
f 1100
g 011
k 00
o 010
r 1101
s 111

Encoded Huffman data 
01110100011111000101101011101000111

Decoded Huffman Data
geeksforgeeks

```

**比较输入文件大小和输出文件大小:**
比较输入文件大小和霍夫曼编码的输出文件。我们可以用一种简单的方法计算输出数据的大小。假设我们的输入是一个字符串“geeksforgeeks”，存储在一个文件 input.txt 中
**输入文件大小:**

```
Input: "geeksforgeeks"
Total number of character i.e. input length: 13
Size: 13 character occurrences * 8 bits = 104 bits or 13 bytes.

```

**输出文件大小:**

```
Input: "geeksforgeeks"
------------------------------------------------
Character |  Frequency |  Binary Huffman Value |
------------------------------------------------
   e      |      4     |         10            |
   f      |      1     |         1100          |   
   g      |      2     |         011           |
   k      |      2     |         00            |
   o      |      1     |         010           |
   r      |      1     |         1101          |
   s      |      2     |         111           |
------------------------------------------------

So to calculate output size:
e: 4 occurrences * 2 bits = 8 bits
f: 1 occurrence  * 4 bits = 4 bits
g: 2 occurrences * 3 bits = 6 bits
k: 2 occurrences * 2 bits = 4 bits
o: 1 occurrence  * 3 bits = 3 bits
r: 1 occurrence  * 4 bits = 4 bits
s: 2 occurrences * 3 bits = 6 bits

Total Sum: 35 bits approx 5 bytes

```

因此，我们可以看到，在对数据进行编码后，我们保存了大量数据。
上述方法也可以帮助我们确定 N 的值，即编码数据的长度。

本文由 **[【哈什特·西德瓦】](https://practice.geeksforgeeks.org/user-profile.php?user=Harshit%20Sidhwa)** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。