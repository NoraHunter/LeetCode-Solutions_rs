# LeetCode


### 1929. Concatenation of Array
```Rust
impl Solution {
    pub fn get_concatenation(nums: Vec<i32>) -> Vec<i32> {
        [&nums[..], &nums[..]].concat()
    }
}
```



### 1920. Build Array from Permutation
```Rust
impl Solution {
    pub fn build_array(nums: Vec<i32>) -> Vec<i32> {
        let mut ans : Vec<i32> = Vec::new();
        for i in 0..nums.len() {
            ans.push(nums[nums[i] as usize]);
        }        
        return ans;
    }
}
```



### 1512. Number of Good Pairs
```Rust
impl Solution {
    pub fn num_identical_pairs(nums: Vec<i32>) -> i32 {
        let mut good_pairs : i32 = 0;
        for i in 0..nums.len(){
            for j in 0..nums.len(){
                if nums[i] == nums[j] && i < j{
                    good_pairs += 1;
                }
            }
        }   
        return good_pairs;
    }
}
```



### 2011. Final Value of Variable After Performing Operations
```Rust
impl Solution {
    pub fn final_value_after_operations(operations: Vec<String>) -> i32 {
        let mut result : i32 = 0;
        for i in operations{
            match i.as_str() {
                "++X" | "X++" => result += 1,
                "--X" | "X--" => result -= 1,
                _ => {},
            }
        }
        return result;
    }
}   
```



### 1470. Shuffle the Array
```Rust
impl Solution {
    pub fn shuffle(nums: Vec<i32>, n: i32) -> Vec<i32> {
        let mut result : Vec<i32> = Vec::new();
        for i in 0..nums.len() / 2{
            result.push(nums[i]);
            result.push(nums[i + n as usize]);
        }
        return result;
    }
}
```



### 1476. Subrectangle Queries
```Rust
struct SubrectangleQueries {
    rectangle: Vec<Vec<i32>>,
}

impl SubrectangleQueries {

    fn new(rectangle: Vec<Vec<i32>>) -> Self {
        Self{ rectangle }
    }
    
    fn update_subrectangle(&mut self, row1: i32, col1: i32, row2: i32, col2: i32, new_value: i32) {
        for i in row1..=row2{
            for j in col1..=col2{
                self.rectangle[i as usize][j as usize] = new_value;
            }
        }
    }
    
    fn get_value(&self, row: i32, col: i32) -> i32 {
        self.rectangle[row as usize][col as usize]
    }
}
```



### 2942. Find Words Containing Character
```Rust
impl Solution {
    pub fn find_words_containing(words: Vec<String>, x: char) -> Vec<i32> {
        let mut result : Vec<i32> = Vec::new();
        for i in 0..words.len(){
            if words[i].contains(x){
                result.push(i as i32);
            }
        }
        return result;
    }
}
```



###  2433. Find The Original Array of Prefix Xor
```Rust
impl Solution {
    pub fn find_array(pref: Vec<i32>) -> Vec<i32> {
        if pref.is_empty() {
            return Vec::<i32>::new();
        }
        let mut result: Vec<i32> = vec![pref[0]];
        for i in 1..pref.len() {
            let mut xor_ops: i32 = 0;
            for j in 0..result.len() {
                xor_ops ^= result[j];
            }
            result.push(xor_ops ^ pref[i]);
        }
        return result;
    }
}
```



### 1672. Richest Customer Wealth
```Rust
impl Solution {
    pub fn maximum_wealth(accounts: Vec<Vec<i32>>) -> i32 {
        let mut result: i32 = 0;
        for client in accounts {
            let mut curr_wealth: i32 = 0;
            for wealth in client {
                curr_wealth += wealth;
            }
            if curr_wealth > result {
                result = curr_wealth;
            }
        }
        return result;
    }
}
```



### 1637. Widest Vertical Area Between Two Points Containing No Points
```Rust
impl Solution {
    pub fn max_width_of_vertical_area(points: Vec<Vec<i32>>) -> i32 {
        let mut x_axis: Vec<i32> = Vec::new();
        for point in points {
            x_axis.push(point[0]);
        }
        x_axis.sort();

        let mut result: i32 = 0;
        for i in 1..x_axis.len() {
            let temp = x_axis[i] - x_axis[i - 1];
            if temp > result {
                result = temp;
            }
        }
        return result;
    }
}
```



### 2798. Number of Employees Who Met the Target
```Rust
impl Solution {
    pub fn number_of_employees_who_met_target(hours: Vec<i32>, target: i32) -> i32 {
        let mut result: i32 = 0;
        for e in hours {
            if e >= target {
                result += 1;
            }
        }
        result
    }
}
```



### 1282. Group the People Given the Group Size They Belong To
```Rust
use std::collections::hash_map::HashMap;

impl Solution {
    pub fn group_the_people(group_sizes: Vec<i32>) -> Vec<Vec<i32>> {
        let mut groups: HashMap<i32, Vec<i32>> = HashMap::new();
        for i in 0..group_sizes.len() {
            if groups.contains_key(&group_sizes[i]) {
                if let Some(x) = groups.get_mut(&group_sizes[i]) {
                    (*x).push(i as i32);
                }
            } else {
                groups.insert(group_sizes[i], vec![i as i32]);
            }
        }
        println!("{:?}", groups);

        let mut result: Vec<Vec<i32>> = vec![];
        for (key, val) in groups {
            for i in val.chunks(key as usize).map(|e| e.to_vec()) {
                result.push(i);
            }
        }
        println!("{result:?}");
        result
    }
}
```



### Find kth smallest 
```Rust
fn find_kth_smallest(mut coins: Vec<i32>, k: i32) -> i64 {
    let multiples = coins.clone();
    let mut result : i64 = 0;
    for _ in 0..k{
        let smallest_val = *coins.iter().min().unwrap();
        for (i, coin) in coins.iter_mut().enumerate(){
            if *coin == smallest_val{
                *coin += multiples[i];
            }
        }
        result = smallest_val as i64;
    }
    return result;
}
```



### 1431. Kids With the Greatest Number of Candies
```Rust
impl Solution {
    pub fn kids_with_candies(candies: Vec<i32>, extra_candies: i32) -> Vec<bool> {
        let greatest = *candies.iter().max().unwrap();
        let mut result: Vec<bool> = Vec::new();
        for e in candies {
            result.push(e + extra_candies >= greatest);
        }
        return result;
    }
}

```



### 2610. Convert an Array Into a 2D Array With Conditions
```Rust
use std::collections::BTreeSet;
impl Solution {
    pub fn find_matrix(mut nums: Vec<i32>) -> Vec<Vec<i32>> {
        let mut result: Vec<Vec<i32>> = Vec::new();
        while nums.len() > 0 {
            let mut temp_set: BTreeSet<i32> = BTreeSet::new();
            let mut removals: Vec<usize> = Vec::new();
            for (i, e) in nums.iter().enumerate() {
                let before_insert = temp_set.len();
                temp_set.insert(*e);
                if temp_set.len() != before_insert {
                    removals.push(i);
                }
            }
            result.push(temp_set.into_iter().collect());
            for i in removals.iter().rev() {
                nums.remove(*i);
            }
        }
        result
    }
}

```



###
```Rust

```

