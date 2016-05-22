#Keith Is A Troll - 100
Ha! Keith likes to troll, and now he's trolling you! He has written a login that he says is impossible to get into. Can you prove him wrong?

The login is as follows:

```java
package exploit;

import java.util.Scanner;

public class KeithLikesToTroll {
	public static void main(String[] args){
		int key;
		
		Scanner scn = new Scanner(System.in);
		System.out.print("Enter key: ");
		key = scn.nextInt();
		scn.close();
		
		if(1338557220 / key * key != 1338557220 && key > 0){
			System.out.println("Login succesful. The flag is the smallest key which will let you log in.");
		}else{
			System.out.println("Login rejected.");
		}
	}
}
```

Simple, just write the following script to get the smallest output:


```java
public class HelloWorld{

    public static void main(String[] args){
		int key=1;
		while (!(1338557220 / key * key != 1338557220 && key > 0)){
			key+=1;
		}
		System.out.println(key);
	}
}
```
The output is 8

flag: 8
