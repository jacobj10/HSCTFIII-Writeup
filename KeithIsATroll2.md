#Keith Is A Troll 2 - 100
You cracked Keith's last database, but he fixed that. Now he has a login that you really can't get past. Or can you?

```java
package exploit;

import java.util.Scanner;

public class KeithLikesToTroll2 {
	public static void main2(String[] args){
		int key;
		
		Scanner scn = new Scanner(System.in);
		System.out.print("Enter key: ");
		key = scn.nextInt();
		scn.close();
		
		if(24.0 / key * key != 24.0 && key > 0){
			System.out.println("Login succesful. The flag is the smallest key which will let you log in.");
		}else{
			System.out.println("Login rejected.");
		}
	}
}
```

Rewrite it to be:

```java
public class HelloWorld{

    public static void main(String[] args){
		int key=1;
		while (!(24.0 / key * key != 24.0 && key > 0)){
			key+=1;
		}
		System.out.println(key);
	}
}
```
and the output is 47

flag: 47
