#include <graphics.h>
#include <conio.h>
#include <cmath>
#include <iostream>
using namespace std;

// Base class Shape for polymorphism
class Shape {
public:
    virtual void draw(int time) = 0;  // Pure virtual function for drawing
};

// Class for Ball derived from Shape
class Ball : public Shape {
    int x, y, radius;
    float amplitude, frequency, velocity;
    int groundLevel;

public:
    Ball(int startX, int startY, int r, int ground) : x(startX), y(startY), radius(r), groundLevel(ground) {
        amplitude = 100;    // Amplitude for sine wave (height of the bounce)
        frequency = 0.1f;   // Frequency for sine wave (speed of the bounce)
        velocity = 5;       // Horizontal velocity (speed of the ball's movement)
    }

    // Override the draw function to implement sine wave motion for the ball
    void draw(int time) override {
        // Calculate new Y position using sine wave function (vertical bounce)
        // Adjust sine wave to bounce on the ground level
        y = groundLevel - amplitude + amplitude * sin(frequency * time);

        // Move the ball horizontally (right direction)
        x += velocity;

        // If the ball goes off the right side, reset its position
        if (x > getmaxx()) {
            x = 0;  // Reset to the left side of the screen
        }

        // Filling the ball with color (solid circle)
        setcolor(RED);
        setfillstyle(SOLID_FILL, RED);
        fillellipse(x, y, radius, radius);  // Filled circle for the ball
    }

    // Draw the ground
    void drawGround() {
        setcolor(GREEN);
        line(0, groundLevel, getmaxx(), groundLevel);  // Draw a line for the ground at groundLevel
    }
};

int main() {
    int gd = DETECT, gm;
    initgraph(&gd, &gm, "");

    // Create Ball object, ground at Y = 400 (move it further below)
    int groundLevel = 400;  // Move the ground further down
    Ball ball(0, groundLevel - 100, 20, groundLevel);  // Start at x=0, y=300, radius=20

    int time = 0;
    // Loop to animate the ball
    while (!kbhit()) {
        cleardevice();  // Clear the screen

        // Draw the ground
        ball.drawGround();

        // Draw the ball with current time
        ball.draw(time);

        time++;  // Increment time to animate sine wave
        delay(10);  // Delay for smooth animation
    }

    closegraph();
    return 0;
}
