<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>All C Codes Display</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background: #f4f4f4;
            padding: 20px;
        }
        h2 {
            background: #222;
            color: #fff;
            padding: 10px;
            border-radius: 5px;
        }
        pre {
            background: #fff;
            padding: 15px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
            overflow-x: auto;
        }
    </style>
</head>
<body>
    <h1>All C Program Codes</h1>

    <h2>Code 1</h2>
    <pre>#include <stdio.h>
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
    scanf(" %[\n]s", day->activity);
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
}</pre>

    <h2>Code 2</h2>
    <pre>#include <stdio.h>
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
        printf("\n--- STACK OPERATIONS MENU ---\n");
        printf("1. Push an element onto stack\n");
        printf("2. Pop an element from stack\n");
        printf("3. Check Palindrome using Stack\n");
        printf("4. Demonstrate Overflow and Underflow\n");
        printf("5. Display Stack\n");
        printf("6. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);
        switch (choice) {
        case 1:
            printf("Enter element to push: ");
            scanf("%d", &element);
            push(element);
            break;
        case 2:
            element = pop();
            if (element != -1)
                printf("Popped element: %d\n", element);
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
            printf("Exiting program...\n");
            exit(0);
        default:
            printf("Invalid choice! Try again.\n");
        }
    }
    return 0;
}
void push(int element) {
    if (top == MAX - 1) {
        printf("Stack Overflow! Cannot push %d\n", element);
    } else {
        stack[++top] = element;
        printf("%d pushed to stack.\n", element);
    }
}
int pop() {
    if (top == -1) {
        printf("Stack Underflow! Cannot pop.\n");
        return -1;
    } else {
        return stack[top--];
    }
}
void display() {
    if (top == -1) {
        printf("Stack is empty!\n");
    } else {
        printf("Stack elements (top to bottom): ");
        for (int i = top; i >= 0; i--)
            printf("%d ", stack[i]);
        printf("\n");
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
        printf("'%s' is a Palindrome.\n", str);
    else
        printf("'%s' is NOT a Palindrome.\n", str);
}
void isOverflow() {
    printf("\n--- Demonstrating Overflow ---\n");
    top = -1;
    for (int i = 0; i < MAX + 1; i++)
        push(i);
}
void isUnderflow() {
    printf("\n--- Demonstrating Underflow ---\n");
    top = -1;
    pop();
}</pre>

    <h2>Code 3</h2>
    <pre>#include <stdio.h>
#include <string.h>
#define MAX 200
void findAndReplace(char str[], char pat[], char rep[]);
int main() {
    char str[MAX], pat[MAX], rep[MAX];
    printf("Enter the main string (STR): ");
    fgets(str, MAX, stdin);
    str[strcspn(str, "\n")] = '\0';
    printf("Enter the pattern string (PAT): ");
    fgets(pat, MAX, stdin);
    pat[strcspn(pat, "\n")] = '\0';
    printf("Enter the replace string (REP): ");
    fgets(rep, MAX, stdin);
    rep[strcspn(rep, "\n")] = '\0';
    findAndReplace(str, pat, rep);
    return 0;
}
void findAndReplace(char str[], char pat[], char rep[]) {
    char result[MAX];
    int i, j, k;
    int found = 0;
    int lenSTR = strlen(str);
    int lenPAT = strlen(pat);
    int lenREP = strlen(rep);
    i = j = 0;
    while (i < lenSTR) {
        for (k = 0; k < lenPAT && (i + k) < lenSTR && str[i + k] == pat[k]; k++);
        if (k == lenPAT) {
            found = 1;
            strcpy(&result[j], rep);
            j += lenREP;
            i += lenPAT;
        } else {
            result[j++] = str[i++];
        }
    }
    result[j] = '\0';
    if (found)
        printf("\nUpdated string after replacement:\n%s\n", result);
    else
        printf("\nPattern not found in the main string.\n");
}</pre>

    <h2>Code 4</h2>
    <pre>#include <stdio.h>
#include <ctype.h>
#include <string.h>
#define MAX 100
char stack[MAX];
int top = -1;
void push(char sym) { stack[++top] = sym; }
char pop() { return stack[top--]; }
char peek() { return (top == -1) ? '\0' : stack[top]; }
int precedence(char op) {
    switch (op) {
        case '^': return 3;
        case '*': case '/': case '%': return 2;
        case '+': case '-': return 1;
        default: return 0;
    }
}
int isOperator(char sym) {
    return (sym == '+' || sym == '-' || sym == '*' || sym == '/' || sym == '%' || sym == '^');
}
void infixToPostfix(char infix[], char postfix[]) {
    int i, j = 0;
    char sym;
    for (i = 0; infix[i] != '\0'; i++) {
        sym = infix[i];
        if (sym == ' ' || sym == '\t')
            continue;
        else if (isalnum(sym))
            postfix[j++] = sym;
        else if (sym == '(')
            push(sym);
        else if (sym == ')') {
            while (peek() != '(')
                postfix[j++] = pop();
            pop();
        }
        else if (isOperator(sym)) {
            while (top != -1 &&   ((precedence(peek()) > precedence(sym)) ||  (precedence(peek()) == precedence(sym) && sym != '^')) &&peek() != '(')
            {
                postfix[j++] = pop();
            }
            push(sym);
        }
    }
    while (top != -1)
        postfix[j++] = pop();
    postfix[j] = '\0';
}
int main()
{
    char infix[MAX], postfix[MAX];
    printf("Enter infix expression: ");
    scanf("%[^\n]", infix);
    infixToPostfix(infix, postfix);
    printf("Postfix expression: %s\n", postfix);
    return 0;
}</pre>

    <h2>Code 5</h
