#### Level 3

URL: http://vg.no/ctf/level3-youcanhazaccezz/

I used Google Chrome because it has a nice developer feature with lot of useful tools, but I guess Firefox with Firebug will do too.

When you load level 3 an alert show up and tells you that it could not get the url for level 4.

Open Developer Tools by pressing Shift + Ctrl + I, then goto network and find level4.php.

In the headers you will see:
```
Request URL:http://vg.no/ctf/level3-youcanhazaccezz/level4.php
Request Method:GET
Status Code: 405 Method Not Allowed
```

And the response headers show:
```
HTTP/1.1 205 Reset Content
Server: Apache/2.2.22 (Ubuntu)
Allow: DELETE
Location: /ctf/level4-http-verbs/
Content-Type: text/html
Content-Length: 0
Accept-Ranges: bytes
Date: Mon, 15 Apr 2013 19:23:19 GMT
Age: 0
Connection: close
X-Cache: MISS
Vary: Accept-Encoding,User-Agent
X-VG-WebCache: hmg9-varnish-03
X-Age: 0
```

We used the GET method, which was not allowed. The response headers say that we may use the DELETE method, so lets try that.

I made this php script which manually sends a DELETE request to level4.php and fetches the response:
```php
<?php

$fp = fsockopen("www.vg.no", 80, $errno, $errstr, 30);
if (!$fp) {
    echo "$errstr ($errno)<br />\n";
} else {
    $out = "DELETE /ctf/level3-youcanhazaccezz/level4.php HTTP/1.1\r\n";
    $out .= "Host: www.vg.no\r\n";
    $out .= "Connection: Close\r\n\r\n";
    fwrite($fp, $out);
    while (!feof($fp)) {
        echo fgets($fp, 128);
    }
    fclose($fp);
}

?>
```

The output:

```
HTTP/1.1 205 Reset Content
Server: Apache/2.2.22 (Ubuntu)
Allow: DELETE
Location: /ctf/level4-http-verbs/
Content-Type: text/html
Content-Length: 0
Accept-Ranges: bytes
Date: Wed, 17 Apr 2013 07:56:17 GMT
Age: 0
Connection: close
X-Cache: MISS
Vary: Accept-Encoding,User-Agent
X-VG-WebCache: hmg9-varnish-03
X-Age: 0
```

And there we have the url for level 4!

