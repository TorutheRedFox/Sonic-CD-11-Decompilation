![](header.png?raw=true)
# **SUPPORT THE OFFICIAL RELEASE OF SONIC CD**
+ Without assets from the official release, this decompilation will not run.

+ You can get the official release of Sonic CD from:
  * [Windows (Via Steam)](https://store.steampowered.com/app/200940/Sonic_CD/)
  * [iOS (Via the App Store)](https://apps.apple.com/us/app/sonic-cd-classic/id454316134)
  * [Android (Via Google Play)](https://play.google.com/store/apps/details?id=com.sega.soniccd.classic&hl=en&gl=US)
  * [Android (Via Amazon)](https://www.amazon.com/Sega-of-America-Sonic-CD/dp/B008K9UZY4/ref=sr_1_2?dchild=1&keywords=Sonic+CD&qid=1607930514&sr=8-2)

Even if your platform isn't supported by the official releases, you **must** buy or officially download it for the assets (you don't need to run the official release, you just need the game assets)

# Advantages over the PC version of Sonic CD
* Sharp, pixel-perfect display.
* Controls are completely remappable via the settings.ini file.
* The window allows windows shortcuts to be used.
* Complete support for using mobile/updated scripts, allowing for features the official PC version never got to be played on PC.
* Native Windows x64 version, as well as an x86 version.

# Advantages over the Mobile versions of Sonic CD
* The rendering backend is based off the PC version by default, so palettes are fully supported (Tidal Tempest water in particular)

# Additional Tweaks
* Added a built in mod loader and API, allowing to easily create and play mods with features such as save file redirection and XML GameConfig data.
* There is now a settings.ini file that the game uses to load all settings, similar to Sonic Mania.
* Dev menu can now be accessed from anywhere by pressing the `ESC` key if enabled in the config.
* The `F12` pause, `F11` step over & fast forward debug features from Sonic Mania have all been ported and are enabled if `devMenu` is enabled in the config.
* A number of additional dev menu debug features have been added:
  * `F1` will load the first scene in the Presentation stage list (usually the title screen)
  * `F2` and `F3` will load the previous and next scene in the current stage list
  * `F5` will reload the current scene, as well as all assets and scripts
  * `F8` and `F9` will visualize touch screen and object hitboxes
  * `F10` will activate a palette overlay that shows the game's 8 internal palettes in real time
* If `useSteamDir` is set in the config, and the user is on Windows, the game will try to load savedata from Steam's `userdata` directory (where the Steam version saves to).
* Added the idle screen dimming feature from Sonic Mania Plus, as well as allowing the user to disable it or set how long it takes for the screen to dim.

# How to build
## Windows
* Clone the repo, then follow the instructions in the [depencencies readme for Windows](./dependencies/windows/dependencies.txt) to setup dependencies, then build via the visual studio solution.
* Alternatively, you can grab a prebuilt executable from the releases section.

## Windows via MSYS2 (64-bit only)
* Download the newest version of the MSYS2 installer from [here](https://www.msys2.org/) and install it.
* Run the MINGW64 prompt (from the windows Start Menu/MSYS2 64-bit/MSYS2 MinGW 64-bit), when the program starts enter `pacman -Syuu` in the prompt and hit Enter.
* Press `Y` when it asks if you want to update packages. If it asks you to close the prompt, do so, then restart it and run the same command again. This updates the packages to their latest versions.
* Install the dependencies with the following command: `pacman -S pkg-config make git mingw-w64-x86_64-gcc mingw-w64-x86_64-SDL2 mingw-w64-x86_64-libogg mingw-w64-x86_64-libvorbis mingw-w64-x86_64-libtheora mingw-w64-x86_64-glew`
* Clone the repo with the following command: `git clone --recursive https://github.com/Rubberduckycooly/Sonic-CD-11-Decompilation.git`
* Go into the repo you just cloned with `cd Sonic-CD-11-Decompilation`.
* Run `make -f Makefile.msys2 CXXFLAGS=-O2 CXX=x86_64-w64-mingw32-g++ STATIC=1 -j5`.
  * The `CXXFLAGS` option can be removed if you do not want optimizations.
  * -j switch is optional, but will make building faster by running it parallel on multiple cores (8 cores would be -j9.)

## Windows UWP (Phone, Xbox, etc.)
* Clone the repo, then follow the instructions in the [depencencies readme for Windows](./dependencies/windows/dependencies.txt) and [depencencies readme for UWP](./dependencies/windows-uwp/dependencies.txt) to setup dependencies.
* Copy your `Data.rsdk` file and `videos` folder into `RSDKv3UWP`, then build and deploy via `RSDKv3.UWP.sln`.
* You may also need to generate visual assets, to do so, open the Package.appxmanifest file in the designer, under the Visual Assets tab, select an image of your choice and click generate.

## Mac
* Clone the repo, follow the instructions in the [depencencies readme for Mac](./dependencies/mac/dependencies.txt) to setup dependencies, then build via the Xcode project.
* A Mac build of v1.3.0 by [Sappharad](https://github.com/Sappharad) can be found [here](https://github.com/Sappharad/Sonic-CD-11-Decompilation/releases/tag/1.3.0_mac).

## Linux
* To setup your build enviroment and library dependecies, run the following commands:
  * Ubuntu (Mint, Pop!\_OS, etc...): `sudo apt install build-essential git libsdl2-dev libvorbis-dev libogg-dev libtheora-dev libglew-dev`
    * If you're using Debian, add `libgbm-dev` and `libdrm-dev`.
  * Fedora Linux: `sudo dnf install g++ SDL2-devel libvorbis-devel libogg-devel libtheora-devel glew-devel`
  * Arch Linux: `sudo pacman -S base-devel git sdl2 libvorbis libogg libtheora glew`
* Clone the repo with the following command: `git clone --recursive https://github.com/Rubberduckycooly/Sonic-CD-11-Decompilation.git`
* Go into the repo you just cloned with `cd Sonic-CD-11-Decompilation`.
* Run `make CXXFLAGS=-O2 -j5`.
  * If your distro is using gcc 8.x.x, then add the argument `LIBS=-lstdc++fs`.
  * The `CXXFLAGS` option can be removed if you do not want optimizations.
  * -j switch is optional, but will make building faster by running it parallel on multiple cores (8 cores would be -j9.)
 
## iOS
* Clone the repo, follow the instructions in the [dependencies readme for iOS](./dependencies/ios/dependencies.txt) to setup dependencies, then build via the Xcode project.

## Android
* Clone the repo, then follow the instructions in the [dependencies readme for Android](./dependencies/android/dependencies.txt).
* Ensure the symbolic links in `android/app/jni` are correct. If not, fix them with the following on Windows:
  * `mklink /D src ..\..\..`
  * `mklink /D SDL ..\..\..\dependencies\android\SDL`
* Open `android/` in Android Studio, install the NDK and everything else that it asks for, and build.

## PlayStation Vita
* Ensure you have Docker installed and run the script `build.sh` from `RSDKv3.vita`. If you are on Windows, WSL2 is recommended.
  * NOTE: You would need to copy Sonic CD game data into `ux0:data/RSDKv3` to boot the game.

## Unofficial Branches
Follow the installation instructions in the readme of each branch.
* For the **Nintendo Switch**, go to [heyjoeway's fork](https://github.com/heyjoeway/Sonic-CD-11-Decompilation).
* For the **Nintendo 3DS**, go to [SaturnSH2x2's fork](https://github.com/SaturnSH2x2/Sonic-CD-11-3DS).
  * A New Nintendo 3DS is required for the game to run smoothly.
  
Because these branches are unofficial, we can't provide support for them and they may not be up-to-date.

## Other Platforms
Currently the only supported platforms are the ones listed above, however the backend uses libogg, libvorbis, libtheora & SDL2 to power it (as well as tinyxml2 for the mod API), so the codebase is very multiplatform.
If you're able to, you can clone this repo and port it to a platform not on the list.

# FAQ
### Q: Why don't some buttons in the menu work?
A: Buttons like leaderboards & achievements require code to be added to support online functionality & menus (though they are saved anyways), and other buttons like the controls button on PC or privacy button on mobile have no game code and are instead hardcoded through callback. I just didn't feel like going through the effort to decompile all that, since it's not really worth it.

### Q: Is the titlecard text slightly offset when using a PC datafile?
A: Unfortunately, it's an error with the scripts. If you wanna go into `TitleCards/R[X]\_TitleCard.txt` and fix it, be my guest, but the best fix is to set `screenWidth` to 400, instead of 424 in the settings.ini file to match the PC version's resolution.

### Q: There's a weird spot on the title screen, how do I fix it?
A: See above.

### Q: The screen is tearing, how do I fix it?
A: Try turning on VSync in settings.ini.

### Q: I found a bug!
A: Submit an issue in the issues tab and we _might_ fix it in the master branch. Don't expect any future releases, however.

### Q: Will you do a decompilation for Sonic 1/Sonic 2?
A: I already have! You can find it [here](https://github.com/Rubberduckycooly/Sonic-1-2-2013-Decompilation).

### Q: Will you do a decompilation for Sonic Mania?
A: No. Sonic Mania is much bigger and requires that I'd decompile not only how the (far more complex) RSDKv5 works, but also all _600+_ objects work.

# Special Thanks
* [Xeeynamo](https://github.com/Xeeynamo): for creating the RSDK Animation editor & an early version of the script unpacker, both of which got me into RSDK modding.
* [Sappharad](https://github.com/Sappharad): for making a decompilation of the Windows Phone 7 version of Sonic CD (found [here](https://github.com/Sappharad/rvm_soniccd)) which gave me the idea & motivation to decompile the PC/iOS/Android versions.
* [SuperSonic16](https://github.com/TheSuperSonic16): for creating & adding some stuff to the Sonic CD mod loader that I asked for.
* The Weigman for creating the header you see up here along with similar assets.
* Everyone in the [Retro Engine Modding Server](https://dc.railgun.works/retroengine): for being supportive of me and for giving me a place to show off these things that I've found.

# Contact:
Join the [Retro Engine Modding Discord Server](https://dc.railgun.works/retroengine) for any extra questions you may need to know about the decompilation or modding it.
