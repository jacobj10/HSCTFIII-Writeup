#Keith Smash - 100

Keith is planning their big debut at the Super Smash Bros Melee World Tournament! Keith intercepted a program that tells their opponents on which frame to use the legendary Falcon Knee attack, and must figure out the frame so that they can execute a counter! The program can be found here.

Rewrite the program to output what it is comparing.

```JAVA
import java.util.Random;
import java.util.Scanner;


public class PlsHalp {
	public static void main(String[] args) {
		Scanner s = new Scanner(System.in);
		
		int i = s.nextInt();
		args = new String[i];
		for(int x = i-1; x >= 0; x--)
			args[x] = s.nextLine();
		
		String tot = "";
		for(String str: args)
			tot += str;
		
		if(tot.equals("my feet smell and nose runs"))
			System.out.println("Use knee on frame: " + (args[0] + args[2] + args[4] + args[6]).replace(" ", "").hashCode());
	}
}
```
An initial input of 7\n my\n feet\n smell\n and\n nose\n runs\n yields: runsnoseandsmellfeetmy

Rearranging the input to 7\n runs\n nose \n and \n smell \n feet \n my \n

Output is : 

my feet smell and nose runs                                                                                                                                                                                      
Use knee on frame: 1325066802 

flag: 1325066802  
