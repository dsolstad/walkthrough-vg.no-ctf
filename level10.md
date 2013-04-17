#### Level 10

URL: http://vg.no/ctf/level10-button/

Cool challenge, but very easy. I was expecting more for the final challenge.

The effects that does the animation for the button, does only apply to <button>, by which you can see in the css.

Open Developer Tools in Chrome or use Firebug in Firefox and edit the html.
For Chrome's Developer Tools, goto the elements tab and find the button. Right click and hit "Edit as HTML".
Replace "button" with "input".

From this:
```html
<form method="post" id="a">
    <fieldset>
        <legend>The Button</legend>
        <input type="hidden" name="d">
        <input type="hidden" name="c">
        <button class="move" type="submit">Click me!</button>
    </fieldset>
</form>
```

To this:
```html
<form method="post" id="a">
    <fieldset>
        <legend>The Button</legend>
        <input type="hidden" name="d">
        <input type="hidden" name="c">
        <input class="move" type="submit">Click me!</button>
    </fieldset>
</form>
```

All done!
