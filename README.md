# Tic-Tac-Toe-Game-C-Language-Code-
This my first project during academics. When i studied in 1st year
<br>
Author:- Shivam Parashar
<br>
Code:-
#include <stdio.h>

#define SIZE 3

// Function prototypes
void printBoard(char board[SIZE][SIZE]);
int checkWin(char board[SIZE][SIZE]);
void makeMove(char board[SIZE][SIZE], int player);

int main() {
    char board[SIZE][SIZE] = {
        {'1', '2', '3'},
        {'4', '5', '6'},
        {'7', '8', '9'}
    };
    int player = 1;
    int status = 0; // 0: Continue, 1: Win, -1: Draw

    while (status == 0) {
        printBoard(board);
        makeMove(board, player);
        status = checkWin(board);

        if (status == 0) {
            player = (player == 1) ? 2 : 1; // Switch player
        }
    }

    printBoard(board);

    if (status == 1) {
        printf("Player %d wins!\n", player);
    } else {
        printf("It's a draw!\n");
    }

    return 0;
}

void printBoard(char board[SIZE][SIZE]) {
    printf("\n");
    for (int i = 0; i < SIZE; i++) {
        for (int j = 0; j < SIZE; j++) {
            printf(" %c ", board[i][j]);
            if (j < SIZE - 1) {
                printf("|");
            }
        }
        printf("\n");
        if (i < SIZE - 1) {
            printf("---+---+---\n");
        }
    }
    printf("\n");
}

int checkWin(char board[SIZE][SIZE]) {
    // Check rows and columns
    for (int i = 0; i < SIZE; i++) {
        if (board[i][0] == board[i][1] && board[i][1] == board[i][2]) {
            return 1;
        }
        if (board[0][i] == board[1][i] && board[1][i] == board[2][i]) {
            return 1;
        }
    }

    // Check diagonals
    if (board[0][0] == board[1][1] && board[1][1] == board[2][2]) {
        return 1;
    }
    if (board[0][2] == board[1][1] && board[1][1] == board[2][0]) {
        return 1;
    }

    // Check for draw
    int draw = 1;
    for (int i = 0; i < SIZE; i++) {
        for (int j = 0; j < SIZE; j++) {
            if (board[i][j] != 'X' && board[i][j] != 'O') {
                draw = 0;
                break;
            }
        }
    }

    if (draw) {
        return -1;
    }

    return 0;
}

void makeMove(char board[SIZE][SIZE], int player) {
    int move;
    char mark = (player == 1) ? 'X' : 'O';

    printf("Player %d, enter your move (1-9): ", player);
    scanf("%d", &move);

    // Map move to board position
    int row = (move - 1) / SIZE;
    int col = (move - 1) % SIZE;

    if (move < 1 || move > 9 || board[row][col] == 'X' || board[row][col] == 'O') {
        printf("Invalid move. Try again.\n");
        makeMove(board, player);
    } else {
        board[row][col] = mark;
    }
}

