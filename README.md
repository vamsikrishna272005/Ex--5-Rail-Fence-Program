# Ex--5-Rail-Fence-Program

# IMPLEMENTATION OF RAIL FENCE – ROW & COLUMN TRANSFORMATION TECHNIQUE

# AIM:

# To write a C program to implement the rail fence transposition technique.

# DESCRIPTION:

In the rail fence cipher, the plain text is written downwards and diagonally on successive "rails" of an imaginary fence, then moving up when we reach the bottom rail. When we reach the top rail, the message is written downwards again until the whole plaintext is written out. The message is then read off in rows.

# ALGORITHM:

STEP-1: Read the Plain text.
STEP-2: Arrange the plain text in row columnar matrix format.
STEP-3: Now read the keyword depending on the number of columns of the plain text.
STEP-4: Arrange the characters of the keyword in sorted order and the corresponding columns of the plain text.
STEP-5: Read the characters row wise or column wise in the former order to get the cipher text.

# PROGRAM
```
#include <stdio.h>
#include <string.h>
#include <ctype.h>
void encryptRailFence(char text[], int depth, char cipher[]) {
    int len = strlen(text);
    char rail[depth][len];
    memset(rail, '\n', sizeof(rail)); 
    int row = 0, down = 1; // Direction flag

    for (int i = 0; i < len; i++) {
        rail[row][i] = text[i]; // Place character in rail matrix
        if (row == 0)
            down = 1;
        else if (row == depth - 1)
            down = 0;
        row += (down ? 1 : -1);
    }
    int k = 0;
    for (int i = 0; i < depth; i++)
        for (int j = 0; j < len; j++)
            if (rail[i][j] != '\n')
                cipher[k++] = rail[i][j];

    cipher[k] = '\0';
}
void decryptRailFence(char cipher[], int depth, char plain[]) {
    int len = strlen(cipher);
    char rail[depth][len];
    memset(rail, '\n', sizeof(rail));

    int row = 0, down = 1, index = 0;
    for (int i = 0; i < len; i++) {
        rail[row][i] = '*';

        if (row == 0)
            down = 1;
        else if (row == depth - 1)
            down = 0;

        row += (down ? 1 : -1);
    }
    for (int i = 0; i < depth; i++)
        for (int j = 0; j < len; j++)
            if (rail[i][j] == '*')
                rail[i][j] = cipher[index++];
    row = 0, down = 1;
    for (int i = 0; i < len; i++) {
        plain[i] = rail[row][i];

        if (row == 0)
            down = 1;
        else if (row == depth - 1)
            down = 0;

        row += (down ? 1 : -1);
    }
    plain[len] = '\0';
}

int main() {
    char text[100], cipher[100], decrypted[100];
    int depth;

    printf("Enter the plaintext: ");
    scanf("%s", text);
    printf("Enter the depth: ");
    scanf("%d", &depth);

    encryptRailFence(text, depth, cipher);
    printf("Encrypted Text: %s\n", cipher);

    decryptRailFence(cipher, depth, decrypted);
    printf("Decrypted Text: %s\n", decrypted);

    return 0;
}
```
# OUTPUT
![Screenshot 2025-04-08 143608](https://github.com/user-attachments/assets/d2f03d01-526b-478c-807b-20ebcbb2dc4b)

# RESULT

The program is executed successfully
