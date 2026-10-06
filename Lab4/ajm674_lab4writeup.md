# Lab 3 writeup
## Alexander Mitasev (ajm674)

**Full code solution:**
```
class Solution {
    public int maxProduct(int[] nums) {
        int max1 = Math.max(nums[0], nums[1]);
        int max2 = Math.min(nums[0], nums[1]);

        for(int i = 2; i < nums.length; i++){
            if(nums[i] >= max2){
                if(nums[i] > max1){
                    max2 = max1;
                    max1 = nums[i];
                }else{
                    max2 = nums[i];
                }
            }
        }

        return (max1 - 1) * (max2 - 1);
        
    }
}
```

**What the code is doing and why:**\
The idea of this problem is to return the maximum value of `(nums[i] - 1) * (nums[j] - 1)`, where i and j are two distinct indices of the array `nums`.\
In the constraints of the problem, the length of the array is guaranteed to be at least two, and each value in `nums` is guaranteed to be positive, so we don't need to worry about not having enough values or having negative values.\
In other words, we just need to find the two largest values in the array, and then return the corresponding product.\
I initialized two variables, `max1` and `max2`, with the first holding the current largest value and the second holding the current second largest value.\
Then, I iterate through the array, checking if each value is larger than one of the two current largest.\
If a value is larger than the second largest, but not the largest, then we just replace the second largest value.\
If a value is larger than the largest value, we set the second largest value to the old largest, then set the new largest value to the value we found.\
We continue this process through the end of the array, then we return the product `(max1 - 1) * (max2 - 1)`
**Runtime and Memory Analysis:**\
The runtime of this algorithm is entirely dependent on how many values are in the initial array, since we traverse through the entire array no matter what to check all values.\
The only case where this is different is the "best case" of there being only two values in the array, since then no traversal is required.\
That being said, this algorithm is $O(1)$ in the best case and $O(n)$ in the average/worst case (all other cases)\
No auxilliary space is used, so the space complexity is $O(1)$