# Hello
```python
name = input("What is your name? ")

print(f"hello, {name}")

```

---
# Mario
```python
def main():

    height = int(input("Choose a number between 1-8: "))

    for i in range(height):

        for j in range(height - i - 1):
            print(" ", end="")

        for j in range(i + 1):
            print("#", end="")

        print("  ", end="")

        for j in range(i + 1):
            print("#", end="")

        print()


main()
```

---

# Cash
```python
def main():

    while True:
        try:
            dollars = float(input("Change owed: "))

            if dollars >= 0:
                break

        except ValueError:
            pass

    cents = round(dollars * 100)

    coins = 0

    while cents >= 25:
        coins += 1
        cents -= 25

    while cents >= 10:
        coins += 1
        cents -= 10

    while cents >= 5:
        coins += 1
        cents -= 5

    while cents >= 1:
        coins += 1
        cents -= 1

    print(coins)


main()
```

---
# Readability
```python
from math import floor

# Had to rebuild my pc but had the psets for CS50P already created
def main():

    text = input("Text: ")

    letters = 0
    words = 1
    sentences = 0

    for character in text:

        if character.isalpha():
            letters += 1

        elif character == " ":
            words += 1

        elif character == "." or character == "!" or character == "?":
            sentences += 1

    L = (letters / words) * 100
    S = (sentences / words) * 100

    index = round(0.0588 * L - 0.296 * S - 15.8)

    if index < 1:
        print("Before Grade 1")

    elif index >= 16:
        print("Grade 16+")

    else:
        print(f"Grade {index}")


main()
```