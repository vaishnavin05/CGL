#include <iostream>
#include <graphics.h>
#include <math.h>
using namespace std;

// Function to move the graphics cursor and draw a line
void move(int direction, int step, int &x, int &y) {
    if (direction == 1)        // Up
        y -= step;
    else if (direction == 2)   // Right
        x += step;
    else if (direction == 3)   // Down
        y += step;
    else if (direction == 4)   // Left
        x -= step;

    lineto(x, y);  // Draw a line to the new position
}

// Recursive function to draw the Hilbert Curve
void hilbert(int r, int d, int l, int u, int i, int h, int &x, int &y) {
    if (i > 0) {
        i--;

        // Hilbert Curve in the left rotation
        hilbert(d, r, u, l, i, h, x, y);

        move(r, h, x, y); // Move right
        hilbert(r, d, l, u, i, h, x, y);

        move(d, h, x, y); // Move down
        hilbert(r, d, l, u, i, h, x, y);

        move(l, h, x, y); // Move left
        hilbert(u, l, d, r, i, h, x, y);
    }
}

int main() {
    int n, x1, y1;
    int x0 = 25, y0 = 50; // Starting coordinates
    int x, y, h = 10;      // Step size
    int r = 2, d = 3, l = 4, u = 1; // Directions

    cout << "Enter the value of n (level of recursion): ";
    cin >> n;

    x = x0;
    y = y0;

    // Extended graphics window (e.g., 1024x768 resolution)
    int width = 1024;  // Desired width
    int height = 768;  // Desired height
    initwindow(width, height, "Hilbert Curve");

    moveto(x, y); // Move to the starting point
    hilbert(r, d, l, u, n, h, x, y); // Draw the Hilbert Curve

    delay(10000); // Pause to view the result
    closegraph(); // Close the graphics window
    return 0;
}
