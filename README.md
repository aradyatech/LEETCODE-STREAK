# LEETCODE-STREAK
DAY 5
class Solution {
public:
    bool isRectangleOverlap(vector<int>& rec1, vector<int>& rec2) {

        // No overlap in X direction
        if (rec1[2] <= rec2[0] || rec2[2] <= rec1[0])
            return false;

        // No overlap in Y direction
        if (rec1[3] <= rec2[1] || rec2[3] <= rec1[1])
            return false;

        return true;
    }
};
DAY 6 
class Solution {
public:
    int maxPalindromes(string s, int k) {

        int n = s.size();

        // dp[i][j] = true if s[i...j] is palindrome
        vector<vector<bool>> dp(n, vector<bool>(n, false));

        // Length 1
        for (int i = 0; i < n; i++) {
            dp[i][i] = true;
        }

        // Length 2 onwards
        for (int len = 2; len <= n; len++) {

            for (int i = 0; i + len - 1 < n; i++) {

                int j = i + len - 1;

                if (s[i] == s[j]) {

                    if (len == 2)
                        dp[i][j] = true;
                    else
                        dp[i][j] = dp[i + 1][j - 1];
                }
            }
        }

        int ans = 0;
        int lastEnd = -1;

        // Greedily choose palindrome with earliest ending position
        for (int r = 0; r < n; r++) {

            for (int l = lastEnd + 1; l <= r; l++) {

                if (r - l + 1 >= k && dp[l][r]) {

                    ans++;
                    lastEnd = r;

                    break;
                }
            }
        }

        return ans;
    }
};
