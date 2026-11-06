# Lab 8 writeup
## Alexander Mitasev (ajm674)

**Full code solution:**
```
class Solution(object):
    def isValid(self, s):
        """
        :type s: str
        :rtype: bool
        """
        stack = []

        for c in s:
            if c == '(' or c == '{' or c == '[':
                stack.append(c)
            if c == ')':
                if not stack or stack.pop() != '(':
                    return False
            if c == '}':
                if not stack or stack.pop() != '{':
                    return False
            if c == ']':
                if not stack or stack.pop() != '[':
                    return False
        return not stack 
        
```

**What the code is doing and why:**\
To solve this problem, I used a stack approach. If the current character is an opening bracket, I push it onto the stack. If the current character is a closing bracket, I first check if there is anything on the stack. If there is nothing on the stack, that means there are no more opening brackets to process, so the string is not valid. Then, I pop a character off the stack and check if it is the correct corresponding opening bracket. If it is not, then the string is invalid and we return false. After the loop finishes iterating, if there are any unprocessed opening brackets on the stack, that means they never got paired to a closing bracket, so the string is invalid.
**Runtime and Memory Analysis:**\
Time complexity is $O(n)$, where n is the amount of characters in the input string. Space complexity is at most $O(n)$ because of the added memory of the stack which will have at most n items, where n is the number of characters in the string. 