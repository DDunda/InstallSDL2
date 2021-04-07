# Installing SDL Portably
Portability is important; linking a project so it can work on other computers lets others compile your work, and contribute to your project. Unfortunately, most online tutorials for installing SDL are *not* portable! Due to this, here is small guide on how to portably install SDL2. It should be generic enough to work with most linking schemes, however linking in this particular guide is demonstrated with Visual Studio.

## Downloading SDL
First, you have to download SDL. I recommend getting the development library from [here](https://www.libsdl.org/download-2.0.php). Optionally, you can also install [SDL_image](https://www.libsdl.org/projects/SDL_image/), [SDL_mixer](https://www.libsdl.org/projects/SDL_mixer/), or [SDL_net](https://www.libsdl.org/projects/SDL_net/). Once downloaded, extract the library/libraries to somewhere on your computer that you will remember (for example, D:\SDL).

## Adding an environment variable
This step is key for portability! Adding environment variables for SDL and/or SDL libraries allows you to bypass hardcoding library directories, or resorting to relative paths.

First, navigate to the environment variables window in your Windows settings. You can do this by searching "edit environment variables" in your taskbar searchbox, and opening "Edit environment variables for your account":

![Opening the window](https://user-images.githubusercontent.com/50138952/113849425-d1007700-97dc-11eb-9b15-d163678c4ebc.png)

Press the button labelled "Environment Variables" in the window that pops up, and you should something that looks like this:

![Incomplete variables](https://user-images.githubusercontent.com/50138952/110579760-87ac1000-81bb-11eb-90ee-e51c858069e7.png)

For each of your lirbaries, press "New..." and enter the name of the library, and it's full path.
(In terms of naming, I call my variables SDL, SDL_image, SDL_mixer, and SDL_net)

![New variable](https://user-images.githubusercontent.com/50138952/110579801-95619580-81bb-11eb-87a4-b950779fa181.png)

When you are finished, your variables may look something like this:

![Complete variables](https://user-images.githubusercontent.com/50138952/110579721-77943080-81bb-11eb-8268-14e25719272d.png)

## Using portably linked SDL projects
If you simply want to use a project that has SDL linked in this way, you can stop after the installation. As long as you set up your environment variables and the project follows this approach, you should be fine!

## Linking SDL yourself
If you are creating a new VS project you will have to link SDL. Linking is largely the same as other instructions, but one key difference is the use of environment variables. Other guides will usually to instruct you to type out a library directory to link it, and while this is fine for working on your own others may not have their libraries at same location! Unfortunately, this can prevent others from compiling your work.

When linking, you should instead make use of your environment variables. In the place of "C:\mylibraries\SDL\lib\x86\\", for example, you can instead write "$(SDL)\lib\x86\\" (in Visual Studio). This is not only shorter, but it will work for anybody who has set their SDL environment variable. Because your libraries will be where the environment variables refer to, you ***do not*** have to copy them to your project directory.

With variables in mind, I would recommend following [this guide](https://thenumbat.github.io/cpp-course/sdl2/01/vsSetup.html) to link your project.

## Creating an executable for release
When compiling in the way used by the guide under "Linking SDL yourself", an executable can run because the necessary dlls needed to run are included in the debug environment. To use an executable outside of that environment, however, ALL necessary dlls (SDL2.dll + additional dlls (i.e. SDL2_image.dll)) must be copied to the executable's directory.

To copy on every build in Visual Studio, Post-Build Events can be used to automatically copy dlls like so: (this example copies from SDL, SDL_image, and SDL_mixer)

![Set your Post-Build Event in Properties>Configuration Properties>Build Events>Post-Build Event>Command Line](https://user-images.githubusercontent.com/50138952/113514420-cca44600-95b1-11eb-9afc-b60de95b2fdd.png)

(Here's the command so you can copy it: `copy "$(SDL)\lib\$(PlatformShortName)\*.dll" "$(OutDir)"&copy "$(SDL_image)\lib\$(PlatformShortName)\*.dll" "$(OutDir)"&copy "$(SDL_mixer)\lib\$(PlatformShortName)\*.dll" "$(OutDir)"`)
