# Tic Tac Toe



## Lecture Code

```python
"""

Homage To The Panda

Display the Board
userTurn
computerTurn
Check for win or end

User is X
User goes first

"""
import sys
import random

# global variables
Board = ["1", "2", "3", "4", "5", "6", "7", "8", "9"]
GameMoves = 0
GameLoop = True


def displayBoard():
    print("Game Board")

    for c in range(9):
        if((c > 0) and (c % 3 == 0)):
            print()
        sys.stdout.write(Board[c].ljust(3))

    print("\n")


def resetVariables():
    global Board
    global GameMoves
    global GameLoop

    Board = ["1", "2", "3", "4", "5", "6", "7", "8", "9"]
    GameMoves = 0
    GameLoop = True

def userTurn():

    global GameMoves

    try:
        print("\nUser's Turn")

        displayBoard()

        userChoice = int(input("Please choose a square: ")) - 1

        if(Board[userChoice] != "X" and Board[userChoice] != "O"):
            Board[userChoice] = "X"
        else:
            # prevent cheating
            userTurn()

        displayBoard()

        GameMoves += 1

    except:
        print("Bad Choice - Please Try Again")
        userTurn()

def computerTurn():

    run = True
    global GameMoves

    while(run):
        ct = random.randint(0, 8)

        if(Board[ct] != "X" and Board[ct] != "O"):
            Board[ct] = "O"
            run = False
            GameMoves += 1

    displayBoard()


def checkForWinOrEnd(playerXO):

    global GamesMoves
    global GameLoop

    if(Board[0] == Board[1] == Board[2] == playerXO):
        print(playerXO + " wins")
        GameLoop = False
        return
    elif(Board[3] == Board[4] == Board[5] == playerXO):
        print(playerXO + " wins")
        GameLoop = False
        return
    elif(Board[6] == Board[7] == Board[8] == playerXO):
        print(playerXO + " wins")
        GameLoop = False
        return
    elif(Board[0] == Board[3] == Board[6] == playerXO):
        print(playerXO + " wins")
        GameLoop = False
        return
    elif(Board[1] == Board[4] == Board[7] == playerXO):
        print(playerXO + " wins")
        GameLoop = False
        return
    elif(Board[2] == Board[5] == Board[8] == playerXO):
        print(playerXO + " wins")
        GameLoop = False
        return
    elif(Board[0] == Board[4] == Board[8] == playerXO):
        print(playerXO + " wins")
        GameLoop = False
        return
    elif(Board[2] == Board[4] == Board[6] == playerXO):
        print(playerXO + " wins")
        GameLoop = False
        return

    if GameMoves == 9:
        GameLoop = False
        print("Tie - no winner")


def main():

    choice = "n"

    while choice != "y":

        displayBoard()

        while(GameLoop):
            userTurn()
            checkForWinOrEnd("X")

            if GameLoop == False:
                break

            computerTurn()
            checkForWinOrEnd("O")

        choice = input("Would you like quit? y/n ").lower()
        resetVariables()

    # userTurn()

    # for c in range(3):
    #    computerTurn()


main()

```

