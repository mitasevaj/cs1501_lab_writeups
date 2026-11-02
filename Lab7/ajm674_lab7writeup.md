# Lab 7 writeup
## Alexander Mitasev (ajm674)

**Full code solution:**
```
class Solution {
    public int[][] floodFill(int[][] image, int sr, int sc, int color) {
        if(image[sr][sc] == color){
            return image;
        }
        int startColor = image[sr][sc];
        image[sr][sc] = color;
        fillNeighbors(image, sr, sc, startColor, color);
        return image;
    }

    private void fillNeighbors(int[][] image, int sr, int sc, int startColor, int newColor){
        if(sr - 1 >= 0 && image[sr - 1][sc] == startColor){
            image[sr - 1][sc] = newColor;
            fillNeighbors(image, sr - 1, sc, startColor, newColor);
        }
        if(sr + 1 < image.length && image[sr + 1][sc] == startColor){
            image[sr + 1][sc] = newColor;
            fillNeighbors(image, sr + 1, sc, startColor, newColor);
        }
        if(sc - 1 >= 0 && image[sr][sc - 1] == startColor){
            image[sr][sc - 1] = newColor;
            fillNeighbors(image, sr, sc - 1, startColor, newColor);
        }
        if(sc + 1 < image[sr].length && image[sr][sc + 1] == startColor){
            image[sr][sc + 1] = newColor;
            fillNeighbors(image, sr, sc + 1, startColor, newColor);
        }
    }
}
```

**What the code is doing and why:**\
To solve this problem, I decided to use a recursive DFS approach. I initially tried to use a BFS based approach, but DFS proved to be easier for me, at least implementation wise. In the main method, we check if the starting pixel matches the value of `color`, then we just return image since we don't need to change anything. I set the value of `startColor` to the initial pixel color, then change the value at the starting pixel.
My `fillNeighbors` method checks every neighbor of the current pixel, starting with the one above it. At each direction, we check if the index is valid and if the value at that neighbor matches the start color. If it meets those two conditions, we continue traversal in that direction.
After the DFS is complete, all neighbors have been checked, and the flood fill is completed.
**Runtime and Memory Analysis:**\
Time complexity is $O(m x n)$, where m and n are the length and width of the `image` 2d array, because every pixel is visited at most once, and the work at each pixel is constant.
Space complexity is at most $O(m x n)$, because at worst we will have a recursive call on the stack for every pixel.