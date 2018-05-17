# Discover-NW
A mobile web application to give travel plan suggestion

## Install
Pull this repo and run

```
npm install
```

## How to run

### Run the app
It is suggested to run this back-end on server and access application on your smart devices through the port number 8080

```
node app.js
```

### Specify the start position and destination
<img src="./demo/demo1.jpg" width="960" height="400" />

* Step1: Click `search` buttton after specifying starting point, destination, spare time, transportation mode.
* Step2&3: When choosing different waypoint types, the app will only give corresponding sets of suggested waypoints. Click the the way points you want to go, and click `route` button to continue.
* Step4: Routing result is displayed. By scrolling you can find `total distance`, `time cost` and `time spare` information to help you get a better understanding on the routing suggested.

## Search scope explanation
* Underlying technique to specify the search scope is drawing an ellipse as searching scope. 
* Since google map API does not natively support drawing an ellipse directly, we set starting point and destination as two focus points (F1 and F2) of ellipse, with an extra parameter to specify the semi-minor axis of ellipse. 

<img src="https://upload.wikimedia.org/wikipedia/commons/9/96/Ellipse-def0.svg" width="300" height="250" /> <img src="./demo/demo2.jpg" width="200" height="280" />

* Using the Parametric Equation of an Ellipse to draw points to form an polygon as an simulation of ellipse.

  ``R(theta) = (a^2 - c^2) / (a - c * sin(theta))``
  
* R is the distance between each point on ellpise and center (the midpoint of F1 and F2). Checking if a candidate is within the ellipse can be done by compare the distance to center with R.

