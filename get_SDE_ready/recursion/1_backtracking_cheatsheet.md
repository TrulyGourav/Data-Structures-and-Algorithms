# Backtracking Cheat Sheet (FAANG Level)

## 1. Universal Template

```java
void backtrack(params...) {

    if (condition) {
        result.add(new ArrayList<>(temp));
        return;
    }

    for (int i = start; i < choices.length; i++) {

        if (skipCondition) continue;

        temp.add(choices[i]);

        backtrack(next_params);

        temp.remove(temp.size() - 1);
    }
}
```

---

## 2. Pattern Identification

| Problem | Pattern |
|--------|--------|
| Subsets | Include/Exclude or Loop |
| Subsets II | Loop + Skip duplicates |
| Permutations | Loop + visited |
| Permutations II | Loop + visited + skip dup |
| Combination Sum | Loop + reuse |
| Combination Sum II | Loop + no reuse + skip dup |

---

## 3. Key Patterns

### Subsets
```java
ans.add(new ArrayList<>(cur));
for (int i = start; i < nums.length; i++) {
    cur.add(nums[i]);
    backtrack(i + 1);
    cur.remove(cur.size() - 1);
}
```

### Subsets with Duplicates
```java
Arrays.sort(nums);
if (i > start && nums[i] == nums[i-1]) continue;
```

### Permutations
```java
if (used[i]) continue;
used[i] = true;
...
used[i] = false;
```

### Permutations with Duplicates
```java
if (i > 0 && nums[i] == nums[i-1] && !used[i-1]) continue;
```

---

## 4. Decision Guide

- Reuse allowed → use `i`
- No reuse → use `i + 1`
- Duplicates → sort + skip
- Order matters → permutations

---

## 5. Golden Rules

- Always copy list:
```java
new ArrayList<>(temp)
```

- Backtracking flow:
```
Choose → Explore → Un-choose
```

---

## 6. Complexities

- Subsets → O(2^n)
- Permutations → O(n!)
- Combination → Exponential
