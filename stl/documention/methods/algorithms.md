
<style>
h2.sr-only{position:absolute;width:1px;height:1px;padding:0;margin:-1px;overflow:hidden;clip:rect(0,0,0,0);border:0}
*{box-sizing:border-box;margin:0;padding:0}
body{font-family:var(--font-sans);color:var(--color-text-primary)}
.wrap{padding:1rem 0}
.tabs{display:flex;flex-wrap:wrap;gap:6px;margin-bottom:1.5rem}
.tab{padding:5px 14px;border-radius:20px;border:0.5px solid var(--color-border-secondary);background:transparent;cursor:pointer;font-size:13px;color:var(--color-text-secondary);transition:all .15s}
.tab.active{background:var(--color-background-info);color:var(--color-text-info);border-color:var(--color-border-info)}
.tab:hover:not(.active){background:var(--color-background-secondary)}
.grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(300px,1fr));gap:12px}
.card{background:var(--color-background-primary);border:0.5px solid var(--color-border-tertiary);border-radius:var(--border-radius-lg);padding:14px 16px;display:flex;flex-direction:column;gap:8px}
.fn-name{font-family:var(--font-mono);font-size:14px;font-weight:500;color:var(--color-text-info)}
.fn-desc{font-size:13px;color:var(--color-text-secondary);line-height:1.5}
.code-block{background:var(--color-background-tertiary);border-radius:var(--border-radius-md);padding:10px 12px;font-family:var(--font-mono);font-size:12px;line-height:1.7;color:var(--color-text-primary);white-space:pre;overflow-x:auto}
.output{font-family:var(--font-mono);font-size:12px;color:var(--color-text-success);background:var(--color-background-success);border-radius:var(--border-radius-md);padding:6px 10px;margin-top:2px}
.badge{display:inline-block;font-size:11px;padding:2px 8px;border-radius:12px;font-weight:500;margin-bottom:2px}
.badge-sort{background:#E6F1FB;color:#0C447C}
.badge-search{background:#E1F5EE;color:#085041}
.badge-count{background:#FAEEDA;color:#633806}
.badge-mod{background:#FBEAF0;color:#72243E}
.badge-perm{background:#EEEDFE;color:#3C3489}
.badge-minmax{background:#EAF3DE;color:#27500A}
.badge-set{background:#FAECE7;color:#712B13}
.badge-heap{background:#F1EFE8;color:#444441}
.badge-num{background:#FCEBEB;color:#791F1F}
.hidden{display:none}
</style>
<h2 class="sr-only">STL algorithm library reference with examples for every function, organized by category</h2>
<div class="wrap">
<div class="tabs" id="tabs"></div>
<div class="grid" id="grid"></div>
</div>
<script>
const cats=[
  {id:"all",label:"All"},
  {id:"sort",label:"Sorting"},
  {id:"search",label:"Searching"},
  {id:"count",label:"Counting"},
  {id:"mod",label:"Modifying"},
  {id:"perm",label:"Permutations"},
  {id:"minmax",label:"Min / Max"},
  {id:"set",label:"Set ops"},
  {id:"heap",label:"Heap"},
  {id:"num",label:"Numeric"},
];

const fns=[
  {cat:"sort",name:"std::sort",desc:"Sorts elements in ascending order (or custom comparator).",
   code:`vector<int> v{5,2,8,1,9,3};\nsort(v.begin(), v.end());\n// v → {1,2,3,5,8,9}`,out:"→ 1 2 3 5 8 9"},

  {cat:"sort",name:"std::stable_sort",desc:"Like sort but preserves relative order of equal elements.",
   code:`sort by last name, stable_sort by age\n// equal ages keep original order`,out:"→ order preserved"},

  {cat:"sort",name:"std::partial_sort",desc:"Sorts only the first N elements.",
   code:`vector<int> v{5,2,8,1,9,3};\npartial_sort(v.begin(),v.begin()+3,v.end());\n// v → {1,2,3,9,8,5}`,out:"→ 1 2 3 | rest unspecified"},

  {cat:"sort",name:"std::nth_element",desc:"Rearranges so that nth position holds the element it would have if sorted.",
   code:`vector<int> v{5,2,8,1,9,3};\nnth_element(v.begin(),v.begin()+2,v.end());\n// v[2] == 3 (3rd smallest)`,out:"→ v[2] = 3"},

  {cat:"sort",name:"std::is_sorted",desc:"Returns true if range is sorted.",
   code:`vector<int> v{1,2,3,4};\nbool ok = is_sorted(v.begin(), v.end());\n// ok == true`,out:"→ true"},

  {cat:"sort",name:"std::is_sorted_until",desc:"Returns iterator to first unsorted element.",
   code:`vector<int> v{1,2,5,3,4};\nauto it = is_sorted_until(v.begin(),v.end());\n// it points to 3`,out:"→ iterator to 3"},

  {cat:"search",name:"std::find",desc:"Finds first occurrence of a value.",
   code:`vector<int> v{1,2,3,4,5};\nauto it = find(v.begin(), v.end(), 3);\n// *it == 3`,out:"→ iterator to 3"},

  {cat:"search",name:"std::find_if",desc:"Finds first element satisfying predicate.",
   code:`auto it = find_if(v.begin(), v.end(),\n  [](int x){ return x > 3; });\n// *it == 4`,out:"→ iterator to 4"},

  {cat:"search",name:"std::find_if_not",desc:"Finds first element NOT satisfying predicate.",
   code:`auto it = find_if_not(v.begin(), v.end(),\n  [](int x){ return x < 4; });\n// *it == 4`,out:"→ iterator to 4"},

  {cat:"search",name:"std::binary_search",desc:"Returns true if value exists in sorted range.",
   code:`vector<int> v{1,2,3,4,5};\nbool found = binary_search(v.begin(),v.end(),3);\n// found == true`,out:"→ true"},

  {cat:"search",name:"std::lower_bound",desc:"Returns iterator to first element >= value (sorted).",
   code:`auto it = lower_bound(v.begin(),v.end(),3);\n// *it == 3`,out:"→ iterator to 3"},

  {cat:"search",name:"std::upper_bound",desc:"Returns iterator to first element > value (sorted).",
   code:`auto it = upper_bound(v.begin(),v.end(),3);\n// *it == 4`,out:"→ iterator to 4"},

  {cat:"search",name:"std::equal_range",desc:"Returns pair of [lower_bound, upper_bound].",
   code:`auto [lo,hi] = equal_range(v.begin(),v.end(),3);\n// range containing all 3s`,out:"→ [lo, hi) = 3"},

  {cat:"search",name:"std::search",desc:"Finds a subsequence inside a range.",
   code:`vector<int> v{1,2,3,4,5}, sub{3,4};\nauto it = search(v.begin(),v.end(),\n  sub.begin(),sub.end());\n// *it == 3`,out:"→ iterator to 3"},

  {cat:"search",name:"std::adjacent_find",desc:"Finds first pair of adjacent equal (or matching) elements.",
   code:`vector<int> v{1,2,2,3,4};\nauto it = adjacent_find(v.begin(),v.end());\n// *it == 2`,out:"→ iterator to first 2"},

  {cat:"count",name:"std::count",desc:"Counts elements equal to a value.",
   code:`vector<int> v{1,2,3,2,1};\nint n = count(v.begin(), v.end(), 2);\n// n == 2`,out:"→ 2"},

  {cat:"count",name:"std::count_if",desc:"Counts elements satisfying a predicate.",
   code:`int n = count_if(v.begin(), v.end(),\n  [](int x){ return x % 2 == 0; });\n// n == 2 (evens: 2,2)`,out:"→ 2"},

  {cat:"mod",name:"std::copy",desc:"Copies elements to another range.",
   code:`vector<int> src{1,2,3}, dst(3);\ncopy(src.begin(),src.end(),dst.begin());\n// dst == {1,2,3}`,out:"→ dst = 1 2 3"},

  {cat:"mod",name:"std::copy_if",desc:"Copies elements satisfying predicate.",
   code:`copy_if(src.begin(),src.end(),\n  back_inserter(dst),\n  [](int x){ return x>1; });\n// dst == {2,3}`,out:"→ dst = 2 3"},

  {cat:"mod",name:"std::transform",desc:"Applies a function to each element, storing result.",
   code:`vector<int> v{1,2,3}, out(3);\ntransform(v.begin(),v.end(),out.begin(),\n  [](int x){ return x*x; });\n// out == {1,4,9}`,out:"→ 1 4 9"},

  {cat:"mod",name:"std::fill",desc:"Assigns a value to every element in a range.",
   code:`vector<int> v(5);\nfill(v.begin(), v.end(), 7);\n// v == {7,7,7,7,7}`,out:"→ 7 7 7 7 7"},

  {cat:"mod",name:"std::fill_n",desc:"Assigns value to first N elements.",
   code:`fill_n(v.begin(), 3, 0);\n// first 3 → {0,0,0,7,7}`,out:"→ 0 0 0 7 7"},

  {cat:"mod",name:"std::replace",desc:"Replaces all occurrences of old_val with new_val.",
   code:`vector<int> v{1,2,3,2,1};\nreplace(v.begin(),v.end(), 2, 99);\n// v == {1,99,3,99,1}`,out:"→ 1 99 3 99 1"},

  {cat:"mod",name:"std::replace_if",desc:"Replaces elements satisfying predicate.",
   code:`replace_if(v.begin(),v.end(),\n  [](int x){return x<3;}, 0);\n// 1,2 → 0`,out:"→ 0 0 3 0 0"},

  {cat:"mod",name:"std::remove",desc:"Logically removes elements equal to value (doesn't resize).",
   code:`vector<int> v{1,2,3,2,1};\nauto end = remove(v.begin(),v.end(),2);\nv.erase(end, v.end());\n// v == {1,3,1}`,out:"→ 1 3 1"},

  {cat:"mod",name:"std::remove_if",desc:"Logically removes elements satisfying predicate.",
   code:`auto end = remove_if(v.begin(),v.end(),\n  [](int x){return x%2==0;});\nv.erase(end,v.end());`,out:"→ removes evens"},

  {cat:"mod",name:"std::unique",desc:"Removes consecutive duplicates.",
   code:`vector<int> v{1,1,2,3,3,3,4};\nauto end = unique(v.begin(),v.end());\nv.erase(end,v.end());\n// v == {1,2,3,4}`,out:"→ 1 2 3 4"},

  {cat:"mod",name:"std::reverse",desc:"Reverses the order of elements in a range.",
   code:`vector<int> v{1,2,3,4,5};\nreverse(v.begin(), v.end());\n// v == {5,4,3,2,1}`,out:"→ 5 4 3 2 1"},

  {cat:"mod",name:"std::rotate",desc:"Rotates elements so that a given iterator becomes the first.",
   code:`vector<int> v{1,2,3,4,5};\nrotate(v.begin(),v.begin()+2,v.end());\n// v == {3,4,5,1,2}`,out:"→ 3 4 5 1 2"},

  {cat:"mod",name:"std::shuffle",desc:"Randomly shuffles elements (needs a random engine).",
   code:`mt19937 rng(42);\nvector<int> v{1,2,3,4,5};\nshuffle(v.begin(),v.end(),rng);`,out:"→ random order"},

  {cat:"mod",name:"std::for_each",desc:"Applies a function to every element (for side effects).",
   code:`vector<int> v{1,2,3};\nfor_each(v.begin(),v.end(),\n  [](int x){ cout << x << ' '; });\n// prints 1 2 3`,out:"→ 1 2 3"},

  {cat:"mod",name:"std::generate",desc:"Fills range using a generator function.",
   code:`int i=0;\nvector<int> v(5);\ngenerate(v.begin(),v.end(),[&]{ return i++; });\n// v == {0,1,2,3,4}`,out:"→ 0 1 2 3 4"},

  {cat:"mod",name:"std::swap_ranges",desc:"Swaps elements of two ranges.",
   code:`vector<int> a{1,2,3}, b{4,5,6};\nswap_ranges(a.begin(),a.end(),b.begin());\n// a=={4,5,6}, b=={1,2,3}`,out:"→ a=4 5 6 b=1 2 3"},

  {cat:"mod",name:"std::merge",desc:"Merges two sorted ranges into one sorted output.",
   code:`vector<int> a{1,3,5}, b{2,4,6}, out;\nmerge(a.begin(),a.end(),\n  b.begin(),b.end(),\n  back_inserter(out));\n// out=={1,2,3,4,5,6}`,out:"→ 1 2 3 4 5 6"},

  {cat:"mod",name:"std::inplace_merge",desc:"Merges two consecutive sorted sub-ranges in place.",
   code:`vector<int> v{1,3,5,2,4,6};\ninplace_merge(v.begin(),v.begin()+3,v.end());\n// v == {1,2,3,4,5,6}`,out:"→ 1 2 3 4 5 6"},

  {cat:"perm",name:"std::next_permutation",desc:"Transforms to next lexicographic permutation; returns false if last.",
   code:`string s = "abc";\nnext_permutation(s.begin(),s.end());\n// s == "acb"`,out:"→ acb"},

  {cat:"perm",name:"std::prev_permutation",desc:"Transforms to previous lexicographic permutation.",
   code:`string s = "bca";\nprev_permutation(s.begin(),s.end());\n// s == "bac"`,out:"→ bac"},

  {cat:"perm",name:"std::is_permutation",desc:"Returns true if one range is a permutation of another.",
   code:`vector<int> a{1,2,3}, b{3,1,2};\nbool ok = is_permutation(a.begin(),a.end(),\n  b.begin());\n// ok == true`,out:"→ true"},

  {cat:"minmax",name:"std::min",desc:"Returns the smaller of two values.",
   code:`int a = min(3, 7);\n// a == 3`,out:"→ 3"},

  {cat:"minmax",name:"std::max",desc:"Returns the larger of two values.",
   code:`int a = max(3, 7);\n// a == 7`,out:"→ 7"},

  {cat:"minmax",name:"std::minmax",desc:"Returns a pair {min, max} of two values.",
   code:`auto [lo,hi] = minmax(3, 7);\n// lo==3, hi==7`,out:"→ {3, 7}"},

  {cat:"minmax",name:"std::min_element",desc:"Returns iterator to smallest element in range.",
   code:`vector<int> v{3,1,4,1,5};\nauto it = min_element(v.begin(),v.end());\n// *it == 1`,out:"→ 1"},

  {cat:"minmax",name:"std::max_element",desc:"Returns iterator to largest element in range.",
   code:`auto it = max_element(v.begin(),v.end());\n// *it == 5`,out:"→ 5"},

  {cat:"minmax",name:"std::minmax_element",desc:"Returns pair of iterators to min and max.",
   code:`auto [mn,mx] = minmax_element(v.begin(),v.end());\n// *mn==1, *mx==5`,out:"→ {1, 5}"},

  {cat:"minmax",name:"std::clamp",desc:"Clamps a value between lo and hi bounds.",
   code:`int a = clamp(10, 1, 5);\n// a == 5  (clamped to max)`,out:"→ 5"},

  {cat:"set",name:"std::set_union",desc:"Produces union of two sorted sets.",
   code:`vector<int> a{1,2,3}, b{2,3,4}, out;\nset_union(a.begin(),a.end(),\n  b.begin(),b.end(),back_inserter(out));\n// out == {1,2,3,4}`,out:"→ 1 2 3 4"},

  {cat:"set",name:"std::set_intersection",desc:"Produces intersection of two sorted sets.",
   code:`set_intersection(a.begin(),a.end(),\n  b.begin(),b.end(),back_inserter(out));\n// out == {2,3}`,out:"→ 2 3"},

  {cat:"set",name:"std::set_difference",desc:"Produces elements in first set not in second.",
   code:`set_difference(a.begin(),a.end(),\n  b.begin(),b.end(),back_inserter(out));\n// out == {1}`,out:"→ 1"},

  {cat:"set",name:"std::set_symmetric_difference",desc:"Produces elements in exactly one of the two sets.",
   code:`set_symmetric_difference(a.begin(),a.end(),\n  b.begin(),b.end(),back_inserter(out));\n// out == {1,4}`,out:"→ 1 4"},

  {cat:"set",name:"std::includes",desc:"Returns true if one sorted range is a subset of another.",
   code:`bool ok = includes(a.begin(),a.end(),\n  b.begin(),b.end());\n// false — {2,3,4} not subset of {1,2,3}`,out:"→ false"},

  {cat:"heap",name:"std::make_heap",desc:"Rearranges range into a max-heap.",
   code:`vector<int> v{3,1,4,1,5,9};\nmake_heap(v.begin(),v.end());\n// v[0] == 9 (max at front)`,out:"→ v[0] = 9"},

  {cat:"heap",name:"std::push_heap",desc:"After push_back, inserts new element into heap.",
   code:`v.push_back(7);\npush_heap(v.begin(),v.end());\n// heap property maintained`,out:"→ heap valid"},

  {cat:"heap",name:"std::pop_heap",desc:"Moves the max element to end; call pop_back to remove.",
   code:`pop_heap(v.begin(),v.end());\nv.pop_back();\n// max removed`,out:"→ max removed"},

  {cat:"heap",name:"std::sort_heap",desc:"Sorts a heap into ascending order.",
   code:`sort_heap(v.begin(),v.end());\n// v now sorted ascending`,out:"→ sorted"},

  {cat:"heap",name:"std::is_heap",desc:"Returns true if range satisfies heap property.",
   code:`bool ok = is_heap(v.begin(),v.end());\n// ok == true after make_heap`,out:"→ true"},

  {cat:"heap",name:"std::is_heap_until",desc:"Returns iterator to first element violating heap property.",
   code:`auto it = is_heap_until(v.begin(),v.end());`,out:"→ first bad element"},

  {cat:"num",name:"std::accumulate",desc:"Computes the sum (or custom fold) of a range. (In <numeric>)",
   code:`vector<int> v{1,2,3,4,5};\nint sum = accumulate(v.begin(),v.end(),0);\n// sum == 15`,out:"→ 15"},

  {cat:"num",name:"std::iota",desc:"Fills range with incrementing sequence. (In <numeric>)",
   code:`vector<int> v(5);\niota(v.begin(),v.end(),1);\n// v == {1,2,3,4,5}`,out:"→ 1 2 3 4 5"},

  {cat:"num",name:"std::inner_product",desc:"Computes dot product of two ranges. (In <numeric>)",
   code:`vector<int> a{1,2,3}, b{4,5,6};\nint dot = inner_product(\n  a.begin(),a.end(),b.begin(),0);\n// 1*4+2*5+3*6 == 32`,out:"→ 32"},

  {cat:"num",name:"std::partial_sum",desc:"Computes prefix sums. (In <numeric>)",
   code:`vector<int> v{1,2,3,4,5}, out(5);\npartial_sum(v.begin(),v.end(),out.begin());\n// out == {1,3,6,10,15}`,out:"→ 1 3 6 10 15"},

  {cat:"num",name:"std::adjacent_difference",desc:"Computes differences of adjacent elements. (In <numeric>)",
   code:`vector<int> v{1,3,6,10}, out(4);\nadjacent_difference(v.begin(),v.end(),out.begin());\n// out == {1,2,3,4}`,out:"→ 1 2 3 4"},

  {cat:"num",name:"std::gcd",desc:"Greatest common divisor of two integers. (In <numeric>)",
   code:`int g = gcd(12, 18);\n// g == 6`,out:"→ 6"},

  {cat:"num",name:"std::lcm",desc:"Least common multiple of two integers. (In <numeric>)",
   code:`int l = lcm(4, 6);\n// l == 12`,out:"→ 12"},

  {cat:"mod",name:"std::all_of",desc:"Returns true if ALL elements satisfy predicate.",
   code:`vector<int> v{2,4,6,8};\nbool ok = all_of(v.begin(),v.end(),\n  [](int x){return x%2==0;});\n// ok == true`,out:"→ true"},

  {cat:"mod",name:"std::any_of",desc:"Returns true if ANY element satisfies predicate.",
   code:`bool ok = any_of(v.begin(),v.end(),\n  [](int x){return x>5;});\n// ok == true`,out:"→ true"},

  {cat:"mod",name:"std::none_of",desc:"Returns true if NO element satisfies predicate.",
   code:`bool ok = none_of(v.begin(),v.end(),\n  [](int x){return x<0;});\n// ok == true`,out:"→ true"},

  {cat:"mod",name:"std::equal",desc:"Returns true if two ranges are element-wise equal.",
   code:`vector<int> a{1,2,3}, b{1,2,3};\nbool ok = equal(a.begin(),a.end(),b.begin());\n// ok == true`,out:"→ true"},

  {cat:"mod",name:"std::mismatch",desc:"Returns iterators to first mismatched pair in two ranges.",
   code:`vector<int> a{1,2,3}, b{1,9,3};\nauto [ia,ib] = mismatch(a.begin(),a.end(),b.begin());\n// *ia==2, *ib==9`,out:"→ 2 vs 9"},

  {cat:"mod",name:"std::lexicographical_compare",desc:"Returns true if first range is lexicographically less.",
   code:`bool ok = lexicographical_compare(\n  a.begin(),a.end(),b.begin(),b.end());\n// true if a < b`,out:"→ true/false"},

  {cat:"mod",name:"std::move",desc:"Moves elements from source to destination range.",
   code:`vector<string> src{"a","b","c"}, dst(3);\nmove(src.begin(),src.end(),dst.begin());\n// src elements in valid but unspecified state`,out:"→ dst has values"},

  {cat:"mod",name:"std::copy_backward",desc:"Copies range to destination starting from the end.",
   code:`vector<int> v{1,2,3,4,5};\ncopy_backward(v.begin(),v.begin()+3,v.end());\n// v=={1,2,1,2,3}`,out:"→ 1 2 1 2 3"},

  {cat:"mod",name:"std::sample",desc:"Randomly selects N elements from range (C++17).",
   code:`mt19937 rng(42);\nvector<int> v{1,2,3,4,5}, out;\nsample(v.begin(),v.end(),\n  back_inserter(out),3,rng);`,out:"→ 3 random elements"},

  {cat:"mod",name:"std::partition",desc:"Reorders elements so those satisfying predicate come first.",
   code:`vector<int> v{1,2,3,4,5};\npartition(v.begin(),v.end(),\n  [](int x){return x%2==0;});\n// evens first`,out:"→ 2 4 | 1 3 5"},

  {cat:"mod",name:"std::stable_partition",desc:"Like partition but preserves relative order.",
   code:`stable_partition(v.begin(),v.end(),\n  [](int x){return x%2==0;});\n// order preserved within groups`,out:"→ 2 4 1 3 5"},

  {cat:"mod",name:"std::partition_point",desc:"Returns iterator to first element in second partition (range must be partitioned).",
   code:`auto it = partition_point(v.begin(),v.end(),\n  [](int x){return x%2==0;});\n// *it == first odd`,out:"→ iterator to 1st odd"},
];

const badgeClass = {sort:"badge-sort",search:"badge-search",count:"badge-count",mod:"badge-mod",perm:"badge-perm",minmax:"badge-minmax",set:"badge-set",heap:"badge-heap",num:"badge-num"};
const catLabel = {sort:"Sorting",search:"Searching",count:"Counting",mod:"Modifying",perm:"Permutations",minmax:"Min/Max",set:"Set ops",heap:"Heap",num:"Numeric"};

const tabsEl = document.getElementById("tabs");
const gridEl = document.getElementById("grid");

cats.forEach(c=>{
  const b = document.createElement("button");
  b.className="tab"+(c.id==="all"?" active":"");
  b.textContent=c.label;
  b.dataset.id=c.id;
  b.onclick=()=>{
    document.querySelectorAll(".tab").forEach(t=>t.classList.remove("active"));
    b.classList.add("active");
    render(c.id);
  };
  tabsEl.appendChild(b);
});

function render(cat){
  gridEl.innerHTML="";
  const list = cat==="all"?fns:fns.filter(f=>f.cat===cat);
  list.forEach(f=>{
    const card = document.createElement("div");
    card.className="card";
    card.innerHTML=`
      <span class="badge ${badgeClass[f.cat]}">${catLabel[f.cat]}</span>
      <div class="fn-name">${f.name}</div>
      <div class="fn-desc">${f.desc}</div>
      <div class="code-block">${f.code}</div>
      <div class="output">${f.output||""}</div>
    `;
    gridEl.appendChild(card);
  });
}

render("all");
</script>
