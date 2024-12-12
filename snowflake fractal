#include <graphics.h>
#include <cmath>
#include <iostream>
using namespace std;

// Function to calculate the next point on the Koch curve
void kochCurve(int x1, int y1, int x2, int y2, int iterations) {
    if (iterations == 0) {
        // Draw the line segment
        line(x1, y1, x2, y2);
    } else {
        // Calculate the points that divide the segment into three equal parts
        int x3 = (2 * x1 + x2) / 3;
        int y3 = (2 * y1 + y2) / 3;
        
        int x4 = (x1 + 2 * x2) / 3;
        int y4 = (y1 + 2 * y2) / 3;

        // Find the peak of the equilateral triangle to form the new point
        int x5 = (x3 + x4) / 2 + (y4 - y3);
        int y5 = (y3 + y4) / 2 - (x4 - x3);

        // Recursively apply the Koch curve to the four new line segments
        kochCurve(x1, y1, x3, y3, iterations - 1);
        kochCurve(x3, y3, x5, y5, iterations - 1);
        kochCurve(x5, y5, x4, y4, iterations - 1);
        kochCurve(x4, y4, x2, y2, iterations - 1);
    }
}

// Function to draw the Koch snowflake fractal
void drawKochSnowflake(int x, int y, int size, int iterations) {
    // Calculate the 3 corners of an equilateral triangle
    int x1 = x;
    int y1 = y - size;

    int x2 = x + size * sqrt(3) / 2;
    int y2 = y + size / 2;

    int x3 = x - size * sqrt(3) / 2;
    int y3 = y + size / 2;

    // Apply the Koch curve algorithm to the 3 sides of the triangle
    kochCurve(x1, y1, x2, y2, iterations);
    kochCurve(x2, y2, x3, y3, iterations);
    kochCurve(x3, y3, x1, y1, iterations);
}

int main() {
    // Initialize graphics mode
    int gd = DETECT, gm;
    initgraph(&gd, &gm, "");

    // Set up the center and size of the snowflake
    int centerX = 300;
    int centerY = 300;
    int size = 150;
    int iterations = 4;  // Number of iterations for fractal depth

    // Draw the Koch snowflake
    drawKochSnowflake(centerX, centerY, size, iterations);

    // Wait for user input to close the window
    getch();
    closegraph();

    return 0;
}
