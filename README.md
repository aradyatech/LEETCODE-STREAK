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

day 7
class Solution {
public:
    int minSumOfLengths(vector<int>& arr, int target) {
        int n = arr.size();
        const int INF = 1e9;

        vector<int> dp(n + 1, INF);

        int left = 0;
        int sum = 0;
        int ans = INF;

        for (int right = 0; right < n; right++) {
            sum += arr[right];

            while (sum > target) {
                sum -= arr[left];
                left++;
            }

            // Current subarray has sum = target
            if (sum == target) {
                int len = right - left + 1;

                // Check if a previous non-overlapping subarray exists
                if (dp[left] != INF) {
                    ans = min(ans, len + dp[left]);
                }

                // Minimum target-subarray length ending at/before right
                dp[right + 1] = min(dp[right], len);
            } 
            else {
                dp[right + 1] = dp[right];
            }
        }

        return ans == INF ? -1 : ans;
    }
};

day 8 
class Solution {
public:
    vector<string> maxNumOfSubstrings(string s) {
        vector<int> first(26, -1);
        vector<int> last(26, -1);

        // First and last occurrence
        for (int i = 0; i < s.size(); i++) {
            int c = s[i] - 'a';

            if (first[c] == -1)
                first[c] = i;

            last[c] = i;
        }

        // Store valid intervals {start, end}
        vector<pair<int, int>> intervals;

        for (int i = 0; i < s.size(); i++) {
            int c = s[i] - 'a';

            // Only start from first occurrence
            if (first[c] != i)
                continue;

            int end = last[c];
            bool valid = true;

            for (int j = i; j <= end; j++) {
                int x = s[j] - 'a';

                // This character appeared before i,
                // so we cannot make a valid substring
                if (first[x] < i) {
                    valid = false;
                    break;
                }

                // Need to include all occurrences of this character
                end = max(end, last[x]);
            }

            if (valid)
                intervals.push_back({i, end});
        }

        // Earliest ending interval first.
        // If same end, later start = shorter substring.
        sort(intervals.begin(), intervals.end(),
             [](pair<int, int> a, pair<int, int> b) {
                 if (a.second != b.second)
                     return a.second < b.second;

                 return a.first > b.first;
             });

        vector<string> ans;
        int prevEnd = -1;

        for (auto interval : intervals) {
            int start = interval.first;
            int end = interval.second;

            if (start > prevEnd) {
                ans.push_back(s.substr(start, end - start + 1));
                prevEnd = end;
            }
        }

        return ans;
    }
};
            }
        }

        return ans;
    }
};
