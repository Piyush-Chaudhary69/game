#include <stdio.h>
#include <stdbool.h>

#define SIZE 9

int board[SIZE][SIZE] = {
    {5, 3, 0, 0, 7, 0, 0, 0, 0},
    {6, 0, 0, 1, 9, 5, 0, 0, 0},
    {0, 9, 8, 0, 0, 0, 0, 6, 0},
    {8, 0, 0, 0, 6, 0, 0, 0, 3},
    {4, 0, 0, 8, 0, 3, 0, 0, 1},
    {7, 0, 0, 0, 2, 0, 0, 0, 6},
    {0, 6, 0, 0, 0, 0, 2, 8, 0},
    {0, 0, 0, 4, 1, 9, 0, 0, 5},
    {0, 0, 0, 0, 8, 0, 0, 7, 9}
};

void printBoard() {
    for (int i = 0; i < SIZE; i++) {
        if (i % 3 == 0 && i != 0) printf("---------------------\n");
        for (int j = 0; j < SIZE; j++) {
            if (j % 3 == 0 && j != 0) printf("| ");
            printf("%d ", board[i][j]);
        }
        printf("\n");
    }
}

bool isValid(int row, int col, int num) {
    for (int x = 0; x < SIZE; x++) {
        if (board[row][x] == num || board[x][col] == num)
            return false;
    }

    int startRow = row - row % 3, startCol = col - col % 3;
    for (int i = startRow; i < startRow + 3; i++) {
        for (int j = startCol; j < startCol + 3; j++) {
            if (board[i][j] == num)
                return false;
        }
    }

    return true;
}

int main() {
    int row, col, num;
    printBoard();

    while (1) {
        printf("Enter row (0-8), column (0-8), and number (1-9): ");
        scanf("%d %d %d", &row, &col, &num);

        if (row == -1) break; // Exit condition

        if (board[row][col] == 0 && isValid(row, col, num)) {
            board[row][col] = num;
        } else {
            printf("Invalid move!\n");
        }

        printBoard();
    }

    return 0;
}

