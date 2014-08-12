Full Tilt JS
============

#### The standalone device orientation sensor library ####

Full Tilt JS is a standalone JavaScript library that allows developers to use device orientation sensor data in web applications in a consistent frame.

This library takes device orientation data and applies a consistent calibration frame to the data output. It also automatically normalizes device orientation data based on the current screen orientation so your applications keep working as users rotate their screen during web application usage.

Full Tilt JS ultimately provides developers with three different but complimentary device orientation sensor output representations – screen-adjusted Quaternions, Rotation Matrixes and Euler Angles – that can be used to create 2D or 3D experiences in web browsers that work consistently across all mobile web platforms and in all screen orientations.

* [Live Demo](http://richtr.github.io/Full-Tilt-JS/examples/vr_test.html)
* [Basic Usage](#basic-usage)
* [API](#api)
* [Reference Material](#reference-material)
* [License](#license)

## Basic Usage ##

Add [fulltilt.js](https://github.com/richtr/Full-Tilt-JS/blob/master/fulltilt.js) (or the [minified version of fulltilt.js](https://github.com/richtr/Full-Tilt-JS/blob/master/fulltilt.min.js)) to your project:

    <script src="fulltilt.js"></script>

Start listening for device orientation sensor changes by calling `FULLTILT.DeviceOrientation.start()` at the appropriate point in your web application:

    // Start listening for raw device orientation event changes
    FULLTILT.DeviceOrientation.start();

Whenever you need to obtain the current device orientation, call the appropriate method depending on the rotation representation you would like to use:

    // Obtain the screen-adjusted normalized rotation as a Quaternion
    var quaternion = FULLTILT.DeviceOrientation.getDeviceQuaternion();

    // Obtain the screen-adjusted normalized rotation as a Rotation Matrix
    var rotmat = FULLTILT.DeviceOrientation.getDeviceRotation();

    // Obtain the screen-adjusted normalized rotation as Tait-Bryan Angles
    var euler = FULLTILT.DeviceOrientation.getDeviceEuler();

At any time you can stop listening for device orientation sensor changes in your web application by calling `FULLTILT.DeviceOrientation.stop()`:

    // Stop listening for raw device orientation event changes
    FULLTILT.DeviceOrientation.stop();

A full example of usage can be found in the [provided example](https://github.com/richtr/Full-Tilt-JS/blob/master/examples/vr_test.html) ([view the example live here](http://richtr.github.io/Full-Tilt-JS/examples/vr_test.html)).

## API ##

### FULLTILT.DeviceOrientation ###

#### Methods ####

##### FULLTILT.DeviceOrientation.start() #####

Start the controller and register all required device orientation event listeners

Example:

    FULLTILT.DeviceOrientation.start();

##### FULLTILT.DeviceOrientation.stop() #####

Stop the controller and de-register all required device orientation event listeners

Example:

    FULLTILT.DeviceOrientation.stop();

##### FULLTILT.DeviceOrientation.getDeviceQuaternion() #####

Return the last available device orientation as a screen-adjusted Quaternion

Example:

    // Return an object of type FULLTILT.Quaternion
    var quat = FULLTILT.DeviceOrientation.getDeviceQuaternion();

##### FULLTILT.DeviceOrientation.getDeviceRotation() #####

Return the last available device orientation as a screen-adjusted Rotation Matrix

Example:

    // Return an object of type FULLTILT.RotationMatrix
    var rotmat = FULLTILT.DeviceOrientation.getDeviceRotation();

##### FULLTILT.DeviceOrientation.getDeviceEuler() #####

Return the last available device orientation as screen-adjusted Euler Angles

Example:

    // Return an object of type FULLTILT.Euler
    var angles = FULLTILT.DeviceOrientation.getDeviceEuler();

##### FULLTILT.DeviceOrientation.isAbsolute() #####

Returns `true` if the device orientation is reporting to be compass-orientated otherwise return `false` to suggest that the device orientation returned is arbitrarily (non-compass) oriented.

At present iOS device orientation should always return `false` while Android device orientation should always return `true`.

Example:

    // Check if the data is aligned to a real-world compass bearing
    var isCompassOriented = FULLTILT.DeviceOrientation.isAbsolute();

##### FULLTILT.DeviceOrientation.getRawDeviceOrientationData() #####

Return the last available original (unprocessed, non-screen-adjusted) device orientation event data provided by the web browser.

Example:

    // Return the original raw deviceorientation event object
    var deviceOrientationEvent = FULLTILT.DeviceOrientation.getRawDeviceOrientationData();

### FULLTILT.Quaternion ###

#### Constructor ####

##### new FULLTILT.Quaternion( [x], [y], [z], [w] ) #####

Create a new `FULLTILT.Quaternion` object.

Arguments:

* `x` - the initial x component (optional)
* `y` - the initial y component (optional)
* `z` - the initial z component (optional)
* `w` - the initial w component (optional)

Returns:

A new [`FULLTILT.Quaternion`](#fulltiltquaternion) object.

Example:

    // Create a new FULLTILT.Quaternion object
    var quat = new FULLTILT.Quaternion( 0, 0, 0, 1 );

#### Properties ####

##### .x #####

##### .y #####

##### .z #####

##### .w #####

#### Methods ####

##### .set( [x], [y], [z], [w] ) this #####

Sets the value of this quaternion.

##### .copy( [quat](#fulltiltquaternion) ) this` #####

Copies the value of the supplied quaternion.

##### .multiply( [quat](#fulltiltquaternion) ) this` #####

Multiplies the current object quaternion by the supplied quaternion.

##### .rotateX( angle ) this` #####

Rotate the current object quaternion around its x-axis by the supplied angle (in Radians).

##### .rotateY( angle ) this` #####

Rotate the current object quaternion around its y-axis by the supplied angle (in Radians).

##### .rotateZ( angle ) this` #####

Rotate the current object quaternion around its z-axis by the supplied angle (in Radians).

### FULLTILT.RotationMatrix ###

#### Constructor ####

##### new FULLTILT.RotationMatrix( [m11, m12, m13, m21, m22, m23, m31, m32, m33] ) #####

Create a new `FULLTILT.RotationMatrix` object.

Arguments:

The matrix component values to initially set for the object (optional).

Returns:

A new [`FULLTILT.RotationMatrix`](#fulltiltrotationmatrix) object.

Example:

    // Create a new FULLTILT.RotationMatrix object
    var rotmat = new FULLTILT.RotationMatrix( 1, 0, 0, 0, 1, 0, 0, 0, 1 );

#### Properties ####

##### .elements #####

A ByteArray containing the 9 values of the rotation matrix

#### Methods ####

##### .set( m11, m12, m13, m21, m22, m23, m31, m32, m33 ) this #####

Sets the component values of this rotation matrix object.

##### .copy( [rotmat](#fulltiltrotationmatrix) ) this` #####

Copies the component values of the supplied rotation matrix.

##### .multiply( [rotmat](#fulltiltrotationmatrix) ) this` #####

Multiplies the current object rotation matrix by the supplied rotation matrix.

##### .rotateX( angle ) this` #####

Rotate the current object rotation matrix around its x-axis by the supplied angle (in Radians).

##### .rotateY( angle ) this` #####

Rotate the current object rotation matrix around its y-axis by the supplied angle (in Radians).

##### .rotateZ( angle ) this` #####

Rotate the current object rotation matrix around its z-axis by the supplied angle (in Radians).


### FULLTILT.Euler ###

#### Constructor ####

##### new FULLTILT.Euler( [alpha], [beta], [gamma] ) #####

Create a new `FULLTILT.Euler` object.

Arguments:

* `alpha` - the initial z-axis rotation in Degrees (optional)
* `beta`  - the initial x-axis rotation in Degrees (optional)
* `gamma` - the initial y-axis rotation in Degrees (optional)

Returns:

A new [`FULLTILT.Euler`](#fulltilteuler) object.

Example:

    // Create a new FULLTILT.Euler object
    var euler = new FULLTILT.Euler( 0, 0, 0 );

#### Properties ####

##### .alpha #####

The computed rotation around the z-axis (in Degrees).

##### .beta #####

The computed rotation around the x-axis (in Degrees).

##### .gamma #####

The computed rotation around the y-axis (in Degrees).

#### Methods ####

##### .set( alpha, beta, gamma ) this #####

Sets the component values of this Euler object.

##### .copy( [euler](#fulltilteuler) ) this` #####

Copies the component values of the supplied Euler object.

##### .rotateX( angle ) this` #####

Rotate the current object Euler angles around its x-axis by the supplied angle (in Radians).

##### .rotateY( angle ) this` #####

Rotate the current object Euler angles around its y-axis by the supplied angle (in Radians).

##### .rotateZ( angle ) this` #####

Rotate the current object Euler angles around its z-axis by the supplied angle (in Radians).

## Reference Material ##

* Article: [Practical application and usage of the W3C Device Orientation API](http://dev.opera.com/articles/view/w3c-device-orientation-usage/)
* [W3C Spec](http://w3c.github.io/deviceorientation/spec-source-orientation.html)

## License ##

MIT. Copyright (c) Rich Tibbett
