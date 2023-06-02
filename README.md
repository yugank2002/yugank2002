#include <stdio.h>
#include <stdlib.h>

int main(int argc, char *argv[]) {
    // Check if 20 integers are provided as command line arguments
    if (argc != 21) {
        printf("Please provide 20 integers as command line arguments.\n");
        return 1;
    }

    // Open the file number.txt for writing
    FILE *file = fopen("number.txt", "w");
    if (file == NULL) {
        printf("Error opening file.\n");
        return 1;
    }

    // Write the integers to number.txt
    for (int i = 1; i <= 20; i++) {
        fprintf(file, "%s\n", argv[i]);
    }

    // Close the file
    fclose(file);

    // Open the file number.txt for reading
    file = fopen("number.txt", "r");
    if (file == NULL) {
        printf("Error opening file.\n");
        return 1;
    }

    // Open the files odd.txt and even.txt for writing
    FILE *oddFile = fopen("odd.txt", "w");
    FILE *evenFile = fopen("even.txt", "w");
    if (oddFile == NULL || evenFile == NULL) {
        printf("Error opening file.\n");
        return 1;
    }

    // Read the numbers from number.txt and separate them into odd and even files
    int num;
    while (fscanf(file, "%d", &num) != EOF) {
        if (num % 2 == 0) {
            fprintf(evenFile, "%d\n", num);
        } else {
            fprintf(oddFile, "%d\n", num);
        }
    }

    // Close the files
    fclose(file);
    fclose(oddFile);
    fclose(evenFile);

    printf("Numbers have been separated into odd.txt and even.txt successfully.\n");

    return 0;
}

