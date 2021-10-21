# SDL and Make Setup
[View as a Web Page](https://www.michaelrryan.com/SDL2-Make-Gameloop) • [View as Markdown](https://github.com/MichaelRRyan/SDL2-Make-Gameloop)

### 1. Download and install VS code:
> https://code.visualstudio.com/Download

### 2. Install the C/C++ extension in VS code 
> ```ctrl + shift + x``` search for ```@ext:ms-vscode.cpptools``` or ```C/C++ IntelliSense, debugging, and code browsing```. Install this plugin.

### 3. Install MSYS2 (following steps taken from the bottom of Phil's notes):
> 1. Download Msys from https://www.msys2.org/
>
> ***NOTE Msys is a helpful installer that uses a package manager called 'pacman'. Pacman is used in Arch Linux for package management.***
> 
> 2. Run the installer and go through the step by step process. This tutorial uses the install location of the root of the C: drive. If you use a different location you'll have to modify some paths.
> 2. Once the install finishes, run the "MSYS2 MSYS" terminal.
> 3. Update the package database and base packages type ```pacman -Syu```.
> 4. Run "MSYS2 MSYS" and update the rest of the base packages with ```pacman -Su```.
> 5. Open "MSYS2 MSYS" terminal and type ```pacman -S mingw-w64-x86_64-gcc``` to install gcc / g++.
> 6. To install GDB Open "MSYS2 MSYS" terminal and type ```pacman -S mingw-w64-x86_64-gdb```.
> 7. Open "MSYS 64" and type ```g++ --version``` to check g++ is installed. Type ```gdb --version``` to check that gdb is installed.
> 8. Modify system path to include path to mingw64: ```C:\msys64\mingw64\bin```.
> 9. Open up a command prompt and type ```g++ --version``` to check g++ is installed. Type ```gdb --version``` to check that gdb is installed globally.

### 4. Download SDL
> Open a "MSYS2 MSYS" terminal and install the necessary SDL packages with the following command:  
> ```pacman -S mingw64/mingw-w64-x86_64-SDL2 mingw64/mingw-w64-x86_64-SDL2_mixer mingw64/mingw-w64-x86_64-SDL2_image mingw64/mingw-w64-x86_64-SDL2_ttf```

### 5. Install Make
> Open a "MSYS2 MSYS" terminal and run ```pacman -S make``` to install make.

### 6. Download project files and build (This is a placeholder for more detailed instructions on creating the project)
> 1. Clone down [this repo](https://github.com/MichaelRRyan/SDL2-Make-Gameloop).
> 2. Open MSYS2 and navigate into the repo's folder with ```cd [folder location]``` (where [folder location] is your actual project folder path).
> 3. Type ```make``` and hit enter.
>
> The project should build the executable to a "bin" folder in the repo's folder. Run this file to make sure it works, it should print out messages about updating and such.

### OPTIONAL 7. Install SFML & Modify Make File
> If you're like me and coming from an SFML background, it could be handy to have this package installed too. Having this package will allow you to build SFML projects the same way you would SDL projects.
> 1. Open a "MSYS2 MSYS" terminal and run ```pacman -S mingw-w64-x86_64-sfml``` to install SFML.
> 2. I've yet to figure out how to include SFML in the SDL make file without causing errors, so instead we'll replace the SDL includes.  
> In the make file, delete line 3 and modify what used to be lines 4 and 6 to the following:  
> ```
> 1. CXX			:= g++
> 2. 
> 3. SFML_LDFLAGS := -lsfml-graphics -lsfml-window -lsfml-system
> 4. 
> 5. CXXFLAGS 	:= -I. -I./include ${SFML_LDFLAGS}
> 6. 
> 7. MSG_START	:= "Build Started"  
> ...  
> ```  
> You'll have to test this with a different project that actually uses SFML, and remember this file expects a "include" and "src" folder structure.
