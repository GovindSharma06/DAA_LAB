#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

#define INF 99999

int main() {
    int n;

    cout << "Enter number of vertices: ";
    cin >> n;

    vector<vector<int>> dist(n, vector<int>(n));

    cout << "Enter adjacency matrix (-1 for no edge):\n";

    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            cin >> dist[i][j];

            if (dist[i][j] == -1) {
                dist[i][j] = INF;
            }
        }
    }

    // Floyd-Warshall Algorithm
    for (int k = 0; k < n; k++) {
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                if (dist[i][k] != INF &&
                    dist[k][j] != INF) {

                    dist[i][j] = min(
                        dist[i][j],
                        dist[i][k] + dist[k][j]
                    );
                }
            }
        }
    }

    cout << "\nShortest Distance Matrix:\n";

    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            if (dist[i][j] == INF) {
                cout << "INF ";
            }
            else {
                cout << dist[i][j] << " ";
            }
        }
        cout << endl;
    }

    return 0;
}
