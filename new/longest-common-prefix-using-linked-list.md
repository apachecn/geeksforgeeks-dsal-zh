# 使用链表

的最长公共前缀

给定一组字符串，找到最长的公共前缀。

**示例：**

```
Input  : {“geeksforgeeks”, “geeks”, “geek”, “geezer”}
Output : "gee"

Input  : {"apple", "ape", "april"}
Output : "ap"

```

**先前的方法：** [逐字匹配](https://www.geeksforgeeks.org/longest-common-prefix-set-1-word-by-word-matching/)，[逐字符匹配](https://www.geeksforgeeks.org/longest-common-prefix-set-2-character-by-character-matching/)，[分而治之](https://www.geeksforgeeks.org/longest-common-prefix-set-3-divide-and-conquer/)，[二进制搜索](https://www.geeksforgeeks.org/longest-common-prefix-set-4-binary-search/)， [使用 Trie 数据结构](https://www.geeksforgeeks.org/longest-common-prefix-set-5-using-trie/)

以下是使用**链表**解决上述问题的算法。

*   使用第一个字符串的字符作为链接列表中的数据创建一个链接列表。

*   然后使用剩余的所有字符串一个接一个地循环访问链表，删除字符串用尽或链表用尽或字符不匹配之后的所有节点。

*   链表中的其余数据是所需的最长公共前缀。

下面是 C++中的实现

```

// C++ Program to find the longest common prefix 
// in an array of strings 
#include <bits/stdc++.h> 
using namespace std; 

// Structure for a node in the linked list 
struct Node { 
    char data; 
    Node* next; 
}; 

// Function to print the data in the linked list 
// Remaining nodes represent the longest common prefix 
void printLongestCommonPrefix(Node* head) 
{ 
    // If the linked list is empty there is  
    // no common prefix 
    if (head == NULL) { 
        cout << "There is no common prefix\n"; 
        return; 
    } 

    // Printing the longest common prefix 
    cout << "The longest common prefix is "; 
    while (head != NULL) { 
        cout << head->data; 
        head = head->next; 
    } 
} 

// Function that creates a linked list of characters 
// for the first word in the array of strings 
void Initialise(Node** head, string str) 
{ 
    // We calculate the length of the string 
    // as we will insert from the last to the  
    // first character 
    int l = str.length(); 

    // Inserting all the nodes with the characters 
    // using insert at the beginning technique 
    for (int i = l - 1; i >= 0; i--) { 
        Node* temp = new Node; 
        temp->data = str[i]; 
        temp->next = *head; 
        *head = temp; 
    } 

    // Since we have passed the address of the  
    // head node it is not required to return  
    // anything 
} 

// Function to delete all the nodes 
// from the unmatched node till the end of the  
// linked list 
void deleteNodes(Node* head) 
{ 
    // temp is used to facilitate the deletion of nodes 
    Node* current = head; 
    Node* next; 
    while (current != NULL) { 
        next = current->next; 
        free(current); 
        current = next; 
    } 
} 

// Function that compares the character of the string with 
// the nodes of the linked list and deletes all nodes after 
// the characters that do not match 
void longestCommonPrefix(Node** head, string str) 
{ 
    int i = 0; 

    // Use the pointer to the previous node to 
    // delete the link between the unmatched node  
    // and its prev node 
    Node* temp = *head; 
    Node* prev = *head; 
    while (temp != NULL) { 

        // If the current string finishes or if the 
        // the characters in the linked list do not match 
        // with the character at the corresponding position 
        // delete all the nodes after that. 
        if (str[i] == '\0' || temp->data != str[i]) { 

            // If the first node does not match then there 
            // is no common prefix 
            if (temp == *head) { 
                free(temp); 
                *head = NULL; 
            } 

            // Delete all the nodes starting from the 
            // unmatched node 
            else { 
                prev->next = NULL; 
                deleteNodes(temp); 
            } 
            break; 
        } 

        // If the character matches, move to next  
        // node and store the address of the current  
        // node in prev 
        prev = temp; 
        temp = temp->next; 
        i++; 
    } 
} 

int main() 
{ 
    string arr[] = { "geeksforgeeks", "geeks", "geek", "geezer", 
                     "geekathon" }; 
    int n = sizeof(arr) / sizeof(arr[0]); 

    struct Node* head = NULL; 

    // A linked list is created with all the characters 
    // of the first string 
    Initialise(&head, arr[0]); 

    // Process all the remaining strings to find the  
    // longest common prefix 
    for (int i = 1; i < n; i++) 
        longestCommonPrefix(&head, arr[i]); 

    printLongestCommonPrefix(head); 
} 

```

**Output:**

```
The longest common prefix is gee

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。