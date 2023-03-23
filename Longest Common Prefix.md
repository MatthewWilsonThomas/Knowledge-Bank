#Problem 
Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string `""`.

```python
class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        longest_prefix: str = strs[0]
        for string in strs:
            if len(string) < len(longest_prefix):
                longest_prefix = longest_prefix[:len(string)]
            for loc, letter in enumerate(string):
                if loc < len(longest_prefix) and letter != longest_prefix[loc]:
                    longest_prefix = longest_prefix[:loc]

        return longest_prefix```