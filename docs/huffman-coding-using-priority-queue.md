# 使用优先级队列的霍夫曼编码

> 原文:[https://www . geesforgeks . org/Huffman-coding-use-priority-queue/](https://www.geeksforgeeks.org/huffman-coding-using-priority-queue/)

**先决条件:** [贪婪算法|在 C++ STL 中设置 3(霍夫曼编码)](https://www.geeksforgeeks.org/huffman-coding-greedy-algo-3/)、 [priority_queue::push()和 priority _ queue::pop()](https://www.geeksforgeeks.org/priority_queuepush-priority_queuepop-c-stl/)
给定一个 char [数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**ch【】**和每个字符的频率为**freq【】**。任务是使用[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)为 **ch[]** 中的每个字符找到霍夫曼码。

**例**

> **输入:**【ch[]=【a】、【b】、【c】、【d】、【e】、【f】、【freq】=【5，9，12，13，16，45】
> **输出:**
> 【F6】【c101】
> 至 1100】

**进场:**

1.  将 **ch[]** 中所有映射到相应频率的字符 **freq[]** 推送到[优先队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)中。
2.  要创建霍夫曼树，从优先级队列中弹出两个节点。
3.  将[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)中的两个弹出节点指定为新节点的左右子节点。
4.  推送优先级队列中形成的新节点。
5.  重复以上所有步骤，直到[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)的大小变为 1。
6.  遍历霍夫曼树(其根是优先级队列中剩下的唯一节点)来存储[霍夫曼码](https://www.geeksforgeeks.org/huffman-coding-greedy-algo-3/)
7.  为 **ch[]** 中的每个字符打印所有存储的霍夫曼码。

下面是上述方法的实现:

## C++

```
// C++ Program for Huffman Coding
// using Priority Queue
#include <iostream>
#include <queue>
using namespace std;

// Maximum Height of Huffman Tree.
#define MAX_SIZE 100

class HuffmanTreeNode {
public:
    // Stores character
    char data;

    // Stores frequency of
    // the character
    int freq;

    // Left child of the
    // current node
    HuffmanTreeNode* left;

    // Right child of the
    // current node
    HuffmanTreeNode* right;

    // Initializing the
    // current node
    HuffmanTreeNode(char character,
                    int frequency)
    {
        data = character;
        freq = frequency;
        left = right = NULL;
    }
};

// Custom comparator class
class Compare {
public:
    bool operator()(HuffmanTreeNode* a,
                    HuffmanTreeNode* b)
    {
        // Defining priority on
        // the basis of frequency
        return a->freq > b->freq;
    }
};

// Function to generate Huffman
// Encoding Tree
HuffmanTreeNode* generateTree(priority_queue<HuffmanTreeNode*,
                              vector<HuffmanTreeNode*>,
                                             Compare> pq)
{

    // We keep on looping till
    // only one node remains in
    // the Priority Queue
    while (pq.size() != 1) {

        // Node which has least
        // frequency
        HuffmanTreeNode* left = pq.top();

        // Remove node from
        // Priority Queue
        pq.pop();

        // Node which has least
        // frequency
        HuffmanTreeNode* right = pq.top();

        // Remove node from
        // Priority Queue
        pq.pop();

        // A new node is formed
        // with frequency left->freq
        // + right->freq

        // We take data as '{content}apos;
        // because we are only
        // concerned with the
        // frequency
        HuffmanTreeNode* node = new HuffmanTreeNode('{content}apos;,
                                  left->freq + right->freq);
        node->left = left;
        node->right = right;

        // Push back node
        // created to the
        // Priority Queue
        pq.push(node);
    }

    return pq.top();
}

// Function to print the
// huffman code for each
// character.

// It uses arr to store the codes
void printCodes(HuffmanTreeNode* root,
                int arr[], int top)
{
    // Assign 0 to the left node
    // and recur
    if (root->left) {
        arr[top] = 0;
        printCodes(root->left,
                   arr, top + 1);
    }

    // Assign 1 to the right
    // node and recur
    if (root->right) {
        arr[top] = 1;
        printCodes(root->right, arr, top + 1);
    }

    // If this is a leaf node,
    // then we print root->data

    // We also print the code
    // for this character from arr
    if (!root->left && !root->right) {
        cout << root->data << " ";
        for (int i = 0; i < top; i++) {
            cout << arr[i];
        }
        cout << endl;
    }
}

void HuffmanCodes(char data[],
                  int freq[], int size)
{

    // Declaring priority queue
    // using custom comparator
    priority_queue<HuffmanTreeNode*,
                   vector<HuffmanTreeNode*>,
                   Compare>
        pq;

    // Populating the priority
    // queue
    for (int i = 0; i < size; i++) {
        HuffmanTreeNode* newNode
            = new HuffmanTreeNode(data[i], freq[i]);
        pq.push(newNode);
    }

    // Generate Huffman Encoding
    // Tree and get the root node
    HuffmanTreeNode* root = generateTree(pq);

    // Print Huffman Codes
    int arr[MAX_SIZE], top = 0;
    printCodes(root, arr, top);
}

// Driver Code
int main()
{
    char data[] = { 'a', 'b', 'c', 'd', 'e', 'f' };
    int freq[] = { 5, 9, 12, 13, 16, 45 };
    int size = sizeof(data) / sizeof(data[0]);

    HuffmanCodes(data, freq, size);
    return 0;
}
```

**Output:** 

```
f 0
c 100
d 101
a 1100
b 1101
e 111
```

**时间复杂度:** O(n*logn)其中 n 为唯一字符数
T3】辅助空间: O(n)