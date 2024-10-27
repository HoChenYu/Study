# quick sort
````c
#include <iostream>
using namespace std;
void swap(int *, int *);
int partition(int *, int, int);
void quicksort(int *, int, int);
void printarray(int *,int);
int main(){
	int data[]={22,11,88,66,55,77,33,44,2,7,4,13,5};
	int arraysize=sizeof(data)/sizeof(data[0]);
	cout<<"first";
	printarray(data,arraysize);
	cout<<endl;
	quicksort(data,0,arraysize-1);
	cout<<"fineshed";
	printarray(data,arraysize);
	cout<<endl;
	return 0;
}
void printarray(int *a,int arraysize){
	for(int i=0;i<arraysize;i++){
		cout<<a[i];
	}
}
int partition(int *a, int left, int right) {
    int i = left, j = right;
    int pivot = a[left];

    while (i < j) {
        while (i < right && a[i] <= pivot) {
            i++;
        }
        while (j > left && a[j] > pivot) {
            j--;
        }
        if (i < j) {
            swap(&a[i], &a[j]);
        }
    }
    swap(&a[left], &a[j]);
    return j;
}
void quicksort(int *a,int left,int right){
	if(left<right){
		int partition_pos;
		partition_pos=partition(a,left,right);
		quicksort(a,left,partition_pos-1);
		quicksort(a,partition_pos+1,right);
	}
}
void swap(int *a, int *b){
	int tmp=*a;
	*a=*b;
	*b=tmp;
}
````
# binary search
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
# Linked list opertaion
````C
void insert_node(Node **start, int insert_after_value, int value)
{
	Node *current = *start; 
	
	while(current != NULL) {
		if(insert_after_value == current->data) {
			Node *new_node = (Node*)malloc(sizeof(Node));	
			new_node->data = value;
			new_node->next = NULL;
			if(current->next == NULL) {
				current->next = new_node;
				break;
			}
			else {
				new_node->next = current->next;
				current->next = new_node;
				break;
			}
		}
		current = current->next;
	}
}

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
typedef struct Node { 
    int data; 
    struct Node* next; 
} Node;

Node* partition(struct Node* left, struct Node* right) 
{ 
    struct Node* pivot = right; // 基準點為最後一個節點
    struct Node* current = left; // 當前節點指標
    struct Node* partitionNode = left; // 分區節點指標
    int temp; 

    while (current != right) { 
        if (current->data < pivot->data) { 
            // 交換 partitionNode 和 current 的數據
            temp = partitionNode->data; 
            partitionNode->data = current->data; 
            current->data = temp; 
  
            // 移動 partitionNode 到下一個節點
            partitionNode = partitionNode->next; 
        } 
  
        // 移動 current 到下一個節點
        current = current->next; 
    } 
  
    // 將基準點數據交換到 partitionNode 的位置
    temp = partitionNode->data; 
    partitionNode->data = pivot->data; 
    pivot->data = temp; 

    return partitionNode; // 返回新的基準點位置
}

void quicksort(Node *left, Node *right) {
    if (left == right) {
        return; // 使用 return 而不是 break
    }
    Node *pos = partition(left, right);
    if (pos != NULL && pos->next != NULL) {
        quicksort(pos->next, right);
    }
    if (pos != NULL && left != pos) {
        quicksort(left, pos);
    }
}

````
# shuffle the array
````C
    #include<stdio.h>
    #include<stdlib.h>
    #include<time.h>

    void shuffle(int *array, size_t n){
        //亂數前置
        srand(time(NULL));
        if (n > 1){
            size_t i;
            for (int i = n-1; i >= 0; i--){
                size_t j = rand() % (i+1);
                int t = array[j];
                array[j] = array[i];
                array[i] = t;
            }
        }
    }
````
