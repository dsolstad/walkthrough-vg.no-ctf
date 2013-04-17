#### Level 9

URL: http://vg.no/ctf/level9-math/

If we look in the source code, we find instructions to what we need to do. 
Basicaly we send a request for a random math equation, we solve it and send it back. 
This goes on until we get the URL for the next challenge.

Not always do we get clean math equations from the site. They add empeded youtube videoes of Rick Roll, 
alerts, makes the site content blink and other irritating stuff in the equations, which we need to filter out.

The comments in the code will explain everything step by step.

Just run the code in the javascript console in your browser.

```javascript
/* This will generate a random number that will be used to get a random math equation. */
var taskId = Math.floor(Math.random() * 10000);
/* This is the number to keep track of how many math equations we have done. */
var taskNum = 0;
/* This is the answer of the equations and the response from the site. */
var ans, response = '';

/* First we do the initial request to get the ball going. */
$.post('task.php?taskId=' + taskId, function(data) {
    /* I want to keep an updated response globaly for later use. */
    response = new String(data);
    
    /* Match and extract the numbers and math operators */
    math = data.match(/(\d+)(.)(\d+)(.)(\d+);/);
    
    /* Evaluates the equation */
    ans = eval(math[1] + math[2] + math[3] + math[4] + math[5]);
    
    /* 
    This function sends requests and evaluates the math expression in the response forever, 
    until we get an URL to vg.no for the next challenge.
    Ajax is done async, so I added a little time delay of one second so it doesn't screw up something 
    */
    function request() {
        $.post('task.php?taskId=' + taskId + '&taskNum=' + taskNum + '&result=' + ans, function(data) {
            response = new String(data);
            math = data.match(/(\d+)(.)(\d+)(.)(\d+);/);
            ans = eval(math[1] + math[2] + math[3] + math[4] + math[5]);
            
            console.log("Data: " + data);
            console.log("Ans: " + ans);
            console.log("Response: " + response);
        });
        
        /* Look for url to next challenge */
        if (response.indexOf('vg.no') != -1) {
            alert(response);
        }
        taskNum++;
    }
    
    window.setInterval(request, 1000);
});
```

The code will produce something like this:
```
...
Ans: -1674.7717943507416
Response: 2246/9842-1675;window;alert('WELL HELLO THAR');;
Data: 486-9354*2395;
Ans: -22402344
Response: 486-9354*2395;
Data: http://vg.no/ctf/level10-button/
```

And there we go. 
