# Longest-Substring-with-Same-Letters-after-Replacement
Given a string with lowercase letters only, if you are allowed to replace no more than ‘k’ letters with any letter, find the length of the longest substring having the same letters after replacement.


This problem follows the Sliding Window pattern, and we can use a similar dynamic sliding window strategy as discussed in Longest Substring with Distinct Characters. We can use a HashMap to count the frequency of each letter.

We will iterate through the string to add one letter at a time in the window.
We will also keep track of the count of the maximum repeating letter in any window (let’s call it maxRepeatLetterCount).
So, at any time, we know that we do have a window with one letter repeating maxRepeatLetterCount times; this means we should try to replace the remaining letters.
If the remaining letters are less than or equal to ‘k’, we can replace them all.
If we have more than ‘k’ remaining letters, we should shrink the window as we cannot replace more than ‘k’ letters.
While shrinking the window, we don’t need to update maxRepeatLetterCount. Since we are only interested in the longest valid substring, our sliding windows do not have to shrink, even if a window may cover an invalid substring. Either we expand the window by appending a character to the right or we shift the entire window to the right by one. We only expand the window when the frequency of the newly added character exceeds the historical maximum frequency (from a previous window that included a valid substring). In other words, we do not need to know the exact maximum count of the current window. The only thing we need to know is whether the maximum count exceeds the historical maximum count, and that can only happen because of the newly added char.

-------------------------------------------------------------------------------------------------------------------------

// Name: Monisha jain G.N
// Institute: PES
// Qualification: MCA
// YoP: 2023
// Little tricky to understand but this Monisha never gives up easily. However tough it is 
// she tries to give her atleast 90 brain!!! What am I saying? 
// My English haha haha :)      :(

import java.util.*;

class Solution {
  public static int findLength(String s, int k) {
      // TODO: Write your code here
      int start = 0;
      int maxLength = 0;
      int maxRepeatLetterCount = 0;
      int windowLength = 0;

      HashMap<Character, Integer> myMap = new HashMap<>();

      for(int end = 0; end < s.length(); end++) {
        char rightChar = s.charAt(end);
        // hashMap -> character, frequency
        myMap.put(rightChar, myMap.getOrDefault(rightChar, 0) + 1);

        maxRepeatLetterCount = Math.max(maxRepeatLetterCount, myMap.get(rightChar));
        windowLength = end - start + 1;

        if(windowLength - maxRepeatLetterCount > k) {
          char leftChar = s.charAt(start); 
           // leftChar coz we dont want to lose original data
          int currentValue = myMap.get(leftChar);
          myMap.put(leftChar, currentValue - 1);
          // myMap.get(leftChar, myMap.get(leftChar) - 1);
          start++;
        }

        maxLength = Math.max(maxLength, end - start + 1);
      }
      return maxLength;
  }
}
