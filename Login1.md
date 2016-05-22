#Login 1 - 100
Help Keith login to a super secure website!

http://ctf.1e100.io/login1/

A peek at the source reveals the following JS.

```Javascript
$(document).ready(function(){
        $("#login").submit(function(e){
            e.preventDefault();

            var username = $("#username").val();
            var password = $("#password").val();

            if(username == "admin" && password == "supersecure") {
                document.location = "success.php";
            } else {
                alert("Incorrect username and password!");
            }

        });
```

