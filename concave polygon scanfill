#include <iostream>
#include <graphics.h>
#include <vector>
#include <algorithm>
using namespace std;

class Polygon {
protected:
    vector<pair<int, int>> vertices; // To store the vertices of the polygon

public:
    void addVertex(int x, int y) {
        vertices.push_back({x, y});
    }

    void drawPolygon() {
        int n = vertices.size();
        for (int i = 0; i < n; i++) {
            line(vertices[i].first, vertices[i].second,
                 vertices[(i + 1) % n].first, vertices[(i + 1) % n].second);
        }
    }
};

class FilledPolygon : public Polygon {
public:
    void fillPolygon(int fillColor) {
        if (vertices.empty()) return;

        // Find the y-range of the polygon
        int ymin = vertices[0].second, ymax = vertices[0].second;
        for (auto &v : vertices) {
            ymin = min(ymin, v.second);
            ymax = max(ymax, v.second);
        }

        // For each scan line, find intersections
        for (int y = ymin; y <= ymax; y++) {
            vector<int> intersections;

            for (size_t i = 0; i < vertices.size(); i++) {
                int x1 = vertices[i].first;
                int y1 = vertices[i].second;
                int x2 = vertices[(i + 1) % vertices.size()].first;
                int y2 = vertices[(i + 1) % vertices.size()].second;

                // Check if the edge crosses the scan line
                if ((y1 <= y && y2 > y) || (y2 <= y && y1 > y)) {
                    int x = x1 + (y - y1) * (x2 - x1) / (y2 - y1);
                    intersections.push_back(x);
                }
            }

            // Sort the intersections
            sort(intersections.begin(), intersections.end());

            // Fill between pairs of intersections
            for (size_t i = 0; i < intersections.size(); i += 2) {
                line(intersections[i], y, intersections[i + 1], y);
            }
        }

        // Set the fill color
        setcolor(fillColor);
    }
};

int main() {
    int gd = DETECT, gm;
    initgraph(&gd, &gm, NULL);

    FilledPolygon polygon;
    
    // Example polygon: concave shape
    polygon.addVertex(200, 100);
    polygon.addVertex(300, 200);
    polygon.addVertex(250, 300);
    polygon.addVertex(150, 300);
    polygon.addVertex(100, 200);

    // Draw and fill the polygon
    polygon.drawPolygon();
    polygon.fillPolygon(YELLOW);

    getch();
    closegraph();
    return 0;
}
