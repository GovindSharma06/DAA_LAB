#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
    int n, W;

    cout << "Enter number of items: ";
    cin >> n;

    vector<int> weight(n), profit(n);

    cout << "Enter weights of items:\n";
    for (int i = 0; i < n; i++) {
        cin >> weight[i];
    }

    cout << "Enter profits of items:\n";
    for (int i = 0; i < n; i++) {
        cin >> profit[i];
    }

    cout << "Enter knapsack capacity: ";
    cin >> W;

    vector<vector<int>> dp(
        n + 1, vector<int>(W + 1, 0)
    );

    // Build DP table
    for (int i = 1; i <= n; i++) {
        for (int w = 0; w <= W; w++) {

            if (weight[i - 1] <= w) {
                dp[i][w] = max(
                    profit[i - 1] + dp[i - 1][w - weight[i - 1]],
                    dp[i - 1][w]
                );
            }
            else {
                dp[i][w] = dp[i - 1][w];
            }
        }
    }

    cout << "Maximum Profit: " << dp[n][W] << endl;

    return 0;
}
