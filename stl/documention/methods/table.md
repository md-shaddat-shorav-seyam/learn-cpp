
<style>
* { box-sizing: border-box; margin: 0; padding: 0; }
body { padding: 0; }
.wrap { padding: 12px 0 24px; font-size: 13px; color: var(--color-text-primary); }
h2 { font-size: 15px; font-weight: 500; margin: 20px 0 8px; color: var(--color-text-primary); }
h2:first-child { margin-top: 4px; }
.sub { font-size: 12px; color: var(--color-text-secondary); margin-bottom: 8px; }
table { width: 100%; border-collapse: collapse; font-size: 12px; }
th {
  background: var(--color-background-secondary);
  color: var(--color-text-secondary);
  font-weight: 500;
  padding: 6px 8px;
  text-align: left;
  border-bottom: 1px solid var(--color-border-secondary);
  white-space: nowrap;
}
th:first-child { width: 155px; }
td {
  padding: 5px 8px;
  border-bottom: 1px solid var(--color-border-tertiary);
  text-align: left;
  vertical-align: middle;
  white-space: nowrap;
}
tr:last-child td { border-bottom: none; }
.method { font-family: var(--font-mono); font-size: 11.5px; color: var(--color-text-primary); }
.yes { color: #1a9b5c; font-size: 14px; }
.no  { color: #cc3a3a; font-size: 14px; }
.na  { font-size: 11px; color: var(--color-text-tertiary); }
.note { font-size: 10.5px; color: var(--color-text-tertiary); font-style: italic; }
.iter { font-size: 11px; color: var(--color-text-secondary); }
.section-gap { height: 28px; }
.legend { display: flex; gap: 16px; font-size: 12px; color: var(--color-text-secondary); margin-bottom: 16px; align-items: center; }
.legend span { display: flex; align-items: center; gap: 4px; }
</style>
<div class="wrap">
<div class="legend">
  <span><span class="yes">✓</span> supported</span>
  <span><span class="no">✗</span> not supported</span>
  <span><span class="na">—</span> not applicable / use alternative</span>
</div>

<h2>1 — Sequence containers</h2>
<table>
<tr>
  <th>Method / Feature</th>
  <th>vector</th><th>deque</th><th>list</th><th>forward_list</th><th>array</th>
</tr>
<tr><td class="method">push_back()</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="no">✗</td><td class="no">✗</td></tr>
<tr><td class="method">push_front()</td><td class="no">✗</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="no">✗</td></tr>
<tr><td class="method">pop_back()</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="no">✗</td><td class="no">✗</td></tr>
<tr><td class="method">pop_front()</td><td class="no">✗</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="no">✗</td></tr>
<tr><td class="method">insert(it, val)</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="na">— <span class="note">insert_after()</span></td><td class="no">✗</td></tr>
<tr><td class="method">insert_after()</td><td class="no">✗</td><td class="no">✗</td><td class="no">✗</td><td class="yes">✓</td><td class="no">✗</td></tr>
<tr><td class="method">emplace()</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="na">— <span class="note">emplace_after()</span></td><td class="no">✗</td></tr>
<tr><td class="method">emplace_back()</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="no">✗</td><td class="no">✗</td></tr>
<tr><td class="method">emplace_front()</td><td class="no">✗</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="no">✗</td></tr>
<tr><td class="method">emplace_after()</td><td class="no">✗</td><td class="no">✗</td><td class="no">✗</td><td class="yes">✓</td><td class="no">✗</td></tr>
<tr><td class="method">erase(it)</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="na">— <span class="note">erase_after()</span></td><td class="no">✗</td></tr>
<tr><td class="method">erase_after()</td><td class="no">✗</td><td class="no">✗</td><td class="no">✗</td><td class="yes">✓</td><td class="no">✗</td></tr>
<tr><td class="method">operator[]</td><td class="yes">✓</td><td class="yes">✓</td><td class="no">✗</td><td class="no">✗</td><td class="yes">✓</td></tr>
<tr><td class="method">at()</td><td class="yes">✓</td><td class="yes">✓</td><td class="no">✗</td><td class="no">✗</td><td class="yes">✓</td></tr>
<tr><td class="method">front()</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="method">back()</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="no">✗</td><td class="yes">✓</td></tr>
<tr><td class="method">size()</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="no">✗</td><td class="yes">✓</td></tr>
<tr><td class="method">max_size()</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="method">empty()</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="method">clear()</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="no">✗</td></tr>
<tr><td class="method">resize()</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="no">✗</td></tr>
<tr><td class="method">assign()</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="no">✗</td></tr>
<tr><td class="method">swap()</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="method">fill() <span class="note">(value)</span></td><td class="no">✗</td><td class="no">✗</td><td class="no">✗</td><td class="no">✗</td><td class="yes">✓</td></tr>
<tr><td class="method">data()</td><td class="yes">✓</td><td class="no">✗</td><td class="no">✗</td><td class="no">✗</td><td class="yes">✓</td></tr>
<tr><td class="method">capacity()</td><td class="yes">✓</td><td class="no">✗</td><td class="no">✗</td><td class="no">✗</td><td class="no">✗</td></tr>
<tr><td class="method">reserve()</td><td class="yes">✓</td><td class="no">✗</td><td class="no">✗</td><td class="no">✗</td><td class="no">✗</td></tr>
<tr><td class="method">shrink_to_fit()</td><td class="yes">✓</td><td class="yes">✓</td><td class="no">✗</td><td class="no">✗</td><td class="no">✗</td></tr>
<tr><td class="method">splice()</td><td class="no">✗</td><td class="no">✗</td><td class="yes">✓</td><td class="yes">✓</td><td class="no">✗</td></tr>
<tr><td class="method">remove() / remove_if()</td><td class="no">✗</td><td class="no">✗</td><td class="yes">✓</td><td class="yes">✓</td><td class="no">✗</td></tr>
<tr><td class="method">unique()</td><td class="no">✗</td><td class="no">✗</td><td class="yes">✓</td><td class="yes">✓</td><td class="no">✗</td></tr>
<tr><td class="method">sort()</td><td class="no">✗</td><td class="no">✗</td><td class="yes">✓</td><td class="yes">✓</td><td class="no">✗</td></tr>
<tr><td class="method">merge()</td><td class="no">✗</td><td class="no">✗</td><td class="yes">✓</td><td class="yes">✓</td><td class="no">✗</td></tr>
<tr><td class="method">reverse()</td><td class="no">✗</td><td class="no">✗</td><td class="yes">✓</td><td class="yes">✓</td><td class="no">✗</td></tr>
<tr><td class="method">begin() / end()</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="method">rbegin() / rend()</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="no">✗</td><td class="yes">✓</td></tr>
<tr><td class="method">before_begin()</td><td class="no">✗</td><td class="no">✗</td><td class="no">✗</td><td class="yes">✓</td><td class="no">✗</td></tr>
<tr><td class="iter">Iterator type</td><td class="iter">Random</td><td class="iter">Random</td><td class="iter">Bidirectional</td><td class="iter">Forward</td><td class="iter">Random</td></tr>
</table>

<h2>2 — Associative containers (ordered, red-black tree)</h2>
<table>
<tr>
  <th>Method / Feature</th>
  <th>set</th><th>multiset</th><th>map</th><th>multimap</th>
</tr>
<tr><td class="method">insert()</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="method">emplace()</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="method">erase(key / it)</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="method">find()</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="method">count()</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="method">contains() <span class="note">(C++20)</span></td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="method">lower_bound()</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="method">upper_bound()</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="method">equal_range()</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="method">operator[]</td><td class="no">✗</td><td class="no">✗</td><td class="yes">✓</td><td class="no">✗</td></tr>
<tr><td class="method">at()</td><td class="no">✗</td><td class="no">✗</td><td class="yes">✓</td><td class="no">✗</td></tr>
<tr><td class="method">size()</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="method">empty()</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="method">clear()</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="method">swap()</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="method">merge() <span class="note">(C++17)</span></td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="method">extract() <span class="note">(C++17)</span></td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="method">key_comp()</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="method">value_comp()</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="method">push_back() / push_front()</td><td class="no">✗</td><td class="no">✗</td><td class="no">✗</td><td class="no">✗</td></tr>
<tr><td class="method">front() / back()</td><td class="no">✗</td><td class="no">✗</td><td class="no">✗</td><td class="no">✗</td></tr>
<tr><td class="method">begin() / end()</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="method">rbegin() / rend()</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="iter">Iterator type</td><td class="iter">Bidirectional</td><td class="iter">Bidirectional</td><td class="iter">Bidirectional</td><td class="iter">Bidirectional</td></tr>
<tr><td class="iter">Ordering</td><td class="iter">sorted, unique</td><td class="iter">sorted, dupes ok</td><td class="iter">sorted by key</td><td class="iter">sorted, dupes ok</td></tr>
</table>

<h2>3 — Unordered containers (hash table)</h2>
<table>
<tr>
  <th>Method / Feature</th>
  <th>unordered_set</th><th>unordered_multiset</th><th>unordered_map</th><th>unordered_multimap</th>
</tr>
<tr><td class="method">insert()</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="method">emplace()</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="method">erase(key / it)</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="method">find()</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="method">count()</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="method">contains() <span class="note">(C++20)</span></td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="method">equal_range()</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="method">operator[]</td><td class="no">✗</td><td class="no">✗</td><td class="yes">✓</td><td class="no">✗</td></tr>
<tr><td class="method">at()</td><td class="no">✗</td><td class="no">✗</td><td class="yes">✓</td><td class="no">✗</td></tr>
<tr><td class="method">lower_bound()</td><td class="no">✗</td><td class="no">✗</td><td class="no">✗</td><td class="no">✗</td></tr>
<tr><td class="method">upper_bound()</td><td class="no">✗</td><td class="no">✗</td><td class="no">✗</td><td class="no">✗</td></tr>
<tr><td class="method">size()</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="method">empty()</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="method">clear()</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="method">swap()</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="method">merge() <span class="note">(C++17)</span></td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="method">extract() <span class="note">(C++17)</span></td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="method">bucket_count()</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="method">bucket_size(n)</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="method">bucket(key)</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="method">load_factor()</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="method">max_load_factor()</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="method">rehash(n)</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="method">reserve(n)</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="method">hash_function()</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="method">key_eq()</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="method">push_back() / push_front()</td><td class="no">✗</td><td class="no">✗</td><td class="no">✗</td><td class="no">✗</td></tr>
<tr><td class="method">front() / back()</td><td class="no">✗</td><td class="no">✗</td><td class="no">✗</td><td class="no">✗</td></tr>
<tr><td class="method">begin() / end()</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="method">begin(n) / end(n) <span class="note">(bucket)</span></td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="iter">Iterator type</td><td class="iter">Forward</td><td class="iter">Forward</td><td class="iter">Forward</td><td class="iter">Forward</td></tr>
<tr><td class="iter">Ordering</td><td class="iter">unordered, unique</td><td class="iter">unordered, dupes ok</td><td class="iter">unordered by key</td><td class="iter">unordered, dupes ok</td></tr>
</table>

<h2>4 — Container adapters</h2>
<p class="sub">No iterators, no begin()/end() — restricted interface by design.</p>
<table>
<tr>
  <th>Method / Feature</th>
  <th>stack</th><th>queue</th><th>priority_queue</th>
</tr>
<tr><td class="method">push()</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="method">emplace()</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="method">pop()</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="method">top()</td><td class="yes">✓</td><td class="no">✗</td><td class="yes">✓</td></tr>
<tr><td class="method">front()</td><td class="no">✗</td><td class="yes">✓</td><td class="no">✗</td></tr>
<tr><td class="method">back()</td><td class="no">✗</td><td class="yes">✓</td><td class="no">✗</td></tr>
<tr><td class="method">size()</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="method">empty()</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="method">swap()</td><td class="yes">✓</td><td class="yes">✓</td><td class="yes">✓</td></tr>
<tr><td class="method">insert() / erase()</td><td class="no">✗</td><td class="no">✗</td><td class="no">✗</td></tr>
<tr><td class="method">operator[] / at()</td><td class="no">✗</td><td class="no">✗</td><td class="no">✗</td></tr>
<tr><td class="method">begin() / end()</td><td class="no">✗</td><td class="no">✗</td><td class="no">✗</td></tr>
<tr><td class="iter">Default underlying</td><td class="iter">deque</td><td class="iter">deque</td><td class="iter">vector</td></tr>
<tr><td class="iter">Access order</td><td class="iter">LIFO (top)</td><td class="iter">FIFO (front)</td><td class="iter">max by default</td></tr>
</table>

<h2>5 — Time complexity reference</h2>
<table>
<tr>
  <th>Operation</th>
  <th>vector</th><th>deque</th><th>list / fwdlist</th><th>set / map</th><th>unordered_*</th>
</tr>
<tr><td class="method">Access by index</td><td>O(1)</td><td>O(1)</td><td class="no">—</td><td class="no">—</td><td class="no">—</td></tr>
<tr><td class="method">push_back / push</td><td>O(1) amort.</td><td>O(1)</td><td>O(1)</td><td class="no">—</td><td class="no">—</td></tr>
<tr><td class="method">push_front</td><td class="no">—</td><td>O(1)</td><td>O(1)</td><td class="no">—</td><td class="no">—</td></tr>
<tr><td class="method">insert (middle)</td><td>O(n)</td><td>O(n)</td><td>O(1) with iter</td><td>O(log n)</td><td>O(1) avg</td></tr>
<tr><td class="method">erase (middle)</td><td>O(n)</td><td>O(n)</td><td>O(1) with iter</td><td>O(log n)</td><td>O(1) avg</td></tr>
<tr><td class="method">find / count</td><td>O(n)</td><td>O(n)</td><td>O(n)</td><td>O(log n)</td><td>O(1) avg</td></tr>
<tr><td class="method">lower_bound</td><td>O(log n)*</td><td>O(log n)*</td><td>O(n)</td><td>O(log n)</td><td class="no">✗</td></tr>
<tr><td class="method">sort</td><td>O(n log n)</td><td>O(n log n)</td><td>O(n log n)</td><td>always sorted</td><td>not sorted</td></tr>
</table>
<p class="sub" style="margin-top:6px">* std::lower_bound works on sorted vector/deque with random iterators — O(log n) comparisons, but O(n) moves for non-random containers.</p>

</div>
