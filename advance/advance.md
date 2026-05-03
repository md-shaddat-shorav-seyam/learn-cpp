Here are all the advanced C++ competitive programming techniques with examples, in full markdown format:

---

# 🚀 Advanced C++ Competitive Programming Techniques

---

## 1. 📊 Data Structures

### 1.1 Segment Tree
**Complexity:** O(log n) per query/update

A binary tree where each node stores aggregate info (sum, min, max) over a segment of the array.

**Use case:** Range sum queries with point updates.

```cpp
#include <bits/stdc++.h>
using namespace std;
const int MAXN = 100005;
int tree[4*MAXN];

void build(int node, int s, int e, int arr[]) {
    if (s == e) { tree[node] = arr[s]; return; }
    int mid = (s+e)/2;
    build(2*node, s, mid, arr);
    build(2*node+1, mid+1, e, arr);
    tree[node] = tree[2*node] + tree[2*node+1];
}

int query(int node, int s, int e, int l, int r) {
    if (r < s || e < l) return 0;
    if (l <= s && e <= r) return tree[node];
    int mid = (s+e)/2;
    return query(2*node, s, mid, l, r)
         + query(2*node+1, mid+1, e, l, r);
}
```

**Sample Output:**
```
arr = [1, 3, 5, 7, 9, 11]
query(l=1, r=3) = 3+5+7 = 15
query(l=2, r=5) = 5+7+9+11 = 32
```

---

### 1.2 Fenwick Tree (BIT)
**Complexity:** O(log n) update & prefix query

Binary Indexed Tree — space-efficient prefix sums using the `lowbit` (i & -i) trick.

**Use case:** Count inversions, prefix frequency queries.

```cpp
#include <bits/stdc++.h>
using namespace std;
int bit[100005], n;

void update(int i, int delta) {
    for (; i <= n; i += i & (-i))
        bit[i] += delta;
}

int query(int i) {
    int sum = 0;
    for (; i > 0; i -= i & (-i))
        sum += bit[i];
    return sum;
}

int rangeSum(int l, int r) {
    return query(r) - query(l - 1);
}
```

**Sample Output:**
```
update(3, 5), update(5, 2)
rangeSum(2, 5) = 7
```

---

### 1.3 Sparse Table (RMQ)
**Complexity:** O(1) query, O(n log n) build

Precomputes range minimums for all power-of-2 intervals. Ideal for static arrays.

**Use case:** Range minimum/maximum on static arrays.

```cpp
#include <bits/stdc++.h>
using namespace std;
const int MAXN = 100005, LOG = 17;
int sparse[MAXN][LOG], lg[MAXN];

void build(int arr[], int n) {
    for (int i = 0; i < n; i++) sparse[i][0] = arr[i];
    for (int j = 1; j < LOG; j++)
        for (int i = 0; i + (1<<j) - 1 < n; i++)
            sparse[i][j] = min(sparse[i][j-1],
                               sparse[i+(1<<(j-1))][j-1]);
}

int query(int l, int r) {
    int k = lg[r-l+1];
    return min(sparse[l][k], sparse[r-(1<<k)+1][k]);
}
```

**Sample Output:**
```
arr = [2, 4, 3, 1, 6, 7, 8, 9]
RMQ(0, 7) = 1
RMQ(1, 4) = 1
RMQ(5, 7) = 7
```

---

### 1.4 Mo's Algorithm
**Complexity:** O((N + Q)√N)

Offline range query algorithm. Sorts queries by block to minimize total pointer movement.

**Use case:** Count distinct elements in range queries offline.

```cpp
#include <bits/stdc++.h>
using namespace std;
int block;
struct Query { int l, r, idx; };

bool cmp(Query a, Query b) {
    if (a.l/block != b.l/block)
        return a.l/block < b.l/block;
    return (a.l/block & 1) ? a.r > b.r : a.r < b.r;
}

int cnt[100005], curAns = 0;

void add(int pos, int arr[]) {
    if (++cnt[arr[pos]] == 1) curAns++;
}
void remove(int pos, int arr[]) {
    if (--cnt[arr[pos]] == 0) curAns--;
}
```

**Sample Output:**
```
arr = [1,2,1,3,2], queries: [(0,2),(1,3),(2,4)]
block = sqrt(5) ≈ 2
Distinct in [0,2] = 2
Distinct in [1,3] = 3
Distinct in [2,4] = 3
```

---

## 2. 🧮 Dynamic Programming

### 2.1 Bitmask DP
**Complexity:** O(2ⁿ × n)

DP over all subsets encoded as bitmasks. Classic for TSP and assignment problems.

**Use case:** Minimum cost Travelling Salesman Problem.

```cpp
#include <bits/stdc++.h>
using namespace std;
const int INF = 1e9;
int dist[10][10];
int dp[1<<10][10];

int tsp(int n) {
    for (auto& row : dp) fill(row.begin(), row.end(), INF);
    dp[1][0] = 0;
    for (int mask = 1; mask < (1<<n); mask++) {
        for (int u = 0; u < n; u++) {
            if (!(mask & (1<<u)) || dp[mask][u] == INF) continue;
            for (int v = 0; v < n; v++) {
                if (mask & (1<<v)) continue;
                int nmask = mask | (1<<v);
                dp[nmask][v] = min(dp[nmask][v],
                                   dp[mask][u] + dist[u][v]);
            }
        }
    }
    int ans = INF;
    for (int u = 1; u < n; u++)
        ans = min(ans, dp[(1<<n)-1][u] + dist[u][0]);
    return ans;
}
```

**Sample Output:**
```
Cities: 4, optimal TSP tour cost = 20
All 2^4 = 16 subsets explored
dp[(1111)][3] = min cost visiting all, ending at 3
```

---

### 2.2 Convex Hull Trick (CHT)
**Complexity:** O(n) amortized with monotone queries

Optimizes DP of the form `dp[i] = min(dp[j] + b[j]*x[i])` using a deque of lines.

**Use case:** Min cost splitting problems with linear cost functions.

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
struct Line { ll m, b; ll eval(ll x) { return m*x + b; } };

struct CHT {
    deque<Line> hull;
    bool bad(Line l1, Line l2, Line l3) {
        return (__int128)(l3.b-l1.b)*(l1.m-l2.m)
             <= (__int128)(l2.b-l1.b)*(l1.m-l3.m);
    }
    void addLine(ll m, ll b) {
        Line l = {m, b};
        while (hull.size() >= 2 && bad(hull[hull.size()-2], hull.back(), l))
            hull.pop_back();
        hull.push_back(l);
    }
    ll query(ll x) {
        while (hull.size() > 1 && hull[0].eval(x) >= hull[1].eval(x))
            hull.pop_front();
        return hull[0].eval(x);
    }
};
```

**Sample Output:**
```
Lines: y=3x+2, y=x+5, y=2x+1
At x=0: min(2, 5, 1) = 1
At x=3: min(11, 8, 7) = 7
At x=6: min(20, 11, 13) = 11
```

---

### 2.3 Digit DP
**Complexity:** O(digits × states)

Count numbers in [0, N] satisfying digit-level constraints by memoizing over position, state, and tight flag.

**Use case:** Count numbers ≤ N with digit sum = K.

```cpp
#include <bits/stdc++.h>
using namespace std;
string num;
int dp[20][200][2];

int solve(int pos, int sum, bool tight) {
    if (pos == (int)num.size()) return sum == 0;
    if (dp[pos][sum][tight] != -1)
        return dp[pos][sum][tight];
    int limit = tight ? (num[pos]-'0') : 9;
    int res = 0;
    for (int d = 0; d <= limit; d++)
        res += solve(pos+1, sum-d, tight && d == limit);
    return dp[pos][sum][tight] = res;
}
// Usage: memset(dp, -1, sizeof(dp)); solve(0, K, true);
```

**Sample Output:**
```
Count numbers ≤ 100 with digit sum = 5:
{5, 14, 23, 32, 41, 50} → answer = 6
tight flag ensures we never exceed N
```

---

### 2.4 SOS DP (Sum over Subsets)
**Complexity:** O(n × 2ⁿ)

Compute for each bitmask the sum over all its subsets in O(n × 2ⁿ) instead of O(3ⁿ) brute force.

**Use case:** AND/OR convolution, subset sum aggregation.

```cpp
#include <bits/stdc++.h>
using namespace std;
int dp[1<<20];

void sos(int n) {
    // dp[mask] initially holds f(mask)
    for (int i = 0; i < n; i++)
        for (int mask = 0; mask < (1<<n); mask++)
            if (mask & (1<<i))
                dp[mask] += dp[mask ^ (1<<i)];
    // now dp[mask] = sum of f(s) for all s ⊆ mask
}
```

**Sample Output:**
```
n=3, f indexed by mask:
dp[000] = 1
dp[001] = f[000]+f[001] = 3
dp[011] = f[000]+f[001]+f[010]+f[011] = 15
dp[111] = sum of all = 255
```

---

### 2.5 Interval DP
**Complexity:** O(n³)

DP over all intervals [i, j]. Optimal substructure splits interval at some point k.

**Use case:** Minimum cost of matrix chain multiplication, balloon burst.

```cpp
#include <bits/stdc++.h>
using namespace std;

// Balloon Burst (Leetcode 312)
int maxCoins(vector<int>& nums) {
    int n = nums.size();
    nums.insert(nums.begin(), 1);
    nums.push_back(1);
    int N = nums.size();
    vector<vector<int>> dp(N, vector<int>(N, 0));
    for (int len = 2; len < N; len++) {
        for (int i = 0; i < N-len; i++) {
            int j = i + len;
            for (int k = i+1; k < j; k++) {
                dp[i][j] = max(dp[i][j],
                    dp[i][k] + nums[i]*nums[k]*nums[j] + dp[k][j]);
            }
        }
    }
    return dp[0][N-1];
}
```

**Sample Output:**
```
nums = [3, 1, 5, 8]
Burst order: 1→5→3→8
Max coins = 3*1*5 + 3*5*8 + 1*3*8 + 1*8*1 = 167
```

---

## 3. 🔤 Strings

### 3.1 KMP Algorithm
**Complexity:** O(n + m)

Uses a failure function (lps array) to avoid redundant character comparisons during pattern matching.

**Use case:** Find all occurrences of pattern in text.

```cpp
#include <bits/stdc++.h>
using namespace std;

vector<int> computeLPS(string pat) {
    int m = pat.size();
    vector<int> lps(m, 0);
    int len = 0, i = 1;
    while (i < m) {
        if (pat[i] == pat[len]) { lps[i++] = ++len; }
        else if (len) len = lps[len-1];
        else lps[i++] = 0;
    }
    return lps;
}

vector<int> kmpSearch(string txt, string pat) {
    auto lps = computeLPS(pat);
    vector<int> res;
    int i = 0, j = 0;
    while (i < (int)txt.size()) {
        if (txt[i] == pat[j]) { i++; j++; }
        if (j == (int)pat.size()) {
            res.push_back(i-j);
            j = lps[j-1];
        } else if (i < (int)txt.size() && txt[i] != pat[j])
            j ? j = lps[j-1] : i++;
    }
    return res;
}
```

**Sample Output:**
```
text    = "AABAACAADAABAABA"
pattern = "AABA"
LPS     = [0, 1, 0, 1]
Matches at indices: 0, 9, 12
```

---

### 3.2 Z-Algorithm
**Complexity:** O(n)

Z[i] = length of the longest substring starting at i that matches a prefix of the string.

**Use case:** Pattern matching, finding string period.

```cpp
#include <bits/stdc++.h>
using namespace std;

vector<int> zFunction(string s) {
    int n = s.size();
    vector<int> z(n, 0);
    z[0] = n;
    int l = 0, r = 0;
    for (int i = 1; i < n; i++) {
        if (i < r) z[i] = min(r-i, z[i-l]);
        while (i+z[i] < n && s[z[i]] == s[i+z[i]])
            z[i]++;
        if (i+z[i] > r) { l = i; r = i+z[i]; }
    }
    return z;
}
// To search pattern P in text T:
// build Z of (P + "$" + T)
// Z[i] == len(P) => match at position i-len(P)-1
```

**Sample Output:**
```
s = "aabxaa"
Z = [6, 1, 0, 0, 2, 1]
Pattern "aab" in "aabxaaab":
Z-array of "aab$aabxaaab"
Z[4]=3 → match found at index 0
```

---

### 3.3 Suffix Array + LCP
**Complexity:** O(n log n) build

Sorted array of all suffixes. Combined with LCP array it enables powerful substring queries.

**Use case:** Count distinct substrings, longest repeated substring.

```cpp
#include <bits/stdc++.h>
using namespace std;

vector<int> buildSA(string s) {
    s += '$'; int n = s.size();
    vector<int> sa(n), rank_(n), tmp(n);
    iota(sa.begin(), sa.end(), 0);
    for (int i = 0; i < n; i++) rank_[i] = s[i];
    for (int gap = 1; gap < n; gap *= 2) {
        auto cmp = [&](int a, int b) {
            if (rank_[a] != rank_[b]) return rank_[a] < rank_[b];
            int ra = a+gap<n ? rank_[a+gap] : -1;
            int rb = b+gap<n ? rank_[b+gap] : -1;
            return ra < rb;
        };
        sort(sa.begin(), sa.end(), cmp);
        tmp[sa[0]] = 0;
        for (int i = 1; i < n; i++)
            tmp[sa[i]] = tmp[sa[i-1]] + (cmp(sa[i-1], sa[i]) ? 1 : 0);
        rank_ = tmp;
    }
    return sa;
}
```

**Sample Output:**
```
s = "banana"
SA = [6, 5, 3, 1, 0, 4, 2]
Sorted: "$","a$","ana$","anana$","banana$","na$","nana$"
Distinct substrings = n(n+1)/2 - sum(LCP) = 15
```

---

### 3.4 Aho-Corasick Automaton
**Complexity:** O(total pattern length + text length)

Multi-pattern matching using a trie with failure links (similar to KMP failure function on a trie).

**Use case:** Find all occurrences of multiple patterns simultaneously in a text.

```cpp
#include <bits/stdc++.h>
using namespace std;

struct AhoCorasick {
    vector<array<int,26>> go;
    vector<int> fail, out;
    AhoCorasick() { go.push_back({}); go[0].fill(-1); fail.push_back(0); out.push_back(0); }

    void insert(string& s, int idx) {
        int cur = 0;
        for (char c : s) {
            int ch = c-'a';
            if (go[cur][ch] == -1) {
                go[cur][ch] = go.size();
                go.push_back({}); go.back().fill(-1);
                fail.push_back(0); out.push_back(0);
            }
            cur = go[cur][ch];
        }
        out[cur] |= (1 << idx);
    }

    void build() {
        queue<int> q;
        for (int c = 0; c < 26; c++) {
            if (go[0][c] == -1) go[0][c] = 0;
            else { fail[go[0][c]] = 0; q.push(go[0][c]); }
        }
        while (!q.empty()) {
            int u = q.front(); q.pop();
            out[u] |= out[fail[u]];
            for (int c = 0; c < 26; c++) {
                if (go[u][c] == -1) go[u][c] = go[fail[u]][c];
                else { fail[go[u][c]] = go[fail[u]][c]; q.push(go[u][c]); }
            }
        }
    }
};
```

**Sample Output:**
```
patterns = {"he", "she", "his", "hers"}
text     = "ushers"
Matches: "she" at 1, "he" at 2, "hers" at 2
All found in single O(n) pass
```

---

## 4. 📈 Graph Algorithms

### 4.1 Dijkstra's Algorithm
**Complexity:** O((V + E) log V)

Single-source shortest paths on graphs with non-negative weights using a min-heap.

**Use case:** Shortest path from a source to all nodes.

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef pair<int,int> pii;
const int INF = 1e9;
vector<pii> adj[100005];

vector<int> dijkstra(int src, int n) {
    vector<int> dist(n+1, INF);
    priority_queue<pii, vector<pii>, greater<pii>> pq;
    dist[src] = 0;
    pq.push({0, src});
    while (!pq.empty()) {
        auto [d, u] = pq.top(); pq.pop();
        if (d > dist[u]) continue;
        for (auto [w, v] : adj[u]) {
            if (dist[u] + w < dist[v]) {
                dist[v] = dist[u] + w;
                pq.push({dist[v], v});
            }
        }
    }
    return dist;
}
```

**Sample Output:**
```
Graph: 1-2(4), 1-3(1), 3-2(2), 2-4(1)
Source: 1
dist = [0, 3, 1, 4]
Shortest to 2: 1→3→2 (cost 3)
```

---

### 4.2 Tarjan's SCC
**Complexity:** O(V + E)

Finds all Strongly Connected Components using DFS with discovery times and low-link values.

**Use case:** 2-SAT, condensation graph, cycle detection.

```cpp
#include <bits/stdc++.h>
using namespace std;
int low[100005], disc[100005], scc_id[100005];
bool onStack[100005];
stack<int> st;
int timer_val = 0, numSCC = 0;
vector<int> adj[100005];

void dfs(int u) {
    low[u] = disc[u] = timer_val++;
    st.push(u); onStack[u] = true;
    for (int v : adj[u]) {
        if (!disc[v]) { dfs(v); low[u] = min(low[u], low[v]); }
        else if (onStack[v]) low[u] = min(low[u], disc[v]);
    }
    if (low[u] == disc[u]) {
        while (true) {
            int v = st.top(); st.pop();
            onStack[v] = false;
            scc_id[v] = numSCC;
            if (v == u) break;
        }
        numSCC++;
    }
}
```

**Sample Output:**
```
Graph: 0→1, 1→2, 2→0, 1→3, 3→4, 4→3
SCCs: {0,1,2}, {3,4}
numSCC = 2
```

---

### 4.3 LCA (Binary Lifting)
**Complexity:** O(n log n) build, O(log n) query

Precomputes 2^k-th ancestors to answer LCA queries in O(log n).

**Use case:** Tree path queries, distance between nodes.

```cpp
#include <bits/stdc++.h>
using namespace std;
const int LOG = 17;
int up[100005][LOG], depth[100005];
vector<int> adj[100005];

void dfs(int u, int p, int d) {
    up[u][0] = p; depth[u] = d;
    for (int j = 1; j < LOG; j++)
        up[u][j] = up[up[u][j-1]][j-1];
    for (int v : adj[u]) if (v != p) dfs(v, u, d+1);
}

int lca(int u, int v) {
    if (depth[u] < depth[v]) swap(u, v);
    int diff = depth[u] - depth[v];
    for (int j = 0; j < LOG; j++)
        if ((diff>>j)&1) u = up[u][j];
    if (u == v) return u;
    for (int j = LOG-1; j >= 0; j--)
        if (up[u][j] != up[v][j]) { u = up[u][j]; v = up[v][j]; }
    return up[u][0];
}
```

**Sample Output:**
```
Tree: root=1, edges 1-2, 1-3, 2-4, 2-5, 3-6
lca(4, 5) = 2
lca(4, 6) = 1
dist(4, 6) = depth[4]+depth[6] - 2*depth[lca] = 3
```

---

### 4.4 Dinic's Max Flow
**Complexity:** O(V² × E)

Fastest max flow in practice. BFS builds a level graph; DFS sends blocking flows repeatedly.

**Use case:** Maximum flow, bipartite matching, min cut.

```cpp
#include <bits/stdc++.h>
using namespace std;
struct Edge { int to, rev, cap; };
vector<Edge> graph[10005];
int level[10005], iter_[10005];

void addEdge(int from, int to, int cap) {
    graph[from].push_back({to, (int)graph[to].size(), cap});
    graph[to].push_back({from, (int)graph[from].size()-1, 0});
}
bool bfs(int s, int t, int n) {
    fill(level, level+n, -1);
    queue<int> q; level[s] = 0; q.push(s);
    while (!q.empty()) {
        int v = q.front(); q.pop();
        for (auto& e : graph[v])
            if (e.cap > 0 && level[e.to] < 0)
                { level[e.to] = level[v]+1; q.push(e.to); }
    }
    return level[t] >= 0;
}
int dfs(int v, int t, int f) {
    if (v == t) return f;
    for (int& i = iter_[v]; i < (int)graph[v].size(); i++) {
        Edge& e = graph[v][i];
        if (e.cap > 0 && level[v] < level[e.to]) {
            int d = dfs(e.to, t, min(f, e.cap));
            if (d > 0) { e.cap -= d; graph[e.to][e.rev].cap += d; return d; }
        }
    }
    return 0;
}
```

**Sample Output:**
```
Source=0, Sink=5
Max flow = 23
BFS builds level graph each phase
DFS sends blocking flow O(VE) per phase
```

---

### 4.5 Centroid Decomposition
**Complexity:** O(n log² n) for path queries

Recursively finds the centroid of a tree, enabling divide-and-conquer on tree paths.

**Use case:** Count pairs of nodes with path length ≤ K.

```cpp
#include <bits/stdc++.h>
using namespace std;
vector<pair<int,int>> adj[100005];
int subtree[100005];
bool removed[100005];

int getSubtree(int u, int p) {
    subtree[u] = 1;
    for (auto [v, w] : adj[u])
        if (v != p && !removed[v])
            subtree[u] += getSubtree(v, u);
    return subtree[u];
}

int getCentroid(int u, int p, int treeSize) {
    for (auto [v, w] : adj[u])
        if (v != p && !removed[v] && subtree[v] > treeSize/2)
            return getCentroid(v, u, treeSize);
    return u;
}

void decompose(int u, int p) {
    int sz = getSubtree(u, p);
    int c = getCentroid(u, p, sz);
    removed[c] = true;
    // process centroid c here
    for (auto [v, w] : adj[c])
        if (!removed[v]) decompose(v, c);
}
```

**Sample Output:**
```
Tree with 7 nodes
Centroid at root: node 4 (splits into subtrees ≤ 3)
All paths pass through some centroid
Recursion depth = O(log n)
```

---

## 5. 🔢 Number Theory & Math

### 5.1 Matrix Exponentiation
**Complexity:** O(k³ log n)

Represent linear recurrences as matrix multiplication and use fast exponentiation.

**Use case:** nth Fibonacci in O(log n).

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef vector<vector<long long>> Mat;
const long long MOD = 1e9+7;

Mat multiply(const Mat& A, const Mat& B) {
    int n = A.size();
    Mat C(n, vector<long long>(n, 0));
    for (int i = 0; i < n; i++)
        for (int k = 0; k < n; k++)
            if (A[i][k]) for (int j = 0; j < n; j++)
                C[i][j] = (C[i][j] + A[i][k]*B[k][j]) % MOD;
    return C;
}

Mat matpow(Mat A, long long p) {
    int n = A.size();
    Mat res(n, vector<long long>(n, 0));
    for (int i = 0; i < n; i++) res[i][i] = 1;
    for (; p; p >>= 1) {
        if (p & 1) res = multiply(res, A);
        A = multiply(A, A);
    }
    return res;
}
// Fib(n): A = [[1,1],[1,0]], ans = matpow(A,n)[0][1]
```

**Sample Output:**
```
F(1)=1, F(5)=5, F(10)=55
F(10^18) computed in ~180 matrix ops
```

---

### 5.2 Miller-Rabin Primality Test
**Complexity:** O(k log² n)

Deterministic for n < 3.3×10²⁴ using fixed witness set. Uses `__int128` to avoid overflow.

**Use case:** Test if numbers up to 10^18 are prime.

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef unsigned long long ull;
typedef __int128 lll;

ull mulmod(ull a, ull b, ull m) { return (lll)a * b % m; }
ull powmod(ull a, ull b, ull m) {
    ull res = 1; a %= m;
    for (; b; b >>= 1) {
        if (b & 1) res = mulmod(res, a, m);
        a = mulmod(a, a, m);
    }
    return res;
}
bool millerTest(ull n, ull a) {
    if (n % a == 0) return n == a;
    ull d = n-1; int r = 0;
    while (d % 2 == 0) { d /= 2; r++; }
    ull x = powmod(a, d, n);
    if (x == 1 || x == n-1) return true;
    for (int i = 0; i < r-1; i++) {
        x = mulmod(x, x, n);
        if (x == n-1) return true;
    }
    return false;
}
bool isPrime(ull n) {
    for (ull a : {2,3,5,7,11,13,17,19,23,29,31,37})
        if (!millerTest(n, a)) return false;
    return true;
}
```

**Sample Output:**
```
isPrime(997)        = true
isPrime(1000000007) = true
isPrime(998244353)  = true
isPrime(1000000008) = false
```

---

### 5.3 NTT (Number Theoretic Transform)
**Complexity:** O(n log n)

FFT over modular arithmetic for exact polynomial multiplication.

**Use case:** Multiply large polynomials modulo a prime.

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const ll MOD = 998244353, g = 3;

ll pw(ll a, ll b, ll mod) {
    ll res = 1; a %= mod;
    for (; b; b >>= 1) { if (b&1) res=res*a%mod; a=a*a%mod; }
    return res;
}

void ntt(vector<ll>& a, bool inv) {
    int n = a.size();
    for (int i=1,j=0; i<n; i++) {
        int bit = n>>1;
        for (; j&bit; bit>>=1) j^=bit;
        j^=bit; if (i<j) swap(a[i],a[j]);
    }
    for (int len=2; len<=n; len<<=1) {
        ll w = inv ? pw(g, MOD-1-(MOD-1)/len, MOD)
                   : pw(g, (MOD-1)/len, MOD);
        for (int i=0; i<n; i+=len) {
            ll wn = 1;
            for (int j=0; j<len/2; j++, wn=wn*w%MOD) {
                ll u=a[i+j], v=a[i+j+len/2]*wn%MOD;
                a[i+j]=(u+v)%MOD;
                a[i+j+len/2]=(u-v+MOD)%MOD;
            }
        }
    }
    if (inv) { ll ni=pw(n,MOD-2,MOD); for (auto& x:a) x=x*ni%MOD; }
}
```

**Sample Output:**
```
A = [1, 2, 3]  →  1 + 2x + 3x²
B = [4, 5, 6]  →  4 + 5x + 6x²
A×B = [4, 13, 28, 27, 18]
Exact result mod 998244353, no float error
```

---

## 6. 🔣 Bit Manipulation

### 6.1 XOR Tricks
**Complexity:** O(n)

XOR properties: `a^a=0`, `a^0=a`. Exploited to cancel pairs and isolate unique elements.

**Use case:** Find single non-duplicate in array; find two missing numbers.

```cpp
#include <bits/stdc++.h>
using namespace std;

// Find single element (all others appear twice)
int singleNumber(vector<int>& nums) {
    int xorAll = 0;
    for (int x : nums) xorAll ^= x;
    return xorAll;
}

// Find two non-duplicate elements
pair<int,int> twoSingle(vector<int>& nums) {
    int xorBoth = 0;
    for (int x : nums) xorBoth ^= x;
    int bit = xorBoth & (-xorBoth); // lowest set bit
    int a = 0, b = 0;
    for (int x : nums)
        (x & bit) ? a ^= x : b ^= x;
    return {a, b};
}

// Essential bit tricks:
// x & (x-1)              → clear lowest set bit
// x & (-x)               → isolate lowest set bit
// __builtin_popcount(x)  → count set bits
// __builtin_clz(x)       → count leading zeros
```

**Sample Output:**
```
singleNumber([4,1,2,1,2]) = 4
twoSingle([1,2,3,4,1,3])  = {2, 4}
x=12(1100): x&(x-1)=8(1000)
x=12(1100): x&(-x) =4(0100)
```

---

### 6.2 Policy-Based DST (PBDS Ordered Set)
**Complexity:** O(log n) per operation

GNU C++ extension: an ordered set supporting O(log n) `order_of_key` (rank) and `find_by_order` (k-th element).

**Use case:** Count elements less than x, k-th smallest element.

```cpp
#include <bits/stdc++.h>
#include <ext/pb_ds/assoc_container.hpp>
#include <ext/pb_ds/tree_policy.hpp>
using namespace std;
using namespace __gnu_pbds;

typedef tree
    int, null_type, less<int>,
    rb_tree_tag,
    tree_order_statistics_node_update
> ordered_set;

int main() {
    ordered_set os;
    os.insert(5); os.insert(2);
    os.insert(8); os.insert(1); os.insert(9);

    cout << *os.find_by_order(2) << "\n"; // 5 (3rd smallest)
    cout << os.order_of_key(6)   << "\n"; // 3 (elements < 6)
}
```

**Sample Output:**
```
os = {1, 2, 5, 8, 9}
find_by_order(0) = 1
find_by_order(2) = 5
order_of_key(6)  = 3  (elements < 6: {1,2,5})
order_of_key(1)  = 0
```

---

## 7. 🔍 Search & Optimization

### 7.1 Binary Search on Answer
**Complexity:** O(log(range) × check)

Binary search on the answer value when the feasibility predicate is monotone.

**Use case:** Minimum days to complete K tasks with given worker speeds.

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

bool canDo(vector<int>& speed, ll k, ll days) {
    ll total = 0;
    for (int s : speed) total += days * s;
    return total >= k;
}

ll minDays(vector<int>& speed, ll k) {
    ll lo = 1, hi = 1e14, ans = hi;
    while (lo <= hi) {
        ll mid = (lo + hi) / 2;
        if (canDo(speed, k, mid)) {
            ans = mid;
            hi = mid - 1;
        } else {
            lo = mid + 1;
        }
    }
    return ans;
}
```

**Sample Output:**
```
speed=[1,2,3], k=10
mid=2: total=2+4+6=12 ≥ 10 ✓ → try fewer
mid=1: total=1+2+3=6  < 10 ✗ → need more
answer = 2 days
```

---

### 7.2 Meet in the Middle
**Complexity:** O(2^(n/2) × log)

Split problem in two halves, enumerate all 2^(n/2) possibilities for each, combine with binary search.

**Use case:** Subset sum with n ≤ 40 (too large for full 2^40 brute force).

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

int countSubsetSum(vector<int>& a, ll target) {
    int n = a.size(), half = n/2;
    vector<ll> left, right;
    for (int mask = 0; mask < (1<<half); mask++) {
        ll sum = 0;
        for (int i = 0; i < half; i++)
            if (mask>>i&1) sum += a[i];
        left.push_back(sum);
    }
    for (int mask = 0; mask < (1<<(n-half)); mask++) {
        ll sum = 0;
        for (int i = 0; i < n-half; i++)
            if (mask>>i&1) sum += a[half+i];
        right.push_back(sum);
    }
    sort(right.begin(), right.end());
    int count = 0;
    for (ll s : left) {
        ll need = target - s;
        count += upper_bound(right.begin(), right.end(), need)
               - lower_bound(right.begin(), right.end(), need);
    }
    return count;
}
```

**Sample Output:**
```
a=[3,34,4,12,5,2], target=9
Left sums:  16 values from first half
Right sums: 8 values from second half
Pairs summing to 9: count = 2
n=40 → 2^20 ≈ 10^6 each half, feasible!
```

---

### 7.3 Ternary Search
**Complexity:** O(log₃(range) × eval)

Find the minimum or maximum of a unimodal function on a continuous or discrete domain.

**Use case:** Minimize a convex function f(x) over a real interval.

```cpp
#include <bits/stdc++.h>
using namespace std;

// f must be unimodal (strictly convex or concave)
double ternarySearch(double lo, double hi) {
    auto f = [](double x) { return (x-3)*(x-3) + 2; };
    for (int iter = 0; iter < 200; iter++) {
        double m1 = lo + (hi-lo)/3;
        double m2 = hi - (hi-lo)/3;
        if (f(m1) < f(m2)) hi = m2;
        else lo = m1;
    }
    return (lo + hi) / 2;
}

// Discrete ternary search on integers:
int discreteTernary(int lo, int hi) {
    auto f = [](int x) { return abs(x-7) + abs(x-3); };
    while (hi - lo > 2) {
        int m1 = lo + (hi-lo)/3;
        int m2 = hi - (hi-lo)/3;
        if (f(m1) <= f(m2)) hi = m2;
        else lo = m1;
    }
    int best = lo;
    for (int x = lo; x <= hi; x++)
        if (f(x) < f(best)) best = x;
    return best;
}
```

**Sample Output:**
```
f(x) = (x-3)² + 2
Minimum at x ≈ 3.0000, f(3) = 2
Discrete: f(x) = |x-7|+|x-3|, minimum at x=5
```

---

## 8. ⚡ Miscellaneous & C++ Specific

### 8.1 Fast I/O + GCC Pragmas
**Complexity:** Constant factor speedup

Critical micro-optimizations: disable sync with C stdio and add GCC vectorization pragmas.

**Use case:** Avoid TLE on problems with large input/output.

```cpp
#pragma GCC optimize("O2,unroll-loops")
#pragma GCC target("avx2,bmi,bmi2,popcnt")
#include <bits/stdc++.h>
using namespace std;

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    // your solution here
}
```

---

### 8.2 Custom Hash for `unordered_map`
**Complexity:** O(1) average, prevents worst-case O(n)

Default hash is vulnerable to anti-hash hacks. Custom hash using `splitmix64` prevents this.

**Use case:** Safe hash map in competitive programming.

```cpp
#include <bits/stdc++.h>
using namespace std;

struct custom_hash {
    static uint64_t splitmix64(uint64_t x) {
        x += 0x9e3779b97f4a7c15;
        x = (x ^ (x >> 30)) * 0xbf58476d1ce4e5b9;
        x = (x ^ (x >> 27)) * 0x94d049bb133111eb;
        return x ^ (x >> 31);
    }
    size_t operator()(uint64_t x) const {
        static const uint64_t FIXED_RANDOM =
            chrono::steady_clock::now().time_since_epoch().count();
        return splitmix64(x + FIXED_RANDOM);
    }
};

unordered_map<long long, int, custom_hash> safeMap;
```

**Sample Output:**
```
Default unordered_map: O(n) worst case with crafted input
Custom hash: randomized seed → no deterministic worst case
Useful in Codeforces Div. 1 problems with large maps
```

---

### 8.3 `__int128` & Coordinate Compression
**Complexity:** O(n log n) for compression

`__int128` handles values up to ~1.7×10³⁸. Coordinate compression maps large sparse values to small dense indices.

**Use case:** Overflow-safe multiplication; compress 10⁹-scale values to array indices.

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef __int128 lll;

// __int128 multiplication without overflow
lll bigMul(lll a, lll b) { return a * b; }

// Coordinate compression
vector<int> compress(vector<int>& arr) {
    vector<int> sorted = arr;
    sort(sorted.begin(), sorted.end());
    sorted.erase(unique(sorted.begin(), sorted.end()), sorted.end());
    vector<int> comp(arr.size());
    for (int i = 0; i < (int)arr.size(); i++)
        comp[i] = lower_bound(sorted.begin(), sorted.end(), arr[i])
                - sorted.begin();
    return comp;
}
```

**Sample Output:**
```
__int128 max ≈ 1.7 × 10^38
bigMul(10^18, 10^18) = 10^36  (no overflow)

arr        = [100, 500, 200, 100, 700]
sorted     = [100, 200, 500, 700]
compressed = [0, 2, 1, 0, 3]
Now safe as segment tree indices
```

---

## 📊 Complexity Cheat Sheet

| Technique | Time | Space |
|---|---|---|
| Segment Tree | O(log n) per op | O(n) |
| BIT (Fenwick) | O(log n) per op | O(n) |
| Sparse Table | O(1) query, O(n log n) build | O(n log n) |
| Mo's Algorithm | O((N+Q)√N) | O(n) |
| Bitmask DP | O(2ⁿ × n) | O(2ⁿ × n) |
| Digit DP | O(digits × states) | O(digits × states) |
| SOS DP | O(n × 2ⁿ) | O(2ⁿ) |
| KMP | O(n + m) | O(m) |
| Z-Algorithm | O(n) | O(n) |
| Suffix Array | O(n log n) | O(n) |
| Aho-Corasick | O(Σ|patterns| + n) | O(Σ|patterns|) |
| Dijkstra | O((V+E) log V) | O(V+E) |
| Tarjan SCC | O(V+E) | O(V+E) |
| LCA Binary Lifting | O(n log n) build, O(log n) query | O(n log n) |
| Dinic Max Flow | O(V²E) | O(V+E) |
| Centroid Decomp | O(n log² n) | O(n log n) |
| Matrix Expo | O(k³ log n) | O(k²) |
| Miller-Rabin | O(k log² n) | O(1) |
| NTT | O(n log n) | O(n) |
| Binary Search on Ans | O(log(range) × check) | O(1) |
| Meet in Middle | O(2^(n/2) × log) | O(2^(n/2)) |
| Ternary Search | O(log(range)) | O(1) |

---

> **Learning roadmap:** Data Structures → DP → Graph → Strings → Math → Bit tricks → C++ specifics. Master each layer before moving on for solid Codeforces Div. 2 → Div. 1 progression.
