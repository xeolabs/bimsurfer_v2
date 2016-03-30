<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [Introduction](#introduction)
- [Usage](#usage)
  - [BIMSurfer](#bimsurfer)
  - [Objects](#objects)
    - [Selecting and deselecting objects](#selecting-and-deselecting-objects)
    - [Showing and hiding objects](#showing-and-hiding-objects)
    - [Changing the color and transparency of objects](#changing-the-color-and-transparency-of-objects)
    - [Clearing objects](#clearing-objects)
  - [Camera](#camera)
    - [Controlling the camera](#controlling-the-camera)
    - [Flying the camera to objects](#flying-the-camera-to-objects)
    - [Camera interaction](#camera-interaction)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Introduction

BIMSurfer is a WebGL-based 3D viewer for [BIMServer]() that's built on [xeoEngine](http://xeoengine.org).
     
# Usage

## BIMSurfer

Creating a [BIMSurfer](bimsurfer/src/BimSurfer.js): 

````javascript
var bimSurfer = new BimSurfer({
    domNode: "viewerContainer"
});
````

Loading a model from BIMServer:
 
````javascript
bimSurfer.load({
        bimserver: ADDRESS,
        username: USERNAME,
        password: PASSWORD,
        poid: 131073,
        roid: 65539,
        schema: "ifc2x3tc1" // < TODO: Deduce automatically
    })
        .then(function (model) {
        
                // Model is now loaded and rendering.
                // The following sections show what you can do with BIMSurfer at this point.
                //...
            });
````

## Objects

### Selecting and deselecting objects

TODO:  

### Showing and hiding objects

Hiding three objects by ID:

````javascript
bimSurfer.setVisibility({ids: ["object3", "object1", "object6"], visible: false });
````

Setting two objects visible by ID:

````javascript
bimSurfer.setVisibility({ids: ["object1", "object6"], visible: true });
````

Hiding all objects of IFC types "IfcSlab" and "IfcWall":

````javascript
bimSurfer.setVisibility({ids: ["IfcSlab", "IfcWall"], visible: false });
````

### Changing the color and transparency of objects

Making two objects pink:

````javascript
bimSurfer.setColor({ids: ["object3", "object6"], color: [1, 0, 1] })
````

An optional fourth element may be specified in the color to set opacity: 

````javascript
bimSurfer.setColor({ids: ["object3", "object6"], color: [1, 0, 1, 0.5] })
````


### Clearing objects
 
TODO

## Camera
  
### Controlling the camera

Setting the camera position:

````javascript
bimSurfer.setCamera({ 
    eye: [-20,0,20],
    target: [0,10,0],
    up: [0,1,0]
});
````

Setting the camera projection to orthographic:

````javascript
bimSurfer.setCamera({ 
    type:"ortho"
});
````

Setting the view volume size for orthographic, switching to orthographic projection first if necessary:

````javascript
bimSurfer.setCamera({ 
    type:"ortho", 
    scale: [10,10,10]
});
````

Setting the camera projection to perspective:

````javascript
bimSurfer.setCamera({ 
    type:"persp"
});
````

Setting the FOV on Y-axis for perspective, switching to perspective projection first if necessary:

````javascript
bimSurfer.setCamera({ 
    type:"persp", 
    fovy: 65
});
````

Querying camera state:

````javascript
var camera = bimSurfer.getCamera();
````

The returned value would be:

````json
{
    "type": "persp",
    "eye": [-20,0,20],
    "target": [0,10,0],
    "up": [0,1,0],
    "fovy": 65
}
````
 
### Flying the camera to objects

Flying the camera to fit specified objects in view:

````javascript
bimSurfer.viewFit({ids: ["object3", "object1", "object6"], animate: true });
````

Jumping the camera to fit specified objects in view:

````javascript
bimSurfer.viewFit({ids: ["object1", "object6"], animate: false });
````

Flying the camera to fit all objects in view:

````javascript
bimSurfer.viewFit({ animate: true });
````
 

