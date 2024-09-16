# Scramble-String

We can scramble a string s to get a string t using the following algorithm:
If the length of the string is 1, stop.
If the length of the string is > 1, do the following:
Split the string into two non-empty substrings at a random index, i.e., if the string is s, divide it to x and y where s = x + y.
Randomly decide to swap the two substrings or to keep them in the same order. i.e., after this step, s may become s = x + y or s = y + x.
Apply step 1 recursively on each of the two substrings x and y.
Given two strings s1 and s2 of the same length, return true if s2 is a scrambled string of s1, otherwise, return false.

Constraints:
s1.length == s2.length
1 <= s1.length <= 30
s1 and s2 consist of lowercase English letters.

class Solution:
    map = {}

    def isScramble(self, s1: str, s2: str) -> bool:
        n = len(s1)
        if s1 == s2:
            return True
        a, b, c = [0] * 26, [0] * 26, [0] * 26
        if (s1 + s2) in self.map:
            return self.map[s1 + s2]
        for i in range(1, n):
            j = n - i
            a[ord(s1[i - 1]) - ord('a')] += 1
            b[ord(s2[i - 1]) - ord('a')] += 1
            c[ord(s2[j]) - ord('a')] += 1
            if a == b and self.isScramble(s1[:i], s2[:i]) and self.isScramble(s1[i:], s2[i:]):
                self.map[s1 + s2] = True
                return True
            if a == c and self.isScramble(s1[:i], s2[j:]) and self.isScramble(s1[i:], s2[:j]):
                self.map[s1 + s2] = True
                return True
        self.map[s1 + s2] = False
        return False
