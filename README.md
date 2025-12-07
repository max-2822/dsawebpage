<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>C Program Display</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background: #f4f4f4;
            padding: 20px;
        }
        pre {
            background: #222;
            color: #0f0;
            padding: 20px;
            border-radius: 10px;
            overflow-x: auto;
        }
    </style>
</head>
<body>
    <h1>C Program Code</h1>
    <pre>
#include <stdio.h>
#include <stdlib.h>
struct Day {
    char *dayName;
    int date;
    char *activity;
};
void create(struct Day *day) {
    day->dayName = (char *)malloc(sizeof(char) * 20);
    day->activity = (char *)malloc(sizeof(char) * 100);
    printf("Enter the day name: ");
    scanf("%s", day->dayName);
    printf("Enter the date: ");
    scanf("%d", &day->date);
    printf("Enter the activity for the day: ");
    scanf(" %[^\n]s", day->activity);
}
void read(struct Day *calendar, int size) {
    for (int i = 0; i < size; i++) {
        printf("Enter details for Day %d:\n", i + 1);
        create(&calendar[i]);
    }
}
void display(struct Day *calendar, int size) {
    printf("\nWeek's Activity Details:\n");
    for (int i = 0; i < size; i++) {
        printf("Day %d:\n", i + 1);
        printf("Day Name: %s\n", calendar[i].dayName);
        printf("Date: %d\n", calendar[i].date);
        printf("Activity: %s\n", calendar[i].activity);
        printf("\n");
    }
}
void freeMemory(struct Day *calendar, int size) {
    for (int i = 0; i < size; i++) {
        free(calendar[i].dayName);
        free(calendar[i].activity);
    }
}
int main() {
    int size;
    printf("Enter the number of days in the week: ");
    scanf("%d", &size);
    struct Day *calendar = (struct Day *)malloc(sizeof(struct Day) * size);
    if (calendar == NULL) {
        printf("Memory allocation failed. Exiting program.\n");
        return 1;
    }
    read(calendar, size);
    display(calendar, size);
    freeMemory(calendar, size);
    free(calendar);
    return 0;
}
    </pre>
    <h1>C Program Code 2</h1>
    <pre>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#define MAX 5
int stack[MAX];
int top = -1;
void push(int element);
int pop();
void display();
void checkPalindrome();
void isOverflow();
void isUnderflow();
int main() {
    int choice, element;
    while (1) {
        printf("
--- STACK OPERATIONS MENU ---
");
        printf("1. Push an element onto stack
");
        printf("2. Pop an element from stack
");
        printf("3. Check Palindrome using Stack
");
        printf("4. Demonstrate Overflow and Underflow
");
        printf("5. Display Stack
");
        printf("6. Exit
");
        printf("Enter your choice: ");
        scanf("%d", &choice);
        switch (choice) {
        case 1:            printf("Enter element to push: ");
            scanf("%d", &element);
            push(element);
            break;
        case 2:
            element = pop();
            if (element != -1)
                printf("Popped element: %d
", element);
            break;
        case 3:
            checkPalindrome();
            break;
        case 4:
            isOverflow();
            isUnderflow();
            break;
        case 5:
            display();
            break;
        case 6:
            printf("Exiting program...
");
            exit(0);
        default:
            printf("Invalid choice! Try again.
");
        }
    }
    return 0;
}
void push(int element) {
    if (top == MAX - 1) {
        printf("Stack Overflow! Cannot push %d
", element);
    } else {
        stack[++top] = element;
        printf("%d pushed to stack.
", element);
    }
}
int pop() {
    if (top == -1) {
        printf("Stack Underflow! Cannot pop.
");
        return -1;
    } else {
        return stack[top--];
    }
}
void display() {
    if (top == -1) {
        printf("Stack is empty!
");
    } else {
        printf("Stack elements (top to bottom): ");
        for (int i = top; i >= 0; i--)
            printf("%d ", stack[i]);
        printf("
");
    }
}
void checkPalindrome() {
    char str[50];
    int tempTop = -1;
    char tempStack[50];
    printf("Enter a string to check palindrome: ");
    scanf("%s", str);

    int len = strlen(str);
    for (int i = 0; i < len; i++)
        tempStack[++tempTop] = str[i];

    int isPal = 1;
    for (int i = 0; i < len; i++) {
        if (str[i] != tempStack[tempTop--]) {
            isPal = 0;
            break;
        }
    }

    if (isPal)
        printf("'%s' is a Palindrome.
", str);
    else
        printf("'%s' is NOT a Palindrome.
", str);
}
void isOverflow() {
    printf("
--- Demonstrating Overflow ---
");
    top = -1;
    for (int i = 0; i < MAX + 1; i++)
        push(i);
}
void isUnderflow() {
    printf("
--- Demonstrating Underflow ---
");
    top = -1;
    pop();
}
    </pre>

    <h1>C Program Code 3</h1>
    <pre>
#include <stdio.h>
#include <string.h>
#define MAX 200
void findAndReplace(char str[], char pat[], char rep[]);
int main() {
    char str[MAX], pat[MAX], rep[MAX];
    printf("Enter the main string (STR): ");
    fgets(str, MAX, stdin);
    str[strcspn(str, "
")] = '
