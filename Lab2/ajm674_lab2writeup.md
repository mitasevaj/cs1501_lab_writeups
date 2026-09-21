# Lab 2 writeup
## Alexander Mitasev (ajm674)

**Full code solution:**
```
class Solution {
    public TreeNode mergeTrees(TreeNode root1, TreeNode root2) {
        //Start with root nodes of both trees
        //Recursive approach, traverse through trees, starting left then going right
        //Check if both nodes are valid, then either add values or put non null value
        //Stop traversal to a given side when there is a null reference from both nodes

        if(root1 == null){
            return root2;
        }
        if(root2 == null){
            return root1;
        }
        
        TreeNode curr1 = root1;
        TreeNode curr2 = root2;
        TreeNode currNew  = null;
        
        currNew = mergeRec(curr1, curr2, currNew);

        return currNew;
    }

    private TreeNode mergeRec(TreeNode curr1, TreeNode curr2, TreeNode currNew){
        if(curr1 != null && curr2 != null){
            currNew = new TreeNode(curr1.val + curr2.val);
            currNew.left = mergeRec(curr1.left, curr2.left, currNew.left);
            currNew.right = mergeRec(curr1.right, curr2.right, currNew.right);
        }else if(curr1 == null && curr2 != null){
            currNew = new TreeNode(curr2.val);
            currNew.left = mergeRec(curr1, curr2.left, currNew.left);
            currNew.right = mergeRec(curr1, curr2.right, currNew.right);
        }else if(curr1 != null && curr2 == null){
            currNew = new TreeNode(curr1.val);
            currNew.left = mergeRec(curr1.left, curr2, currNew.left);
            currNew.right = mergeRec(curr1.right, curr2, currNew.right);
        }else{
            return null;
        }
        
        return currNew;
    }
}
```

**What the code is doing and why:**\
For this problem, I decided that it was best to use a recursive approach. I knew that traversing both trees would be required to merge them together, as well as keeping track of the position within the new tree being created as a result of the merge. To start, I checked if either of the trees were null, since then the result would just be the other tree. I don't know if this was actually a test case or not but I thought it would be good to account for. Then I initialized references for the current node in the first tree, the current node in the second tree, and the current node in the new tree. Afterwards, I called a recursive helper method that I wrote to help with the traversal.
First, this method checks if both of the current Node pointers for the two original trees are not null. If both nodes are not null, then we add the two keys and make a new node in the new tree with that key. We first traverse all the way to the left, then all the way to the right, since both of the nodes have a place to go off of. In the case that one node is null and the other isn't, we create a new node with the same key as the non-null node. In this case, we only continue traversal in from the node that is not null, since the null node has nowhere to go. In the final case, where both nodes are null, we have reached past the leaves of both trees, so there is no more new keys to add to that subtree in the new tree, so we just return null. Finally, the method call returns the node that will be put in the corresponding location in the new tree.
After this method is finished running, the reference 'currNew' contains the head of the merged tree and we return it.

**Runtime and Memory Analysis:**\
In this case, the runtime is bound by O(m + n), where m is the size of the first tree and n is the size of the second tree, or more simply just O(n).
The recursive algorithm visits every position where a given tree has a node, then stops recursion when there is a position reached where neither tree has a node. In the worse case, this will visit the same amount of positions in each tree, meaning that the two trees are the same shape.
In terms of memory, I created a new tree with the merge results instead of merging the two trees in place, which is more expensive memory-wise. This means that the algorithm uses O(n) extra space to create the amount of nodes needed for this new tree.
The memory is also affected by the recursive implementation, since most of the time there is multiple function calls on the stack at a given moment. This is bounded by the heights of the trees, which is O(lg n) in the best case and O(n) in the worst case.