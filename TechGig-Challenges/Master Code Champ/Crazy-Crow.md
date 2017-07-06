# Problem:
There are N pots. Every pots have some water in it. They may be partially filled. So there is a Overflow
Number O associated with every pot which tell how many minimum stone pieces are require for that pot to
overflow. So if for a pot O-value is 5 it means minimum 5 stone pieces should be put in that pot to make it
overflow. Initially a crow watched those pots and by seeing the water level he anticipated O-value correctly
for every pot ( that is he knew O1 to On). But when he came back in evening he found that every pot is
painted from outside and he is not able to know which pot has what O-value. Crow wants some K pots to
overflow so that he can serve his child appropriately. For overflow of pots he need to search for stone in
forest( assume that every stone has same size). He wants to use minimum number of stones required to
overflow K pots. But only he know the O-value of pots he doesn't know now which pot has what O-value. So
the task is that in what minimum number of stones he can make K pots overflow in worst case.

Input Format:

You will be given a function which contains an integer array O corresponding to O-value of N pots {O1, O2,
....... , On} and a K - Value representing the number of pots which the crow wants to overflow
Output Format:
You need to return the Minimum number of stones(in the form of integer) required to make K pots overflow
in worst case. If input is invalid, return -1.
Sample Test Case :
Sample Input:
2
5
58
1
Sample Output:
10

Explanation:
Let say there are two pots
pot 1 has O value of 5 , O1= 5
pot 2 has O value of 58, O2= 58
Let say crow wants to make one of the pot​ to overflow. If he know which pot has what O-value he would
simple search for 5 stones and put then in pot 1 to make it overflow. But in real case he doesn't know which
pot has what O-value so just 5 stones may not always work. However he does know that one pot has
O-value 5 and other has 58. So even in worst case he can make one of the pot overflow just by using 10
stones. He would put 5 stones in one pot if it doesn't overflow he would try the remaining 5 in the other pot
which would definitely overflow because one of the pot has O-value of 5. So the answer for above question
is minimum 10 stones even in worst case.


# Solution:


```sh
import java.io.*;
import java.util.*;
import java.text.*;
import java.math.*;
import java.util.regex.*;
public class CandidateCode {
    /*
     * Complete the function below.
    */
    
public static int ThirstyCrowProblem(int[] input1,int input3) {
		int n = input1.length;
		int k = input3;
		int tempk = 0;

		if(input1 == null || k < 0 || k > input1.length || n <= 0 || input1.length != n) {
			return -1;
		}

		if(k==0) {
			return 0;
		}

		for(int i = 0; i < n; i++) {
			if(input1[i] < 0) {
				return -1;
			} else if (input1[i] == 0) {
				if(++tempk==k) {
					return 0;
				}
			}
		}
		Arrays.sort(input1);
		return minStones(input1,k-tempk,tempk);
	}
    public static int minStones(int[] input, int k, int start) {
    	 List<Integer> minStones = new ArrayList<Integer>();
         minStones.add(Integer.MAX_VALUE);
         minStones(input,k,start,0,minStones);
         return minStones.get(0);
    }
    public static void minStones(int[] input, int k,int start, int stones, List<Integer> minStns) {

      if(k==0) {
          if(stones < minStns.get(0)) {
              minStns.set(0, stones);
          }
          return;
      }

      int[] clone = null;
      for(int i = start; i <= input.length-1-(k-1);i++) {
          if(input[i] == 0) {
              continue;
          }
          clone = input.clone();
          //change clone
          int stns = 0;
          int tempk = 0;
          for(int j = clone.length-1; j >= i;j--) {
              if(clone[j] == 0) {
                  continue;
              }
              if(clone[j] <= clone[i]) {
                  stns+=clone[j];
                  clone[j] = 0;
                  if(++tempk == k) {
                	  break;
                  } else {
                	  continue;
                  }
              }
              stns+=clone[i];
              clone[j] -= clone[i];
          }
          minStones(clone,k-tempk,i,stones+stns,minStns);
      }
    }

    public static void main(String[] args) throws IOException{
        Scanner in = new Scanner(System.in);
        int output = 0;
        int ip1_size = 0;
        ip1_size = Integer.parseInt(in.nextLine().trim());
        int[] ip1 = new int[ip1_size];
        int ip1_item;
        for(int ip1_i = 0; ip1_i < ip1_size; ip1_i++) {
            ip1_item = Integer.parseInt(in.nextLine().trim());
            ip1[ip1_i] = ip1_item;
        }
        int ip2 = Integer.parseInt(in.nextLine().trim());
        output = ThirstyCrowProblem(ip1,ip2);
        System.out.println(String.valueOf(output));
    }
}

```

# Result

[![N|Solid](https://cdn.rawgit.com/jaideepghosh/Coding-Challenges/c4fedd8a/TechGig-Challenges/Master%20Code%20Champ/Techgig%20-%20Master%20Code%20Champ%20-%20Crazy%20Crow%20(Thrusty%20Crow).jpg)](https://jaideepghosh.blogspot.in)
