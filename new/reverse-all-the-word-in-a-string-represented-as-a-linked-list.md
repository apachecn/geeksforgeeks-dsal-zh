# 反转表示为链表

的字符串中的所有单词

给定一个表示句子S的链表，使得每个节点代表一个字母，任务是在不反转单个单词的情况下反转该句子。
例如，对于给定的句子“我爱极客，极客”，[链表](http://www.geeksforgeeks.org/data-structures/linked-list/)表示为：
I- >-> l- > o -> v- > e- >-> G- > e- > e- > k- > s- >-> f- > o- > r- >-> G- > e- > e- > k- > s

**示例：**

> **输入：**我爱极客，极客
> **输出：**极客，极客爱我
> 
> **输入：**练习使人完美
> **输出：**完美练习器使人

**方法：**的想法是从头开始导航链接列表。 每次遇到空格时，请将空格交换到该单词的开头。 重复此步骤，直到到达最后一个节点。 最后，将第一个单词的最后一个字母设置为指向null，它将成为最后一个节点，并不断更改指针。

下面是该方法的实现：

## 爪哇

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// Linked List Implementation``public` `class` `Node {` `public` `Node(` `char` `data, Node next)` `{` `Data = data;` `Next = next;` `}` `public` `char` `Data;` `public` `Node Next;``}``class` `GFG {` `// Function to create a linked list` `// from the given String` `private` `static` `Node CreateLinkedList(String s)` `{` `Node header =` `null` `;` `Node temp =` `null` `;` `// Generates characters from the given string` `for` `(` `int` `i =` `0` `; i < s.length(); i++) {` `char` `c = s.charAt(i);` [HT G59] `new` `Node(c,` `null` `);` `if` `(header ==` `null` `) {` `header = node;` `temp = header;` `}` `else` `{` `temp.Next = node;` `temp = temp.Next;` `}` `}` `return` `header;` `}` `// Function to reverse the words` `// Assume str = "practice makes man perfect"` `// to understand proper understanding of the code` `private` `static` `Node Reverse(Node header)` `{` `if` `(header ==` `null` `)` `return` `header;` `Node wordStartPosition =` `null` `;` `Node endOfSentence =` `null` `;` `Node sentenceStartPosition =` `null` `;` `// Initialize wordStartPosition to header` `// ie. node 'p' first letter of the word 'practice'` `wordStartPosition = header;` `// Navigate the linked list until` `// a space(' ') is found or header is null` `//(this is for handing if there is` `// only one word in the given sentence)` `while` `(header !=` `null` `&& header.Data !=` `' '` `) {` `// Keep track the previous node.` `// This will become the` `// last node of the linked list` `endOfSentence = header;` `// Keep moving to the next node` `header = header.Next;` `}` `// After the above while loop,` `// endOfSentence points to` `// the last letter 'e'of word 'practice'` `// header points to the space(' ')` `// which is next to word 'practice'` `// If header is null then there is only` `// one word in the given sentance` `// so set header to the`]  `// first/wordStartPosition node and return.` `if` `(header ==` `null` `) {` `header = wordStartPosition;` `return` `header;` `}` `do` `{` `// Swapping the space ie.` `// convert 'practice<space>' to` `//'<space>practice'` `// store the node which is next to space(' ')` `// 'm' which is the first letter of the word 'make'` `Node temp = header.Next;` `header.Next = wordStartPosition;` `wordStartPosition = header;` `header = temp;` `Node prev =` `null` `;` `// Setting sentenceStartPosition to node 'm'` `//(first letter of the word 'make')` `sentenceStartPosition = header;` `// Again Navigate the linked list until` `// a space(' ') is found or` `// header == null end of the linked list` `while` `(header !=` `null` `&& header.Data !=` `' '` `) {` `prev = header;` `header = header.Next;` `}` `// When the next space is found,` `// change the pointer to point the previous space` `// ie. the word is being converted to` `// "m->a->k->e->s-> ->p->r->a->c->t->i->c->e"` `prev.Next = wordStartPosition;` `// Newly found space will point to` `//'m' first letter of the word 'make'` `wordStartPosition = sentenceStartPosition;`​​ `if` `(header ==` `null` `)` `break` `;` `// Repeat the loop until` `// the end of the linked list is reached` `}` `while` `(header !=` `null` `);` `header = sentenceStartPosition;` `// Set the last node's next to null` `// ie. ->m->a->k->e->s-> ->p->r->a->->c->t->i->c->e->null` `endOfSentence.Next =` `null` `;` `return` `header;` `}` `// Function to print the Linked List` `private` `static` `void` `PrintList(Node Header)` `{` `Node temp = Header;` `// Navigate till the end and print the data in each node` `while` `(temp !=` `null` `) {` `System.out.print(temp.Data);` `temp = temp.Next;` `}` `}` `// Driver code` `public` `static` `void` `main(String[] args)` `{` `String s =` `"practice makes a man perfect"` `;` `// Convert given string to a linked list` `// with character as data in each node` `Node header = CreateLinkedList(s);` `System.out.println(` `"Before:"` `);` `PrintList(header);` `header = Reverse(header);` `System.out.println(` `"\nAfter:"` `);` `PrintList(header);`]  `}``}` |

*chevron_right**filter_none*