#### Level 6

URL: http://vg.no/ctf/level6-canvas/

We need to sum up the RGB values of this picture: http://www.vg.no/ctf/gfx/vg-logo.png

Open the developer tools in Chrome and go to the console tab and enter this code, which is pretty straight forward:

```javascript
sum = 0;
c = window.VG.canvasContext;
h = c.canvas.attributes.height.value;
w = c.canvas.attributes.width.value;

for (var y = 0; y < h; ++y) {
    for (var x = 0; x < w; ++x) {
        var r = c.getImageData(x, y, 1, 1).data[0];
        var g = c.getImageData(x, y, 1, 1).data[1];
        var b = c.getImageData(x, y, 1, 1).data[2];
        sum += (r+g+b);
    }
}

console.log(sum);
```

This will output: `3558452`
