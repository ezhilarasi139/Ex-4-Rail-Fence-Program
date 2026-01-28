# Ex-4 Rail-Fence-Program
### NAME : EZHILARASI N
### DATE : 28.01.26
## IMPLEMENTATION OF RAIL FENCE – ROW & COLUMN TRANSFORMATION TECHNIQUE

## AIM:

To write a C program to implement the rail fence transposition technique.

## DESCRIPTION:

In the rail fence cipher, the plain text is written downwards and diagonally on successive "rails" of an imaginary fence, then moving up when we reach the bottom rail. When we reach the top rail, the message is written downwards again until the whole plaintext is written out. The message is then read off in rows.

## ALGORITHM:

STEP-1: Read the Plain text.
STEP-2: Arrange the plain text in row columnar matrix format.
STEP-3: Now read the keyword depending on the number of columns of the plain text.
STEP-4: Arrange the characters of the keyword in sorted order and the corresponding columns of the plain text.
STEP-5: Read the characters row wise or column wise in the former order to get the cipher text.

## PROGRAM
```
#include <stdio.h>
#include <string.h>

void encrypt(char *s, int r, char *e) {
    int i, j = 0, d = 1, row = 0, len = strlen(s);
    char rail[r][len];
    memset(rail, 0, sizeof(rail));

    for (i = 0; i < len; i++) {
        rail[row][i] = s[i];
        row += d;
        if (row == r - 1 || row == 0) d = -d;
    }

    for (i = 0; i < r; i++)
        for (j = 0; j < len; j++)
            if (rail[i][j]) *e++ = rail[i][j];
    *e = '\0';
}

void decrypt(char *s, int r, char *d) {
    int i, j, k = 0, row = 0, dir = 1, len = strlen(s);
    char rail[r][len];
    memset(rail, 0, sizeof(rail));

    for (i = 0; i < len; i++) {
        rail[row][i] = '*';
        row += dir;
        if (row == r - 1 || row == 0) dir = -dir;
    }

    for (i = 0; i < r; i++)
        for (j = 0; j < len; j++)
            if (rail[i][j] == '*') rail[i][j] = s[k++];

    row = 0; dir = 1;
    for (i = 0; i < len; i++) {
        *d++ = rail[row][i];
        row += dir;
        if (row == r - 1 || row == 0) dir = -dir;
    }
    *d = '\0';
}

int main() {
    char msg[1000], enc[1000], dec[1000];
    int rails;

    printf("Simulating Rail Fence Cipher\n");
    printf("Enter a Secret Message: ");
    fgets(msg, 1000, stdin);
    msg[strcspn(msg, "\n")] = 0;

    printf("Enter number of rails: ");
    scanf("%d", &rails);

    encrypt(msg, rails, enc);
    printf("Encrypted Message: %s\n", enc);

    decrypt(enc, rails, dec);
    printf("Decrypted Message: %s\n", dec);
}

```
## OUTPUT
<img width="608" height="280" alt="image" src="https://github.com/user-attachments/assets/5bcd28b7-488f-4750-b7e2-649400bf940b" />


## RESULT : 
Thus the implementation of RAIL FENCE – ROW & COLUMN transformation technique is executed successfully.
