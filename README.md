# Abhyudit
Maze Puzzle solver
#include <stdio.h>

#define ROW 5
#define COL 5

// Maze matrix: 1 = wall, 0 = path
int maze[ROW][COL] = {
    {0, 1, 0, 0, 0},
    {0, 1, 0, 1, 0},
    {0, 0, 0, 1, 0},
    {1, 1, 0, 1, 0},
    {0, 0, 0, 0, 0}
};

int visited[ROW][COL]; // Keep track of visited cells

// Directions: right, down, left, up
int dir[4][2] = { {0,1}, {1,0}, {0,-1}, {-1,0} };

int solveMaze(int x, int y) {
    if (x < 0 || y < 0 || x >= ROW || y >= COL)
        return 0; // Out of bounds
    if (maze[x][y] == 1 || visited[x][y])
        return 0; // Wall or already visited

    visited[x][y] = 1;

    if (x == ROW - 1 && y == COL - 1) {
        printf("(%d, %d)\n", x, y); // End found
        return 1;
    }

    for (int i = 0; i < 4; i++) {
        int newX = x + dir[i][0];
        int newY = y + dir[i][1];

        if (solveMaze(newX, newY)) {
            printf("(%d, %d)\n", x, y); // Print path
            return 1;
        }
    }

    return 0; // No path found
}

int main() {
    printf("Maze path (from end to start):\n");
    if (!solveMaze(0, 0)) {
        printf("No path found!\n");
    }
    return 0;
}
