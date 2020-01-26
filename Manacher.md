# Manacher Algorithm

Longest Palindromic Substring
<https://leetcode.com/problems/longest-palindromic-substring/> 

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
