# Display Wall

## Authors
- Sandip Chitale, sandipchitale

## Description
This is simple Google Chrome Packaged app that lets you generate your own modern art desktop display wall. The idea is to use it as initial display before your main presentation starts. You can reveal only parts of the desktop to peek viewers intrest. Subsequently you can close Display Wall tiles one by one by clicking in the center and revealing the main presentation.

A random tile generation could be used to create a dynamic modern art wall paper for your desktop.

## Link to Prototype

Simply load the

[project_code/DisplayWall](project_code/DisplayWall)

as unpacked extension in Chrome Browser using [these](http://developer.chrome.com/extensions/getstarted#unpacked) instructions.

## Example Code
Here is how the panels are created:
```
var panels = [];
function showPanel(w, h, left, top) {
    var createOptions = {
        'width' : w,
        'minWidth' : w,
        'maxWidth' : w,
        'height' : h,
        'minHeight' : h,
        'maxHeight' : h,
        'frame' : 'none'
    };
    
    if (left) {
        createOptions.left = left;
    }
    if (top) {
        createOptions.top = top;
    }
    
    chrome.app.window.create('panel.html', createOptions, function(panel) {
        panels.push(panel);
        var focusing = false;
        panel.contentWindow.onfocus = function() {
            if (focusing) {
                return;
            }
            focusing = true;
            for (var i = 0; i < panels.length; i++) {
                if (panels[i].contentWindow.CLOSED === true) {
                    var index = panels.indexOf(panels[i]);
                    if(index!=-1){
                       panels.splice(index, 1);
                    }
                } else {
                    panel[i].focus();
                }
            }
            focusing = false;
        }
    });
}
```

The code tow draw the canvas is here:

- [project_code/DisplayWall/panel.html](project_code/DisplayWall/panel.html)
- [project_code/DisplayWall/panel.js](project_code/DisplayWall/panel.js)

## Links to External Libraries
 External libraries not used by this project.

## Images & Videos
NOTE: For additional images you can either use a relative link to an image on this repo or an absolute link to an externally hosted image.

![Display Wall](project_images/cover.jpg?raw=true "Display Wall")
