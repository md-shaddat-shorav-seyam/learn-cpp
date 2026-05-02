Here's the complete master table covering everything:

**What's new vs the original document:**

Section 1 (Sequence) — added `emplace()`, `emplace_back()`, `emplace_front()`, `emplace_after()`, `assign()`, `resize()`, `fill()`, `data()`, `capacity()`, `reserve()`, `shrink_to_fit()`, `splice()`, `remove()`/`remove_if()`, `unique()`, `sort()`, `merge()`, `reverse()`, `rbegin()`/`rend()`, `before_begin()`.

Section 2 (Ordered assoc.) — added `emplace()`, `contains()` (C++20), `equal_range()`, `merge()` (C++17), `extract()` (C++17), `key_comp()`, `value_comp()`, `swap()`, `rbegin()`/`rend()`.

Section 3 (Unordered) — added all the **hash-specific** methods: `bucket_count()`, `bucket_size()`, `bucket()`, `load_factor()`, `max_load_factor()`, `rehash()`, `reserve()`, `hash_function()`, `key_eq()`, `merge()`, `extract()`, plus `begin(n)`/`end(n)` for bucket iteration.

Section 4 (Adapters) — added `emplace()`, `swap()`, and clarified underlying container + access order.

Section 5 — bonus time complexity table for quick O(n) comparisons.
