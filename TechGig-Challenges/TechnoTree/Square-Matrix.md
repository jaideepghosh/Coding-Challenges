# Problem: 
Given a square matrix of alphabets which contain English letters in arbitrary manner. While searching a word in it, you can go left to right horizontally, vertically downwards or diagonally towards left (both upwards and downwards).
 
You have to find the number of matches of a given word in the matrix.

For example, In the given square matrix {A#A#K,A#S#K,A#K#K},

[![N|Solid](http://www.techgig.com/files/nicUploads/662429267307743.jpg)](https://jaideepghosh.blogspot.in)

The word "ASK"  is matched four times in the input matrix. So the output will be 4.

Input Format 

i)  An array of string {N strings containing N uppercase alphabets separated by #} 
ii) String (Word to be searched)  

Output Format
Number of occurrences of the word in the matrix {an integer} 

Sample Test case 1 
------------------

Sample Input

2

A#S

S#T

AS

Sample Output

2

==================
Sample Test case 2
------------------

Sample Input

5

E#D#E#E#E

D#I#S#K#E

E#S#E#E#E

E#C#E#E#E

E#E#E#E#E 

DISK

Sample Output:

1

Explanation 
In this example, "DISK"  is matched only one time in the input matrix. So the output will be 1.

# Solution:

```sh
import java.io.IOException;
import java.util.Scanner;

public class CandidateCode {
	public static int word_count(String[] matrixSet, String word) {
                int matRowCount=matrixSet.length;;
		int r = 0;
		StringBuilder diagonal1 = new StringBuilder("");
		StringBuilder diagonal2 = new StringBuilder("");
		StringBuilder[] input = new StringBuilder[matrixSet.length];
		StringBuilder[] column = new StringBuilder[matrixSet.length];
                
		for (int i = 0; i < matrixSet.length; i++) {
			input[i]=new StringBuilder();
			matrixSet[i]=matrixSet[i].replace("#", "");
			input[i].append(matrixSet[i]);
                        
			r += getOccurenceCount(matrixSet[i],word);
                        
			r += getOccurenceCount(input[i].reverse().toString(),word);
			diagonal1.append(matrixSet[i].charAt(i));
			diagonal2.append(matrixSet[i].charAt(matRowCount - i - 1));
			
			for (int j = 0; j < matRowCount; j++) {
				if (column[j] == null) {
					column[j] = new StringBuilder();					
				}
				column[j].append(matrixSet[i].charAt(j));
			}
		}
		r += getOccurenceCount(diagonal1.toString(),word);		
		r += getOccurenceCount(diagonal1.reverse().toString(),word);
		r += getOccurenceCount(diagonal2.toString(),word);		
		r += getOccurenceCount(diagonal2.reverse().toString(),word);		
		
		for (int i = 0; i < matRowCount; i++) {
                    
			r += getOccurenceCount(column[i].toString(),word);
			r += getOccurenceCount(column[i].reverse().toString(),word);
                        
		}
		return r;
	}
        
	private static int getOccurenceCount(String string, String word) {	
		return (string.length() - string.replace(word, "").length())/word.length();
		
	}
        

    public static void main(String[] args) throws IOException{
        Scanner in = new Scanner(System.in);
        int output = 0;
        int ip1_size = 0;
        ip1_size = Integer.parseInt(in.nextLine().trim());
        String[] ip1 = new String[ip1_size];
        String ip1_item;
        for(int ip1_i = 0; ip1_i < ip1_size; ip1_i++) {
            try {
        ip1_item = in.nextLine();
            } catch (Exception e) {
        ip1_item = null;
            }
            ip1[ip1_i] = ip1_item;
        }
        String ip2 = in.nextLine().trim();
        output = word_count(ip1,ip2);
        System.out.println(String.valueOf(output));
    }
}

```
