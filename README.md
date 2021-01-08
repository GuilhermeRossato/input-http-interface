# Mouse and Keyboard control via HTTP [Unfinished]

This repository is a project for building a simple C/C++ program to manipulate input (keyboard and mouse) via the HTTP requests.

The program exposes a HTTP server in a specified port (default 8082) to allow for any program (e.g. a Web Browser) to send mouse and keyboard changes to your computer.

It was developed to work on Windows and does not support other operational systems as of now.

## How to use

Download a release from the [releases page](https://github.com/GuilhermeRossato/input-http-interface/releases) (an executable) and run it. It should open a server at port `8082` by default (check standard output), use a browser to access http://localhost:8082/ and you should get a menu to allow you to explore the functionalities of this tool like this:

![Menu Screen](https://raw.githubusercontent.com/GuilhermeRossato/input-http-interface/master/demo.png)

Check the standard and error output to check for errors if anything went wrong.

## Feature examples

To request the menu and list of options, access root:

`GET` http://localhost:8082/

To get the current mouse position in plain text (two integers, x and y, separated by a comma):

`GET` http://localhost:8082/mouse/pos/

To move the mouse to the right by 100 pixels instantly:

`POST` http://localhost:8082/mouse/move/?dx=100

To move the mouse to a specific position slowly (like a human would):

`POST` http://localhost:8082/mouse/move/?x=100&y=100&speed=3

To get the screen size (to know the limits of the mouse) in JSON format:

`GET` http://localhost:8082/screen-size/?json

To get the state of the left mouse button in a digit (text) format (0 or 1, where 1 means it is pressed):

`GET` http://localhost:8082/mouse/get/left/

To get the state of the all mouse buttons in a JSON format:

`GET` http://localhost:8082/mouse/get/?json

To request a left press at the current mouse position for the default duration of 0.1s:

**Unimplemented** `POST` http://localhost:8082/mouse/press/left/

To set the right mouse button down and keep it down (until you or the user requests it to go up):

**Unimplemented** `POST` http://localhost:8082/mouse/set/right/?down

To request a middle mouse button press at the current mouse position and keep it down for 1.5 seconds

**Unimplemented** `POST` http://localhost:8082/mouse/press/middle/?time=1.5

To check if the right arrow key is pressed down in JSON format:

**Unimplemented** `GET` http://localhost:8082/keyboard/get/VK_RIGHT?json

To set the ESC key as pressed down:

**Unimplemented** `POST` http://localhost:8082/keyboard/set/VK_ESCAPE?down

To set the ESC key as pressed up:

**Unimplemented** `POST` http://localhost:8082/keyboard/set/VK_ESCAPE?up

To press a key and keep it down for one second and a half:

**Unimplemented** `POST` http://localhost:8082/keyboard/press/VK_VOLUME_MUTE?time=1.5

To press a key by hexadecimal code (in this case the `B` key in the keyboard) for the default time of a tenth of second:

**Unimplemented** `POST` http://localhost:8082/keyboard/press/0x42

Obs: The key codes are called "Virtual-Key Codes" and should be defined at a lookup table in `./src/keycodes.cpp`. You may also check them in the [official docs](https://docs.microsoft.com/en-us/windows/win32/inputdev/virtual-key-codes) for win32 by Microsoft.

To write a text at a 100 characters-per-minute (default speed), POST a body content to:

**Unimplemented** `POST` http://localhost:8082/keyboard/type/?cpm=100

Don't forget the body when writing or you'll get an error.

## Why

I frequently need to use other software in other languages like NodeJS, Python, or even C++ to control my keyboard or mouse for automation purposes and other random experiments.

It seems that every language has their own "module" or "library" or "namespace" to send keyboard presses and button clicks. Some languages don't allow for middle button clicks, some don't move the mouse by delta position, some don't allow for full keyboard control, some have bugs, some have to update every two weeks, etc.

I needed something that is predictable, does not update, and can be used by any other tool via a common interface.

## Security

Do not leave this running on your computer unattended. A connected computer with access to your network can access the interface and send all sort of keyboard commands like "open command prompt > download virus > execute virus"

## Disclaimer

The project is unfinished, I do not make any warranty about the working state of the software included in this repository. I also shall not be responsible for any harm the use of the software might cause.
