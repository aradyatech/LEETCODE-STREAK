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
                day 7 
                class Solution {
public:
    long long power(long long a, long long b, long long mod) {
        long long res = 1;

        while (b > 0) {
            if (b & 1)
                res = res * a % mod;

            a = a * a % mod;
            b >>= 1;
        }

        return res;
    }

    int numberOfSets(int n, int k) {
        const long long MOD = 1000000007;

        int N = n + k - 1;
        int R = 2 * k;

        // factorial
        vector<long long> fact(N + 1, 1);

        for (int i = 1; i <= N; i++)
            fact[i] = fact[i - 1] * i % MOD;

        // C(N,R) = fact[N] / (fact[R] * fact[N-R])
        long long numerator = fact[N];

        long long denominator =
            fact[R] * fact[N - R] % MOD;

        // Modular inverse using Fermat's Little Theorem
        long long inverse =
            power(denominator, MOD - 2, MOD);

        return numerator * inverse % MOD;
    }
};
            }
        }

        return ans;
    }
};
