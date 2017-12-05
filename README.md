# bi-grams

Data-Source
---
- bi-gram data set (assume MySQL table named bigram_tbl)
 
Input
---
- String <start_word> Integer <max_num>

Algorithm
---
1. Initialize counter to 0

2. Choose the bigram w/ the largest match_count and starting with <start_word>.  
- Use the following SQL parameterized with <start_word> ==> ':word'.

```
"SELECT n-gram, SUM(match_count) as matches
FROM bigram_tbl
GROUP BY n-gram
HAVING n-gram LIKE ':word %'
ORDER BY matches DESC 
LIMIT 1;"
```

- If result is empty-set, halt.

- increment counter

3. Take the second-word in the chosen bigram as the next <start_word>.
- In case of a double-word bigram being selected, halt? (avoid endless loop).
- Compare counter to max_num.  If counter == max_num, halt.
- Repeat step #2 and proceed until counter == max_num, or query returns empty set.