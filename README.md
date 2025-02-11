#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// Define maximum number of rooms
#define MAX_ROOMS 10

// Structure to hold information about each room
struct Room {
    int roomNumber;
    char customerName[50];
    int isOccupied; // 0 = vacant, 1 = occupied
};

// Function to display the menu
void displayMenu() {
    printf("\n--- Hotel Management System ---\n");
    printf("1. View all rooms\n");
    printf("2. Book a room\n");
    printf("3. Check-out a room\n");
    printf("4. Exit\n");
}

// Function to view all rooms
void viewRooms(struct Room rooms[], int size) {
    printf("\nRoom Number\tCustomer Name\tStatus\n");
    printf("---------------------------------------------\n");
    for (int i = 0; i < size; i++) {
        if (rooms[i].isOccupied == 0) {
            printf("%d\t\tVacant\n", rooms[i].roomNumber);
        } else {
            printf("%d\t\t%s\tOccupied\n", rooms[i].roomNumber, rooms[i].customerName);
        }
    }
}

// Function to book a room
void bookRoom(struct Room rooms[], int size) {
    int roomNumber;
    char customerName[50];

    printf("Enter the room number to book (1-%d): ", size);
    scanf("%d", &roomNumber);

    // Check if the room number is valid and vacant
    if (roomNumber >= 1 && roomNumber <= size) {
        if (rooms[roomNumber - 1].isOccupied == 0) {
            printf("Enter the customer's name: ");
            getchar(); // Consume leftover newline
            fgets(customerName, 50, stdin);
            customerName[strcspn(customerName, "\n")] = '\0';  // Remove newline from name

            strcpy(rooms[roomNumber - 1].customerName, customerName);
            rooms[roomNumber - 1].isOccupied = 1;
            printf("Room %d has been successfully booked for %s.\n", roomNumber, customerName);
        } else {
            printf("Sorry, Room %d is already occupied.\n", roomNumber);
        }
    } else {
        printf("Invalid room number. Please try again.\n");
    }
}

// Function to check-out a room
void checkOutRoom(struct Room rooms[], int size) {
    int roomNumber;

    printf("Enter the room number to check-out (1-%d): ", size);
    scanf("%d", &roomNumber);

    // Check if the room number is valid and occupied
    if (roomNumber >= 1 && roomNumber <= size) {
        if (rooms[roomNumber - 1].isOccupied == 1) {
            rooms[roomNumber - 1].isOccupied = 0;
            printf("Room %d has been successfully checked-out.\n", roomNumber);
        } else {
            printf("Room %d is already vacant.\n", roomNumber);
        }
    } else {
        printf("Invalid room number. Please try again.\n");
    }
}

int main() {
    struct Room rooms[MAX_ROOMS]; // Declare an array of rooms

    // Initialize rooms with room number and vacant status
    for (int i = 0; i < MAX_ROOMS; i++) {
        rooms[i].roomNumber = i + 1;
        rooms[i].isOccupied = 0;
    }

    int choice;
    do {
        displayMenu(); // Display the menu
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                viewRooms(rooms, MAX_ROOMS);
                break;
            case 2:
                bookRoom(rooms, MAX_ROOMS);
                break;
            case 3:
                checkOutRoom(rooms, MAX_ROOMS);
                break;
            case 4:
                printf("Exiting Hotel Management System. Goodbye!\n");
                break;
            default:
                printf("Invalid choice! Please try again.\n");
        }
    } while (choice != 4);

    return 0;
}
