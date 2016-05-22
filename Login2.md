#Login 2 - 100
Help Keith login to a super secure website!

ctf.1e100.io/login2/

```JS
$(document).ready(function(){
        $("#login").submit(function(e){
            e.preventDefault();

            var username = $("#username").val();
            var password = $("#password").val();

            if(username == "admin" && md5(password) == "d5aa1729c8c253e5d917a5264855eab8") {
                document.location = "success.php?password=" + password;
            } else {
                alert("Incorrect username and password!");
            }

        });
    });
``` 
Cracking the MD5 Hash on any hash cracking website reveals the password to be freedom

Entering with username admin and password freedom returns

The flag is super_secure_javascript_login_with_md5_support

flag: super_secure_javascript_login_with_md5_support


