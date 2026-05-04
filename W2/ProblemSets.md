# Scrabble

In the game of Scrabble, players create words to score points, and the number of points is the sum of the point values of each letter in the word.

```
A
1
B
3
C
3
D
2
E
1
F
4
G
2
H
4
I
1
J
8
K
5
L
1
M
3
N
1
O
1
P
3
Q
10
R
1
S
1
T
1
U
1
V
4
W
4
X
8
Y
4
Z
10
```
For example, if we wanted to score the word “CODE”, we would note that the ‘C’ is worth 3 points, the ‘O’ is worth 1 point, the ‘D’ is worth 2 points, and the ‘E’ is worth 1 point. Summing these, we get that “CODE” is worth 7 points.

In a file called scrabble.c in a folder called scrabble, implement a program in C that determines the winner of a short Scrabble-like game. Your program should prompt for input twice: once for “Player 1” to input their word and once for “Player 2” to input their word. Then, depending on which player scores the most points, your program should either print “Player 1 wins!”, “Player 2 wins!”, or “Tie!” (in the event the two players score equal points).


Submission
```c
#include <stdio.h>
#include <ctype.h>
#include <string.h>
#include <cs50.h>

// Points for each letter A-Z
int POINTS[] = {
    1, 3, 3, 2, 1, 4, 2, 4, 1, 8, 5, 1, 3,
    1, 1, 3, 10, 1, 1, 1, 1, 4, 4, 8, 4, 10
};

int compute_score(string word);

int main(void)
{
    char player1[100];
    char player2[100];

    printf("Player 1: ");
    fgets(player1, sizeof(player1), stdin);

    printf("Player 2: ");
    fgets(player2, sizeof(player2), stdin);

    int score1 = compute_score(player1);
    int score2 = compute_score(player2);

    if (score1 > score2)
    {
        printf("Player 1 wins!\n");
    }
    else if (score2 > score1)
    {
        printf("Player 2 wins!\n");
    }
    else
    {
        printf("Tie!\n");
    }
}

// Compute Scrabble score
int compute_score(string word)
{
    int score = 0;

    for (int i = 0; word[i] != '\0'; i++)
    {
        if (isalpha(word[i]))
        {
            int index = toupper(word[i]) - 'A';
            score += POINTS[index];
        }
    }

    return score;
}
```

---
# Readability

According to Scholastic, E.B. White’s Charlotte’s Web is between a second- and fourth-grade reading level, and Lois Lowry’s The Giver is between an eighth- and twelfth-grade reading level. What does it mean, though, for a book to be at a particular reading level?

Well, in many cases, a human expert might read a book and make a decision on the grade (i.e., year in school) for which they think the book is most appropriate. But an algorithm could likely figure that out too!

In a file called readability.c in a folder called readability, you’ll implement a program that calculates the approximate grade level needed to comprehend some text. Your program should print as output “Grade X” where “X” is the grade level computed, rounded to the nearest integer. If the grade level is 16 or higher (equivalent to or greater than a senior undergraduate reading level), your program should output “Grade 16+” instead of giving the exact index number. If the grade level is less than 1, your program should output “Before Grade 1”.


Submission
```c
#include <stdio.h>
#include <ctype.h>
#include <math.h>
#include <string.h>
#include <cs50.h>

int main(void)
{
    char text[1000];

    printf("Text: ");
    fgets(text, sizeof(text), stdin);

    int letters = 0;
    int words = 1;
    int sentences = 0;

    for (int i = 0; text[i] != '\0'; i++)
    {
        if (isalpha(text[i]))
        {
            letters++;
        }
        else if (text[i] == ' ')
        {
            words++;
        }
        else if (text[i] == '.' || text[i] == '!' || text[i] == '?')
        {
            sentences++;
        }
    }

    float L = ((float) letters / words) * 100;
    float S = ((float) sentences / words) * 100;

    int index = round(0.0588 * L - 0.296 * S - 15.8);

    if (index < 1)
    {
        printf("Before Grade 1\n");
    }
    else if (index >= 16)
    {
        printf("Grade 16+\n");
    }
    else
    {
        printf("Grade %i\n", index);
    }
}

```
---
# Caesar 
Supposedly, Caesar (yes, that Caesar) used to “encrypt” (i.e., conceal in a reversible way) confidential messages by shifting each letter therein by some number of places. For instance, he might write A as B, B as C, C as D, …, and, wrapping around alphabetically, Z as A. And so, to say HELLO to someone, Caesar might write IFMMP instead. Upon receiving such messages from Caesar, recipients would have to “decrypt” them by shifting letters in the opposite direction by the same number of places.

The secrecy of this “cryptosystem” relied on only Caesar and the recipients knowing a secret, the number of places by which Caesar had shifted his letters (e.g., 1). Not particularly secure by modern standards, but, hey, if you’re perhaps the first in the world to do it, pretty secure!

Unencrypted text is generally called plaintext. Encrypted text is generally called ciphertext. And the secret used is called a key.

To be clear, then, here’s how encrypting HELLO with a key of 1 yields IFMMP:


More formally, Caesar’s algorithm (i.e., cipher) encrypts messages by “rotating” each letter by 𝑘 positions. More formally, if 𝑝 is some plaintext (i.e., an unencrypted message), 𝑝𝑖 is the 𝑖𝑡⁢ℎ character in 𝑝, and 𝑘 is a secret key (i.e., a non-negative integer), then each letter, 𝑐𝑖, in the ciphertext, 𝑐, is computed as

```
𝑐𝑖=(𝑝𝑖+𝑘)⁢ % ⁢26
```
wherein % ⁢26 here means “remainder when dividing by 26.” This formula perhaps makes the cipher seem more complicated than it is, but it’s really just a concise way of expressing the algorithm precisely. Indeed, for the sake of discussion, think of A (or a) as 0, B (or b) as 1, …, H (or h) as 7, I (or i) as 8, …, and Z (or z) as 25. Suppose that Caesar just wants to say Hi to someone confidentially using, this time, a key, 𝑘, of 3. And so his plaintext, 𝑝, is Hi, in which case his plaintext’s first character, 𝑝0, is H (aka 7), and his plaintext’s second character, 𝑝1, is i (aka 8). His ciphertext’s first character, 𝑐0, is thus K, and his ciphertext’s second character, 𝑐1, is thus L. Make sense?

In a file called caesar.c in a folder called caesar, write a program that enables you to encrypt messages using Caesar’s cipher. At the time the user executes the program, they should decide, by providing a command-line argument, what the key should be in the secret message they’ll provide at runtime. We shouldn’t necessarily assume that the user’s key is going to be a number; though you may assume that, if it is a number, it will be a positive integer.


Submission
```c
#include <cs50.h>
#include <stdio.h>
#include <stdlib.h>  // for atoi
#include <ctype.h>   // for isalpha, isupper, islower

int main(int argc, string argv[])
{
    // Check correct number of arguments
    if (argc != 2)
    {
        printf("Usage: ./caesar key\n");
        return 1;
    }

    // Check that key is made up of digits only
    for (int i = 0; argv[1][i] != '\0'; i++)
    {
        if (!isdigit(argv[1][i]))
        {
            printf("Usage: ./caesar key\n");
            return 1;
        }
    }

    // Convert key to integer
    int k = atoi(argv[1]);

    // Get plaintext from user
    string plaintext = get_string("plaintext:  ");

    // Print ciphertext
    printf("ciphertext: ");

    for (int i = 0; plaintext[i] != '\0'; i++)
    {
        char c = plaintext[i];

        if (isupper(c))
        {
            // Encrypt uppercase
            printf("%c", (((c - 'A') + k) % 26) + 'A');
        }
        else if (islower(c))
        {
            // Encrypt lowercase
            printf("%c", (((c - 'a') + k) % 26) + 'a');
        }
        else
        {
            // Leave non‑letters unchanged
            printf("%c", c);
        }
    }
    printf("\n");

    return 0;
}
```