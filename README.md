#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* next;
};

int countNodes(struct Node* head) {
    int count = 0;
    struct Node* temp = head;
    while (temp != NULL) {
        count++;
        temp = temp->next;
    }
    return count;
}

void insertAtStart(struct Node** head, int data) {
    struct Node* new_node = (struct Node*)malloc(sizeof(struct Node));
    new_node->data = data;
    new_node->next = *head;
    *head = new_node;
}

struct Node* reverseList(struct Node* head) {
    struct Node* prev = NULL;
    struct Node* current = head;
    struct Node* next = NULL;
    while (current != NULL) {
        next = current->next;
        current->next = prev;
        prev = current;
        current = next;
    }
    return prev;
}

void displayList(struct Node* head) {
    struct Node* temp = head;
    while (temp != NULL) {
        printf("%d -> ", temp->data);
        temp = temp->next;
    }
    printf("NULL\n");
}

int main() {
    struct Node* head = NULL;
    int choice, value;
    
    while (1) {
        printf("\n1. Insert at Start\n2. Reverse and Display\n3. Count Nodes\n4. Exit\n");
        printf("Enter choice: ");
        scanf("%d", &choice);
        
        if (choice == 1) {
            printf("Enter value: ");
            scanf("%d", &value);
            insertAtStart(&head, value);
        } else if (choice == 2) {
            printf("Original List:\n");
            displayList(head);
            struct Node* reversedHead = reverseList(head);
            printf("Reversed List:\n");
            displayList(reversedHead);
        } else if (choice == 3) {
            printf("Total Nodes: %d\n", countNodes(head));
        } else if (choice == 4) {
            break;
        } else {
            printf("Invalid choice.\n");
        }
    }
    return 0;
}
