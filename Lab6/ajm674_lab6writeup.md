# Lab 6 writeup
## Alexander Mitasev (ajm674)

**Full code solution:**
```
class Solution {
    public int findJudge(int n, int[][] trust) {
        int[][] howManyTrust = new int[n][2];
        for(int i = 0; i < trust.length; i++){
            howManyTrust[trust[i][0] - 1][0]++;
            howManyTrust[trust[i][1] - 1][1]++;
        }
        for(int i = 0; i < howManyTrust.length; i++){
            if(howManyTrust[i][0] == 0 && howManyTrust[i][1] == n - 1) return i + 1;
        }
        return -1;
    }
}
```

**What the code is doing and why:**\
We can think of the problem described as being represented as a directed graph, where an edge from one vertex to another means that the starting vertex "trusts" the destination vertex. I created a 2d array `count` to store the amount of times a vertex is the end of an edge and the amount of times a vertex is the start of an edge. Then, I search this 2d array for a vertex that has `n - 1` connections to it and 0 connections from it, since this vertex would fit the description of the town judge (the town judge trusts nobody and everybody trusts the town judge). If no such vertex exists, return -1;
**Runtime and Memory Analysis:**\
The runtime for this solution is $O(T + N)$ where $T$ is the amount of connections in the `trust` 2d array and where $N$ is the amount of people in the town. This is because we start with an $O(T)$ traversal of `trust` to count all of the connections, then we have a $O(N)$ traversal of `howManyTrust` to search for the town judge. There is a space complexity of $O(N)$ due to the creation of an extra 2d array of size `n`.