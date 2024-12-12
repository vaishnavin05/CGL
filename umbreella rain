#include <graphics.h>
#include <conio.h>
#include <dos.h>  // For delay function

// Function to draw a man walking with an umbrella
void drawMan(int x, int y) {
    // Draw head (circle)
    circle(x, y - 20, 10);

    // Draw body (line)
    line(x, y - 10, x, y + 20);

    // Draw legs (lines)
    line(x, y + 20, x - 10, y + 40);
    line(x, y + 20, x + 10, y + 40);

    // Draw arms (lines)
    line(x - 20, y, x + 20, y);

    // Draw umbrella (arc and lines)
    arc(x, y - 30, 0, 180, 20 ); // umbrella arc
    line(x, y - 30, x, y - 50);      // umbrella handle

    // Draw umbrella in man's hand (adjust position)
    line(x - 20, y - 10, x, y - 30); // line for umbrella handle in hand
}

// Function to simulate falling rain
void drawRain(int x, int y, int numDrops) {
    for (int i = 0; i < numDrops; i++) {
        int dropX = rand() % getmaxx();  // Random X position
        int dropY = rand() % getmaxy();  // Random Y position
        line(dropX, dropY, dropX, dropY + 5); // Raindrop line
    }
}

int main() {
    // Initialize graphics mode
    int gd = DETECT, gm;
    initgraph(&gd, &gm, "");

    // Set initial position of the man
    int x = 100, y = 200;

    // Draw ground
    setcolor(WHITE);
    line(0, getmaxy() - 20, getmaxx(), getmaxy() - 20);  // Ground line

    // Start animation loop
    while (!kbhit()) {
        // Clear the screen for each frame
        cleardevice();

        // Draw the ground
        setcolor(WHITE);
        line(0, getmaxy() - 20, getmaxx(), getmaxy() - 20);  // Ground line

        // Draw the man walking
        drawMan(x, y);

        // Draw the rain
        drawRain(x, y, 100);

        // Move the man to simulate walking
        x += 5;  // Move the man horizontally
        
        // Reset position when the man moves off the screen
        if (x > getmaxx()) {
            x = 0;
        }

        // Delay to control the speed of animation
        delay(50);  // Delay in milliseconds
    }

    // Close the graphics mode
    closegraph();
    return 0;
}
