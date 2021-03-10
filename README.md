# Installing SDL
Since a lot of my projects use SDL at this point, I thought I'd write a small guide on how to install SDL for use with Visual Studio. There are plenty of guides online, but I'm doing it in a slightly different way that I find pretty useful. There are a few key steps, and I'll go through all of them in this readme.

## Downloading SDL
First, you have to download SDL. I recommend getting the development library from [here](https://www.libsdl.org/download-2.0.php). Optionally, you can also install [SDL_image](https://www.libsdl.org/projects/SDL_image/), [SDL_mixer](https://www.libsdl.org/projects/SDL_mixer/), or [SDL_net](https://www.libsdl.org/projects/SDL_net/). Once you've downloaded SDL or a library, extract your download and place it somewhere on your computer that you will remember (for example, D:\SDL).

## Adding an environment variable
This step is quite simple, but also very important for the installation. Adding environment variables for SDL and/or SDL libraries can cut down a lot of hassle in downloading projects with SDL or making new ones.

First, navigate to the environment variables window in your settings. You can do this by searching "edit environment variables" on your taskbar, and opening "edit environment variables for your account". Press the button labelled "Environment Variables" in the window that pops up, and you should something that looks like this:

![Incomplete variables](https://user-images.githubusercontent.com/50138952/110579760-87ac1000-81bb-11eb-90ee-e51c858069e7.png)

Next, press "New..." and enter the name of the library, and it's full path.
In terms of naming, I call my variables SDL, SDL_image, SDL_mixer, and SDL_net.

![New variable](https://user-images.githubusercontent.com/50138952/110579801-95619580-81bb-11eb-87a4-b950779fa181.png)

When you are finished, your variables may look something like this:

![Complete variables](https://user-images.githubusercontent.com/50138952/110579721-77943080-81bb-11eb-8268-14e25719272d.png)

## Using VS projects with SDL linked
If you simply want to use a project that has SDL linked, you can stop after the installation. As long as SDL is linked using environment variables and you have set them up, you should be fine.

## Linking SDL for VS projects
If you are creating a new VS project you will have to link SDL. Linking is largely the same as other instructions, but one key difference is the use of environment variables. Other guides will likely tell you to directly type out a library directory to link its resources, and while this is fine for working on your own others may not have their libraries at same location. This can, unfortunately, prevent others from compiling your work.

When linking, you should instead make use of your environment variables. In the place of "C:\mylibraries\SDL\lib\x86\\", for example, you can instead write "$(SDL)\lib\x86\\". This is not only shorter, but it will work for anybody who has set an SDL environment variable. Because your libraries will be where the environment variables refer to, you ***do not*** have to copy them to your project directory.

Keeping variables in mind, I would recommend following [this guide](https://thenumbat.github.io/cpp-course/sdl2/01/vsSetup.html) to link the resources to your project.

## Creating a standalone executable
When compiling with VS under these conditions, your executable can run because the necessary dlls needed to run are included in the debug environment (the guide linked under "Linking SDL for VS projects" covers how to change your debug environment). If you want to use your executable outside of that environment, however, you must copy the necessary dlls from your libraries to your executable's directory.

You can do this by hand easily by simply navigating to your library, into lib, and then into your platform. You will always need SDL2.dll, and you may need additional ones to suit your libraries (such as SDL2_image.dll for SDL_image). If you want to copy on every build, you can set dlls to be copied by Visual Studio. To use environment variables for the path, however, you will need to modify the .sln file directly (with notepad, for example).
