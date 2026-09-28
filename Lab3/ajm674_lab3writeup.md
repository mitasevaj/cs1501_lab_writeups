# Lab 3 writeup
## Alexander Mitasev (ajm674)

**Full code solution:**
```
class Solution {
    public List<String> removeSubfolders(String[] folder) {
        ArrayList<String> removed = new ArrayList<String>();
        Arrays.sort(folder);
        String comp = folder[0];
        removed.add(comp);
        for(int i = 1; i < folder.length; i++){
            if(!folder[i].startsWith(comp + "/")){
                comp = folder[i];
                removed.add(folder[i]);
            }
        }
        return removed;

    }
}
```

**What the code is doing and why:**\
Initially, my first thought was to use some sort of trie implementation to solve this problem. That turned out to be way too complicated and too much effort for a problem like this, but it took me a while to think of a simpler way to approach this. I knew that prefixes were important but what would we the best way to actually check them. The TA gave us a hint at the end of recitation, saying that if the folder array was sorted, all of the subfolders would strictly come after the original folders, which helped me come up with my actual implementation.
First, I created an ArrayList of String to be the returned list of non-subfolders. Then, I sorted the array of folders and added the first value in the array to list of non-subfolders. This is because the subfolders have to come after the original folders in the sorted array, so the first item can't be a subfolder. I set a reference `comp` that I am using to check if a given folder is a subfolder or not. Initially this is set to the first value.
Then, I iterate through the array of folders, and check if each value starts with the compare string plus a forward slash. This checks if the folder starts with the same path as the original folder, and adding the slash prevents the algorithm from falsely detecting a subfolder in the case of one folder name having the same prefix as another. If the folder is found to not be a sub folder, we change the value of `comp` to that folder, then add that folder to the final list.
Afterwards, `removed` contains all of the non-subfolders from the original list.\
**Runtime and Memory Analysis:**\
The sorting algorithm at the start of the solution runs in `O(n * lg(n))` time, and the actual iteration through the array runs in linear time `O(n)`. This means that in total, we can say that the algorithm runs in `O(n * lg(n))` time, since it is dominated by the sorting at the start.
For space complexity, we create an ArrayList to store the final list of folders to return, and Arrays.sort() requires O(n) auxilliary space because it uses Timsort which is not an in place sorting algorithm. The call to `comp + "/"` does create an extra string object, but it doesn't actually add much space overhead, it's just kind of a minor inefficiency.