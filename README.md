#include <iostream>
using namespace std;

char board[3][3] = {
    {'1', '2', '3'},
    {'4', '5', '6'},
    {'7', '8', '9'}
};

// Display the game board
void displayBoard() {
    cout << "\n";
    cout << "     |     |     \n";
    cout << "  " << board[0][0] << "  |  " << board[0][1] << "  |  " << board[0][2] << "\n";
    cout << "_____|_____|_____\n";
    cout << "     |     |     \n";
    cout << "  " << board[1][0] << "  |  " << board[1][1] << "  |  " << board[1][2] << "\n";
    cout << "_____|_____|_____\n";
    cout << "     |     |     \n";
    cout << "  " << board[2][0] << "  |  " << board[2][1] << "  |  " << board[2][2] << "\n";
    cout << "     |     |     \n\n";
}

// Check whether a player has won
bool checkWin(char player) {
    // Check rows
    for (int i = 0; i < 3; i++) {
        if (board[i][0] == player &&
            board[i][1] == player &&
            board[i][2] == player) {
            return true;
        }
    }

    // Check columns
    for (int i = 0; i < 3; i++) {
        if (board[0][i] == player &&
            board[1][i] == player &&
            board[2][i] == player) {
            return true;
        }
    }

    // Check diagonals
    if (board[0][0] == player &&
        board[1][1] == player &&
        board[2][2] == player) {
        return true;
    }

    if (board[0][2] == player &&
        board[1][1] == player &&
        board[2][0] == player) {
        return true;
    }

    return false;
}

// Check whether the board is full
bool checkDraw() {
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            if (board[i][j] >= '1' && board[i][j] <= '9') {
                return false;
            }
        }
    }

    return true;
}

// Place the player's move
bool makeMove(int position, char player) {
    if (position < 1 || position > 9) {
        return false;
    }

    int row = (position - 1) / 3;
    int col = (position - 1) % 3;

    // Check if the position is already occupied
    if (board[row][col] == 'X' || board[row][col] == 'O') {
        return false;
    }

    board[row][col] = player;
    return true;
}

int main() {
    int position;
    char currentPlayer = 'X';

    cout << "=============================\n";
    cout << "       TIC-TAC-TOE GAME      \n";
    cout << "=============================\n";

    cout << "\nPlayer 1: X";
    cout << "\nPlayer 2: O\n";

    while (true) {
        displayBoard();

        cout << "Player " << currentPlayer
             << ", enter a position (1-9): ";
        cin >> position;

        // Handle invalid input
        if (cin.fail()) {
            cin.clear();
            cin.ignore(10000, '\n');
            cout << "Invalid input! Please enter a number.\n";
            continue;
        }

        // Try to make the move
        if (!makeMove(position, currentPlayer)) {
            cout << "Invalid move! Choose an empty position from 1-9.\n";
            continue;
        }

        // Check for winner
        if (checkWin(currentPlayer)) {
            displayBoard();
            cout << "Congratulations! Player "
                 << currentPlayer << " wins!\n";
            break;
        }

        // Check for draw
        if (checkDraw()) {
            displayBoard();
            cout << "It's a draw!\n";
            break;
        }

        // Change player
        if (currentPlayer == 'X') {
            currentPlayer = 'O';
        } else {
            currentPlayer = 'X';
        }
    }

    cout << "\nThanks for playing!\n";

    return 0;
}
