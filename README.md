# Sum of all substrings of a number
class Solution {
    public int sumSubstrings(String s) {
        int totalSum = 0;
        for (int i = 0; i < s.length(); i++) {
            for (int j = i + 1; j <= s.length(); j++) {
                String substring = s.substring(i, j);
                totalSum += Integer.parseInt(substring);
            }
        }
        return totalSum;
    }
    public static void main(String[] args) {
        String s = "6759";
        Solution ob = new Solution();
        System.out.println("Output: " + ob.sumSubstrings(s)); // Output: 8421
    }
}
