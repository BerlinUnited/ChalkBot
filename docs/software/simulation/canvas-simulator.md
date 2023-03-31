Since we learned how to use the simulator, I want to explain to you how the simulator and canvas work in the background.
When you draw a line in the drawing area several small blue arrows (as seen in the picture below) are created on that line. 

![Drawing in canvas](../../img/canvas-simulation/drawingCanvas.png)

The x and y coordinates of these are stored in an array and get sent to the simulator or real life ChalkBot when you hit SEND. ChalkBot will then drive along those points and print the line. Every line you draw in the canvas is scaled by 10 to the real world. If you want to change if the simulator or ChalkBot should receive the coordinates, open CanvasServer.py in the canvas directory and move the hash from one to the other. The scaling is also changeable in this function.

```javascript
def sendToRobot(self, coordinates):
    chalkbot = ChalkBotHTTPClient("127.0.0.1:8000")
    #chalkbot = ChalkBot("10.0.4.99")
    
    scale = 10.0
```

SAVE TO FILE uses the same array of coordinates and just saves them to a file, the name of the file can be also changed in CanvasServer.py in the do_Post function as seen below.

```javascript
if save_to_file:
    file = open("coords.json", "w")
    file.write(json.dumps(msg))
    file.close()
```

CLEAR CANVAS removes all drawn lines by using the clearRect function by the canvas API, it also resets the array with the coordinates, because they would still be stored in the array otherwise after removing the drawn lines.

```javascript
function clearCanvas() {
    var canvas = document.getElementById("canvas");
    var context = canvas.getContext("2d");
    context.clearRect(0, 0, canvas.width, canvas.height);
    strokes=[];
}
```

The scaling of the drawing area is done by the following code.

```javascript
function scaleCanvas() {
    var pct = Number(document.getElementById("scale").value);
    var myCanvas=document.getElementById("canvas");
    var ctx=myCanvas.getContext("2d");
    var cw=canvas.width;
    var ch=canvas.height;
    var tempCanvas=document.createElement("canvas");
    var tctx=tempCanvas.getContext("2d");
    var cw=canvas.width;
    var ch=canvas.height;
    tempCanvas.width=cw;
    tempCanvas.height=ch;
    tctx.drawImage(canvas,0,0);
    canvas.width*=pct;
    canvas.height*=pct;
    var ctx=canvas.getContext('2d');
    ctx.drawImage(tempCanvas,0,0,cw,ch,0,0,cw*pct,ch*pct);
}
```

We just create a second canvas element and just copy all parameters from the previous canvas and then scale the height and width by the given value. The scale by button is implemented like this:

```html
<form>
    Scale by: <input type="number" step="0.01" min="0" max="10" name="scale" id="scale" value="0.75"><br>
    <input type='button' id='btnScale' value='Scale' onclick='scaleCanvas();'>
</form>
```

To load the saved file, we need to filter out the coordinates, that's done with the following code that removes all characters that are not important to draw the saved lines. 

```javascript
file = input.files[0];
fr = new FileReader();
fr.onload = receivedText;
fr.readAsText(file);

function receivedText(e) {
    var lines = e.target.result;   
    lines = lines.substring(11);
                
    var drawing = [];
    var drawingtemp = [];
    var temp = [];
    var numbertemp=""; 

    for(let i = 0; i < lines.length; i++) {

        if (lines[i] == ']' && temp!="") {
            drawingtemp.push(temp);
            temp=[];
        }
                    
        if(lines[i] == '0' || lines[i] == '1' || lines[i] == '2' || lines[i] == '3' || lines[i] == '4' ||
            lines[i] == '5' || lines[i] == '6' || lines[i] == '7' || lines[i] == '8' || lines[i] == '9') { 
            numbertemp+=lines[i];  
            if((lines[i+1] ==',' || lines[i+1] ==']' ) && numbertemp!="" ) {
                temp.push(parseInt(numbertemp)); 
                numbertemp="";
            }
        }  
    }
    drawing.push(drawingtemp);  
    sendJSON(
        {
            "coords": drawing,
            "file": false
        }); 
                
}
```

Now the coordinates are just sent to the simulator in the same way they would have been if you drew the line in the drawing area.
