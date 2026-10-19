# Lab 5 writeup
## Alexander Mitasev (ajm674)

**Full code solution:**
```
public class LZW {
    private static final int R = 256; // number of input chars
    private static int L = 512; // number of codewords = 2^W
    private static int W = 9; // codeword width

    public static void compress() {
        resetLW();
        String input = BinaryStdIn.readString();
        TST<Integer> st = new TST<Integer>();
        for (int i = 0; i < R; i++)
            st.put("" + (char) i, i);
        int code = R + 1; // R is codeword for EOF

        while (input.length() > 0) {
            String s = st.longestPrefixOf(input); // Find max prefix match s.
            BinaryStdOut.write(st.get(s), W); // Print s's encoding.
            int t = s.length();
            if (t < input.length() && code < L){
                st.put(input.substring(0, t + 1), code++);  // Add s to symbol table.
            }else if(t < input.length() && W < 16){
                updateLW();
                st.put(input.substring(0, t + 1), code++);
            }    
            input = input.substring(t); // Scan past s in input.
        }
        BinaryStdOut.write(R, W);
        BinaryStdOut.close();
    }

    public static void expand() {
        resetLW();
        String[] st = new String[65536];
        int i; // next available codeword value

        // initialize symbol table with all 1-character strings
        for (i = 0; i < R; i++)
            st[i] = "" + (char) i;
        st[i++] = ""; // (unused) lookahead for EOF

        int codeword = BinaryStdIn.readInt(W);
        if (codeword == R)
            return; // expanded message is empty string
        String val = st[codeword];

        while (true) {
            BinaryStdOut.write(val);
            if(i >= L && W < 16){
                updateLW();
            }
            codeword = BinaryStdIn.readInt(W);
            if (codeword == R)
                break;
            String s = st[codeword];
            if (i == codeword)
                s = val + val.charAt(0); // special case hack
            if (i < L){
                st[i++] = val + s.charAt(0);
            }
            val = s;
        }
        BinaryStdOut.close();
    }

    private static void resetLW(){
        L = 512;
        W = 9;
    }

    private static void updateLW(){
        W++;
        L *= 2;
    }
}
```

**What the code is doing and why:**\
To implement the change from fixed width to variable width codewords, I knew that I needed to adjust the width at a certain point in compression, and then adjust the width at the same point in expansion. I adjusted the values of the L and W variables to start at a 9 bit width, and made them not final since they needed to be adjusted. During compression, I checked if the code was less than the length. If the code was equal to the length and the width was less than 16, I adjusted the width and length accordingly. During expansion, since we are a step ahead, we need to check the length before reading in the next value. Before reading in the next value, I check if the current codeword is greater than the length, and if it is, we adjust the length and width accordingly.
**Runtime and Memory Analysis:**\
The changes made don't substantially change the runtime. The runtime for compression and expansion is still $O(n)$. The space is bounded by the maximum size of the codebook, which in our case is 2^16 since we have a maxmimum codeword width of 16 bits. In expansion, we allocate an array of size 65536, which technically isn't the most space efficient option, but it is a marginal increase in space complexity in exchange for removing the runtime overhead of resizing the array.