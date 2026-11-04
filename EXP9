#include <iostream>
#include <vector>
#include <string>
#include <algorithm>
using namespace std;

int main() {
    string s1, s2;

    cout << "Enter first string: ";
    cin >> s1;

    cout << "Enter second string: ";
    cin >> s2;

    int m = s1.length();
    int n = s2.length();

    vector<vector<int>> dp(m + 1, vector<int>(n + 1, 0));

    // Build the DP table
    for (int i = 1; i <= m; i++) {
        for (int j = 1; j <= n; j++) {
            if (s1[i - 1] == s2[j - 1]) {
                dp[i][j] = 1 + dp[i - 1][j - 1];
            }
            else {
                dp[i][j] = max(dp[i - 1][j],
                               dp[i][j - 1]);
            }
        }
    }

    cout << "Length of LCS: " << dp[m][n] << endl;

    return 0;
}
