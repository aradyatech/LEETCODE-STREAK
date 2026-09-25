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

    day 9 
    class Solution {
public:
    bool checkOverlap(int radius, int xCenter, int yCenter, 
                      int x1, int y1, int x2, int y2) {
        
        // Circle center ke nearest rectangle point
        int x = max(x1, min(xCenter, x2));
        int y = max(y1, min(yCenter, y2));
        
        // Distance squared
        int dx = xCenter - x;
        int dy = yCenter - y;
        
        return dx * dx + dy * dy <= radius * radius;
    }
};
};
            }
        }

        return ans;
    }
};

day 10
class Solution {
public:
    int reverseDegree(string s) {
        int ans = 0;

        for (int i = 0; i < s.length(); i++) {
            int reversePos = 26 - (s[i] - 'a');
            int stringPos = i + 1;

day 11 
class Solution {
public:
    vector<long long> resultArray(vector<int>& nums, int k) {
        vector<long long> ans(k, 0);
        
        vector<long long> dp(k, 0);

        for (int num : nums) {
            vector<long long> newDp(k, 0);

            // Subarray containing only num
            newDp[num % k]++;

            // Extend all previous subarrays
            for (int r = 0; r < k; r++) {
                if (dp[r] > 0) {
                    int newRemainder = (1LL * r * num) % k;
                    newDp[newRemainder] += dp[r];
                }
            }

            // Add counts to final answer
            for (int r = 0; r < k; r++) {
                ans[r] += newDp[r];
            }

            dp = newDp;
        }

        return ans;
    }
};
day 12 
class Solution {
    struct Node {
        int prod;
        int cnt[5];

        Node(int k = 5) {
            prod = 1;
            for (int i = 0; i < 5; i++)
                cnt[i] = 0;
        }
    };

    int k;
    vector<Node> tree;

    Node merge(Node &L, Node &R) {
        Node res;

        // Product of complete segment
        res.prod = (L.prod * R.prod) % k;

        // Prefixes completely inside left segment
        for (int r = 0; r < k; r++) {
            res.cnt[r] = L.cnt[r];
        }

        // Prefixes that take all of left
        // and some prefix of right
        for (int r = 0; r < k; r++) {
            int newRem = (L.prod * r) % k;
            res.cnt[newRem] += R.cnt[r];
        }

        return res;
    }

    void build(int node, int l, int r, vector<int>& nums) {
        if (l == r) {
            int rem = nums[l] % k;

            tree[node].prod = rem;
            tree[node].cnt[rem] = 1;

            return;
        }

        int mid = (l + r) / 2;

        build(node * 2, l, mid, nums);
        build(node * 2 + 1, mid + 1, r, nums);

        tree[node] = merge(tree[node * 2], tree[node * 2 + 1]);
    }

    void update(int node, int l, int r, int idx, int val) {
        if (l == r) {
            int rem = val % k;

            tree[node] = Node();
            tree[node].prod = rem;
            tree[node].cnt[rem] = 1;

            return;
        }

        int mid = (l + r) / 2;

        if (idx <= mid)
            update(node * 2, l, mid, idx, val);
        else
            update(node * 2 + 1, mid + 1, r, idx, val);

        tree[node] = merge(tree[node * 2], tree[node * 2 + 1]);
    }

    Node query(int node, int l, int r, int ql, int qr) {
        // Completely inside
        if (ql <= l && r <= qr)
            return tree[node];

        int mid = (l + r) / 2;

        // Only left
        if (qr <= mid)
            return query(node * 2, l, mid, ql, qr);

        // Only right
        if (ql > mid)
            return query(node * 2 + 1, mid + 1, r, ql, qr);

        // Both sides
        Node L = query(node * 2, l, mid, ql, qr);
        Node R = query(node * 2 + 1, mid + 1, r, ql, qr);

        return merge(L, R);
    }

public:
    vector<int> resultArray(vector<int>& nums, int K,
                            vector<vector<int>>& queries) {

        k = K;

        int n = nums.size();

        tree.resize(4 * n);

        build(1, 0, n - 1, nums);

        vector<int> ans;

        for (auto &q : queries) {

            int index = q[0];
            int value = q[1];
            int start = q[2];
            int x = q[3];

            // Permanent update
            update(1, 0, n - 1, index, value);

            // Query [start ... n-1]
            Node res = query(1, 0, n - 1, start, n - 1);

            ans.push_back(res.cnt[x]);
        }

        return ans;
    }
};

            ans += reversePos * stringPos;
        }

        return ans;
    }
};

day 15
class Solution {
public:
    int digitSum(int n) {
        int sum = 0;

        while (n > 0) {
            sum += n % 10;
            n /= 10;
        }

        return sum;
    }

    int smallestIndex(vector<int>& nums) {
        for (int i = 0; i < nums.size(); i++) {
            if (digitSum(nums[i]) == i) {
                return i;
            }
        }

        return -1;
    }
};
class Solution {
public:
    string s;
    int i;

    // Parses an expression until '}' or end
    set<string> parseExpression() {
        set<string> result;

        // First parse concatenated terms
        set<string> current = parseTerm();

        // Add current results
        result.insert(current.begin(), current.end());

        // Handle union: a,b,c
        while (i < s.size() && s[i] == ',') {
            i++;  // skip ','

            set<string> next = parseTerm();
            result.insert(next.begin(), next.end());
        }

        return result;
    }

    // Parses concatenation: ab{c,d}e
    set<string> parseTerm() {
        set<string> result;
        result.insert("");

        while (i < s.size() && s[i] != '}' && s[i] != ',') {

            set<string> part;

            // Single character
            if (s[i] >= 'a' && s[i] <= 'z') {
                part.insert(string(1, s[i]));
                i++;
            }

            // Braced expression
            else if (s[i] == '{') {
                i++;  // skip '{'

                part = parseExpression();

                i++;  // skip '}'
            }

            // Cartesian product for concatenation
            set<string> temp;

            for (string a : result) {
                for (string b : part) {
                    temp.insert(a + b);
                }
            }

            result = temp;
        }

        return result;
    }

    vector<string> braceExpansionII(string expression) {
        s = expression;
        i = 0;

        set<string> ans = parseExpression();

        return vector<string>(ans.begin(), ans.end());
    }
};
