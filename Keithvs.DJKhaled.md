#Keith vs DJ Khaled - 100
Keith is rap-battling DJ Khaled, and is losing badly. However, DJ Khlaed has accidentally given Keith his one lyrical weakness in the form of code, which - if used against him - will cause DJ Khaled to disintegrate into a pile of cash and diamonds. Help Keith figure out what to say to win!


The following Java file is given:

```Java
import java.util.Base64;
import java.util.Scanner;

public class Reversing {
    public static String confuse(String w) {
        String string = "";
        String[] bits = w.split("");
        for(int i = 0; i < bits.length; i++) {
            char y = bits[i].charAt(0);
            y = (char)(Math.pow(y, 2) / 120);
            bits[i] = y + "";
            string += bits[i];
        }
        return string;
    }

    public static String confuse2(String w) {
        byte[] b = w.getBytes();
        return Base64.getEncoder().encodeToString(b);
    }

    public static void check(String key) {
        String ans = confuse2(confuse(key));
        if(!ans.equals("TmRmcFpVbEtmZFU=")) {
            System.out.println("DJ Khaled is not impressed.");
        }
        else {
            System.out.println("You have achieved the key to success! The flag is '" + key + "'");
        }
    }

    public static void main(String[]args) {
        Scanner k = new Scanner(System.in);
        String ans = k.nextLine();
        check(ans);
    }
}
```

In the Check function ans=confuse2(confuse(key)) and this is compared to what B64 decodes to NdfpZUlKfdU. Since Confuse2 simply Base64 encodes it, Confuse must equal the string.

Confuse simply squares the character value and divides it by 120. Writing a reverse program like :

```Java
import java.util.Base64;
import java.util.Scanner;

public class HelloWorld {
    public static String confuse(String w) {
        String string = "";
        String[] bits = w.split("");
        for(int i = 0; i < bits.length; i++) {
            char y = bits[i].charAt(0);
            y = (char)(Math.pow(y*120, .5)+1);
            
            bits[i] = y + "";
            string += bits[i];
        }
        System.out.println(string);
        return string;
    }

    public static String confuse2(String w) {
        byte[] b = w.getBytes();
        return Base64.getEncoder().encodeToString(b);
    }

    public static void check(String key) {
        String ans = confuse2(confuse(key));
    }

    public static void main(String[]args) {
        String ans = "NdfpZUlKfdU";
        check(ans);
    }
}
```
Reveals the flag.

flag: another_one
