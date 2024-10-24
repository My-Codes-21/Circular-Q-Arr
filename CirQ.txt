#include <stdio.h>
#include <stdlib.h>

int choice, item, front = -1, rear = -1, QUEUE_SIZE;
int q[100]; // Static array for the circular queue (max size 100)

void insert_rear() {
    if ((rear + 1) % QUEUE_SIZE == front) {
        printf("Queue overflow\n");
        return;
    }

    printf("Enter the item to insert: ");
    scanf("%d", &item);

    if (front == -1) front = 0; // Initialize front if it's the first element

    rear = (rear + 1) % QUEUE_SIZE;
    q[rear] = item;

    printf("%d inserted into the queue\n", item);
}

int delete_front() {
    if (front == -1) {
        printf("Queue underflow\n");
        return -1;
    }

    int deleted_item = q[front];
    if (front == rear) {
        // Reset queue when it becomes empty
        front = rear = -1;
    } else {
        front = (front + 1) % QUEUE_SIZE;
    }

    return deleted_item;
}

void display() {
    if (front == -1) {
        printf("Queue is empty\n");
        return;
    }

    printf("Contents of the queue:\n");
    int i = front;
    while (i != rear) {
        printf("%d ", q[i]);
        i = (i + 1) % QUEUE_SIZE;
    }
    printf("%d\n", q[rear]);
}

int main() {
    printf("Enter the size of the circular queue (max 100): ");
    scanf("%d", &QUEUE_SIZE);

    if (QUEUE_SIZE > 100) {
        printf("Queue size exceeds maximum limit of 100.\n");
        exit(1);
    }

    while (1) {
        printf("\nCircular Queue Operations:\n");
        printf("1. Insert at rear\n");
        printf("2. Delete from front\n");
        printf("3. Display queue\n");
        printf("4. Exit\n");
        printf("Enter your choice: ");

        scanf("%d", &choice);

        switch (choice) {
            case 1:
                insert_rear();
                break;
            case 2: {
                int deleted_item = delete_front();
                if (deleted_item != -1) {
                    printf("%d deleted from the queue\n", deleted_item);
                }
                break;
            }
            case 3:
                display();
                break;
            case 4:
                exit(0);
            default:
                printf("Invalid choice!\n");
        }
    }

    return 0;
}
