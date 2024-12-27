#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// Structure to store patient details
struct Patient {
    int id;
    char name[50];
    int age;
    char disease[50];
    char gender[10];
};

// Global variables
struct Patient patients[100];
int count = 0;

// Function prototypes
void addPatient();
void viewPatients();
void searchPatient();
void updatePatient();
void deletePatient();

int main() {
    int choice;

    while (1) {
        printf("\n==== Hospital Management System ====\n");
        printf("1. Add Patient\n");
        printf("2. View Patients\n");
        printf("3. Search Patient\n");
        printf("4. Update Patient\n");
        printf("5. Delete Patient\n");
        printf("6. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                addPatient();
                break;
            case 2:
                viewPatients();
                break;
            case 3:
                searchPatient();
                break;
            case 4:
                updatePatient();
                break;
            case 5:
                deletePatient();
                break;
            case 6:
                exit(0);
            default:
                printf("Invalid choice! Try again.\n");
        }
    }

    return 0;
}

// Function to add a new patient
void addPatient() {
    printf("\nEnter Patient ID: ");
    scanf("%d", &patients[count].id);
    printf("Enter Patient Name: ");
    scanf(" %[^\n]%*c", patients[count].name); // Allows spaces in input
    printf("Enter Age: ");
    scanf("%d", &patients[count].age);
    printf("Enter Gender: ");
    scanf("%s", patients[count].gender);
    printf("Enter Disease: ");
    scanf(" %[^\n]%*c", patients[count].disease);

    count++;
    printf("Patient added successfully!\n");
}

// Function to view all patients
void viewPatients() {
    if (count == 0) {
        printf("\nNo patients found.\n");
        return;
    }

    printf("\n=== List of Patients ===\n");
    for (int i = 0; i < count; i++) {
        printf("\nID: %d\nName: %s\nAge: %d\nGender: %s\nDisease: %s\n",
               patients[i].id, patients[i].name, patients[i].age,
               patients[i].gender, patients[i].disease);
    }
}

// Function to search for a patient by ID
void searchPatient() {
    int id, found = 0;

    printf("\nEnter Patient ID to search: ");
    scanf("%d", &id);

    for (int i = 0; i < count; i++) {
        if (patients[i].id == id) {
            printf("\nPatient Found:\n");
            printf("ID: %d\nName: %s\nAge: %d\nGender: %s\nDisease: %s\n",
                   patients[i].id, patients[i].name, patients[i].age,
                   patients[i].gender, patients[i].disease);
            found = 1;
            break;
        }
    }

    if (!found) {
        printf("\nPatient not found.\n");
    }
}

// Function to update patient details
void updatePatient() {
    int id, found = 0;

    printf("\nEnter Patient ID to update: ");
    scanf("%d", &id);

    for (int i = 0; i < count; i++) {
        if (patients[i].id == id) {
            printf("\nEnter New Details:\n");
            printf("Enter Patient Name: ");
            scanf(" %[^\n]%*c", patients[i].name);
            printf("Enter Age: ");
            scanf("%d", &patients[i].age);
            printf("Enter Gender: ");
            scanf("%s", patients[i].gender);
            printf("Enter Disease: ");
            scanf(" %[^\n]%*c", patients[i].disease);
            printf("\nPatient updated successfully!\n");
            found = 1;
            break;
        }
    }

    if (!found) {
        printf("\nPatient not found.\n");
    }
}

// Function to delete a patient by ID
void deletePatient() {
    int id, found = 0;


    printf("\nEnter Patient ID to delete: ");
    scanf("%d", &id);

    for (int i = 0; i < count; i++) {
        if (patients[i].id == id) {
            for (int j = i; j < count - 1; j++) {
                patients[j] = patients[j + 1];
            }
            count--;
            printf("\nPatient deleted successfully!\n");
            found = 1;
            break;
        }
    }

    if (!found) {
        printf("\nPatient not found.\n");
    }
}
