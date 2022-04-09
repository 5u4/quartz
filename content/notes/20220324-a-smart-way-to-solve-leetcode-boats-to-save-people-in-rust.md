---
title: A smart way to solve Leetcode boats to save people in Rust
date: 2022-03-24
tags:
  - leetcode
---

While I was solving [881. Boats to Save People](https://leetcode.com/problems/boats-to-save-people/), I found out a special issue on Rust.

The following solution should work normally in other languages like Java.

```rs
impl Solution {
    pub fn num_rescue_boats(people: Vec<i32>, limit: i32) -> i32 {
        let mut people = people;
        people.sort_unstable();

        let mut count = 0;
        let mut i = 0;
        let mut j = people.len() - 1;

        while i <= j {
            if people[i] + people[j] <= limit {
                i += 1;
            }
            j -= 1;
            count += 1;
        }

        count
    }
}
```

However, the program panics on the following test case:

```rs
#[test]
fn example3() {
    let actual = Solution::num_rescue_boats(vec![3, 5, 3, 4], 5);
    let expected = 4;
    assert_eq!(actual, expected);
}

// thread '...' panicked at 'attempt to subtract with overflow' ...
```

The reason is that `j` is an `usize` which cannot be subtracted below 0.

I found out a smart solution that deals with the edge case elegantly. It counts all people first
and then subtract count when there are more than 1 people can take the boat.

```rs
impl Solution {
    pub fn num_rescue_boats(people: Vec<i32>, limit: i32) -> i32 {
        let mut people = people;
        people.sort_unstable();

        let mut count = people.len() as i32;
        let mut i = 0;
        let mut j = people.len() - 1;

        while i < j {
            if people[i] + people[j] <= limit {
                i += 1;
                count -= 1;
            }
            j -= 1;
        }

        count
    }
}
```
