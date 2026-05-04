# Hello World
Thanks to Professor Brian Kernighan (who taught CS50 when David took it!), “hello, world” has been implemented in hundreds of languages. Let’s add your implementation to the list!

In a file called hello.c, in a folder called world, implement a program in C that prints hello, world\n, and that’s it!

Submission
```c
char myName[25];

int main(void){
	printf("Hello World\n")
{

```
---
# Hello, It's Me

In a file called hello.c, in a folder called me, implement a program in C that prompts the user for their name and then says hello to that user. For instance, if the user’s name is Adele, your program should print hello, Adele\n

Submission
```c
#include <stdio.h>

char myName[25];

int main(void)
{

    printf("What is your name?\n");

    scanf("%s", myName);

    printf("hello, %s\n", myName);
}
```

---
# Mario
Toward the beginning of World 1-1 in Nintendo’s Super Mario Brothers, Mario must hop over adjacent pyramids of blocks, per the below.

screenshot of Mario jumping over adjacent pyramids

In a file called mario.c in a folder called mario-more, implement a program in C that recreates that pyramid, using hashes (#) for bricks, as in the below:

   #  #
  ##  ##
 ###  ###
####  ####
And let’s allow the user to decide just how tall the pyramids should be by first prompting them for a positive int between, say, 1 and 8, inclusive.

Examples
Notice that width of the “gap” between adjacent pyramids is equal to the width of two hashes, irrespective of the pyramids’ heights

Submission
```c
#include <stdio.h>

int main(void)
{
    int height;
    printf("Choose a number between 1-8: ");
    scanf("%d", &height);

    for (int i = 0; i < height; i++)
    {
        for (int j = 0; j < height - i - 1; j++)
            printf(" ");
        for (int j = 0; j <= i; j++)
            printf("#");
        printf("  ");
        for (int j = 0; j <= i; j++)
            printf("#");
        printf("\n");
    }
}
```

---
# Cash

Suppose you work at a store and a customer gives you $1.00 (100 cents) for candy that costs $0.50 (50 cents). You’ll need to pay them their “change,” the amount leftover after paying for the cost of the candy. When making change, odds are you want to minimize the number of coins you’re dispensing for each customer, lest you run out (or annoy the customer!). In a file called cash.c in a folder called cash, implement a program in C that prints the minimum coins needed to make the given amount of change, in cents, as in the below:

```
Change owed: 25
1
```
But prompt the user for an int greater than 0, so that the program works for any amount of change:

```
Change owed: 70
4
```
Re-prompt the user, again and again as needed, if their input is not greater than or equal to 0 (or if their input isn’t an int at all!).

```c
#include <stdio.h>

int main(void)
{
    int cents;
    int coins = 0;

// Validating input as positive number - used Perplexity for implementation suggestions
    while (1)
    {
        printf("Change owed: ");
        if (scanf("%d", &cents) == 1 && cents >= 0)
        {
            break;
        }

        while (getchar() != '\n');
    }

    while (cents >= 25)
    {
        coins++;
        cents -= 25;
    }

    while (cents >= 10)
    {
        coins++;
        cents -= 10;
    }

    while (cents >= 5)
    {
        coins++;
        cents -= 5;
    }

    while (cents >= 1)
    {
        coins++;
        cents -= 1;
    }

    printf("%d\n", coins);
}

```