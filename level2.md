#### Level 2

URL: http://vg.no/ctf/level2-secureenough/

View the source again and meet this javascript:

```javascript
(function(d) {
    var login = d.getElementById('login');

    login.addEventListener('submit', function(e) {
        e.preventDefault();
        var secret = login.secret.value.toLowerCase(),
            level3 = '';

        for (var i = 0; i < secret.length; i++) {
            level3 += '' + secret.charCodeAt(i);
        }

        if (level3 == "121111117999711010497122979999101122122") {
            location.href = '../level3-' + secret + '/';
        } else {
            alert('Sorry, wrong secret!');
        }
    });
})(document);
```

Don't bother try "121111117999711010497122979999101122122" as the password, because it's not.

So what can we gather from this javascript?
The password is lower case:
```var secret = login.secret.value.toLowerCase()```
Each character you write as password will be converted to ascii decimal:
```
for (var i = 0; i < secret.length; i++) {
    level3 += '' + secret.charCodeAt(i);
}
```

Because lower case characters begin at 97, then we can separate the numbers like this:
121 111 117 99 97 110 104 97 122 97 99 99 101 122 122

Here is a php script that reverses what the javascript does by converting the ascii numbers to characters:
```php
<?php
foreach(explode(" ", "121 111 117 99 97 110 104 97 122 97 99 99 101 122 122") as $s) {
    print chr($s);
}
?>
```

Output:
`youcanhazaccezz`
