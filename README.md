#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <stdbool.h>

#define MAX_MOVIES 10
#define MAX_NAME_LENGTH 50

char movieNames[MAX_MOVIES][MAX_NAME_LENGTH];
char theatres[MAX_MOVIES][MAX_NAME_LENGTH];
int availableSeats[MAX_MOVIES];
int ticketPrices[MAX_MOVIES][MAX_MOVIES]; 
int availableSeatsTheatres[MAX_MOVIES];
int foodPrices[MAX_MOVIES];

void initializeMovies();
void displayMovies();
void initializeTheatres();
void displayTheatres();
void initializeFoodPrices();
int bookTicket(int movieIndex, int theatreIndex, int numSeats);
int buyFood();
void makePayment(int totalPrice);
void displayFinalResult(int totalPrice);

void initializeMovies() {
    strcpy(movieNames[0], "Spiderman: Across The Spiderverse");
    availableSeats[0] = 100;

    strcpy(movieNames[1], "Inception");
    availableSeats[1] = 90;

    strcpy(movieNames[2], "Avatar");
    availableSeats[2] = 110;

    strcpy(movieNames[3], "Indiana Jones");
    availableSeats[3] = 80;

    strcpy(movieNames[4], "Pirates");
    availableSeats[4] = 70;
}

void initializeTheatres() {
    strcpy(theatres[0], "Venkateshwara Cinemas");
    availableSeatsTheatres[0] = 90;

    strcpy(theatres[1], "Bhramaramba Multiplex");
    availableSeatsTheatres[1] = 100;

    strcpy(theatres[2], "Mallikarjuna Screens");
    availableSeatsTheatres[2] = 80;

    strcpy(theatres[3], "PVR Producers cut");
    availableSeatsTheatres[3] = 70;
}

void initializeTicketPrices() {
    
    ticketPrices[0][0] = 15;
    ticketPrices[0][1] = 20;
    ticketPrices[0][2] = 18;
    ticketPrices[0][3] = 22;

    ticketPrices[1][0] = 16;
    ticketPrices[1][1] = 18;
    ticketPrices[1][2] = 19;
    ticketPrices[1][3] = 21;

    ticketPrices[2][0] = 17;
    ticketPrices[2][1] = 19;
    ticketPrices[2][2] = 21;
    ticketPrices[2][3] = 23;

    ticketPrices[3][0] = 18;
    ticketPrices[3][1] = 20;
    ticketPrices[3][2] = 22;
    ticketPrices[3][3] = 24;

    ticketPrices[4][0] = 19;
    ticketPrices[4][1] = 21;
    ticketPrices[4][2] = 23;
    ticketPrices[4][3] = 25;
}

void displayMovies() {
    printf("Available Movies:\n");
    for (int i = 0; i < MAX_MOVIES; i++) {
        if (availableSeats[i] > 0) {
            printf("%d. %s\n", i + 1, movieNames[i]);
        }
    }
}

void displayTheatres() {
    printf("Available Theatres:\n");
    for (int j = 0; j < MAX_MOVIES-1; j++) {
        if (availableSeatsTheatres[j] > 0) {
            printf("%d. %s\n", j+1 , theatres[j]);
        }
    }
}

int bookTicket(int movieIndex, int theatreIndex, int numSeats) {
    if (movieIndex < 0 || movieIndex >= MAX_MOVIES) {
        printf("Invalid movie selection.\n");
        return 0;
    }

    if (theatreIndex < 0 || theatreIndex >= MAX_MOVIES) {
        printf("Invalid theatre selection.\n");
        return 0;
    }

    if (availableSeats[movieIndex] >= numSeats) {
        availableSeats[movieIndex] -= numSeats;
        int ticketPrice = ticketPrices[movieIndex][theatreIndex] * numSeats;
        int foodPrice = buyFood();
        int totalPrice = ticketPrice + foodPrice;
        makePayment(totalPrice);
        displayFinalResult(totalPrice);
         printf("Confirm payment (1 - Yes, 0 - No): ");
        int confirm;
        scanf("%d", &confirm);
        if (confirm == 1)
        {
            makePayment(totalPrice);
            displayFinalResult(totalPrice);
            return 1;
        }
        else
        {
            printf("Payment cancelled.\n");
            return 0;
        }
    }
    else
    {
        printf("Insufficient seats available.\n");
        return 0;
    }
}

void initializeFoodPrices() {
    
    foodPrices[0] = 50;
    foodPrices[1] = 60;
    foodPrices[2] = 55;
    foodPrices[3] = 70;
    foodPrices[4] = 65;
}

int buyFood() {
    int choice;
    int numItems;
    int totalPrice = 0;

    printf("Food Menu:\n");
    printf("1. Popcorn - $10\n");
    printf("2. Soft Drink - $5\n");
    printf("3. Burger - $15\n");
    printf("Enter the number of food items you want to purchase: ");
    scanf("%d", &numItems);

    for (int i = 0; i < numItems; i++) {
        printf("Enter your choice for food item %d: ", i + 1);
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                totalPrice += 10;
                break;
            case 2:
                totalPrice += 5;
                break;
            case 3:
                totalPrice += 15;
                break;
            default:
                printf("Invalid choice. Ignoring the item.\n");
        }
    }

    return totalPrice;
}
void makePayment(int totalPrice) {
    printf("Payment successful! Total amount: $%d\n", totalPrice);
}

void displayFinalResult(int totalPrice) {
    printf("Ticket(s) and food purchased successfully!\n");
    printf("Total Price: $%d\n", totalPrice);
}


int main() {
    
    char correctUsername[] = "User";
    char correctPassword[] = "Password";

    char username[50];
    char password[50];

    printf("Username: ");
    scanf("%s", username);
    printf("Password: ");
    scanf("%s", password);

    bool isAuthenticated = (strcmp(username, correctUsername) == 0 && strcmp(password, correctPassword) == 0);

    if (isAuthenticated) {
        int choice;
        int movieIndex;
        int theatreIndex;
        int numSeats;

        initializeMovies();
        initializeTheatres();
        initializeTicketPrices();
        initializeFoodPrices();

        printf("\n==========================================================");
        printf("\n");
        printf("\t\t###Movie Ticket Booking### ");
        printf("\n");
        printf("\n===========================================================");
        printf("\n");
        while (1) {
            // Display the menu and perform operations
            printf("\nMOVIE TICKET BOOKING SYSTEM\n");
            printf("1. Display available movies\n");
            printf("2. Display available theaters\n");
            printf("3. Book tickets\n");
            printf("4. Exit\n");
            printf("Enter your choice: ");
            scanf("%d", &choice);

            switch (choice) {
                case 1:
                    displayMovies();
                    break;
                case 2:
                    displayTheatres();
                    break;
                case 3:
                    printf("Enter movie index: ");
                    scanf("%d", &movieIndex);
                    printf("Enter theatre index: ");
                    scanf("%d", &theatreIndex);
                    printf("Enter number of seats: ");
                    scanf("%d", &numSeats);
                    bookTicket(movieIndex - 1, theatreIndex - 1, numSeats);
                    break;
                case 4:
                    printf("Exiting...\n");
                    printf("Thank you");
                    exit(0);
                default:
                    printf("Invalid choice.\n");
                    printf("Please enter a valid option");
            }
        }
    } else {
        printf("Authentication failed. Incorrect username or password.\n");
    }

    return 0;
}
