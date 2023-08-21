#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* next;
};

typedef struct Node Node;

Node* createNode(int value) {
    Node* newNode = (Node*)malloc(sizeof(Node));
    newNode->data = value;
    newNode->next = NULL;
    return newNode;
}

void insertAtEnd(Node** head, int value) {
    Node* newNode = createNode(value);
    if (*head == NULL) {
        *head = newNode;
        return;
    }

    Node* current = *head;
    while (current->next != NULL) {
        current = current->next;
    }
    current->next = newNode;
}

void displayList(Node* head) {
    Node* current = head;
    while (current != NULL) {
        printf("%d -> ", current->data);
        current = current->next;
    }
    printf("NULL\n");
}

void modifyData(Node* head, int oldValue, int newValue) {
    Node* current = head;
    while (current != NULL) {
        if (current->data == oldValue) {
            current->data = newValue;
            return;
        }
        current = current->next;
    }
    printf("Data not found in the linked list.\n");
}

int main() {
    Node* head = NULL;
    int choice, data, oldValue, newValue;

    do {
        printf("1. Insert data\n");
        printf("2. Modify data\n");
        printf("3. Display list\n");
        printf("4. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                printf("Enter data to insert: ");
                scanf("%d", &data);
                insertAtEnd(&head, data);
                break;

            case 2:
                printf("Enter the old data value to modify: ");
                scanf("%d", &oldValue);
                printf("Enter the new data value: ");
                scanf("%d", &newValue);
                modifyData(head, oldValue, newValue);
                break;

            case 3:
                printf("Linked List: ");
                displayList(head);
                break;

            case 4:
                printf("Exiting the program.\n");
                break;

            default:
                printf("Invalid choice. Please enter a valid option.\n");
        }
    } while (choice != 4);

    return 0;
}
