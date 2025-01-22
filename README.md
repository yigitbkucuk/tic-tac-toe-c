# tic-tac-toe-c

# Tic Tac Toe Game in C

This code implements a simple console-based Tic Tac Toe game for two players in the C programming language. Players alternate turns to place their markers (X or O) on a 3x3 board, and the game determines if there is a winner or if it ends in a draw.

# Code Implementation

#include <stdio.h>

char board[3][3];

void initialize_board() {
    int i, j;
    for (i = 0; i < 3; i++) {
        for (j = 0; j < 3; j++) {
            board[i][j] = '-';
        }
    }
}

void print_board() {
    int i, j;
    printf("\n  1 2 3\n");
    for (i = 0; i < 3; i++) {
        printf("%d ", i + 1);
        for (j = 0; j < 3; j++) {
            printf("%c ", board[i][j]);
        }
        printf("\n");
    }
    printf("\n");
}

int player_move(int row, int col, char player) {
    if (board[row - 1][col - 1] == '-') {
        board[row - 1][col - 1] = player;
        return 1;  // Valid move
    } else {
        printf("Invalid move, please try again.\n");
        return 0;  // Invalid move
    }
}

int check_game_over() {
    int i, j;
    // Check rows
    for (i = 0; i < 3; i++) {
        if (board[i][0] == board[i][1] && board[i][1] == board[i][2] && board[i][0] != '-') {
            return 1;  // Winner
        }
    }
    // Check columns
    for (i = 0; i < 3; i++) {
        if (board[0][i] == board[1][i] && board[1][i] == board[2][i] && board[0][i] != '-') {
            return 1;  // Winner
        }
    }
    // Check diagonals
    if ((board[0][0] == board[1][1] && board[1][1] == board[2][2] && board[0][0] != '-') ||
        (board[0][2] == board[1][1] && board[1][1] == board[2][0] && board[0][2] != '-')) {
        return 1;  // Winner
    }
    // Check for empty spaces (game ongoing)
    for (i = 0; i < 3; i++) {
        for (j = 0; j < 3; j++) {
            if (board[i][j] == '-') {
                return 0;  // Game ongoing
            }
        }
    }
    return -1;  // Draw
}

int main() {
    int row, col, game_over, valid_move;
    char player = 'X';
    initialize_board();
    while (1) {
        print_board();
        printf("Player %c, select row and column (1-3): ", player);

        // Loop until a valid move is made
        valid_move = 0;
        while (!valid_move) {
            scanf("%d %d", &row, &col);
            if (row < 1 || row > 3 || col < 1 || col > 3) {
                printf("Invalid row or column number, please try again.\n");
                continue;
            }
            valid_move = player_move(row, col, player);
        }

        game_over = check_game_over();
        if (game_over == 1) {
            print_board();
            printf("Player %c wins!\n", player);
            break;
        } else if (game_over == -1) {
            print_board();
            printf("The game is a draw.\n");
            break;
        }

        // Switch player after a valid move
        if (player == 'X') {
            player = 'O';
        } else {
            player = 'X';
        }
    }
    return 0;
}
