# strcpy, srtcat, strlen, strcmp
### strcpy
````c
void strcpy(char *dest, const char *src)
{
    if (dest == NULL || src == NULL) return;
    
    while (*src != '\0') {
        *dest = *src;
        dest++;
        src++;
    }
````
### strcat
````C
void strcat(char *dest, const char *src)
{
    char *p = dest;
    int loc = 0;

    if (dest == NULL || src == NULL) return;

    while(*(p++) != '\0') loc++;
    
    while(*src != '\0') {
        dest[loc] = *src;
        src++;
        loc++;
    }
}
````
### strlen
````C
int strlen(const char *str)
{
    int len = 0;
    while (*str++ != '\0') len++;
    
    return len;
}
````
### strcmp
````C
int strcmp(const char *a, const char *b) {
    while (*a && (*a == *b)) {
        a++;
        b++;
    }
    return *a - *b;
}
````
### binary search
````c
void binary_search(int *arr, int len, int target)
{
    int right = len - 1, left = 0, mid = 0;
    
    while (right >= left) {
        mid = (right + left) / 2;
        if (arr[mid] < target) {
            left = mid + 1;
        } else if (arr[mid] > target) {
            right = mid - 1;
        } else if (arr[mid] == target) {
            printf("Found it\n");
            return;
        }
    }
    
    printf("Not found\n");
}
````
# Linked list
### Middle of the Linked List(Leetcode876)
````C
class Solution {
public:
    ListNode* middleNode(ListNode* head) {
        ListNode *slow=head;
        ListNode *fast=head;
        while(fast!=nullptr && fast->next!=nullptr){
            fast=fast->next->next;
            slow=slow->next;
        }
        return slow;
    }
};
````
### Linked List Cycle(Leetcode141)
````C
class Solution {
public:
    bool hasCycle(ListNode *head) {
        if(head==NULL){
            return false;
        }
        ListNode *slow=head;
        ListNode *fast=head;
        while(fast->next!=NULL &&fast->next->next!=NULL){
            fast=fast->next->next;
            slow=slow->next;
            if(fast==slow){
                return true;
            }
        }
        return false;
    }
};
````
### Remove Duplicates from Sorted List(Leetcode83)
````C
class Solution {
public:
    ListNode* deleteDuplicates(ListNode* head) {
        ListNode *current=head;
        ListNode *pre=NULL;
        while(current!=NULL && current->next!=NULL){
            if(current->val==current->next->val){
                current->next=current->next->next;
            }
            else{
                current=current->next;
            }
        }
        return head;
    }
};
````
### Reverse Linked List(Leetcode206)
````C
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode *current=head;
        ListNode *prev=NULL;
        ListNode *next=NULL;
        while(current!=nullptr){
            next=current->next;
            current->next=prev;
            prev=current;
            current=next;
        }
        return prev;
    }
};
````
### Merge Two Sorted Lists(Leetcode21)
````C
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
        ListNode dummy(0);
        ListNode *current = &dummy;

        while(list1 && list2){
            if(list1->val <list2->val){
                current->next = list1;
                list1 = list1->next;
            }
            else{
                current->next =list2;
                list2 = list2->next;
            }
            current=current->next;
        }
        if(!list1){
            current->next=list2;
        }
        else{
            current->next=list1;
        }
        return dummy.next;
    }
};
````
# Linked list implement queue
````C
struct linked_list {
    linked_list *next;
    uint8_t data;
};

struct Queue {
    linked_list *head;
    linked_list *tail;
    int size; // 來跟蹤隊列的大小
};
void initQueue(struct Queue *q) {
    q->head = NULL;
    q->tail = NULL;
    q->size = 0;
}
void push(Queue *q, uint8_t data) {
    linked_list *new_node = (linked_list *)malloc(sizeof(linked_list));
    if (new_node == NULL) {
        perror("Failed to allocate memory");
        return;
    }
    new_node->data = data;
    new_node->next = NULL;
    
    if (q->tail != NULL) {
        q->tail->next = new_node;
    }
    q->tail = new_node;
    
    if (q->head == NULL) {
        q->head = new_node;
    }
    
    q->size++;
}
void pop(struct Queue *q) {
    if (q->head == NULL) {
        printf("Queue is empty\n");
        return;
    }

    struct linked_list *temp = q->head;
    q->head = q->head->next;
    
    if (q->head == NULL) {
        q->tail = NULL;
    }
    
    free(temp);
    q->size--;
}
uint8_t getFront(struct Queue *q) {
    if (q->head == NULL) {
        printf("Queue is empty\n");
        return 0; // 或者返回一個錯誤值
    }
    return q->head->data;
}
uint8_t getRear(struct Queue *q) {
    if (q->tail == NULL){
        printf("Queue is empty\n");
        return 0; // 或者返回一個錯誤值
    }
    return q->tail->data;
}
bool isEmpty(struct Queue *q) {
    return q->head == NULL;
}
size_t getSize(struct Queue *q) {
    return q->size;
}
int main() {
    struct Queue q;
    initQueue(&q);

    push(&q, 10);
    push(&q, 20);
    push(&q, 30);

    printf("Front: %u\n", getFront(&q)); // 應該輸出 10
    printf("Rear: %u\n", getRear(&q));   // 應該輸出 30
    printf("Size: %zu\n", getSize(&q));  // 應該輸出 3

    pop(&q);
    printf("Front after pop: %u\n", getFront(&q)); // 應該輸出 20
    printf("Size after pop: %zu\n", getSize(&q));  // 應該輸出 2

    // 釋放剩餘的內存
    while (!isEmpty(&q)) {
        pop(&q);
    }

    return 0;
}

````
# Linked list sorting
### quick sort
````C
//from:https://www.geeksforgeeks.org/quicksort-on-singly-linked-list/
struct Node { 
    int data; 
    struct Node* next; 
}; 
struct Node* partition(struct Node* first, struct Node* last) 
{ 
    // Get first node of given linked list 
    struct Node* pivot = first; 
    struct Node* front = first; 
    int temp = 0; 
    while (front != NULL && front != last) { 
        if (front->data < last->data) { 
            pivot = first; 
  
            // Swapping  node values 
            temp = first->data; 
            first->data = front->data; 
            front->data = temp; 
  
            // Visiting the next node 
            first = first->next; 
        } 
  
        // Visiting the next node 
        front = front->next; 
    } 
  
    // Change last node value to current node 
    temp = first->data; 
    first->data = last->data; 
    last->data = temp; 
    return pivot; 
} 
  
// Performing quick sort in  the given linked list 
void quick_sort(struct Node* first, struct Node* last) 
{ 
    if (first == last) { 
        return; 
    } 
    struct Node* pivot = partition(first, last); 
  
    if (pivot != NULL && pivot->next != NULL) { 
        quick_sort(pivot->next, last); 
    } 
  
    if (pivot != NULL && first != pivot) { 
        quick_sort(first, pivot); 
    } 
} 
````

