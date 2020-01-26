# Manacher Algorithm 

Time Complexity: O(n)
Space Complexity: O(n)

Example: Longest Palindromic Substring <https://leetcode.com/problems/longest-palindromic-substring/> 

## Overview:
Each palindrome has a center.  
There are two types of palindrome: palindrome with odd length with single char as center, and palindrome with even length with center between two chars.  
For simplification Manacher algorithm modifies input string to work with palindromes having odd length only.  
We can say each palindrome has c - center, l - left border or first char, r - right border or last char and d - distance.  
Distance of palindrome d = r - center => l = center - d. For example, s = "ababa": c = s[2], l = s[0], r = s[4], d = 2.  

## Variables:
 M - modified string, for example: "aba" -> "@#a#b#a#$"
 C - center of palindrome. No need to check center between two characters since we use modified string
 R - max index in M reached by expanding around center C
 P - array. P[i] is max distance for palindrome with center i. 
 

```pytnon3
def longestPalindrome(self, s: str) -> str:
        # O(N) Manacher

        # edge cases
        if len(s) < 2: return s

        # modify input to catch center between two letters, handle boundaries
        # format looks like: "@#{"#".join(s)}#$"
        M = ["@", "#"]
        for x in s:
            M.append(x)
            M.append("#")
        M.append("$")

        # initialize P, P[i] is a max distance if i is center
        P = [0]*len(M)
        # initialize global R = right border and C - corresponding center for R
        R = C = 0
        for i in range(1, len(M) - 1):
            # C < i by default, C was checked before
            # check this to define if iMirror exists
            if i <= R:
                iMirror = C - (i - C)
                # cut palindrome distance if right can exceed global right border R
                # availble max distance for center i is R - i
                P[i] = min(P[iMirror], R - i)

            # expand palindrome for center i increasing distance if M[l] == M[r]
            while M[i - P[i] - 1] == M[i + P[i] - 1]:
                    P[i] += 1

            # update R and C in case if greater R was reached
            if i + P[i] - 1 > R:
                C = i
                R = i + P[i] - 1

        # find center with max dist
        center = 0
        for i in range(1, len(P)):
            if P[center] < P[i]:
                center = i

        # construct palindrome cleaning '#'
        p = []
        for i in range(center-P[center], center + P[center]-1):
            if M[i] != "#": p.append(M[i])

        return "".join(p)
```
