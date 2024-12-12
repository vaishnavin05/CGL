#include <iostream>
using namespace std;

// Defining the region codes
#define INSIDE 0  // 0000
#define LEFT 1    // 0001
#define RIGHT 2   // 0010
#define BOTTOM 4  // 0100
#define TOP 8     // 1000

// Define the rectangle as (xmin, ymin, xmax, ymax)
struct Rectangle {
    int xmin, ymin, xmax, ymax;
};

// Function to compute the region code for a point (x, y)
int computeRegionCode(int x, int y, Rectangle rect) {
    int code = INSIDE;
    
    if (x < rect.xmin)     // to the left of the rectangle
        code |= LEFT;
    else if (x > rect.xmax) // to the right of the rectangle
        code |= RIGHT;
    if (y < rect.ymin)     // below the rectangle
        code |= BOTTOM;
    else if (y > rect.ymax) // above the rectangle
        code |= TOP;

    return code;
}

// Function to implement Cohen-Sutherland clipping
void cohenSutherlandClip(int x1, int y1, int x2, int y2, Rectangle rect) {
    // Compute region codes for the endpoints of the line
    int code1 = computeRegionCode(x1, y1, rect);
    int code2 = computeRegionCode(x2, y2, rect);
    bool accept = false;

    while (true) {
        if ((code1 == 0) && (code2 == 0)) {
            // Both endpoints are inside, accept the line
            accept = true;
            break;
        }
        else if ((code1 & code2) != 0) {
            // Both endpoints are outside, reject the line
            break;
        }
        else {
            // Some portion of the line is inside, calculate the intersection
            int codeOut;
            int x, y;

            // Find the endpoint outside the rectangle
            if (code1 != 0)
                codeOut = code1;
            else
                codeOut = code2;

            // Calculate the intersection point
            if (codeOut & TOP) {
                x = x1 + (x2 - x1) * (rect.ymax - y1) / (y2 - y1);
                y = rect.ymax;
            }
            else if (codeOut & BOTTOM) {
                x = x1 + (x2 - x1) * (rect.ymin - y1) / (y2 - y1);
                y = rect.ymin;
            }
            else if (codeOut & RIGHT) {
                y = y1 + (y2 - y1) * (rect.xmax - x1) / (x2 - x1);
                x = rect.xmax;
            }
            else if (codeOut & LEFT) {
                y = y1 + (y2 - y1) * (rect.xmin - x1) / (x2 - x1);
                x = rect.xmin;
            }

            // Update the endpoint outside the rectangle
            if (codeOut == code1) {
                x1 = x;
                y1 = y;
                code1 = computeRegionCode(x1, y1, rect);
            }
            else {
                x2 = x;
                y2 = y;
                code2 = computeRegionCode(x2, y2, rect);
            }
        }
    }

    // If the line is accepted, print the clipped line coordinates
    if (accept) {
        cout << "Clipped line segment: (" << x1 << ", " << y1 << ") to (" << x2 << ", " << y2 << ")" << endl;
    }
    else {
        cout << "Line rejected" << endl;
    }
}

int main() {
    // Define the rectangle (xmin, ymin, xmax, ymax)
    Rectangle rect = { 10, 10, 50, 50 };

    // Define the line endpoints
    int x1 = 5, y1 = 5, x2 = 60, y2 = 60;

    cout << "Original line segment: (" << x1 << ", " << y1 << ") to (" << x2 << ", " << y2 << ")" << endl;

    // Call the clipping function
    cohenSutherlandClip(x1, y1, x2, y2, rect);

    return 0;
}
