#### Level 1

URL: http://vg.no/ctf/level1/

Just view the source and you will see this javascript:

```javascript
(function(d) {
    var login = d.getElementById('login');
    login.addEventListener('submit', function(e) {
        e.preventDefault();
        if (login.username.value == 'secure' && login.password.value == 'enough') {
            location.href = '../level2-secureenough/';
        } else {
            alert('Sorry, wrong username or password!');
        }
    });
})(document);
```

As you may guess, the username is "secure" and the password is "enough".
