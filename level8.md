#### Level 8

URL: http://vg.no/ctf/level8-qr/

If we look at the source code of the QR table you will see that the data-row and data-col numbers doesn't match with the position in the table.
The task is simple, just rearrange the order of the cells.

I made this ugly javascript which does the job. Open the console tab in Chrome again and copy paste this:

```javascript
/* Create 2d array */
var cells = []
for (var i=0 ; i < 21; i++) {
     cells[i] = [];
}

/* Get all cells and store them in the array. */
$("table td").not(document.getElementById('playground')).each(function() {
    $this = $(this)
    var row = $this.attr("data-row");
    var col = $this.attr("data-col");
    var color = $this.attr("class");
    cells[row][col] = (color != undefined? 1 : 0);
});

/* Add them sorted back to the playground table. */
for (var i = 0; i < 21; i++) {
    var tr = $("<tr></tr>").appendTo($("#playground"));
    for (var j = 0; j < 21; j++) {
        color = (cells[i][j]? "dark" : "");
        $("<td class=" + color + "></td>").appendTo(tr);
    }
}

/* Add some space */
$("#playground").css("margin-top", "50px");
```

Open a QR scanner app on your smartphone and you will get this plain text: `account`

If you don't have php on your computer, just goto codepad.org, hit php and paste:
```php
<?php
echo md5("account");
?>
```

The output: `e268443e43d93dab7ebef303bbe9642f`

