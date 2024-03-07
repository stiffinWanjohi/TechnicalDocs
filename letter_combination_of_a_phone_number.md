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

## Approach

We can solve this problem using a backtracking approach. Here's the general idea:

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
