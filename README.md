# Slot Machine Game

This repository contains a slot machine game implemented in Python. The game allows the player to deposit money, choose the number of lines to bet on, and place bets. The slot machine will then spin and display the results, showing the winnings and updating the player's balance.

## Table of Contents

1. [Overview](#overview)
2. [Setup](#setup)
3. [Usage](#usage)
    - [Deposit](#deposit)
    - [Betting](#betting)
    - [Spinning the Slot Machine](#spinning-the-slot-machine)
    - [Checking Winnings](#checking-winnings)
4. [Functions](#functions)
5. [License](#license)

## Overview

The slot machine game simulates a basic slot machine with the following features:
- Four symbols (`A`, `B`, `C`, `D`) with different counts and values.
- Ability to place bets on multiple lines.
- A function to check for winning lines and calculate winnings.

## Setup

To run this game, you'll need Python installed. The code uses the `random` library which is included in the Python Standard Library, so no additional installations are required.

## Usage

### Deposit

The game starts by asking the player to deposit an amount of money. The deposit must be a positive number.

```python
def deposit():
    while True:
        amount = input("What would you like to deposit? $")
        if amount.isdigit():
            amount = int(amount)
            if amount > 0:
                break
            else:
                print("Amount must be greater than 0")
        else:
            print("Please enter a number.")
    return amount
```

### Betting

The player is prompted to select the number of lines to bet on and the amount to bet per line. The bet amount must be between $1 and $100.

```python
def get_number_of_lines():
    while True:
        lines = input("Enter the number of lines to bet on (1-3):")
        if lines.isdigit():
            lines = int(lines)
            if 1 <= lines <= 3:
                break
            else:
                print("Enter a valid number of lines")
        else:
            print("Please enter a number.")
    return lines

def get_bet():
    while True:
        amount = input("What would you like to bet on each line? $")
        if amount.isdigit():
            amount = int(amount)
            if 1 <= amount <= 100:
                break
            else:
                print("Amount must be between $1-$100.")
        else:
            print("Please enter a number.")
    return amount
```

### Spinning the Slot Machine

The slot machine is spun based on the player's bet. It generates random results for each column and displays them.

```python
def spin(balance):
    lines = get_number_of_lines()
    while True:
        bet = get_bet()
        total_bet = bet * lines

        if total_bet > balance:
            print(f"You have insufficient amount to bet, your current balance is ${balance}")
        else:
            break

    print(f"You are betting ${bet} on {lines} lines. Total bet is ${total_bet}")
    slots = get_slot_machine_spin(ROWS, COLS, symbol_count)
    print_slot_machine(slots)
    winnings, winning_lines = check_winnings(slots, lines, bet, symbol_value)
    print(f"You won ${winnings}.")
    print(f"You won on lines:", *winning_lines)
    return winnings - total_bet
```

### Checking Winnings

The winnings are calculated based on the symbols that appear in the winning lines. Each symbol has a predefined value, and winnings are computed accordingly.

```python
def check_winnings(Columns, lines, bet, values):
    winning_lines = []
    winnings = 0
    for line in range(lines):
        symbol = Columns[0][line]
        for column in Columns:
            symbol_to_check = column[line]
            if symbol != symbol_to_check:
                break
        else:
            winnings += values[symbol] * bet
            winning_lines.append(line + 1)
    return winnings, winning_lines
```

## Functions

- `deposit()`: Prompts the user to deposit an amount of money.
- `get_number_of_lines()`: Asks the user how many lines they want to bet on.
- `get_bet()`: Asks the user how much to bet per line.
- `spin(balance)`: Executes a spin, calculates winnings, and updates the balance.
- `check_winnings(Columns, lines, bet, values)`: Checks which lines are winning lines and calculates the winnings.
- `get_slot_machine_spin(rows, cols, symbols)`: Generates a random spin for the slot machine.
- `print_slot_machine(Columns)`: Prints the slot machine's current spin.

## License

This project is licensed under the MIT License. See the LICENSE file for more details.
