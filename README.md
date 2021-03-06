#glslViewer

![](http://patriciogonzalezvivo.com/images/glslViewer.gif)

[![Donate](https://www.paypalobjects.com/en_US/i/btn/btn_donate_SM.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=4BQMKQJDQ9XH6)

Live-coding console tool that renders GLSL Shaders. Every file you use (frag/vert shader, images and geometries) are watched for modification, so they can be updated on the fly.

## Install

### Installing in Ubuntu

You need to [install GLFW](http://www.glfw.org/docs/latest/compile.html#compile_deps_x11) then download the code, compile and install. 

```
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install git-core cmake xorg-dev libglu1-mesa-dev
cd ~ 
git clone https://github.com/glfw/glfw.git
cd glfw
cmake .
make
sudo make install
cd ..
git clone http://github.com/patriciogonzalezvivo/glslViewer
cd glslViewer
make
sudo make install
```

### Installing in RaspberryPi

You just need to download the code, compile and install.

```
cd ~ 
git clone http://github.com/patriciogonzalezvivo/glslViewer
cd glslViewer
make
sudo make install
```

### Installing in Mac OSX

You need to [install GLFW](http://www.glfw.org), ```pkg-config``` first and then download the code, compile and install.

```
brew update
brew upgrade
brew tap homebrew/versions
brew install glfw3 pkg-config
cd ~ 
git clone http://github.com/patriciogonzalezvivo/glslViewer
cd glslViewer
make
make install
```

If glfw3 was installed before, after running the code above, remove glfw3 and try:

```
brew install glfw3 pkg-config
export PKG_CONFIG_PATH=/usr/local/lib/pkgconfig
make
make install
```

## Use

In the most simple scenario you just want to load a fragment shader. For that you need to:

* Run the app passing the shader as an argument

```bash
cd examples
glslViewer test.frag
```

* Then edit the shader with your favorite text editor. 

```bash
vim test.frag
```

**Note**: In RaspberryPi you can avoid taking over the screen by using the ```-l``` or ```--live-coding``` flags so you can see the console. Also you can edit the shader file through ssh/sftp.

**Note**: On Linux and MacOS you may used to edit your shaders with Sublime Text 2, if thats your case you should try this [Sublime Text 2 plugin that lunch glslViewer every time you open a shader](https://packagecontrol.io/packages/glslViewer).

### Loading Vertex shaders and geometries

![](http://patriciogonzalezvivo.com/images/glslViewer-3D.gif)

You can also load both fragments and vertex shaders. Of course modifing a vertex shader makes no sense unless you load an interesting geometry. That's why ```glslViewer``` is can load ```.ply``` files. Try doing:

```bash
glslViewer bunny.frag bunny.vert bunny.ply
```

### Pre-Define ```uniforms``` and ```varyings```

* ```uniform float u_time;```: shader playback time (in seconds)

* ```uniform vec2 u_resolution;```: viewport resolution (in pixels)

* ```uniform vec2 u_mouse;```: mouse pixel coords (xy: pos, zw: buttons)

* ```varying vec2 v_texcoord```: UV of the billboard ( normalized )

### Textures

You can load PNGs and JPEGs images to a shader. They will be automatically loaded and asigned to an uniform name acording to the order they are pass as arguments: ex. ```u_tex0```, ```u_tex1```, etc. Also the resolution will be assigned to ```vec2``` uniform acording the texture uniforma name: ex. ```u_tex0Resolution```, ```u_tex1Resolution```, etc. 

```bash
glslViewer test.frag test.png
```

In case you want to assign customs names to your textures uniforms you must specify the name with a flag before the texture file. For example to pass the following uniforms ```uniform sampled2D imageExample;``` and  ```uniform vec2 imageExampleResolution;``` is defined in this way:

```bash
glslViewer shader.frag -imageExample image.png
```

### Others arguments

Beside for texture uniforms other arguments can be add to ```glslViewer```:

* ```-x [pixels]``` set the X position of the billboard on the screen

* ```-y [pixels]``` set the Y position of the billboard on the screen

* ```-w [pixels]``` or ```--width [pixels]```  set the width of the billboard

* ```-h [pixels]``` or ```--height [pixels]``` set the height of the billboard

* ```-s [seconds]``` exit app after a specific amount of seconds

* ```-o [image.png]``` save the viewport to a image file before

* ```-l``` or ```--live-coding``` to draw a 500x500 billboard on the top right corner of the screen that let you see the code and the shader at the same time:

### Inject other files

You can include other GLSL code using a traditional ```#include “file.glsl”``` macro. Note: included files are not under watch so changes will not take effect until the main file is save.

## Author

[Patricio Gonzalez Vivo](http://https://twitter.com/patriciogv): [github](https://github.com/patriciogonzalezvivo) | [twitter](http://https://twitter.com/patriciogv) | [website](http://patricio.io)

## Acknowledgements

Inspired by [Karim’s Naaki](http://karim.naaji.fr/) [fragTool](https://github.com/karimnaaji/fragtool).
