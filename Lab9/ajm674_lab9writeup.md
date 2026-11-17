# Lab 9 writeup
## Alexander Mitasev (ajm674)

**Full code solution:**
```
class Solution {
    public int minCostClimbingStairs(int[] cost) {
        int[] minCost = new int[cost.length];
        minCost[0] = cost[0]; minCost[1] = cost[1];
        for(int i = 2; i < cost.length; i++){
            minCost[i] = cost[i] + Math.min(minCost[i - 1], minCost[i - 2]);
        }
        return Math.min(minCost[cost.length - 1], minCost[cost.length -2]); 
    }
}
```
**What the code is doing and why:**\
To solve this problem, I used a dynamic programming approach to find the minimum cost of moving from any given step, since the minimum cost depends on the sum of all previous minimum costs. My solution checks the cost of leaving a step, and then checks what the minimum cost to get to that step is, which is the minimum cost value of the two previous steps. Iterating through the cost array once gives the solution, which is the minimum value of the miinmum costs to leave the last 2 steps.
**Runtime and Memory Analysis:**\
Time complexity is $O(n)$, where n is the length of the array `cost`, since we iterate through the array once. There is also an $O(n)$ space complexity, since we create an array `minCost` that is the same size as `cost` to hold the minimum values.