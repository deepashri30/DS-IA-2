#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_ITEMS 8

typedef struct {
    char name[30];
    float price;
} Item;

typedef struct CartNode {
    Item item;
    struct CartNode* next;
} CartNode;

typedef struct {
    CartNode* head;
} ShoppingCart;

void addItemToCart(ShoppingCart* cart, Item item) {
    CartNode* newNode = (CartNode*)malloc(sizeof(CartNode));
    newNode->item = item;
    newNode->next = cart->head;
    cart->head = newNode;
    printf("Added %s to cart.\n", item.name);
}

void viewCart(ShoppingCart* cart) {
    if (cart->head == NULL) {
        printf("Your cart is empty.\n");
        return;
    }

    printf("Your Shopping Cart:\n");
    float total = 0.0;
    CartNode* current = cart->head;
    while (current != NULL) {
        printf("%s - ₹%.2f\n", current->item.name, current->item.price);
        total += current->item.price;
        current = current->next;
    }
    printf("Total: ₹%.2f\n", total);
}

void checkout(ShoppingCart* cart) {
    if (cart->head == NULL) {
        printf("Your cart is empty. Cannot checkout.\n");
        return;
    }

    printf("Checking out...\n");
    viewCart(cart);
    printf("Thank you for your purchase!\n");

    // Clear the cart
    CartNode* current = cart->head;
    while (current != NULL) {
        CartNode* temp = current;
        current = current->next;
        free(temp);
    }
    cart->head = NULL; // Reset the cart

    // Exit the program after checkout
    exit(0);
}

void freeCart(ShoppingCart* cart) {
    CartNode* current = cart->head;
    while (current != NULL) {
        CartNode* temp = current;
        current = current->next;
        free(temp);
    }
}

void displayItems(const char* category, Item* items, int size) {
    printf("%s:\n", category);
    for (int i = 0; i < size; i++) {
        printf("%d. %s - ₹%.2f\n", i + 1, items[i].name, items[i].price);
    }
}

void addMultipleItemsToCart(ShoppingCart* cart, Item* fruits, Item* vegetables, Item* electronics, const int* choices, int count) {
    for (int i = 0; i < count; i++) {
        int itemChoice = choices[i];
        if (itemChoice > 0 && itemChoice <= MAX_ITEMS) {
            addItemToCart(cart, fruits[itemChoice - 1]);
        } else if (itemChoice > MAX_ITEMS && itemChoice <= 2 * MAX_ITEMS) {
            addItemToCart(cart, vegetables[itemChoice - MAX_ITEMS - 1]);
        } else if (itemChoice > 2 * MAX_ITEMS && itemChoice <= 3 * MAX_ITEMS) {
            addItemToCart(cart, electronics[itemChoice - 2 * MAX_ITEMS - 1]);
        } else {
            printf("Invalid item number: %d\n", itemChoice);
        }
    }
}

int main() {
    Item fruits[MAX_ITEMS] = {
        {"Apple", 20.00}, {"Banana", 10.00}, {"Orange", 15.00}, {"Grapes", 40.00},
        {"Strawberry", 50.00}, {"Peach", 30.00}, {"Watermelon", 60.00}, {"Pineapple", 45.00}
    };

    Item vegetables[MAX_ITEMS] = {
        {"Carrot", 20.00}, {"Broccoli", 50.00}, {"Spinach", 30.00}, {"Potato", 20.00},
        {"Tomato", 25.00}, {"Onion", 15.00}, {"Cucumber", 18.00}, {"Bell Pepper", 40.00}
    };

    Item electronics[MAX_ITEMS] = {
        {"Smartphone", 15000.00}, {"Laptop", 50000.00}, {"Headphones", 2000.00},
        {"Smartwatch", 4000.00}, {"Tablet", 25000.00}, {"Camera", 30000.00},
        {"Bluetooth Speaker", 1500.00}, {"Smart TV", 40000.00}
    };

    ShoppingCart cart = { .head = NULL };
    int choice;

    do {
        printf("\n--- Online Shopping Cart ---\n");
        displayItems("Fruits", fruits, MAX_ITEMS);
        displayItems("Vegetables", vegetables, MAX_ITEMS);
        displayItems("Electronics", electronics, MAX_ITEMS);

        printf("Select items to add to cart (use item numbers separated by commas, e.g., 1,9,17), or 0 to view cart: ");
        
        char input[100];
        scanf(" %[^\n]%*c", input);

        if (strcmp(input, "0") == 0) {
            viewCart(&cart);
        } else {
            int choices[100];
            int count = 0;
            char* token = strtok(input, ",");
            while (token != NULL && count < 100) {
                choices[count++] = atoi(token);
                token = strtok(NULL, ",");
            }
            addMultipleItemsToCart(&cart, fruits, vegetables, electronics, choices, count);
        }

        printf("3. Checkout\n");
        printf("Select an option: ");
        scanf("%d", &choice);

        if (choice == 3) {
            checkout(&cart);
        }
    } while (1); // Infinite loop; program exits after checkout

    freeCart(&cart);
    return 0;
}
