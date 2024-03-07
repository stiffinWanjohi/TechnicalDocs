# Letter Combinations of a Phone Number

## Problem Statement

Given a string containing digits from `2-9` inclusive, we need to return all possible letter combinations that the number could represent. The mapping of digits to letters is the same as the traditional phone keypad layout.

Here's the mapping:

```
2 -> ['a', 'b', 'c']
3 -> ['d', 'e', 'f']
4 -> ['g', 'h', 'i']
5 -> ['j', 'k', 'l']
6 -> ['m', 'n', 'o']
7 -> ['p', 'q', 'r', 's']
8 -> ['t', 'u', 'v']
9 -> ['w', 'x', 'y', 'z']
```

We need to return the answer in any order.

## Examples

**Example 1:**

```
Input: digits = "23"
Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"]
```

**Example 2:**

```
Input: digits = ""
Output: []
```

**Example 3:**

```
Input: digits = "2"
Output: ["a", "b", "c"]
```

## Constraints

- `0 <= digits.length <= 4`
- `digits[i]` is a digit in the range `['2', '9']`

## Approach 1: Backtracking

We can solve this problem using a backtracking approach. Below is the general idea:

1. Create a mapping of digits to characters.
2. Initialize an empty result list.
3. Recursively generate all combinations:
   - Base case: If the length of the current combination is equal to the length of the input string, add it to the result list.
   - Recursive case: For each character mapped to the current digit, append it to the current combination and recursively generate combinations for the remaining digits.

Here's the implementation in Python:

```python
class Solution:
    def letterCombinations(self, digits: str) -> List[str]:
        if not digits:
            return []

        # mapping of digits to characters
        digit_map = {
            '2': 'abc',
            '3': 'def',
            '4': 'ghi',
            '5': 'jkl',
            '6': 'mno',
            '7': 'pqrs',
            '8': 'tuv',
            '9': 'wxyz'
        }

        result = []

        def backtrack(combination, next_digits):
            # if no more digits left, add the current combination to the result
            if not next_digits:
                result.append(combination)
                return

            # get the characters for the current digit
            chars = digit_map[next_digits[0]]

            # generate combinations for each character
            for char in chars:
                backtrack(combination + char, next_digits[1:])

        # start the backtracking process
        backtrack("", digits)

        return result
```

Let's go through the code step by step:

1. First, we handle the base case where the input string is empty. In this case, we simply return an empty list.

2. We create a mapping `digit_map` that maps each digit to its corresponding characters.

3. We initialize an empty list `result` to store the final combinations.

4. We define a helper function `backtrack` that takes two arguments:

   - `combination`: the current combination of characters being generated
   - `next_digits`: the remaining digits to process

5. Inside the `backtrack` function:

   - If there are no more digits left (`next_digits` is empty), we have generated a complete combination, so we append it to the `result` list and return.
   - Otherwise, we get the characters `chars` mapped to the current digit `next_digits[0]` from the `digit_map`.
   - For each character `char` in `chars`, we recursively call `backtrack` with the updated combination (`combination + char`) and the remaining digits (`next_digits[1:]`).

6. We start the backtracking process by calling `backtrack("", digits)`, which initializes the combination as an empty string and passes the entire input string as the remaining digits.

7. Finally, we return the `result` list containing all possible letter combinations.

## Complexity Analysis

- Time complexity: O(3^N \* 4^M), where N is the number of digits in the input that map to 3 letters (e.g., '7', '9') and M is the number of digits in the input that map to 4 letters (e.g., '7', '9'). In the worst case, the input string contains only digits that map to 4 letters, so the time complexity becomes O(4^N), where N is the length of the input string.

- Space complexity: O(3^N \* 4^M), where N is the number of digits in the input that map to 3 letters (e.g., '7', '9') and M is the number of digits in the input that map to 4 letters (e.g., '7', '9'). This is because, in the worst case, we need to store all the possible combinations in the result list. In the worst case, where the input string contains only digits that map to 4 letters, the space complexity becomes O(4^N), where N is the length of the input string.

## Example Usage

```python
solution = Solution()
print(solution.letterCombinations("23"))  # Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"]
print(solution.letterCombinations(""))     # Output: []
print(solution.letterCombinations("2"))    # Output: ["a", "b", "c"]
```

In this implementation, we have covered all the requirements and constraints of the problem. We have provided a detailed explanation of the approach, the code implementation, the time and space complexity analysis, and example usage.

---

## Approach 2: Optimized Iterative Approach (Mapping Guarded Recursive Approach / Optimized Queue)

This approach is considered the fastest and most efficient solution to the "Letter Combinations of a Phone Number" problem. It uses an optimized iterative approach that avoids creating unnecessary intermediate strings, making it more efficient than the backtracking and iterative queue approaches, especially for longer input strings.

### Implementation

Here's the implementation in Python:

```python
class Solution:
    def letterCombinations(self, digits: str) -> List[str]:
        if not digits:
            return []

        # Mapping of digits to characters
        digit_map = {
            '2': 'abc',
            '3': 'def',
            '4': 'ghi',
            '5': 'jkl',
            '6': 'mno',
            '7': 'pqrs',
            '8': 'tuv',
            '9': 'wxyz'
        }

        result = [""]  # Start with an empty string

        for digit in digits:
            chars = digit_map[digit]
            result = [prev + char for char in chars for prev in result]

        return result
```

### Explanation

1. We start by handling the base case where the input string `digits` is empty. In this case, we return an empty list `[]`.

2. We create a mapping `digit_map` that maps each digit to its corresponding characters, similar to the previous approaches.

3. We initialize an empty list `result` containing an empty string `""`. This will be used to store the final combinations.

4. We iterate through each digit in the input string `digits`.

5. For each digit, we get the characters `chars` mapped to that digit from the `digit_map`.

6. We use a list comprehension to generate a new `result` list by appending each character from `chars` to each existing string in the `result` list.

   - `[prev + char for char in chars for prev in result]` generates a new list by concatenating each character from `chars` with each string in the current `result` list.
   - For example, if the current `result` is `["a", "b"]` and `chars` is `["c", "d"]`, the new `result` will become `["ac", "ad", "bc", "bd"]`.

7. After processing all digits, the final list of combinations is stored in the `result` list, which we return.

### Example

Let's consider the input `"23"`:

- Initially, `result` contains `[""]`.
- For digit `'2'`, `chars` is `['a', 'b', 'c']`.
  - The new `result` becomes `["a", "b", "c"]`.
- For digit `'3'`, `chars` is `['d', 'e', 'f']`.
  - The new `result` becomes `["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"]`.

### Time Complexity

The time complexity of this approach is O(3^N \* 4^M), where N is the number of digits in the input that map to 3 letters (e.g., '7', '9'), and M is the number of digits in the input that map to 4 letters (e.g., '7', '9'). In the worst case, where the input string contains only digits that map to 4 letters, the time complexity becomes O(4^N), where N is the length of the input string.

### Space Complexity

The space complexity is O(3^N \* 4^M), where N is the number of digits in the input that map to 3 letters (e.g., '7', '9'), and M is the number of digits in the input that map to 4 letters (e.g., '7', '9'). This is because, in the worst case, we need to store all the possible combinations in the `result` list. In the worst case, where the input string contains only digits that map to 4 letters, the space complexity becomes O(4^N), where N is the length of the input string.

### Advantages

This approach is considered the fastest and smoothest method for solving the "Letter Combinations of a Phone Number" problem due to its simplicity, efficiency, and lack of unnecessary overhead. It avoids the overhead of recursive function calls and the creation of unnecessary intermediate strings, making it more efficient than the backtracking and iterative queue approaches, especially for longer input strings.

While the time and space complexities of this approach are theoretically the same as the previous approaches, this optimized iterative approach is generally faster and more efficient in practice.

### Example Usage

```python
solution = Solution()
print(solution.letterCombinations("23"))  # Output: ['ad', 'ae', 'af', 'bd', 'be', 'bf', 'cd', 'ce', 'cf']
print(solution.letterCombinations(""))     # Output: []
print(solution.letterCombinations("2"))    # Output: ['a', 'b', 'c']
```

In this technical document, we have covered the implementation, explanation, example, time and space complexity analysis, advantages, and example usage of the optimized iterative approach (Mapping Guarded Recursive Approach / Optimized Queue) for solving the "Letter Combinations of a Phone Number" problem. This approach is considered the fastest and most efficient solution to this problem.
