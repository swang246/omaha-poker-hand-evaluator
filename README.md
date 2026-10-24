# Omaha Poker Hand Evaluator

## 1. Introduction

This project implements a C program that evaluates the winner of a two-player Omaha-High poker game. Each player receives four private cards, and five community cards are shared between both players.

Unlike Texas Hold’em, Omaha requires each player to use **exactly two of their four private cards and exactly three of the five community cards** to form a five-card poker hand. The program evaluates every valid combination for each player, identifies their strongest hand, and compares the results to determine the winner.

### Poker Hand Rankings

Poker hands are ranked from lowest to highest:

1. **High Card:** The highest-value card when no higher-ranking combination is formed.
2. **One Pair:** Two cards of the same value.
3. **Two Pair:** Two separate pairs.
4. **Three of a Kind:** Three cards of the same value.
5. **Straight:** Five consecutive card values.
6. **Flush:** Five cards of the same suit.
7. **Full House:** Three of a kind and one pair.
8. **Four of a Kind:** Four cards of the same value.
9. **Straight Flush:** Five consecutive cards of the same suit.
10. **Royal Flush:** A ten, jack, queen, king, and ace of the same suit.

Card values range from 2 through ace, with ace being the highest card. When players have hands of the same category, their card values and applicable tie-breakers determine the winner.

## 2. Project Goal

The goal is to determine the winner of each poker deal by evaluating the best possible hand for both players.

For each deal, the program generates all valid five-card combinations, evaluates their strengths, and compares each player's strongest hand. It reports one of three results:

- `Player 1 wins`
- `Player 2 wins`
- `No single winner`

A tie is reported when the players' evaluated best hands have equal strength.

## 3. Input and Output

### Input Format

The program reads poker deals from a plain-text input file. Each line contains 13 cards separated by spaces:

- **Cards 1–4:** Player 1's private cards
- **Cards 5–8:** Player 2's private cards
- **Cards 9–13:** The five community cards

Card values use `2`–`9`, `T` for ten, `J` for jack, `Q` for queen, `K` for king, and `A` for ace. Suits are represented by `C` (clubs), `D` (diamonds), `H` (hearts), and `S` (spades).

Example input:

```text
8H AS 3S 3H TH AD 8D 9C 2C 9S JH 4D 5S
```

Each line represents one complete deal. The program processes multiple deals until the input file has been read.

### Output Format

For each deal, the program prints the winner on a separate line. The expected output is exactly one of the following:

```text
Player 1 wins
Player 2 wins
No single winner
```

The output corresponds to the deals in the same order as the input.

## 4. Implementation

### Card Representation

Cards are represented using C structures and enumerations. Each card stores its value and suit, while each hand stores five cards, card-value counts, and an unsigned integer bit vector representing hand strength.

### Hand Combination Generation

Each player has four private cards and access to five community cards. The program generates every combination that uses exactly two private cards and three community cards.

This produces:

$$
\binom{4}{2} \times \binom{5}{3}
= 6 \times 10
= 60
$$

possible five-card hands per player.

### Hand Evaluation

The program counts occurrences of card values and checks for hand characteristics such as:

- Straights
- Flushes
- Straight flushes
- Full houses
- Pairs and multiples of the same card value

### Bit-Vector Hand Ranking

Hand strength is represented using bitwise operations and an unsigned integer. The program sets bits corresponding to card values and hand categories, then compares the resulting vectors to select each player's strongest hand.

### Winner Determination

After evaluating all 60 combinations for each player, the program compares their best-hand vectors. The player with the stronger evaluated hand wins; equal vectors result in `No single winner`.

## 5. Technologies and Concepts

- **Language:** C
- **Libraries:** Standard C library
- **Data structures:** Structures, enumerations, and arrays
- **Programming concepts:** Pointers, nested loops, memory initialization, and file processing
- **Algorithms:** Combinatorial enumeration and hand-strength comparison
- **Bitwise operations:** Bit masks and bit-vector representation

## 6. Building and Running

### Prerequisites

- A C compiler such as GCC or MinGW
- An input file containing poker deals

### Compile

Run the following command in the directory containing `omaha_poker.c` and `omaha_poker.h`:

```bash
gcc -std=c99 omaha_poker.c -o omaha_poker
```

### Run

**Windows PowerShell:**

```powershell
.\omaha_poker omaha.txt
```

**Linux/macOS:**

```bash
./omaha_poker omaha.txt
```

Replace `input.txt` with the path to the input file you want to evaluate.

## 7. Potential Improvements

- Validate input cards and handle malformed input files.
- Test all poker hand categories and tie-breaking scenarios.
- Verify hand-ranking logic against known poker examples.
- Improve handling of ace-low straights and other edge cases.
- Add automated tests with expected outcomes.
- Separate card parsing, hand evaluation, and winner determination into clearly organized modules.

## 8. Purpose

This project demonstrates how C programming, bitwise operations, and combinatorial algorithms can be used to evaluate poker hands, compare possible outcomes, and determine a winner across multiple deals.
